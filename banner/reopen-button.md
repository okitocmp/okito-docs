---
description: Let visitors change or withdraw consent at any time.
---

# Reopen button and consent withdrawal

After a visitor chooses, a small floating button stays on the page. Clicking it reopens the banner or preference centre, so the visitor can change or withdraw consent as easily as they gave it.

* Choose its side (left or right) in Banner Builder → Layout.
* Place it where it isn't covered by a chat widget or cookie-free zone.

## Open the banner from your own link

You can also add a "Cookie settings" link to your footer:

```html
<a href="#" onclick="window.CookieManager && window.CookieManager.forceShowBanner(); return false;">Cookie settings</a>
```

See [JavaScript API](../developers/javascript-api.md).

## US State Laws

With the US State Laws template, the **Do Not Sell or Share My Personal Information** link opens the opt-out pop-up. Add the same link to your footer, as the CCPA requires a link on your homepage.

## What happens on withdrawal

When a visitor turns a category off, Okito sends the consent mode update (`denied`), updates the other platforms, stops releasing scripts in that category and deletes the category's cookies that it can reach.
