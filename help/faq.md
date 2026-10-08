---
description: Short answers to common questions.
---

# FAQ

### Is Okito a certified CMP?

Okito is an IAB Europe registered CMP for the Transparency & Consent Framework (CMP ID 508).

### Does Okito support Google Consent Mode v2?

Yes. Basic consent mode is available on every plan; advanced consent mode is included from the Standard plan. See [Google Consent Mode v2](../google/google-consent-mode.md).

### Do I need Google Tag Manager?

No. You can install Okito with the snippet and script, a plugin or an app. If you already use GTM, the [Okito CMP template](../installation/google-tag-manager.md) is the easiest way.

### Will Okito slow down my site?

The Okito script loads from a CDN, the banner renders in an isolated Shadow DOM, and the Consent Mode snippet is a few lines of inline code. See [CSP, performance and SPAs](../developers/csp-and-performance.md).

### Which languages does the banner support?

The banner's titles and buttons are available in 50+ languages, and IAB TCF texts use IAB Europe's official translations. Default banner messages are ready in English, Turkish, German, French, Spanish and Italian. See [Content and languages](../banner/content-and-languages.md).

### Does Okito work on mobile apps?

Yes, with the native [iOS and Android SDKs](../installation/mobile-apps.md).

### Does the banner show to everyone?

By default, visitors in every region see the banner. You can hide it for visitors outside the regions whose laws need prior consent. See [Where consent is not required](../compliance/consent-not-required.md).

### Where is my data stored?

In the region you chose when you created your account: Türkiye or the EU. See [Data regions](../getting-started/data-regions.md).

### Can visitors change their mind?

Yes, with the floating reopen button or your own "Cookie settings" link. See [Reopen button](../banner/reopen-button.md).

### How long is a choice remembered?

Up to 13 months, or less: Okito also asks again when you ask every visitor again after a meaningful change, and on IAB TCF sites when your vendors or restrictions change. See [Consent renewal](../compliance/consent-renewal.md).

### Does Okito respect Global Privacy Control?

Yes. See [US state privacy laws and GPC](../compliance/us-state-laws.md).

### Can I test on localhost?

Yes, the banner loads on `localhost` for development. Installation verification and cookie scans need a public HTTPS address.
