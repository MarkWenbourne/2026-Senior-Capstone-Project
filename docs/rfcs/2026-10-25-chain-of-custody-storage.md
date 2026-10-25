# RFC: Chain-of-Custody Record Storage for Hazard Track

| Field | Value |
| --- | --- |
| Author | Mark Wenbourne |
| Date | 2026-10-25 |
| Status | Proposed |
| Decision Date | TBD |
| Deciders | TBD — team and project partner, as appropriate |
| Superseded By | N/A |

## Problem and Context

Hazard Track is being expanded to support radioactive-waste pickup requests, container identification and lifecycle tracking, and cost analysis. One requirement is a chain-of-custody history for hazardous and radioactive waste containers. EH&S staff need to know a container's current status and be able to reconstruct how it moved through stages such as issued, filled, picked up, processed, stored, and shipped. A status shown on a dashboard is useful, but it does not by itself answer who changed that status, when, or why.

The team must decide how the application will store current container state and historical transitions. This decision affects the database schema, application update logic, reporting, and the reliability of later investigations. Once real records accumulate, changing the storage model may require migrations, backfilling missing history, and changing code that reads or writes container data. Information never recorded cannot reliably be reconstructed later.

The team has not yet received last year's Hazard Track codebase because IT has been working on an issue with it. A meeting to provide access is expected soon. We therefore do not know the inherited database technology, whether custody events are already recorded, or what integrations depend on existing tables. We should frame a preferred approach now, but not commit to a migration until we inspect the system and confirm operational requirements with the project partner.

If the team does nothing, it may be possible to continue with the inherited tracking design temporarily. That could be the least disruptive choice if the existing system already preserves a sufficient custody history. If it does not, however, implementing new status changes without a history plan could produce records that are incomplete for audits and incident reconstruction. This RFC is intended to guide a decision before those workflows are built.

## Options

### Option A: Current-State Storage Only

Maintain one current record per container, with fields such as status, location, and last-updated timestamp. Each transition overwrites those fields. This is straightforward to query and likely requires minimal new storage and application logic. It could be appropriate if an existing, independently verified audit mechanism already captures all required custody details, or if the feature is only a short-lived prototype using sample data.

The cost is lost history if no separate audit mechanism exists. A row showing `Stored` cannot by itself explain when a container was picked up, which user handled it, or whether an unexpected transition occurred. Adding history later would not recover past transitions that were never recorded. Therefore, current-state-only storage is not sufficient as a final design unless another system supplies reliable custody records.

### Option B: Append-Only Events as the Source of Truth

Write a new event for each container transition, including the container identifier, event type, previous and new state, actor, timestamp, and relevant location or notes. Determine current status from the event sequence or a derived projection. This resembles event sourcing: changes are represented as events, allowing a past state to be reconstructed from recorded changes [1]. It is attractive when detailed histories, replay, and multiple downstream views are central requirements.

The costs are greater design and operational complexity. The team must handle event ordering, concurrency, duplicate requests, corrections, projection rebuilding, and schema evolution. Reading current state may require a maintained projection for acceptable performance. This option would be appropriate if the inherited architecture already uses event sourcing, or if several consumers must reliably derive different views from the same event stream.

### Option C: Hybrid Current State and Append-Only History

Keep a current-state container record for efficient operational queries and a separate history table containing every meaningful custody transition. On a successful transition, the application updates the current record and inserts one history entry in a single database transaction. The history records the actor, timestamp, old and new status, and relevant custody details. The current-state table supports dashboards; the history supports audit review and incident reconstruction.

This approach offers simpler current-state queries than replaying an event stream, while retaining an explicit history. Its main cost is maintaining consistency between two representations. A partial write could leave the current status without a matching event, or vice versa, unless transaction boundaries and error handling are correct. This option is appropriate if the existing database supports transactions and the team needs both fast current-state lookup and reliable historical records without adopting full event sourcing.

### Option D: Do Nothing for Now

Leave the inherited storage model unchanged while the team obtains the codebase, inventories its behavior, and asks the project partner what records are required. This avoids an unnecessary redesign if the existing implementation already meets the requirements. It also preserves time for inspecting dependencies before changing data structures.

The cost arrives when new container-tracking features are implemented without a confirmed history strategy: missing fields, inconsistent transition logic, or records that cannot be reconstructed later. Do nothing is reasonable **only as a time-boxed discovery step**, not as an indefinite substitute for a decision. The team should revisit it immediately after gaining code access and completing an initial schema and workflow review.

## Analysis

**Performance.** Option A provides direct current-state lookups with few writes. Option B can retain rich event histories but may need projections to avoid rebuilding current state from many events; event-sourcing literature identifies derived state as a common implementation concern [1]. Option C adds a history insert to each status change but preserves direct queries for current status. For Hazard Track, the number of containers, update frequency, and dashboard latency targets are not yet known, so no option can honestly be declared fastest in practice. A representative prototype should measure update latency and current-status and history-query response times before a final commitment.

**Complexity and maintainability.** Option A is simplest initially, but only if custody history is provided elsewhere. Option B requires event semantics, ordering, projections, and correction policies that may be excessive for this expansion. Option C uses familiar relational patterns but demands careful transaction design. Database transactions can group related changes so they succeed or fail together, a useful property for synchronizing status and history [2]. The inherited stack may alter this comparison: an existing event-based implementation would make Option B less costly, while an established relational schema may favor Option C.

