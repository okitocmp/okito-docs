---
description: The pieces of Okito and what happens when a visitor opens your site.
---

# How Okito works

## The pieces

| Piece | What it is |
| --- | --- |
| **Dashboard** | [app.okito.com](https://app.okito.com). Where you add websites, design the banner, scan cookies and read reports. |
| **Website key** | A public identifier for one website, for example `eu_okito-d288cf-c0d2b7-d`. It appears in your script URL. |
| **Okito script** | `https://cdn.okito.com/js/YOUR_WEBSITE_KEY`. Loads your banner configuration and applies consent on the page. |
| **Consent Mode snippet** | A small inline script for `<head>` that sets Google consent mode defaults before any Google tag runs. |
| **Integrations** | WordPress plugin, Shopify app, Webflow app, Framer plugin, GTM template and mobile SDKs. They install the script and snippet for you. |

## What happens on a page view

1. The page loads the Consent Mode snippet (if installed). Google tags now start with a **denied** state in regions that need consent, and **granted** elsewhere (you can change this; see [Where consent is not required](../compliance/consent-not-required.md)).
2. The Okito script loads. It detects the visitor's region and language and decides which experience to show: the GDPR banner, the US state law banner, the IAB TCF banner, or no banner.
3. If the visitor already chose, Okito applies that choice right away: it sends a consent mode **update**, releases the scripts the visitor allowed and notifies other platforms.
4. If not, Okito shows the banner, counts the banner view anonymously (see [What the banner sends](#what-the-banner-sends)) and holds back tracking scripts in categories that need consent.
5. When the visitor chooses (Accept All, Reject All or Save preferences), Okito:
   * stores the choice in the browser,
   * records it in your [consent records](../compliance/consent-records.md), under a random visitor ID that the browser keeps from the first choice on,
   * sends the consent mode **update** to Google tags,
   * updates Microsoft UET, Amazon, Meta and TikTok signals, the WordPress Consent API and, in TCF mode, the TC string,
   * releases the scripts in the allowed categories and services,
   * fires the `okito:consent` event (every template) and, for the GDPR banner, `cookiemanager:consent` for your own code (see [Consent events](../developers/events.md)).

## What the banner sends

Before the visitor makes a choice, the banner sends one request to count the banner view: the website ID, the banner ID and, during an [A/B test](../banner/ab-testing.md), the version shown. It carries no visitor ID, page address, page title or device details. Counting the view reads and writes nothing on the visitor's device, and the request sends no referrer. Okito derives the country from the IP address when the request arrives and does not store the address. Views from crawlers and headless browsers (recognised by their user agent) are not counted.

Besides that count, the banner only loads what it shows, without a visitor ID: on [IAB TCF](../compliance/iab-tcf.md) sites the vendor list, and, when the visitor opens a vendor's details, that vendor's device storage disclosure (the request names only the vendor). The two exceptions are a [Global Privacy Control](../compliance/us-state-laws.md#global-privacy-control-gpc) signal on the US template, which Okito records as an opt-out without a click (see below), and [cross-device consent](../developers/cross-device-consent.md) (further down).

After a choice, the banner sends the [consent record](../compliance/consent-records.md): a random visitor ID kept in the browser's local storage, the choice, how it was made, and the banner and notice version. Okito adds the shortened IP address, the browser's user agent and the time. A Global Privacy Control opt-out on the US template is recorded the same way, once per browser session, with no click: under the visitor ID the browser already has, or else under a one-off receipt ID (starting `gpc_`) that is not kept in the browser. On a site that has no cookie list yet, the banner also sends the names of the cookies on the page (not their values), once per browser session and only after the visitor's choice (never before), so they appear in your cookie list.

Okito does not fingerprint devices or use the Topics API. The banner's requests to Okito send no referrer; the request for the Okito script itself comes from your page and follows your page's referrer policy.

With [cross-device consent](../developers/cross-device-consent.md), a page where a user is signed in also asks Okito for that user's stored choice, with the hashed user ID your server signed.

## Where the choice is stored

The choice is stored in the visitor's browser for the site address (for example `www.example.com`), so it applies to every page there. By default each subdomain asks on its own; with [Share consent across subdomains](../banner/subdomain-consent.md) on, one choice applies to your domain and all its subdomains. Okito asks again after 13 months, when the visitor reopens the banner, when you ask every visitor again after a meaningful change, and on IAB TCF sites when your vendors, publisher restrictions or the TCF policy version change, or when you turned IAB TCF on after the visitor chose (see [Consent renewal](../compliance/consent-renewal.md)).

## Categories

Every cookie and script belongs to one category: **Necessary**, **Functional**, **Analytics**, **Performance**, **Advertisement** or **Uncategorized**. Necessary is always on. See [Cookie categories](../cookies-and-scripts/cookie-categories.md).
