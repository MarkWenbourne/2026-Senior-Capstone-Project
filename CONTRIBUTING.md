NOTE: This is a work in-progress, and will be updated throught the year!

# Contributing Guide

**Project:** Hazard Track: Radioactive Waste, Container Tracking, and Cost Analysis Expansion  
**Team:** Mark Wenbourne, Addison Howard, Noah Gregie, Eduardo Juchem Balzan
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

**TBD:** Languages/frameworks, required versions, installation steps, environment variable names, local application startup command, and sample/test data. **Owner:** Quality Owner, Noah Gregie

## Branching & Workflow

Use a lightweight feature-branch workflow with `main` as the protected default branch. Create one branch per issue, such as `feature/23-container-labels`, `fix/31-status-update`, or `docs/12-setup-guide`. Open a pull request (PR) into `main`; do not commit directly to `main` after branch protection is enabled. Prefer updating a feature branch from `main` before review; use merge or squash according to the team's final GitHub settings. Do not force-push shared branches without agreement.

**TBD:** Confirm default branch, branch protection, merge strategy, and whether rebasing is allowed. **Owner:** Quality Owner, Noah Gregie

## Issues & Planning

Use GitHub Issues for individual tasks and GitHub Projects to track sprint progress. Each issue should have a clear title, short description, acceptance criteria, an assignee, and a sprint or milestone. **Proposed labels:** `feature`, `bug`, `documentation`, `testing`, and `blocked`. Review priorities, estimate or size tasks, and assign owners at sprint planning meetings. Break large tasks into pieces that can be completed and reviewed within a sprint. Link PRs to their issues.

**TBD:** Final issue template, estimation method, and triage rotation. **Owner:** Project Manager, Mark Wenbourne

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

**Not configured:** No formatter, linter, configuration path, or executable check/fix command has been confirmed. When selected, document the exact commands here and in `README.md`, along with configuration file locations. **Owner:** Quality Owner, Noah Gregie

## Testing

Add or update tests whenever a change introduces or modifies behavior. Planned test categories include unit tests for validation and business rules, integration tests for system interactions, and manual acceptance checks for workflows that cannot yet be automated. Use synthetic data rather than confidential waste, personnel, or partner records. Record manual test steps and results in the PR when automation is unavailable.

**Not configured:** Test framework, local test command, test-data setup, and coverage threshold are TBD. Until a test suite exists, the PR must explicitly state what was checked manually and what remains unverified; manual checks are not a substitute for future automated gates. **Owner:** Quality Owner, Noah Gregie **Coverage threshold:** TBD by team and mentor; do not claim a threshold is enforced before it is configured.


## Definition of Done

A contribution is considered **Done** only when its acceptance criteria have been met, the required reviews and checks are complete, and the team has accepted the work. These requirements apply to code, tests, documentation, and other project deliverables where applicable.

Some automated checks have not yet been implemented because the development stack is still being determined. Until those checks are available, manual verification must be documented in the pull request (PR).

### Required Checks

| Check | Acceptance Condition | Enforcement / Current Status | Target Sprint | Owner |
|---|---|---|---|---|
| Issue Acceptance | The contribution meets the acceptance criteria defined in its linked GitHub Issue. | GitHub Issues and PR checklist; manual verification currently required. | Sprint 2 | Mark Wenbourne — Project Manager |
| Code Review | At least one teammate other than the author reviews and approves the PR. | GitHub PR approval; branch protection not yet configured. | Sprint 3 | Noah Gregie — Quality Owner |
| Automated Testing | Relevant tests pass, and new functionality includes appropriate tests where feasible. | GitHub Actions test job; not yet configured. Manual testing evidence required until implemented. | Sprint 4 | Noah Gregie — Quality Owner |
| Code Style and Linting | Code follows the selected formatting and linting standards. | GitHub Actions lint job or pre-commit hook; not yet configured. | Sprint 4 | Noah Gregie — Quality Owner |
| Security Checks | No credentials or confidential information are committed, and applicable security checks pass. | Manual review initially; automated secret and dependency scanning planned. | Sprint 4 | Noah Gregie — Quality Owner |
| Documentation | Relevant project documentation is updated to reflect changes. | PR checklist and reviewer verification. | Sprint 3 | Eduardo Juchem Balzan — Deployment and Documentation Owner |
| CI Status | All required automated jobs pass before merging. | GitHub Actions and required status checks; not yet configured. | Sprint 4 | Noah Gregie — Quality Owner |

