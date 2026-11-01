**Note:** Everything here is **loosely** put together due to the lack of code, with some requirements expected to change in priority, and non-goals being added/removed.  
# Hazard Track — Requirements

**Project:** Hazard Track: Radioactive Waste, Container Tracking, and Cost Analysis Expansion  
**Team:** Mark Wenbourne, Noah Gregie, Addison Howard, Eduardo Juchem Balzan  
**Status:** Draft — Pending Codebase Review and Partner Validation  
**Last Updated:** 2026-10-31

## 1. Problem Statement

Oregon State University's Environmental Health and Safety (EH&S) staff and waste generators need reliable ways to request radioactive-waste pickups, identify and track waste containers, and understand waste management costs. The Hazard Track expansion is intended to address these needs by adding radioactive-waste request workflows, container lifecycle and chain-of-custody tracking, and cost reporting capabilities to the existing application. These needs are identified in the capstone project description and initial team planning; the team has not yet independently verified the existing workflows or established baseline performance measurements. The goal is to improve record accuracy, operational visibility, and reporting while supporting applicable safety and compliance requirements.

## 2. Requirements Status and Prioritization

This document describes the intended expansion of Hazard Track. It does not claim that the listed features are already implemented.

Requirements are prioritized using the MoSCoW method:

- **Must:** Essential to the intended functionality of the expansion.
- **Should:** Important to the project's goals but potentially deliverable after the core workflows.
- **Could:** Beneficial functionality that may be deferred if resources are limited.
- **Won't:** Outside the current planned scope.

Priorities describe the importance of functionality, not the order of implementation. Implementation order will be tracked on the team's GitHub Project Board.

Requirements also have a validation status:

- **Project Scope:** Identified in the provided project description, but detailed behavior still requires partner validation.
- **Assumed:** Proposed by the team and not yet confirmed by the project partner.
- **Confirmed:** Explicitly validated by the project partner or an appropriate user.

No requirement is currently marked Confirmed because formal validation of the detailed requirements has not yet been documented.

Acceptance criteria describe expected behavior. Automated tests will be associated with completed functional requirements when the inherited codebase and testing framework are available.

## 3. Functional Requirements

### 3.1 Radioactive Waste Pickup Requests

#### FR-01: Submit Radioactive Waste Requests

**Priority:** Must — Request submission is the foundation of the radioactive-waste pickup workflow.  
**Status:** Project Scope

The system shall allow authorized users to submit radioactive-waste pickup requests.

**Acceptance Criteria:**
- Given a completed request containing all required information, submission succeeds and creates a retrievable request record.
- Given a request missing required information, submission is rejected with an explanation.
- A submitted request can be retrieved using its assigned identifier.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-02: Capture Radioactive Waste Information

**Priority:** Must — Waste information is necessary for safe handling and processing.  
**Status:** Project Scope

The system shall collect isotope, activity, waste form, container type, and shielding information for radioactive-waste requests.

**Acceptance Criteria:**
- A request provides fields for all five specified categories.
- A request missing a required field cannot be submitted.
- Retrieved request records preserve the submitted values.
- Required units and valid input ranges are confirmed with the project partner.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-03: Generate Radioactive Waste Labels

**Priority:** Must — Accurate labels support identification and handling of radioactive waste.  
**Status:** Project Scope

The system shall generate radioactive-waste labels containing the RAM symbol, isotope, activity, date, generator, and container identifier.

**Acceptance Criteria:**
- Generated labels contain all six required elements.
- Label information matches the associated waste record.
- A label can be displayed in a printable format.
- Label formatting is reviewed against partner-approved requirements.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-04: Route Pickup Requests

**Priority:** Must — Pickup location determines the appropriate handling workflow.  
**Status:** Project Scope

The system shall distinguish between on-campus and remote-site radioactive-waste pickup requests.

**Acceptance Criteria:**
- Users can specify whether a pickup is on-campus or remote.
- Saved requests retain their location classification.
- Requests are assigned to the corresponding partner-approved workflow.
- The routing rules for each location category are documented before implementation.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-05: Radiation Safety Inventory Integration

**Priority:** Should — Integration reduces duplicated records and improves coordination with Radiation Safety.  
**Status:** Project Scope

