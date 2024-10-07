---
title: "River Poker Casino Investigation"
date: 2024-09-18T15:25:11-04:00
slug: 2024-09-18-river-poker-casino-investigation
type: posts
draft: false
categories:
  - default
  - investigation
tags:
  - default
  - osint
  - crypto
  - gambling
  - vasp
summary: This is one of two articles based on \"prompted\" investigations. Starting out with an initial question and/or piece of media, the investigation is still open ended.
---

{{< rawhtml >}}
</br>
<a href="https://metasleuth.io/" target="_blank">
<img
  src="./images/blocksec-metasleuth.png"
  alt="Blocksec Metasleuth logo"
  width=400
></img>
</a>
{{< /rawhtml >}}

> ### Thank you [Blocksec](https://x.com/BlockSecTeam) for allowing me access to their [Metasleuth](https://x.com/MetaSleuth) platform to conduct the on-chain portion of this report. Look into using [Metasleuth](https://metasleuth.io/) for your next investigation

## Preface

This is the second of two articles based on “prompted” investigations. Starting out with an initial question and/or piece of media, the investigation is still open ended.

Initial Prompt:

“Tehran Tokyo” by Sasy was published in 2021. An ad placement for an online casino is found in [this music video](https://www.youtube.com/watch?v=NNtMb0DrBRA). To the best of your effort, answer the following questions:

1. What other domain URLs does the casino operate (operated) from?
2. Do they have any official social media presence / instant message  support? If yes, what are their handles/phone numbers?
3. Produce a list of USDT-TRC20 deposit addresses of the casino.

## Domain Investigation

In [the music video](https://www.youtube.com/watch?v=NNtMb0DrBRA) for "Tehran Tokyo" by Sasy, an advertisement is present for "River Poker" along with a link "www\[\.]RiverPoker\[\.]info." When visiting the site, we can quickly see there is [a linked Instagram account](https://www.instagram.com/river_poker/) at the bottom of the page. The Instagram page is very active, garnering over 22,000 followers and having over 2,000 posts as well as multiple "story" posts per day. Along with this, a different domain is present in the bio of the account, "www[\.]riverpoker\[\.]com"

Both sites contain the same content, visually, link to the same social media profile, and link to the same download URLs.

![[River Poker Site Visual Comparison.png]](./images/River%20Poker%20Site%20Visual%20Comparison.png)

Looking into both the source of the sites as well as DNS and WHOIS data, we can further increase our confidence these domains belong to the same entity. Both domains' currently are registered with GoDaddy, use WHOIS privacy services, and use Cloudflare name servers (NS).

DNS-wise, both domains have American "A" record IPs that are owned by Cloudflare (ASN: AS13335), and use Google-based mail servers (MX). It is to note that the "com" domain contains slightly more DNS records include: an additional "A" record (belonging to Cloudflare), and two "TXT" records (Google verifications). The "info" domain contains two extra "MX" records (main\[.]riverpoker\[.]info; they likely attempted to run their own mail server at one point; and a Google verification MX URL).

![[River Poker WHOIS Comparison.png]](./images/River%20Poker%20WHOIS%20Comparison.png)

![[River Poker DNS Comparison.png]](./images/River%20Poker%20DNS%20Comparison.png)

Looking into SSL certificates yields no results, as the "info" and "com" issuing organizations are different, Cloudflare and Google Trust Services (GTS) respectively. However, [Cloudflare does use GTS](https://developers.cloudflare.com/ssl/reference/certificate-authorities/) as a certificate authority as part of their universal SSL feature.

While not definitive proof, both sites also use the same Google Tag Manager ID.

![[River Poker GTag Comparison.jpg]](./images/River%20Poker%20GTag%20Comparison.jpg)

### Other Domains In Use

Going forward, the "com" domain (site) will be the main pivot point. On the site, there are various links for application downloads (Android, iOS, Windows) that all utilize different domains, an "affiliate" page, and an "iTech Labs RNG Certification."

The download links are as follows:

- Android: hxxps://www\[.]riverpoker\[.]com/download/mobile/pokermobile.apk
- Windows: hxxps://www\[.]rghvir45\[.]com/download/setup.exe
- iOS: itms-services\[\:]//www\[.]rivappsdo\[.]com?action=download-manifest&url=hxxps://www\[.]rivappsdo\[.]com/download/mobile/ios/manifest.plist

This introduces two new domains, both registered, again, with GoDaddy on the same day (May 31st, 2023); except the NS for these domains are likely registrar defaults (both using
ns05.domaincontrol.com and ns06.domaincontrol.com). Both domains seem to solely be serving downloads from the same server running Red Hat Linux with nginx hosted using Amazon AWS in India.

![[River Download DNS.png]](./images/River%20Download%20DNS.png)

![[Maltego Graph 2.jpg]](./images/Maltego%20Graph%202.jpg)

It is to note that the "com" domain is a resold domain. The original registration date is August 24th, 2000 (over 24 years ago). On or about November 30th, 2022, the domain was transferred to GoDaddy from Namecheap and had its NS changed from Sedo Parking to Cloudflare. This sale is further confirmed by [this article from DNW](https://domainnamewire.com/2022/11/29/turkey-week-end-user-domain-name-sales/) talking about sales on the Sedo marketplace that took place that week. An [archive](https://web.archive.org/web/20211223025335/http://riverpoker.com/) of the "com" site in December 2021 shows a Sedo landing page saying the site is for sale for the price of EUR$3,000.

Looking further into domains linked in the footer of the site, the affiliate buttons lead to the www\[.]chariv37\[.]com (the "Agent Backoffice \[sic]") that is registered with GoDaddy and on the same Cloudflare NS as the main River Poker site. Among the many contact emails listed on the Agent site, they all share the same email domain www\[.]rnying32\[.]com. This domain currently is not registered, but, using historical WHOIS data, it was active between 2022 and 2023, registered using GoDaddy, and used Cloudflare NS.

![[Maltego Graph 3.jpg]](./images/Maltego%20Graph%203.jpg)

### Looking into Archives

Using archive.org to look into archives of both the "info" and "com" domains, many other domains that were used for downloads stand out:

- rtonpas56.com
- rivdx1.com (Expired, offline)
- riverpn37.com (Expired, offline)
- rghvir45.com

All of the above domains currently are, or previously were, registered with GoDaddy.

### iTech Labs Document

Earlier, it was noted that River Poker displays a certification from "iTech Labs" regarding their provably fair randomness. However, the current document only certifies "CZAR GAMING PRIVATE LIMITED" and their URL "czargaming.com." *Czar Gaming* seems to only be a partial games provider to River Poker (such as live games that require a dealer).

Simply Googling for `itech labs "river poker"` returns a [very similar certification](https://itechlabs.com/certificates/CzarGaming/RNG_Certificate_CzarGaming_RiverPriver_UK_19Nov2018.pdf) document ([archive](https://archive.ph/emGAR)); once again certifying *Czar Gaming*, but this time River Poker as the "operator" with a different domain hxxp://www.riverpriver.com. This site is currently offline and has fallen out of registration, but archives of it do exist.

![[iTech RiverPriver Certificate.jpg]](./images/iTech%20RiverPriver%20Certificate.jpg)

In [one of the archives](https://web.archive.org/web/20190519061054/http://riverpriver.com/) from 2019, four social media profiles and a new domain are present in the footer of the site:

- Telegram: @riverpoker (Channel)
- Telegram: @River_support (User)
- Facebook: RIVER-POKER-363891307068132
- Instagram: @river_poker
- Domain: www\[.]riverpop77\[.]com

The www\[.]riverpop77\[.]com domain was registered with GoDaddy and active between 2019 and 2020. It seems that there are no working archives of the site.

The @riverpoker Telegram handle seems to lead to an unrelated poker/gambling Telegram channel, presently. It is possible this might have been a mistake at the time of the archive, as the text content of the site said "Twitter," but linked to a Telegram. Searching Telegram for "River Poker" leads to a channel with the username @RiverPoker_com that has been actively posting about River Poker since 2016 utilizing the same logo as they do now; new posts in the channel link to the "com" site.

### Analyzing Eight Years of Telegram Messages

Using [this Python project](https://github.com/vile/telegram-from-json-to-url), it becomes very easy to filter the large Telegram chat export from River Poker's channel (consisting of over 14,000 messages over the past 8 years) for URLs that might be of interest. With some simple filtering built into the script (excluding a few social media sites and removing exact duplicate URLs), the number of unique URLs comes down to 53.

Manual analysis of these domains to ensure they are related to River Poker yields 22 that were, with a 100% confidence, used to promote and/or access River Poker at some point in time. In addition to this, one domain is unclear if it was actively used by River Poker (or an affiliate), as there is no live or archived content of it.

Confident domains:

- riv9922.com
- rivertime99.com
- riverchampions.com
- ribax99.com
- riverplay2play.com
- riverp1.org
- rivxc2.com
- riverforplay.com
- ribax4.com
- riverking2020.com
- river21.com
- riverp99.com
- river4play.com
- riverbet1.com
- riv8080.com
- riveraceking.com
- riverkingking.com
- rivdec25.com
- riverpoker77.com
- rivxy5.com
- riverforplay.com
- rifox123.com

Unsure domains:

- rivtehran.com

A new YouTube channel can also be found amongst the links posted in the channel.

- <https://www.youtube.com/@Riverpoker.online/videos>

## River Affiliate Domains

Including domains owned and operated by River Poker affiliates (that earn a commission by driving traffic) and not River Poker themselves, it quickly increases the number of total domains.  Searching queries such as `riverpoker.com` and `river poker com iran` yield sites and social media profiles using the logos of River Poker previously unknown. However, these sites and profiles link back to known River Poker domains, except with an affiliate ID as part of the URL (which is sometimes obfuscated or hidden).

Some examples include:

- hxxp://river-poker\[.]com
- hxxps://riverpoker\[.]online
- hxxps://river-poker\[.]info
- hxxps://riverpokerinfo\[.]blogspot\[.]com
- hxxps://riverpoker2024\[.]com
- hxxps://riverpokers\[.]com
- hxxps://www.instagram\[.]com/riverpoker.c
- hxxps://www.behance\[.]net/river-poker

![[Obfuscated Affiliate Link.jpg]](./images/Obfuscated%20Affiliate%20Link.jpg)

## Tron Deposit Addresses

On July 9th, 2024, the River Poker Instagram account posted two short form videos about how to deposit TRX and TRC20-USDT into the platform. During the course of the videos, a live deposit address is used as an example, shown in both text and QR code format.

While the text itself is slightly difficult to read, the QR code is high quality enough to be scanned:

- [TC3hN1LoW87EMaEv9Gre7QGe3ZRsahQwVy](https://tronscan.org/#/address/TC3hN1LoW87EMaEv9Gre7QGe3ZRsahQwVy)

![[River Poker Instagram Deposit.jpg]](./images/River%20Poker%20Instagram%20Deposit.jpg)

Using this as a pivot point, [River Poker's Tron hot wallet](https://platform.arkhamintelligence.com/explorer/address/TC3hN1LoW87EMaEv9Gre7QGe3ZRsahQwVy) can quickly be found. Subsequently, it can safely be assumed that all incoming funds are deposits relevant to the platform. Filtering all incoming USDT transactions (with a minimum of 1 token) for unique senders, 108 deposit address are identified. [Visualize the incoming flow using Arkham](https://platform.arkhamintelligence.com/visualizer/entity/TC3hN1LoW87EMaEv9Gre7QGe3ZRsahQwVy?flow=all&positions=%7B%225b31d181-13e5-4cd1-b07e-ab6c973febc0%22%3A%7B%22fx%22%3A-22%2C%22fy%22%3A-15%7D%7D&sortDir=desc&sortKey=time&to=TC3hN1LoW87EMaEv9Gre7QGe3ZRsahQwVy&tokens=tether&usdGte=1).

{{< details "Unique USDT Deposit Addresses" >}}

- TG45NjaKHSa5hvzb9GrEYkHL1HEqvko2je
- TRMZ21ByRaxVMPziDG6CsqNNzs8xhiZZhP
- TK6TZsmE2juaG8AxsBozYG3GZuXKW1ybtF
- THMNWVU5PprKZfNcw7Zwq6kgw3FNU94A6c
- TL6Vi5RBfgqttGRKmXXC9mhF7UJjh1BBrd
- TV7jZyg2zuC39sQXnYnp9rCqxnhdFMzjhu
- TMmT8gjYDBEuSNh1FNapkYD7whUfJtidZq
- TTECq4N7Wc5caS51Q7hFZeZAtzExjDGprZ
- TWyQjZfmx1zNw7oXBeWG5Tp9QLZVUhXj56
- TEdc8TePisLynDyfh1TNZoL2SM64fg73vZ
- TXHSiWWFA82sbEj216QgPsvqdo5trFPKBr
- TAWuxbTmX1hzY5ioKTCgzECHKUWre3i8XL
- TWrBjbREdioCcgDctaZibf1gUpdqVPXf45
- TRtBt21p86E7tbF7km1eP4CGEJ9m3KDboa
- TEQChZYdXcYibV849N2xrecnwndhhVMesK
- TY9NZNcjSR4mo5WYUtsZGXQ3T7m7EDMwPS
- TCfVoa3xqWQUXYh7jncfoCzArqwBDU9cZv
- TKSmv1kdTompVHtTwwvNtJsAMSGH34p7Ms
- TXz4uZrcsYvEmBGsAyRBXRhiMPvRkzZVbE
- TAFtEm22yiN4YncRFFXXtpj2DtgdLFjFcF
- TDEVNN4t7BxpjHmYCKWog9X6gh9rLYGzQW
- TErKnMEnQjGGVcHYjnT7E5oMHbAqwUcnZP
- TWUzEVFCY8jhuv6A9EhZwKqQ3nXn1Tta7X
- TZJnCM6RmYKf4A4ttk3jr4BUr6LdMb8bBK
- TJwuGGPLuHE7ScfofSr2iYH7gZazrzEunP
- TYd56zTfMTQWHaB6egdv5EUjjWesA7R1R7
- TBASheH8JBCmhQPvNC2zUhRo15evDuNaW9
- TBVahEDzjnBgJ8qW3NDD4YuJBGRPQxaeSa
- TSed5QWFx13kzidXx46MtdKsccfHbg2m2C
- TLAikCr4AuUG2ocxqAUXLqrcFSpAS93wfd
- TX9634a6iFNhJfiBkeuCLWzCdsp99yqqqT
- TEUaFfM414R75dw3tVx8oyo2KHGfcoRppD
- TN9eAv5Yh4Wm8UcvhKJYHeky7UXcikMpJv
- TVnuvP9AoaH8Tv72MJsHUTThbgwzEGBw2h
- TREkK1mBF1Yo8URztGKNnywFWyn9YJWj1M
- TRpZr2NrCDsFaxkwGbcrLRAoaFDRa64KKZ
- TMJjoh5BZ9nzQjaqZyhFpNNAFy5v7553vW
- TJiHNTUYZeLDTsxoEU7rUyxGzKAa3ewPph
- TDf1jmwX4SgVMHZToaHWcKrKKebjWDgff2
- TRXzGvBPYF9wdNY4icZX6ezTnhQtBE4n5T
- TPbUBZp3KBrefcJBH6W4hAcp7H2SJ884wv
- TT32Vd4R5DiTknHoR9DGNLzuqRWS9vTedo
- TX8h4sqCj1ywycCNtmLSc9n8vBAFGCx3gP
- TM4yCUfH42sjCGkifaQTyoLuPp3VgCz84W
- TVtHQhakKZQe4toBuSGgNUYPKajBDo4H7u
- TWdyGpdg8Kcxfv9J7WMymm4bYuERKcTWvc
- TK9SBgnbMZgVA2seNS8Cm8Gb7g8nzdUGjB
- TE31XZdFdmvMek2CUrRme83sqiiYej6CZs
- TRQMcqVVyrTpMn3vbqqcjAnamXa3K1uCeT
- TWawYHykA3ynvbVyoZ7ZyU7XQbAvHM4xSa
- TR5QXCAqteifATKn4upJgVdAC66ED9W8fd
- TUaxRHhrFsxAgHY5NCmuiEaYCqigqfc1kN
- TWHJ91NDLWxtLsEw97sSo2hqNzizSTv5P7
- TPLKsEJo7LUd5XNG8xpdwAzWPSRYSS7efM
- TT4ecTwRsbmHGiyRcKHvpx3mZYxEvb1PW8
- TN61xMiqyFPovfTntG6Vg83FttFkNu6i8q
- TRK2LPxcFf1nLhZ7yubsjPDzXCZh14sDcz
- TG3xxjMHX2D7Ua3JvrFrG1io9cvEZbeuEq
- TGnkNihL8A6r2f8hncDzzxQXJtZdAuTcBh
- TU8vwAogXZsqdscq9Dv2mrK3M5acWuj8Ax
- TKn68oyHg4x5WRfYsHQMtBiJcGnRk5fZVc
- TQW8WZncBFNDkJakfMbWN8WZKCpf35fZVc
- TCDeWGkDJDa4Lx34gPCPeK9tZnY14aGEig
- TBtpMTn6wnEzkyT79M45B57ziZAp6gQ8Mz
- TKL1tW8RBCnnchezHp4fSA6Y38gccEAkKX
- TVYqUyDJS7QziRYXuBDyMpMXN16qMnzxtG
- TJeAPvjJ5S8rwU7jJWoTHrBd6RmTqxeyQd
- THQ9MA5tecobQnetcSPryVNEfzYVzcJUw8
- TKnLb1K3UXo8iWgUkz6eXUh4u5vWk5fZVc
- TJiPf843HXU77vESr7VACSnZmZbpFbHFbS
- TSj7rwxr4RmUb91qihxWcDCvBSDeF1dxUo
- TL25AGRRFERV8RqBUS73vHH8Jresh8HeeC
- TEvSfAXGYWG82MdXqg388TavfwPnTcqJMm
- TXaMaeUP1drtQwiMxfQbJYdcHZN9zSU2PY
- TA2UZd1GvWQJihkBU7r7vTeoJjiU6H5Jrp
- TNESB1Bu6pBdKHNkNFHvFWuYgwmeZpxsQM
- TLmuubgmpD9VEBVVYhavrFcdKRVa8Uv9Ed
- TA4CuShCUT9FEUJsrLp2cYjFDB9ZYVucZo
- TYnaHwwAHhFtzR7W2fFJC5mr6CyiNTWAEz
- TZ95FJRmNCEaMiUqVEvPHsAwL6JEYP6p7J
- TM1abMGkrHmMrCb36hK8JHxM6oQH1axT3M
- TAh7tBj3hf1LFnZNBeYmThErrDvqU2TyBE
- TRQ8RSJDUnLEdue4Bee8MnYxD6mtkfAWQy
- TTowwTqnuFenYRABLtwFpvJMFHUGQHjQSB
- TBmKCzYywPDqnpfSEomqJfEGzUA9dQ3ZYp
- TYgXNrukfPRsz8GM5JY1aScJ7eDAGWJYGv
- TG4GH8FmHJzuMRQhofS8d2gcKMpRnVbKHG
- TEqsGUKQEKd6BG9Xivjbcz5oxkyGBGeVmB
- TU3gUWPxwWmWRtkHH8dyZNPjMavMeGTybz
- TRMfXEP8pyrdWNZCMfAvpL8cv5gozpf5Ww
- TKZ7kx4VaqUbsuGw5wrj2D3oNnivr9L41T
- TKdDcLZgT5Hngh2fZx1WsnW1xuU7YBn15C
- TPTxkXA8kiKAeWM2VuCYbVEkxib2Uz1Dwg
- TPfExaq5cBmf2SMqL7QmMCkVCkWtRkpcFb
- TTc15yJ62vBYvhswFVDDyjmJuSt2fGHvbz
- TUgX3231ipgRKsg8MtwjsD4ZeUcsMkqiPS
- TQRZBefWUAavT7ntW6vPmWCU5MMQGfHZK2
- TYpp917PLrMgUnwqS1tcmdUfuvdULVmyRZ
- TPrm7X5PuU9LnTws8BpL2A2Pw9sGdgn6mH
- TCgD1zMFV8nQxHXFRHw8R7rxBLpoXpgFzq
- TZCokNMTLZcbgQtDFotkkrvCdfU8jeKxkU
- TW94sXj28Y952r44M9HU3GDVrUKBTAPJy8
- TX6udWv8fcEHdqyeNu1CQk39ow3vvBv1UM
- TKgRJhka2mePejRSswbtD4Ae2ZXpqvPSA1
- TWjx238kn8tfW4m41yKjLmPdcJuczvyE9G
- TQ4XRhjLRqi27K58BbMwuJM8K2mLkSEBWP
- TNAZrvZ3F38z6pMEupTGZYRFmdYraxENtt
- TA79AVNuzte3jkgqxcsZyzLBBK2itjMLCy

{{< /details >}}
