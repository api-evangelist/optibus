---
name: Read the operational plan and payroll
description: Retrieve Optibus operational plans, work entities, statistics and payroll for downstream reporting.
api: openapi/optibus-operations-openapi.yml
operations: [GetOperationalPlanV2, GetWorkEntities, GetPayroll, GetStats, GetRoster]
---

# Read the operational plan and payroll

Extract the planned/actual operational picture for reporting and payroll.

## Auth
`Authorization: <API_KEY>` + `X-Optibus-Api-Client: <ACCOUNT_NAME>`.

## Steps
1. `GetOperationalPlanV2` — the current operational plan (prefer v2; `/v1/operational-plan` variants are deprecated).
2. `GetRoster` — driver roster for the period.
3. `GetWorkEntities` — work entities underlying duties.
4. `GetStats` / `GetPayroll` — statistics and payroll figures.

## Rules
- Dense days: when `daysLimit` is 0 from `GetDutyStatsCalculationLimit`, request a single day (`fromDate` == `toDate`) with at most `tasksLimit` task ids.
- Read-only flow; no writes.
