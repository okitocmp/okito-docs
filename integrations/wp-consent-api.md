---
description: Pass the visitor's choice to the WordPress Consent API, Site Kit and other plugins.
---

# WordPress Consent API and Site Kit

The [WP Consent API](https://wordpress.org/plugins/wp-consent-api/) is a standard way for WordPress plugins to learn the visitor's consent. Site Kit by Google and many other plugins read it.

## What Okito does

When the WP Consent API plugin is active, Okito:

* sets the consent type: `optin` for opt-in visitors, `optout` for the US opt-out model and for regions where consent is not required,
* passes each choice with `wp_set_consent`:

| WP Consent API category | Okito category |
| --- | --- |
| functional | Always allowed |
| preferences | Functional |
| statistics, statistics-anonymous | Analytics |
| marketing | Advertisement |

Okito waits for the WP Consent API to load if it arrives later than the Okito script (for example when a caching plugin delays it).

## Set it up

1. Install and activate the **WP Consent API** plugin.
2. In **Site Kit → Settings → Admin Settings**, turn on **Consent Mode**.
3. The Okito plugin's Site Health checks confirm both are on.

The Okito WordPress plugin keeps the WP Consent API and Site Kit's consent script out of WP Rocket's "Delay JavaScript", so Site Kit gets the choice right away. See [WordPress](../installation/wordpress.md).
