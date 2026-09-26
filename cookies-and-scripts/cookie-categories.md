---
description: The six categories Okito uses for cookies and scripts.
---

# Cookie categories

| Category | Purpose | Consent needed (GDPR template) |
| --- | --- | --- |
| **Necessary** | Needed for the site to work: session, security, load balancing, storing the consent choice. | No. Always on. |
| **Functional** | Extra features and preferences: language, chat, embedded videos. | Yes |
| **Analytics** | Measuring how visitors use the site: Google Analytics, Hotjar, Microsoft Clarity. | Yes |
| **Performance** | Site speed and performance measurement. | Yes |
| **Advertisement** | Advertising and remarketing: Google Ads, Meta Pixel, TikTok Pixel, Microsoft Advertising. | Yes |
| **Uncategorized** | Cookies not yet reviewed. | Yes |

You can rename categories and change their descriptions per language in Banner Builder → Content.

## How categories map to other systems

| Okito category | Google consent mode | WP Consent API | Other platforms |
| --- | --- | --- | --- |
| Necessary | `security_storage` (always granted) | functional | — |
| Functional | `functionality_storage`, `personalization_storage` | preferences | — |
| Analytics | `analytics_storage` | statistics | — |
| Advertisement | `ad_storage`, `ad_user_data`, `ad_personalization` | marketing | Microsoft UET, Amazon, Meta, TikTok |

See [Consent mode settings reference](../google/settings-reference.md) and [WordPress Consent API](../integrations/wp-consent-api.md).

{% hint style="warning" %}
Put a cookie in Necessary only if the site can't work without it. Analytics and advertising cookies are never necessary.
{% endhint %}
