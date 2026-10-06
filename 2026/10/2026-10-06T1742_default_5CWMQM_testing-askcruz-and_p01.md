---
"schema_version": 2
"thread_id": "01M494Z88B9XF1STKDXJ5CWMQM"
"title": "Testing AskCruz and EOXS Connectors"
"slug": "testing-askcruz-and"
"account": "default"
"client": "remote"
"model": ""
"created": "2026-10-06T17:42:50.891684+00:00"
"updated": "2026-10-06T17:43:19.625927+00:00"
"page": 1
"prev": null
"next": null
"turn_count": 2
"turn_range":
- 1
- 1
"bytes": 2447
"gaps": []
"redacted": false
"tags": []
"open_turn": null
"paused": false
"nonce": "1ece"
---


# Testing AskCruz and EOXS Connectors

---

<!-- turn i=1 role=user ts=2026-10-06T17:42:50.894458+00:00 fidelity=verbatim chars=106 hash=c48b7815 anchor="give me the list of question to ask from" turn_key=2822e53b97c12aaf98e58bcfae4e61cc94a0aa9f80f6166aede9633327f3dfeb nonce=1ece -->
## User

give me the list of question to ask from the askcruz connectors and eoxs to test those connectors response
<!-- /turn i=1 nonce=1ece -->

---

<!-- turn i=1 role=assistant fidelity=reported chars=1373 hash=b55bd6cb nonce=1ece -->
## Claude

1. **Get client profile** — "What's the full contact and background info for [Client Name]?" → `get_client_profile()`

2. **Search emails** — "Find all emails mentioning [topic/client name]" → `search_emails()`

3. **Get specific email** — "Show me the full email thread about [specific subject]" → `get_email(id)`

4. **Search calls** — "What calls did we have with [person/client name]?" → `search_calls()`

5. **Get call transcript** — "Show me the full transcript from the call on [date]" → `get_call(id)`

6. **Search implementation tasks** — "What implementation work is happening for [client name]?" → `search_implementation_tasks()`

7. **Search internal assets/docs** — "What's our SOP for [process name]?" → `search_assets()`

8. **Search wiki** — "Find synthesis pages about [topic/client]" → `search_wiki()`

9. **Query eoxs-teams (CRM/tickets/invoices)** — "What's the pipeline stage and revenue for [prospect/deal name]?" or "List all open support tickets for [client]" → `query()` on eoxs-teams

10. **Query teams-askcruz (project tasks)** — "What tasks is [person name] assigned to on the askcruz project?" or "Show all tasks in [stage] with deadline coming up" → `query()` on teams-askcruz

---

These 10 will test: client retrieval, correspondence (emails/calls), internal documentation, CRM/sales data, and project management across all three connectors.
<!-- /turn i=1 nonce=1ece -->
