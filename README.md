# Hildebrand (hildebrand)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Hildebrand Technology Limited is a London-based energy data company and, since 2019, the United Kingdom's first independent DCC Other User with a direct connection to the Smart Data Communications Company network. It sits between Britain's mandated smart-metering infrastructure and the applications built on top of it: it makes Glow hardware (CADs, in-home displays, sub-meters, temperature sensors), ingests and stores smart-meter reads at scale, and republishes them through the Glowmarkt Platform APIs, the consumer Bright app, and the commercial Glow Data Service. Its API posture is an honest reflection of the British market seam — Britain mandated the metering INFRASTRUCTURE, not a consumer data right, so there is no Consumer Data Right or Green Button obligation on Hildebrand and no standards-conformant data-sharing surface to point at. What exists instead is a proprietary but genuinely well-documented platform: five public Swagger 2.0 definitions are served anonymously from api.glowmarkt.com/api-docs, and any individual who installs Bright, creates an account and passes meter-point verification can call the same production API for their own household data with a published applicationId. Third-party organisational access to other people's data is the closed half — it runs through Glow Data Service on a signed contract from GBP 595/month per MPxN, with consumer verification and consent captured per meter point. Hildebrand publishes no open grid or market data of any kind: every documented endpoint returns HTTP 400 without an applicationId header, so this is a closed-market-data, consent-gated-consumer-data provider.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/hildebrand/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/hildebrand/refs/heads/main/apis.yml)

## Tags

- Energy
- United Kingdom
- Utilities
- Electricity
- Gas
- Smart Metering
- Energy Data
- Demand Response
- IoT
- Metering

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### Glowmarkt User System API

User, account, authentication and consent management for the Glow Platform. Covers user registration, account profiles and sessions, JWT issuance via `POST /auth`, an OAuth 2.0 authorization-code grant (`POST /auth/oauth` and `POST /auth/oauth/access`), and — the part that matters most in the British smart-metering context — Meter Point Consent and Verification, where consent to retrieve data is renewed and revoked per MPxN.

