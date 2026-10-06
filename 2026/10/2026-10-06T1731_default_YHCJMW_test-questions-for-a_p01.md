---
"schema_version": 2
"thread_id": "01M494ADT5G6AGMGQ6AZYHCJMW"
"title": "Test Questions for AskCruz and EOXS Connectors"
"slug": "test-questions-for-a"
"account": "default"
"client": "remote"
"model": ""
"created": "2026-10-06T17:31:28.452981+00:00"
"updated": "2026-10-06T17:40:00.338234+00:00"
"page": 1
"prev": null
"next": null
"turn_count": 6
"turn_range":
- 1
- 3
"bytes": 6665
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

---

<!-- turn i=2 role=user ts=2026-10-06T17:37:02.117717+00:00 fidelity=verbatim chars=78 hash=0eff3358 anchor="list all active projects in the askcruz " turn_key=963254377714ce14e72338163c4e0703b2924d7c1a4f8e8dadec2c815a339797 nonce=5832 -->
## User

List all active projects in the AskCruz Odoo instance using askcruz connectors
<!-- /turn i=2 nonce=5832 -->

---

<!-- turn i=2 role=assistant fidelity=reported chars=1081 hash=83fbd57b nonce=5832 -->
## Claude

All active projects in AskCruz Odoo instance (15 total):

| ID | Project Name | Owner ID | Created | Privacy |
|---|---|---|---|---|
| 23 | GTM - PR Board | 17 | 2026-09-24 | portal |
| 21 | GTM - LinkedIn Outreach | 18 | 2026-09-24 | portal |
| 20 | GTM - Email Marketing | 18 | 2026-09-24 | portal |
| 18 | Customer 3 - Sabre Alloys | 6 | 2026-09-07 | portal |
| 17 | Team Sales | 12 | 2026-08-27 | portal |
| 16 | Ai/Product Interns | 16 | 2026-08-25 | portal |
| 14 | Customer 2 - 3GM | 7 | 2026-08-21 | portal |
| 12 | HR | 19 | 2026-08-19 | portal |
| 11 | GTM - Data Extraction | 6 | 2026-08-18 | portal |
| 9 | Hiring Funnels | 7 | 2026-08-07 | portal |
| 7 | Idea Board | 6 | 2026-08-05 | portal |
| 6 | AskCruz | 17 | 2026-08-05 | portal |
| 5 | Daily Snippets | 7 | 2026-08-05 | portal |
| 4 | Customer 1 - EOXS | 6 | 2026-08-04 | portal |
| 3 | 50 MBA Inters Cohert | 6 | 2026-08-03 | portal |

Connector test result: Read-only connector successfully queried project_project table using SQL SELECT. Query returned 15 active projects, all with portal privacy visibility.
<!-- /turn i=2 nonce=5832 -->

---

<!-- turn i=3 role=user ts=2026-10-06T17:38:54.002535+00:00 fidelity=verbatim chars=74 hash=4f8a60d7 anchor="show recent sales orders or invoices fro" turn_key=43a28ad0587eba54b8cca3d2d11a86fd045137722a2987ac0f1b9b74aa3da375 nonce=5832 -->
## User

Show recent sales orders or invoices from EOXS Teams Odoo using connectors
<!-- /turn i=3 nonce=5832 -->

---

<!-- turn i=3 role=assistant fidelity=reported chars=1965 hash=f0d43a5f nonce=5832 -->
## Claude

Recent Sales Orders (Last 10):

| Order ID | Name | Date | State | Amount | Customer |
|---|---|---|---|---|---|
| 216 | S00216 | 2026-10-05 12:38 | sale | $9,720.00 | Sabre Alloys |
| 215 | S00215 | 2026-10-05 12:32 | sale | $3,959.00 | Discount Pipe & Steel |
| 214 | S00214 | 2026-10-05 12:24 | sale | $2,200.00 | PPC Speciality Metals |
| 213 | S00213 | 2026-09-24 17:04 | sale | $2,340.00 | Eastern Steel Sales |
| 212 | S00212 | 2026-09-07 20:44 | sale | $205.85 | Sabre Alloys |
| 208 | S00208 | 2026-09-04 12:28 | sale | $10,452.00 | Sabre Alloys |
| 210 | S00210 | 2026-08-28 18:35 | sale | $2,200.00 | PPC Speciality Metals |
| 211 | S00211 | 2026-08-28 18:35 | sale | $3,959.00 | Discount Pipe & Steel |
| 209 | S00209 | 2026-08-28 18:35 | sale | $2,340.00 | Eastern Steel Sales |
| 198 | S00198 | 2026-08-04 14:28 | sale | $3,569.00 | Discount Pipe & Steel |

Recent Customer Invoices (Last 10):

| Invoice ID | Number | Date | State | Amount | Customer | Payment Status |
|---|---|---|---|---|---|---|
| 924 | INV/2026/0409 | 2026-10-05 | posted | $9,720.00 | Sabre Alloys | not_paid |
| 923 | INV/2026/0403 | 2026-10-05 | posted | $3,959.00 | Discount Pipe & Steel | not_paid |
| 922 | INV/2026/0397 | 2026-10-05 | posted | $2,200.00 | PPC Speciality Metals | not_paid |
| 921 | INV/2026/0391 | 2026-09-24 | posted | $2,340.00 | Eastern Steel Sales | not_paid |
| 882 | INV/2026/0385 | 2026-09-09 | posted | $1,356.00 | Brannon Steel | not_paid |
| 894 | INV/2026/0373 | 2026-09-07 | posted | $3,959.00 | Discount Pipe & Steel | paid |
| 896 | INV/2026/0379 | 2026-09-07 | posted | $205.85 | Sabre Alloys | not_paid |
| 893 | / | 2026-09-06 | cancel | $3,000.00 | 3GM Steel | not_paid |
| 892 | INV/2026/0361 | 2026-09-04 | posted | $2,340.00 | Eastern Steel Sales | paid |
| 891 | INV/2026/0355 | 2026-09-04 | posted | $2,200.00 | PPC Speciality Metals | paid |

Connector: Eoxs-Teams. SQL queries executed against sale_order and account_move tables.
<!-- /turn i=3 nonce=5832 -->
