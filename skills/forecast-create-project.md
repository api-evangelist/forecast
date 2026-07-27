---
name: forecast-create-project
description: Create a Forecast project for a client and add tasks to it.
api: Forecast API
base_url: https://api.forecast.it/api/v1/
operations:
- GET /v1/clients
- POST /v1/projects
- GET /v1/projects/{projectId}
- POST /v3/tasks
operations_generated: '2026-07-19'
generated: '2026-07-19'
method: generated
source: https://github.com/Forecast-it/API
---

# Create a project in Forecast

Stand up a new project, attach it to a client, and seed it with tasks.

## Prerequisites
- API key in `X-FORECAST-API-KEY`; JSON `Content-Type` on writes.

## Steps
1. (Optional) Resolve the client: `GET /v1/clients`, note the client `id`.
2. Create the project: `POST /v1/projects` with `name`, optional `client`,
   `stage` (PLANNING/RUNNING/HALTED/DONE), `budget_type`, and dates. Returns `201`.
3. Read it back: `GET /v1/projects/{projectId}` (add `?includeProgress=true` for progress).
4. Add tasks: `POST /v3/tasks` referencing the new project id.

## Conventions & errors
- Per-resource versioning: projects are v1, tasks are v3/v4 — use the version in the path.
- Errors are `{ "status", "message" }`; `400` explains invalid input, `404` = bad id.
- See ../conventions/forecast-conventions.yml and ../data-model/forecast-data-model.yml.
