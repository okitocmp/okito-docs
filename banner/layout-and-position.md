---
description: Banner, box or pop-up, and where it appears.
---

# Layout and position

Choose the layout in Banner Builder → **Layout**.

| Layout | Positions |
| --- | --- |
| **Banner** (full width) | Top, bottom |
| **Box** | Bottom left, bottom right, bottom centre, top left, top right, top centre |
| **Pop-up** | Centre of the screen, with an overlay |

## Other layout options

* **Reopen button side**: whether the floating [reopen button](reopen-button.md) sits on the left or the right.
* **Close button**: an X in the corner of the banner. Closing the banner counts as **Reject all**: only necessary cookies are used, and the choice is recorded like any other. It is off by default. The Focus, Noir and Nova designs always have one. The US State Laws notice has none.
* **Corner radius and shadow**: the banner's rounding and shadow.

## Logo and custom CSS

Available on the Professional plan (Banner Builder → **Layout**).

* **Logo**: an https address. It replaces the Okito icon on the banner; in design themes it sits above the title (Harbor shows it in place of its icon). Addresses that are not https are not shown.
* **Custom CSS**: added on your site after Okito's own styles, so your rules win at equal specificity. Useful selectors: `#cm-cookie-banner` (the banner), `[data-action="accept-all"]`, `[data-action="reject-all"]`, `[data-action="customize"]`. `@import` and anything that could run code are removed; up to 20,000 characters.
* The Banner Builder preview shows the logo but does not apply the CSS: check the banner on your site after saving.
* On a lower plan the logo and CSS stay saved but are not shown.
