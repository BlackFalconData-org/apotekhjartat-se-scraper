# Apotekhjartat Sweden Scraper [Just 💰$1.8]

Extract structured data from [apotekhjartat.se](https://apotekhjartat.se) — apotekhjartat.se — every product from a search, category or brand page of the Swedish online pharmacy. Every record carries price and price the source publishes. Structured rows, ready to import into a CRM or a spreadsheet.

**[Apotekhjartat Sweden Scraper [Just 💰$1.8] on Apify →](https://apify.com/blackfalcondata/apotekhjartat-se-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword. Filter by 📝 description format, and more.

**Detail enrichment** — Fetch full descriptions, structured metadata for each product.

**Incremental mode** — Only get new or changed products since your last run. Content hash per product — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how products evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N products (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every product returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured products from apotekhjartat.se on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor products, track trends, and analyze market dynamics with structured, deduplicated data from apotekhjartat.se.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per product is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "vitamin",
  "maxResults": 100,
  "descriptionMaxLength": 0,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all",
  "includeDetails": false
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | A product search term (e.g. "vitamin"), or an apotekhjartat.se category/brand path or URL (e.g. "/forkylning") to list that section. Required if no Start URLs are provided. Use a JSON array for several searches in one run. |
| `maxResults` | integer | `100` | Maximum total products (0 = unlimited). |
| `startUrls` | array | `[]` | Paste apotekhjartat.se search or category URLs. Each URL becomes its own task; results are merged and deduped by product across all URLs. When provided, Start URLs REPLACE the search term (unsupported URLs are skipped, and if none is supported the run stops with an input error). |
| `descriptionMaxLength` | integer | `0` | Truncate the product description to N characters. 0 = no truncation. |
| `compact` | boolean | `false` | Core product fields only (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state and return only new or changed products. stateKey is optional — it defaults to a value derived from your search inputs so different searches never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked product universe. Leave empty to auto-generate from the search inputs. |
| `emitUnchanged` | boolean | `false` | When incremental, also emit products that haven't changed since the previous run. |
| `emitExpired` | boolean | `false` | When incremental, also emit products that are no longer listed. |
| `skipReposts` | boolean | `false` | When incremental, skip products whose content matches one that disappeared in a prior run (cross-run duplicate detection). |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED products. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of products included in each notification message (1-20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |
| `includeDetails` | boolean | `false` | Open each product page to add the full product description (the editorial text shown on the page) as `fullDescription`. Increases run time. Leave off for a fast, low-cost run. |

---

## Output fields

Every product returns the same 37-field schema. Missing values are `null` — never omitted.

- `listingId`
- `id`
- `sku`
- `productNumber`
- `title`
- `url`
- `brand`
- `category`
- `ean`
- `price`
- `priceExclVat`
- `vatPercent`
- `currency`
- `discount`
- `isOnSale`
- `storePrice`
- `pricePerUnit`
- `availability`
- `imageUrl`
- `images`
- `description`
- `activeSubstances`
- `isOtcMedicine`
- `isBuyableWithoutPrescription`
- `isDietarySupplement`
- `isWebSaleOnly`
- `isSponsored`
- `maxQuantityPerOrder`
- `labels`
- `scrapedAt`
- `portalUrl`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `source`
- `contentHash`
- `changeType`

---

## Sample output

One object per product. Here is a real example from a production run:

```json
{
  "listingId": "16afe9162ef71364dffff08f739e6866a2d07b2cda1ce23571dca801eb6dfe1d",
  "id": "1074520",
  "sku": "1074520",
  "productNumber": "456389",
  "title": "4HER Hair 60 tabletter",
  "url": "https://www.apotekhjartat.se/varumarken/4her/4her-hair-60-tabletter",
  "brand": "4HER",
  "category": "Kosttillskott hår, hud & naglar",
  "ean": "7090027121362",
  "price": 274,
  "priceExclVat": 258.49,
  "vatPercent": 6
}
```

*Truncated — full records contain 37 fields. See Output fields for the complete schema.*

**[Try Apotekhjartat Sweden Scraper [Just 💰$1.8] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/apotekhjartat-se-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.0045 |
| Result | $0.0018 |

See the [actor on Apify](https://apify.com/blackfalcondata/apotekhjartat-se-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape apotekhjartat.se?**
Use this actor on Apify to extract structured data from apotekhjartat.se. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get apotekhjartat.se data as JSON, CSV, or Excel?**
The actor writes each product to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape apotekhjartat.se?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check apotekhjartat.se's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each product gets a content hash. On subsequent runs, only new or changed products are emitted — saving time, compute, and storage. Expired products can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Apotekhjartat Sweden Scraper [Just 💰$1.8]](https://apify.com/blackfalcondata/apotekhjartat-se-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
