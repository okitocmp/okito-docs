---
description: Cookie Scanner and Policy Generator over HTTPS. Professional plan.
---

# REST API

The Okito REST API lets you run cookie scans and generate policies from your own systems. It is included in the Professional plan.

## Authentication

1. Create a key in **Settings → API Keys**. Each key has a list of **allowed domains**; it only works for those domains.
2. The key is shown once. Store it as a secret.
3. Send it with every request, either as `X-API-Key: okito_live_…` or `Authorization: Bearer okito_live_…`.

Base URL: `https://app.okito.com`

{% hint style="danger" %}
API keys are secrets. Never put them in your website's front-end code. Website keys (in your script URL) are public; API keys are not.
{% endhint %}

## Cookie Scanner API

### Synchronous scan

`POST /api/external/cookie-scanner/scan`

Runs a full scan and returns the cookies in the same response. It waits up to about 85 seconds for the scan; see [Long scans](#long-scans) for what happens after that.

```bash
curl -X POST https://app.okito.com/api/external/cookie-scanner/scan \
  -H "X-API-Key: okito_live_..." \
  -H "Content-Type: application/json" \
  -d '{ "websiteUrl": "https://example.com" }'
```

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `websiteUrl` | string | Yes | Full URL to scan. Its host must be in the key's allowed domains. |

```json
{
  "success": true,
  "scanId": "ext_1713690000000_abc12345",
  "websiteUrl": "https://example.com",
  "domain": "example.com",
  "durationMs": 4832,
  "summary": { "total": 17 },
  "complete": true,
  "cookies": [
    {
      "name": "_ga",
      "domain": ".example.com",
      "category": "analytics",
      "provider": "Google Analytics",
      "description": "...",
      "purpose": "...",
      "duration": "2 years"
    }
  ]
}
```

`complete` is `false` when the site loaded only partly; `incompleteReason` then says why. A site that could not be loaded at all answers `502` with `code: "SCAN_INCOMPLETE"`.

#### Long scans

If the scan has not finished after about 85 seconds, the answer is `202 Accepted`. The scan keeps running on our side; read its result from the [status endpoint](#asynchronous-scan) with the `scanId`:

```json
{
  "success": true,
  "scanId": "ext_1713690000000_abc12345",
  "status": "running",
  "message": "The scan is still running. Check back with this scan ID.",
  "pollUrl": "/api/external/cookie-scanner/scan/async/ext_1713690000000_abc12345?domain=example.com"
}
```

Call `pollUrl` as it is (it already names the domain) with the same key every few seconds until `status` is `completed` or `failed`. Treat `202` as "not finished yet", not as an error.

### Asynchronous scan

For large sites, start a scan and poll for the result.

`POST /api/external/cookie-scanner/scan/async` with `{ "websiteUrl": "https://example.com" }` returns a `scanId` with `status: "queued"`.

`GET /api/external/cookie-scanner/scan/async/:scanId?domain=example.com` returns the status (`queued`, `running`, `completed` or `failed`) and, when `status` is `completed`, the cookies. Only the key that started the scan can read it. A failed scan has an `error` such as `SCANNER_BUSY` or `SCAN_TIMEOUT`. Scans are kept for 7 days.

### Scanner responses

| Status | `code` | Meaning |
| --- | --- | --- |
| `200` | | The scan finished; the cookies are in the response. |
| `202` | | Still running (synchronous scan after about 85 seconds, or any asynchronous start). Poll the status endpoint. |
| `404` | `SCAN_NOT_FOUND` | No scan with this `scanId` was started by your key, or it is older than 7 days. |
| `502` | `SCAN_INCOMPLETE` | The website could not be loaded for scanning. |
| `502` | `SCANNER_UPSTREAM_ERROR` | The synchronous scan failed (it ran out of time, was interrupted, or the scanner failed). Try again later. |
| `503` | `SCANNER_BUSY` | Too many scans are running. Retry after the `Retry-After` header (60 seconds); a refused request does not count against your key's rate limit. |
| `503` | `SCAN_STATUS_UNAVAILABLE` | The synchronous scan started but its status could not be read. Poll its `scanId` a little later. |

## Policy Generator API

### Generate a policy

`POST /api/public/policies/generate`

```bash
curl -X POST https://app.okito.com/api/public/policies/generate \
  -H "X-API-Key: okito_live_..." \
  -H "Content-Type: application/json" \
  -d '{
    "domain": "example.com",
    "policyType": "privacy",
    "language": "en",
    "companyName": "Example Inc.",
    "contactEmail": "privacy@example.com",
    "industry": "ecommerce",
    "includeGoogleAnalytics": true,
    "includeFacebookPixel": true,
    "includeMarketing": true
  }'
```

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `domain` | string | Yes | Must be in the key's allowed domains. |
| `policyType` | `privacy` \| `cookie` \| `terms` | No | Default `privacy`. |
| `language` | string | No | ISO code such as `en`, `tr`, `de`, `fr`, `es`. Default `en`. |
| `companyName` | string | No | Default: the domain. |
| `contactEmail` | string | No | Contact email in the document. |
| `industry` | string | No | Industry hint, for example `fintech`. |
| `includeGoogleAnalytics`, `includeFacebookPixel`, `includeMarketing`, `includeThirdPartyIntegrations` | boolean | No | Optional sections. Default `false`. |

The response contains the policy in Markdown and your usage. Generations share the dashboard's monthly quota (7 per user).

### Read your quota

`GET /api/public/policies/usage?domain=example.com` returns `used`, `limit`, `remaining` and `resetAt` for the current month.
