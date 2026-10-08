---
description: When Okito asks visitors again.
---

# Consent renewal

A visitor's choice is stored in their browser. Okito shows the banner again when:

* the choice is **older than 13 months**,
* the stored choice is missing or can't be read (for example after the visitor cleared their cookies or uses a new browser),
* the visitor clicks the [reopen button](../banner/reopen-button.md) or your "Cookie settings" link,
* you ask every visitor again (see below),
* on [IAB TCF](iab-tcf.md#when-visitors-are-asked-again) sites, your vendor list, your publisher restrictions or the TCF policy version changed, or you turned IAB TCF on after the visitor chose (every visitor the GDPR applies to is then asked once with the TCF banner; see that page for the full list).

## Ask every visitor again

After a meaningful change, such as new banner text, a new cookie policy or a new category, open Banner Builder → General and click **Ask every visitor again**. Every visitor who made their choice before that moment sees the banner on their next page view. Until they choose again, their earlier choice stays in effect. Small fixes, such as correcting a typo, don't need it.

It applies to websites and to apps with the Okito mobile SDKs.

## Signed-in users on several devices

With [cross-device consent](../developers/cross-device-consent.md), a signed-in user's latest choice is applied on their other devices, so they aren't asked again on each one.
