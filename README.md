# Ascend Advanced Therapies

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