The system shall support associating radioactive-waste requests with relevant Radiation Safety inventory information.

**Acceptance Criteria:**
- A radioactive-waste request can be associated with an appropriate inventory record.
- The association is preserved when the request is retrieved.
- Invalid or unavailable inventory references are handled without corrupting the request.
- The integration mechanism is approved by the project partner.

**CI Test:** TBD — Pending integration requirements.

#### FR-05A: Decay-in-Storage Handling

**Priority:** Must — Applicable radioactive-waste handling rules must be respected.  
**Status:** Project Scope

The system shall support partner-approved decay-in-storage rules for applicable radioactive waste.

**Acceptance Criteria:**
- Applicable waste records can be identified for decay-in-storage handling.
- The system applies the rules supplied or approved by Radiation Safety.
- Waste that does not meet the approved release or processing conditions is not incorrectly marked eligible.
- Rule behavior is verified using partner-approved test cases.

**CI Test:** TBD — Pending regulatory and partner clarification.

### 3.2 Internal Labeling and Container Tracking

#### FR-06: Unique Container Identification

**Priority:** Must — Every container must be distinguishable for tracking and recordkeeping.  
**Status:** Project Scope

The system shall assign each registered container a unique identifier that can be represented using a QR code or barcode.

**Acceptance Criteria:**
- Registering two different containers produces two different identifiers.
- Attempting to register a duplicate identifier is rejected.
- Entering or scanning an existing identifier retrieves the corresponding container.
- Entering an unknown identifier does not return an unrelated container.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-07: Container Lifecycle Tracking

**Priority:** Must — Lifecycle tracking is a central objective of the expansion.  
**Status:** Project Scope

The system shall track containers through applicable lifecycle stages, including issued, filled, picked up, processed, stored, and shipped.

**Acceptance Criteria:**
- Each container has a retrievable current lifecycle status.
- Authorized users can update a container's status.
- Valid status changes are saved successfully.
- Invalid status transitions are rejected.
- Allowed transitions are documented and approved by the project partner before implementation.

**CI Test:** TBD — Pending codebase access and lifecycle validation.

#### FR-08: Container Status Dashboard

**Priority:** Must — EH&S staff need visibility into current container information.  
**Status:** Project Scope

The system shall provide authorized EH&S staff with a dashboard displaying current container statuses.

**Acceptance Criteria:**
- The dashboard displays registered containers and their current statuses.
- A container can be located using its identifier.
- A successfully saved status change is reflected when the dashboard data is refreshed.
- Users without appropriate permissions cannot access restricted information.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-09: Multiple Waste Type Support

**Priority:** Must — The expansion must support both hazardous and radioactive waste workflows.  
**Status:** Project Scope

The system shall support tracking containers associated with hazardous waste and radioactive waste.

**Acceptance Criteria:**
- Containers can be associated with the appropriate waste category.
- Category-specific information is preserved.
- Retrieving a container returns its correct waste category.
- Category-specific workflows follow partner-approved rules.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-10: Chain-of-Custody Records

**Priority:** Must — Historical records are necessary for traceability and audit support.  
**Status:** Project Scope

The system shall maintain a retrievable history of container handling and status changes.

**Acceptance Criteria:**
- A successful tracked action produces a historical record.
- Each record identifies the container, action, timestamp, and responsible user.
- Updating a container's current status does not erase earlier history.
- Authorized users can retrieve the recorded history of a container.
- Unauthorized users cannot alter historical records outside approved correction procedures.

**CI Test:** TBD — Pending codebase access and storage design.

### 3.3 Cost Tracking and Analysis

#### FR-11: Vendor Disposal Cost Tracking

**Priority:** Must — Vendor disposal expenses are essential to the cost analysis expansion.  
**Status:** Project Scope

The system shall record vendor disposal costs associated with waste records, including applicable weight, container, and waste category information.

**Acceptance Criteria:**
- Authorized users can enter a vendor disposal cost.
- Costs can be associated with the appropriate waste record.
- Retrieved cost records preserve their amounts and associations.
- Invalid cost inputs, such as negative amounts where not permitted, are rejected.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-12: Internal Labor Cost Tracking

**Priority:** Should — Internal labor costs provide a more complete picture of waste management expenses.  
**Status:** Project Scope

