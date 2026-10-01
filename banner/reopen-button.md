---
description: Let visitors change or withdraw consent at any time.
---

# Reopen button and consent withdrawal

After a visitor chooses, a small floating button stays on the page. Clicking it reopens the banner or preference centre, so the visitor can change or withdraw consent as easily as they gave it.

* Choose its side (left or right) in Banner Builder → Layout.
* Place it where it isn't covered by a chat widget or cookie-free zone.

## Open the choices from your own link

You can also add a "Cookie settings" link to your footer. It opens the preference centre (with the US State Laws template, the opt-out pop-up), as the floating button does:

```html
<a href="#" onclick="window.CookieManager && window.CookieManager.showPreferences(); return false;">Cookie settings</a>
```

To show the first-layer banner instead, call `window.CookieManager.forceShowBanner()`.

See [JavaScript API](../developers/javascript-api.md).

## US State Laws

With the US State Laws template, the **Do Not Sell or Share My Personal Information** link opens the opt-out pop-up. Add the same link to your footer, as the CCPA requires a link on your homepage.

## What happens on withdrawal

When a visitor turns a category off, Okito sends the consent mode update (`denied`), updates the other platforms, stops releasing scripts in that category and deletes the category's cookies that it can reach.

A choice that refuses something the visitor had allowed (a category, one service, or an IAB TCF purpose, vendor or special feature) is recorded as a **withdrawal** in the consent history and the audit log, so your records show when consent was withdrawn.
