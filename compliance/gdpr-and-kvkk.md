---
description: How Okito's GDPR template supports opt-in consent in the EU, UK, Switzerland and Türkiye.
---

# GDPR, UK GDPR and KVKK

The GDPR, UK GDPR, the Swiss FADP, the ePrivacy rules and Türkiye's KVKK expect prior, informed and freely given consent for cookies that are not strictly necessary. Okito's [GDPR template](../banner/consent-templates.md) is built for this.

## What the GDPR template does

| Expectation | How Okito handles it |
| --- | --- |
| No non-essential cookies before consent | Categories other than Necessary start off. [Script blocking](../cookies-and-scripts/script-blocking.md) holds back trackers; Google tags receive a denied consent mode default. |
| Rejecting is as easy as accepting | **Reject All** sits next to **Accept All** on the first layer. |
| Granular choice | The preference centre offers categories and individual services. |
| Informed consent | Your banner text, a link to your privacy policy, and the cookie list from your scans. |
| Withdrawal at any time | The [reopen button](../banner/reopen-button.md) and your own "Cookie settings" link. |
| Proof of consent | [Consent records](consent-records.md) with timestamp, choice and banner version. |
| Renewal | Okito asks again after 13 months, and sooner when you ask every visitor again after a meaningful change (new text, policy or category). See [Consent renewal](consent-renewal.md). |

## KVKK (Türkiye)

For a website whose country is Türkiye, visitors in Türkiye get the KVKK wording by default ("açık rıza", "Aydınlatma Metni"), in Turkish or English.

* Add your Aydınlatma Metni (disclosure notice) and privacy policy in Banner Builder → **Content → Links**. Visitors in Türkiye see the Aydınlatma Metni link under the banner text, so it can be reached from the first layer, as the Kurul's cookie guide (2022) recommends. See [Content and languages](../banner/content-and-languages.md#privacy-policy-and-kvkk-disclosure-notice-links).
* Add Turkish to your banner's languages: a visitor whose browser is set to Turkish then gets the banner in Turkish, even if your page says it is in another language, unless the URL path has a language (such as `/en/`) or the visitor picked one in the banner.

### KVKK cookie guide checklist

For a website whose country is Türkiye, **Compliance → KVKK** shows a checklist based on the KVKK Authority's guide on cookie practices ("Çerez Uygulamaları Hakkında Rehber", 2022):

* **Checked from your settings**: script blocking is automatic, an Aydınlatma Metni link is set, Turkish is one of your banner's languages, and a scan found cookies to list. Each open item links to where you fix it.
* **Done by Okito**: Reject All next to Accept All, no pre-ticked options, withdrawal through the reopen button, and [consent records](consent-records.md) as proof.
* **Your responsibility**: what your Aydınlatma Metni says, no cookie wall, banner text that doesn't assume consent, a KVKK Art. 9 basis for transfers abroad, and VERBİS registration where required.

The checklist is guidance, not legal advice.

## Your part

* Write your banner text and privacy policy for your own processing.
* Keep the cookie list accurate with regular [scans](../cookies-and-scripts/cookie-scanner.md).
* Handle [privacy requests](privacy-requests.md) within the legal deadlines.
* Record Okito as a processor in your records of processing, where applicable.

{% hint style="warning" %}
Okito is a tool. It does not make a website compliant by itself. Have your setup reviewed by a qualified advisor. See [Legal notice](../help/legal-notice.md).
{% endhint %}
