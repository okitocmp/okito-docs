---
description: GDPR (opt-in), US State Laws (opt-out), or both by region.
---

# Consent templates: GDPR, US and both

The consent template decides how the banner asks for consent. Choose it in Banner Builder → General → **Consent Template**.

## GDPR

An **opt-in** banner for the GDPR (EU / EEA), UK GDPR, Switzerland and Türkiye's KVKK:

* Non-essential cookies and scripts stay off until the visitor accepts.
* **Accept All**, **Reject All** and **Manage Preferences** are offered side by side.
* The preference centre lets the visitor choose by category and service.

For Turkish-language banners on websites based in Türkiye, the default texts follow KVKK wording.

## US State Laws

An **opt-out** notice for US state privacy laws such as the CCPA / CPRA (California) and the laws of Virginia, Colorado, Connecticut and Utah:

* Cookies and scripts run by default.
* The banner shows a **Do Not Sell or Share My Personal Information** link. The visitor can opt out of the sale and sharing of their data and limit the use of sensitive data.
* The browser's [Global Privacy Control](../compliance/us-state-laws.md) signal is treated as an opt-out.

The opt-out notice is shown to US visitors only. A visitor located outside the US (for example in the EU or Türkiye) sees the GDPR opt-in banner instead, because an opt-out notice does not meet those laws. When a visitor's location cannot be determined, the US notice is shown.

## GDPR & US State Laws

Both templates, chosen per visitor by location: US visitors see the US notice; everyone else sees the GDPR banner. You edit each template's texts separately (switch with the template selector in the Content tab).

This template needs geo-targeting, included from the Beginner plan.

## Which one do I need?

| Your visitors | Template |
| --- | --- |
| Mainly EU, UK, Switzerland or Türkiye | GDPR |
| Only US | US State Laws |
| Both, or worldwide | GDPR & US State Laws |

{% hint style="info" %}
Outside these regions (for example Japan), you decide whether visitors see a banner and whether measurement starts on. See [Where consent is not required](../compliance/consent-not-required.md).
{% endhint %}