- **Human URL:** [https://api.glowmarkt.com/api-docs/v0-1/usersys/usertypes/](https://api.glowmarkt.com/api-docs/v0-1/usersys/usertypes/)
- **Base URL:** `https://api.glowmarkt.com/api/v0-1`

#### Tags

- Users
- Accounts
- Authentication
- OAuth
- Consent
- Meter Points

#### Properties

- [OpenAPI](openapi/hildebrand-glowmarkt-user-system-swagger.json) — Swagger 2.0, 29 paths
- [API Reference](https://api.glowmarkt.com/api-docs/v0-1/usersys/usertypes/)
- [Documentation](https://docs.glowmarkt.com/GlowmarktAPIDataRetrievalDocumentationIndividualUserForBright.pdf)

### Glowmarkt Resource System API

Time-series energy data retrieval. A resource is a single data stream — electricity consumption, electricity cost, gas consumption, gas cost, electricity export, reactive import/export — each carrying a classifier such as `electricity.consumption` or `gas.consumption.cost`. Exposes historical readings with ISO 8601 aggregation periods (PT1M through P1Y), current readings, first/last reading times, cumulative meter reads, the tariff applied to a cost resource and its history, a DCC catchup trigger, a DCC daily consumption log, and raw data in Hildebrand's Glow Binary format.

- **Human URL:** [https://api.glowmarkt.com/api-docs/v0-1/resourcesys/](https://api.glowmarkt.com/api-docs/v0-1/resourcesys/)
- **Base URL:** `https://api.glowmarkt.com/api/v0-1`

#### Tags

- Energy Data
- Consumption
- Tariffs
- Time Series
- Smart Metering
- DCC

#### Properties

- [OpenAPI](openapi/hildebrand-glowmarkt-resource-system-swagger.json) — Swagger 2.0, 18 paths
- [API Reference](https://api.glowmarkt.com/api-docs/v0-1/resourcesys/)
- [Documentation](https://docs.glowmarkt.com/GlowmarktAPIDataRetrievalDocumentationIndividualUserForBright.pdf)

### Glowmarkt Virtual Entity System API

CRUD over Virtual Entities — the Glow Platform's model of a physical "thing" such as a home or a site, made up of metadata and a collection of resources. Lists the virtual entities a caller has access to, resolves the resources belonging to each, manages virtual entity types and metadata attributes, and reports per-application virtual entity statistics.

- **Human URL:** [https://api.glowmarkt.com/api-docs/v0-1/vesys/](https://api.glowmarkt.com/api-docs/v0-1/vesys/)
- **Base URL:** `https://api.glowmarkt.com/api/v0-1`

#### Tags

- Virtual Entities
- Sites
- Metadata
- Energy Data

#### Properties

- [OpenAPI](openapi/hildebrand-glowmarkt-virtual-entity-system-swagger.json) — Swagger 2.0, 8 paths
- [API Reference](https://api.glowmarkt.com/api-docs/v0-1/vesys/)
- [Documentation](https://docs.glowmarkt.com/GlowmarktAPIDataRetrievalDocumentationIndividualUserForBright.pdf)

### Glowmarkt Device Management System API

Registration and status of the physical hardware feeding the platform — gateways such as the Glow CAD and GlowStick, sensors such as smart electricity meters, and actuators such as auxiliary load control switches. Also exposes the DCC inventory of a meter point by MPxN or by smart-meter EUI, the resources associated to a meter point, and gateway packet-delivery status.

- **Human URL:** [https://api.glowmarkt.com/api-docs/v0-1/dmssys/](https://api.glowmarkt.com/api-docs/v0-1/dmssys/)
- **Base URL:** `https://api.glowmarkt.com/api/v0-1`

#### Tags

- Devices
- Hardware
- Gateways
- Smart Metering
- DCC
- IoT

#### Properties

- [OpenAPI](openapi/hildebrand-glowmarkt-device-management-system-swagger.json) — Swagger 2.0, 11 paths
- [API Reference](https://api.glowmarkt.com/api-docs/v0-1/dmssys/)

### Glowmarkt Notification System API

Alerting and messaging for Glow-based applications. Defines alert types, manages per-channel and per-culture message templates, sends alerts to users, and reports notification delivery and logs. Served from its own base path, `/api/v0-1/ns`.

- **Human URL:** [https://api.glowmarkt.com/api-docs/v0-1/notificationsys/](https://api.glowmarkt.com/api-docs/v0-1/notificationsys/)
- **Base URL:** `https://api.glowmarkt.com/api/v0-1/ns`

#### Tags

- Notifications
- Alerts
- Templates
- Messaging

#### Properties

- [OpenAPI](openapi/hildebrand-glowmarkt-notification-system-swagger.json) — Swagger 2.0, 10 paths
- [API Reference](https://api.glowmarkt.com/api-docs/v0-1/notificationsys/)

## Mandate and Access

| | |
| --- | --- |
| **Home market** | United Kingdom |
| **Mandate regime** | `smart-meter-infrastructure` — Smart Energy Code / DCC User Entry Process. Not a consumer data right. |
| **Mandate status** | `live-implemented` — verified in the official SEC Parties List spreadsheet: *Hildebrand Technology Limited — "Yes - Other User"*. |
| **Data standard** | No standard reference found. Proprietary Device / Resource / Virtual Entity model with classifier strings; no Green Button, ESPI, CDR, CIM, IEEE 2030.5, OpenADR or OCPP/OCPI. |
| **Consumer data API** | Yes — half-hourly electricity and gas consumption, cost, export and 13 months of history, consent-managed per MPxN. |
| **Open market data** | No — every documented endpoint returns HTTP 400 without an `applicationId` header. |
| **Access gate** | `customer-account-required` for your own data via Bright; `licence-agreement` (contract, from GBP 595/month per MPxN) for organisational access to others' data. |
| **Auth model** | JWT in a custom `token` header plus a mandatory `applicationId` header; OAuth 2.0 authorization-code grant also defined. No OIDC discovery document. |

See [review.yml](review.yml) for the full probe log, harvest provenance, and mandate evidence.

## Common Properties

- [Website](https://www.hildebrand.co.uk/)
- [Documentation](https://api.glowmarkt.com/api-docs/v0-1/resourcesys/)
- [API Reference](https://api.glowmarkt.com/api-docs/v0-1/usersys/usertypes/)
- [Sign Up](https://data.glowforindustry.com/signup)
- [Pricing](https://data.glowforindustry.com/#pricing)
- [Support](https://www.hildebrand.co.uk/contact-us)
- [Forum](https://forum.glowmarkt.com/)
- [LinkedIn](https://www.linkedin.com/company/hildebrand/)
- [Privacy Policy](https://www.hildebrand.co.uk/privacy-policy)

## Maintainers

- Kin Lane — kin@apievangelist.com
