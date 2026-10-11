NOTE: This is a work in-progress, and will be updated throught the year!

# Contributing Guide

**Project:** Hazard Track: Radioactive Waste, Container Tracking, and Cost Analysis Expansion  
**Team:** Four student contributors  
**Status:** Early project planning; items marked **TBD** require confirmation.

This guide explains how to plan, implement, test, review, and accept contributions to the Hazard Track expansion. It applies to code, tests, documentation, design, and other project deliverables. Do not treat proposed processes or future checks as currently enforced.

## Code of Conduct

Treat teammates, mentors, and project partners respectfully. Give constructive feedback, communicate blockers promptly, and avoid sharing confidential project information. Raise team concerns through email or at a team meeting. For sensitive concerns, contact the course instructor or designated project mentor privately.

## Getting Started

1. Obtain repository access from a team member and clone the GitHub repository:
   ```bash
   git clone <REPOSITORY_URL>
   cd <REPOSITORY_DIRECTORY>
   ```
2. Read `README.md`, open GitHub Issues/Projects, and review the current sprint tasks.
3. Confirm the development stack, prerequisites, and access permissions with the mentor before installing project-specific tools.
4. Follow the setup and local-run commands in `README.md` once those instructions have been verified.
5. Never commit credentials, tokens, real sensitive records, or local `.env` files. Use a documented `.env.example` with placeholder values if configuration variables are needed.

**TBD:** Languages/frameworks, required versions, installation steps, environment variable names, local application startup command, and sample/test data. **Owner:** Quality Owner

## Branching & Workflow

Use a lightweight feature-branch workflow with `main` as the protected default branch. Create one branch per issue, such as `feature/23-container-labels`, `fix/31-status-update`, or `docs/12-setup-guide`. Open a pull request (PR) into `main`; do not commit directly to `main` after branch protection is enabled. Prefer updating a feature branch from `main` before review; use merge or squash according to the team's final GitHub settings. Do not force-push shared branches without agreement.

**TBD:** Confirm default branch, branch protection, merge strategy, and whether rebasing is allowed. **Owner:** Quality Owner

## Issues & Planning

Use GitHub Issues for individual tasks and GitHub Projects to track sprint progress. Each issue should have a clear title, short description, acceptance criteria, an assignee, and a sprint or milestone. **Proposed labels:** `feature`, `bug`, `documentation`, `testing`, and `blocked`. Review priorities, estimate or size tasks, and assign owners at sprint planning meetings. Break large tasks into pieces that can be completed and reviewed within a sprint. Link PRs to their issues.

**TBD:** Final issue template, estimation method, and triage rotation. **Owner:** Project Manager

## Commit Messages

Use Conventional Commits: `type: short description`. Examples:

```text
feat: add container status model
fix: correct waste category validation
docs: clarify local setup instructions
test: cover label generation rules
```

Use descriptive, focused commits. Reference the relevant issue in the PR description (for example, `Closes #23`), or in a commit message when helpful. Do not include confidential data in commit messages.

## Code Style, Linting & Formatting

Use the language-appropriate formatter and linter selected after the stack is confirmed. Keep changes readable, consistent with the existing Hazard Track codebase, and limited to the issue's scope. Review generated files before committing them.

**Not configured:** No formatter, linter, configuration path, or executable check/fix command has been confirmed. When selected, document the exact commands here and in `README.md`, along with configuration file locations. **Owner:** Quality Owner

## Testing

Add or update tests whenever a change introduces or modifies behavior. Planned test categories include unit tests for validation and business rules, integration tests for system interactions, and manual acceptance checks for workflows that cannot yet be automated. Use synthetic data rather than confidential waste, personnel, or partner records. Record manual test steps and results in the PR when automation is unavailable.

**Not configured:** Test framework, local test command, test-data setup, and coverage threshold are TBD. Until a test suite exists, the PR must explicitly state what was checked manually and what remains unverified; manual checks are not a substitute for future automated gates. **Owner:** Quality Owner **Coverage threshold:** TBD by team and mentor; do not claim a threshold is enforced before it is configured.

## Definition of Done

A contribution is **Done** only when its applicable acceptance criteria have been met and the team has accepted it. The following are the team's **proposed merge requirements**; they become mandatory automated gates only after the corresponding tooling is implemented.

| Check | Acceptance condition | Enforcement / current status | Planned owner and target |
| Issue acceptance | Linked issue has clear criteria; deliverable meets them | GitHub Issue and PR checklist; manual review planned | Issue assignee and reviewer; immediately after policy approval |
| Code review | At least one other team member approves the PR | GitHub PR approval; branch protection **not configured** | Repository administrator; next planning sprint |
| Tests | Relevant automated tests pass; new behavior has tests where feasible | CI test job **not configured**; manual evidence required meanwhile | Testing-infrastructure assignee; first implementation sprint after stack confirmation |
| Formatting / lint | Applicable checks pass without unresolved errors | CI lint job or local check **not configured** | Development-tooling assignee; first implementation sprint after stack confirmation |
| Security | No committed secrets; dependency and code risks reviewed | Secret/dependency scanning **not confirmed**; manual review meanwhile | Security/tooling assignee; first implementation sprint after stack confirmation |
| Documentation | Setup, behavior, or user-facing changes reflected in relevant docs | PR checklist and reviewer inspection; automated doc check **not configured** | PR author and reviewer; immediately after policy approval |
| CI status | All required jobs pass before merge | GitHub Actions **not configured** | CI assignee; first implementation sprint after stack confirmation |

