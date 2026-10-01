---
description: One choice for your site and its subdomains, so the banner is not shown again on each one.
---

# Share consent across subdomains

With **Share consent across subdomains** on (Banner Builder → General → Other settings), a choice a visitor makes on your site's domain or one of its subdomains applies on all of them. A visitor who accepts on `www.example.com` doesn't see the banner again on `shop.example.com` or `blog.example.com`.

* Your site's domain is the one set for the website in the dashboard (for example `example.com`). If it is set as `www.example.com`, Okito uses `example.com`. Pages on that domain and on its subdomains share the choice; other domains don't.
* Every subdomain must load this website's Okito script (the same website key).
* The choice is also kept in a cookie on your domain (`okito_shared_consent_…`, 13 months). Each subdomain keeps its own stored choice too; when a newer choice was made on another subdomain, it applies here before the banner decides.
* The newest choice wins: if the visitor changes their mind on one subdomain, the others follow on their next page view.
* It works with the GDPR/KVKK banner and the US State Laws notice. Under the US notice, [Global Privacy Control](../compliance/us-state-laws.md) still applies on every subdomain: a shared choice never overrides it. With [IAB TCF](../compliance/iab-tcf.md) on, choices stay on each subdomain: a TCF choice does not fit in a shared cookie.

Choices made before you turn the setting on stay on the subdomain where they were made until the visitor chooses again.
