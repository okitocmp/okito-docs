---
description: How Google tags read consent on an IAB TCF site.
---

# IAB TCF and Google

On an [IAB TCF](../compliance/iab-tcf.md) site, Google tags can get consent from two places: the TC string and consent mode.

## Google as a TCF vendor

Google is IAB TCF vendor **755**. Make sure it is in your vendor list (**IAB TCF** page in the dashboard) if you use Google advertising products. Google reads its advertising consent from the TC string.

## Google ads consent from the TC string

Turn on **Google ads consent from the TC string** (Banner Builder → General, under IAB TCF). Okito then sets `enableAdvertiserConsentMode` in the TC data, so Google tags read `ad_storage`, `ad_user_data` and `ad_personalization` from the TC string. `analytics_storage` is still sent through consent mode.

## Additional Consent

Turn on **Additional Consent (AC String)** to ask for consent for Google's ad technology providers that are not registered in the IAB TCF. Okito creates the AC string alongside the TC string.

## Load order and the TCF stub

Google tags look for the TCF API (`__tcfapi`) when they start. When your banner can use IAB TCF (TCF is on, or your plan includes TCF), the Okito Consent Mode snippet, the WordPress plugin and the Shopify app add a small **TCF stub** at the top of the page, so `__tcfapi` exists before any Google tag runs, even if the Okito script loads later. The GTM template adds it when **My banner uses IAB TCF** is ticked (see [IAB TCF sites](../installation/google-tag-manager.md#iab-tcf-sites)). On sites without TCF, Google tags follow Google Consent Mode. [Debug mode](debug-mode.md) warns if Google tags ran before the TCF API was available.

## Where TCF applies

On plans that include IAB TCF, Okito uses the TCF banner for visitors in the EEA, the UK and Switzerland on the GDPR side of your banner, as Google's EU user consent policy expects for personalised ads.
