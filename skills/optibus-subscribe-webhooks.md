---
name: Subscribe to operational webhooks
description: Receive and verify Optibus operational event webhooks (duty cancel/reactivate/delete) as they happen.
api: openapi/optibus-operations-openapi.yml
operations: [EventWebhookPost]
---

# Subscribe to operational webhooks

Receive real-time operational changes from Optibus OPS as outbound HTTP webhooks.

## Setup (provided to Optibus CSM)
- Callback URL, subscription window (relative operational-day range), the `action_types` you want, and your operational-day start time.

## Verify every request
1. Read the raw JSON body and the `X-HMAC-SIGNATURE` header.
2. Compute `base64(HMAC-SHA256(secret, body))` and compare; reject on mismatch.
3. Process events sharing an `aggregate_id` sequentially to preserve correctness.

## Payload
ODS-inspired entities: `runs`, `run_assignments`, `run_events`, `blocks`, `block_assignments`. Identify entities by `run_id`/`block_id` (not the `_internal_id` fields). Known action types: `cancel_duty`, `reactivate_duty`, `delete_duty`.

See asyncapi/optibus-operational-webhooks.yml.
