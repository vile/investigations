---
title: "How to Actually Secure Your X Account"
date: 2024-10-20T21:45:39-04:00
slug: 2024-10-20-how-to-actually-secure-your-x-account
type: posts
draft: false
categories:
  - default
  - security
tags:
  - default
  - socialmedia
summary: "There has been a large increase in X account compromises over the past few months. As such, I wanted to compile a list of security policies and tips as well as common phishing tactics."

# Twitter Card
description: There has been a large increase in X account compromises over the past few months. As such, I wanted to compile a list of security policies and tips as well as common phishing tactics.
images: ["posts/2024-10-20-how-to-actually-secure-your-x-account/images/cover.png"]
---

{{< rawhtml >}}
</br>
<img
  src="./images/cover.png"
  alt="Header image saying 'How to Actually Secure Your X Account'"
></img>
{{< /rawhtml >}}

---

There has been a large increase in X account compromises over the past few months. As such, I wanted to compile a list of security policies and tips as well as common phishing tactics.

## Secure Password

This is your first line of defense for your account. Passwords should be long (greater than 16 characters at a minimum), consist of a variety of character types, and be random or pseudorandom. If you find it difficult to memorize a 30 character password, use a known and secure password manager (for all of your accounts, really). Popular managers include [1Password](https://1password.com/), [Bitwarden](https://bitwarden.com/), and [KeePassXC](https://keepassxc.org/). These products, and the companies behind them, are not immune to security incidents themselves, such as in the case of [LastPass](https://www.cybersecuritydive.com/news/lastpass-cyberattack-timeline/643958/); DYOR.

In addition to this, you should be rotating (changing) your password at least somewhat frequently. Between 30 and 45 days is usually recommended.

While it is relatively uncommon now for unauthorized parties to simply log into accounts as their main attack vector, it's still a possibility if an account has literally zero other security features.

## Turn on 2FA

There is no scenario where 2FA should not be enabled. Furthermore you should be using a physical, hardware 2FA key (such as a [Yubico YubiKey](https://www.yubico.com/products/)) in almost every scenario. Hardware keys are compatible with the vast majority of devices supporting various physical (USB-C, Lightning, etc.), nearfield connection (NFC) types, or a combination of these.

You should:

- ALWAYS have at least two (2) hardware keys associated with your account (most platforms allow a large number of keys to be registered on your account, including X).
- ALWAYS ensure the physical security of your hardware key (always know where its located, lock it in a safe when not in use, do not travel with it unless absolutely necessary, etc.).
- ONLY purchase hardware keys from the manufacturer's official site; do not use third party retailers or second-hard marketplaces for used devices.

Company and project accounts SHOULD NOT be directly logged into (and most cases can't be if hardware keys are used), credentials and 2FA method(s) should be controlled by a single, knowledgeable, and trustworthy person that employs all security best practices. If access is needed by other users (e.g., social media managers, marketing team), use the delegation feature which is touched on more further down. All accounts with delegation access MUST employ the same set of security practices.

## Obfuscate Email

While security by obscurity is not the optimal way to secure something, it does have its use cases. Many guides and people will say to use the "dot trick" or "plus trick" with your email, I highly advise against this as: 1) not all email providers support this (you should be sending emails to a completely different address you don't control), 2) your main email is still guessable or may already be exposed. You can check if your email(s) are associated with data breaches by using sites like [HIBP](https://haveibeenpwned.com/) or [Pentester](https://pentester.com/).

You should also avoid the user of corporate or custom email domains. While it may seem logical to use twitter@myproject\[.]com or me@personalwebsite\[.]com, again, these are guessable (with enough time and effort) or may already be exposed. Assume all data associated with your accounts will be exposed at any point, whether through data breach, exploit, or other malicious tactics such as [fraudulent EDRs](https://krebsonsecurity.com/2022/03/hackers-gaining-power-of-subpoena-via-fake-emergency-data-requests/) or corrupt/compromised employees. Such as in the case of the [2021 Twitter API exploit](https://hackerone.com/reports/1439026) where [200 million emails and phone numbers were leaked](https://www.bleepingcomputer.com/news/security/200-million-twitter-users-email-addresses-allegedly-leaked-online/) with their corresponding Twitter information, such as usernames and public account IDs

One of two strategies should be used:

1. A brand new, random email address should be created with a common email provider (gmail, proton, yahoo, riseup, etc.). The account should be locked down and secure just like any other social media account. However, the downside of this is that you have to manage a completely new email inbox; while many email providers allow users to forward all incoming mail to a different address, this can still be cumbersome.
2. Use an email aliasing service. This allows you to generate an "alias" that forwards all incoming mail to a predetermined address automatically, effectively cutting out the middleman (but not really since you're just relying on a completely different service now). The benefit of aliasing is that they're infinitely rotatable and significantly easier to setup and manage. Many aliasing providers exist, both paid and free. Some include [SimpleLogin](https://simplelogin.io/) (owned by and integrated with Proton), [Addy](https://addy.io/), and [Apple iCloud](https://support.apple.com/guide/icloud/add-and-manage-email-aliases-mm6b1a490a/icloud).

Another consideration with custom email domains is in the case that they fall out of registration (say the project is abandoned or shutdown), the domain can be re-registered by an attacker who can then receive all emails associated with that domain.

## Phone Numbers

If you take away any piece of information, it should be that **you should never have a phone number associated with your account**.

The only scenario where you MUST associate a phone number with your X account is when you are initially signing up for premium (the blue checkmark). However, you can immediately remove the number after you have completed your payment. Even then, try to use a phone number that is not your real phone number, consider using a VOIP number (such as Google Voice) or whatever low cost/pay-as-you-go carrier is the most accessible in your area.

Leaving a phone number associated on the account opens you up to SIM swaps or social engineering of X support, or yourself, as your phone number can lead to LOTS of personal information (the country code, area code, and prefix of your number heavily narrow down your location; think of accounts that primarily use a phone number to sign up such as WhatsApp, Telegram, or Venmo; your caller ID may reveal your full name, be associated with data breaches, or be part of "people" sites like WhitePages or ThatsThem).

## Account Security Settings

### Additional Password Protection

This setting requires that you (or someone attempting to break into your account) provide the currently registered email address to reset your password. This goes back to having a random, non-guessable email associated with your account. This should ALWAYS be turned on.

### Connected Apps

Every app you've ever logged into using X will be listed here if you've never revoked them. Connected apps can have **dangerous permissions** such as having the ability to post on your behalf automatically or read your DMs. Only TRUSTED and ESSENTIAL apps should be actively connected, such as post management integrations (e.g., Typefully). Static (read-only) connections should be revoked ASAP (e.g., Discord or airdrop claims). Apps will be touched on more in the phishing techniques section.

You should be frequently checking what apps have access to your account and revoking anything that you do not actively use.

### Sessions & Logged-in Devices and Apps

Both of these sections touch on roughly the same thing, sessions show all active sessions (which can be multiple per device), whereas devices show individual devices. Immediately revoke any sessions or devices you are not using or you do not recognize.

You should also be frequently checking active sessions and devices and revoking them, especially if you have lost or replaced a device recently.

### Delegation

What exactly is [delegation](https://help.x.com/en/managing-your-account/how-to-use-the-delegate-feature)? It's a feature that allows others to act on your behalf, such as posting, sending DMs, or viewing certain analytics, without actually being logged into the account.

Whether you use delegation or not, "Allow others to invite you to their account" should ALWAYS be turned off UNLESS you are actively intending to be invited to another account. Turning this setting off does not remove your account from accounts you have already been delegated access to. While this doesn't exactly protect you from anything per se, this is just good practice. In addition to this, check the "Members you've delegated." If you are on a personal account, there likely should be ZERO delegations listed. If you are on a company or project account, ensure each delegated individual is recognized and known, if there are any unusual or unknown delegations, revoke them immediately.

If you are actively managing a company or project account, consider having an X account solely for delegation access separate from your personal account(s).

### Discoverability and Contacts

I highly recommend turning off discoverability by email address and phone number, as well as removing all contacts. It makes it slightly more difficult for an attacking party to confirm whether or not they have a real associated email or phone number.

### Data Sharing and Personalization

This is up to you whether or not you are fine with X and advertisers having and using your data (interests, activity patterns, location history, etc.). If you do not want this information shared, turn off all the settings here.

## Phishing Techniques

Outside of SIM swaps, spear phishing and social engineering make up the vast majority of modern attacks on X accounts. There are three categories that attacks will, generally, fall into: direct credential phishing, session hijacking, OAuth/external app abuse. Within these categories, attacks have an unlimited number of variations and unique scenarios.

**Direct credential phishing** is the most straight forward. For example, you may receive an email to the address associated with your X account stating a new login attempt has been made from a foreign country. The email may include a button that says "Not you? Reset your password now." Clicking the button leads you to an exact clone of the X site asking you for your old password along with a new password, except its on x\[.]com\[.]reset-pass\[.]org. You've just given up your password (and potentially more information or metadata, like your IP address) to the phishers. If you don't use 2FA or have a weak 2FA method, such as SMS, you're now compromised. Such is the case of [Linus Tech Tips X account compromise](https://www.dexerto.com/tech/linus-tech-tips-reveals-how-scammers-took-control-of-x-twitter-account-2867428/).

**Session hijacking** takes a little bit more setup and has a larger technical component. For context, [your browser stores cookies and other information](https://www.cloudflare.com/learning/privacy/what-are-cookies/) that is largely abstracted away the end user. This allows you to freely browse and post on X without having to constantly re-login with your email and password (and hopefully 2FA). The goal of session hijacking is to steal the cookies and information stored inside your browser so an attacker can "log in" as you without needing your email and password. There are many ways to do this, but primarily through an end user unknowingly revealing this information. Examples of this are [malicious bookmarklets](https://krebsonsecurity.com/2023/05/discord-admins-hacked-by-malicious-bookmarks/), leaking information when sharing your screen, or info stealing malware. There are too many variations of this type of attack to go into depth, but largely, you should not be opening or doing ANYTHING that you do not fully understand. Common setups include [assisting a "developer" to debug a site](https://medium.com/@0xFantasy/xss-attack-in-popular-nft-project-website-steals-discord-tokens-and-hacks-nft-discord-servers-3da9c89d4afa) that integrates with X, a "VC" asking you to open and sign an agreement in the form of, what appears to be, a PDF, or [a "journalist" asks you to submit a form on their site](https://x.com/Jon_HQ/status/1684251223472615425) which requires you to prove you are not a robot by dragging something to your bookmarks.

**OAuth and external app abuse** are relatively new for X phishing. Specifically, OAuth abuse is the easiest method to fall for. Whenever the phishing setup directs you to X, you are on the real X domain, already logged in, and one click away from granting permission to an attacker to post tweets and read/send DMs on your behalf. The usual setup for this type of phishing is some sort of video conference (such as Zoom or Google Meet) or calendar scheduling (such as Calendly). Either before or during an attempt to join a meeting or book a calendar slot, you will be prompted to authorize an app on your X account account, usually impersonating whatever service you were just previously visiting, to either verify, provide contact information, etc. This seems like a very logical thing to do, especially if you're also contacted on X through DMs. After you have authorized this app, the attacker can now interact with your account in various ways, such as posting drainer links or reading your DMs. To stop such an attack, go to your account's authorized apps and revoke access to EVERYTHING as it may not be immediately clear which app is malicious. Later, you can reauthorize legitimate apps that you need to use.

A common tactic used with all of the above phishing methods is embed spoofing. Whenever you see a link on X with a "card" below it, usually an image with a title and some sub-text, that is generated by X automatically visiting that site and gathering metadata. However, these can be manipulated and [spoofed to show what is seemingly a legitimate site](https://www.bleepingcomputer.com/news/security/twitter-can-be-tricked-into-showing-misleading-embedded-links/), but actually lead to a phishing link. The only way to combat this is to use a link un-shortener; X still uses the t.co short link, you can use a service like [unshorten.it](https://unshorten.it/) to see where the short link actually leads before visiting it.

## Conclusion

We've covered the most essential knowledge for securing your X account, both things you should and shouldn't do. In the event that a compromise does that, that's a whole other can of worms.
