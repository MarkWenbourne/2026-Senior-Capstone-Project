
# Hazard Track

**Radioactive Waste, Container Tracking, and Cost Analysis Expansion**

**Team:** Mark Wenbourne, Addison Howard, Noah Gregie, Eduardo Juchem Balzan  
**Institution:** Oregon State University  
**Project:** 2026–2027 Software Engineering Capstone  
**Status:** Planning and Documentation — Awaiting Inherited Codebase

## Project Overview

Hazard Track is an existing application used by Oregon State University's Environmental Health and Safety (EH&S) department to support hazardous waste management.

Our capstone project focuses on expanding Hazard Track with additional capabilities for radioactive-waste pickup requests, internal container labeling and tracking, and waste management cost analysis.

The goal is to improve record accuracy, container traceability, operational visibility, and reporting while supporting applicable safety and regulatory requirements.

This project is intended to extend the existing Hazard Track application rather than replace it.

## Project Objectives

The expansion focuses on three major areas.

### 1. Radioactive Waste Pickup Requests

Provide workflows for submitting and managing radioactive-waste pickup requests.

Planned capabilities include:

- Collecting isotope, activity, waste form, container type, and shielding information.
- Generating radioactive-waste labels with required identification information.
- Supporting on-campus and remote pickup workflows.
- Associating requests with Radiation Safety inventory information.
- Supporting applicable decay-in-storage rules.
- Maintaining records needed for operational and compliance purposes.

### 2. Internal Labeling and Container Tracking

Improve identification and tracking of hazardous and radioactive waste containers.

Planned capabilities include:

- Assigning unique QR code or barcode identifiers to containers.
- Tracking containers through lifecycle stages such as issued, filled, picked up, processed, stored, and shipped.
- Providing an EH&S dashboard showing current container statuses.
- Supporting both hazardous and radioactive waste workflows.
- Maintaining historical chain-of-custody records.

### 3. Cost Tracking and Analysis

Provide tools for tracking and reviewing waste management expenses.

Planned capabilities include:

- Recording vendor disposal costs.
- Tracking internal labor and handling costs.
- Analyzing costs by department, waste type, and fiscal quarter.
- Forecasting future disposal expenses.
- Exporting reports for leadership reviews and audits.

These capabilities represent the planned expansion and should not be interpreted as already implemented.

## Current Project Status

The team is currently working on project planning, documentation, and preparation for development.

The inherited Hazard Track codebase has not yet been made available. As a result, the team has not been able to inspect the existing application, verify its architecture, or determine its development and deployment requirements.

The team has contacted course instructors for guidance regarding the access issue.

Until the inherited codebase becomes available, the team is focusing on documenting requirements, identifying technical risks, and preparing the repository for future development.

**Current limitations:**

- The existing application's source code is unavailable.
- The technology stack has not been verified.
- Build and execution commands are not yet known.
- Application tests and CI configuration have not been established.
- The deployment environment has not been confirmed.

This README will be updated as the team gains access to the application and begins implementation.

## Getting Started

### Prerequisites

To work with the currently available repository contents, you will need:

- Git
- A GitHub account for contributing changes
- A text editor or IDE, such as Visual Studio Code

Additional development prerequisites will be documented after the inherited codebase is available.

### Clone the Repository

Clone the repository using:

```bash
git clone <REPOSITORY_URL>
```

Navigate into the project directory:

```bash
cd <REPOSITORY_DIRECTORY>
```

Replace `<REPOSITORY_URL>` with the repository's GitHub URL and `<REPOSITORY_DIRECTORY>` with the cloned directory name.

### Install Dependencies

**Status: Blocked — Inherited codebase unavailable**

The team has not yet identified the existing application's package manager, dependencies, or installation process.

Dependency installation instructions will be added after the inherited codebase has been reviewed.

### Environment Configuration

**Status: Blocked — Inherited codebase unavailable**

Required environment variables, configuration files, and external services are not yet known.

These requirements will be documented after the existing application has been inspected.

Do not commit passwords, API keys, access tokens, or other secrets to the repository.

### Run the Application Locally

**Status: Blocked — Inherited codebase unavailable**

The application cannot currently be started from this repository because the inherited application code has not yet been received.

Once access is available, this section will provide:

- Required development tools and versions.
- Dependency installation commands.
- Environment setup instructions.
- Database initialization steps, if applicable.
- Commands for starting the application.
- Instructions for verifying successful startup.

### Run Tests

**Status: Not configured**

The team has not yet established an application test suite.

After the inherited codebase is reviewed, this section will identify:

- The testing framework.
- Commands for running tests locally.
- Required test configuration.
- How test results are verified.

### Continuous Integration

**Status: Not configured**

The team intends to establish automated checks through GitHub Actions or another appropriate CI system after reviewing the inherited application's build and testing requirements.

Once implemented, this section will describe the automated checks and link to the corresponding workflows.

## Repository Structure

The planned repository structure is:

```text
Hazard-Track/
├── .github/
│   └── workflows/           # CI workflows (planned)
├── docs/
│   ├── requirements.md      # Functional and non-functional requirements
│   ├── design.md            # Architecture and technical design
│   ├── risks.md             # Risks, blockers, and mitigations
│   └── rfcs/                # Technical proposals and decisions
├── AGENTS.md                # AI assistant and project context
├── CONTRIBUTING.md          # Contribution guidelines
└── README.md                # Project overview and setup instructions
```

This structure describes the intended organization. Some directories and files may not exist yet.

The structure will be updated when the inherited application is added to the repository.

## Project Documentation

The following documents describe the project's requirements, technical direction, and development practices:

- [Requirements](docs/requirements.md) — Functional requirements, non-functional requirements, constraints, success metrics, and open questions.
- [Technical Design](docs/design.md) — Proposed architecture, interfaces, data relationships, deployment considerations, and deferred decisions.
- [Risks](docs/risks.md) — Project risks, blockers, mitigations, and unresolved dependencies.
- [Contributing Guide](CONTRIBUTING.md) — Development workflow, code review expectations, and contribution standards.
- [AI Context](AGENTS.md) — Repository context and instructions for AI-assisted development.

Some documents may still be under development.

## Development Workflow

The team uses GitHub for version control and project coordination.

Planned development practices include:

1. Creating or selecting an issue from the GitHub Project Board.
2. Assigning an owner and identifying acceptance criteria.
3. Creating a branch for the work.
4. Making and testing changes.
5. Opening a pull request for review.
6. Addressing review feedback.
7. Merging approved changes according to the team's agreed workflow.

The detailed contribution process is described in [CONTRIBUTING.md](CONTRIBUTING.md).

Processes that depend on application code, automated tests, or CI will be established and verified as development progresses.

## Requirements and Traceability

Project requirements are documented in [docs/requirements.md](docs/requirements.md).

Requirements use identifiers such as FR-01, FR-02, and NFR-01 to support traceability between documentation, implementation issues, and tests.

As implementation begins, the team will connect relevant GitHub issues and pull requests to these requirement identifiers.

## Project Risks and Dependencies

The most significant current dependency is obtaining access to the inherited Hazard Track codebase.

Without the existing application, the team cannot fully verify technical requirements, select implementation approaches, or test integration with existing functionality.

Additional risks and mitigation plans are maintained in [docs/risks.md](docs/risks.md).

## Contributing

Contributions should follow the procedures described in [CONTRIBUTING.md](CONTRIBUTING.md).

Before making changes, contributors should review the project requirements, technical design, and applicable repository guidelines.

Do not assume that planned tooling, automated checks, or deployment processes are already available.
