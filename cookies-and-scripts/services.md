---
description: Let visitors allow or refuse individual services inside a category.
---

# Services and per-service consent

A **service** is one named tool that sets cookies, for example Google Analytics, Google Ads or Meta Pixel. Each service belongs to one category and has URL patterns that match its scripts.

In the preference centre, visitors can switch a whole category or single services inside it. For example, a visitor can allow Analytics but turn off Hotjar.

## Where services come from

* **Automatically from scans**: after each [cookie scan](cookie-scanner.md), Okito creates services for the known providers it found and links their cookies to them.
* **By hand**: in Cookie Manager, add a service with a name, category, description (per language) and URL patterns.

You can hide a service so it isn't offered as a switch.

## How per-service consent works

* If a visitor turns a service off, its scripts stay blocked even if its category is allowed.
* Services the visitor didn't touch follow their category.
* Scripts are matched to services by URL pattern, or by the `data-okito-service` attribute when you [mark scripts by hand](manual-script-marking.md).

Service descriptions are translated into your banner languages automatically; you can edit each translation.
