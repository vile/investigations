---
title: "Mujahideen Brigade Investigation"
date: 2024-09-17T21:27:38-04:00
slug: 2024-09-17-mujahideen-brigade-investigation
type: posts
draft: false
categories:
  - default
  - investigation
tags:
  - default
  - osint
  - terrorism
---

## Preface

This is one of two articles based on "prompted" investigations. Starting out with a initial question and/or piece of media, the investigation is still open ended.

Initial Prompt:

How much information can you extract from the poster below? Bonus points for scraping any blockchain addresses with subsequent tracing.

![[Original Advertisement.png]](./images/amb-investigation/Original%20Advertisement.png)

## Initial Advertisement Analysis

At an initial glance, this seems to be a cropped or only part of a full image. The question specifically asks for blockchain addresses, however the text content of the image only asks for donations to help the Palestinian people without any further context or information.

First, let's figure out who this image might be promoted by. There is a large logo on the top left of the image consisting of a masked person holding a rifle along with other iconography and Arabic script. The same logo can be seen on the headband in the bottom right.

This logo is consistent with ones displayed by the Mujahideen Brigades a/k/a Al-Mujahidin Brigades (AMB); this is an OFAC-sanctioned entity active in Gaza, the West Bank, and Cairo (<https://www.opensanctions.org/entities/NK-eWVNkBLnU4whv7rUPaEv2G/>).

When looking for a social media presence for this group, various sources mentioned X (formerly Twitter) and Telegram accounts posting and claiming responsibility for various attacks. However, these sources either did not directly mention the usernames of accounts, provide links to the accounts, and/or images used in the sources were not original (e.g., they were heavily censored). However, one specifically did confirm my original suspicion that this was, in-fact, a cropped image (<https://www.memri.org/cjlab/gaza-based-al-mujahideen-brigades-which-kidnapped-israelis-october-7-opens-new-x-account>)

![[Memri Censored Adverisement.avif]](./images/amb-investigation/Memri%20Censored%20Adverisement.avif)

Continuing to research, [a TRM blog](https://www.trmlabs.com/post/us-doj-charges-hamas-leaders-with-october-7-attacks-details-hamas-use-of-cryptocurrencies) talks about several DOJ charges against leaders of Hamas and their relation to sanctions evasion by using cryptocurrency. In the same article, the AMB's solicitation of cryptocurrency is mentioned, which includes an example promotional image. In this fully uncensored and uncropped image, the same logos, style, and layout is used, along with three cryptocurrency addresses (and their respective QR codes) specifically for TRC20 USDT, Bitcoin, and Ether, as well as two Telegram links.

Cryptocurrency addresses present are:

- [TBL1w8wuCuTmwcDXx97AWcTNLLLAWQh3mg](https://tronscan.org/#/address/TBL1w8wuCuTmwcDXx97AWcTNLLLAWQh3mg) (Tron)
- [bc1qf42hkrnn8uj8z7kdk29dqs6hfzw6u06cpa4y70](https://mempool.space/address/bc1qf42hkrnn8uj8z7kdk29dqs6hfzw6u06cpa4y70) (Bitcoin)
- [0xeF8105D04D85395FF8328b694729687E54Bf68C5](https://etherscan.io/address/0xeF8105D04D85395FF8328b694729687E54Bf68C5) (Ether)

Telegram usernames present are:

- @kholafaps ("Channel 1")
- @darebmojahden ("Channel 2")

![[Uncensored TRM Ad.jpeg]](./images/amb-investigation/Uncensored%20TRM%20Ad.jpeg)

*Channel 1* (Arabic: مجمع الخلفاء الراشدين الدعوي - غزة; English: Rashidun Caliphs Call Complex - Gaza) predominantly contains general Islamic-related content, however it has solicited cryptocurrency donations multiple times to assist "struggling people in Gaza."

![[Rashidun Donation Ad.jpg]](./images/amb-investigation/Rashidun%20Donation%20Ad.jpg)

*Channel 2*, specifically, is run by the AMB (Arabic: كتائب المجاهدين - فلسطين; English: Mujahideen Brigades - Palestine). *Channel 2* consistently posts on a daily basis about attacks and actions attributed to the AMB. Along with this, calls for cryptocurrency donations are occasionally posted. Analyzing donation advertisements posted in the channel over the past year, it can be seen that the first use of the original image was on February 8th, 2024. The cryptocurrency addresses used in the image are consistent with the ones present in the TRM article.  Currently, as of September 15th, none of these addresses are publicly attributed or sanctioned by OFAC (as part of the SDN list).

![[AMB Donation Ad.jpg]](./images/amb-investigation/AMB%20Donation%20Ad.jpg)

## On-Chain Donation Address Tracing

Starting with the TRX address ([TBL1w](https://tronscan.org/#/address/TBL1w8wuCuTmwcDXx97AWcTNLLLAWQh3mg)), as it has the largest on-chain volume, it quickly becomes clear that the largest share of donations are direct USDT withdrawals from Binance. Spread across 32 incoming transactions, roughly USD\$2,710 has been sent to the address. Following Binance, [ByBit](https://platform.arkhamintelligence.com/explorer/address/TU4vEruvZwLLkSfV9bNw12EJTPvNr7Pvaa) and an unknown exchange ([TXtp6](https://platform.arkhamintelligence.com/explorer/address/TXtp6FhA3NXP2eZehTu3W1CptFjaMECDcJ)) have withdrawals of between USD\$500 and USD\$600. MEXC and Gate.io are also present in incoming transactions, but have a significantly lower combined dollar value (less than USD\$100). The remaining volume consists of independent wallets funded by some of the previously mentioned CEXs (such as Gate.io), as well as unmentioned CEXs (such as KuCoin and Bitget, and OKX). While it is concerning that such a large amount of direct withdrawals have been made to the addresses, direct CEX withdrawals have ceased as of March 11th, 2024; all subsequent funds come from self-hosted wallets.

![[AMB-TRX-small.png]](./images/amb-investigation/AMB-TRX-small.png)
\[<https://metasleuth.io/result/tron/TBL1w8wuCuTmwcDXx97AWcTNLLLAWQh3mg?source=cbdec801-3e4b-45a2-892d-5f44eb389bf8>; <https://postimg.cc/1VcVr7Yv>]

Now looking at the BTC address ([bc1qf](https://mempool.space/address/bc1qf42hkrnn8uj8z7kdk29dqs6hfzw6u06cpa4y70)), again, the vast majority of incoming volume is from CEXs, specifically [Binance](https://platform.arkhamintelligence.com/explorer/tx/783cb5fe6635348960b46ed76c068fa9a1c210cb6192c534a704cda8d0367968), [Crypto.com](https://platform.arkhamintelligence.com/explorer/tx/5adb0f91019011c5dd0bebcd3d92050e18c90ba5f1dba11c008b4b68f8c65113), and [Coinbase](https://platform.arkhamintelligence.com/explorer/tx/4f1fe8ad3215ba55201bcdeece14793a3ff6790e3d29f39a1f427e092ae22a4c). And, again, Binance makes up the largest share of CEX withdrawal activity (greater than 50%). The remaining volume consists of self-hosted wallets, except with a larger distance from the original CEX funding compared to Tron. However, the total USD\$ volume of the BTC address is less than 10% compared to Tron (~USD\$230).

![[AMB-BTC-small.png]](./images/amb-investigation/AMB-BTC-small.png)

\[<https://metasleuth.io/result/btc/bc1qf42hkrnn8uj8z7kdk29dqs6hfzw6u06cpa4y70?source=91642e48-4c4b-490d-bf33-278800f9f33e>; <https://postimg.cc/JD6DtHvh>]

The ETH address is slightly more interesting compared to Tron and Bitcoin. Activity is spread across both L1 Ethereum and BSC. CEX withdrawals are almost solely from BitGo, but a single small withdrawal was also made from Bitget. A large portion of funds eventually get deposited back into Bitget, whether directly or through an intermediary wallet. Remaining self-hosted wallet volume is consist with activity on TRX and BTC; some donating wallets on Ethereum have also donated to other OFAC- and CSL-sanctioned Middle Eastern related entities, such as [Gaza Now](https://www.opensanctions.org/entities/ofac-47635/).

It is also to note that the [single largest incoming transaction](https://etherscan.io/tx/0xc853c0a0fac9ccb66422aa840756594b07df9c00b2aceff02a99d1b2000efb5e) of any chain is present on Ethereum, a ~0.615 ETH "donation" worth roughly USD\$1600 at the time it was sent.

![[AMB-ETH-small.png]](./images/amb-investigation/AMB-ETH-small.png)
\[<https://metasleuth.io/result/eth/0xeF8105D04D85395FF8328b694729687E54Bf68C5?source=dc3be3bd-46b4-42a0-b22b-2fdbb0d3c311>; <https://postimg.cc/H8m578tD>]

### Gaza Donation Ruse

While looking at the surface of *Channel 1*, it seems to be solely promoting religious information and updates those affected in Palestine. However, analyzing the handful of solicitations for donations, makes the connection between Rashidun and the AMB much clearer.

The first cryptocurrency donation solicitation from *Channel 1* was on November 26th, 2023. This precedes the original AMB solicitation of interest by over four months. Looking back, the first cryptocurrency donation solicitation from *Channel 2* was also on November 26th, 2023, in addition to this, it was also a forwarded message from *Channel 1*. However, when following the forwarded message between the channels, the content is completely different; the message is marked as "edited" and contains a different cryptocurrency address. This was likely to be a mistake that was later corrected to keep perceived distance between the groups and channels.

![[First Donation Ad Comparison.png]](./images/amb-investigation/First%20Donation%20Ad%20Comparison.png)
\[Left: *Channel 1* (Rashidun); Right: *Channel 2* (AMB)]

Cryptocurrency addresses present in *Channel 1*:

- [TBL1w8wuCuTmwcDXx97AWcTNLLLAWQh3mg](https://tronscan.org/#/address/TBL1w8wuCuTmwcDXx97AWcTNLLLAWQh3mg) (Tron)
- [bc1qf42hkrnn8uj8z7kdk29dqs6hfzw6u06cpa4y70](https://mempool.space/address/bc1qf42hkrnn8uj8z7kdk29dqs6hfzw6u06cpa4y70) (Bitcoin)
- [0xeF8105D04D85395FF8328b694729687E54Bf68C5](https://etherscan.io/address/0xeF8105D04D85395FF8328b694729687E54Bf68C5) (Ether)
- [0x2F6cF9C58Ff6F82686E474F20dFD6a46199D655A](https://etherscan.io/address/0x2F6cF9C58Ff6F82686E474F20dFD6a46199D655A) (Ether)
- [0x5cb8ab15610502478a7f784AE2DAeEfe45aCb4Cd](https://etherscan.io/address/0x5cb8ab15610502478a7f784AE2DAeEfe45aCb4Cd) (Ether)
- [bc1q8y6wp8dmkjx0e3ngtlmjx6n9ry369khd3muum7](https://mempool.space/address/bc1q8y6wp8dmkjx0e3ngtlmjx6n9ry369khd3muum7) (Bitcoin; QR Code Only)
- [bc1qmakfg2avr5c5n8dm30cfaeqa273hc6pfpyswj9](https://mempool.space/address/bc1qmakfg2avr5c5n8dm30cfaeqa273hc6pfpyswj9) (Bitcoin; Text Only)

When looking on Ethereum and Bitcoin, the connection becomes very apparent, very quickly.

![[Mismatched QR Code.png]](./images/amb-investigation/Mismatched%20QR%20Code.png)

![[AMB-ETH-2-small.png]](./images/amb-investigation/AMB-ETH-2-small.png)
\[<https://metasleuth.io/result/eth/0xeF8105D04D85395FF8328b694729687E54Bf68C5?source=8ebcd070-2aeb-461a-aaf5-372fbc071dc6>; <https://postimg.cc/xJgP3Ppy>; If the graphic is difficult to understand, please use the interactive MetaSleuth chart link]

![[AMB+Rashidun-BTC-small.png]](./images/amb-investigation/AMB+Rashidun-BTC-small.png)
\[<https://metasleuth.io/result/btc/bc1qf42hkrnn8uj8z7kdk29dqs6hfzw6u06cpa4y70?source=648d9b93-22ed-4c8e-8aea-a35d1dff13da>; <https://postimg.cc/3dgJGkb9>]

In these charts, the blue nodes are known-AMB addresses, the red nodes are new Rashidun (*Channel 2*) addresses, then the green and gray pairs of nodes are the same addresses across different networks (ETH and BSC).

On Ethereum, both AMB- and Rashidun-associated addresses have utilized the same [Bitget deposit address](https://platform.arkhamintelligence.com/explorer/address/0x27486693cb339AfF673BCf66736227B559486a20) (on different networks), as well as have sent funds directly to each other. Similar activity is also present on Bitcoin when utilizing the same [Payeer deposit address](https://platform.arkhamintelligence.com/explorer/address/34TBpq7eJXDgC1vrv3tbTnCDe79eFzj97e).

It can also be seen on the BTC chart that one address has donated to both AMB and Rashidun wallets.

View Arkham entities of the [AMB](https://platform.arkhamintelligence.com/explorer/entity/67b7fce5-5561-4da2-8547-6096c1548276), [Rashidun](https://platform.arkhamintelligence.com/explorer/entity/cf627155-5f72-4ece-ba88-88ae0e6457d5), and [AMB Associated](https://platform.arkhamintelligence.com/explorer/entity/5e4883a7-cab2-40a2-a78c-efd81dd07289) wallets.

## Other OPSEC Notes

Trust Wallet seems to be the primary, if not the sole, wallet software used across both channels. All QR codes posted are consistent with the style used by the Trust Wallet mobile app. It is unclear from promotional images what mobile OS is being used.

The AMB (and Rashidun by extension) rely entirely on centralized, off-chain platforms for moving and concealing funds. No on-chain concealment, coin-join, chain hopping, or DeFi was observed. Except for a single DEX swap on BSC using Mimic Finance ([which is integrated into Trust Wallet](https://medium.com/mimicfi/introducing-mimic-v3-diving-into-new-depths-of-efficiency-4e564ad2714a)).
