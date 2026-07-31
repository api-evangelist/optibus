---
name: Manage vehicles and downtimes
description: Read and update Optibus vehicle fleet data and vehicle downtimes from a fleet management system.
api: openapi/optibus-operations-openapi.yml
operations: [GetVehiclesInfoV1, PostVehicles, PutVehicles, GetVehiclesDowntimes, PutVehiclesDowntimes]
---

# Manage vehicles and downtimes

Keep the Optibus vehicle fleet in sync with an external Fleet Management System.

## Auth
`Authorization: <API_KEY>` + `X-Optibus-Api-Client: <ACCOUNT_NAME>`.

## Steps
1. `GetVehiclesInfoV1` — read the current fleet.
2. `PostVehicles` / `PutVehicles` — create or update vehicles to match the FMS.
3. `GetVehiclesDowntimes` — read scheduled/active downtimes.
4. `PutVehiclesDowntimes` — write downtime windows when a vehicle goes out of service in the FMS.

## Rules
- Prefer the non-deprecated `/v1/vehicles` operations; `GetVehiclesInfo` (`/vehicles`) is deprecated.
- Batch-size aware: large writes may return 413 — size against `GET /v2/calculation-limit`.
