---
description: Test a second banner design against your current one and keep the one more visitors answer.
---

# A/B testing the banner design

**A/B testing** (Professional plan) shows your current banner (**A**, the control) to part of your visitors and a second design (**B**, the variant) to the rest, then tells you whether B changes how many visitors make a choice. Open it with **A/B test** next to **Create new banner** in Banner Builder.

{% hint style="info" %}
A/B testing is being rolled out gradually. If the page says it is not available yet, it will be soon.
{% endhint %}

## What can differ

Only the design:

* the **position** (unless your banner uses a design theme other than Classic, which sets the layout itself),
* the **colours**: banner, buttons and preference window.

Everything else is your current banner's, for both versions: texts and button labels, links, the design theme, the close button, logo and custom CSS, languages, categories, IAB TCF and Google settings. Both versions show the same notice, so a choice made on either is equally valid.

Okito won't start a test whose variant makes **Reject all** harder to see than **Accept all** (the same check as Banner Builder's colour warnings).

## Who sees which version

* The version is drawn at random on **every page load**, by the share you set (10–50% for B). Nothing is stored on the visitor's device for it, so no cookie or storage is added. A visitor may see A on one page and B on another.
* Visitors who have already made a choice don't see the banner, so they are not part of the test.
* The test runs only with the standard embed (`/js/YOUR-KEY`, as on the install page and in the WordPress plugin). An embed that sets the language in the script URL (`?lang=`) always gets A.
* Version 1 works with the **GDPR** consent template (with or without IAB TCF). It isn't available with the US State Laws or GDPR + US templates, or on Shopify stores.

## What is measured

The test compares the **decision rate**: the share of banner views that ended in a choice: accept all, reject all or a custom choice. A banner that more visitors answer is the better banner. Okito never declares a winner by acceptance alone; the results always show the accept-all and reject-all rates side by side.

When you create the test you pick the smallest difference worth finding (3, 5 or 10 percentage points). Okito works out how many banner views each version needs from your site's traffic of the last 28 days and shows how long the test will take. A test that would need more than 60 days can't start: try a larger difference or a larger share for B.

## Results

Results stay hidden while the test runs: looking at numbers before the end and stopping at a lucky moment is the most common way to pick a false winner. While it runs you see the number of views per version and how many days have passed.

The test ends on its own once at least **14 days** have passed and both versions have enough views. You then see:

* the verdict: **B is better**, **B is worse**, **no meaningful difference** or **inconclusive**,
* the decision rate of each version, and the difference with its 95% confidence interval,
* accept all, reject all and custom choices per banner view, side by side.

If a test doesn't collect enough views in **60 days**, it ends as **inconclusive**. If the views are split far from the share you set, the verdict is **data problem** and no winner is chosen.

When the test has ended, choose **Apply variant** (B's position and colours become your banner's) or **Keep control**.

## While a test runs

* Your banner can't be edited, deactivated or replaced. **Stop and edit** ends the test without a verdict.
* If the website's plan no longer includes A/B testing, the test pauses and everyone sees A. You can resume it within the 60 days if the plan comes back.
* One test at a time per website.

## Privacy

* Choosing the version uses no cookie or device storage.
* Okito records which version a banner view showed, together with the view (as for every banner view: the visitor ID, the page, the browser and the masked IP address) and, without any identifier, whether that view ended in a choice. This is processing of personal data on your behalf as the controller, usually under your legitimate interest (GDPR Art. 6(1)(f), KVKK Art. 5(2)(f)). Mention it in your privacy notice.
* Those records are deleted 30 days after the test ends; the test's results stay in your dashboard.
* Consent records note the version the visitor answered (banner and revision), as part of the proof of what they were shown.