The system shall support recording labor time and calculating internal handling costs using approved rates.

**Acceptance Criteria:**
- Authorized users can record labor time associated with waste handling.
- The system calculates cost using the approved labor rate and recorded time.
- Calculated results match independently verified sample calculations.
- The calculation method and rate source are documented.

**CI Test:** TBD — Pending cost model validation.

#### FR-13: Cost Trend Analysis

**Priority:** Must — Analyzing disposal expenses is a central project objective.  
**Status:** Project Scope

The system shall provide cost summaries grouped by department, waste type, and fiscal quarter.

**Acceptance Criteria:**
- Users can select a supported grouping.
- Cost totals match the underlying records in a representative test dataset.
- Records outside the selected reporting period are excluded.
- Empty reporting periods are handled without displaying misleading totals.

**CI Test:** TBD — Pending codebase access and test framework selection.

#### FR-14: Cost Forecasting

**Priority:** Should — Forecasting supports future budget planning but depends on reliable historical cost data.  
**Status:** Project Scope

The system shall support forecasting future waste management costs using available historical data.

**Acceptance Criteria:**
- Authorized users can request a forecast for a supported reporting period.
- Forecast calculations follow a documented method.
- Results identify the reporting period and assumptions used.
- Insufficient historical data is handled explicitly rather than presented as a reliable forecast.

**CI Test:** TBD — Pending forecasting method approval.

#### FR-15: Exportable Reports

**Priority:** Must — Exported reports support leadership review, annual summaries, and audit preparation.  
**Status:** Project Scope

The system shall allow authorized users to export waste management and cost reports.

**Acceptance Criteria:**
- Users can export a report using a partner-approved format.
- Exported records match the selected report filters.
- Report totals match the underlying data.
- Users without appropriate permissions cannot export restricted information.

**CI Test:** TBD — Pending report format confirmation and test framework selection.

## 4. Non-Functional Requirements

The numerical thresholds below are proposed acceptance targets, not existing performance measurements or partner-approved commitments.

### NFR-01: Data Integrity

**Priority:** Must — Incorrect waste and container records could undermine safety and auditability.  
**Status:** Assumed

The system shall preserve record consistency during normal and failed operations.

**Proposed Acceptance Target:**
- In 100 automated test operations involving valid and invalid record updates, zero operations leave saved records in an inconsistent state.

**Verification:** Automated tests covering validation failures, interrupted updates, and record retrieval.

### NFR-02: Access Control

**Priority:** Must — Waste management information and restricted actions require appropriate authorization.  
**Status:** Assumed

The system shall enforce role-based or equivalent partner-approved access restrictions.

**Proposed Acceptance Target:**
- In the agreed authorization test suite, 100% of unauthorized attempts to perform restricted actions are rejected.

**Verification:** Automated permission tests for each defined user role.

### NFR-03: Audit Record Completeness

**Priority:** Must — Chain-of-custody history must remain traceable.  
**Status:** Assumed

The system shall record the required audit information for tracked container actions.

**Proposed Acceptance Target:**
- In 100 tested successful tracked actions, 100% produce records containing the container identifier, action, timestamp, and responsible user.

**Verification:** Automated tests comparing completed actions against saved audit records.

### NFR-04: Dashboard Performance

**Priority:** Should — EH&S staff need timely access to operational information.  
**Status:** Assumed

The container dashboard shall return usable results within a measurable response-time limit.

**Proposed Acceptance Target:**
- At least 95% of dashboard requests complete within 3 seconds using a representative test dataset and an agreed test environment.

**Verification:** Repeatable performance tests with documented dataset size and environment.

### NFR-05: Usability

**Priority:** Should — The system must be practical for staff performing routine workflows.  
**Status:** Assumed

Users shall be able to complete representative waste management tasks using the application interface.

**Proposed Acceptance Target:**
- At least 4 out of 5 representative users complete an agreed pickup-request or container-tracking task without developer assistance.

**Verification:** Observed usability testing with representative users and documented task definitions.

### NFR-06: Maintainability

**Priority:** Should — Future capstone teams and maintainers must be able to understand and extend the application.  
**Status:** Assumed

The expansion shall include documented setup procedures and automated checks for supported functionality.

