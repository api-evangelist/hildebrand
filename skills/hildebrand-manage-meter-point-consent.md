---
generated: '2026-07-27'
method: generated
name: Manage per-MPxN consent and verification
description: Check, renew and revoke a consumer's consent to share smart-meter data, per GB meter point (MPxN), through the Glowmarkt User System.
api: openapi/hildebrand-glowmarkt-user-system-swagger.json
operations: [usernamelogin, getUserMeterPointVerificationConsentStatus, getMeterPointConsentRenewal, renewMeterPointConsent, renewMeterPointConsentBulk, getMeterPointConsentRevocation, revokeMeterPointConsent, renewMeterPointConsentRevokeBulk]
source: >-
  Grounded in openapi/hildebrand-glowmarkt-user-system-swagger.json ("Meter Point Consent &
  Verification" tag); every operationId verified verbatim. Regulatory context from review.yml.
---

# Manage per-MPxN consent and verification

Great Britain mandated the smart-metering infrastructure, not a consumer data right — so this
consent model is Hildebrand's own product decision, not a compliance API. It is nonetheless the
gate on every byte of third-party data access: an organisation may only retrieve data for a meter
point where the consumer has verified their right to grant consent and that consent is still valid.

## Auth
- `token` + `applicationId` headers on every call, as always. Organisational access uses your
  contracted `applicationId`; individual Bright users cannot manage anyone else's consent.
- Token from `usernamelogin` (`POST /auth`), 7-day lifetime. See
  `authentication/hildebrand-authentication.yml`.

## Idempotency
- Not supported — there is no `Idempotency-Key` header. Renewal and revocation are WRITES. Do not
  blind-retry on timeout: re-read the status with
  `getUserMeterPointVerificationConsentStatus` first and only then retry.

## Steps
1. **Read current state** — `getUserMeterPointVerificationConsentStatus`
   (`GET /user/verification/status`) returns the caller's meter points with
   `isVerified`, `isValidUntil`, `mpxn` and `mpxnKey`. Treat `isValidUntil` as the expiry you must
   renew before.
2. **Renew one meter point** — `renewMeterPointConsent`
   (`POST /user/verification/status/mpxn/{mpxn}/renewal`). Read the renewal record back with
   `getMeterPointConsentRenewal` (`GET /user/verification/status/mpxn/{mpxn}/renewal`).
3. **Renew many at once** — `renewMeterPointConsentBulk`
   (`POST /user/verification/status/mpxns/renewal`) with the MPxN list in the body. Use this for
   portfolio-scale renewal rather than looping step 2.
4. **Revoke one meter point** — `revokeMeterPointConsent`
   (`POST /user/verification/status/mpxn/{mpxn}/revocation`); read it back with
   `getMeterPointConsentRevocation` (`GET /user/verification/status/mpxn/{mpxn}/revocation`).
5. **Revoke many at once** — `renewMeterPointConsentRevokeBulk`
   (`POST /user/verification/status/mpxns/revocation`).

## Rules
- Consent is scoped to a single meter point (MPxN — MPAN for electricity, MPRN for gas), never to a
  customer as a whole. A dual-fuel household is two consents.
- Verification (`isVerified`) is separate from consent: the consumer must first prove their right
  to grant it. Glow publishes nine verification methods for domestic and non-domestic consumers,
  including the Glow Agent Portal for on-site verification during a site visit.
- Revocation must stop data retrieval immediately — do not keep serving cached readings for a
  revoked MPxN.
- A revoked or expired consent surfaces downstream as `401 {"error":"Access denied"}` on the
  Resource System, not as a distinct consent error.

## Errors
- `400 {"error":"missing elements"}` / `{"error":"incorrect elements"}` — bad or absent MPxN.
- `401 {"error":"Access denied"}` — token expired, or the application is not entitled to that
  meter point.
- `500 {"error":"An error has occurred"}`.
- Full catalogue: `errors/hildebrand-problem-types.yml`.

## Notes
- Organisational consent management requires a Glow Data Service contract; see
  `plans/hildebrand-plans.yml`.
- Keep your own audit trail: the API returns current state, not a consent history.
