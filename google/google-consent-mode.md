---
description: How Okito sets Google consent mode for your Google tags.
---

# Google Consent Mode v2

Consent mode lets you communicate your visitors' cookie or app identifier consent status to Google. Tags adjust their behaviour and respect the choices visitors make in the Okito banner. Okito sets the consent mode **default** and **update** commands for you; consent mode itself does not show a banner.

{% hint style="info" %}
Consent mode is a way to pass consent choices to Google tags. It is not designed to meet any particular legal or regulatory requirement; which consent your site needs depends on your own obligations.
{% endhint %}

Google Consent Mode is included from the Standard plan.

{% hint style="info" %}
Missing consent mode or TCF signals on your Google tags? Contact [Okito support](../help/support.md) first, not Google. Google support asks for proof that you contacted your CMP before it looks into consent mode questions.
{% endhint %}

## What Okito does

1. **Default**: before any Google tag runs, the Okito Consent Mode snippet (or the WordPress plugin, Shopify app or GTM template) sets the default consent state. Visitors in regions where your banner asks for consent first start **denied**; other visitors start with the state you choose in [Where consent is not required](../compliance/consent-not-required.md).
2. **Update**: when the visitor chooses (or returns with a stored choice), the Okito script sends a consent mode update with the granted or denied state for each consent type.
3. **Settings**: Okito sets `ads_data_redaction`, optionally `url_passthrough`, and Okito's Google developer ID `developer_id.dZGJiMm`.

## Set it up

1. Choose **advanced** or **basic** consent mode in Banner Builder → General → **Google tags**. See [Basic and advanced consent mode](basic-and-advanced.md).
2. Install Okito so it runs before your Google tags. See [Load order](load-order.md).
3. Check the setup with [Debug mode](debug-mode.md) and the [Consent mode check](consent-mode-check.md).

## Guides

* [Consent mode settings reference](settings-reference.md)
* [Basic and advanced consent mode](basic-and-advanced.md)
* [Load order](load-order.md)
* [Google tag gateway (GTG)](google-tag-gateway.md)
* [IAB TCF and Google](tcf-and-google.md)
* [Google Consent Mode banner template](../banner/google-consent-mode-template.md)

## Google documentation

* [Consent mode overview](https://developers.google.com/tag-platform/security/concepts/consent-mode)
* [Set up consent mode on websites](https://developers.google.com/tag-platform/security/guides/consent)
* [gtag.js API reference (consent command)](https://developers.google.com/tag-platform/gtagjs/reference)
* [Tag Manager consent APIs](https://developers.google.com/tag-platform/tag-manager/templates/consent-apis)
* [Use consent mode with the IAB TCF](https://developers.google.com/tag-platform/security/guides/implement-TCF-strings)
* [Verify and debug consent mode](https://developers.google.com/tag-platform/security/guides/consent-debugging)
* [About consent mode (Google Ads Help)](https://support.google.com/google-ads/answer/10000067)
* [How Google uses information from sites or apps that use its services](https://business.safety.google/privacy)
