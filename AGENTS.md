# LinkScrub — Agent Interface

## What it does

LinkScrub removes tracking parameters from URLs — UTM tags, fbclid, gclid, msclkid, and 25+ other known trackers — returning a clean, shareable URL.

## Current state

**Version: 1.0 (browser-only)**

The free tier runs entirely in the browser. No API is live yet. The planned API is documented below for integration planning.

## Planned API (not yet live)

```
GET /api/scrub?url=<encoded-url>
```

**Response:**
```json
{
  "original": "https://example.com/page?utm_source=newsletter&utm_campaign=may26&fbclid=IwAR123",
  "clean": "https://example.com/page",
  "removed": [
    { "key": "utm_source", "value": "newsletter" },
    { "key": "utm_campaign", "value": "may26" },
    { "key": "fbclid", "value": "IwAR123" }
  ],
  "kept": [],
  "changed": true
}
```

**Parameters removed (25+):**
- UTM: `utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content`, `utm_id`
- Google: `gclid`, `gclsrc`, `dclid`, `_ga`, `_gid`, `_gl`
- Facebook: `fbclid`, `fb_action_ids`
- Microsoft: `msclkid`
- TikTok: `ttclid`
- Twitter: `twclid`
- LinkedIn: `li_fat_id`
- Instagram: `igshid`
- MailChimp: `mc_cid`, `mc_eid`
- Adobe: `s_cid`, `s_kwcid`
- Marketo: `mkt_tok`
- HubSpot: `_hsmi`, `_hsenc`
- Yahoo/Yandex: `yclid`
- Generic: `ref`, `affiliate`, `click_id`, `clickid`

## Planned MCP tool

```
Tool name: scrub_url
Input: { url: string }
Output: { original: string, clean: string, removed: [{key, value}], changed: boolean }
```

**Use cases for agents:**
- Clean URLs before inserting into documents, emails, or social posts
- Normalize URLs before storing in databases (avoid duplicate records from same page with different tracking params)
- Build privacy-preserving link sharing features
- Pre-process URLs in web scraping or data pipelines

## Pricing

- **Free tier:** Web app at linkscrub.radicchio.page — unlimited use, no auth
- **Planned paid tier:** Browser extension for one-click scrubbing ($4.99 one-time) — not yet available
- **API access:** Not yet priced — planned with paid tier

## Authentication

None required for the web app. API (when live) will use API key in `Authorization: Bearer <key>` header.

## Support

https://bitterdesk.com/s/linkscrub/
