---
description: Every cookie scan checks all scanned pages for consent mode gaps, and emails you when it finds any.
---

# Consent mode check

Every cookie scan also checks each page it opens, before any consent is given:

* whether the **Okito script** is on the page,
* whether the **consent mode default is set before the first Google tag**,
* whether a late Google tag is served from **your own domain** (Google tag gateway),
* in basic mode, whether a Google tag loaded before the visitor consented.

Open **Consent mode check** in the dashboard to see the report page by page and run a new check. Scheduled scans run it automatically, and you get an email when a scan finds gaps.

## The report

For each page, the report shows the result and a **How to fix** link:

| Result | Meaning | Fix |
| --- | --- | --- |
| **The consent mode default was set before the first Google tag.** | All good. | — |
| **Late** | A Google tag ran before the consent mode default. | First verify whether the tag is served through Google tag gateway; if so follow the [GTG steps](google-tag-gateway.md), otherwise fix the [load order](load-order.md). |
| **Order held by chance** | Your Google tags were queued before the consent mode default. Okito put its default in front because it loaded before Google's script on this scan; on other page views Google's script can load first. | Put the Okito Consent Mode snippet above your Google tags ([load order](load-order.md)). |
| **No default** | Google tags run but no consent mode default was set. | Add the Consent Mode snippet or check the installation. |
| **Okito script missing** | The page has no banner and no consent mode default. | Add the Okito code to that page (often pages built with a separate tool, such as a catalogue viewer or 3D tour). |
| **Basic mode: tag loaded before consent** | In basic mode, a Google tag loaded before the visitor consented. | [Mark the tag](../cookies-and-scripts/manual-script-marking.md) so Okito can hold it. |
| **No Google tag** / **consent mode off** | For information only. | — |

## Verify Google tag gateway yourself

The scan flags a late tag as *likely served through Google tag gateway* when it loads from your own domain. Always verify this yourself:

1. Open the page with your browser's developer tools on the **Network** tab and reload. If the Google tag (gtag/js or gtm.js) loads from a path on your own domain instead of `www.googletagmanager.com`, it is served through Google tag gateway.
2. Open `https://your-domain/your-gateway-path/healthy` (for example `https://example.com/metrics/healthy`). If it shows `ok`, the gateway is set up.
3. If it is served through Google tag gateway, follow the [Google tag gateway steps](google-tag-gateway.md). If not, move the Okito snippet and script above your Google tags.

## Email notification

When a scan finds gaps, the account owner gets an in-app notification and an email (unless compliance alerts are turned off in the notification settings). The email lists each affected page with a **How to fix** link, the manual Google tag gateway verification steps above, and a link to the report.

![Consent mode gaps email](../.gitbook/assets/consent-mode-check-email.png)

## Run a check

Click **Check now** on the Consent mode check page. It runs a cookie scan (counted against your monthly scans) and updates the report when it finishes.
