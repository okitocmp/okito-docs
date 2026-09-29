---
description: Banner texts, button labels and languages.
---

# Content and languages

## Languages

In Banner Builder → General → **Language Settings**:

* **Supported Languages**: the languages your banner is available in. English is always included.
* **Default Language (Fallback)**: used when the visitor's language is not in your list.

Okito picks the language from the page (`<html lang>`, a language in the URL path such as `/de/`) and the visitor's browser. More than one language needs the Beginner plan or higher.

On a website whose country is Türkiye, a visitor whose browser is set to Turkish gets the banner in Turkish, even if the page says it is in another language. If Turkish is not one of your languages, the banner uses Okito's default Turkish texts. A language the visitor picks in the banner, or one in the URL path, still comes first.

## Texts

In the **Content** tab, choose a language and edit:

* **Banner title** and **message**
* **Accept All**, **Reject All**, **Manage Preferences** and **Save** button labels
* Category names and descriptions in the preference centre
* Cookie list labels (Cookie, Duration, Description, Always Active)
* **Links** to your privacy policy and Aydınlatma Metni (see below)

Okito ships default banner messages for the GDPR template in English, Turkish, German, French, Spanish and Italian (KVKK wording in Turkish and English), and titles and button labels in 50+ languages. Adapt the defaults to your own processing and privacy policy.

### Privacy policy and KVKK disclosure notice links

In **Content → Links**, enter the full addresses (starting with `https://`) of:

* **Privacy policy**: shown to every visitor, under the banner text.
* **Aydınlatma Metni (KVKK)**: for a website whose country is Türkiye. Visitors in Türkiye get the KVKK text, and this link before the privacy policy link, as "Aydınlatma Metni" in Turkish ("Disclosure Notice" in English).

The links open in a new tab and use the visitor's language for the privacy policy label. An address that doesn't start with `http://` or `https://` is not shown.

### Links in the message

Web addresses that start with `https://` in the banner message also become links automatically.

## IAB TCF texts

When [IAB TCF](../compliance/iab-tcf.md) is on, the banner uses IAB Europe's official texts and translations for purposes, features and vendors. These fields are locked in Banner Builder so the texts can't drift from the official wording.

## Google Consent Mode template

If you use Google consent mode without IAB TCF, the Content tab recommends the Google Consent Mode template. See [Google Consent Mode banner template](google-consent-mode-template.md).