**Sprint ownership rule:** At the next sprint planning meeting, create one GitHub Issue for each missing gate, assign a named team member, and replace the role-based owners and relative targets above with actual names and sprint numbers. Until a gate exists, mark it **not yet automated** in PRs; do not report it as passing. A reviewer should not approve a change with unresolved critical security concerns or unmet acceptance criteria.

## Contribution Norm

**Minimum expectation:** Every one of the four student contributors completes **at least one accepted piece of work per sprint**. Work should be sized so each member has a realistic opportunity to meet this expectation. Pairing is encouraged, but each person's contribution must be identifiable.

| Work type | Where evidence lives | What counts as accepted |
| Code, tests, configuration | GitHub repository, linked issue, and PR | Reviewed and merged PR meeting applicable Definition of Done checks |
| Documentation or design | Repository documentation and linked GitHub Issue | Reviewed and merged documentation, or an approved linked design deliverable |
| Research, planning, partner coordination | GitHub Issue/Projects with meeting notes or approved artifact; partner system only if authorized | Issue has a concrete deliverable and acceptance confirmation from the team or mentor |

At sprint planning, assign each person at least one achievable issue. Review progress and blockers in meetings and by email; re-scope or pair on tasks when necessary. **Proposed review turnaround:** Aim for an initial response within two working days, subject to course schedules. At sprint end, record accepted work and evidence links in GitHub Projects and the required course sprint notes. Activity alone (for example, attending meetings or opening an unfinished PR) does not automatically count as accepted work. **TBD:** Confirm whether the mentor has additional acceptance requirements.

## Pull Requests & Reviews

Keep PRs focused on one issue. Include a summary, linked issue, testing evidence, documentation changes, screenshots when useful, and any risks or follow-up work. Request review from at least one teammate who did not author the change. Reviewers check correctness, readability, test evidence, documentation, and security. Address comments before merging. Large changes should be split where practical; no numeric PR size limit is set yet. Do not merge while required checks fail or required approval is missing once protection is enabled.

**TBD:** PR template, required reviewer count, numeric size limit, and GitHub protection rules. **Owner:** Quality Owner

## CI/CD

**Current state:** No CI/CD pipeline has been configured. **Proposed:** Use GitHub Actions to run the selected formatter/linter, tests, and applicable security checks on pull requests. Pipeline definitions will live under `.github/workflows/` once created. Review results in the PR's **Checks** tab or the repository's **Actions** tab; authorized contributors may re-run failed jobs after diagnosing the failure. Merging should require all designated checks to pass once configured.

**TBD:** Workflow filenames, job names, exact commands, release automation, and deployment permissions. **Owner:** Quality Owner. **Target:** First implementation sprint after stack confirmation. Until then, PRs must record manual verification and explicitly identify missing automation.

## Security & Secrets

Never commit API keys, passwords, access tokens, real sensitive records, or other confidential partner information. Store secrets only through an approved local secret mechanism or repository/hosting secret manager, and provide placeholder configuration examples. Report suspected vulnerabilities or exposed credentials privately to the mentor and repository administrator by email; do not publish exploit details in a public issue. Rotate exposed credentials promptly through authorized owners. Review dependencies before adding them and apply security updates after compatibility testing.

**TBD:** Approved security scanner, dependency update cadence, vulnerability response contact, data classification rules, and access boundaries. **Owner:** Mentor and AI Coordinator. **Target:** First implementation sprint after stack confirmation. Do not upload partner data or internal system details to unapproved AI services.

## Documentation Expectations

Update `README.md` when setup or usage changes; maintain relevant technical documentation under `docs/` if that directory is adopted. Document interfaces and business rules as they are implemented, including radioactive-waste pickup, container tracking, and cost-analysis behaviors. Update `CHANGELOG.md` for user-visible changes once a changelog process is adopted. Comments and docstrings should explain non-obvious behavior and important constraints, not repeat the code. PRs should link documentation updates or explain why none are needed.

**TBD:** Documentation structure, API reference generator, and changelog format. **Owner:** Project Manager

## Release Process

**Not finalized:** The team has not approved a versioning, packaging, deployment, or rollback procedure. **Proposed:** Use version tags and release notes after a mentor-approved release process is established. Before release, verify the Definition of Done, record known limitations, obtain required partner approval, and document how to restore the previous known-good version. Do not deploy to partner systems without authorization.

**TBD:** Version scheme, release approver, release cadence, deployment environment, rollback procedure, and any integration-specific controls. **Owner:** Team and mentor; decide before the first planned release.

## Support & Contact

Use team email and scheduled meetings for questions, blockers, and review coordination. Link technical questions to the relevant GitHub Issue so decisions are documented. Contact the project mentor for requirements, access, and integration decisions. **Proposed:** Acknowledge routine team questions within two working days; raise urgent blockers as soon as practical. **TBD:** Maintainer email or group address, mentor contact route, meeting schedule, and final response-time expectations.

---

**Next planning actions:** Confirm the stack with the mentor; approve or revise the proposed branch/PR workflow; assign named owners and sprint numbers to missing Definition of Done gates; add verified local setup, lint, and test commands as the codebase develops.
