---
title: "Google: You Get an Open Redirect! You Get an Open Redirect!"
date: 2026-05-28T19:34:33-04:00
slug: 2026-05-28-google-redirects
type: posts
draft: false
categories:
  - default
  - security
tags:
  - default
  - web
  - appsec
  - phishing
summary: Google has a multitude of open redirects that are frequently abused by threat actors. They are used to both deter initial URL scanning and obfuscate the final phishing URL. A recent example of this in the wild found by KnowBe4 showcased combining multiple redirects in a row. Google seemingly has no interest in fixing these issues according to their VRP. These redirects span different Google domains and products including Search, Meet and Ads (formerly DoubleClick).
---

<!-- markdownlint-disable no-inline-html -->

While not the most exhilarating topic, looking into Google's open redirects was a fun evening.

## TLDR

Google has a multitude of open redirects that are frequently abused by threat actors.
They are used to both deter initial URL scanning and obfuscate the final phishing URL.
A recent example of this in the wild found by KnowBe4 [showcased combining multiple redirects in a row](https://x.com/Kb4Threatlabs/status/2059277859148206363).
Google seemingly has no interest in fixing these issues according to [their VRP](https://bughunters.google.com/learn/invalid-reports/web-platform/navigation/open-redirectors).
These redirects span different Google domains and products including Search, Meet and Ads (formerly DoubleClick).

## What is an Open Redirect?

Simply put an "open redirect is an attack that occurs when a web application redirects users to a URL supplied via an unvalidated parameter" ([OWASP](https://owasp.org/www-community/attacks/open_redirect)).

## Classic Redirect in Google Search

Two extremely well-known redirects for the base `google.com` domain are `/url?q=` and `/amp/s/` (also just `/amp/`).
The former accepts a protocol-prefixed URL (e.g., `https://blog.fa.nta.sy`) while the latter accepts a bare locator (e.g., `blog.fa.nta.sy`).
This distinction is interesting since the `amp` path uses the `/url?q=` redirector underneath.
Both redirects preserve target URL paths and query parameters, but not fragments.

It is important to note that the *majority* of the time, a pop-up warning about the redirect shows the final target URL (even resolving through multiple layers of normal Google redirects; [example](https://google.com/url?q=https://google.com/url?q=https://google.com/url?q=https://google.com/url?q=https://example.com)).
This may be helpful or hurtful for a phishing campaign depending on the use case.
For example, requiring a manual acknowledgement will stop simple web scanners, but may make users slightly wary of the destination.

It is also interesting to note that the only other protocol allowed in `/url?q=` is `ftp`.
All other protocol prefixes (including `ssh`, `ldap`, `smb`, `chrome`, `ms-appx`, etc.) all return a redirect warning stating "invalid url."
Not even `sftp://` works.
The only exception is the `tel:` URI for phone numbers which embeds, in plain text, the actual phone number provided in addition to the "invalid url" warning ([example](https://www.google.com/url?q=tel:1(555)-555-5555)).

## Google Meet Redirect

The new kid on the block is using Google Meet's `/linkredirect?dest=`.
This redirect also ends up using `/url?q=` under the hood, but potentially has larger social engineering implications if
someone blindly trusts the `meet.google.com` domain without paying attention to the remainder of the URL.
This redirect also supports full URL encoding, compared to `/amp/`, allowing for minor obfuscation of the target URL.

## Surfing on Google Ads

Google Ads (previously DoubleClick) maintains significant infrastructure for URL redirection (kind of the whole point of ad tracking URLs).
While many domains and endpoints seem to have protections against blindly changing the ad target URL, some very much don't.

### DoubleClick Domain with No Checks

The only domain and path found during my testing that blindly accepts any URL with no authentication was `adclick.g.doubleclick.net/pcs/click?adurl=`
and its slightly shorter domain cousin `ad.doubleclick.net`.
Simply appending a protocol-prefixed URL after `adurl` results in a bare HTTP 302 redirect.
No URL encoding is supported for this redirect.

The downside of using DoubleClick domains is that they are frequently part of ad blocker blocklists (both client- and network-based), meaning that they may not
work in certain environments.

### Paid Ad Surfing

Three major domain and path combinations were identified that support piggybacking off existing **live** ads.
These include `ad.doubleclick.net/ddm/clk/`, `ad.doubleclick.net/ddm/trackclk/...?`, and `googleads.g.doubleclick.net/dbm/clk?...&adurl=`.

The `/ddm/clk/` and `clk?...&adurl=` ad paths are fairly common with modern Google Ads (site banners, etc.) and allow for simple hijacking.
However, only **live** ads can be hijacked; once an ad becomes inactive, the URL returns an HTTP 404.
This, too, can be helpful or hurtful: if an ad expires before a novice analyst views it, they may think the phishing URL is down, instead of the ad link that is being piggybacked on.

The `/ddm/clk/` path, however, is unique in that almost any regional Google domain under the `adservice` subdomain (e.g., adservice.google.info, adservice.google.co.kr, adservice.google.fr, etc.) can be substituted.
This can allow for a unique trust-building technique for phishing campaigns that may be targeting a specific country by using their native Google domain instead of a DoubleClick domain.

The `/ddm/clk/` path does not support URL encoding, but `clk?...&adurl=` does.

The `ddm/trackclk/...?` path is also unique as it is primarily used for long-lasting ad campaigns compared to the short-lived `/ddm/clk/` ad URLs.
These URLs are some of the simplest to hijack, simply by removing any existing query parameters and appending the target URL (e.g., [ad.doubleclick.net/ddm/trackclk/.../...?https://blog.fa.nta.sy](http://ad.doubleclick.net/ddm/trackclk/N1153793.2061500TWITTER-OFFICIAL/B35446380.442289925;dc_trk_aid=635650078;dc_trk_cid=252361683?https%3A%2F%2Fblog%2Efa%2Enta%2Esy)).
In addition, this type of ad URL dynamically appends the original ad campaign ID to the target location, meaning that it can be used to check if a visitor actually came from the ad URL instead of directly visiting the site.
However, no alternative domains seem to be supported and URL encoding is not supported.
