---
description: What visitors see, and whether measurement starts, outside the regions that need prior consent.
---

# Where consent is not required

Okito asks for consent first in the regions whose laws expect it: the EEA, the UK, Switzerland, Türkiye, Brazil, Canada, South Africa, Australia, Saudi Arabia, Argentina, Andorra, the Faroe Islands, South Korea, China, India and, with the GDPR template, the US. For all other visitors (for example in Japan), choose the behaviour in Banner Builder → General → **Where consent is not required (e.g. Japan)**:

| Option | Banner | Google consent mode for these visitors |
| --- | --- | --- |
| **Show the banner, keep measurement on** (default) | Shown | Starts **granted**; the visitor can still reject. |
| **No banner, keep measurement on** | Not shown | **Granted**. Beginner plan and higher. |
| **Show the banner, measurement off until a choice** | Shown | Starts **denied** until the visitor chooses. |

Global Privacy Control always wins: a visitor whose browser sends GPC starts denied, and scripts that need consent stay blocked until the visitor accepts them.

## Why "keep measurement on" is the default

If you turn on Google's **Data Transmission Controls** or **Global Consent Defaults** for every country, Google applies them to all visitors. Okito's granted default for visitors outside the opt-in regions keeps measurement working where no banner is needed, while visitors in opt-in regions still start denied.

{% hint style="info" %}
After changing this setting, copy the Consent Mode snippet from **Install banner** again (or update the GTM template setting), because the snippet contains the default.
{% endhint %}
