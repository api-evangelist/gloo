# Gloo

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

Gloo is Solo.io's family of open-source and enterprise API gateway, service mesh and developer portal products, built on Envoy Proxy and Istio and delivered as software the customer runs in their own Kubernetes clusters rather than as a hosted SaaS. Gloo Edge and Gloo Gateway provide ingress, advanced traffic management, external auth, rate limiting, WAF, GraphQL and AI/LLM traffic routing; Gloo Mesh manages multi-cluster Istio; and Gloo Portal publishes API products to internal and external consumers with teams, applications, subscriptions, API keys and OAuth credentials. Solo.io renamed its commercial line in 2026 — Gloo Gateway is now Solo Enterprise for kgateway and Gloo Mesh is now Solo Enterprise for Istio — and the upstream kgateway project is a conformant implementation of the Kubernetes Gateway API, passing 93 of 93 core and extended conformance tests against v1.6.1.

**Areas:** API Gateway · Cloud-Native · Developer Portal · Envoy · Istio · Kubernetes · Kubernetes Gateway API · Open Source · Service Mesh

## Gloo on APIs.io

Everything profiled for Gloo is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/gloo/](https://apis.io/providers/gloo/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Gloo Edge](https://apis.io/apis/gloo/gloo-edge/) — Gloo Edge is a feature-rich, Kubernetes-native ingress controller and API gateway built on Envoy Proxy, supporting advanced routing, security policies, and…
- [Gloo API Products API](https://apis.io/apis/gloo/gloo-api-products-api/) — The API Products API from Gloo — 3 operation(s) for api products.
- [Gloo Applications API](https://apis.io/apis/gloo/gloo-applications-api/) — The Applications API from Gloo — 8 operation(s) for applications.
- [Gloo Me API](https://apis.io/apis/gloo/gloo-me-api/) — The Me API from Gloo — 1 operation(s) for me.
- [Gloo Subscriptions API](https://apis.io/apis/gloo/gloo-subscriptions-api/) — The Subscriptions API from Gloo — 2 operation(s) for subscriptions.
- [Gloo Teams API](https://apis.io/apis/gloo/gloo-teams-api/) — The Teams API from Gloo — 5 operation(s) for teams.
- [Gloo User API](https://apis.io/apis/gloo/gloo-user-api/) — The User API from Gloo — 1 operation(s) for user.
- [Gloo Webhooks API](https://apis.io/apis/gloo/gloo-webhooks-api/) — The Webhooks API from Gloo — 2 operation(s) for webhooks.
- [Gloo APIs API](https://apis.io/apis/gloo/gloo-apis-api/) — The APIs API from Gloo — 5 operation(s) for apis.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Gloo Webhooks](https://apis.io/asyncapis/gloo/gloo-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [gloo-mcp.yml](https://apis.io/servers/gloo/gloo-mcp-yml/)

#### Overlays (4)

OpenAPI overlays, including conversational phrasing for each operation.

- [Gloo Ai Guardrail Webhook Overlay](https://apis.io/overlays/gloo/gloo-ai-guardrail-webhook-overlay/)
- [Gloo Idp Connect Overlay](https://apis.io/overlays/gloo/gloo-idp-connect-overlay/)
- [Gloo Platform Portal Overlay](https://apis.io/overlays/gloo/gloo-platform-portal-overlay/)
- [Gloo Portal Server Overlay](https://apis.io/overlays/gloo/gloo-portal-server-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Gloo Authentication](https://apis.io/security/gloo/gloo-authentication/)
- [Gloo Domain Security](https://apis.io/security/gloo/gloo-domain-security/)
- [Gloo Trust Center](https://apis.io/security/gloo/gloo-trust-center/)
- [Gloo Vulnerability Disclosure](https://apis.io/security/gloo/gloo-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Gloo Plans Pricing](https://apis.io/plans/gloo/gloo-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Gloo Rate Limits](https://apis.io/rate-limits/gloo/gloo-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Gloo Finops](https://apis.io/finops/gloo/gloo-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.solo.io/)
- [Documentation](https://docs.solo.io/)
- [Getting started](https://docs.solo.io/gloo-edge/latest/getting_started/)
- [API reference](https://docs.solo.io/gateway/latest/reference/api/)
- [Pricing](https://www.solo.io/pricing)
- [Support](https://www.solo.io/company/contact/)
- [Changelog](https://github.com/solo-io/gloo/releases)
- [Blog](https://www.solo.io/blog/)
- [Security](https://www.solo.io/security)
- [Trust centre](https://trust.solo.io/)
- [Terms of service](https://legal.solo.io/#website-terms-of-use)
- [Privacy policy](https://legal.solo.io/#privacy-policy)
- [GitHub](https://github.com/solo-io)

## API Evangelist rating

**Kin Score 56.3** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 58.5 |
| Contract governance | 18.2 |
| Operational transparency | 44.7 |
| Developer ergonomics | 80.4 |
| Access clarity | 28.9 |

**Agent readiness 34.5** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 31.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/gloo/](https://apis.io/providers/gloo/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Gloo: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/gloo/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
