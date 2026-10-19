---
description: List your site's cookies on your cookie policy page; the list follows every scan.
---

# Cookie table for your cookie policy

Add one line to your cookie policy page, and the Okito script fills it with the cookies from your latest [scan](cookie-scanner.md):

```html
<div data-okito-cookie-table></div>
```

* Cookies are grouped by [category](cookie-categories.md), with the category's name and description. Necessary cookies are marked as always active.
* Each cookie shows its name, its provider (the [service](services.md) it belongs to, otherwise the domain that sets it), its purpose and its duration.
* The table follows the banner language: headings, category names and durations, and the cookie descriptions, which are translated automatically into your banner languages (a new language can take a few minutes; until then the description shows as written). Descriptions you write yourself in Cookie Manager are taken to be in your default language.
* A button under the table opens the preference window, so visitors can change their choice from the policy page.
* After every scan the table shows the new list. You never edit the policy for it.
* The table stays while no banner is shown (site paused or monthly pageview limit reached), without the button.

Find the line in the dashboard under **Cookie Manager → Cookies**. The page must load the Okito script, like every page of your site.

## WordPress

Add the `[okito_cookie_table]` shortcode to your cookie policy page (Okito plugin 1.1.5 or later), or the line above in a Custom HTML block.

## Shopify

In the Okito app, **Settings → Cookie table → Add cookie table** (also at the bottom of **Cookie Manager → Cookies**) opens the theme editor with the **Cookie table** block added to the default page template. The block shows on every page that uses that template: if other pages use it too, give your cookie policy page its own template (theme editor: **Pages → Create template**, then choose it under **Theme template** on the page) and add the block there (**Add section → Apps → Cookie table**). Click **Save**. The app's **Cookie banner** embed must be on (see [Shopify](../installation/shopify.md#install)).

## Styling

The table uses your page's font and colours. Its elements have classes you can style: `.okito-cookie-table`, `.okito-ct-title`, `.okito-ct-description`, `.okito-ct-table`, `.okito-ct-provider` and `.okito-ct-button`.

## Single-page apps

If your page adds the element after the Okito script has loaded, call `OkitoCMP.renderCookieTable()` once the element is on the page.
