# Risks

Objective: OSU EH&S staff and waste generators submit radioactive-waste requests, track container lifecycles, and analyze disposal costs in the expanded Hazard Track app. Rank: likelihood/impact (H/M/L) and why.

R-1 technical, H/H (currently blocked; every feature extends the existing app).
  The inherited Hazard Track codebase is unavailable; until access is granted,
  we cannot audit the stack or integrate features. Asked: project partner and
  course instructors, Week 4. Owner: Mark. Mitigate: run CI on a starter
  scaffold and isolate domain logic until access lands. Trigger: no repository
  access by 2026-11-08.
  
R-2 business, H/H (unconfirmed; wrong rules invalidate core workflows).
  Radioactive decay-in-storage and container lifecycle rules are unvalidated;
  if our assumptions conflict with EH&S compliance, core workflows fail.
  Asked: project partner, Week 4. Owner: Noah. Mitigate: review FR-01 through
  FR-10 with the partner before building state rules. Trigger: no validation
  meeting 
  
R-3 business, M/H (IT reviews take weeks; it gates production). The hosting
  target and OSU IT review have no date; until approved, the walking skeleton
  cannot deploy in Week 10. Owner: Addison.Mitigate: send the deployment proposal 
  now and run a team staging instance first. Trigger: no hosting target agreed 
  
R-4 technical, M/M (unknown schema; blocks FR-05). Radiation Safety inventory
  access is unproven; without it, pickup requests cannot link to live
  inventory. Start by: 2026-11-15. Owner: Eduardo. Mitigate: build an adapter
  with a CSV import fallback. Trigger: no inventory sample data two weeks
  after codebase access.
  
R-5 team, M/M (delayed access compresses onboarding). Late codebase delivery
  leaves little time to learn the stack; if only one person learns the deploy,
  absences stall releases. Owner: Mark. Mitigate: pair on the clean-clone
  setup and first two deploys. Trigger: fewer than two teammates run the
  inherited build within 72 hours of access.


## Closed
None yet.
