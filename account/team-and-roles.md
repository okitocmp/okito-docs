---
description: Invite colleagues and choose what each can do.
---

# Team and roles

Invite colleagues from **Team** in the dashboard. They get an email invitation and join your account.

| Role | Access |
| --- | --- |
| **Owner** | Full access, including billing, subscription plans, team, API keys, the cross-device signing key and audit logs. |
| **Admin** | Full access, including team, API keys, the cross-device signing key and audit logs. Billing and subscription plans are those of the Admin's own account. |
| **Editor** | Banner Builder, Cookie Manager, cookie scans and categories, the banner and website settings, **Ask every visitor again**, **Verify** and emailing the installation to a colleague, Script Blocking, scheduled scans, A/B tests, legal bases, privacy settings, consent record downloads (CSV) and privacy requests, adding websites to the team under **Add to** (billed to their own account), plus everything a viewer sees. |
| **Viewer** | Dashboard, websites, analytics, compliance pages and consent records, read only. Viewers see Banner Builder and Cookie Manager read only. Viewers cannot download consent records and do not see privacy requests. |

Plans are per website. The dashboard shows everyone on the team the selected website's own plan, not their own account's, and the same goes for the people an agency invites to a client workspace.

## Which websites each person sees

* Everyone on the team sees the websites of the account that invited them, with the role they were given.
* A member who has an Okito account of their own chooses where a new website goes under **Add to** when they add it: **My account** (the default) or a team where they are an Editor or Admin. Everyone on that team then sees the website with their own role. Websites they add to their own account stay there, and the team does not see them. **Add to** appears only for someone with an account of their own who is an Editor or Admin on at least one other team; client workspaces are never offered (see [Agency partners](agency.md#who-sees-which-client-website)).
* A website added to a team still belongs to the person who added it, and so does its bill: its plan is paid from their account, and on Free it uses their account's one Free website. The team's websites do not share a plan.
* Someone who joined only through an invitation signs in with their own login but has no workspace of their own. A website they add while your team is the only team they are on is shared with your team: everyone on the team sees it with their own role, also after they leave. Like any website, it stays owned by the person who added it (see below).
* Their other websites, added while they were on more than one team or before Okito started recording which team a website belongs to, are seen by every team they are on. Client workspaces do not see them; see [Agency partners](agency.md#who-sees-which-client-website).
* If you belong to more than one team or client workspace, the website list shows the websites of each, and your role on a website is the role that workspace gave you.
* The person who added a website remains its owner, including someone who joined only through an invitation. Renaming it, changing its domain, turning it off, deleting it and changing its plan or billing are done by that person, whatever your role, also after they leave the team. If that person can no longer do it, contact [support](../help/support.md).
* Banner Builder and Cookie Manager open for everyone who sees a website, including through a team or client workspace. Owners, Admins and Editors change the banner, cookies and cookie categories, run cookie scans and save the website's banner settings. Viewers see the same pages read only.
* On **Install banner**, everyone who sees a website can copy its installation code, website key and snippets. Owners, Admins and Editors also set up the banner, click **Verify** and email the installation to a colleague. Viewers copy only.
* The cross-device signing key in Banner Builder is shown only to the person who added the website and to the team's Owner and Admins, who can also replace it.
* The policy generator is not tied to a role: anyone on the team can use it, within the plan and monthly limit shown on its page.
* Viewers cannot change the banner, cookies, cookie categories or services, IAB TCF vendors and publisher restrictions, Script Blocking rules, scheduled scans, A/B tests, legal bases or privacy settings. They cannot run cookie scans, ask every visitor again or download consent records. Owners, Admins and Editors can.

## Audit logs

**Audit logs** (Owner and Admin) record who changed what in the account.

When someone leaves, remove them from the team and rotate any API keys they could have copied. If they were an Admin, also click **New key** for the [cross-device signing key](../developers/cross-device-consent.md) of each website that uses it. Websites that belong to the team stay with it, and the person who added them remains their owner. Their other websites are no longer shown to the team.
