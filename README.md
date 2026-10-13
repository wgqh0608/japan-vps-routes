# japan vps: how to pick a Tokyo server that survives evening peak — routes, real prices, and DMIT's plans compared

Most people typing "japan vps" into a search box are not shopping for a country. They already know they want a server in Japan. What they're actually trying to figure out is which of the ten providers with a Tokyo button will still be usable at 9pm, and why two 1-core 1GB machines with identical spec sheets behave completely differently once real traffic shows up.

That gap is almost entirely about routing and overselling, not CPU. So this piece starts there, then gets specific about one provider with an unusually clear lineup in Tokyo — DMIT — including its full Japan pricing, which plans are actually worth the money, and which ones are a trap for the wrong buyer.

## The three different jobs people mean by "japan vps"

Search intent on this keyword splits cleanly, and the right answer changes depending on which bucket you're in.

**Serving users inside Japan.** A shop, a SaaS backend, a game server, anything where the audience is in Tokyo, Osaka, or Fukuoka. Here you want a Tokyo facility with dense local peering — the exchanges that matter are JPNAP, JPIX and BBIX — and you're measuring latency in single-digit milliseconds. Nothing exotic required.

**Reaching East Asia from a middle point.** Users in Korea, Taiwan, coastal China, plus Japan. Tokyo happens to be the geographic sweet spot for this, and the numbers back it up. From a Tokyo data center, round-trip times run roughly 2–5ms locally, 30–35ms to Seoul, 50–55ms to Taipei, 50–60ms to Hong Kong and 70–80ms to Singapore, versus 100–110ms to Los Angeles and 180–200ms to New York.

**Needing a Japanese IP, or a route that behaves on mainland China networks.** Japan-origin IPs matter for account registration, certain streaming catalogues, and Japanese-market e-commerce. If mainland China access quality is also part of the requirement, you're now shopping for a much smaller set of products, because standard NTT transit from Tokyo to China routinely degrades badly during the evening.

That last bucket is where most disappointment lives. "Japan is close to China" is true geographically and often false on paper. Packets can and do route Tokyo → US west coast → back into China, and a Japan server that pings 60ms at noon can sit above 200ms with visible packet loss by 10pm. Physical distance stops being the deciding factor the moment you're on shared international transit.

## Route tiers in Japan, minus the marketing

Providers in Tokyo sell essentially four kinds of network, and the price gap between them is not arbitrary.

**Plain international transit.** Usually NTT, sometimes mixed with Cogent or Telia. Great for global reachability and Japanese domestic traffic, weak for mainland China, especially evenings. Cheap.

**Optimized China return routes.** This is where terms like CN2 GIA (China Telecom's premium international backbone), AS9929 (China Unicom's premium network) and CMI (China Mobile International) come from. A server with CN2 GIA on the return path skips the congested public handoff points, and the practical difference during peak hours is not subtle.

**Other regional optimizations.** SoftBank and IIJ routes are well regarded for China-bound traffic in their own right and are what you'll see pitched by Japanese and Chinese-market providers alike. They are not CN2 GIA, and they are not equivalent to it.

**DDoS-filtered transit.** Relevant for game servers and anything with an adversarial audience; usually sold as an add-on or a separate network profile.

Worth flagging: "CN2" on a product page is a weak claim by itself. Plenty of Japan VPS products use CN2 on the outbound path only, or only for one of the three Chinese carriers, and market the whole thing as a China-optimized server. Before paying a premium, check which direction is optimized and for which carrier.

## Tokyo vs Hong Kong vs Singapore vs Osaka

| Location | Typical latency to mainland China | Best for |
| --- | --- | --- |
| Tokyo | ~50–90ms on optimized routes | Needing a Japan IP; mixed Japan/Korea/China audiences |
| Hong Kong | ~20–50ms | China-first traffic where a Japan IP is irrelevant |
| Singapore | ~70–80ms from Tokyo, higher to China | Southeast Asia coverage |
| Osaka | Slightly higher than Tokyo to China | Cheaper redundancy / failover in-country |

