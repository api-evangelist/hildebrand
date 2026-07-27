---
generated: '2026-07-27'
method: generated
name: Inspect a meter point, its DCC inventory and Glow hardware
description: Look up the DCC inventory of a GB meter point by MPxN or smart-meter EUI, resolve its resources, check gateway health, and force a DCC catchup when readings go stale.
api: openapi/hildebrand-glowmarkt-device-management-system-swagger.json
operations: [usernamelogin, device.getMeterPointInventory, device.getMeterPointInventoryByEUI, device.getMeterPointResources, device.findAll, device.findById, device.findByResourceId, device.getStatusbyDeviceId, device.getStatusbyHardwareId, resource.catchUpReadings, resource.getDailyConsumptionLog]
source: >-
  Grounded in openapi/hildebrand-glowmarkt-device-management-system-swagger.json and
  openapi/hildebrand-glowmarkt-resource-system-swagger.json; every operationId verified verbatim.
  Hildebrand's DCC reach is the SEC Party / DCC Other User registration PLK001 (see review.yml).
---

# Inspect a meter point, its DCC inventory and Glow hardware

This is the diagnostic path: what hardware is at this meter point, is it talking, and why is the
data stale. It is also the clearest evidence of Hildebrand's DCC connection — these operations read
the national smart-metering inventory, not just Glow's own devices.

## Auth
- `token` + `applicationId` headers on every call; token from `usernamelogin` (`POST /auth`).
- Several device operations also expect a `userId` header — a missing one returns
  `400 {"error":"missing elements -userId"}`.

## Steps
1. **DCC inventory by meter point** — `device.getMeterPointInventory`
   (`GET /device/meter-point/{meterPointNumber}/inventory`) with the MPxN (MPAN for electricity,
   MPRN for gas). Returns per-device records: `DeviceManufacturer`, `DeviceModel`,
   `DeviceFirmwareVersion`, `DeviceType`, `DeviceStatus`, `EUI`, `SmetsVersion`,
   `DateCommissioned`, `ImportMPxN`.
2. **Or by EUI** — `device.getMeterPointInventoryByEUI`
   (`GET /device/smart-meter/{eui}/inventory`) when you have the meter's EUI rather than the MPxN.
3. **Resolve the meter point's data streams** — `device.getMeterPointResources`
   (`GET /device/meter-point/{meterPointNumber}/resources`) to bridge from a meter point straight to
   resource ids without walking virtual entities.
4. **Glow hardware inventory** — `device.findAll` (`GET /device`) for the user's devices,
   `device.findById` (`GET /device/{id}`) for one, and `device.findByResourceId`
   (`GET /device/resource/{resourceId}`) to find which device sources a given data stream.
5. **Is the gateway alive?** — `device.getStatusbyDeviceId` (`GET /device/{id}/status`) or
   `device.getStatusbyHardwareId` (`GET /device/status`) — both report whether a gateway is sending
   packets. Use this before blaming the data pipeline.
6. **Force a DCC catchup** — `resource.catchUpReadings` (`GET /resource/{id}/catchup`) triggers a
   request to retrieve the latest available readings from the DCC for a resource. Use sparingly;
   DCC-sourced half-hourly data is delayed by design.
7. **Daily consumption log** — `resource.getDailyConsumptionLog`
   (`GET /resource/{id}/daily-consumption-log`) returns the DCC daily consumption log for
   reconciliation against the half-hourly series.

## Errors
- `400 {"error":"missing elements -userId"}` — add the `userId` header.
- `404` — unknown MPxN/EUI/device id, or not visible to this application.
- `401 {"error":"Access denied"}` — expired token or no entitlement to that meter point.
- Full catalogue: `errors/hildebrand-problem-types.yml`.

## Notes
- Meter-point inventory reads are consent-gated exactly like data reads; an organisation must hold
  a valid per-MPxN consent (see the consent skill).
- Hardware-sourced data (Glow CAD/GlowStick) is near-real-time; DCC-sourced data is delayed
  half-hourly. Which one a resource uses determines whether a catchup will help at all.
- `resource.getGlowBinary` (`GET /resource/{id}/glowbinary`) returns the raw data in Hildebrand's
  proprietary Glow Binary format if you need the unprocessed stream.
