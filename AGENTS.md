# AGENTS.md

Context and rules for AI tools used on this project.
Owner: Addison Howard
Last reviewed: 10/11/2026


## Project Context

This CS 46X capstone project extends Hazard Track, a web application used by Oregon State University Environmental Health and Safety (EH&S). The partner is Peter Schoonover. 

The planned work includes:
- Radioactive-waste pickup requests: isotope, activity, form, container type, and shielding details; label generation; on-campus and remote-site routing; Radiation Safety inventory and decay-in-storage rules.
- Container tracking: unique QR/barcode IDs, lifecycle tracking from issuance through shipment, an EH&S status dashboard, and chain-of-custody history for hazardous and radioactive waste.
- Cost tracking and analysis: vendor disposal costs, internal labor and time modeling, trend analysis, forecasting, and exportable reports.


## Repository Guidance

- The team has not yet reviewed the inherited codebase. 
- Setup instructions are in `README.md`. The workflow, review requirements, and Definition of Done are in `CONTRIBUTING.md`.
- Limit each change to the task at hand, and flag any new dependency for team review.
- Report only test and build results that were actually obtained. State clearly when a check was not run.



## AI Use and Confidentiality

- Only public information, synthetic examples, and material the team and partner have approved may be submitted to external AI services.
- Real EH&S records, isotope inventories, researcher or lab details, vendor rates, partner documents, and meeting notes are excluded unless the specific tool has been approved for that material.
- Tests, fixtures, screenshots, and demonstrations use synthetic data only.
- Credentials, API tokens, SSH keys, and passwords must never appear in prompts, generated files, commits, or logs.
- This section reflects Section 6 of the Team Charter. If the two differ, the charter governs and this file will be corrected.


## Human Review

- The teammate submitting AI-assisted work is responsible for understanding it and explaining it during review.
- Tests, review, and merge requirements are defined in `CONTRIBUTING.md`.
- Passing tests do not establish that compliance logic, decay calculations, or cost figures are correct. A teammate must verify these independently.


## Planned Updates (Week 2)

| Missing guidance | Owner | Update trigger |
| --- | --- | --- |
| Stack, setup steps, and instructions for running the application | Addison Howard | After the team's initial codebase review |
| Test, lint, and CI commands | Noah Gregie | Once CI and tests are configured |
| Repository layout and data model | Addison Howard | After the team's initial codebase review |
| EH&S rules for decay-in-storage and routing | Addison Howard | Once the partner confirms them |
| Approved AI tools and the partner data each may receive | Addison Howard | Before any partner data is used with AI tools |

Planned features and commands are not to be described as implemented until they exist in the repository.