Tokyo's selling point is not that it wins on China latency — Hong Kong does, and costs more for it. It wins when you need a Japanese presence and a China-friendly route in the same box.

## DMIT's Japan lineup: what's actually on the menu

DMIT is a US-registered host (New York) that third-party write-ups consistently date to around 2017–2018, with a Chinese-speaking team and data centers in Los Angeles, Hong Kong and Tokyo. Independently of that background, the reason it shows up in Japan VPS discussions is bandwidth ownership: the company holds its own CN2 GIA, AS9929 and CMIN2 capacity rather than reselling someone else's transit, which is also the basis for its stated no-overselling position. Payments run through Alipay, WeChat Pay, PayPal and cards.

The Tokyo facility currently sells two network profiles. A third one is gone, and that matters for anyone following an older guide:

- **TYO.Pro (Premium)** — CN2 GIA return path, paired with AS9929/10099 (Unicom premium) and CMI (China Mobile). KVM virtualization, AMD EPYC 7003-series CPUs, 1Gbps port, 1 IPv4 plus a /64 IPv6 block. Traffic overage stops the service rather than throttling it. Test IP: 154.12.190.32.
- **TYO.T1 (Tier 1)** — international transit with no mainland China optimization. Reported routing is NTT both ways for China Telecom and China Unicom (with some paths detouring via Lumen in the US) and CMI for China Mobile. KVM, same CPU generation, 1 IPv4 plus /64 IPv6. Traffic overage throttles instead of cutting you off. Test IP: 154.31.112.5.
- **TYO.EB (Eyeball)** — delisted. Third-party trackers reported subscribers were notified the Tokyo Eyeball line would be retired on 15 June 2026. If you find a page or a coupon referencing it, treat it as dead stock.

That overage difference is not a footnote. On Pro, blowing through your monthly quota means the server goes dark until the cycle resets. On T1, you drop to a slower unmetered speed and keep serving. If your traffic is spiky or unpredictable, the cheaper line is sometimes the safer one.

## TYO.Pro plans and current pricing

Specs and price as listed across recent third-party listings. DMIT revises this price sheet periodically, so treat the checkout page as the authority.

