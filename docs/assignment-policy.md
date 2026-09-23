# Assignment policy v0 (design proposal)

## Principles

The scheduler is deterministic and auditable. An optional classifier proposes category and skill tags; only validated, approved fields enter the scheduler. A fixed policy version and identical input snapshot produce identical assignments. Store reasons for inclusion, exclusion, and selection.

## Definitions

- **Available minutes**: confirmed on-shift minutes in the rolling window, less absence and committed assignments.
- **Worked minutes**: actual technician effort, attributed separately for each member of a team.
- **Load ratio**: (actual worked minutes + weighted remaining planned minutes) / max(eligible available minutes, floor). Compare only technicians with meaningful shared eligibility; zero-availability people are excluded.
- **Skill confidence**: verified qualification or supervised experience by category, not a model guess.
- **Training coverage**: categories/mentors completed and signed off for a new technician.

A worked-minutes-only ratio can disadvantage slower trainees; report training separately and use configurable mentoring credit for the mentor. Use category and shift comparisons alongside the global figure. Avoid a permanent score based on historical ticket count.

## Candidate selection

1. Route to a staff service pool according to approved category rules. Unknown or sensitive cases go to triage.
2. Determine task duration, minimum crew, deadline, location and access requirements. If any are unclear, hold for review or use an explicit safe default.
3. Build technician candidates with confirmed overlap, remaining capacity, required access, and qualifications. Enforce mentor pairing if a trainee cannot do the task alone.
4. Enumerate feasible crews of minimum size. Prefer a second technician only when duration, safety, training, or coverage requires it. Reserve capacity for other queued tickets; evaluate the whole current queue before finalizing assignments.
5. Rank feasible assignments lexicographically: meet urgency and deadlines; cover required skills and mentorship; minimize maximum projected workload ratio within a comparable pool; improve trainee category/mentor coverage; prefer verified specialization; use stable ticket and technician IDs to break ties.
6. Save the candidate set, projected ratios, rule decisions, policy version, and tie-break. If no feasible crew exists, queue with a reason and escalate at the approved threshold.

Lexicographic priorities keep a skill or deadline from being traded away for a tiny fairness gain. Specialization helps among feasible candidates, but its weight cannot overwhelm documented imbalance. All thresholds, capacity estimates, and crew-size rules are configurable and versioned by authorized staff.

## Example

A 20-computer lab task requires two people for two hours, so it represents four person-hours. With four eligible technicians on shift, assign two whose projected normalized loads are lower, subject to skills and training coverage. Keep the other two available for another ticket. If the first pair each work two hours, record two hours per person; when comparable future lab work arrives, previously lighter eligible technicians will tend to win. A technician who works one hour because of a handoff is credited for one hour, not the whole lab ticket.

## Status and rescheduling

On absence, blocked work, deadline change, or new urgent ticket, reconsider *unstarted* assignments and seek a safe handoff for work in progress. Record a reassignment event and notify affected people. Do not silently reshuffle started tasks. Freeze past decisions and keep historical snapshots so reports remain reproducible.

## Evaluation before rollout

Run the policy against synthetic weeks and, if approved, de-identified past tickets. Measure deadline misses, unassigned work, availability violations, category-specific disparity, training coverage, switches between jobs, and override rates. Compare to existing practice in shadow mode. Ask techs and staff whether explanations match their experience; revise policy with a versioned change log. Never claim the algorithm guarantees fairness without agreed metrics and measured results.
