Hazard Track Design

Project: Hazard Track: Radioactive Waste, Container Tracking, and Cost Analysis Expansion

Team: Mark Wenbourne, Noah Gregie, Addison Howard, Eduardo Juchem Balzan

Status: Draft, based on the project requirements. The inherited codebase has not yet been made available, so this document describes what the expansion must do and what is still undecided. It does not describe the existing application's internals.

Overview

Hazard Track is an existing Oregon State University Environmental Health and Safety (EH&S) application. This project expands it so that:

Waste generators can request radioactive-waste pickups.
EH&S staff can identify and track waste containers from issue to shipment, with a full history of who did what.
EH&S staff and leadership can see, analyze, forecast, and export waste management costs.

The expansion extends the existing application rather than replacing it. The goals are accurate records, operational visibility, and better reporting, while supporting applicable safety and compliance requirements.

ARCHITECTURE

<img width="1370" height="956" alt="Hazard Track Diagram System Context" src="https://github.com/user-attachments/assets/2f44ed2f-bf8f-41ef-a443-59b6944bd309" />
<img width="1712" height="1634" alt="Hazard Track Diagram Provisional Container Architecture" src="https://github.com/user-attachments/assets/e29e0536-3c1a-4f75-8085-45178d182122" />

Context

Two groups of people use Hazard Track, and one outside system connects to it:

-Waste generators use it to request pickups.
-EH&S staff use it to track containers and review costs.
-Radiation Safety inventory is an outside source of information. Radioactive-waste requests can be associated with it. That link is a lower-priority feature, so the core workflows must work without it.

Capabilities

Radioactive waste pickup requests:

-Authorized users submit requests, which are saved and can be retrieved later.
-Each request records isotope, activity, waste form, container type, and shielding.
-The system generates printable labels showing the radioactive-material symbol, isotope, activity, date, generator, and container identifier.
-Each request is marked on-campus or remote and follows the workflow for that category.
-The system supports decay-in-storage rules supplied or approved by Radiation Safety, and never marks waste eligible unless those rules say so.

Container tracking:

-Every container gets a unique identifier that can be shown as a QR code or barcode.
-Containers move through lifecycle stages, and invalid status changes are rejected.
-EH&S staff see a dashboard of current container statuses.
-Both hazardous and radioactive waste containers are supported.
-Every handling action and status change is kept in a history that is never erased by later updates.

Cost tracking and analysis:

-Vendor disposal costs and internal labor costs are recorded against waste records.
-Cost summaries can be grouped by department, waste type, and fiscal quarter.
-Future costs can be forecast from historical data.
-Authorized users can export waste management and cost reports.

Access control

-Restricted actions and information require appropriate authorization. Users without the right permissions cannot view restricted container information, alter history, or export restricted reports. The specific roles are not yet defined.

Interfaces

This section lists what each interaction must do. How they are built (screens, endpoints, file formats) depends on the existing application and is not yet decided.

Submit a radioactive-waste request

-A complete request is saved and retrievable by its identifier.
-A request missing required information is rejected with an explanation.

View a label

-The label contains all six required elements and matches the waste record.
-It can be shown in a printable format.

Choose pickup location

-The user picks on-campus or remote.
-The choice is saved and the request is assigned to the matching workflow.

Link a request to inventory

-The link is preserved when the request is retrieved.
-An invalid or unavailable inventory reference does not corrupt the request.

Register a container

-Different containers get different identifiers.
-A duplicate identifier is rejected.

Look up a container

-Entering or scanning an identifier returns that container.
-An unknown identifier never returns an unrelated container.

Update container status

-Authorized users only.
-Valid changes are saved and invalid transitions are rejected.

View the dashboard

-Shows registered containers and current statuses.
-Lets staff find a container by identifier.
-Shows saved changes when refreshed.

View container history

Authorized users can retrieve the full history of a container.

Enter a vendor disposal cost

-Authorized users can enter it and tie it to a waste record.
-Invalid inputs, such as negative amounts where not permitted, are rejected.

Record labor time

-Authorized users record time, and the system calculates cost from the approved rate.

View a cost summary

-Users choose a grouping.
-Totals match the underlying records.
-Records outside the period are excluded.
-Empty periods do not show misleading totals.

Request a forecast

-Authorized users request one for a supported period.
-The result states the period and assumptions.
-Insufficient history is stated explicitly rather than presented as a reliable forecast.

Export a report

-Output uses a partner-approved format and matches the selected filters.
-Totals match the data.
-Restricted information is blocked for unauthorized users.

Data

What is recorded

-Radioactive-waste request: isotope, activity, waste form, container type, shielding, pickup location (on-campus or remote), assigned identifier.
-Container: unique identifier, waste category (hazardous or radioactive), category-specific information, current lifecycle status.
-Container history entry: container, action, timestamp, responsible user.
-Vendor disposal cost: amount, tied to a waste record, with weight, container, and waste category where applicable.
-Labor entry: labor time and the approved rate used.
-Department: used to group cost summaries.
-Inventory link: reference to Radiation Safety inventory information.

Container lifecycle

A container moves through these stages, listed in the order the requirements give them:

issued > filled > picked up > processed > stored > shipped

The exact set of allowed transitions may differ by waste category and is not yet confirmed. Any change not on the approved list is rejected.

Rules the data must follow
-Updating a container's status never erases its earlier history.
-Each history entry records the container, the action, the time, and the responsible user.
-A failed or rejected update never leaves the current status out of step with the recorded history.
An invalid or interrupted update never leaves saved records inconsistent.
-Waste and chain-of-custody records are kept for the required retention period and cannot be deleted early through ordinary workflows.
-Cost totals in summaries and exports match the underlying records.
-Real operational data is not used until the partner's security and access-control policies are confirmed.

Deployment

The hosting arrangement, infrastructure ownership, and deployment process are not yet known. They depend on the inherited application and on the project partner and IT. They will be written here once confirmed.


Quality targets

These targets are proposed, not yet measured or approved by the project partner.

Dashboard speed: at least 95% of requests finish within 3 seconds on a representative dataset.
Access control: 100% of unauthorized attempts at restricted actions are rejected in the agreed test suite.
Audit records: 100% of 100 tested actions produce records with container, action, timestamp, and user.
Usability: at least 9 of 10 representative users finish a task without developer help.
Maintainability: a clean clone can run the build and tests from the documented setup, and required checks pass before changes are integrated.
