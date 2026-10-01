---
description: How Google tags read consent on an IAB TCF site.
---

# IAB TCF and Google

On an [IAB TCF](../compliance/iab-tcf.md) site, Google tags can get consent from two places: the TC string and consent mode.

## Google as a TCF vendor

Google is IAB TCF vendor **755**. Okito adds it to the vendor list of every IAB TCF site automatically, so you don't need to add it yourself. Google reads its advertising consent from the TC string.

## Google ads consent from the TC string

Turn on **Google ads consent from the TC string** (Banner Builder → General, under IAB TCF). Okito then sets `enableAdvertiserConsentMode` in the TC data, so Google tags read `ad_storage`, `ad_user_data` and `ad_personalization` from the TC string. `analytics_storage` is still sent through consent mode.

## TCF purposes and consent mode

On IAB TCF sites, Okito sends the consent mode update from the TCF purposes the visitor accepted, based on the rule Google uses when it reads a TC string. Storage needs purpose 1 (store and/or access information on a device), and the advertising types need consent for Google as a vendor (755).

| Consent mode type | Granted when the visitor accepted |
| --- | --- |
| `ad_storage` | Google, purpose 1 and an advertising purpose (2, 3 or 4) |
| `ad_user_data` | Google, purposes 1 and 7 |
| `ad_personalization` | Google, purposes 3 and 4 |
| `analytics_storage` | Purpose 1, and purpose 8 or 9 |
| `functionality_storage` | Purpose 1 |
| `personalization_storage` | Purpose 1, and purpose 5 or 6 |
| `security_storage` | Always granted |

A purpose you do not allow Google with a [publisher restriction](../compliance/iab-tcf.md#publisher-restrictions) counts as not accepted for `ad_storage`, `ad_user_data` and `ad_personalization`. The other types don't change.

`ad_storage` asks for an advertising purpose on top of Google's rule, so a visitor who refused every advertising purpose never grants it (tags of other ad vendors in Google Tag Manager often check `ad_storage`). A category switched on in the TCF preferences (Advertisement, Analytics, Functional) grants its types too; for the advertising types only together with consent for Google, and not on a purpose you do not allow Google. Because Okito always lists Google, **Accept all** grants everything, unless a publisher restriction does not allow Google a purpose that an advertising type needs (for example purpose 1, 3, 4 or 7). The consent records use the same purpose rule without the vendor condition.

## Additional Consent

Turn on **Additional Consent (AC String)** to ask for consent for Google's ad technology providers that are not registered in the IAB TCF. Okito creates the AC string alongside the TC string. It is available to tags through `__tcfapi` (`addtlConsent`), in the `localStorage` key `IABTCF_AddtlConsent` (in apps, the same key in the [mobile SDKs' storage](../installation/mobile-apps.md)) and, for server-side use, in the first-party `addtl_consent` cookie (kept as long as the `euconsent-v2` cookie).

## Load order and the TCF stub

Google tags look for the TCF API (`__tcfapi`) when they start. When your banner uses IAB TCF (TCF is on), the Okito Consent Mode snippet (or, with Google tags set to basic or off, the stub **Install banner** shows on its own), the WordPress plugin and the Shopify app add a small **TCF stub** at the top of the page, so `__tcfapi` exists before any Google tag runs, even if the Okito script loads later. The GTM template adds it when **My banner uses IAB TCF** is ticked (see [IAB TCF sites](../installation/google-tag-manager.md#iab-tcf-sites)). On sites without TCF, Google tags follow Google Consent Mode. [Debug mode](debug-mode.md) warns if Google tags ran before the TCF API was available.

## Where TCF applies

On plans that include IAB TCF, Okito uses the TCF banner for visitors in the EEA, the UK and Switzerland on the GDPR side of your banner, as Google's EU user consent policy expects for personalised ads.
