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

Runs a full scan and returns the cookies in the same response.

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
  "scanId": "opt-1713690000000-abc123",
  "websiteUrl": "https://example.com",
  "domain": "example.com",
  "durationMs": 4832,
  "summary": { "total": 17 },
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

### Asynchronous scan

For large sites, start a scan and poll for the result.

`POST /api/external/cookie-scanner/scan/async` with `{ "websiteUrl": "https://example.com" }` returns a `scanId` with `status: "queued"`.

`GET /api/external/cookie-scanner/scan/async/:scanId?domain=example.com` returns the status and, when `status` is `completed`, the cookies. Only the key that started the scan can read it.

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
