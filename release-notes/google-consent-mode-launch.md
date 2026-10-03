---
description: >-
  Google Consent Mode v2 in Okito, from setup wizard to a check across all your
  pages.
---

# Launch: Google Consent Mode v2

_September 2026_

Okito now sets up Google Consent Mode v2 for you, from the first minute. If your site uses Google Analytics, Google Ads or Google Tag Manager, your Google tags receive your visitors' consent choices without extra code.

## What's new

### Consent mode in the setup wizard

The setup wizard has a new **Google consent mode** step. Keep **Enable Google Consent Mode** selected and choose **advanced** (recommended) or **basic**. Okito configures your banner accordingly. [Basic and advanced consent mode →](../google/basic-and-advanced.md)

### Default and update commands, by region

Okito sets the consent mode **default** before your Google tags run and sends the **update** as soon as the visitor chooses. Visitors in regions where your banner asks for consent first start denied; you decide what happens elsewhere. [Consent mode settings →](../google/settings-reference.md)

### Install your way

* Consent Mode snippet and Okito script for any website
* **Okito CMP** template in the Google Tag Manager Community Template Gallery
* WordPress plugin, Shopify app, Webflow app and Framer plugin

[Installation →](../installation/installation.md)

### A banner template for Google's requirements

A new **Google Consent Mode template** explains analytics and personalisation, links to how Google uses information from sites that use its services, and keeps a clear **Accept All**. Banner Builder recommends it when you use consent mode without IAB TCF. [Banner template →](../banner/google-consent-mode-template.md)

### Check your setup

* **Debug mode**: add `?okito_debug=1` to any page to see whether the consent mode default was set before your Google tags. [Debug mode →](../google/debug-mode.md)
* **Consent mode check**: every cookie scan checks all scanned pages and emails you when it finds gaps, with fix instructions. [Consent mode check →](../google/consent-mode-check.md)

### Google tag gateway guidance

Using Google tag gateway? Learn how to verify it and keep consent in order. [Google tag gateway →](../google/google-tag-gateway.md)

### IAB TCF and Google

On IAB TCF sites (Okito is a registered TCF CMP, ID 508), Google can read advertising consent from the TC string, and Additional Consent covers Google's ad technology providers outside the TCF. [IAB TCF and Google →](../google/tcf-and-google.md)

### More controls

`ads_data_redaction` and `url_passthrough` settings, Okito's Google developer ID on every installation, and consent signals for Microsoft Advertising, Amazon Ads, Meta and TikTok.

## Availability

Google Consent Mode and IAB TCF are included in the **Standard** and **Professional** plans. [Plans →](../getting-started/plans-and-limits.md)

## Get started

New to Okito? Start with the [Quick start](../getting-started/quick-start.md). Already using Okito? Open Banner Builder → General → **Google tags** and run a cookie scan to see your consent mode check.

Questions? Email [info@okito.com](mailto:info@okito.com).
