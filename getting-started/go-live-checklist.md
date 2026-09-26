---
description: Check these before real visitors see your banner.
---

# Go-live checklist

## Setup

- [ ] The website in Okito uses your real production domain (with or without `www`, as your site is served).
- [ ] The banner text matches your processing, and your privacy / cookie policy link works.
- [ ] You chose the right [consent template](../banner/consent-templates.md) for your visitors (GDPR, US or both).
- [ ] If you use Google tags, you chose [basic or advanced consent mode](../google/basic-and-advanced.md).

## Installation

- [ ] The Okito script is on **every** page, including checkout, 404 and landing pages.
- [ ] The script is installed **once**: not in the theme *and* a plugin *and* GTM.
- [ ] In advanced mode, the Consent Mode snippet and the Okito script are at the top of `<head>`, **above** Google Tag Manager and gtag.js. See [Load order](../google/load-order.md).
- [ ] Your Content-Security-Policy allows `https://cdn.okito.com`. See [CSP, performance and SPAs](../developers/csp-and-performance.md).

## Testing

- [ ] In a private window without ad blockers, the banner appears.
- [ ] **Accept All**, **Reject All** and **Save preferences** each work, and the banner stays closed after a reload.
- [ ] The reopen button lets you change your choice.
- [ ] `?okito_debug=1` shows a green box. See [Debug mode](../google/debug-mode.md).
- [ ] With Google Tag Assistant, Google tags show `denied` before a choice and `granted` after Accept All.
- [ ] You ran a [cookie scan](../cookies-and-scripts/cookie-scanner.md), and no marketing cookie is listed as Necessary.
- [ ] The [consent mode check](../google/consent-mode-check.md) shows no gaps.
