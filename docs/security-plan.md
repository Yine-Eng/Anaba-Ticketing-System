# Security plan and evidence checklist

**Status:** proposed controls for a senior project; none are implemented or independently verified yet. A secure deployment cannot be established by a README or a claim that the app is self-hosted. Approval and technical verification belong to the university's responsible IT/security staff.

## Trust boundaries

Requester ticket text and attachments are untrusted. The ticket platform, Anaba API, database, browser, and optional model have separate privileges. The public GitHub repository contains no real tickets, student schedules, names, tokens, or credentials. A mock dataset is the default for development and demonstrations.

## Controls to design and test

| Area | Proposed control | Evidence before a live pilot |
| --- | --- | --- |
| Identity | Campus-managed sign-in and MFA if approved; no shared admin login. | Documented identity flow and tests for terminated/changed roles. |
| Authorization | Server-side role and per-ticket checks; deny by default; separate technician, manager, analyst, and operator privileges. | Tests showing users cannot view or mutate another team's records or promote themselves. |
| Data | Minimize fields, define retention and deletion with IT, protect traffic with TLS and storage/backups under university policy. | Data inventory, retention schedule, restore test, and approved hosting location. |
| Secrets | Store API tokens outside source control; scope and rotate them; restrict service accounts. | Secret scan, permission review, rotation/runbook test. |
| Integration | Verify webhook authenticity using the provider's supported mechanism; otherwise use a controlled polling adapter. Validate input, deduplicate events, rate-limit, retry safely, and reconcile missed events. | Replay, malformed-event, sync failure, and permission tests. |
| AI | Keep ticket text as data, use an allowlisted output schema, review uncertain or sensitive classifications, and keep operational actions outside the model. Keep a local model endpoint private. | Prompt-injection cases, category evaluation, privacy review, and fallback demonstration. |
| Audit and recovery | Record logins, role/policy changes, decisions and overrides without logging secrets or unnecessary ticket content; protect logs and monitor errors. | Audit samples, alert and incident runbook, backup restoration and rollback drill. |
| Web app | Validate inputs and uploads; protect sessions and state changes; keep dependencies patched. | Automated tests, dependency review, OWASP ASVS-based review, and university security sign-off. |

## Safe progression

1. Build and test solely with invented records.
2. Have staff and the university security owner review a data-flow diagram, access matrix, and deployment plan.
3. If approved, start with minimum-scope read-only integration and compare recommendations in shadow mode.
4. Permit live assignment or ticket updates only after security review, rollback rehearsal, and an identified operations owner.

The claim to make in a meeting is: **"I have a plan for how security will be verified, and I will not use real ticket data or connect to campus systems without your approval."** Do not claim the app is already secure.

## Reference standards

- OWASP Application Security Verification Standard: https://owasp.org/www-project-application-security-verification-standard/
- OWASP Authorization Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
- OWASP Logging Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html
- OWASP LLM Prompt Injection: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
