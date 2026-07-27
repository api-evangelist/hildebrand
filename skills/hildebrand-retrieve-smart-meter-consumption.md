---
generated: '2026-07-27'
method: generated
name: Retrieve GB smart-meter consumption data
description: Authenticate against the Glow Platform, walk virtual entities to their resources, and pull half-hourly or daily electricity and gas consumption for a household.
api: openapi/hildebrand-glowmarkt-resource-system-swagger.json
operations: [usernamelogin, virtualentity.findAll, virtualentity.findResourcesbyVeId, resource.getFirstTime, resource.getLastTime, resource.getReading, resource.getCurrentReading]
source: >-
  Grounded in openapi/hildebrand-glowmarkt-user-system-swagger.json,
  openapi/hildebrand-glowmarkt-virtual-entity-system-swagger.json and
  openapi/hildebrand-glowmarkt-resource-system-swagger.json; every operationId verified verbatim.
  Conventions and limits from conventions/hildebrand-conventions.yml (sourced from the official
  individual-user PDF v1.8).
---

# Retrieve GB smart-meter consumption data

The canonical read path through the Glow Platform: token -> virtual entity -> resources -> readings.

## Auth
- Every request carries TWO headers: `token` (JWT) and `applicationId` (UUID). There is no
  `Authorization` header.
- Get the token with `usernamelogin` (`POST /api/v0-1/auth`), body `{"username": "...", "password": "..."}`,
  with the `applicationId` header already set. The response contains `token` and `exp`.
- Tokens expire after 7 days. Cache and reuse; do not re-authenticate per call.
- Individual Bright users call with the published applicationId
  `b0f1b774-a586-4f72-9edd-27ead8aa7a8d` and can only ever see their OWN data. Organisations use
  their own contracted applicationId. See `authentication/hildebrand-authentication.yml`.

## Idempotency
- Not supported. There is no `Idempotency-Key` header on this API. Everything in this skill is a
  read, so retries are safe; do not blind-retry the write operations elsewhere in the platform.

## Steps
1. **Authenticate** — `usernamelogin` (`POST /auth`). Keep `token`; note `exp`.
2. **List the homes/sites** — `virtualentity.findAll` (`GET /virtualentity`). Returns an array of
   virtual entities, each with `veId`, `name` and a `resources[]` array of
   `{resourceId, resourceTypeId}` pairs.
3. **Resolve the data streams** — `virtualentity.findResourcesbyVeId`
   (`GET /virtualentity/{id}/resources`) for the chosen `veId`. This returns each resource in full,
   including `classifier` and `baseUnit`. Pick by classifier:
   `electricity.consumption` (kWh), `gas.consumption` (kWh), `electricity.export` (kWh),
   `electricity.consumption.cost` / `gas.consumption.cost` (pence).
4. **Bound the window (optional but recommended)** — `resource.getFirstTime`
   (`GET /resource/{id}/first-time`) and `resource.getLastTime` (`GET /resource/{id}/last-time`)
   give the UTC extent of available data. History runs to roughly 13 months.
5. **Pull the time series** — `resource.getReading`
   (`GET /resource/{id}/readings?from&to&period&offset&function`).
   - `from`/`to`: `yyyy-mm-ddThh:mm:ss`, no timezone suffix.
   - `period`: `PT1M` (electricity only), `PT30M`, `PT1H`, `P1D`, `P1W`, `P1M`, `P1Y`.
   - `offset`: minutes between your timezone and UTC, sign-inverted — BST is `-60`, US East Coast
     is `+300`.
   - `function`: `sum` for a total per period.
   - Response: `{"status":"OK", ..., "data": [[utc_epoch_seconds, value], ...]}`.
6. **Or read the live value** — `resource.getCurrentReading` (`GET /resource/{id}/current`) returns
   a single `[timestamp, value]`. With Glow hardware it refreshes every 6-10 seconds. For cost
   resources this returns power (electricity) or the cumulative meter reading (gas) — Glow
   deliberately does not extrapolate a cost from an instantaneous power reading.

## Query windows (hard limits)
The maximum `to - from` span depends on `period`. Chunk longer ranges into successive calls:

| period | max span |
|---|---|
| PT30M | 10 days |
| PT1H | 31 days |
| P1D | 31 days |
| P1W | 6 weeks |
| P1M | 366 days |
| P1Y | 366 days |

For `P1W` and `P1M` the start date must be a Monday / the 1st of the month respectively.

## Errors
- `400 {"error":"missing elements"}` — a header is missing. Anonymous calls return 400, not 401.
- `401 {"error":"Access denied"}` — token expired (7 days) or not entitled to that resource;
  re-run step 1.
- `500 {"error":"An error has occurred"}` — platform error; back off and retry.
- Full catalogue: `errors/hildebrand-problem-types.yml`.

## Notes
- There is no pagination anywhere; collections return in full and volume is bounded by the query
  windows above.
- No rate limits or throttling headers are published. Poll considerately — half-hourly DCC data
  does not change more than twice an hour.
- If readings look stale for a DCC-sourced (non-hardware) meter, see the DCC catchup skill.
