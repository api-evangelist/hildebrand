# Hildebrand

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
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

**Areas:** Energy · United Kingdom · Utilities · Electricity · Gas · Smart Metering · Energy Data · Demand Response · IoT · Metering

## Hildebrand on APIs.io

Everything profiled for Hildebrand is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/hildebrand/](https://apis.io/providers/hildebrand/)** — or go straight to one of the APIs or properties below.

### APIs (21)

- [Hildebrand Account API](https://apis.io/apis/hildebrand/hildebrand-account-api/) — The Account API from Hildebrand — 8 operation(s) for account.
- [Hildebrand Account Profile API](https://apis.io/apis/hildebrand/hildebrand-account-profile-api/) — The Account Profile API from Hildebrand — 2 operation(s) for account profile.
- [Hildebrand Account Session API](https://apis.io/apis/hildebrand/hildebrand-account-session-api/) — The Account Session API from Hildebrand — 1 operation(s) for account session.
- [Hildebrand Alert API](https://apis.io/apis/hildebrand/hildebrand-alert-api/) — An application can send an alert to a customer across multiple channels (email, push, inbox) which will convey some type of specific message (defined by the…
- [Hildebrand Alerttype API](https://apis.io/apis/hildebrand/hildebrand-alerttype-api/) — The definition of an alert, what functionality the alert represents. It is an identifier which amongst other elements will point us to the correct template.…
- [Hildebrand Auth API](https://apis.io/apis/hildebrand/hildebrand-auth-api/) — The Auth API from Hildebrand — 5 operation(s) for auth.
- [Hildebrand Device API](https://apis.io/apis/hildebrand/hildebrand-device-api/) — The Device API from Hildebrand — 5 operation(s) for device.
- [Hildebrand Device Meter Point DCC inventory API](https://apis.io/apis/hildebrand/hildebrand-device-meter-point-dcc-inventory-api/) — The Device Meter Point DCC inventory API from Hildebrand — 3 operation(s) for device meter point dcc inventory.
- [Hildebrand Device Type API](https://apis.io/apis/hildebrand/hildebrand-devicetype-api/) — The DeviceType API from Hildebrand — 2 operation(s) for devicetype.
- [Hildebrand Discover API](https://apis.io/apis/hildebrand/hildebrand-discover-api/) — The discover API from Hildebrand — 1 operation(s) for discover.
- [Hildebrand Meter Point Consent & Verification API](https://apis.io/apis/hildebrand/hildebrand-meter-point-consent-verification-api/) — The Meter Point Consent & Verification API from Hildebrand — 5 operation(s) for meter point consent & verification.
- [Hildebrand Notification API](https://apis.io/apis/hildebrand/hildebrand-notification-api/) — When an application triggeers an alert, for each channel of communication a notification is created. This enables the system to monitor seperately whant…
- [Hildebrand Resource API](https://apis.io/apis/hildebrand/hildebrand-resource-api/) — A Resource is a representation of data collected from a physical device, like sensor readings, or changes in an actuating device state etc.
- [Hildebrand Resource Type API](https://apis.io/apis/hildebrand/hildebrand-resource-type-api/) — A Resource Type defines the storage structure of the resources supported by the Glow Platform.
- [Hildebrand Template API](https://apis.io/apis/hildebrand/hildebrand-template-api/) — The template of the message that is being sent; it can be passed through as HTML or JSON. Each template has an alert type, is specific to a single channel…
- [Hildebrand User API](https://apis.io/apis/hildebrand/hildebrand-user-api/) — The User API from Hildebrand — 6 operation(s) for user.
- [Hildebrand Virtual Entity API](https://apis.io/apis/hildebrand/hildebrand-virtual-entity-api/) — A Virtual Entity is an instance of the Virtual Entity Type and is tied to an owner as well as an applicationId. In order to create a Virtual Entity a user…
- [Hildebrand Virtual Entity's Metadata API](https://apis.io/apis/hildebrand/hildebrand-virtual-entity-s-metadata-api/) — A Virtual Entity's metadata can be used to save information that will facilitate the virtual representation of the entity. This is typically attribute data…
- [Hildebrand Virtual Entity Statistics API](https://apis.io/apis/hildebrand/hildebrand-virtual-entity-statistics-api/) — APIs that return an overview of the Virtual Entities an application has (administrative API).
- [Hildebrand Virtual Entity Type API](https://apis.io/apis/hildebrand/hildebrand-virtual-entity-type-api/) — Entity that belongs and is managed by an application and contains the definition and combination of the Resource Types that are required to create a Virtual…
- [Hildebrand O Auth API](https://apis.io/apis/hildebrand/hildebrand-oauth-api/) — The OAuth API from Hildebrand — 2 operation(s) for oauth.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Hildebrand Event Surface](https://apis.io/asyncapis/hildebrand/hildebrand-event-surface/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [hildebrand-glowmarkt](https://apis.io/servers/hildebrand/hildebrand-glowmarkt/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Hildebrand Agentic Access](https://apis.io/agentic-access/hildebrand/hildebrand-agentic-access/)

#### Collections (5)

Postman and Open Collection request collections.

- [Device Management System](https://apis.io/collections/hildebrand/open-hildebrand-glowmarkt-device-management-system-swagger/)
- [Notification System](https://apis.io/collections/hildebrand/open-hildebrand-glowmarkt-notification-system-swagger/)
- [Resource System](https://apis.io/collections/hildebrand/open-hildebrand-glowmarkt-resource-system-swagger/)
- [Glowmarkt User System](https://apis.io/collections/hildebrand/open-hildebrand-glowmarkt-user-system-swagger/)
- [Virtual Entity System](https://apis.io/collections/hildebrand/open-hildebrand-glowmarkt-virtual-entity-system-swagger/)

#### Overlays (5)

OpenAPI overlays, including conversational phrasing for each operation.

- [Hildebrand Glowmarkt Device Management System Overlay](https://apis.io/overlays/hildebrand/hildebrand-glowmarkt-device-management-system-overlay/)
- [Hildebrand Glowmarkt Notification System Overlay](https://apis.io/overlays/hildebrand/hildebrand-glowmarkt-notification-system-overlay/)
- [Hildebrand Glowmarkt Resource System Overlay](https://apis.io/overlays/hildebrand/hildebrand-glowmarkt-resource-system-overlay/)
- [Hildebrand Glowmarkt User System Overlay](https://apis.io/overlays/hildebrand/hildebrand-glowmarkt-user-system-overlay/)
- [Hildebrand Glowmarkt Virtual Entity System Overlay](https://apis.io/overlays/hildebrand/hildebrand-glowmarkt-virtual-entity-system-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Hildebrand Authentication](https://apis.io/security/hildebrand/hildebrand-authentication/)
- [Hildebrand Domain Security](https://apis.io/security/hildebrand/hildebrand-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Hildebrand Plans](https://apis.io/plans/hildebrand/hildebrand-plans/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.hildebrand.co.uk/)
- [Documentation](https://api.glowmarkt.com/api-docs/v0-1/resourcesys/)
- [Getting started](https://docs.glowmarkt.com/GlowmarktAPIDataRetrievalDocumentationIndividualUserForBright.pdf)
- [API reference](https://api.glowmarkt.com/api-docs/v0-1/usersys/usertypes/)
- [Pricing](https://data.glowforindustry.com/#pricing)
- [Sign up](https://data.glowforindustry.com/signup)
- [Support](https://www.hildebrand.co.uk/contact-us)
- [Blog](https://data.glowforindustry.com/articles)
- [Compliance](https://www.hildebrand.co.uk/about)
- [Privacy policy](https://www.hildebrand.co.uk/privacy-policy)
- [GitHub](https://github.com/HildebrandTechnology)

## API Evangelist rating

**Kin Score 50.2** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 55.4 |
| Contract governance | 18.2 |
| Operational transparency | 10.5 |
| Developer ergonomics | 49.4 |
| Access clarity | 68.4 |

**Agent readiness 30.1** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 32.0** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/hildebrand/](https://apis.io/providers/hildebrand/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Hildebrand: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/hildebrand/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