| Plan | vCPU | RAM | SSD | Monthly traffic | Port | Price (USD) | Billing | Get it |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TYO.Pro.TINY | 1 | 1 GB | 20 GB | 500 GB | 1 Gbps | $21.90/mo | Monthly, quarterly, annual | [See TYO.Pro.TINY pricing](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.STARTER | 1 | 2 GB | 40 GB | 1 TB | 1 Gbps | $45.90/mo | Monthly, quarterly, annual | [Check the STARTER plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.MINI | 2 | 2 GB | 60 GB | 2 TB | 1 Gbps | $89.90/mo | Monthly, quarterly, annual | [View MINI configuration](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.MICRO | 4 | 4 GB | 80 GB | 4 TB | 1 Gbps | $189.90/mo | Monthly, quarterly, annual | [See MICRO specs](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.MEDIUM | 4 | 8 GB | 160 GB | 5 TB | 1 Gbps | $320.90/mo | Monthly, quarterly, annual | [Check MEDIUM availability](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.LARGE | 8 | 16 GB | 320 GB | 8 TB | 1 Gbps | $429.90/mo | Monthly, quarterly, annual | [View LARGE plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.GIANT | 8 | 24 GB | 640 GB | 15 TB | 1 Gbps | $799.90/mo | Monthly, quarterly, annual | [See GIANT configuration](https://www.dmit.io/aff.php?aff=12046) |

Two honest caveats, because pretending the price data is cleaner than it is would be worse than useless.

First, older write-ups published a lower sheet — STARTER at $39.90 with 500GB, MINI at $79.90 with 1TB, MICRO at $159.90 with 2TB, MEDIUM at $259.90 with 3TB. The pattern suggests DMIT raised the Pro traffic quotas and adjusted prices upward for tiers above TINY, with TINY unchanged at $21.90. Both numbers still circulate, and you should assume neither is guaranteed until you see it in the cart.

Second, TYO.Pro inventory is genuinely thin. Multiple sources describe the line as restocked in small batches as IPs free up, and specific tiers go out of stock for extended periods. If you're set on Pro, expect to check availability rather than assume.

## TYO.T1: the budget line, and where it stops making sense

| Plan | vCPU | RAM | SSD | Traffic (max) | Overage behaviour | Price (USD) | Billing | Get it |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TYO.T1.WEE | 1 | 1 GB | 20 GB | 1 TB | Throttled to 50 Mbps, unmetered | $36.90/yr | Annual only | [Grab T1.WEE at $36.90/year](https://www.dmit.io/aff.php?aff=12046) |
| TYO.T1.TINY | 1 | 1 GB | 20 GB | 2 TB | Throttled to 100 Mbps, unmetered | $6.90/mo | Monthly, quarterly, annual | [Check T1.TINY pricing](https://www.dmit.io/aff.php?aff=12046) |
| TYO.T1.STARTER | 1 | 2 GB | 40 GB | 4 TB | Throttled to 100 Mbps, unmetered | $12.90/mo | Monthly, quarterly, annual | [See T1.STARTER specs](https://www.dmit.io/aff.php?aff=12046) |
| TYO.T1.MINI | 2 | 2 GB | 60 GB | 8 TB | Throttled to 100 Mbps, unmetered | $21.90/mo | Monthly, quarterly, annual | [View T1.MINI plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.T1.MICRO | 4 | 4 GB | 80 GB | 16 TB | Throttled to 200 Mbps, unmetered | $32.90/mo | Monthly, quarterly, annual | [Check T1.MICRO availability](https://www.dmit.io/aff.php?aff=12046) |
| TYO.T1.MEDIUM | 4 | 8 GB | 160 GB | 32 TB | Throttled to 200 Mbps, unmetered | $49.90/mo | Monthly, quarterly, annual | [See T1.MEDIUM configuration](https://www.dmit.io/aff.php?aff=12046) |
| TYO.T1.LARGE | 8 | 16 GB | 320 GB | 64 TB | Throttled to 500 Mbps, unmetered | $99.90/mo | Monthly, quarterly, annual | [View T1.LARGE plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.T1.GIANT | 8 | 24 GB | 640 GB | 128 TB | Throttled to 1 Gbps, unmetered | $199.90/mo | Monthly, quarterly, annual | [Check T1.GIANT specs](https://www.dmit.io/aff.php?aff=12046) |

The T1 line is the easy recommendation for three groups: anyone serving Japanese or Southeast Asian users who never touch mainland China networks, anyone who needs a Japan IP for registration or catalogue reasons, and anyone building a relay or landing node where the box itself just needs to exist reliably.

It is the wrong purchase for one group: people who need fast, stable mainland China access. Not "slightly worse" — the routing has no China optimization at all, and no amount of RAM compensates. The T1.TINY at $6.90/month is a fine machine to see whether that's actually a problem for you, but if China latency is the whole point, skip the T1 table entirely.

## Reported discount codes

These come from third-party deal trackers and community write-ups rather than the official site, and they're tied to specific product lines and billing cycles. Test each one in the cart with the validate-code button — DMIT does not run the constant sitewide sales that some hosts do, and codes expire quietly.

| Code | Applies to | Discount | Notes |
| --- | --- | --- | --- |
| `202510_HKG_TYO_PRO_20OFF_RECURRING` | TYO/HKG Pro, quarterly or longer | 20% off | Recurring, applies on renewals too |
| `202510_HKG_TYO_T1_30OFF_RECURRING` | TYO/HKG T1, quarterly or longer | 30% off | Recurring; WEE excluded per listings |
| `2025-TYO-T1-HI-GSL-NON-MONTHLY-30OFF` | TYO T1, TINY and up, quarterly/annual | 30% off | Recurring |
| `2025-TYO-T1-HI-GSL-MONTHLY-10OFF` | TYO T1, TINY and up, monthly | 10% off | Monthly variant |
| `Special-Annual-50off-Replace-IP-Restricted-To-Once-Per-30-Days` | TYO.Pro, STARTER and up, annual | 50% off for 3 cycles | Reported as excluding TINY and carrying IP-replacement restrictions (once per 30 days, $5 fee) |

That last one is the one to read the terms on before you apply it. A half-price annual plan sounds great until you notice the IP policy attached to it, which matters a lot if you're buying for reasons that make IP cleanliness important.

For the Pro line, the practical takeaway is that quarterly or annual billing is where the discounts live. Monthly orders rarely qualify for anything meaningful.

## Test it yourself in ten minutes

Do this before you buy, regardless of provider. It's the single highest-value step in the whole process.

1. Run a ping and a traceroute from your own connection to DMIT's Tokyo test IPs — 154.12.190.32 for the Pro profile and 154.31.112.5 for Tier 1 — and note which route your traffic takes.
2. Repeat it at 9–11pm local time, which is when cheap transit falls apart. A route that looks fine at noon tells you nothing.
3. Check DMIT's public looking glass (lg.dmit.sh) to see the path from Tokyo to your city, not just the reverse direction.
4. Run the same tests against your current host, or against a cheap hourly-billed competitor, so you're comparing rather than just admiring numbers.
5. Take a one-month order before committing to an annual plan, especially on the T1 line.

If you want to skip ahead and test from a real instance, you can 👉 [start with a single month of DMIT Tokyo](https://www.dmit.io/aff.php?aff=12046) and upgrade later without re-deploying.

## Which plan for which buyer

| Your situation | Sensible pick |
| --- | --- |
| Personal project, Japanese or global audience, no China requirement | TYO.T1.TINY at $6.90/mo |
| Small Japanese-market site, predictable traffic | TYO.T1.STARTER or T1.MINI |
| Heavy traffic, unreliable volume, can tolerate slower speeds | T1.MEDIUM or T1.LARGE — throttling beats a suspended server |
| Serving mainland China visitors and Japan at once | TYO.Pro.TINY at $21.90/mo, verified with a real ping test first |
| Production business site needing China quality and headroom | TYO.Pro.STARTER or above, ideally on quarterly/annual billing with a code |
| Doing this on a tight budget | Neither line — a plain NTT-based Tokyo VPS costs less, if you don't need the routing |

The most common mistake here is buying Pro for a workload that doesn't need it, because "premium" reads like "better." If your visitors are in Tokyo and Frankfurt, CN2 GIA is expensive decoration. The second most common mistake is buying T1 for a site whose audience is in Chengdu, then wondering why it's slow at night.

## A note on stock, and buying

DMIT's Tokyo inventory is restocked in small batches, and the Pro tiers in particular sell out. Some buyers track stock via third-party monitors rather than refreshing the site. Register with a normal connection and accurate details — affiliate-driven signups through unusual IPs tend to trip fraud checks, and providers in this segment generally auto-refund suspicious orders rather than investigating them.

One location, two sensible products, one clear line between them: if you need mainland China to be fast, buy Pro and verify the route before you commit to a long billing cycle. If you don't, T1 does the job at a fraction of the price — and the overage throttling means a traffic spike costs you speed rather than downtime. Either way, run the ping test first. It costs nothing and it's the only thing that reliably tells you which side of that line your own connection lands on.

👉 [Compare current DMIT Tokyo plans and pricing](https://www.dmit.io/aff.php?aff=12046)
