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

## Google reCAPTCHA

Okito lists Google reCAPTCHA (the `_GRECAPTCHA` cookie and its scripts) as **Necessary**: it protects the forms the visitor submits from spam and abuse, and blocking it until consent breaks those forms (reCAPTCHA v3, for example in Contact Form 7, needs its token when the form is sent). Okito does not block it, and the consent record and cookie table list it as necessary. Mention reCAPTCHA in your privacy policy, as Google's terms ask.

Some data protection authorities consider that reCAPTCHA needs consent because Google also uses the data for its own purposes. If you follow that view, move the reCAPTCHA service to **Functional** under [Services](services.md). The consent record follows that category, and Okito then holds the reCAPTCHA scripts it can intercept (those your site adds after the Okito script has loaded) until the visitor accepts Functional. A reCAPTCHA `<script>` tag written directly in your page's HTML starts before Okito can stop it: mark it yourself (see [Mark scripts manually](manual-script-marking.md)) with `data-cookie-category="functional"`, or the record will say "refused" while reCAPTCHA runs. Your forms then need another spam check for visitors who refuse.
