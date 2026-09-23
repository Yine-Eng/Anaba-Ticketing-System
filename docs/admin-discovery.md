# Admin discovery guide

Use this to learn the workflow and seek a small, safe pilot. Record answers, the person responsible, and any follow-up; do not collect credentials, private tickets, or personal schedules in meeting notes.

## Opening

> I'm planning a senior project called Anaba around IT ticket routing and student technician scheduling. I'd like to understand how your current workflow operates and where software could save coordination time, make coverage clearer, and help new techs learn. I don't want to assume the existing process is wrong. I would first build with sample data and show you the recommendations before proposing any connection to live tickets. Could I ask how the process works and what you would find useful?

## Questions for a first 20–30 minute conversation

1. When someone submits the Bluefield State help form, where does the request go? Is the product Zoho Desk? Are email, phone, and walk-ins entered too?
2. Who first reads a ticket, who assigns it, and who updates or closes it? Which parts take the most time?
3. Which request types go to student technicians, and which must go to full-time or authorized staff? What cases always need human review?
4. How do you decide who is available? How are class schedules, sick days, breaks, location, and urgent changes handled?
5. What determines whether a job needs one tech, two techs, or a team? Are there tasks that should never be assigned to a trainee alone?
6. What would a good assignment system optimize for: fast response, even effort, skill fit, mentoring, minimizing travel, or something else? What would make you distrust its recommendation?
7. What are the most common exceptions where you need to override an assignment? Who should be able to do so, and how should the reason be recorded?
8. How do new technicians learn the work now? What should they experience before working alone?
9. What information do you already track about time spent, completion, reopens, and workload? What reports would actually help?
10. Would a demo using invented tickets and schedules be useful? If yes, who else should review it, and what would a successful pilot look like?

## Follow-up with the system owner / campus IT security

- Who owns the form, ticket platform, API access, and integration changes? What licensing or rate limits apply?
- Is campus single sign-on available to student projects? Which identity provider and role source should a production app use?
- What ticket fields are sensitive, who may access them, how long may they be retained, and where may they be hosted or backed up?
- Is an internally hosted server possible? Who patches it, monitors it, restores backups, and supports it after graduation?
- What review is needed before read-only access, shadow mode, or changing live assignments? Is use of ticket content with a local LLM permitted?
- Who can approve a prototype, and who could own an eventual deployment?

## Tone and framing

Talk about *capacity, consistency, transparency, and onboarding* rather than claiming particular people are unfair. Current manual assignment may reflect emergencies, access limits, and information you cannot yet see. Ask for their constraints and invite them to define success. Show an override mechanism with an audit trail: human judgment stays available, while patterns become easier to inspect.

Avoid promising that Anaba will replace Zoho, eliminate administrators, or prove fairness before you have data. Offer to share a mock-data demo and get criticism early. If the department cannot authorize live data, the senior project remains viable as a standalone simulated system.

## What to bring back

A workflow sketch; approved categories and assignment constraints; anonymized or invented examples; fairness definition; security/hosting requirements; pilot owner; and unresolved questions. Update the requirements and policy documents with the answers, distinguishing confirmed facts from proposals.
