# CN2 VPS: Is the Return Path Really GIA? What Happens After the Traffic Cap, and Which Plan Fits Your Users (Full Plan Table + Peak-Hour Latency)

A CN2 VPS is worth its price only when the return path from mainland China back to your server runs on CN2 GIA (AS4809). Outbound-only GIA is why a provider's looking glass shows 150 ms while someone in Shanghai waits eight seconds for a page at 9 p.m. The second thing that decides whether a plan is still usable six weeks in is what the host does when you burn through the monthly transfer.

Evoxt, the host this article covers plan by plan, does not sell CN2 GIA. Its Hong Kong and Osaka nodes peer at HKIX, JPIX and BBIX with direct links to China Unicom, which is solid regional peering and a different product from China Telecom's premium transit. So the useful question isn't which Evoxt plan is secretly GIA. It's whether you need GIA at all, and if you don't, how much machine $5.99 or $23.99 actually buys.

Below: how to tell real GIA from a CN2 label, the full Evoxt lineup with prices, what the same money gets you at three GIA specialists, and three things to confirm before you pay anyone.

> **Quick pick.** Start with **VM-1 at $5.99/month** — 1 core, 2 GB RAM, 20 GB storage, 1 TB of transfer on a 1 Gbps port, with weekly offsite backup included. It's the cheapest Evoxt plan with enough RAM to run a real site, a small API backend, or a build box, and VM-2 doubles cores and RAM for another $6. If China Telecom households are your audience and evening latency decides whether they stay on the page, Evoxt is the wrong product and no plan in this table fixes that.
> 👉 [Check VM-1's current price and availability on Evoxt](https://bit.ly/EvoXt)

## The full Evoxt lineup, both networks

Evoxt splits its catalog by network quality, not by routing optimisation. The same VM-1 costs the same on the Standard network and on the Premium network; only the monthly transfer allowance changes. That is an unusual way to structure a price list, and it's worth understanding before you pick.

**Standard network** (17 locations across the US, Canada, UK, Germany, Poland, Netherlands, Switzerland, France, Japan, Hong Kong, Malaysia, Indonesia, Australia and South Korea):

| Plan | vCPU / RAM | Storage | Transfer | Price (USD) | Order |
| --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 core / 512 MB | 5 GB | 500 GB | $2.99/mo | [Order VM-0.5](https://bit.ly/EvoXt) |
| VM-1 | 1 core / 2 GB | 20 GB NVMe | 1,000 GB | $5.99/mo | [Order VM-1](https://bit.ly/EvoXt) |
| VM-2 | 2 cores / 4 GB | 30 GB | 2,000 GB | $11.99/mo | [Order VM-2](https://bit.ly/EvoXt) |
| VM-4 | 4 cores / 8 GB | 60 GB | 4,000 GB | $23.99/mo | [Order VM-4](https://bit.ly/EvoXt) |
| VM-8 | 8 cores / 16 GB | 80 GB | 6,000 GB | $47.99/mo | [Order VM-8](https://bit.ly/EvoXt) |
| VM-16 | 16 cores / 32 GB | 100 GB | 10,000 GB | $95.99/mo | [Order VM-16](https://bit.ly/EvoXt) |

**Premium network** (Hong Kong and Osaka — same plan names, same CPUs, less transfer because Asian bandwidth costs more):

| Plan | vCPU / RAM | Storage | Transfer | Price (USD) | Order |
| --- | --- | --- | --- | --- | --- |
| VM-1 | 1 core / 2 GB | 20 GB | 500 GB | $5.99/mo | [Order Premium VM-1](https://bit.ly/EvoXt) |
| VM-2 | 2 cores / 4 GB | 30 GB | 1,000 GB | $11.99/mo | [Order Premium VM-2](https://bit.ly/EvoXt) |
| VM-4 | 4 cores / 8 GB | 60 GB | 2,000 GB | $23.99/mo | [Order Premium VM-4](https://bit.ly/EvoXt) |

You pay the same $5.99 for VM-1 on either network and get half the transfer on Premium. What that missing 500 GB buys is a Hong Kong or Osaka IP with regional peering. It does not buy routing priority to China Telecom. If you were hoping the word "Premium" meant CN2, it doesn't here.

The hardware pitch is the other half of the story. Evoxt advertises single-core clocks up to 6.0 GHz and compares itself directly against AWS at 2.4 GHz, Azure at 2.3 GHz, DigitalOcean at 2.3 GHz and Google Cloud at 2.2 GHz on that one metric. Every plan includes weekly offsite backup at no extra cost, and the platform supports Bitcoin and USDT payment, a REST API, floating IPs, sub-accounts and VM cloning. For a host selling $2.99 boxes, the backup inclusion is the detail that stands out; most budget providers charge for it or skip it.

## CN2, CN2 GT, CN2 GIA: what actually differs

China Telecom runs two CN2 tiers and the gap between them is the whole reason this topic is confusing.

**CN2 GT (Global Transit)** is the lesser tier. It beats the old 163 backbone, but capacity is shared and it congests during the evening peak along with everything else. Plenty of providers market GT, or a partially-optimised mix, as "premium CN2."

**CN2 GIA (Global Internet Access)** is the dedicated tier: fewer hops, separately provisioned capacity, materially lower packet loss. China Telecom charges upstream carriers roughly **$120 per Mbps** for it, which is why genuine GIA plans start around $30/month and why $2/month "CN2" listings are almost never GIA.

A properly built GIA path from the US West Coast to mainland China looks like this:

- **Outbound:** China Telecom via CN2 GIA (AS4809), China Unicom direct (AS4837), China Mobile via CMI (AS58453)
- **Return:** all three carriers back through CN2 GIA (AS4809)
- **Latency:** roughly 140–180 ms from mainland China, flat through the evening peak

A generic US VPS on whatever transit is cheapest lands at 250–300 ms with packet loss that climbs as the night goes on. That's the difference between a visitor who never notices your server is in Los Angeles and one who gives up at the eight-second mark.

The return path is the part buyers get wrong. A lot of providers buy GIA outbound, route the return traffic over whatever is cheapest, and the result tests well from the provider's own network while feeling broken from Shanghai at 9 p.m. Bidirectional GIA is the only version that delivers the 140–180 ms figure above. When you evaluate any host, ask which carriers return via AS4809, whether the plan is GIA or GT, and whether there's a looking glass you can traceroute from a China Telecom line during peak hours. A "CN2" tag in a catalog means nothing on its own; it has to be checked per data centre.

## Where Evoxt fits, and where it doesn't

Evoxt is a Malaysia-headquartered provider founded in 2020, and its product is fast cores at low prices. On the China question, the honest position is that Hong Kong and Osaka are well-peered, not premium-transit. HKIX, JPIX and BBIX plus direct China Unicom links give you decent regional latency and a respectable path for Unicom users. They do not give you the AS4809 return path that Telecom residential users feel at dinner time.

That makes the decision fairly clean:

- **China Telecom residential users are your audience and evening latency is the product.** Buy bidirectional GIA from a specialist. Evoxt's Hong Kong node will not close the gap, and paying for a bigger Evoxt plan won't either.
- **Your traffic is mostly China Unicom, or your users are spread across Asia rather than concentrated in mainland China.** Well-peered Hong Kong or Osaka is a reasonable bet, and Evoxt's price per core is hard to beat.
- **China routing isn't the point at all.** You want cheap fast cores for CI runners, a game server, a dev sandbox, or a container host. This is where the lineup makes sense.

👉 [Compare Evoxt's Standard and Premium plan lists side by side](https://bit.ly/EvoXt)

## What the same money buys at the GIA specialists

This is the comparison that actually decides the purchase. All figures below are list prices from published plan pages and third-party trackers; none of these providers are affiliated with Evoxt.

| Provider & plan | Specs | Port / transfer | Price | Refund |
| --- | --- | --- | --- | --- |
| DMIT LAX.Pro.TINY | 1 vCore, 2 GB, 20 GB SSD | 1 Gbps / 1 TB | $88.88/yr | 3 days (under 30 GB used) |
| DMIT LAX.Pro.STARTER | 2 vCores, 2 GB, 40–80 GB SSD* | 10 Gbps / 3 TB | $29.90/mo | 3 days |
| HostDare CSSD1 | 1 core, 1 GB, 25 GB NVMe | 50 Mbps / 500 GB | $60.99/yr | 3 days, less $0.50–1 |
| HostDare CSSD2 | 2 cores, 2 GB, 50 GB NVMe | 60 Mbps / 1 TB | $115.99/yr | 3 days |
| BandwagonHost DC9 CN2 GIA | 1 vCPU, 1 GB, 20 GB SSD | 500 GB or 1 TB | $79.99/yr** | Not published |
| BandwagonHost KVM 20G | 2 vCPU, 1 GB, 20 GB SSD | 1 TB | $49.99/yr** | Not published |

\* Third-party write-ups of DMIT's LAX.Pro line disagree on whether the STARTER ships 40 GB or 80 GB and on the Pocket's vCPU count. The TINY figures ($88.88/yr, 1 core, 2 GB, 20 GB, 1 TB) are consistent across sources.

\** BandwagonHost figures come from a third-party price tracker that labels the DC9 entries as imported list prices, not live checkout quotes. The same tracker warns that a CN2 label in a catalog doesn't guarantee GIA, which is the right instinct.

Two things jump out. First, port speed separates these plans more than price does. HostDare caps uplink at 30–100 Mbps depending on the plan; DMIT runs 1–10 Gbps; Evoxt lists 1 Gbps across its lineup. If you're moving files rather than text, a 50 Mbps port is the constraint you'll hit first, not the transfer allowance. Second, the entry ticket to real GIA is lower than the folklore suggests. DMIT's TINY at $88.88/year is genuine bidirectional GIA on 2 GB of RAM, which is roughly the same hardware Evoxt sells for $71.88 across twelve months.

## Three things almost nobody asks before paying

### What happens when you exceed the monthly transfer

Three models exist, and they feel completely different at 2 a.m. during a traffic spike.

DMIT throttles. Nothing gets cut off and no overage invoice arrives; the port just drops. WEE and MALIBU fall to 2 Mbps, TINY through STARTER to 4 Mbps, MINI and MICROv3 to 8 Mbps, MEDIUM and above to 10 Mbps. For a personal blog that suddenly gets shared somewhere popular, 4 Mbps keeps the site up and reachable. It won't keep video smooth, but it won't take you offline either.

The other two models are suspension (your VM goes dark until the next billing cycle or until you buy more) and metered overage (you get a bill). Both turn a good day of traffic into a bad one. Evoxt's public plan listings quote a monthly transfer figure without spelling out the overage behaviour, so ask support directly before you pick a plan you expect to run hot. It's a two-minute email that decides whether a spike is an inconvenience or an outage.

### Does IPv6 take the same route

Even on networks that advertise full GIA, IPv6 often doesn't get the premium path. DMIT's LAX.Pro series is explicit about this: IPv4 goes over CN2 GIA, IPv6 goes over AS4134, ordinary China Telecom. If half your traffic is IPv6 and you assumed the whole pipe was premium, you're paying GIA prices for standard routing on that half.

Ask any host two questions: does this node hand out IPv6 at all, and does IPv6 leave through the same carrier path as IPv4. Neither answer is usually on the pricing page.

### What happens when the IP gets blocked

Any IP serving mainland China eventually gets blocked. The variable is what the replacement costs. DMIT's Premium and Eyeball tiers replace a blocked IP free once every 15 days, then charge $5 per replacement after that. That's a concrete, budgetable number, and it's the kind of policy that separates a host that expects this problem from one that doesn't. Ask before you buy, especially on annual plans where you can't simply walk away.

## The twelve-month arithmetic

Evoxt's listed prices are monthly. Here's what a year at list price actually costs, before any annual-billing discount you may or may not find at checkout:

| Plan | Monthly | 12 months at list price |
| --- | --- | --- |
| VM-0.5 | $2.99 | $35.88 |
| VM-1 | $5.99 | $71.88 |
| VM-2 | $11.99 | $143.88 |
| VM-4 | $23.99 | $287.88 |
| VM-8 | $47.99 | $575.88 |
| VM-16 | $95.99 | $1,151.88 |

Put VM-1 next to DMIT's LAX.Pro.TINY and the comparison gets uncomfortable in a useful way. Both give you 1 core, 2 GB RAM, 20 GB of disk, 1 TB of transfer on a 1 Gbps port. Evoxt costs $71.88 over twelve months; DMIT costs $88.88 a year. The gap is **$17**, and what the $17 buys is the AS4809 return path. If your users are on China Telecom and latency matters, $17 a year is the cheapest upgrade in this entire article.

At the other end, Evoxt VM-4 at $23.99/month works out to $287.88 a year for 4 cores, 8 GB RAM, 60 GB and 4 TB. DMIT's LAX.Pro.STARTER runs $29.90/month, or $358.80 a year, for 2 vCores, 2 GB, 3 TB and a 10 Gbps port with GIA. Those aren't competing products. One is a compute box, the other is a routed network with a server attached.

One thing to verify before committing to an annual term: the renewal rate. Introductory pricing that resets in year two changes the arithmetic above completely, and it's the single most common surprise in this market. Confirm the renewal figure in writing.

👉 [Start with VM-1 at $5.99/month and confirm renewal pricing at checkout](https://bit.ly/EvoXt)

## Which plan, and what to confirm first

Match the plan to what actually hurts.

**A tiny always-on box** — a monitoring agent, a jump host, a WireGuard endpoint for two people — VM-0.5 at $2.99/month is enough and nothing more expensive is justified.

**A real site, a small API, a build agent, a Telegram bot** — VM-1 at $5.99/month. The 2 GB of RAM is the line between running Nginx, PHP and MySQL comfortably and swapping constantly. Most readers land here.

**Compile-heavy work, CI runners, game servers, a dozen containers** — VM-4 at $23.99/month. Four fast cores and 8 GB for under $24 is the plan that makes people re-read the page, and it's the one place where Evoxt's positioning is genuinely difficult to argue with.

**Hong Kong or Osaka presence with decent regional peering** — Premium VM-1 or VM-2. Take the halved transfer allowance as the price of the location, and don't expect GIA behaviour from it.

**China Telecom users at peak, where latency decides revenue** — not Evoxt. Buy bidirectional GIA, budget roughly $89 a year as the entry point, and test from a real China Telecom line inside the refund window.

Three things to confirm before you pay anyone, including Evoxt: what happens at the transfer cap on your specific plan, whether the node's IPv6 takes the same route as its IPv4, and what the renewal price is after the first term. Get those three in writing and the rest of the decision is arithmetic.

👉 [Check current Evoxt plan availability and pricing](https://bit.ly/EvoXt)