**Proposed Acceptance Target:**
- A team member following the documented clean-clone setup can run the supported build and test commands successfully.
- All required automated checks pass before a change is considered ready for integration.

**Verification:** Clean-clone setup exercise and CI results.

### NFR-07: Reliability of Container Updates

**Priority:** Must — Failed updates must not produce misleading container statuses.  
**Status:** Assumed

Failed container status changes shall not leave the current status inconsistent with the recorded history.

**Proposed Acceptance Target:**
- Across 100 simulated failed or rejected container updates, zero leave conflicting current-state and historical records.

**Verification:** Automated failure-injection and consistency tests.

### NFR-08: Record Retention

**Priority:** Must — Applicable waste management records must remain available for required retention periods.  
**Status:** Project Scope

The system shall retain relevant waste and chain-of-custody records according to applicable, partner-approved retention rules.

**Acceptance Target:**
- 100% of records in the agreed retention test cases remain available for the required simulated retention periods.
- Records cannot be deleted before their applicable retention deadline through ordinary user workflows.

**Verification:** Automated retention-policy tests using approved retention rules and simulated dates.

**Note:** Specific retention periods remain unresolved and must be validated before implementation.

## 5. Constraints

### C-01: Inherited Codebase

The project must extend the existing Hazard Track application rather than assume a complete replacement.

The existing architecture, dependencies, tests, and deployment configuration must be reviewed before making implementation decisions.

### C-02: Codebase Access

The previous year's Hazard Track codebase has not yet been made available to the team.

This currently prevents verification of existing functionality, dependencies, development commands, testing infrastructure, and deployment requirements.

The team has requested guidance from course instructors following an unsuccessful attempt to obtain access.

### C-03: Existing Technology and Infrastructure

The expansion must account for the inherited application's technology stack, interfaces, hosting arrangements, and maintenance expectations.

Specific technologies and infrastructure requirements remain unknown until the codebase and partner guidance are available.

### C-04: Regulatory and Safety Requirements

Radioactive and hazardous waste workflows must follow applicable requirements established by relevant authorities, potentially including the Oregon Department of Environmental Quality (ORDEQ), Oregon Health Authority (OHA), and Nuclear Regulatory Commission (NRC).

The applicability of specific regulations, labeling rules, decay-in-storage requirements, and record retention periods must be confirmed with the project partner and appropriate compliance stakeholders.

### C-05: Data Security

Waste management records and user information must be handled according to the project partner's applicable security, privacy, and access-control policies.

Specific restrictions must be confirmed before production deployment or the use of real operational data.

### C-06: Academic Schedule and Resources

Development must be completed within the capstone schedule and available team resources.

Scope adjustments may be necessary if inherited-codebase access or external dependencies remain blocked.

## 6. Success Metrics

The following three metrics are proposed for partner validation. They measure representative end-to-end outcomes rather than claiming current performance.

### SM-01: Radioactive Waste Request Completion

**Target:** 100% of 10 representative valid radioactive-waste pickup requests can be submitted and retrieved with their required information preserved.

**Collection Method:** Execute a documented acceptance-test dataset and compare submitted values with retrieved records.

**Decision Rule:** Pass if all 10 requests are saved and retrieved correctly; otherwise, fail.

### SM-02: Container Traceability

**Target:** 100% of 10 representative container histories preserve the expected sequence of recorded lifecycle actions, with no missing required audit fields.

**Collection Method:** Perform documented container lifecycle scenarios and compare the resulting history with expected records.

**Decision Rule:** Pass if all 10 histories match the expected actions and required audit fields; otherwise, fail.

### SM-03: Cost Reporting Accuracy

**Target:** 100% of totals in 10 representative cost-reporting scenarios match independently calculated expected totals.

**Collection Method:** Use a known test dataset containing vendor costs, labor costs where applicable, departments, waste categories, and reporting periods.

**Decision Rule:** Pass if all 10 scenarios produce the expected totals; otherwise, fail.

**Validation Note:** These targets are proposed. The project partner must confirm that the scenarios and success thresholds reflect useful project outcomes.

## 7. Non-Goals

The following capabilities are currently considered outside the planned expansion, pending confirmation with the project partner:

