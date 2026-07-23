---
name: Track Ascend Advanced Therapies job openings
description: Retrieve and monitor open roles at Ascend Advanced Therapies from the Careers custom post type on its WordPress content API.
api: openapi/ascend-advanced-therapies-wp-rest-openapi.yml
operations:
  - listJobOpenings
  - getJobOpening
  - listTypes
---

# Track Ascend Advanced Therapies job openings

Ascend Advanced Therapies publishes its Careers listings as a WordPress custom post type,
`awsm_job_openings`, which is anonymously readable over the site's content API. This is the only
route on the host that exposes company-operational data rather than marketing content.

Base URL: `https://www.ascend-adv.com/wp-json`

## Authentication

None. Every operation in this skill is anonymously readable — do not send credentials. Application
Password credentials exist only for the write surface and are not needed here.

## Steps

1. **Confirm the custom post type is still registered.** Call `listTypes`
   (`GET /wp/v2/types`) and look for the `awsm_job_openings` key. Read its `rest_base` rather than
   hardcoding the path — a plugin change can rename it. If the key is absent, the site has changed
   its careers implementation; stop and report that rather than guessing another path.

2. **List the open roles.** Call `listJobOpenings`
   (`GET /wp/v2/awsm_job_openings?per_page=100&orderby=date&order=desc`).
   - `per_page` is capped at 100. Values outside 1-100 return HTTP 400 `rest_invalid_param`.
   - Read `X-WP-Total` and `X-WP-TotalPages` from the response headers to size the result set, and
     follow the `Link` header `rel="next"` to page rather than incrementing `page` blindly.

3. **Read each role.** Useful fields on each item: `title.rendered`, `excerpt.rendered`,
   `content.rendered` (the full posting, as HTML), `link` (the public careers page for the role),
   `date` and `modified` (both also available as `_gmt` variants), and `slug`.
   Role attributes such as location, department, and employment type are not first-class fields —
   they live in the `meta` and `acf` bags. Inspect those per item; do not assume a key exists.

4. **Fetch a single role when you already have its ID.** Call `getJobOpening`
   (`GET /wp/v2/awsm_job_openings/{id}`). An ID that does not resolve returns HTTP 404 with code
   `rest_post_invalid_id`.

5. **Detect changes across runs.** Key on `id` and compare `modified_gmt`. A role that disappears
   from the collection has been closed or unpublished; the API returns no tombstone, so absence is
   the only signal.

## Rules

- Read-only. Never attempt POST, PUT, PATCH, or DELETE against these routes.
- Responses are edge cached for 10 minutes (`cache-control: max-age=600, must-revalidate`). Polling
  faster than that returns stale data and gains nothing; once or twice a day is appropriate.
- There is no documented rate limit and no rate-limit headers are returned. Stay well within
  courteous volumes and honour `Last-Modified` with a conditional request where possible.
- Errors use the WordPress envelope — `code`, `message`, `data.status` — as `application/json`, not
  RFC 9457 problem+json. Branch on `code`, not on the message string. See
  `errors/ascend-advanced-therapies-problem-types.yml`.
- `content.rendered` is HTML, not plain text or markdown. Sanitize before display.
