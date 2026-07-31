---
name: Sync driver absences to an HR system
description: Read Optibus driver rosters and absences and reconcile them into an external HR/payroll system.
api: openapi/optibus-operations-openapi.yml
operations: [GetDriversV2, GetAbsencesV2, PostDriverAbsences, GetTimeOffBalances, GetAbsenceQuotas]
---

# Sync driver absences to an HR system

Optibus is the system of record for driver operational data. This skill pulls drivers and their absences and pushes/reconciles absence records.

## Auth
Send `Authorization: <API_KEY>` and `X-Optibus-Api-Client: <ACCOUNT_NAME>` on every request. The account-specific `BASE_URL` is provisioned by your Optibus Customer Success Manager.

## Steps
1. `GetDriversV2` — list active drivers to establish the roster you are syncing.
2. `GetAbsencesV2` — fetch driver absences for the date window (use `fromDate`/`toDate` filters; long GET URIs over 10240 bytes return 414 — switch to POST query variants).
3. `GetTimeOffBalances` / `GetAbsenceQuotas` — read remaining balances/quotas before writing new absences.
4. `PostDriverAbsences` — create absences originating in the HR system back into Optibus.

## Rules
- Not idempotent: there is no idempotency key. De-duplicate on your side before POSTing.
- Errors use a typed envelope `{ "error": { "type", "message", "details" } }` (see errors/optibus-problem-types.yml). Handle 409 `conflictProcessingRequest` with retry/backoff.
