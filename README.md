# Ascend Advanced Therapies

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

Ascend Advanced Therapies is a gene-to-GMP contract development and manufacturing organization
(CDMO) for advanced therapies, specializing in adeno-associated virus (AAV) vector development and
manufacture for gene therapies, immunotherapies, oncolytics, and vaccines. Formed in 2023 when
expert teams merged behind more than $130M of funding, and aligned with ABL, Inc. since late 2024,
Ascend operates GMP manufacturing, aseptic fill-finish, and analytical facilities in Rockville,
Maryland and Alachua, Florida alongside European capacity. Services span process development, gene
therapy formulation, scalable manufacturing, in-house fill-finish, GMP QC testing, long-read NGS for
viral vectors, and potency assay development, built on its EpyQ production system and proprietary
AAV yield enhancers.

Website: https://www.ascend-adv.com/
Backed by: dcvc (DCVC Bio), alongside Abingworth, Petrichor, 4BIO Capital, Cathay Health, Deerfield
Management, Digitalis Ventures, and Ajinomoto.

## API surface

Ascend is a life-science manufacturer, not a software vendor. It offers **no commercial product
API**, no developer portal, no SDKs, and no public developer program. The one machine-readable
interface it exposes is the **WordPress REST content API** behind its corporate site
(`https://www.ascend-adv.com/wp-json`), which is anonymously readable and serves the News & Insights
stream, site pages, media, taxonomy, site search, and the `awsm_job_openings` custom post type
behind the Careers listings.

That surface has been captured here as an OpenAPI 3.1 specification derived from live route
discovery — 328 routes were enumerated from the discovery document, and only operations verified to
return HTTP 200 anonymously are documented.

## Artifacts

| Artifact | Path | Method |
|---|---|---|
| OpenAPI 3.1 | `openapi/` | derived from live route discovery |
| Overlay | `overlays/` | generated |
| Authentication | `authentication/` | searched (advertised at `/wp-json/`) |
| Conventions | `conventions/` | derived |
| Error catalog | `errors/` | searched (live probe of each error) |
| Data model | `data-model/` | derived |
| Lifecycle | `lifecycle/` | derived |
| Conformance | `conformance/` | derived |
| MCP server | `mcp/` | derived, candidate — no hosted server exists |
| Agent skills | `skills/` | generated, read-only |
| llms.txt | `llms/` | generated — provider publishes none |
| Well-known | `well-known/` | searched — all discovery paths 404 |
| Domain security | `security/` | probed |

## Verified absences

Probed on 2026-07-19 and recorded rather than inferred: no `/.well-known/` surface, no
`security.txt`, no `llms.txt`, no vulnerability disclosure policy, no trust center or published
compliance certifications, no status page, no changelog, no deprecation policy or SLA, no SDKs or
packages on any registry, no GitHub organization, no CLI, no sandbox, no webhooks or event surface,
no Postman collection, and no idempotency contract. TLS 1.3 with SPF and DMARC (quarantine) present;
HSTS, DNSSEC, and CAA absent.
