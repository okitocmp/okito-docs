---
description: Amazon Consent Signal (ACS) for Amazon Ads tags.
---

# Amazon Ads

Amazon Ads tags read consent from the **Amazon Consent Signal**. Okito provides it automatically.

## Without IAB TCF

Okito writes a first-party `amzn_consent` cookie with the visitor's country and two signals, `amzn_ad_storage` and `amzn_user_data`:

* Before a choice: `DENIED` in regions that need consent, `GRANTED` elsewhere (following [Where consent is not required](../compliance/consent-not-required.md)). Okito writes this default only when your cookie scan or services list includes Amazon Ads; on other sites it writes no cookie before the visitor chooses.
* After the choice: `GRANTED` if the visitor accepts **Advertisement**, otherwise `DENIED`.

{% hint style="warning" %}
If you add Amazon Ads tags, run a cookie scan (or add the Amazon Ads service) right away. Until Okito knows the site uses Amazon Ads, Amazon gets no `DENIED` default before the visitor's choice. Okito does not write the cookie on sites without Amazon Ads, so that nothing is stored on their visitors' devices before a choice.
{% endhint %}

## With IAB TCF

On TCF sites, Amazon reads the TC string (`euconsent-v2`) instead, so Okito doesn't write `amzn_consent`. Make sure Amazon is in your TCF vendor list.
