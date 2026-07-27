---
name: forecast-webhook-subscribe
description: Subscribe to Forecast task/project/phase/time events via webhooks and verify delivery.
api: Forecast API
base_url: https://api.forecast.it/api/v1/
operations:
- GET /v1/webhook_subscriptions
- POST /v1/webhook_subscriptions
- DELETE /v1/webhook_subscriptions/{id}
generated: '2026-07-19'
method: generated
source: https://github.com/Forecast-it/API/blob/master/sections/webhook_subscriptions.md
---

# Subscribe to Forecast webhooks

Register a subscription so Forecast POSTs events to your endpoint.

## Prerequisites
- API key in `X-FORECAST-API-KEY`; a public HTTPS URL that returns 2xx quickly.

## Steps
1. List existing subscriptions: `GET /v1/webhook_subscriptions`.
2. Create one: `POST /v1/webhook_subscriptions` with `name`, `type`
   (TASK | TIME_REG | PROJECT | PHASE), `event` (CREATE | UPDATE | DELETE),
   `url`, and `active: true`.
3. Receive events: Forecast POSTs `{ timestamp, event, object.id, person.id, fields_changed }`.
   Respond 2xx fast; non-2xx triggers up to 5 retries (1/2/3/5/10 min backoff).
4. Remove when done: `DELETE /v1/webhook_subscriptions/{id}`.

## Notes
- `fields_changed` is only present on UPDATE events.
- See ../asyncapi/forecast-webhooks.yml for the full event catalog.
