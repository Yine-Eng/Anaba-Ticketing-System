# Anaba

**The right IT work, with the right people, at the right time.**

Anaba is a proposed smart ticket routing and technician scheduling platform for a university IT department. It combines service-category triage, student technicians' real availability, and an explainable assignment policy to distribute work fairly while getting requests to the people equipped to handle them.

A password request should reach authorized help desk staff. A lab refresh may need two technicians and a new hire who can learn from one of them. Anaba aims to make those decisions consistent, visible, and responsive as schedules and priorities change.

## What it aims to do

- Route help requests to the correct service team, with human review for unclear or sensitive cases.
- Assign technician work based on availability, skills, estimated effort, and workload, with a recorded explanation.
- Pair new technicians with mentors and rotate them across different kinds of work.
- Give technicians a phone-friendly site for schedules, assignments, and progress.
- Give authorized staff a view of workload, backlog, and outcomes.

The assignment engine is deterministic. An optional AI component can suggest a ticket category, but it does not decide who works, grant access, or change accounts.

## Project status

**Planning / senior project proposal.** The first build will use synthetic tickets. Integration with the department's existing system, hosting, and any real ticket data depend on department approval.

Start with the [product requirements](docs/product-requirements.md), [assignment policy](docs/assignment-policy.md), [roadmap](docs/roadmap.md), [admin discovery guide](docs/admin-discovery.md), and [security plan](docs/security-plan.md).

**Proposed stack:** Python, FastAPI, PostgreSQL, and a responsive web frontend. The integration and optional local model will be evaluated after the core assignment system works.
