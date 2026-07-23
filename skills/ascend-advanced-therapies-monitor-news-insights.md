---
name: Monitor Ascend Advanced Therapies News & Insights
description: Retrieve, filter by category, and monitor the News & Insights content stream from the Ascend Advanced Therapies WordPress content API.
api: openapi/ascend-advanced-therapies-wp-rest-openapi.yml
operations:
  - listPosts
  - getPost
  - listCategories
  - getCategory
  - listMedia
  - searchContent
---

# Monitor Ascend Advanced Therapies News & Insights

Ascend Advanced Therapies runs its News & Insights stream — company news, technical articles, blog
posts, and webinar announcements — on the WordPress `post` type, anonymously readable over the
site's content API. Use this to follow AAV manufacturing announcements, technical publications, and
company milestones as structured JSON rather than scraping the site.

Base URL: `https://www.ascend-adv.com/wp-json`

## Authentication

None. Every operation here is anonymously readable — do not send credentials.

## Steps

1. **Resolve the categories you care about.** Call `listCategories`
   (`GET /wp/v2/categories?per_page=100`). The site organizes content into news, articles, blogs,
   and webinar. Capture each term's integer `id` — the post filters take IDs, not slugs. Cache these;
   they change rarely. `getCategory` (`GET /wp/v2/categories/{id}`) reads a single term.

2. **List posts.** Call `listPosts`
   (`GET /wp/v2/posts?per_page=100&orderby=date&order=desc`), optionally narrowing with
   `categories=<id>` or `search=<term>`.
   - 55 posts were present at capture. Read `X-WP-Total` and `X-WP-TotalPages` for the true size and
     follow the `Link` header `rel="next"` to page.
   - `per_page` is capped at 100; out-of-range values return HTTP 400 `rest_invalid_param` with the
     specific bound in `data.params.per_page`.

3. **Pull related resources in one call.** Append `_embed` to inline the author, featured image, and
   taxonomy terms into an `_embedded` object on each post. This avoids a follow-up `listMedia` or
   `getCategory` per item. Without `_embed`, `featured_media` and `categories` are bare integer IDs
   you would have to resolve yourself.

4. **Read a single post.** Call `getPost` (`GET /wp/v2/posts/{id}`). Useful fields:
   `title.rendered`, `excerpt.rendered`, `content.rendered`, `link`, `date`/`date_gmt`,
   `modified`/`modified_gmt`, `categories`, `tags`. A non-resolving ID returns HTTP 404 with code
   `rest_post_invalid_id`.

5. **Search across all content types.** Call `searchContent`
   (`GET /wp/v2/search?search=<term>`) when you want pages and other content types alongside posts.
   Results are lightweight stubs — `id`, `title`, `url`, `type`, `subtype` — so follow up with
   `getPost` or `getPage` for the full record.

6. **Retrieve assets.** Call `listMedia` (`GET /wp/v2/media?media_type=image`) or read the embedded
   featured media. `source_url` is the direct asset URL; posters and white papers are also in the
   media library.

## Rules

- Read-only. Never attempt writes against these routes.
- Poll no faster than the 10-minute edge cache (`cache-control: max-age=600, must-revalidate`).
  Daily is appropriate for a news stream. Use `Last-Modified` for conditional requests.
- `content.rendered` and `excerpt.rendered` are HTML. Sanitize before display and strip markup
  before summarizing.
- Branch on the error `code` field, not the message. See
  `errors/ascend-advanced-therapies-problem-types.yml` for the catalog.
- The RSS feed at `https://www.ascend-adv.com/feed/` carries the same stream if you only need
  titles and links; prefer the API when you need taxonomy IDs, custom fields, or full content.
- Attribute anything you surface to Ascend Advanced Therapies and link the post's `link` field.
