---
generated: '2026-07-27'
method: generated
name: Read tariffs and calculate energy cost
description: Pull the tariff applied to a cost resource, its history, and the matching cost time series so an application can show spend alongside consumption.
api: openapi/hildebrand-glowmarkt-resource-system-swagger.json
operations: [usernamelogin, virtualentity.findResourcesbyVeId, resource.getTariff, resource.getTariffHistory, resource.getReading, resource.getCurrentReading, resource.getMeterRead]
source: >-
  Grounded in openapi/hildebrand-glowmarkt-resource-system-swagger.json and
  openapi/hildebrand-glowmarkt-virtual-entity-system-swagger.json; every operationId verified
  verbatim. Cost semantics quoted from the official individual-user PDF v1.8.
---

# Read tariffs and calculate energy cost

Glow models cost as its own resource stream rather than as a computed field. Consumption and cost
are separate resources on the same virtual entity.

## Auth
- `token` + `applicationId` headers on every call; token from `usernamelogin` (`POST /auth`),
  7-day lifetime.

## Steps
1. **Find the cost resources** — `virtualentity.findResourcesbyVeId`
   (`GET /virtualentity/{id}/resources`) and select by `classifier`:
   `electricity.consumption.cost` and `gas.consumption.cost` (both `baseUnit: pence`).
2. **Get the current tariff** — `resource.getTariff` (`GET /resource/{id}/tariff`) against a COST
   resource. Returns the latest unit rate / standing charge applied to that stream.
3. **Get the tariff history** — `resource.getTariffHistory` (`GET /resource/{id}/tariff-list`) when
   you need to reprice a historical window across a rate change.
4. **Pull the cost series** — `resource.getReading` on the cost resource, same
   `from`/`to`/`period`/`offset`/`function=sum` contract and the same per-period window caps as
   consumption. Values are pence.
5. **Live spend rate** — `resource.getCurrentReading` (`GET /resource/{id}/current`) on a cost
   resource returns POWER for electricity (not a cost) and the CUMULATIVE meter reading for gas.
   Glow deliberately refuses to extrapolate a cost from an instantaneous power reading. Bright
   itself computes "cost if this power ran for an hour" by combining the instantaneous electricity
   consumption with the unit rate from `resource.getTariff` — do the same rather than expecting the
   API to do it.
6. **Cumulative meter read (optional)** — `resource.getMeterRead`
   (`GET /resource/{id}/meterread`) returns the cumulative value reported on the metering device.
   Not supported for all resource types; handle a non-200 gracefully.

## Errors
- `401 {"error":"Access denied"}` — expired token or a resource the caller is not entitled to.
- `500 {"error":"An error has occurred"}`.
- Full catalogue: `errors/hildebrand-problem-types.yml`.

## Notes
- Cost resources exist only where a tariff is known to the platform; a household may have
  consumption resources with no matching cost resource.
- Gas cost calculations against the cumulative reading are not meaningful — use the gas cost
  resource's time series instead.
- Window caps and the `offset` convention are identical to the consumption skill; see
  `conventions/hildebrand-conventions.yml`.
