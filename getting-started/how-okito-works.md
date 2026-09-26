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
4. If not, Okito shows the banner and holds back tracking scripts in categories that need consent.
5. When the visitor chooses (Accept All, Reject All or Save preferences), Okito:
   * stores the choice in the browser,
   * records it in your [consent records](../compliance/consent-records.md),
   * sends the consent mode **update** to Google tags,
   * updates Microsoft UET, Amazon, Meta and TikTok signals, the WordPress Consent API and, in TCF mode, the TC string,
   * releases the scripts in the allowed categories and services,
   * fires the `cookiemanager:consent` event for your own code (see [Consent events](../developers/events.md)).

## Where the choice is stored

The choice is stored in the visitor's browser for the website's domain, so it applies to every page of that site. Okito asks again after 13 months (see [Consent renewal](../compliance/consent-renewal.md)), or when the visitor reopens the banner.

## Categories

Every cookie and script belongs to one category: **Necessary**, **Functional**, **Analytics**, **Performance**, **Advertisement** or **Uncategorized**. Necessary is always on. See [Cookie categories](../cookies-and-scripts/cookie-categories.md).
