# TradingView Teardown

Research brief, 29 September 2026. Prepared for Mason. What TradingView offers, what its new Technology Fee changes and what a Pine-compatible competitor has to ship first. Facts were checked against primary sources where they could be reached; estimates and unknowns are labeled. Not legal advice.

## Bottom line

- **Is the fee real?** Yes. It is Section 22A of TradingView's Terms of Use, word for word. Once a vendor passes 100 users every user is billed, so 101 users cost $3,024.95 a month. No effective date is published; the first count could be 30 September 2026.
- **Should we build a full TradingView clone?** No. TradingView has 21 chart types, 110+ drawing tools, 100+ brokers and 3.5M instruments. It claims 100M users and ships something new most weeks. Build the slice vendors and their customers need. Of the 147 features graded below, 53 are launch items.
- **Is there a market?** Likely, and the $5 share widens it. TradingView's fee only hits vendors over 100 users outside Paid Spaces. For them it takes 50% to 109% of revenue at most major vendors' published prices, and fewer than 5% of Paid Spaces applicants get in. The $5 per member also gives smaller vendors a reason to move. The catch is that their customers need a membership, while TradingView's free plan runs invite-only scripts at no charge. None of this is proven until vendors commit.
- **Are we first?** No. LuxAlgo, one of the biggest vendors, launched a Pine-native charting platform on 31 August 2026 and owns the leading open-source Pine engine. Our opening is neutrality: other vendors will not want to hand their code and customers to their largest competitor.
- **Can vendors' Pine code run outside TradingView?** Yes. PyneCore's published tests show it matching TradingView's output on 770 of 819 real scripts. No engine comes with a platform, though. Rendering, alerts, data and access control are ours to build.
- **Can we do it at a fraction of the cost?** For vendors, better than that. Hosting costs one membership and each member using their script earns them $5 a month, against TradingView's $29.95 per user. For traders, partly. One membership replaces TradingView's tiers, but at $14.99 it only beats Essential ($14.95 monthly, $12.95 annual) if it includes Plus and Premium features. CME futures and US stocks still carry exchange fees, so the best we can do there is match TradingView's $9.95 add-ons.
- **Can we call it Pine Script?** No. "PINE SCRIPT" is a registered US trademark of TradingView. We can say "compatible with Pine Script®" with a non-affiliation notice. Keep "Pine", "TV" and "TradingView" out of our name.
- **Can we test parity against TradingView?** Not until a lawyer signs off. TradingView's Terms ban "creating products or services based on TradingView content". In the closest precedent, a company that tuned its clone against the original's output under a restrictive license was hit with a $79.1M judgment.

## The fee, verified

The quote is real and word for word. It is Section 22A of TradingView's Terms of Use, headed "Technology Fee for invite-only indicators". TradingView also added "(g) any failure to pay a Technology Fee when due under Section 22A" to the termination grounds in Section 18.

> If you publish one or more invite-only scripts on TradingView, TradingView shall charge you a technology fee (the "Technology Fee") of US$29.95 per calendar month per user whose access to any invite-only script published by you is active at the end of that calendar month. The Technology Fee applies only where the total number of users with active access to your invite-only scripts exceeds 100 at the end of the relevant calendar month. TradingView may change the Technology Fee at any time on written notice to you.
>
> Source: TradingView Terms of Use, Section 22A (undated page, read 29 Sep 2026)

The rest of Section 22A adds the mechanics:

- **Counting.** Users are counted "as at the last day of each calendar month, based on its own records of access grants and script usage".
- **Billing.** An invoice arrives within 30 days of month end and is "payable within 14 days". TradingView "may collect payment ... by charging any payment method held on your account". The fee is non-refundable.
- **Non-payment.** TradingView may block new grants, revoke existing access, remove scripts, withdraw vendor privileges, terminate the account and "recover unpaid fees together with interest and costs".
- **Scope.** It "applies to all invite-only scripts and users, including existing scripts and existing vendors."

Three details matter more than the headline number:

1. **It is a cliff.** The 100-user figure is a trigger, not an allowance. At 100 users the bill is $0. At 101 users it is $3,024.95 a month, because all 101 users are billed.
2. **$29.95 is exactly TradingView's Plus plan price** (billed annually). In effect TradingView charges vendors a Plus subscription for every customer, including customers who already pay TradingView for Premium.
3. **Lifetime deals become liabilities.** A vendor who sold lifetime access now owes $359.40 a year for each of those customers, with no revenue to cover it.

### What nobody knows yet

- **Effective date: I don't know.** I found no announcement, blog post, FAQ or email. The Terms page carries no revision date, and Section 1 says changes apply once posted. The worst case is that the first count is 30 September 2026 (tomorrow), invoiced by about 30 October and due about 13 November. The Wayback Machine has copies of the Terms from 1 July, 1 August, 1 September and 20 September 2026 that would date the change. The archive is blocked from this environment, so someone needs to compare those copies by hand.
- **Whether Paid Spaces customers count: I don't know.** Section 22A has no carve-out, and TradingView's Vendor Requirements call Paid Space scripts "special invite-only scripts". As written they count. This single answer decides whether Paid Spaces is an escape hatch, so ask TradingView support in writing.
- **Whether free or trial grants count.** There is no carve-out, so assume yes.
- **Whether revoking access before month end avoids the count.** The count also uses "script usage" records, and the House Rules and Vendor Requirements forbid workarounds. Vendors who try to game the snapshot risk their accounts.

The Pine Script manual still says "TradingView does not benefit from script sales." The documentation has not caught up with the Terms, which suggests the clause is very recent.

### What the fee costs a vendor

At a $40 monthly price the fee takes 75% of revenue at any size above 100 users. At $30 it takes all of it.

| Customers with access at month end | Fee per month | Fee per year |
|---|---|---|
| 100 | $0 | $0 |
| 101 | $3,024.95 | $36,299 |
| 250 | $7,487.50 | $89,850 |
| 1,000 | $29,950 | $359,400 |
| 5,000 | $149,750 | $1,797,000 |
| 20,000 | $599,000 | $7,188,000 |

Under the model in this brief, the same 1,000-user vendor would pay one $14.99 membership and earn $5,000 a month from the revenue share.

## Paid Spaces, TradingView's storefront

The fee does not stand alone. TradingView has spent a year building its own storefront for paid scripts, and the fee pushes vendors toward it.

- **Timeline.** Paid Spaces launched on 13 November 2025. The Creator Program application hub opened on 12 August 2026 with 39 creators, and TradingView said "over 1,000 people have applied". On 29 September 2026 the marketplace listed 47 Paid Spaces priced from $4.99 to $199 a month.
- **Who is in.** AlgoAlpha ($65.57), ChartPrime Plus ($117), BigBeluga Premium ($66.47), Zeiierman ($95.20), DeMARK 9-13 ($29.99), Trendoscope ($69.99), LonesomeTheBlue ($49.99), loxx ($120) and Nison Candle Scanner ($199), among others. LuxAlgo and Market Cipher are not listed.
- **Fee.** The platform fee is "currently 0% per transaction", and TradingView "may change the platform fee, but only with advance notice". Only authors approved before 1 April 2026 keep 0% permanently. A Finance Magnates article (5 Aug 2026) described the 0% as lasting "until at least Oct. 1, 2026". That wording is not on the live terms page.
- **Gate.** It is invitation only. Authors need a Premium or Ultimate plan and a public invite-only script that was published more than 3 months ago and has 100+ boosts. Each author gets one Space holding up to 50 scripts (a help article says 25).
- **Billing.** Monthly subscriptions only, bought on the web only. TradingView is the merchant of record, adds VAT and offers a 7-day refund window, with refunds and chargebacks charged back to the author. Payouts are monthly, in USD, through PayPal only, after up to 30 days of settlement, with a $100 minimum.
- **Pitch.** "Skip the admin." TradingView handles billing, renewals, cancellations and access for the vendor.

### What this means for us

For vendors TradingView admits, the alternative to us is not "TradingView plus a $29.95 fee". It is "TradingView at a 0% platform fee, with billing handled and customers who never leave TradingView." We cannot beat 0% on price. The pitch to those vendors has to be ownership and control:

- TradingView owns the customer, the checkout and the payout rail. The vendor gets PayPal transfers.
- Monthly billing only. Vendors lose annual plans, lifetime deals, bundles with courses or Discord, coupons and their own trials.
- TradingView can change the fee with notice, and every author approved after 1 April 2026 has no grandfathering.
- TradingView decides who gets in and can remove anyone.

The better targets are vendors TradingView will not admit or who will not accept those terms: vendors over 100 users outside Paid Spaces, vendors carrying lifetime or annual customers, Discord and trading communities that give scripts to members and vendors who sell bundles.

The pattern is worth naming. In 2020 TradingView closed its first marketplace so vendors could sell "without a Marketplace in the way". It has now built a new one, put a fee on selling outside it and kept the right to change the fee inside it on notice. Plan for a non-zero Paid Spaces fee at some point; the terms already allow it.

## Who pays the fee

The fee only touches vendors with more than 100 active users who sell outside Paid Spaces (or inside it, if Paid Spaces is not exempt). That is a short list of large vendors plus a longer tail of mid-size ones. Nobody publishes a count of invite-only vendors. TradingView says it hosts 150,000+ community scripts, about half open source.

