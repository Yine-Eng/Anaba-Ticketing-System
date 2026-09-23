# Anaba

Anaba is a proposed ticket routing and workload balancing system for a university IT department. It is currently **in planning**; no production integration or deployment has been approved.

The core problem: student IT technicians have different schedules, capabilities, and workloads. Assigning the next ticket to whoever looks free can repeatedly give the same people more work. Anaba will make assignments explainable, account for estimated effort and actual work, and pair new technicians with mentors across varied tasks.

## Proposed workflow

1. Ingest a help request from the existing ticket system, initially through a mock adapter.
2. Classify it into an approved service category and route it to the appropriate staff pool. Unknown, sensitive, urgent, or low-confidence requests go to a triage queue.
3. For technician work, filter candidates by published availability, capability, required access, onboarding constraints, and estimated capacity.
4. Use a deterministic, versioned assignment policy to choose a technician or small team. Record the inputs and explanation.
5. Notify assigned workers, collect status and actual effort, and reconcile changes back to the source ticket system when integration is approved.
6. Show workload, aging, completion, and fairness metrics to authorized viewers.

Classification can later use an LLM to **suggest** a category or skill tags. An LLM will not decide who gets work, grant access, or perform password or account changes.

## First release

A responsive, authenticated technician site; schedule and absence entry; synthetic tickets; staff categories; explainable assignments; onboarding pairs; status updates; and a read-only operations dashboard. Begin with a simulated feed and shadow mode, in which suggested assignments are compared with human assignments. See [product requirements](docs/product-requirements.md), [assignment design](docs/assignment-policy.md), and [roadmap](docs/roadmap.md).

## Tentative technology

Python with FastAPI, PostgreSQL, a background worker, and a responsive TypeScript web client (React is a reasonable choice). Use campus single sign-on if the university permits integration. An optional local model behind a separate service can be evaluated after a baseline is measured. Deployment, data retention, and any use of university ticket content require department approval.

The name **Anaba** is a working title. A crown-shaped A in gold could be explored as a logo, but typography and contrast must remain readable; check institutional branding and whether a personal name suits a departmental production system.
