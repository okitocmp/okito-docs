---
description: Opt-out notices, "Do Not Sell or Share" and Global Privacy Control.
---

# US state privacy laws and GPC

US state privacy laws such as the CCPA / CPRA (California), VCDPA (Virginia), CPA (Colorado), CTDPA (Connecticut) and UCPA (Utah) follow an **opt-out** model: data processing can start by default, but visitors must be able to opt out of the sale and sharing of their personal data.

## The US State Laws template

With the [US State Laws or GDPR & US State Laws template](../banner/consent-templates.md):

* US visitors see a notice at collection with a **Do Not Sell or Share My Personal Information** link.
* The link opens a pop-up where the visitor can opt out of the sale and sharing of their data, and **limit the use and disclosure of sensitive personal information**.
* Cookies and scripts run by default; an opt-out turns off advertising (and the other categories the visitor turns off), deletes their cookies where possible and sends the denied consent mode update.

Add the same link to your site's footer. The CCPA requires it on your homepage.

## Global Privacy Control (GPC)

When the visitor's browser sends the [Global Privacy Control](https://globalprivacycontrol.org/) signal:

* In the US template, Okito treats it as an opt-out of sale and sharing, without the visitor having to click anything, and stores it as their choice.
* Google consent mode starts **denied** for that visitor, wherever they are.
* The US Privacy string (`__uspapi`) reports the opt-out (`1YYN`).

## US Privacy API

Okito provides the IAB US Privacy API (`__uspapi`) for ad tech that reads the US Privacy string. See [IAB TCF and US privacy APIs](../developers/tcf-and-usp-apis.md).

## Privacy requests

US laws give residents rights to access, delete and correct their data and to appeal a refusal. The public [privacy request form](privacy-requests.md) covers these, with a 45-day response deadline.
