---
description: Design and configure your banner without writing code.
---

# Banner Builder overview

Banner Builder is where you set up everything visitors see and everything the banner does. You don't need HTML or JavaScript. The preview on the right updates as you edit.

Click **Save Banner** to apply your changes. There is no separate publish step: the Okito script serves the new version on the next page load. Reload the page in a private window to see it.

## Tabs

| Tab | What you set |
| --- | --- |
| **General** | Banner name, [consent template](consent-templates.md), languages and compliance settings: Google Consent Mode, IAB TCF, Additional Consent, cross-device consent, script blocking and [where consent is not required](../compliance/consent-not-required.md). |
| **Layout** | Banner, box or pop-up, and its [position](layout-and-position.md). |
| **Mobile SDK** | The consent screen for [iOS and Android apps](../installation/mobile-apps.md). |
| **Content** | Title, message and button texts for each language, and the [Google Consent Mode template](google-consent-mode-template.md). |
| **Theme** | One of the [design themes](themes-and-colors.md). |
| **Colors** | Light, dark or custom colours for the banner, pop-up and buttons. |

## Compliance settings (General tab)

| Setting | What it does | Page |
| --- | --- | --- |
| Consent template | GDPR, US State Laws, or GDPR & US State Laws. | [Consent templates](consent-templates.md) |
| Auto Cookie Detection | Uses scan results to categorise cookies and scripts. | [Cookie scanner](../cookies-and-scripts/cookie-scanner.md) |
| Cross-Device Consent | Syncs a signed-in user's choice across devices. | [Cross-device consent](../developers/cross-device-consent.md) |
| Google Consent Mode Integration | Sends consent mode signals to Google tags. | [Google Consent Mode v2](../google/google-consent-mode.md) |
| Google tags | Advanced, basic or off. | [Basic and advanced](../google/basic-and-advanced.md) |
| Redact ads data / Pass ad click information through URLs | `ads_data_redaction` and `url_passthrough`. | [Settings reference](../google/settings-reference.md) |
| Where consent is not required | Banner and measurement outside the regions that need consent. | [Where consent is not required](../compliance/consent-not-required.md) |
| IAB TCF | Turns the banner into an IAB TCF banner with TC string. | [IAB TCF](../compliance/iab-tcf.md) |
| Google ads consent from the TC string | Lets Google read ad consent from the TC string. | [IAB TCF and Google](../google/tcf-and-google.md) |
| Additional Consent (AC String) | Google Additional Consent for ad tech providers not in the TCF. | [IAB TCF](../compliance/iab-tcf.md) |
| Script Blocking | Holds back tracking scripts until consent. | [Script blocking](../cookies-and-scripts/script-blocking.md) |

Some settings depend on your plan (for example Google Consent Mode and IAB TCF from Standard). Locked settings show an upgrade note. See [Plans and limits](../getting-started/plans-and-limits.md).