### Enforcement and Implementation

The Quality Owner is responsible for maintaining the Definition of Done and coordinating the implementation of quality checks.

- **Sprint 2:** Establish issue acceptance requirements and document how contributions are reviewed and accepted.
- **Sprint 3:** Configure pull request review requirements, establish branch protection, and finalize documentation review expectations.
- **Sprint 4:** Implement automated testing, linting, applicable security scanning, and required GitHub Actions status checks.

These sprint targets are proposed and must be confirmed by the team before submission. Changes to approved targets must be recorded in GitHub Issues/Projects.

Each unfinished check must have a corresponding GitHub Issue assigned to a named team member, with its target sprint and acceptance criteria recorded.

The Project Manager tracks progress on these issues, while the Quality Owner coordinates technical implementation. The AI Coordinator maintains confidentiality requirements and advises on security-related restrictions.

### Requirements Before Merging

Before merging a pull request, the following conditions must be satisfied:

1. The PR is linked to a GitHub Issue with clearly defined acceptance criteria.
2. The changes satisfy the issue's acceptance criteria.
3. At least one teammate other than the author has reviewed and approved the PR.
4. Relevant automated tests have passed, or manual testing evidence is documented when automated tests are unavailable.
5. Applicable formatting, linting, and security checks have been completed, with unavailable automated checks clearly identified.
6. Documentation has been updated where necessary.
7. All configured and required CI checks have passed.
8. No unresolved critical defects, security concerns, or confidentiality violations remain.

Until automated checks are implemented, contributors must identify which checks were performed manually and which could not be completed. Unavailable checks must never be reported as passing.

Once the planned CI gates are implemented, all required automated checks must pass before merging. Exceptions must be documented and approved through the team's established decision process.

### Shared Responsibility

Although the Quality Owner maintains the Definition of Done, all four team members are responsible for following it.

Contributors must verify their work before requesting review, and reviewers must confirm that applicable requirements have been satisfied.

The Definition of Done will be reviewed during sprint retrospectives and updated as the project develops, testing tools are introduced, and additional requirements are confirmed with the project mentor.

## Contribution Norm

**Minimum expectation:** Every one of the four student contributors completes **at least one accepted piece of work per sprint**. Work should be sized so each member has a realistic opportunity to meet this expectation. Pairing is encouraged, but each person's contribution must be identifiable.

| Work type | Where evidence lives | What counts as accepted |
| Code, tests, configuration | GitHub repository, linked issue, and PR | Reviewed and merged PR meeting applicable Definition of Done checks |
| Documentation or design | Repository documentation and linked GitHub Issue | Reviewed and merged documentation, or an approved linked design deliverable |
| Research, planning, partner coordination | GitHub Issue/Projects with meeting notes or approved artifact; partner system only if authorized | Issue has a concrete deliverable and acceptance confirmation from the team or mentor |

At sprint planning, assign each person at least one achievable issue. Review progress and blockers in meetings and by email; re-scope or pair on tasks when necessary. **Proposed review turnaround:** Aim for an initial response within two working days, subject to course schedules. At sprint end, record accepted work and evidence links in GitHub Projects and the required course sprint notes. Activity alone (for example, attending meetings or opening an unfinished PR) does not automatically count as accepted work. **TBD:** Confirm whether the mentor has additional acceptance requirements.

**Owner:** Project Manager, Mark Wenbourne

## Pull Requests & Reviews