| Vendor | Cheapest published rate per user | Fee as share of that revenue | In Paid Spaces | User claim (vendor's own marketing) |
|---|---|---|---|---|
| BigBeluga | $27.36/mo billed yearly | 109% | Yes, $66.47/mo | 77,000 TradingView followers |
| LuxAlgo | $27.99/mo first-year promo | 107% | No, runs its own platform | "100,000+ traders" |
| AlgoAlpha | $28.72/mo billed yearly | 104% | Yes, $65.57/mo | "95k+ active traders" |
| Zeiierman | $37.99/mo billed yearly | 79% | Yes, $95.20/mo | "over 25,000 users" |
| ChartPrime | $40.75/mo billed yearly | 73% | Yes, $117/mo | "100K+ active users" |
| SMRT Algo | $41.42/mo billed yearly | 72% | No | "15,000+ traders" |
| Market Cipher | $50/mo on a 12-month plan | 60% | No | Not published |
| Flux Charts | $59.99/mo billed yearly | 50% | No | "20,000+ active traders" |
| QuantVue | $124.75/mo billed yearly | 24% | No | Not published |

These percentages assume the literal reading of Section 22A (every user billed once the count passes 100). User claims are marketing numbers. They include people who are not on TradingView invite-only access today.

What the numbers say:

- **At typical price points the fee takes most or all of the revenue.** Vendors will respond with price rises, dropped lifetime plans, pruned free grants, Paid Spaces applications and selling on several platforms at once.
- **Lifetime customers turn into a running cost.** At $359.40 a year each, a $1,399 BigBeluga lifetime sale or a $1,500 Market Cipher lifetime sale is used up in about four years.
- **Four of the biggest names are already inside Paid Spaces.** AlgoAlpha, ChartPrime, BigBeluga and Zeiierman sell there. Some also still sell on their own sites. How exposed they are depends on the unanswered Paid Spaces question.
- **Reaction: I don't know.** I found no public vendor reaction to the fee on vendor sites, blogs or YouTube. Reddit and X could not be reached from this environment, and the search quota ran out near the end. The next step is to ask vendors directly.

### How vendors sell today

- **Checkout:** Whop (2.7% + $0.30, with a TradingView username flow), Stripe (2.9% + 30 cents), Gumroad (10% + $0.50) and LaunchPass (Discord and Telegram only).
- **Access automation:** there is no official API. Tools such as Trendoscope's access manager and the TradingView-API project call TradingView's internal endpoints with the vendor's password, with two-factor authentication switched off. Trendoscope itself warns that TradingView "is tolerant on individual use" and could shut it down. An official access API with checkout integrations is the cheapest thing we can offer that TradingView does not.

### What their customers plug into

Customers wire alerts into bots, so our alerts must look like TradingView's to these services:

| Service | Users (claimed) | Payload it expects | Takes non-TradingView sources |
|---|---|---|---|
| TradersPost | 70,000+ | JSON: ticker, action, quantity, orderType, price, takeProfit, stopLoss | Yes, any JSON sender |
| PineConnector | 66,000+ | Comma-separated text, e.g. `60123456789,buy,EURUSD,vol_lots=0.5` | Not stated |
| PickMyTrade | 50,000+ | JSON | Not stated |
| 3Commas, WunderTrading, Alertatron | Not published | JSON or their own command formats | Yes |
| CrossTrade | Not published | Semicolon key=value pairs | Yes |

TradingView's webhook behavior to match: HTTP POST sent as `application/json` when the body is valid JSON and `text/plain` otherwise, ports 80 and 443 only, a 3-second timeout, four published source IP addresses, 2FA required, placeholders such as `{{ticker}}`, `{{close}}` and `{{strategy.order.action}}` and a throttle of 15 triggers per 3 minutes. Some receivers allowlist TradingView's IPs, so we must publish ours and get added.

## Who else is going after this

**LuxAlgo is the competitor that matters, and it is months ahead.**

- LuxAlgo is one of the biggest TradingView indicator vendors, with 1.4 million TradingView followers, 409 scripts and a claim of "100,000+ traders".
- On 1 June 2026 it acquired PineTS, the leading open-source Pine runtime.
- On 31 August 2026, 19 days after TradingView opened its Creator Program, it launched its own charting platform (QuantCharts). It runs Pine v5 and v6 natively, with US stocks from Cboe EDGX via Databento, real-time CME futures with 16 years of history and FX from FMP. There is a free tier; paid plans list at $39.99 to $119.99 a month.
- On 3 September it open-sourced the Vela chart engine (Apache-2.0). The bridge that runs Pine on Vela is AGPL-3.0.
- On 22 September it published a guide to running Pine outside TradingView.
- I found no third-party vendor marketplace on QuantCharts.

What that means for us:

1. **The thesis is validated.** Pine outside TradingView works well enough that the largest vendor bet its platform on it.
2. **We are not first.** Any pitch built on "the first Pine-compatible alternative" is false.
3. **LuxAlgo is every other vendor's largest competitor.** Few vendors will hand their source code and customer list to LuxAlgo. A neutral host that does not sell its own indicators is a position LuxAlgo cannot take.
4. **Building on PineTS means depending on that competitor.** The alternatives are AGPL obligations or a commercial license from LuxAlgo.

Other moves worth knowing:

| Company | What it did | Why it matters |
|---|---|---|
| OpenMarket | 16 charts per layout free (27 Sep 2026), own kScript language | Undercuts TradingView's $2,399/yr Ultimate on layouts. Not Pine. |
| cTrader | Subscriptions in its Store (28 Jul 2026), 30% commission | Openly courting paid-tool creators. |
| TakeProfit | Creators keep 80% to 100%; AI Pine-to-Indie converter "roughly nine in ten indicators" | Price attack plus conversion, but vendors must accept a new language. |
| TrendSpider | JavaScript scripting, store with 20% commission, Pine conversion program | Established, but conversion is a rewrite. |
| PyneSys / PyneCore | Pine-to-Python compiler ($8 to $45/mo); all 819 test scripts compile and run, 770 match TradingView and 99.717% of 99.9M plotted values are bit-identical (self-reported) | Evidence that high parity is achievable. Runtime is Apache-2.0. |
| PineForge | Pine v6 to C++ for backtesting, about 98% coverage claimed; marketplace planned for 2027 | Another engine in the race. |
| NinjaTrader | Ecosystem 2.0 moving to user-based "invite-only" licensing | Futures vendors have a mature alternative. |
| TopstepX | Embeds TradingView charts but "custom indicators are not available due to TradingView's commercial licensing terms" | Prop-firm traders cannot use paid indicators there. That is an open door. |

Marketplace commission norms: 20% (TrendSpider, MQL5, TakeProfit), 27% on Bookmap add-ons, 30% at cTrader. Paid Spaces charges 0% for now.

## Running Pine outside TradingView

It works, several teams have shown it and it is still the largest single thing we would build.

### What the engine has to reproduce

- **A moving target.** Pine v6 is current and changes almost every month. 2025 and 2026 added bid and ask, `request.footprint`, multiline strings, sorting of user-defined types, the `once` keyword and a strategy engine overhaul (July 2026).
- **Several versions at once.** In the largest published test corpus (819 popular public scripts), 298 are v4, 319 are v5 and 202 are v6. v6 changed behavior as well as syntax, so the engine needs per-version rules.
- **A big surface.** About 940 reference entries: 475 functions, 161 variables and 239 constants.
- **Unusual semantics.** Every function call site keeps its own state. The live bar rolls back and re-runs on every tick, and `varip` escapes the rollback. Higher-timeframe requests can leak future data under lookahead. The strategy engine simulates fills along documented intrabar price paths.

How often public v6 scripts on GitHub (about 12,736 files) use the hard parts:

| Feature | Share of scripts |
|---|---|
| `strategy.entry` | 27% |
| `request.security` | 25% |
| `table.new` | 24% |
| `label.new` | 22% |
| `line.new` | 17% |
| `box.new` | 11% |
| Library `import` | up to 5.6% |
| `request.security_lower_tf` | 1.6% |
| `varip` | 1.2% |
| `request.financial` | 0.3% |

Closed vendor scripts probably lean harder on drawings and multi-timeframe requests. That is unverified until we see real vendor code.

### Engines that exist today

| Engine | License | Evidence it matches TradingView | Share of vendor scripts likely to run unchanged and match |
|---|---|---|---|
| PyneCore + PyneComp (Python, PyneSys) | Runtime Apache-2.0. Compiler is a closed paid service. | 770 of 819 real scripts match; 99.717% of 99.9M plotted values are bit-identical; 296,924 strategy trades match. Almost all tests ran on one crypto market. | 75 to 90% |
| PineForge (C++, strategies only) | Engine Apache-2.0. Code generator is non-commercial without a deal. | 4,182 of 4,190 strategy tests rated "excellent" (self-reported). No plots, drawings or alerts. | Strategies 85 to 95%; indicators 0% |
| PineTS (TypeScript, owned by LuxAlgo) | AGPL-3.0 or a commercial license ($1,199 per developer a year or $20,000 a year) | No library imports; `varip` behaves like `var`; 3 of 11 request functions; 12 of 31 reference strategies match. | 50 to 75% |
| resin (TypeScript) | Apache-2.0 | 99.5% of 2,979 scripts run, but values were checked on only 91 cases. Seven weeks old and built by an autonomous AI agent loop against an unverified "sibling implementation". | 55 to 80% |
| piner (TypeScript, runs fractalchart.com) | AGPL-3.0 | Follows the manual closely but was never checked against TradingView output. | 40 to 70% |

The last column is a research estimate at low to moderate confidence, based on each project's published results. Treat it as a starting hypothesis for the bake-off, not a measurement.

### Recommendation

1. **Do not build on PineTS.** AGPL or a license from LuxAlgo puts our core in our main competitor's hands, and its parity evidence is the weakest of the serious engines.
2. **Fastest credible path: PyneCore plus a self-hosted PyneComp deal.** The runtime is Apache-2.0 and the published parity evidence is the strongest. Vendors will not accept their source passing through a third party's hosted compiler, so the deal must let us run the compiler ourselves. LuxAlgo bought PineTS. The equivalent move for us is a deal with PyneSys.
3. **Long term: own a deterministic core.** Build it in Rust or C++, compiled natively for servers and to WASM for browsers. JavaScript's math functions can return different results in different browsers; WASM arithmetic does not.
4. **Decide with data.** Benchmark PyneCore, PineTS under its commercial license and resin on 50 to 100 real vendor scripts supplied with the vendors' consent. Counsel must approve the testing method first. Budget two to four weeks.

**Parity is also a data problem.** A perfect engine gives different signals on different candles. Crypto and CME can match when we use the same venue. FX cannot match unless we carry the same broker feeds customers chart on TradingView (OANDA, FXCM, FOREX.com and others), because FX prices differ by broker.

### Legal lines (not legal advice; get counsel)

- **Re-implementing the language is defensible.** The EU Court of Justice held in SAS v World Programming (2012) that functionality and programming languages are not protected expression. The US Federal Circuit rejected SAS's copyright claim in 2023. Google v. Oracle (2021) found re-implementing an API fair use.
- **The exposure is contract.** World Programming ran programs through SAS's software and tuned its clone until the outputs matched, under a license that banned reverse engineering. That produced breach of contract and fraud liability, with $26.4M in damages trebled to a $79.1M judgment. TradingView's Terms ban copying its software or documentation "including ... creating derivative works", ban "creating products or services based on TradingView content" and ban commercial use of its services. Until counsel signs off, nobody on the team uses a TradingView account to generate reference output, bulk-download scripts or export data for testing.
- **Write everything from scratch.** Do not copy TradingView's manual text or built-in indicator code; write built-ins from public formulas. Two open engines (pinecone and piner) ship copies of TradingView's manual, so do not take code from them.
- **Check community licenses.** Most public scripts are MPL-2.0, which allows commercial use if modified files are published. LuxAlgo's public scripts are CC BY-NC-SA 4.0, which bans commercial use.
- **Re-check vendors' borrowed code.** TradingView makes vendors get permission to reuse someone else's code "in a paid script". That permission covered TradingView. Moving the script may need fresh consent.

### Architecture that follows

- Run closed-source scripts on our servers and stream plot and drawing descriptions to the browser. Open-source scripts can run in the browser.
- Sandbox every run with CPU, memory and loop limits at least as generous as TradingView's.
- Share computation. Run one engine instance per script version, input set, symbol and timeframe. Fan the results out to every subscriber. At PyneCore's median speed one core handles about 11,000 bar executions per second, so per-tick evaluation needs tick coalescing.
- Checkpoint engine state so a restart does not replay 5,000 to 40,000 bars.

## Market data sets the price floor

A platform that runs vendor scripts on its own servers cannot avoid exchange fees. They decide the lowest price we can charge in each market.

| Asset class | Launch route | Fixed cost per month | Cost per user per month | What to know |
|---|---|---|---|---|
| Crypto | Licensed aggregator such as CoinAPI (Streamer $249, Pro $599) | $249 to $599 | About $0 | Exchanges' free public APIs are not licensed for commercial display. Coinbase, OKX and Kraken require written consent. Binance's terms bar profiting from its data without consent (2021 wording; current text not verified). |
| Forex | Vendor with display rights: Twelve Data Venture (from $149) or TraderMade (£599) | $149 to about $1,100 | About $0 | Parity needs the broker feeds customers use on TradingView. OANDA's redisplay pricing is not published. |
| US stocks | Cboe One Summary feed | $5,000 distributor fee (offset by user fees, waived for 12 months for new vendors) plus $1,000 | $0.25 | Nasdaq Basic adds $2,140 a month plus $1.00 per user. The SIP becomes the CT Plan on 1 April 2027; agreements are due 1 March 2027. |
| CME futures, real time | CME distribution licenses | About $9,760 for all four exchanges ($29,280 a year each), up to about $12,200 with feed fees | $4.65 top of book, $36.50 with depth | CME and CBOT alone (ES, NQ, RTY, YM): $4,880 a month plus $3.10 per user. Non-display fees for server-side use start at $609 a month (classification unverified). |
| CME futures, delayed | CME delayed distribution | About $7,280 for all four | $0 | Not free for a distributor, unlike TradingView's free 10-minute delay. |

For comparison, TradingView charges traders $9.95 a month for the CME bundle and $9.95 for the US stock bundle (or $3 per exchange). Cboe One and 10-minute-delayed CME are free.

Three findings change the plan:

1. **Non-pro CME pricing may not be open to us.** CME's non-professional definition (2023 copies) requires "an active futures trading account" and a terminal "capable of routing orders to the CME Globex Platform". Sierra Chart enforces a funded futures account for non-pro CME data. TradingView's criteria do not mention either requirement, and I don't know whether CME gives TradingView an exception. Ask CME in writing before pricing futures.
2. **Bring-your-own-data does not fit this product.** Letting traders connect their own broker data avoids distributor licensing only when the data never touches our servers. Server-side scripts and alerts are the core of this product and put the data on our servers. Tradovate's API license also bans building "a competitive product or service" and bans AGPL code.
3. **Futures need scale before they pay.** At a $9.95 add-on and $4.65 per-user cost, about 1,840 paying futures users cover the base CME licenses. Feed and non-display fees raise that to about 2,420. Add CME when design-partner vendors can commit that many users.

Launch mix: crypto through a licensed aggregator, FX through a vendor with display rights, US stocks through Cboe One under the vendor waiver, then CME as a pass-through add-on priced like TradingView's.

## Chart engine

TradingView's own libraries are out. The free Advanced Charts license (June 2026) is "a free offering only" and limited to public sites. It also forbids using the library "to develop any competing offerings". Lightweight Charts is Apache-2.0 and usable. It has no built-in drawing tools or indicators, and its NOTICE requires a TradingView credit and link on our charts.

| Option | License and cost | What it gives us | Catch |
|---|---|---|---|
| KLineChart 10.0.3 | Apache-2.0, free | 28 indicators, 16 drawing overlays, about 40 KB | Performance at 100K+ bars untested |
| Vela (LuxAlgo) | Engine Apache-2.0; Pine bridge AGPL-3.0 | Released 3 Sep 2026 alongside LuxAlgo's Pine platform | Roadmap belongs to our main competitor. Fork the engine only, never the AGPL bridge. |
| Lightweight Charts 5.2.1 | Apache-2.0, free | Fast, multi-pane, 35 KB | Every drawing tool is ours to build. A TradingView credit and link must appear. |
| SciChart JS 6.0.1 | $1,349.66 a year per developer, up to 15,000 end users | WebGL speed | End-user cap. Drawing tools unverified. |
| Highcharts Stock 13.1.1 | $732 a seat (Core plus Stock); SaaS license covers 1 app | 40+ indicators and Stock Tools annotations | Per-app licensing |
| Our own renderer (Canvas or WebGL) | Engineering time | Exact control of Pine visuals | L to XL build |

Recommendation: prototype on KLineChart or a fork of Vela's Apache-2.0 engine, and plan to own the renderer. Pine's visual contract has to look like TradingView: label styles, table layout, text sizing, z-order, line extensions and the 500-object limits. Benchmark every candidate at 100K+ bars against that contract before committing.

## Live chart sessions

A host, whether a vendor or any member, opens a live room on their own chart. Invited members watch in real time as the host changes symbols and timeframes, draws, adds indicators and trades. Think of a weekly charting session or a room that trades the New York open. Nothing in the research shows TradingView offering this. Creators run these sessions today by screen-sharing on Discord, YouTube or Twitch.

How it should work:

- **Share chart state, never prices.** The room carries the host's symbol, timeframe, visible range, drawings, indicator settings and cursor. Each viewer's app loads prices itself under that viewer's own data license. That keeps us inside exchange rules and stops the host from redistributing data.
- **Every viewer needs the data for what is on screen.** If the host is on CME real-time and a viewer lacks the CME package, that pane locks with an offer to add it. Don't fall back to delayed data, because the host's drawings would not line up with a chart running 10 minutes behind.
- **Scripts keep their own access rules.** The host's own scripts show for everyone the host admits. Third-party invite-only scripts show only to viewers who have access to them, so no vendor's product leaks through someone else's room.
- **Follow the host or look around.** Viewers follow the host by default. They can scroll and switch timeframes on their own and jump back to the host's view with one click.
- **The host controls collaboration.** View-only or collaborative, for everyone or per viewer, changeable at any time. Viewer drawings are labeled with who made them, can be cleared in one action and never change the host's saved layout unless the host keeps them.
- **Room access uses the script access system.** Grants, expiry and Whop sync work the same way, so a creator can sell a live room like an indicator.
- **Trades at launch are markers.** The host's trade markers (entry, stop, target, exit) and position tools stream to viewers. Real broker positions need broker integrations, which come later and carry license limits; Tradovate's API license bans competitive products.
- **Script output is computed once.** Server-side results are shared across every viewer of the same script version, inputs, symbol and timeframe. It is the same shared computation that powers alerts.
- **Plan for the opening bell.** Thousands of viewers can join the same room in the same minute at the New York open. Late joiners get a snapshot, then the live stream.

Viewers need a membership to join invite-only rooms, plus the data packages for whatever the host shows. Every popular futures room sells CME packages.

## Feature inventory and grades

Every TradingView feature the research found, graded for a vendor-first competitor. 147 features: 53 P0 Launch, 36 P1 Fast follow, 33 P2 Later, 19 P3 Park and 6 Skip. The launch list looks long because the Pine runtime alone accounts for 17 items. Most of the rest are small.

- **P0 Launch:** vendors cannot migrate, or their customers cannot use the scripts, without it. Ships in the first release.
- **P1 Fast follow:** customers churn back to TradingView within weeks without it. Target the first 90 days after launch.
- **P2 Later:** real value, but not a switching reason. Build once the vendor base is paying.
- **P3 Park:** low value for this audience or very expensive, usually because of data licensing. Link out or revisit in year two.
- **Skip:** do not build. Wrong business, legal exposure or a cost sink with no switching value.

Effort: S is under 2 engineer-weeks, M is 2 to 6, L is 6 to 16 and XL is more than 16. These are planning estimates. "For" names who the feature serves: Vendor (script sellers), Trader (their customers), Both or Us (internal).

### Pine runtime

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Pine v6 language core | P0 Launch | XL | Vendor | v6 is current (late 2024) and gets additions almost monthly: bid and ask, request.footprint, multiline strings, sorting of user-defined types, the once keyword. | This is the product. Vendors port only if their code compiles and behaves the same with no rewrite. |
| Pine v5 compatibility | P0 Launch | M | Vendor | v5 scripts keep running; a v6 converter is built into the editor. v6 changed behavior, not just syntax. | 319 of 819 popular public scripts in the largest published test corpus are v5. Vendors will not rewrite during a move. |
| Execution model parity | P0 Launch | XL | Us | Per-call-site state, history operator, var and varip, live-bar rollback on every tick, history buffers sized from the first 244 bars. | Signals must match bar for bar, including how they repaint live. Every mismatch becomes a support ticket from every customer. |
| Built-in function library | P0 Launch | L | Vendor | About 940 reference entries: 475 functions, 161 variables and 239 constants across ta, math, str, array, map, matrix and more. | Every script depends on them. Engines diverge on seeding, na handling and number formatting, so each needs its own tests. |
| request.security | P0 Launch | L | Vendor | Other symbols and timeframes with lookahead and gaps options; dynamic requests in v6; 40 unique calls (64 on Ultimate). | Used in 25% of public v6 scripts. Lookahead and confirmation rules decide whether signals repaint. |
| Plots and chart styling | P0 Launch | L | Vendor | Up to 64 plot counts per script: plot, plotshape, plotchar, plotarrow, plotcandle, plotbar, hline, fill, bgcolor, barcolor. | What customers look at. Styles, colors, offsets and display flags must render identically. |
| Drawing objects from code | P0 Launch | L | Vendor | Up to 500 lines, boxes and labels, 100 polylines and 9 tables per script, from 10,000 bars back to 500 bars forward. | Tables appear in 24% of public v6 scripts, labels 22%, lines 17%, boxes 11%. Smart-money products are mostly drawings. |
| Script inputs and settings dialog | P0 Launch | M | Both | 13 input types with groups, inline rows, tooltips, active flags and confirm (click on chart to pick a value). | Customers use the settings every day, and vendors write their docs around them. |
| Alert functions in code | P0 Launch | M | Vendor | alert() once per bar, at bar close or on every call; alertcondition() in indicators. | For many customers the alert is what they pay for. The runtime half of the alert service. |
| Strategy engine | P0 Launch | XL | Vendor | Broker emulator with market, limit, stop and stop-limit orders, pyramiding, OCA groups, commission, slippage and margin calls; overhauled Jul 2026. | 27% of public v6 scripts call strategy.entry, and bots automate from strategy fills. Fills must follow TradingView's documented intrabar path rules. |
| Libraries | P0 Launch | M | Vendor | Libraries export functions, types, methods and constants; always open source; up to 1M tokens of imports. | About 5% of public scripts import libraries and fail outright without them. Get library source from vendors or authors, never by scraping. |
| Pine editor | P0 Launch | M | Vendor | Side-panel cloud editor with autocomplete, command palette, version history and error messages. | Vendors must paste, compile and fix code on day one. Basic is enough at launch. |
| Execution limits and sandbox | P0 Launch | M | Us | 20 s run time on Basic, 40 s on paid plans, 100 s on Ultimate; 500 ms per loop per bar; 2-minute compile; 100K-element collections. | Multi-tenant safety. Limits must be at least as generous as TradingView's or real scripts fail. |
| Keeping pace with Pine releases | P0 Launch | M | Us | Language changes ship nearly every month. | Ongoing cost, not a one-off. Vendors adopt new features and every gap breaks a port. |
| Compatibility checker | P0 Launch | M | Vendor | Nothing comparable; TradingView is the only place Pine runs natively. | Upload source, get a report of anything unsupported. The first thing a vendor does with us, and it sets their confidence. |
| Parity test suite | P0 Launch | L | Us | Nothing comparable. | Independent expected outputs for every built-in and semantic rule. Must not come from automating TradingView (see legal). |
| Server-side execution of closed source | P0 Launch | L | Vendor | TradingView runs scripts on its servers; invite-only source never reaches the browser. | Vendors will not hand over code that customers could extract. Transpiling to JavaScript or WASM obscures but does not protect. |
| Pine v4 and older | P1 Fast follow | M | Vendor | Older versions still run; converters exist. | 298 of those 819 scripts are still v4. Some vendors will up-convert first, many will not. Support within 90 days. |
| request.security_lower_tf | P1 Fast follow | M | Vendor | Intrabar data arrays from lower timeframes, 100K to 200K intrabars by plan. | Only 1.6% of public v6 scripts use it, but volume-delta style tools depend on it. |
| Indicator-on-indicator sources | P1 Fast follow | M | Trader | input.source can read another script's plot; limits of 1 on Basic up to 49 on Ultimate. | Common when customers stack a vendor's tools. Not needed for a single script to work. |
| Pine Logs | P1 Fast follow | S | Vendor | log.info, log.warning and log.error output panel. | Cheap, and vendors need it to debug ports. |
| Pine Profiler | P2 Later | M | Vendor | Per-line execution time profiling. | Helps heavy scripts. Not a switching reason. |
| Fundamental and event requests | P3 Park | M | Vendor | request.financial (FactSet), request.earnings, request.dividends, request.splits, request.economic. | 0.3% of public v6 scripts. Needs a fundamentals license, and output can never match TradingView's FactSet numbers exactly. |
| request.footprint | P3 Park | L | Vendor | Volume footprint data in Pine since Jan 2026, Premium and Ultimate only, one call per script. | Needs tick data and a footprint pipeline. Too new for vendor catalogs to depend on. |
| Deprecated data requests | Skip | - | Vendor | request.seed (Pine Seeds) accepts no new repos; request.quandl is legacy. | Commercial scripts should not depend on them. |

### Vendor tools

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Access grants and expiry | P0 Launch | M | Vendor | Manual username entry in a Manage access dialog with optional expiry dates. Premium plan ($59.95/mo) or higher to publish invite-only. | The core job vendors hire us for. Must handle thousands of users per vendor. |
| Public access API | P0 Launch | M | Vendor | No official API. Vendors run unofficial bots on internal endpoints with their password and two-factor authentication switched off. | The foundation every billing integration plugs into. Fixes TradingView's worst vendor pain point. |
| Whop sync | P0 Launch | M | Vendor | Whop's TradingView app has buyers enter a TradingView username to claim access. | Most vendors already sell on Whop. Grant access on purchase and remove it when the vendor subscription ends, which also stops the $5 share. Linking each purchase to a platform account is the hard part. |
| Revenue share tracking | P0 Launch | M | Vendor | None. TradingView charges vendors $29.95 per user once they pass 100 users. | $5 a month per active member who still has access to the vendor's script. One payout per member per month, credited to the referring vendor or split. Vendors need referral links and a statement they can check. |
| Customer migration kit | P0 Launch | S | Vendor | Nothing comparable. | Bulk import of customer lists, invite links and onboarding emails. Switching friction is the biggest risk to the plan. |
| Source code custody | P0 Launch | M | Vendor | TradingView holds invite-only source privately. | Encryption at rest, audit logs, no routine staff access. One leak ends vendor trust. |
| Script versioning and updates | P0 Launch | S | Vendor | Vendors publish updates with release notes; public scripts are editable for only 15 minutes after publishing. | Vendors ship fixes weekly. Add staged rollout and rollback, which TradingView lacks. |
| Third-party code consent check | P0 Launch | S | Us | Vendor Requirements demand explicit permission to reuse others' code in a paid script. | That permission was given for TradingView. Porting may need fresh consent from the original authors. |
| Vendor vetting and conduct rules | P0 Launch | M | Us | Vendor Requirements, moderator review, House Rules and bans; script pre-moderation since 14 Aug 2026. | Free hosting and a $5 share attract everyone, including vendors TradingView rejected. Vetting protects customers and the payout pool. |
| Vendor payouts | P1 Fast follow | M | Vendor | Paid Spaces pays monthly through PayPal in USD after up to 30 days of settlement, with a $100 minimum and W-9 or W-8 forms at $600. | Tax forms, a minimum payout, a holding period and clawbacks on refunds and chargebacks. First payouts fall due after the hold, so this can trail launch by weeks. |
| Checkout sync beyond Whop | P1 Fast follow | S | Vendor | None official. | Stripe, LaunchPass and Gumroad on the same access API, so vendors are not forced onto Whop. |
| Vendor analytics | P1 Fast follow | M | Vendor | A list of users with access. No usage analytics. | Active users, retention and usage per script are easy wins. |
| Discord and Telegram role sync | P1 Fast follow | S | Vendor | None. Vendors link accounts through third-party bots. | Most vendors run their community on Discord. Access tied to roles removes manual admin. |
| Native checkout for vendor sales | P2 Later | L | Vendor | Paid Spaces only: monthly plans, web purchase, TradingView as merchant of record, PayPal payouts in USD, 0% fee for now. | Vendors keep selling on Whop and similar tools. Build it only if vendors ask. |
| Marketplace and discovery | P2 Later | M | Both | Paid Spaces marketplace: 47 spaces on 29 Sep 2026, $4.99 to $199 a month, admission under 5% of applicants. | Vendors bring their own customers first. Discovery matters once there is a trader base. |
| Open and protected publishing | P2 Later | M | Both | 150,000+ community scripts, about half open source; publishing capped at 5 public scripts a day and 15 a month since Aug 2026. | Builds an ecosystem over time. Not why paid vendors switch. |
| Team seats for vendors | P2 Later | S | Vendor | One account per vendor profile. | Larger vendors have staff for access and support. |

### Chart types

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Candles, bars, line, area and Heikin Ashi | P0 Launch | M | Trader | Part of 21 chart types. | Table stakes. Heikin Ashi is widely used alongside paid scripts. |
| Other standard styles | P1 Fast follow | S | Trader | Hollow candles, baseline, columns, high-low, HLC area, step line, line with markers. | Cheap once the renderer exists. |
| Range bars | P1 Fast follow | M | Trader | Custom range bars from Essential. | Popular with futures traders, a core buyer group. |
| Seconds intervals | P1 Fast follow | M | Trader | 1 to 45 seconds, Premium ($59.95/mo) and Ultimate only. | Futures scalpers want them and TradingView charts $59.95 a month. Offering them on a cheap tier is a direct poach. |
| Custom intervals | P1 Fast follow | S | Trader | Any count of seconds, minutes, hours, days, weeks or months, from Essential. | Many scripts are tuned to odd timeframes such as 3m or 45m. |
| Renko, Kagi, Point and Figure, Line Break | P2 Later | M | Trader | Available on all plans; intraday versions from Plus. | Niche, and scripts behave differently on synthetic bars, which adds parity work. |
| Volume footprint, TPO and volume candles | P2 Later | L | Trader | Premium and Ultimate only, with alerts on footprint and TPO levels. | Needs tick data and a new renderer. Order-flow traders already use ATAS or Bookmap. |
| Tick intervals | P2 Later | L | Trader | 1, 10, 100 and 1,000 ticks on nearly all exchanges since May 2025; Ultimate only ($199.95/mo). | Needs full tick history and storage. Seconds first. |

### Chart data

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Standard intervals and history depth | P0 Launch | M | Trader | 1 minute to 1 month; 5K intraday bars on Basic, 10K Essential and Plus, 20K Premium, 40K Ultimate. | Scripts need warm-up history. 20K bars on a free account beats every TradingView tier below Premium. |
| Symbol search | P0 Launch | M | Trader | Search across 3.5M instruments from hundreds of feeds. | Fast and forgiving search over a clean symbol master per data source. |
| Timezones, sessions and extended hours | P0 Launch | S | Both | Chart timezone, regular and extended sessions on all plans, 24h overnight session for some US stocks since Jul 2026. | Pine time functions depend on sessions. Wrong sessions mean wrong signals. |
| Continuous futures and rolls | P1 Fast follow | M | Trader | Continuous contracts with optional back-adjustment. | Needed the day futures data ships, and must match TradingView's roll rules for parity. |
| Compare and overlay symbols | P2 Later | S | Trader | Overlay symbols in percent or price, all plans. | Nice to have. |
| Spread and ratio charts | P2 Later | M | Trader | Custom formulas across symbols; intraday from Plus. | Pairs traders use them. Low priority. |

### Drawing tools

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Core drawing set | P0 Launch | L | Trader | Trend line, ray, horizontal and vertical lines, rectangle, channel, Fibonacci retracement and extension, text, arrows, measure, long and short position tools. | Every trader marks levels next to the paid script. The position tool gets used constantly. |
| Drawing ergonomics | P1 Fast follow | M | Trader | Magnets (including snap to indicators), templates, lock and hide, object tree, favorites toolbar. | Missing ergonomics feel broken to TradingView users even when the tools exist. |
| Drawings synced across layouts and timeframes | P1 Fast follow | M | Trader | Drawings sync across charts of the same symbol. | Expected by multi-timeframe traders. |
| Alerts on drawings | P1 Fast follow | M | Trader | Alerts on trend lines, rectangles, Fibonacci and position drawings. | Common workflow that reuses the alert service. |
| Full drawing library | P2 Later | L | Trader | 110+ tools in 8 groups including pitchforks, Gann, harmonic patterns, Elliott waves, cycles, brushes, icons and embedded posts. | Long tail. Add the most requested ones after launch. |

### Indicators

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Top 30 built-in indicators | P0 Launch | M | Trader | 400+ built-ins claimed (Help Center documents 209 indicators and 20 strategies). | Write them in Pine on our engine from public formulas, not TradingView's source. Doubles as runtime testing. |
| Volume profile tools | P1 Fast follow | M | Trader | 7 volume profile indicators (fixed range, anchored, session, visible range, periodic) from Essential. | Heavily used by futures traders. Needs lower-timeframe data. |
| Rest of the built-in library | P2 Later | M | Trader | The remaining built-in indicators and strategies. | Long tail. Community scripts fill it. |
| Pattern recognition | P2 Later | M | Trader | 44 candlestick patterns on all plans; 16 auto chart patterns on Premium and up; auto Fibonacci. | Good for marketing, rarely decisive for this audience. |
| Seasonals | P3 Park | S | Trader | Seasonality charts since Jan 2025. | Low demand among script buyers. |

### Chart workspace

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Chart renderer | P0 Launch | XL | Us | Proprietary renderer. The free Advanced Charts library license forbids competing products. | Pine drawings, labels, tables and z-order must look like TradingView. Prototype on an Apache-2.0 library, then own the renderer. |
| Saved layouts | P0 Launch | M | Trader | 1 layout on Basic, 5 Essential, 10 Plus, unlimited Premium and up. | Losing a setup on refresh is unacceptable. |
| Indicators per chart | P0 Launch | S | Trader | 2 on Basic, 5 Essential, 10 Plus, 25 Premium, 50 Ultimate. | A packaging choice, not a build. Cap it on the free tier and keep it generous for members; vendor bundles often need 3 to 5 scripts. |
| Themes and chart colors | P0 Launch | S | Trader | Light and dark themes with full color control. | Cheap and expected. |
| Multi-chart layouts | P1 Fast follow | M | Trader | 1, 2, 4, 8 or 16 charts per tab by plan. | Start at 4, then 8. OpenMarket gives 16 free since 27 Sep 2026, so this is table stakes for a challenger. |
| Symbol, interval, crosshair and time sync | P1 Fast follow | M | Trader | Sync across charts and across desktop windows with tab linking. | Multi-timeframe analysis depends on it. |
| Templates | P1 Fast follow | S | Trader | Chart templates and indicator templates. | Vendors ship recommended templates with their products. |
| Price scale options | P1 Fast follow | S | Trader | Auto, log, percent, indexed to 100, inverted, manual. | Log scale matters for crypto. |
| Hotkeys, undo and redo | P1 Fast follow | S | Trader | Extensive keyboard shortcuts and a command search. | Match common TradingView shortcuts so muscle memory carries over. |
| Data window and object tree | P1 Fast follow | S | Both | Per-bar plot values (floating under the cursor since Jun 2025) and a tree of chart objects. | Vendors use the data window to support customers. |
| Screenshots and share links | P1 Fast follow | S | Both | Snapshots and shareable layouts. | Free marketing when customers share charts. |
| Table views | P2 Later | S | Trader | Chart data as a table (Sep 2025); Pine tables docked below the chart (Sep 2026). | Useful for dashboard-style scripts. Not urgent. |
| Export chart data | P3 Park | S | Trader | CSV export from Plus. | Vendors may want exports switched off for their plots to limit reverse engineering. |

### Live sessions

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Live chart sessions | P0 Launch | L | Both | No live co-viewing found in the research. Layouts can be shared as links and snapshots; creators stream by screen-sharing on Discord, YouTube or Twitch. | Creators already run weekly sessions and New York open rooms over screen-shares. A native room shows the real chart, lets viewers look around and keeps every viewer inside their own data license. |
| Room access and host controls | P0 Launch | M | Both | None. | Rooms use the same access system as scripts, including Whop sync. The host can switch collaboration on or off at any time for everyone or per viewer. The host can also mute or remove viewers and clear their drawings. |
| Viewer data and script checks | P0 Launch | M | Us | Not applicable. Each TradingView account buys its own data add-ons. | Each viewer loads prices under their own license and the room never relays the host's data. Without the needed package the pane locks with an offer to add it. Third-party invite-only scripts show only to viewers with access. |
| Trades in live sessions | P0 Launch | M | Both | Trading panel and paper trading for your own account; no live broadcast of trades found. | At launch the host's trade markers and position tools stream live. Real broker positions need broker integrations, which come later. |
| Session chat | P1 Fast follow | S | Trader | Private chats relaunched Aug 2026; public chats retired 30 Sep 2026. | Viewers ask questions during the session. A small build on the room's channel. |
| Host voice and video | P2 Later | L | Both | Live video Streams appear discontinued (not verified). | Real-time audio and video is its own infrastructure. Hosts keep Discord or YouTube for voice at launch, linked from the room. |
| Session recordings | P2 Later | M | Both | None found. | Sessions are small event logs, so replays are cheap to store. Replays need historical data rights for each viewer. |

### Alerts

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Server-side script alerts | P0 Launch | L | Both | Technical alerts: 0 on Basic, 20 Essential, 100 Plus, 400 Premium, 1,000 Ultimate. Alerts expire after 1 to 2 months below Premium. | For many customers the alert is the product. No expiry and generous counts beat TradingView's limits outright. |
| Price alerts | P0 Launch | S | Trader | 3 on Basic up to 1,000 on Ultimate; 13 built-in conditions. | Table stakes. |
| Webhooks compatible with TradingView | P0 Launch | M | Trader | From Essential. POST as JSON or plain text, ports 80 and 443, 3-second timeout, 4 fixed source IPs, 2FA required, placeholders such as {{ticker}} and {{strategy.order.action}}, throttle of 15 triggers in 3 minutes. | TradersPost, PineConnector and PickMyTrade parse this format. Matching it keeps customers' automation working with no changes. |
| Email, Telegram and Discord delivery | P0 Launch | S | Trader | App push, popup, email, webhook, sound and plain-text email. No Discord delivery found. | Vendors' communities live on Telegram and Discord. Cheap to build. |
| Shared computation for alerts | P0 Launch | M | Us | Not applicable. | Run each script version, input set, symbol and timeframe once and fan out to every subscriber. This is how alerts get cheap enough to price far below TradingView. |
| Mobile push | P1 Fast follow | M | Trader | Native push through the iOS and Android apps. | Web push from a PWA covers most of it before native apps. |
| Alert log | P1 Fast follow | S | Trader | History of triggered alerts. | Needed for support and for trust in signals. |
| Multi-condition and watchlist alerts | P2 Later | M | Trader | Multi-condition (up to 5 conditions) from Plus; watchlist alerts: 2 on Premium, 15 on Ultimate. | Power-user features. Watchlist alerts are expensive to compute. |
| Alert schedules and presets | P2 Later | S | Trader | Notification schedules (Jul 2026) and up to 5 presets. | Quality of life. |
| Alerts on news, fundamentals and patterns | P3 Park | M | Trader | Alerts on news flows, financial and valuation metrics, chart patterns, TPO and footprint. | Depends on data we will not carry early. |

### Backtesting

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Strategy report | P1 Fast follow | L | Both | Renamed from Strategy Tester in Jul 2026: metrics, trades, equity; CSV and XLSX export from Essential. | Follows the strategy engine. Vendors sell backtests as proof. |
| Bar Replay | P1 Fast follow | M | Trader | Daily data on all plans; minute data for 180 days on Essential, 365 on Plus, all on Premium; seconds on Premium; 7 days of ticks on Ultimate. | Popular for practice and vendor demos. Needs stored intraday history. |
| Deep Backtesting and bar detalization | P2 Later | M | Vendor | Premium and up: any date range, up to 2M bars; intrabar fills from lower timeframes (formerly Bar Magnifier). | Valued by strategy vendors. Builds on the strategy engine. |
| Parameter optimization | P2 Later | L | Vendor | No native input optimizer. | A real gap in TradingView and a good differentiator once the engine is solid. |
| Replay trading | P2 Later | M | Trader | Paper trades during Bar Replay. | Practice feature. Not a switching reason. |

### Market data

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Crypto spot and perpetuals | P0 Launch | M | Trader | 50+ crypto exchanges and DEX venues, real-time free. | Biggest share of script buyers and cheap per user, but exchanges' free APIs are not licensed for commercial display. Use a licensed aggregator (CoinAPI from $249/mo) with venue-level candles so they match TradingView. |
| Forex | P0 Launch | M | Trader | Broker FX and CFD feeds (OANDA, FXCM, FOREX.com and others), real-time free. | Core audience for smart-money products. FX prices differ by broker, so parity needs the feeds customers use on TradingView. Vendors with display rights start around $149/mo. |
| Data parity with TradingView | P0 Launch | L | Us | Candles depend on the source, session rules, adjustments and futures rolls. | A perfect engine still gives different signals on different candles. Match TradingView's source and rules per symbol. |
| US index futures | P1 Fast follow | L | Trader | CME Group delayed 10 minutes by default; real-time bundle $9.95 a month non-pro. | Core buyer group, but real-time distribution costs about $9,760/mo in fixed CME licenses plus $4.65 per user. Non-pro rates may also require a futures account. Pilot with crypto and FX vendors; add CME when committed demand covers it. |
| US stocks | P1 Fast follow | L | Trader | Cboe One real-time free; NYSE, Nasdaq and Arca $3 each or a $9.95 bundle non-pro. | Cboe One Summary costs $0.25 per user with a 12-month distributor-fee waiver for new vendors. Cheap enough to follow right after launch. |
| Indices | P2 Later | M | Trader | S&P DJI indices $10 a month non-pro; Cboe Global Indices $9.95. | Separate licenses. Use futures or ETFs as proxies first. |
| Bring-your-own broker data | P3 Park | M | Trader | Broker verification only waives TradingView's own data charge; TradingView still streams from its licensed feed. | Avoids exchange licensing only if data never touches our servers, which rules out server-side scripts and alerts. Tradovate's API license also bans competitive products and AGPL code. |
| Free delayed futures quotes | P3 Park | S | Trader | CME data free with a 10-minute delay on every plan. | Delayed distribution still costs $21,840 a year per exchange, so keep futures off the free tier. |
| International stocks and futures | P3 Park | XL | Trader | 100+ stock and futures exchanges; most delayed 15 minutes, paid add-ons per exchange. | Expensive long tail. |
| Bonds, economic data and options data | P3 Park | L | Trader | Government and corporate bonds, 300 to 400+ economic metrics, OPRA, CME and Eurex options. | Little overlap with script buyers. |

### Screeners

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Pine Screener | P2 Later | L | Both | Beta, Premium and up: one script across up to 4,000 symbols on 10 fixed timeframes, last 500 bars; invite-only scripts allowed since Aug 2026. | Strong fit for vendor scripts: scan 50 pairs for today's signals. Build once alerts scale. |
| Crypto screener | P2 Later | M | Trader | Coin, CEX pair (40+ exchanges) and DEX pair screeners. | Cheap on data we already carry. |
| Stock, ETF, bond and forex screeners | P3 Park | L | Trader | 7 screeners in total with 400 to 500+ fields; AI Screener (Aug 2026) on paid plans. | Needs fundamentals licensing. Finviz and TradingView already do this well. |
| Heatmaps and market overview | P3 Park | M | Trader | Stock, ETF and crypto heatmaps, forex and bond heatmaps, yield curves, Macro Maps, market pages. | Marketing surface more than a daily tool for this audience. |

### Research and news

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Economic calendar | P2 Later | S | Trader | Global economic events with forecasts and actuals, plus chart event markers. | Futures and FX traders avoid trading into CPI or payrolls. License a feed or embed a provider. |
| News feed | P3 Park | L | Trader | News Flow from 65+ providers with AI summaries of filings. | Expensive licensing and low differentiation. |
| Earnings, dividends and IPO calendars | P3 Park | M | Trader | Corporate event calendars. | Stock-only and needs a data license. |
| Fundamentals and ratings | P3 Park | L | Trader | Statements, 100+ metrics, Fundamental Graphs, analyst estimates, Fitch and Moody's ratings, Quartr documents with AI summaries. | Different customer. Link out. |
| Options tools | Skip | - | Trader | Chains with greeks, strategy builder, volatility curves, options volume profile. | Different product and expensive OPRA data. |

### Trading

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Prop-firm distribution | P1 Fast follow | M | Both | Brokers sponsor free TradingView plans. TopstepX embeds TradingView charts but cannot load custom or purchased indicators. | Prop-firm traders are a big buyer group that TradingView's own license locks out of paid scripts on TopstepX. |
| Broker integrations | P2 Later | XL | Trader | 100+ brokers (33 visible to US visitors) including NinjaTrader, Tradovate, Interactive Brokers, TradeStation, OANDA, Kraken and Coinbase. | Buyers already automate through webhooks. Add a few high-demand brokers later, prop-firm futures platforms first. |
| Native auto-trading from alerts | P2 Later | L | Trader | None. TradingView says it is 'considering' it with 'no ETA'; users route webhooks to third parties. | A real gap, but it brings broker certification, liability and regulatory questions. Partner with TradersPost-style services first. |
| Paper trading | P2 Later | M | Trader | Multi-asset simulated accounts with custom balance, commission and leverage. | Useful for trials of vendor strategies. |
| Depth of market and chart trading | P3 Park | L | Trader | DOM with Tier-2 brokers; order entry, brackets and drag-to-modify on the chart. | Only matters once broker trading exists. |

### Watchlists

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Watchlists | P0 Launch | M | Trader | Basic: 1 list of 30 symbols. Paid: unlimited lists of 1,000 symbols with sections, 7 flag colors and custom columns. | Basic lists at launch; columns and flags follow. |
| Import TradingView watchlists | P0 Launch | S | Trader | Paid plans export watchlists as .txt files; Basic cannot export. | Removes a switching cost in one click. Also accept pasted symbol lists for free users. |
| Portfolios | P3 Park | M | Trader | Portfolio tracking since Jun 2025 with benchmarks, dividends and share links. | Different job. |

### Community

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Vendor announcements | P1 Fast follow | S | Vendor | Release notes on script pages. | In-app notices to a vendor's own customers, which TradingView's link rules restrict. |
| Reviews and ratings | P2 Later | M | Both | Boosts and comments; comments need phone verification. | Trust signals for a future marketplace. |
| Ideas and Minds | Skip | - | Trader | Published chart ideas, video ideas and per-symbol short posts; about 5,300 publications a day. | A social network needs moderation at scale and is not why anyone switches. |
| Chats | Skip | - | Trader | One-to-one and private group chats relaunched Aug 2026; public chats retired 30 Sep 2026; Streams appear discontinued. | Vendors already run their communities on Discord. |
| Trading contests | Skip | - | Trader | Community contests (Aug 2026) and The Leap real-money contests. | Marketing program, not a switching reason. |

### Apps

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Web app | P0 Launch | XL | Both | Full platform on the web. | Where everything starts. Desktop browsers first. |
| Mobile web and PWA | P1 Fast follow | M | Trader | Native apps: iOS 4.8 stars from 414K ratings, Android 50M+ downloads, 19 languages. | Customers check signals on their phones. A responsive web app with push covers launch. |
| Native mobile apps | P2 Later | XL | Trader | Native iOS and Android apps with home-screen widgets. | Expensive. Build once retention proves out. |
| Desktop app | P3 Park | S | Trader | Windows, macOS and Linux (v3.4.1, Sep 2026) with native multi-monitor. | A wrapper around the web app is enough when asked for. |
| Telegram mini app | P3 Park | S | Trader | TradingView mini app inside Telegram since Apr 2025. | Alert delivery to Telegram covers the need. |

### Account

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Accounts, sign-in and 2FA | P0 Launch | S | Both | Email and social sign-in; 2FA is required before webhooks work. | Webhooks move money, so 2FA ships at launch. |
| Free tier plus one membership | P0 Launch | M | Both | Basic free; Essential $12.95, Plus $29.95, Premium $59.95, Ultimate $199.95 a month billed annually (monthly billing costs more); prices rose about 17 to 20% on 10 Apr 2026. | One paid plan is required for real-time data, data packages and invite-only scripts, so billing ships at launch. Fair-use limits replace tiers. |
| Help center and support | P1 Fast follow | M | Both | Help center; no support on Basic, ticket support on paid plans, weekdays only. | Vendors will forward their customers' problems to us. |
| Localization | P2 Later | M | Trader | Interface in many languages (19 in the mobile apps). | Many vendor audiences are non-English. Add the top languages from vendor data. |

### AI

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| AI migration assistant | P1 Fast follow | M | Vendor | Nothing comparable for porting. | Suggests fixes for anything the compatibility checker flags. Speeds up onboarding. |
| AI copilot | P2 Later | M | Trader | AI Copilot add-on (28 Sep 2026) reads data, draws levels, creates alerts and writes and applies Pine; not on mobile. | Expected eventually. Also a threat: easy Pine generation erodes demand for simple paid scripts. |
| Public API and MCP server | P2 Later | S | Both | MCP server in public beta since 16 Sep 2026: 35 tools, Essential and up, delayed data. | Cheap once our API exists, and agents are becoming a way users operate tools. |
| AI screener and summaries | P3 Park | M | Trader | AI Screener (Aug 2026) and AI summaries of news, filings and documents. | Tied to fundamentals and news we will not carry early. |

### B2B products

| Feature | Grade | Effort | For | TradingView today | Why this grade |
|---|---|---|---|---|---|
| Widgets and charting libraries | Skip | - | Us | 22 free widgets, open-source Lightweight Charts, Advanced Charts (free only with attribution on public, non-paywalled sites) and the paid Trading Platform library. | A different business. Stay focused on vendors and their customers. |

## Recommended launch scope

The durations below are planning assumptions, not quotes. They assume about 6 to 8 experienced engineers and a licensed engine. Building the engine in-house adds months. Live chart sessions were added after these estimates; by the effort scale in the feature grades they add roughly 12 to 34 engineer-weeks to the pilot.

### Validate (Weeks 0 to 3)
- Get written answers from TradingView support on the effective date, whether Paid Spaces subscribers count and whether free grants count.
- Compare the archived copies of the Terms (1 Jul, 1 Aug, 1 Sep and 20 Sep 2026) to date the clause.
- Interview 20 vendors with more than 100 users outside Paid Spaces. Sign 3 to 5 design partners with letters of intent and consent to test their scripts.
- Counsel reviews Terms Section 3, trademark use, the clean-room process, test data and an AGPL policy.
- Run the engine bake-off on design partners' scripts, then decide whether to license or build.
- Fix the revenue share rule (one payout per member per month) and measure compute per member before announcing the $5.
- Ask CME about non-pro eligibility and non-display classification. Ask Cboe about the vendor waiver.
- Ask CME and each exchange we carry to confirm in writing that live rooms need no extra license when they share chart state only and every viewer loads data under their own license.
- Get counsel's view on paid live trading rooms.

### Pilot (Months 1 to 4)
- Every P0 item in the feature grades.
- Pine v5 and v6 indicators and strategies running server-side in a sandbox, with the compatibility checker and parity suite.
- Web chart with the core drawing set, top 30 built-ins, saved layouts and watchlists with TradingView import.
- Crypto and FX data matched per symbol to TradingView's sources.
- Server-side alerts with TradingView-compatible webhooks, email, Telegram and Discord, on shared computation.
- Public access API with Whop sync, the migration kit, revenue share tracking and code custody.
- Free tier and membership billing with fair-use limits.
- Live chart sessions with invite-only rooms, follow mode, host controls and the collaboration switch. Every viewer is checked for data and script access, and trade markers stream live.
- Vendor vetting, conduct rules and 2FA.

### Launch (Months 4 to 7)
- The P1 items.
- Strategy report, Bar Replay, v4 scripts and lower-timeframe requests.
- Multi-chart layouts (4, then 8), sync, templates, seconds charts, range bars and volume profile.
- US stocks through Cboe One. CME futures and continuous contracts once committed demand covers the license.
- Vendor payouts, checkout sync beyond Whop (Stripe, LaunchPass, Gumroad), Discord role sync, vendor analytics, PWA with push and a first prop-firm integration.
- Session chat.

### Scale (Months 7 to 12)
- The P2 items, in the order vendors ask for them.
- Pine Screener, parameter optimizer, deep backtesting, native apps, a marketplace, a public API with an MCP server and auto-trading partners.
- Host voice and video, session recordings and broker-linked trades in live rooms.

## Pricing we can win with

The model: a free tier, one paid membership and market data add-ons. No tiers.

**Free tier**

- Charts with delayed data, built-in indicators and a capped number of indicators per chart.
- No invite-only scripts, no real-time data and no futures. Delayed CME data still costs about $7,280 a month to distribute.

**Membership (working number: $14.99 a month)**

- Required for real-time data and for buying data packages.
- Required to use invite-only scripts and to host them. Hosting has no per-user cost, however many users a vendor has.
- Required to join invite-only live rooms. Viewers also need the data packages for whatever the host shows.
- Everything else sits in one plan, with fair-use limits on alerts and charts per layout instead of tiers.

**Add-ons**

- Market data packages at cost plus a small margin: CME near TradingView's $9.95, US stocks from Cboe One.

**Vendor revenue share**

- A vendor earns $5 a month for each member who is active with us and still has access to that vendor's script.
- Access follows the vendor's billing platform. Whop comes first: access is granted on purchase and removed automatically when the vendor subscription ends, which also ends the $5.
- One payout per member per month. If a member uses several vendors, the $5 goes to the vendor who referred them or is split across their active vendors. Without that rule, a member using three vendors costs $15 on a $14.99 plan.
- Pay it every month the member stays, not just the first. Recurring income is what makes vendors move their customers.
- Decide whether live room access earns the $5 the same way script access does.

For a vendor with 1,000 users, TradingView's bill is $29,950 a month. With us the vendor pays one $14.99 membership and earns $5,000 a month.

**What to settle before announcing it**

- **The price against Essential.** TradingView's Essential plan costs $14.95 billed monthly or $12.95 billed annually and includes webhooks. At $14.99 the membership is only cheaper if it includes what TradingView sells in Plus and Premium: 100+ alerts, 8 charts per layout, seconds charts and 20K bars. Otherwise price it under $12.95.
- **For many script buyers the membership is a new cost.** TradingView lets free Basic accounts run invite-only scripts; only publishing them needs a paid plan. The pitch to those buyers has to rest on what the membership includes.
- **Margin.** $14.99 minus the $5 share minus about $0.73 in card fees leaves about $9.26 per member for compute, data, support and every free-tier user. Compute per member is unknown until the pilot measures it. Measure it before promising the $5 in public, because cutting it later would repeat TradingView's move on vendors.
- **Payout operations.** Tax forms (W-9, W-8BEN), 1099s for US vendors, a minimum payout, a holding period (Paid Spaces holds up to 30 days) and clawbacks on refunds and chargebacks.

## Risks and second-order effects

Severity is my judgment of impact times likelihood.

- **High: TradingView controls our wedge.** Section 22A says TradingView "may change the Technology Fee at any time on written notice". It can cut the fee, exempt large vendors privately or admit more of them to Paid Spaces at 0%. Any of those removes the switching reason overnight. Mitigation: win on things TradingView will not match (the vendor owns the customer, a $5 monthly share per member, an access API, Discord and Telegram delivery, prop-firm access) and sign design partners to annual terms.
- **High: LuxAlgo is ahead and owns the leading engine.** It has a live Pine platform, bundled data and a brand. Mitigation: be the neutral host that does not sell indicators, and do not make our core depend on LuxAlgo's license.
- **High: Traders do not want to leave TradingView.** Vendors will not move if customers churn during the move. Mitigation: a membership priced against TradingView's Essential plan, one-click watchlist import, identical alert and webhook behavior, support for running both platforms during a transition and prop-firm distribution.
- **High: Parity failures kill trust.** A signal that differs from TradingView by one bar produces a support ticket from every customer. Parity testing is also legally awkward: Terms Section 3 bars "creating products or services based on TradingView content" and "any processing of TradingView's content". Mitigation: a clean-room engine built from documented semantics, independent test vectors and a lawyer's sign-off before anyone uses TradingView output in testing.
- **High: Futures and stock data costs.** Exchange licensing is the one cost that does not shrink with good engineering. Mitigation: crypto and FX first, then CME as a pass-through add-on once committed demand covers the fixed licenses. Confirm non-pro eligibility with CME before pricing it.
- **Medium: Adverse selection of vendors.** The first vendors to arrive may include ones TradingView rejected or banned, and free hosting plus a $5 share makes us more attractive to them. They bring refund disputes, performance-claim problems and regulatory attention to "signal selling". Mitigation: vetting, conduct rules modeled on TradingView's Vendor Requirements and no unverified performance claims.
- **Medium: Code custody.** Vendors hand us their most valuable asset. One leak ends the company. Mitigation: server-side execution only, encryption at rest, audit logs and a SOC 2 plan.
- **Medium: The $5 share squeezes margin.** Each member leaves about $9.26 after the share and card fees, before compute, data, support and free users. If costs run high the share is the obvious thing to cut, and cutting it repeats TradingView's move on vendors. Mitigation: measure compute per member in the pilot and set the share before announcing it.
- **Medium: Payout and tax operations.** Paying vendors brings tax forms, 1099s, holds, clawbacks and payout compliance. Selling memberships abroad adds VAT. Mitigation: a payout provider that handles tax forms, a minimum payout and a holding period.
- **Medium: Trademark and naming.** "PINE SCRIPT" is a registered US trademark of TradingView (Reg. No. 7,559,746). Use it only to describe compatibility, with the ® and a disclaimer. Keep "Pine", "TV" and "TradingView" out of the product name and domain.
- **Medium: Live rooms could leak data.** If room traffic ever carries the host's prices, a recording or a screenshot stream, we redistribute data to viewers who have not paid for it. Mitigation: rooms carry chart state only, and every viewer's data stream is checked against that viewer's license.
- **Medium: Paid trading rooms draw regulators.** Rooms where hosts call trades for paying members can fall under trading-advice rules; in the US, futures advice is overseen by the CFTC and NFA. Mitigation: host terms that make hosts responsible for their content, required disclaimers, no unverified performance claims and counsel before launch.
- **Medium: Opening-bell load.** Thousands of viewers join the same room in the same minute, and each opens their own data stream. Mitigation: publish-subscribe fan-out for room state, snapshots for late joiners and load tests at real room sizes.
- **Medium: Webhooks move money.** A hijacked account can fire trades through a customer's bot. Mitigation: 2FA at launch, signed webhooks and alert audit logs.
- **Low: TradingView pushback on vendors.** House Rules ban links in script content. The only allowed pointer is a link in "Author's instructions" to the vendor's own page, plus the Signature field on Premium and up. The $5 share gives vendors a reason to push harder, so they must move customers through their own sites, Discord and email. TradingView may keep hosting a departed vendor's scripts under the Section 22 license, which is irrevocable but not exclusive.
- **Low: AGPL contamination.** Engineers copying PineTS or the Vela-PineTS bridge into a closed codebase would create an obligation to publish source. Mitigation: a dependency license policy enforced in CI.

### What you are not seeing

- **The pool may shrink for everyone.** If vendors respond by raising prices, dropping lifetime plans and cutting free grants, the paid-indicator market gets smaller before anyone moves. We would be competing for a shrinking pie at launch.
- **AI is commoditizing simple indicators.** TradingView's AI Copilot (28 Sep 2026) writes and applies Pine on the chart, and TakeProfit and ChartingLens convert Pine automatically. Simple paid indicators lose pricing power. Value moves to vendors with real research, signals, education and community. Our pitch should target those vendors and sell infrastructure they cannot replace with a prompt.
- **Vendors will run on both platforms.** Paid Spaces gives discovery that we cannot match early. Expect vendors to keep a TradingView presence and move their heaviest or most profitable users to us. Design for running on both platforms, not for exclusivity.
- **Prop firms are the unguarded door.** TopstepX embeds TradingView charts but cannot load custom or purchased indicators because of TradingView's licensing. Prop-firm futures traders are a big buyer group for paid scripts, and a prop-firm integration is a distribution channel TradingView's own license blocks.
- **Live rooms sell data.** Viewers need a membership and the host's data packages to watch live, so every popular futures room sells CME packages and memberships.
- **Rooms compete with Discord habits.** Creators already run live rooms with voice on Discord, YouTube and Twitch. Without voice at launch hosts will run both apps, so link their voice channel from the room from day one.
- **A room is a product vendors can sell.** Room access runs on the same grants and Whop sync as scripts. That opens a second revenue line for creators and raises the question of whether room access earns the $5.
- **Agents are becoming a channel.** TradingView shipped an MCP server (public beta 16 Sep 2026, 35 tools). A clean public API makes our platform usable by agents at little extra cost.
- **Gaming the snapshot is a trap.** The count happens on the last day of the month, so some vendors will try revoking access before month end. TradingView also counts "script usage" and bans rule-dodging, and vendors who get caught lose everything. Expect some banned vendors to show up on our doorstep, which feeds the adverse-selection risk.

## Unknowns and how to close them

| Unknown | Why it matters | How to close it |
|---|---|---|
| When the fee took effect | Sets vendor urgency and our window | Compare the archived Terms (1 Jul, 1 Aug, 1 Sep, 20 Sep 2026); ask TradingView support; ask vendors whether they received notices or invoices |
| Whether Paid Spaces subscribers count | Decides whether Paid Spaces is an escape hatch | Written question to TradingView support |
| The Paid Spaces fee after 1 Oct 2026 | A non-zero fee strengthens our pitch | Watch the Creator Program terms page from 1 October |
| How many vendors have more than 100 users | Market size | No public data exists. Use interviews, vendor claims and checkout marketplaces. Do not scrape TradingView. |
| How vendors are reacting | Demand signal | Reddit, X and Discord were blocked from this research environment. Check them by hand and call vendors. |
| Pine versions and features in paid scripts | Engine scope | Design partners' source code |
| Whether vendor-supplied TradingView exports can be used for testing | The parity-testing method | Counsel |
| CME non-pro eligibility without order routing | Futures pricing | Written answer from CME market data (marketdata@cmegroup.com) |
| Crypto display rights | Data sourcing | Aggregator warranties and indemnities, or direct exchange licenses |
| Compute cost per member | Whether $14.99 with a $5 share leaves a margin | Measure in the pilot before announcing the share |
| Exchange view on live rooms | Whether rooms need extra licenses | Written confirmation from CME and each exchange we carry |
| Whether room access earns the $5 share | Cost of the share and the creator pitch | Decide before launch |
| Whether other platforms offer live co-viewing | Positioning | Not covered by this research. Check before marketing it as unique. |
| How members who use several vendors are credited | The real cost of the $5 share | Decide before launch: one payout per member per month |

## Sources

All pages were read on 29 September 2026 unless a date is given. Full research notes with every source and verification label are in the repository under `docs/research/notes/`.

- TradingView Terms of Use, Sections 3, 18, 22 and 22A: https://www.tradingview.com/policies/
- Paid Spaces terms: https://www.tradingview.com/support/solutions/43000772177-tradingview-creator-program-paid-spaces-terms/
- Creator Program announcement (12 Aug 2026): https://www.tradingview.com/blog/en/tradingview-creator-program-60011/
- Paid Spaces launch (13 Nov 2025): https://www.tradingview.com/blog/en/paid-indicators-strategies-on-tradingview-54934/
- Paid Spaces marketplace: https://www.tradingview.com/scripts/marketplace/
- Vendor Requirements: https://www.tradingview.com/support/solutions/43000549951-vendor-requirements/
- Script publishing update (14 Aug 2026): https://www.tradingview.com/blog/en/updated-script-publishing-60116/
- Pricing and plan limits: https://www.tradingview.com/pricing/
- Features: https://www.tradingview.com/features/
- Pine limits: https://www.tradingview.com/pine-script-docs/writing/limitations/
- Pine release notes: https://www.tradingview.com/pine-script-docs/release-notes/
- Webhooks: https://www.tradingview.com/support/solutions/43000529348-about-webhooks/
- AI Copilot (28 Sep 2026): https://www.tradingview.com/blog/en/ai-copilot-now-on-tradingview-61231/
- MCP server (16 Sep 2026): https://www.tradingview.com/blog/en/tradingview-mcp-server-public-beta-60864/
- "PINE SCRIPT" trademark, US Reg. No. 7,559,746: https://tsdr.uspto.gov/statusview/sn97298638
- LuxAlgo acquires PineTS (1 Jun 2026): https://www.luxalgo.com/blog/luxalgo-acquires-pinets-to-bring-pine-script-r-everywhere/
- LuxAlgo charting platform (31 Aug 2026): https://www.luxalgo.com/blog/luxalgo-charting-platform/
- Vela (3 Sep 2026): https://www.luxalgo.com/blog/introducing-vela/
- PineTS: https://github.com/LuxAlgo/PineTS
- PyneCore: https://github.com/PyneSys/pynecore and https://wild.pynesys.io/
- PineForge: https://github.com/pineforge-4pass/pineforge-engine
- cTrader subscriptions (5 Aug 2026): https://www.financemagnates.com/forex/products/ctrader-adds-subscriptions-as-trading-platforms-court-paid-tool-creators/
- OpenMarket (27 Sep 2026): https://x.com/openmarket_xyz/status/2104254223517106349
- TopstepX TradingView charts: https://help.topstepx.com/components/tradingview-tm-charts
- SAS v. World Programming, 4th Cir. (12 Mar 2020): https://www.ca4.uscourts.gov/Opinions/191290.P.pdf
- SAS v. World Programming, Fed. Cir. (6 Apr 2023): https://www.cafc.uscourts.gov/opinions-orders/21-1542.OPINION.4-6-2023_2106573.pdf
- Google v. Oracle (5 Apr 2021): https://www.supremecourt.gov/opinions/20pdf/18-956_d18f.pdf
- CME fee list, effective 1 Jan 2026 (Databento copy): https://api.databento.com/static/licensing/cme/cme-market-data-fee-list.pdf
- Cboe US market data price list: https://cdn.cboe.com/resources/membership/US_Market_Data_Product_Price_List.pdf
- CT Plan fees: https://consolidatedtape.com/fees
- Coinbase market data terms (7 Aug 2026): https://www.coinbase.com/legal/market_data
- CoinAPI pricing: https://www.coinapi.io/products/market-data-api/pricing
- TradingView Advanced Charts license (June 2026): https://s3.amazonaws.com/tradingview/charting_library_license_agreement.pdf
- Lightweight Charts: https://github.com/tradingview/lightweight-charts
- KLineChart: https://github.com/klinecharts/KLineChart
- Vendor pricing pages: https://www.luxalgo.com/pricing/ , https://algoalpha.io/pricing , https://chartprime.com/ , https://bigbeluga.ai/ , https://www.zeiierman.com/ , https://marketciphertrading.com/pricing/ , https://www.fluxcharts.com/ , https://smrtalgo.com/ , https://www.quantvue.io/pricing
- Automation services: https://traderspost.io/ , https://www.pineconnector.com/ , https://pickmytrade.io/pricing
