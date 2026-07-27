---
name: forecast-log-time
description: Log time against a Forecast task or project and confirm it was recorded.
api: Forecast API
base_url: https://api.forecast.it/api/v1/
operations:
- GET /v4/tasks
- GET /v3/tasks/{taskId}
- POST /v1/time_registrations
- GET /v4/time_registrations
generated: '2026-07-19'
method: generated
source: https://github.com/Forecast-it/API
---

# Log time in Forecast

Record a time registration against a task (or project) for a person.

## Prerequisites
- A Forecast API key sent in the `X-FORECAST-API-KEY` header on every request.
- JSON only: send `Content-Type: application/json; charset=utf-8` on writes.

## Steps
1. Find the target task: `GET /v4/tasks` (paginated with `pageNumber`/`pageSize`)
   or `GET /v3/tasks/{taskId}` if you already have the id. Note its `id` and `project_id`.
2. Create the time registration: `POST /v1/time_registrations` with the person id,
   task/project reference, date, and minutes.
3. On success you get `201 CREATED` and the created object echoed back.
4. Verify: `GET /v4/time_registrations` (optionally `.../date_after/YYYYMMDD`).

## Conventions & errors
- No idempotency keys: a repeated POST creates a duplicate registration — guard client-side.
- Errors are `{ "status", "message" }`; `401` = bad API key, `415` = missing JSON Content-Type.
- See ../conventions/forecast-conventions.yml and ../errors/forecast-problem-types.yml.
