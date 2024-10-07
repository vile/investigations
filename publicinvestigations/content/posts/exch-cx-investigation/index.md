---
title: "Investigating Hackers', Exploiters' Favorite Instant Crypto Exchange"
date: 2024-10-06T20:31:24-04:00
slug: 2024-10-06-exch-cx-investigation
type: posts
draft: false
categories:
  - default
  - investigation
tags:
  - default
  - osint
  - crypto
  - vasp
summary: "If you've done any reading or sleuthing regarding the movements of funds after hacks, you've probably encountered eXchCX before. Incidents including but not limited to... "
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

## Context

If you've done any reading or sleuthing regarding the movements of funds after hacks, you've probably encountered eXch\[.]cx before (incidents including but not limited to: [the DPRK a/k/a Lazarus](https://www.linkedin.com/pulse/attackers-using-exchcx-launder-money-series-recent-hacks-ffjze/), [Monkey Drainer](https://www.binance.com/en/square/post/428465), [Inferno Drainer](https://x.com/MistTrack_io/status/1828612983901299055), [Pink Drainer](https://x.com/MistTrack_io/status/1785061811106021712), [Mark Cuban stolen funds](https://x.com/bax1337/status/1804895980644364337), [the Lykke exploiter](https://x.com/MistTrack_io/status/1834185964585164858), [Mango Farm's exit scam](https://x.com/tayvano_/status/1743789297877262642), [Terra IBC exploiter (Astroport token)](https://x.com/Rarma_/status/1818813592214684037), [the FixedFloat exploiter](https://x.com/GlobalLedger/status/1760641171288740300), [various phishing customers](https://x.com/MOKSHA_256/status/1774146600559837532), [CEX fraud](https://x.com/zachxbt/status/1758542426128679172), and many, many more). But, where exactly did this infamous hardline no-KYC exchange come from?

## Exch's 2014 Origins

Exch originally operated under the eXch\[.]cc domain between April 2014 and May 2016, only supporting Bitcoin, Perfect Money, and BTC-e vouchers. Their first online presence outside of the domain was established April 19th, 2014 when a BitcoinTalk forum account was registered. On this account, a thread was published under the "Service Discussion" topic promoting the site's 24/7 automatic exchanging of Bitcoin and Perfect Money (later WebMoney and manual PayPal exchanges were supported). The thread received a handful of replies about the service, but activity would quickly peter out at the beginning of 2015. Exch's personal BitcoinTalk account activity would abruptly cease in May 2015.

Looking into the account's more recent activity, post-2022, we can get an idea of what happened between 2015 and 2016 that led to the closing of the service. No exact specifics are mentioned, but the falling out of a partnership between eXch and BTC-e seems to be the main reason.

During 2014, eXch's BitcoinTalk account would reply to many threads on the forum, ranging from technical to personal. While many of the account's posts have been scrubbed (various instances of quoted posts exist with no original post), the currently available posts can paint a picture of the operator. A male, non-native English speaker, ex-smoker, interested in privacy, cybersecurity, Porsches, and 90's era music and film, favorite game Lineage 2, and likely living in Austria (Innsbruck) or Germany.

![[BitcoinTalk Posts.png]](./images/BitcionTalk%20Posts.png)

We can gather a handful of other clues from BitcoinTalk activity, such as consistently posting in the afternoon and evening for American time zones, which would align with Austria and Germany's evening and night, and noticing that some of the posts that include images utilize German-based image hosters (i.e., myimg.de).

Buried in a 2023 BitcoinTalk post by the eXch account, we can find eXch's old BestChange profile. While there is not a lot of information on the profile, it does show the country of operation as Germany.

![[BestChange Profile.png]](./images//BestChange%20Profile.jpg)

## Tracing eXch's Original Bitcoin Wallet

Exch's original ".cc" Bitcoin wallet was funded on January 25th, 2014 between two transactions totaling roughly 12.5 BTC. It can be found [hidden in various archives](https://web.archive.org/web/20150319012239/https://exch.cc/?!=btcpm) of the old site (open inspect element and search for "OUR BITCOIN ADDRESS"). Following the original chain of UTXOs, these funds are likely to originate from BTC-e (specifically [this consolidation wallet](https://platform.arkhamintelligence.com/explorer/address/1Facb8QnikfPUoo8WVFnyai3e1Hcov9y8T)). Throughout eXch's normal operation, interactions with darknet markets, high risk merchants, OFAC sanctioned entities, and Coinjoin services were common. Entities include, [UniCC Shop](https://www.elliptic.co/blog/unicc-the-largest-dark-web-vendor-of-stolen-credit-cards-retires-after-raking-in-358-million-in-crypto), [LuxSocks](https://krebsonsecurity.com/2022/07/911-proxy-service-implodes-after-disclosing-breach/), [Ali Khorashadizadeh](https://home.treasury.gov/news/press-releases/sm556), [JokerStash](https://www.bleepingcomputer.com/news/legal/us-charges-jokers-stash-and-rescator-money-launderers/), [AlphaBay](https://www.justice.gov/opa/pr/alphabay-largest-online-dark-market-shut-down), [RAMP](https://en.wikipedia.org/wiki/Russian_Anonymous_Marketplace), and [Evolution Market](https://www.bitdefender.com/blog/hotforsecurity/dark-web-drug-market-evolution-vanishes-off-the-net-taking-millions-of-dollars-with-it/).

Exch would continue to operate normally until May 21st, 2016 when transactions abruptly stopped; a total of 57.677 BTC (roughly $136,000 at the time) still remained in the wallet.

On May 25th, four days later, eXch's remaining BTC would start moving. Over the next three days, coins would be deposited into various exchanges including BTC-e, Kraken, Bithumb, Korbit, the P2P exchange Paxful, and primarily Bitfinex (roughly 40 of the 57 BTC). A small portion of funds, roughly 3.1 BTC, would end up being deposited into Bitcoin mixers, specifically Bitmixer and Bitcoin Fog. Both mixers would eventually shut down, whether [willingly](https://www.bleepingcomputer.com/news/technology/internets-largest-bitcoin-mixer-shuts-down-realizing-bitcoin-is-not-anonymous/) or [not](https://www.elliptic.co/blog/us-takes-down-bitcoin-fog-mixing-service). [See the interactive chart here](https://metasleuth.io/result/btc/f5e3ad4d33e9df9eae58d1f37d1826a11a1f98425dda2b3d640be1c32041e401?source=a7f4f1dc-ab26-4c0b-9884-0e0dc7f686b2).

## The Funding of Modern eXch Wallets

Exch's current Ethereum hot wallet was funded on July 20th, 2022 with $113 worth of ETH originating from Binance. Over the next four months, various test transactions occur and liquidity is finally added. Funds primarily originate from OKX, but Binance was used at least one other time, as well as Kraken in 2023.

Using timing analysis, its possible to identify a likely OKX deposit address belonging to eXch, [0xf5dc](https://platform.arkhamintelligence.com/explorer/address/0xF5dc7E011Daeff0B2628E492262892000cA78847). Exactly 40 ETH and 70,000 USDC is withdrawn from eXch's hot wallet on October 2nd, 2022 which is then deposited into OKX between four transactions. Specifically, [30,000 USDC is deposited]( https://platform.arkhamintelligence.com/explorer/tx/0x8b71d2f9e6c043265adb24f83d266bc0985cb314e1342d3049fa2bfdd55c2825) at 12:52 PM UTC. Subsequently, [29,860 DAI is withdrawn](https://platform.arkhamintelligence.com/explorer/tx/0x53969a0afbb8b5fb046be29bb945b6f0154d7c4d08911941912186b913d5a81e) from OKX to one of eXch's original funding wallets at 1:02 PM UTC. This DAI Is then directly sent to eXch to provide liquidity.  [See the interactive chart here](https://metasleuth.io/result/eth/0xf1dA173228fcf015F43f3eA15aBBB51f0d8f1123?source=203e1c93-3f2d-4ffe-add2-da3f74adefca)

![[eth-0xf5dc7e011daeff0b2628e492262892000ca78847-small.png]](./images/eth-0xf5dc7e011daeff0b2628e492262892000ca78847-small.png)

The other deposits do not seem to have conclusive outputs, which likely means funds were exchanged and withdrawn as Monero. Later, eXch would [start utilizing DEXs instead of CEXs](https://platform.arkhamintelligence.com/explorer/address/0x2aB34e155F103eAe29A16db40e8d66D41A831B31), specifically for balancing stablecoins.

The use of these three CEXs specifically aligns with both posts by eXch on BitcoinTalk, as well as their site. Exch has previously stated on the forum that they occasionally used Binance and Kraken to increase XMR reserves, but stopped doing so as "they became very uncomfortable with us draining so much liquidity from them." In addition, eXch previously obtained pricing information for coins by using the "latest trading data of the following markets: Binance, OKEX, Kraken" which can be [seen in various archives](https://web.archive.org/web/20221005033424/https://exch.cx/).

![[Connection to Binance Kraken.jpg]](./images/Connection%20to%20Binance%20Kraken.jpg)

![[XMR Reserves.jpg]](./images/XMR%20Reserves.jpg)

## Not-So-Clean Funds

Exch has been consistently accepting clearly stolen funds, days and even months after they've been publicly attributed to exploits and hacks. For example, tokens from the Terra IBC/Astroport exploit were bridged to Ethereum on July 30th, 2024 and then swapped using eXch over the following 6 days. There was no obfuscation of the funds going into eXch, they were directly deposited.

The funds from the Terra IBC exploit were attributed within four hours of them being bridged, in [this Tweet by Rarma](https://x.com/rarma_/status/1818489754373308907). Subsequently, the address was labeled on Etherscan and other providers (such as BlockSec). In the following days, the exploit and address would gain continued coverage, such as from [Rekt News](https://rekt.news/astroport-rekt/), [Binance](https://www.binance.com/en/square/post/2024-07-31-hack-exploits-astroport-code-on-neutron-millions-of-astro-issued-11521954943842), and [Blockbasis](https://blockbasis.com/p/astroport-hack-64-million-loss-security-failures).

Maybe there is some leniency here, eXch is a relatively small platform with few to maybe even zero employees. However, this can be immediately dismissed as another researcher, [RealVovochka](https://x.com/TobyFrei4), [emailed eXch on August 1st, 2024](https://x.com/TobyFrei4/status/1818976403548737686) (two days after the hack) asking for assistance in identifying funds that had already passed through the platform, providing both deposit addresses and the exploiter's main wallet. Exch responds after eight hours and proceeds to give a non-answer to the request, but, more interestingly, claims to use Elliptic's risk screening service and states they were "too slow to mark these funds as stolen" thus it was not their fault. Where this falls apart, is the fact that the exploiter, now known to both eXch and the wider community, proceeds to send another $259,000 between seven deposits into eXch **three days after** Vovochka's email and **four days the initial attribution**.

![[Toby Email.png]](./images/Toby%20Email.png)

![[Further eXch Deposits.png]](./images/Further%20eXch%20Deposits.png)

This is not an isolated incident. The [Lykke exploiter](https://x.com/somaxbt/status/1799812652610511043) has moved almost $6 million DAI through eXch between early August and Late September 2024. Once again, there is no obfuscation. Five months after the attribution, eXch is still happily accepting the exploiter's funds.

The chart below shows the exploiter's movement of funds, primarily sending DAI to eXch. [See the interactive chart here](https://metasleuth.io/result/eth/0x9172a72f5009ca609833819763A2722e53806443?source=e574cd9f-65b6-4e7f-b11f-2705ac380f60) (red nodes are the Lykke exploiter and the blue node is eXch's Ethereum hot wallet).

![[eth-0xf1da173228fcf015f43f3ea15abbb51f0d8f1123-small.png]](./images/eth-0xf1da173228fcf015f43f3ea15abbb51f0d8f1123-small.png)

I find it highly unlikely this is the fault of the risk screening, these exploits are too high profile to fly under the radar of an analytics and compliance company like Elliptic.

These are just two recent examples, eXch has been accepting high risk funds nearly since its inception. [Monkey Drainer's federalagent.eth](https://etherscan.io/txs?a=0x84527b5949d479c879b8dd71cd8f79048cdf6fb8) wallet started using eXch just six months after the platform came back online in 2022. Between March and April of 2023, Monkey would deposit over $1.45 million worth of ETH into eXch.

Even further back, eXch started receiving funds from the [Magos ICO scam](https://steemit.com/magos/@nighthawk888/the-million-dollar-magos-io-and-aio-network-scam) ([archive](https://archive.ph/W1YmY)) **less than 30 days** after relaunching their service. [The first Magos deposit](https://platform.arkhamintelligence.com/explorer/tx/0xcf49f03ede1953eb464080c6f942ee3786ef29df831320cbdad868dc6606f3f4) was the 140th incoming transaction to eXch, and the majority of transactions before this were test deposits by eXch themselves. [See the interactive chart here](https://metasleuth.io/result/eth/0xcf49f03ede1953eb464080c6f942ee3786ef29df831320cbdad868dc6606f3f4?source=1493d126-fab7-46e0-b9e4-5f69fd8f72b2).

![[eth-0x9a389153f472ea2a0210d31431f08c0d9afad48b-small.png]](./images//eth-0x9a389153f472ea2a0210d31431f08c0d9afad48b-small.png)

All of these examples directly go against eXch's claims on the BitcoinTalk forum about how "clean" their funds actually are.

![[eXch Clean Funds Claim 1.png]](./images/eXch%20Clean%20Funds%20Claim%201.png)

![[eXch Clean Funds Claim 2.png]](./images/eXch%20Clean%20Funds%20Claim%202.png)

## The Precedent of No-KYC Exchanges

As of September 2024, there have been two independent actions taken against no-KYC exchanges. Specifically, Germany's "[Operation Final Exchange](https://www.chainalysis.com/blog/german-authorities-seize-russia-centric-exchanges/)" which seized the infrastructure of 47 Russian-based no-KYC exchanges and [OFAC's sanctions](https://www.chainalysis.com/blog/ofac-sanctions-russian-exchange-cryptex-uaps-fraud-shop-2024/) against a different no-KYC exchange, PM2BTC. These services primarily serviced cybercriminal proceeds, including those coming from darknet markets, ransomware gangs, scams, and fraud.

## Closing Remarks

In my opinion, there are likely few to zero further OSINT leads regarding eXch and the ball is now in law enforcement's court. Exch has accepted high risk funds without remorse both during 2014-2016 and 2022 onwards. If any official agencies are interested in information I have not made public, please reach out via Telegram ([@Fable](https://t.me/Fable)) or email f \[at] nta \[dot] sy.