Keep PRs focused on one issue. Include a summary, linked issue, testing evidence, documentation changes, screenshots when useful, and any risks or follow-up work. Request review from at least one teammate who did not author the change. Reviewers check correctness, readability, test evidence, documentation, and security. Address comments before merging. Large changes should be split where practical; no numeric PR size limit is set yet. Do not merge while required checks fail or required approval is missing once protection is enabled.

**TBD:** PR template, required reviewer count, numeric size limit, and GitHub protection rules. **Owner:** Quality Owner, Noah Gregie

## CI/CD

**Current state:** No CI/CD pipeline has been configured. **Proposed:** Use GitHub Actions to run the selected formatter/linter, tests, and applicable security checks on pull requests. Pipeline definitions will live under `.github/workflows/` once created. Review results in the PR's **Checks** tab or the repository's **Actions** tab; authorized contributors may re-run failed jobs after diagnosing the failure. Merging should require all designated checks to pass once configured.

**TBD:** Workflow filenames, job names, exact commands, release automation, and deployment permissions.

The **Quality Owner**, Noah Gregie, is responsible for establishing and maintaining the project's continuous integration pipeline.

The team plans to configure GitHub Actions during Sprint 3 or 4, following confirmation of the development stack. The initial pipeline will include automated tests, linting and formatting checks, and applicable security checks.

GitHub branch protection and required status checks will be configured during Sprint 3 or 4.

Until these checks are implemented, pull requests must document manual verification and identify any unavailable automated checks. Once configured, all required CI jobs must pass before a pull request can be merged.

## Security & Secrets

Never commit API keys, passwords, access tokens, real sensitive records, or other confidential partner information. Store secrets only through an approved local secret mechanism or repository/hosting secret manager, and provide placeholder configuration examples. Report suspected vulnerabilities or exposed credentials privately to the mentor and repository administrator by email; do not publish exploit details in a public issue. Rotate exposed credentials promptly through authorized owners. Review dependencies before adding them and apply security updates after compatibility testing.

**TBD:** Approved security scanner, dependency update cadence, vulnerability response contact, data classification rules, and access boundaries. **Owner:** Mentor and AI Coordinator (Addison Howard). **Target:** First implementation sprint after stack confirmation. Do not upload partner data or internal system details to unapproved AI services.

## Documentation Expectations

Update `README.md` when setup or usage changes; maintain relevant technical documentation under `docs/` if that directory is adopted. Document interfaces and business rules as they are implemented, including radioactive-waste pickup, container tracking, and cost-analysis behaviors. Update `CHANGELOG.md` for user-visible changes once a changelog process is adopted. Comments and docstrings should explain non-obvious behavior and important constraints, not repeat the code. PRs should link documentation updates or explain why none are needed.

**TBD:** Documentation structure, API reference generator, and changelog format. **Owner:** Deployment and Documentation Owner, Eduardo Juchem Balzan

## Release Process

**Not finalized:** The team has not approved a versioning, packaging, deployment, or rollback procedure. **Proposed:** Use version tags and release notes after a mentor-approved release process is established. Before release, verify the Definition of Done, record known limitations, obtain required partner approval, and document how to restore the previous known-good version. Do not deploy to partner systems without authorization.

**TBD:** Version scheme, release approver, release cadence, deployment environment, rollback procedure, and any integration-specific controls. **Owner:** Team and mentor; decide before the first planned release.

## Support & Contact

Use team email and scheduled meetings (Microsoft Teams) for questions, blockers, and review coordination. Link technical questions to the relevant GitHub Issue so decisions are documented. Contact the project mentor for requirements, access, and integration decisions. **Proposed:** Acknowledge routine team questions within two working days; raise urgent blockers as soon as practical. **TBD:** Maintainer email or group address, mentor contact route, meeting schedule, and final response-time expectations.

**Owner:** Project Manager, Mark Wenbourne

---

**Next planning actions:** Confirm the stack with the mentor; approve or revise the proposed branch/PR workflow; assign named owners and sprint numbers to missing Definition of Done gates; add verified local setup, lint, and test commands as the codebase develops.