**Security and auditability.** Audit records should support accountability and be protected against unauthorized access or modification. NIST's log-management guidance discusses protecting, reviewing, and retaining log data as part of a sound logging program [3]. Option A alone cannot provide a complete history of transitions. Options B and C can preserve such history, but an `append-only` application convention does not make data tamper-proof. The team must still define permissions, correction procedures, backups, retention, and access to sensitive operational information. Whether specific regulatory recordkeeping requirements apply must be confirmed with Radiation Safety and the project partner; this RFC does not claim that any storage design alone establishes ORDEQ, OHA, or NRC compliance.

**Cost and change risk.** Option A uses the least additional storage but risks costly retrofitting if history becomes mandatory after deployment. Option B may require more infrastructure or engineering effort, especially if the current system is not event-based. Option C duplicates some state but likely has manageable storage requirements for a campus-scale workflow; this is a hypothesis, not a measured fact. Option D avoids immediate changes but risks delaying dependent work. The greatest unknown is compatibility with the codebase still held by IT. That uncertainty is a reason to defer irreversible migration, not a reason to ignore the decision.

**Provisional assessment.** Option C best fits the stated need for a live dashboard plus historical custody records, assuming a transactional database and no adequate inherited history system. Option B becomes more attractive if the existing application is event-driven. Option D is appropriate for the short interval before inspection. Option A is acceptable only if another verified component already provides the required audit trail.

## Recommendation and Verification Plan

I recommend **Option C: Hybrid Current State and Append-Only History**, provisionally. The team should **not** merge a database migration on the strength of this RFC alone. First, inspect the inherited codebase and demonstrate that the chosen model fits its storage technology and existing workflows. If the current application already records trustworthy custody events, extending that mechanism should take precedence over building a duplicate one.

The following checks are proposed acceptance criteria, **not tests that have already passed**:

1. **Schema and requirements review (before implementation):** Identify existing container tables, history mechanisms, and dependencies; confirm required event fields and retention expectations with the project partner.
2. **Atomic transition test (prototype):** For every successful status change, verify that exactly one matching history entry is committed. Force a failure during the operation and confirm that neither the current-state change nor the history insert remains partially committed.
3. **Lifecycle validation (prototype):** Test valid transitions through the agreed stages and reject invalid or unauthorized transitions without creating misleading history.
4. **Concurrency and duplication tests (before merge):** Simulate simultaneous updates and retried requests; verify that the resulting state and history are consistent and do not contain unintended duplicate transitions.
5. **Audit retrieval test (before merge):** Given representative sample records, retrieve a container's ordered history with actor, time, status changes, and location details; compare it against the known test sequence.
6. **Performance check (before acceptance):** Measure status lookup, history retrieval, and update latency using representative data volumes. Agree on acceptable thresholds with the team and partner rather than inventing them in advance.
7. **Migration and recovery rehearsal (before deployment):** Test any schema migration on a disposable database copy, confirm backups can be restored, and document how deployment would be stopped or recovered if validation fails.

The decision can be accepted when the team has reviewed the existing implementation, the partner has confirmed the record requirements, and a prototype satisfies the relevant acceptance criteria. A reviewer should be able to inspect the test evidence and the resulting sample history.

## Constraints

**Existing architecture and schedule:** The expansion must fit the inherited Hazard Track application where practical. Codebase access is pending, so database-specific migrations and commitments should wait for inspection.

**Licensing and intellectual property:** The team must respect the inherited application's license terms, third-party dependencies, and ownership boundaries. No new database service or library should be assumed approved before those constraints are checked.

**Data use and confidentiality:** Waste records may contain operational details, user identities, and location information. Prototypes should use synthetic or partner-approved data. Access to real records, retention periods, and sharing of implementation details must follow partner and university requirements. The team should not put confidential datasets or credentials in the public repository.

**Compliance:** The project identifies ORDEQ, OHA, and NRC considerations, but applicable obligations and retention periods have not yet been verified. The partner and Radiation Safety personnel must validate these requirements before the schema is finalized.

## Delegation and Validation

I used ChatGPT to help organize the RFC, compare possible storage architectures, and draft explanatory text and proposed verification criteria. This assistance was for analysis and writing, **not** for inspecting the unavailable Hazard Track codebase, implementing a prototype, or executing tests.

At the time of this draft, the team has a GitHub repository but has not received the inherited application code. I therefore cannot claim that automated tests, required CI checks, staging, branch protections, or a tested rollback procedure currently guard this design. Those are proposed controls to verify or establish once the repository's actual state and technology stack are known. The team's planning documents and safety-net audit do not by themselves prove that those controls are enforced.

Before recommending acceptance, I will personally compare the proposal against the inherited schema and application workflows, check that cited sources support the claims made here, and review the prototype's transaction-failure and history-retrieval results. I will also seek teammate and project-partner feedback on whether the recorded fields are sufficient for real custody investigations. These checkpoints matter because missing history may be impossible to reconstruct after real containers have been processed.

## Decision

**Proposed.** No storage architecture has been accepted through this RFC. The team should review the options after codebase access and record the chosen option, decision date, deciders, and decision chair here. If the RFC is later replaced, update the header and link the superseding record.