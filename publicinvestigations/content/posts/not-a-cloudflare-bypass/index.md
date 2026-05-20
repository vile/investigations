---
title: "No, your phishing kit does not have a Cloudflare bypass"
date: 2026-04-13T16:05:35-04:00
slug: 2026-04-13-not-a-cloudflare-bypass
type: posts
draft: false
categories:
  - default
  - security
tags:
  - default
  - web
  - phishing
summary: Through my daily work and from reading quite a few blog posts, researchers consistently mistake that a phishing kit is leveraging /cdn-cgi/phish-bypass to hinder web and security scanners. This stems from a misunderstanding of what the Cloudflare /cdn-cgi/ endpoint is and how it operates.
---

<!-- markdownlint-disable no-inline-html -->

Through my daily work and from reading quite a few blog posts, researchers consistently mistake that a phishing kit is leveraging `/cdn-cgi/phish-bypass` to hinder web and security scanners.
This stems from a misunderstanding of what the Cloudflare /cdn-cgi/ endpoint is and how it operates.

## What is the /cdn-cgi/ endpoint?

When a site uses Cloudflare as a reverse proxy and DNS provider, the `/cdn-cgi/` endpoint is automatically added and hosted on the domain by Cloudflare.
This path is exclusively managed and served directly by Cloudflare and "[i]t cannot be modified or customized." [[1](https://developers.cloudflare.com/fundamentals/reference/cdn-cgi-endpoint/)]

This endpoint is the base for the majority of Cloudflare products, such as challenge (turnstile), image optimization, web analytics, email obfuscation, etc.
This endpoint is also used for `phish-bypass`.

## Cloudflare Phishing Warning

Similar to Google Safe Browsing or Microsoft SmartScreen for Edge, Cloudflare maintains a curated list of phishing domains that leverage Cloudflare infrastructure.
These sites display a prominent warning before entering stating that the content is potentially malicious.
Passing this warning requires a manual acknowledgement.

{{< rawhtml >}}

<img src="https://global.discourse-cdn.com/cloudflare/original/3X/6/f/6f3592a6d02734f0ace78cff0490d0da0bd623c5.png" alt="Screenshot of Cloudflare phishing warning screen"/>

{{< /rawhtml >}}

## Technical Details of the Cloudflare Phishing Warning

Under the hood, there are quite a few steps that must succeed before a manual acknowledgement is accepted for the phishing warning.
First, a turnstile challenge must be completed, either in the background or via manual "click" challenge.
Once this challenge is completed and the "Ignore & Proceed" button is pressed, a `GET` request is sent to `domain.com/cdn-cgi/phish-bypass` which includes an `atok` (a CSRF-like token) and the turnstile challenge response.
If the challenge response is accepted, this endpoint then returns an HTTP 301 response including two critical components: `Location` and `Set-cookie` for an HTTP cookie `__cf_mw_byp` (assumed to mean "Cloudflare Malware Bypass").
The `Location` redirects to the originally requested content (in case the phishing warning modified the URL path) and the `__cf_mw_byp` cookie allows for continuous browsing of the site without having to re-acknowledge the phishing warning.

It is extremely common for security scanners to get stuck on the "turnstile token missing" error because it is easy to grab the `atok` token, but is difficult to solve the turnstile challenge (see [URLScan for example](https://urlscan.io/search/#page.url%3A%22cdn-cgi%2Fphish-bypass%22)).
Both components are required to successfully view content behind the warning page.

This behavior also confuses human researchers.
An [article from Palo Alto's Unit42](https://unit42.paloaltonetworks.com/iranian-cyberattacks-2026/) ([archive](https://archive.ph/8aVHf)) incorrectly states that "...attackers [are] using the cdn-cgi/phish-bypass... to exploit and circumvent security challenges."
While it technically does defeat security scanners who are not able to complete the turnstile challenge, the site is already marked as phishing for every visitor.