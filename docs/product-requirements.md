# Product requirements (draft, 2026-09-23)

## Goal and boundaries

Improve fair assignment of student IT technician work while keeping routing, outcomes, and exceptions visible. This is a proposal for discussion with Bluefield State IT leadership, not a statement of existing policy. The precise current form-to-Zoho flow and Zoho product/configuration must be verified.

### Roles

| Role | Can do |
| --- | --- |
| Requester | Submit and receive updates through the existing approved channel (no requester portal initially). |
| Technician | See assigned work, update progress and effort, maintain schedule/absence, request reassignment. |
| Service owner / full-time staff | Receive tickets in their approved service category; work those tickets through the source system. |
| Scheduler / administrator | Manage people, roles, categories, skills, schedules, training duration and policy versions; see routing rationale; flag bad assignments. Cannot silently pick a favored technician. |
| Analyst permission | View authorized aggregate and ticket-level metrics as needed; grant through role-based access, never via a shared admin login. |
| System operator | Configure integrations and monitor failures; sensitive privileges separated and audited. |

A human must have a documented emergency override for outages, safety issues, special access, and sick leave. Every override requires a reason, actor, timestamp, and subsequent review. This preserves trust and operational continuity.

## Ticket lifecycle

New → needs triage / routed → queued → assigned → in progress → blocked / waiting → resolved → reopened (if needed). Preserve source ticket ID and history. Handle duplicate events idempotently, reopens, cancellations, stale tickets, and availability changes. Define whether the source system or Anaba owns each status field before two-way synchronization.

Classify first to service categories such as account/help desk, infrastructure, technician hardware, printer, software deployment, or unknown. These are examples; staff must define the real taxonomy. Account lockouts and password resets go to authorized personnel using approved identity verification; do not collect passwords in Anaba. Distinguish category from urgency and skill requirements. High-impact incidents and unclear requests get review.

## Functional requirements

- Import or mock tickets; maintain source IDs, timestamps, location, category, priority, estimated effort, requirements, and audit history.
- Store recurring weekly shifts and dated exceptions in the campus time zone; capture last-minute absence and actual available minutes. Never infer availability solely from an unconfirmed schedule.
- Assign only eligible technicians who are on shift, have access/skills, and can finish or hand off within a feasible window. Support multi-person jobs with a configurable minimum/maximum crew and estimated person-hours. Avoid assigning four people merely because four are free.
- Track both planned load and actual work minutes. Count shared jobs per person's actual effort, not one full ticket each. Show rolling comparisons by available capacity, category, undesirable work, and training opportunity.
- During a configurable onboarding period (initial proposal: one month from hire), require a qualified mentor for unsupervised-prohibited tasks. Rotate across job types and mentors when feasible. Permit explicit sign-off and extension rather than assuming competence on day 31.
- Let technicians accept/start/block/resolve work, add safe notes and time spent, and report incorrect classification or estimates. Give requesters updates via the approved existing channel.
- Provide dashboards with assignment rationale, workload distribution, completion times, backlog and routing corrections. Separate individual data from aggregate reports by permission.
- Send notifications through channels approved by IT; the web app must work on phones without requiring a native app.

## Trust, security, and privacy

Use institutional identity and MFA where feasible, least-privilege roles, server-side authorization, encrypted transport, backups, retention rules, audit logs, and approved hosting. Do not put credentials, passwords, access tokens, or unredacted ticket text in a public repository. Only use synthetic or properly de-identified data while prototyping. Limit LLM input to needed fields, reject instructions embedded in ticket text as untrusted data, validate structured output against allowed categories, and fall back to review when unavailable or uncertain.

## Pilot acceptance criteria (proposed, tune with staff)

- 100% of assignment decisions have a reproducible policy version, eligible-candidate snapshot and explanation.
- No simulated assignment to an unavailable, unauthorized, or unmentored technician; tests cover shift edges, absences, and DST.
- Under matched skills and availability in simulation, workload-per-available-hour does not diverge beyond a staff-agreed tolerance over a rolling window; show exceptions and tradeoffs.
- Every unknown/low-confidence category is reviewable; routing errors and overrides are measurable.
- During shadow mode, staff can compare recommendations with actual assignment and document corrections before any live routing.

## Questions to resolve with the department

1. Is the system Zoho Desk? Who owns the current form, API credentials, workflow rules and ticket data?
2. Which service categories belong to student techs versus which full-time teams, and who can make account changes?
3. What is a shift: scheduled hours, clocked hours, or confirmed daily availability? How late may an absence be reported?
4. What is the meaningful fairness unit: effort minutes, complexity, unpleasant tasks, or a weighted combination? How are overtime and voluntary extra shifts treated?
5. Which tasks require two people, special access, location, deadline, or supervised training?
6. What institutional authentication, accessibility, data retention, incident response and hosting requirements apply?
7. Who owns the deployed system after graduation, and who can amend assignment policy?

## Non-goals for the initial pilot

Replacing the public help form, autonomous account actions, model fine-tuning on staff behavior, and production deployment. Specialization should be inferred from reviewed work history or declared skills with human validation; assignment frequency by itself reflects prior bias and is not proof of ability.
