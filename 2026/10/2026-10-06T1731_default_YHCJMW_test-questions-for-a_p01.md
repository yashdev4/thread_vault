---
"schema_version": 2
"thread_id": "01M494ADT5G6AGMGQ6AZYHCJMW"
"title": "Test Questions for AskCruz and EOXS Connectors"
"slug": "test-questions-for-a"
"account": "default"
"client": "remote"
"model": ""
"created": "2026-10-06T17:31:28.452981+00:00"
"updated": "2026-10-06T17:32:48.804158+00:00"
"page": 1
"prev": null
"next": null
"turn_count": 2
"turn_range":
- 1
- 1
"bytes": 2625
"gaps": []
"redacted": false
"tags": []
"open_turn": null
"paused": false
"nonce": "5832"
---


# Test Questions for AskCruz and EOXS Connectors

---

<!-- turn i=1 role=user ts=2026-10-06T17:31:28.456069+00:00 fidelity=verbatim chars=106 hash=c48b7815 anchor="give me the list of question to ask from" turn_key=2822e53b97c12aaf98e58bcfae4e61cc94a0aa9f80f6166aede9633327f3dfeb nonce=5832 -->
## User

give me the list of question to ask from the askcruz connectors and eoxs to test those connectors response
<!-- /turn i=1 nonce=5832 -->

---

<!-- turn i=1 role=assistant fidelity=reported chars=1548 hash=c0cee4fb nonce=5832 -->
## Claude

Here are 10 test questions to validate AskCruz and EOXS connector responses:

1. **List all active projects in the AskCruz Odoo instance** — Tests `teams-askcruz.list_tables()` and `get_business_schema()`

2. **What tasks are currently assigned to Dhanshree in the AskCruz project?** — Tests `teams-askcruz.query()` with project_task and res_users join

3. **Show me the last 5 email threads involving support tickets** — Tests `eoxs-db.search_emails()` with keyword filtering

4. **What's the current status and stage of all open support tickets in EOXS Teams?** — Tests `eoxs-teams.query()` against ticket/stage tables

5. **List all EOXS clients and their primary contact names** — Tests `eoxs-db.list_clients()` and `eoxs-db.list_contacts()`

6. **Fetch the client profile for a specific account including recent interactions** — Tests `eoxs-db.get_client_profile()` with correspondence context

7. **What are the pending implementation tasks grouped by status?** — Tests `eoxs-db.list_implementation_tasks()` or `search_implementation_tasks()`

8. **Show recent sales orders or invoices from EOXS Teams Odoo** — Tests `eoxs-teams.query()` against account_invoice or sale_order tables

9. **Search the internal wiki for a specific topic and return synthesized pages** — Tests `eoxs-db.search_wiki()` with text matching

10. **Get a specific call transcript and validate extracted metadata** — Tests `eoxs-db.get_call()` with proper ID reference

These span read queries, relationship joins, synthesized data, and raw SQL across both connectors.
<!-- /turn i=1 nonce=5832 -->