- GPS-based real-time location tracking of waste containers.
- AI-generated waste management recommendations.

These exclusions help maintain focus on radioactive-waste requests, internal container tracking, and cost analysis. Any changes to scope should be documented and reviewed with the project partner.

## 8. Open Questions

Each open question has an accountable follow-up role and a target decision point. These are proposed assignments, not claims that the named parties have accepted responsibility.

| ID | Open Question | Follow-Up Owner | Target Decision Point |
| --- | --- | --- | --- |
| OQ-01 | What languages, frameworks, and database technologies does the inherited application use? | Development team | Upon receiving codebase access |
| OQ-02 | Which existing features can be reused or extended? | Development team | After inherited-codebase audit |
| OQ-03 | How will the application integrate with Radiation Safety inventory? | Project partner; team follows up | Before FR-05 implementation |
| OQ-04 | What decay-in-storage rules must the system enforce? | Project partner / Radiation Safety; team follows up | Before FR-05A implementation |
| OQ-05 | What record retention periods apply to each waste category? | Project partner / compliance stakeholders; team follows up | Before retention implementation |
| OQ-06 | Which user roles may view, create, modify, or export records? | Project partner; team follows up | Before access-control implementation |
| OQ-07 | Which report export formats are required? | Project partner; team follows up | Before FR-15 implementation |
| OQ-08 | What forecasting method and historical data should be used? | Project partner; team follows up | Before FR-14 implementation |
| OQ-09 | Where will the application be hosted, and who owns the infrastructure? | Project partner / IT; team follows up | Before deployment planning is finalized |
| OQ-10 | What performance and availability targets are appropriate? | Project partner; team follows up | Before NFR targets are finalized |
| OQ-11 | Which lifecycle transitions are valid for each waste category? | Project partner / EH&S; team follows up | Before FR-07 implementation |
| OQ-12 | Which requirements belong in the first deliverable release? | Development team and project partner | Before finalizing the release scope |
| OQ-13 | How should the team satisfy code, testing, and CI checkpoint requirements while codebase access is blocked? | Development team; course instructors consulted | Before Repo Checkpoint 1 submission |

## 9. Requirements Validation and Traceability

The requirements in this document originate primarily from the provided capstone project description and the team's initial planning activities.

The team has completed user story mapping and identified major implementation decisions. These planning artifacts inform the proposed scope but do not substitute for direct validation with the project partner.

The following process will be used as the project progresses:

1. Review proposed requirements with the project partner or appropriate users.
2. Record confirmed requirements and revise assumptions that are incorrect.
3. Link implementation issues and pull requests to their requirement IDs.
4. Associate completed functional requirements with named automated tests where applicable.
5. Update this document in the same pull request as changes that alter documented behavior.
6. Keep unresolved requirements and acceptance criteria visible until they are implemented and verified.

The GitHub Project Board will track work assignments, progress, and implementation order. This document will remain the version-controlled record of product requirements.

## 10. Current Project Status

The team has completed initial planning work, including user story mapping, hard-to-reverse decisions, a safety net audit, a team charter, and development guidelines.

The repository currently contains `AGENTS.md` and `CONTRIBUTING.md`, with additional required project documentation being prepared.

The inherited Hazard Track codebase remains unavailable. A planned access meeting did not result in successful access, and the team has contacted course instructors for guidance.

As a result:

- Existing application behavior has not been independently verified.
- The technology stack and dependencies remain unknown.
- No inherited application tests or CI configuration have been inspected.
- The detailed requirements have not yet been formally validated with the project partner.
- Proposed performance targets and success metrics have not yet been measured.
- Implementation and deployment decisions remain open.

This document describes intended functionality and proposed acceptance conditions, not completed or verified features.

The team will update the requirements after obtaining codebase access, completing the inherited-codebase audit, and reviewing outstanding questions with the project partner.

## 11. References

- [OSU Capstone Project Requirements Guide](https://capstone.alexulbrich.com/guides/requirements/)
- Hazard Track: Radioactive Waste, Container Tracking, and Cost Analysis Expansion — provided project description.
- Team User Story Mapping — initial planning artifact.
- Team Hard-to-Reverse Decisions — initial planning artifact.
- Team Safety Net Audit — initial planning artifact.
