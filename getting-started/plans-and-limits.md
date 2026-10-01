---
description: What each plan includes. Prices are on the pricing page.
---

# Plans and limits

Okito has four plans. **Each website has its own plan**: you can run one site on Professional and another on Free, and upgrading one website doesn't change the others. Pageview and scan limits apply per website. Current prices are on the [pricing page](https://app.okito.com/pricing).

| | Free | Beginner | Standard | Professional |
| --- | --- | --- | --- | --- |
| Pageviews per month | 3,000 | 75,000 | 250,000 | 500,000 |
| Pages per cookie scan | 5 | 50 | 100 | 200 |
| Cookie scans per month | 5 | 20 | 50 | Unlimited |
| Consent banner, GDPR / KVKK | ✓ | ✓ | ✓ | ✓ |
| Consent records | ✓ | ✓ | ✓ | ✓ |
| Cookie scanner | ✓ | ✓ | ✓ | ✓ |
| Advanced customisation and themes | | ✓ | ✓ | ✓ |
| [Logo and custom CSS](../banner/layout-and-position.md#logo-and-custom-css) | | | | ✓ |
| Multiple languages | | ✓ | ✓ | ✓ |
| Automatic script blocking | | ✓ | ✓ | ✓ |
| Geo-targeting (GDPR + US, banner only where required) | | ✓ | ✓ | ✓ |
| Policy generator | | ✓ | ✓ | ✓ |
| **Google Consent Mode v2**, basic | ✓ | ✓ | ✓ | ✓ |
| **Google Consent Mode v2**, advanced | | | ✓ | ✓ |
| **IAB TCF** | | | ✓ | ✓ |
| Advanced analytics | | | ✓ | ✓ |
| [A/B testing the banner design](../banner/ab-testing.md) | | | | ✓ |
| Scheduled scans | | | | ✓ |
| REST API | | | | ✓ |
| Priority support | | | | ✓ |

## What happens at a plan limit

* **Pageviews**: when a website reaches its monthly pageview quota, the Okito script is paused for that website until the next month or an upgrade. The site keeps working, but no banner is shown.

A pageview is a full page load that runs the Okito banner script. Reloading a page or opening another page counts again. Navigating inside a single-page app (without a page load) does not, and a page that includes the Okito code twice counts once.
* **Scans**: you cannot start a new scan until the next month or an upgrade.
* **Google Consent Mode and IAB TCF on Free / Beginner**: Google tags use [basic consent mode](../google/basic-and-advanced.md#basic-configuration-google-tags-are-blocked-until-consent): they wait for the visitor's consent and then get the visitor's choice. Advanced consent mode and IAB TCF are locked in the dashboard; your choice in the setup wizard is saved and applies as soon as you upgrade. You can still turn consent mode off in Banner Builder.

## Shopify

On Shopify, you pay for Okito through Shopify App Pricing, with the same four plans. See [Shopify](../installation/shopify.md).
