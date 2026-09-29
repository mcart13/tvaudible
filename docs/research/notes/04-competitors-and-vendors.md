# TradingView invite-only vendors: competitive landscape and vendor market

> Research notes compiled on 29 September 2026. They are the evidence behind [the teardown](../tradingview-teardown.md). Claims keep the labels used during research (VERIFIED, UNVERIFIED, NOT FOUND and similar). Punctuation was normalized afterwards; the wording is otherwise as researched.

Research as of 2026-09-29

**How to read this.** Tags such as [S12] point to the numbered source list at the end, which gives each URL and its date (the publication date or "acc." = accessed 2026-09-29 when the page shows no date).
- **Default label:** every claim is **VERIFIED** against its tagged source unless it is marked otherwise.
- **U** = UNVERIFIED. **NF** = NOT FOUND. **C** = sources conflict.
- **V\*** = verified only from the search-engine excerpt of that official page, because the page itself would not load (JavaScript-rendered or blocked).
- **"Analysis"** marks my own inferences, not sourced claims.

**Limitations.**
- X/Twitter, Reddit, Discord and Patreon could not be reached, so public-reaction data is thin.
- The session's web-search quota ran out near the end, so the last checks used direct page fetches only.
- Page quotes come from an automated page reader; the key numbers were cross-checked where possible.

## Key findings
1. **Fee cost for vendors (Analysis).** Read literally, the Technology Fee equals **72 to 109% of per-user revenue** at the cheapest published annual tier of 7 of the 10 major vendors I priced (table in §3).
2. **Paid Spaces is the only cheap route, and it is selective.** It had 39 creators on Aug 12, 2026 and 47 on Sep 29, against 1,000+ applicants. Its platform fee is 0% until at least Oct 1, 2026.
3. **The largest vendor has already built its own platform.** LuxAlgo launched **QuantCharts** on Aug 31, 2026. It runs Pine natively through **PineTS**, the open-source Pine runtime LuxAlgo controls (AGPL or commercial licence).
4. **Pine is becoming portable.** Options now include PineTS, PyneSys/PyneCore, PineForge and AI converters from TakeProfit, ChartingLens and TrendSpider.
5. **Marketplace fee norms:**
   - 20%: TrendSpider, MQL5, TakeProfit.
   - 27% on add-ons: Bookmap.
   - 30%: cTrader.
   - Vendor sales tooling costs about 3 to 13% (Whop, Stripe, Gumroad, LaunchPass).
6. **No public reaction to the Technology Fee** from any vendor or platform was found, and I found no announcement date.

## 0. Baseline: what TradingView changed
- **Technology Fee (Terms of Use §22A)** [S1]:
  - Wording: "US$29.95 per calendar month per user whose access to any invite-only script published by you is active at the end of that calendar month. The Technology Fee applies only where the total number of users with active access to your invite-only scripts exceeds 100."
  - Counting and billing: users are counted on the last day of the month from TradingView's "records of access grants and script usage". The invoice arrives within 30 days and is payable within 14 days. TradingView may change the fee "at any time on written notice."
  - If unpaid, TradingView may:
    - block new access grants
    - revoke existing access
    - remove scripts
    - withdraw vendor privileges
    - suspend the account
    - recover the money with interest.
  - The section applies to existing scripts and existing vendors (V\* [S1]).
- **The wording is ambiguous (Analysis).**
  - Read literally, once a vendor passes 100 users, *every* user is billed: 101 users would cost $3,024.95 a month. If only users above 100 are billed, 101 users would cost $29.95.
  - Free, trial, complimentary and lifetime grants count if they are active.
  - TradingView has not clarified this in any source I found.
- **Announcement or effective date: NF.** The policies page carries no date, and I found no blog post or press coverage.
- **Observation.** The fee equals the Plus plan's annual-billed monthly price of $29.95 [S9]. Invite-only scripts also work on free Basic accounts [S88][S93]. Analysis: in effect, vendors pay for a Plus seat for each user.
- **Paid Spaces / Creator Program:**
  - In-platform paid subscriptions launched Nov 13, 2025 with a hand-picked group [S7].
  - On Aug 12, 2026 applications opened: 39 creators, "$4.99 to $199 per month", "Over 1,000 people have applied" [S2].
  - Eligibility: a Premium or Ultimate plan, plus a public invite-only script published more than 3 months ago with 100+ boosts [S5].
  - Platform fee: 0% "until at least Oct. 1, 2026" [S23]. Authors approved before Apr 1, 2026 keep 0% permanently [S3].
  - Payouts: USD via PayPal, $100 minimum [S3], 30-day settlement [S4].
  - Script cap: up to 50 per Space [S3] versus up to 25 [S4][S23] (C).
  - Subscriptions can only be bought on the web version [S4].
  - TradingView handles billing, renewals, access and VAT/sales tax and cites a "16M+ audience… use Supercharts every month" [S8].
- **Do Paid Space subscribers count toward the fee? NF.** Paid Space scripts are "special invite-only scripts" [S10], and §22A lists no exemption [S1]. The client should confirm this directly with TradingView.
- **Other 2026 changes:**
  - All paid plans rose about 17 to 20% on Apr 10, 2026 [S16]. Monthly billing is now $14.95 / $34.95 / $69.95 / $239.95; annual billing is $12.95 / $29.95 / $59.95 / $199.95 per month [S9].
  - Since Aug 14, 2026, scripts need moderator approval before appearing in feeds, with caps of 5 new public scripts per 24 hours and 15 per 30 days [S11].

## 1. Competing platforms

| Platform | Pricing | Scripting | Third-party marketplace / fee to vendors | Data model & assets | Form | Users (published) |
|---|---|---|---|---|---|---|
| TradingView (baseline) | $12.95 to $199.95/mo billed annually [S9] | Pine | Paid Spaces 0% [S23]; Technology Fee for invite-only sold outside TradingView [S1] | Bundled data; exchange fees extra | Web, desktop, mobile | "100 million traders" [S9]; 16M+ monthly Supercharts users [S8] |
| TrendSpider | Annual ≈$54/$91/$122 per month for Standard/Premium/Enhanced [S36][S37]; monthly and Advanced prices C ($82 to 321 [S36] vs $89 to 447 [S37]) | JavaScript [S38 V\*] | Store: developer keeps 80%, TrendSpider 20%; monthly subscriptions only; 5-day free trial required [S38 V\*][S39] | Bundled; stocks, crypto, futures, FX [S37] | Web (U) | NF |
| NinjaTrader | Free / $99 per month / $1,499 lifetime (sets commission tier) [S30] | NinjaScript (U) | Ecosystem: "1,000+ vendors" who sell direct; "Ecosystem 2.0" moving to user-based "invite-only" licensing [S32][S33]; vendor fees NF | Futures broker; owned by Payward (Kraken) [S31] | Desktop, web, mobile [S30] | "over 2 million users" [S31] |
| Tradovate | $0 / $99 per month / $1,499 lifetime [S34] | JavaScript; community sharing [S35] | Paid sales: NF | Futures broker (NinjaTrader Group) [S34] | Web, mobile (U) | NF |
| Sierra Chart | $26 to $56/mo [S41] | ACSIL, C++ (U) | No marketplace; free web control panel to authorise users and set expiry [S42] | Own feed (Denali) or bring your own: IB, CQG, Rithmic [S41] | Windows desktop (U) | NF |
| Quantower | $70/mo, 10 to 30% off for longer terms [S43]; about $1,590 lifetime (U) | C# (U) | NF | Bring your own broker; data not included [S43] | Desktop | NF |
| MotiveWave | Free Community edition; lifetime $245 to $2,295; lease about $23 to $152/mo [S46] | Java SDK in every edition [S44] | Marketplace by partnership; fees NF [S45] | 30+ brokers and data feeds, bring your own [S44] | Desktop | NF |
| MultiCharts | $291 for 3 months, $534 for 6, $797 per year, $1,497 lifetime [S47] | PowerLanguage, EasyLanguage-compatible, imports TradeStation .ELD files [S48 V\*]; .NET; Python beta [S47] | NF | Bring your own: 20+ feeds, 10+ brokers [S47] | Windows (U) | NF |
| TradeStation | Desktop free with a funded account; $10/mo inactivity fee [S50] | EasyLanguage | TradingApp Store: third-party developers, monthly subscriptions [S49]; revenue share NF | Broker-bundled | Desktop, web (U) | NF |
| thinkorswim | Free; $0 stocks, $0.65 per options contract [S51] | thinkScript, desktop only [S51] | None; code cannot be protected [S52] | Schwab broker-bundled | Desktop, web, mobile [S51] | NF |
| TC2000 | $24.99 / $49.99 / $99.99 per month [S53] | PCF formulas | None found | US stocks and options bundled; brokerage discount up to $300/yr [S53] | U | NF |
| MetaTrader 4/5 | Free via brokers (U) | MQL4/5 | MQL5 Market: 20% commission, $30 minimum price [S27]; rentals of 1/3/6/12 months [S28]; "10,000 products" [S29] | Data from the broker | Desktop, web, mobile (U) | NF |
| cTrader | Free via brokers (U) | C#, Python [S26] | Store: 30% commission [S23]; subscriptions since Jul 2026 [S24]; affiliates earn up to 20% [S25]; 2,000 products, 300 sellers [S26] | Data from the broker (FX/CFD) | Windows, Mac, web, mobile [S26] | "over 11 million traders" [S25] |
| ProRealTime | Web version free; Complete €24/$32, Premium €70/$91 per month, plus data [S54] | ProBuilder | ProRealCode MarketPlace with vetted authors [S55]; fee NF | Bundled data plus broker links | Web, desktop, mobile [S54] | NF |
| GoCharting | Free / Premium / CME plans; prices not shown [S56] | LipiScript; docs never mention Pine [S57] | 7,000+ community scripts [S57]; paid sales NF | Bundled: CBOE, SIP, CME, crypto, FX; Rithmic/Tradovate feeds for prop traders [S56] | Web (U) | "3M+ traders" [S56] |
| ATAS | €0 / €24.95 / €69.95 / €89.95 per month; lifetime €999, €1,999 [S58] | API included [S58] | NF | Bring your own connections [S58] | Desktop; ATAS X beta on Windows/macOS [S58] | "360,000+ traders" [S58] |
| Bookmap | Free / $19 / $49 / $99 per month; lifetime $990 / $1,990 [S59] | API (U) | Marketplace: vendor keeps **73%** on add-ons, 88% on services [S60] | Crypto data free; bring your own for futures and stocks [S59] | Desktop | NF |
| Tickblaze | NF | C#, Python [S61] | Vetted marketplace; fee NF | Direct CME/Nasdaq licences plus Rithmic, dxFeed, Polygon [S61][S62] | Desktop; web version launched May 5, 2026; mobile [S62] | NF |
| TopstepX | Included with Topstep accounts [S64]; API $29/mo [S65] | None: "custom indicators are not available due to TradingView's commercial licensing terms" [S64][S63] | None | Topstep prop accounts only; ProjectX exclusive to Topstep since Feb 2026 [S65] | Web (U) | NF |
| Koyfin | $0 / $39 / $79 / $209 / $299 per month [S66] | Custom formulas only | None | Bundled (S&P Capital IQ, Morningstar) [S67] | Web (U) | 500,000+ investors; 50,000+ advisers [S67] |
| TakeProfit | $20/mo; annual $120 [S68] vs $100 [S70] (C) | Indie, a Python dialect [S71] | Creator keeps 80% (100% on buyers they referred); widgets 70% [S69] | Bundled real-time US stocks; 70+ crypto exchanges [S68][S70] | Web (U) | NF |
| **New: LuxAlgo QuantCharts** (Aug 31, 2026) | Free; paid $39.99 to $119.99 list ($27.99 to $54 promotional) [S76] | Native Pine v5/v6 via PineTS [S74] | LuxAlgo's own library only; third-party sales NF | Bundled: Cboe EDGX via Databento, CME real-time with 16 years of history, FMP for FX [S74] | Web [S74] | "100,000+ traders" [S77] |
| **New: ChartingLens** | Free; $14.99 to $29.99 [S18] | AI conversion of Pine [S18] | NF | NF | Web | NF |

## 2. Pine Script compatibility, and who is courting vendors

**Tools that run or convert Pine**
- **PineTS (LuxAlgo):**
  - Open-source transpiler and runtime for Pine v5/v6 in Node.js and the browser, claiming "1:1 syntax compatibility".
  - Licensed under AGPL-3.0 or a commercial licence (price NF). The AGPL copyleft applies when the software is offered as a network service. 706 GitHub stars [S79].
  - It powers QuantCharts ("Paste an indicator you wrote and it plots"). It also pairs with the embeddable Vela chart (Apache-2.0) through the Vela-PineTS engine (AGPL) [S78].
  - LuxAlgo says Vela and PineTS "see tens of thousands of installs a month" [S77].
- **PyneSys / PyneCore:**
  - A deterministic compiler from Pine to Python, $8 to $45/mo.
  - Claims "819/819 real TradingView scripts compile & run" and "99.717% of 100 million compared bars bit-exact" [S83].
  - The PyneCore runtime is Apache-2.0 [S84 V\*].
- **PineForge:**
  - Converts Pine v6 to C++ for backtesting and claims about 98% coverage.
  - Forward-testing Q3 2026, live trading 2027, strategy marketplace 2027 [S82].
- **AI converters:**
  - TakeProfit (Pine to Indie): "roughly nine in ten indicators cleanly" [S70][S71].
  - ChartingLens [S18].
  - TrendSpider's Code Conversion programme for Pine and thinkScript [S40 V\*].
- **Pine support in GoCharting and TabTrader:** claimed only by third parties. GoCharting's official documentation does not mention Pine (U).
- **Precedent:** MultiCharts built its business on compatibility with TradeStation's EasyLanguage, including importing .ELD files; encrypted .ELD files need MultiCharts' help [S48 V\*].

**Platforms courting creators, Aug to Sep 2026**
- **cTrader** added subscriptions to its Store on Jul 28 [S24]. On Aug 5, Finance Magnates covered this under the headline "cTrader Adds Subscriptions as Trading Platforms Court Paid-Tool Creators", comparing cTrader's 30% with MQL5's 20% and TradingView's 0% [S23].
- **LuxAlgo** launched QuantCharts 19 days after the Creator Program opened. On Sep 22 it followed with "How to Run Pine Script® Outside of TradingView (2026 Guide)" [S74][S78].
- **TakeProfit** runs an ongoing creator programme paying 80 to 100% [S69]. Its Aug 17 post attacked TradingView's data fees [S70].
- **Any platform explicitly citing the Technology Fee to recruit vendors: NF.**

## 3. The vendor market

| Vendor | Direct pricing | In Paid Spaces? (Sep 29) | Published user claims | Platforms |
|---|---|---|---|---|
| LuxAlgo | Premium $39.99/mo list ($27.99 promo) or $479.88/yr; Ultimate $59.99 ($35.99) or $719.88/yr; AI Ultra $119.99 ($54) or $1,439.88/yr [S76] | Not listed [S6] | "100,000+ traders" [S77]; 1.4M TradingView followers, 409 scripts [S19] | TradingView on any plan [S80], plus its own platform |
| AlgoAlpha | Indicators $344.64/yr (≈$28.72/mo); VIP $951.84/yr; Signals $772.44/yr [S85]. The Indicators plan was $24.98/mo billed yearly on Jun 7 [S86] | $65.57/mo [S6] | "95k+ Active traders" [S85] | TradingView only |
| ChartPrime | Pro $67/mo or $489/yr; Plus $117/mo or $708/yr [S87] | $117/mo, 5 scripts [S21] | "100K+ Active Users" [S87] | TradingView |
| BigBeluga | $56.50/mo; $27.36/mo billed yearly; $1,399 lifetime [S89] | $66.47/mo [S20] | 77,000 TradingView followers (not paying customers) [S89] | TradingView only |
| Zeiierman | $95.20/mo; $37.99/mo billed yearly; lifetime price NF [S88] | $95.20/mo [S6] | "over 25,000 users" [S88] | TradingView only |
| Market Cipher | $600 for 12 months; $1,500 lifetime [S90] | Not listed | NF | TradingView |
| Trading Alpha | NF (page renders in JavaScript); "no refunds" [S91] | Not listed | 61,000 Discord members [S91] | TradingView |
| QuantVue | Pro $197/mo or $1,497/yr; Elite $447/mo or $2,897/yr [S92] | Not listed | NF | TradingView and NinjaTrader |
| "Smart Money Algo": exact brand NF. Closest match is SMRT Algo | $97/mo, $497/yr, $795 lifetime (list prices) [S93] | Not listed | "15,000+ traders" [S93] | TradingView only |
| Flux Charts | $59.99/mo; $719.88/yr [S94] | Not listed | "20,000+ active traders" [S94] | TradingView only |

- **Other Paid Spaces** (at least 47 creators listed [S6]): DeMARK $29.99, Nison Candle Scanner $199, Trendoscope $69.99, jdehorty $49.99, LonesomeTheBlue $49.99, TradingFinder $48.88, Trading-IQ $79.99, loxx $120, toodegrees $120, BullByte $199.
- **Public reaction to the Technology Fee: NF for every vendor.** None of the vendor sites I fetched mention it.
- **Indirect signals (Analysis):**
  - LuxAlgo's platform launch, and an FAQ that now centres on its own workspace [S81].
  - AlgoAlpha's annual price rose about 15% between June and September; the cause is unknown.
  - jdehorty moved into Paid Spaces, re-priced on TradingView and grandfathered existing subscribers (Patreon post dated Dec 7, 2025 per search index) [S95 V\*].

**Fee economics (Analysis; literal reading, cheapest published per-user rate)**

| Vendor tier | $/mo | Fee as % of revenue |
|---|---|---|
| BigBeluga yearly [S89] | 27.36 | 109% |
| LuxAlgo Premium, first-year promo [S76] | 27.99 | 107% |
| AlgoAlpha Indicators yearly [S85] | 28.72 | 104% |
| Zeiierman yearly [S88] | 37.99 | 79% |
| LuxAlgo Premium renewal [S76] | 39.99 | 75% |
| ChartPrime Pro yearly [S87] | 40.75 | 73% |
| SMRT Algo yearly, list price [S93] | 41.42 | 72% |
| Market Cipher, 12 months [S90] | 50.00 | 60% |
| Flux Charts yearly [S94] | 59.99 | 50% |
| QuantVue Pro yearly [S92] | 124.75 | 24% |

- **Lifetime licences become ongoing costs.** Each lifetime user with active access costs $359.40 a year in fees, so a $1,500 Market Cipher or $1,399 BigBeluga lifetime sale is used up in about four years.
- **Illustration only:** if ChartPrime's "100K+" users all held TradingView access, the fee would be about **$3.0M per month**.

**Market-size data**
- TradingView hosts 150,000+ community scripts, "half of which are open-source" [S12]. That implies up to about 75,000 closed-source scripts, either protected or invite-only (Analysis).
- Count of invite-only scripts or vendors: **NF**.
- Paid Spaces went from 39 creators (Aug 12) to 47 (Sep 29) against 1,000+ applicants, an admission rate under 5% [S2][S6].

## 4. Tools vendors use to sell and manage TradingView access

| Tool | Fees | TradingView integration |
|---|---|---|
| Whop | 2.7% + $0.30 domestic; +1.5% international cards; +1% currency conversion; instant payout 4% + $1 [S97]. A 3% platform fee on Discord/Telegram/TradingView-gated sales was listed Dec 11, 2025 and gone by Feb 15, 2026 [S96] (C: some 2026 sources still cite it) | TradingView app: the buyer enters a TradingView username and access is granted [S98][S99] |
| Gumroad | 10% + $0.50 on direct sales; 30% via its Discover marketplace; merchant of record since Jan 1, 2025 [S100] | Native integration NF |
| LaunchPass | Free tier with no transaction fee; Premium $29/mo + 3.5%; Stripe 2.9% + 30¢ on top [S101] | Discord, Telegram, Slack only |
| Stripe (build it yourself) | 2.9% + 30¢; Billing 0.7%; Tax 0.5% [S102] | Build it yourself |
| Vendors' own dashboards | n/a | "Connect TradingView (and Discord)" flows at LuxAlgo, ChartPrime, Zeiierman, SMRT Algo [S80][S87][S88][S93] |
| Access automation | Free, open source | No official API: "backend calls that are not officially supported by tradingview". The tools store the vendor's password and require two-factor authentication to be switched off [S22][S103] |
| TradingView native | n/a | Manual "Manage access" [S10], or Paid Spaces |

## 5. Alert-automation ecosystem (what webhook compatibility a competitor needs)

| Service | Price | Alert payload format | Accepts non-TradingView sources? | Connects to | Users |
|---|---|---|---|---|---|
| PineConnector | $59 to $199/mo [S106] | Comma-separated text: `60123456789,buy,EURUSD,vol_lots=0.5,sl_pips=20,tp_pips=40` [S105] | Not stated | MT5 (MT4 legacy per [S106] vs "MT5 exclusively" per [S105]: C) | 66,000+ traders; 193M+ signals [S105] |
| TradersPost | $41.65 to $254.15/mo billed yearly [S107] | JSON: `ticker`, `action`, plus sentiment, quantity, orderType, price, takeProfit, stopLoss [S109] | Yes: any JSON sender, e.g. TrendSpider [S109] | Tradovate, TradeStation, IBKR, NinjaTrader, ProjectX, Alpaca, Robinhood, Webull, tastytrade, E*TRADE, Tradier; Coinbase, Kraken, Binance, Bybit, Crypto.com [S108] | 70,000+; $550M+ in connected accounts [S108] |
| 3Commas | $15/$38/$105 billed annually; $20/$50/$140 monthly [S110] | JSON with a secret and bot ID (U) | Yes: "Java and Python scripts… IFTTT" [S111] | About 9 crypto exchanges [S110] | NF |
| WunderTrading | Free plus 3 paid tiers; prices NF [S112] | Comment codes or JSON (U) | Yes: "Any Signal Source" [S112] | 18+ crypto exchanges, incl. Hyperliquid [S112] | NF |
| Alertatron | $59 / $99 / $199 per month [S113] | Its own command language (U) | Yes: "almost anything" [S113] | Bybit, Binance Futures, BitMEX, Deribit and others [S113] | NF |
| Capitalise.ai | NF (site would not load) | NF | NF | NF | NF |
| Tickerly | $19 / $29 / $39 per month [S114] | NF | Also takes MT4/MT5 alerts [S114] | Crypto exchanges; Oanda, Capital.com, Alpaca; MT4/5 [S114] | NF |
| PickMyTrade | $50/mo [S115] | JSON (fields NF) | NF | 50+ brokers incl. Tradovate, Rithmic, IBKR, ProjectX, cTrader; Topstep, Apex [S115] | 50,000+ [S115] |
| CrossTrade | $29 / $49 / $99 per month [S116] | Semicolon-separated key=value, e.g. `account=sim101;` `destination=tradovate;` [S116] | Yes [S116] | NinjaTrader 8, Tradovate [S116] | NF |

**TradingView's webhook behaviour, which a competitor would need to match** [S13][S14][S9]:
- An HTTP POST, sent as `application/json` if the body is valid JSON, otherwise as `text/plain`.
- Only ports 80 and 443; the request is cancelled after 3 seconds.
- Sent from four published IP addresses. Receivers that allowlist those IPs would need to add the competitor's (U).
- Two-factor authentication must be on; webhooks require the Plus plan or higher.
- Message placeholders such as `{{strategy.order.action}}`, `{{strategy.order.contracts}}`, `{{strategy.market_position}}` and `{{strategy.order.alert_message}}`.
- Alerts stop if they fire more than 15 times in 3 minutes.

## 6. End-user switching costs, and complaints a competitor could exploit
- **What users can take with them:**
  - Watchlists export and import as a .txt file of exchange-prefixed, comma-separated symbols [S15].
  - Exporting layouts, drawings or alerts: NF; treat these as lock-in (U).
- **Purchased indicators cannot move.** Under TradingView's invite-only model "the script is never provided" to the buyer [S52], so a vendor must re-provision customers on any new platform.
- **Broker and prop-firm lock-in:**
  - NinjaTrader advertises its TradingView integration [S30].
  - TopstepX embeds TradingView charts but cannot load custom or purchased indicators [S63][S64]. Analysis: prop-firm traders are an underserved segment.
- **2026 complaints:**
  - Prices rose about 17 to 20% on Apr 10 [S16].
  - One review says "Alerts on the Plus plan still expire after two months" [S16]. The pricing page shows "Alert durations: 2 mo." for Essential through Premium [S9].
  - Webhooks require the Plus plan [S9].
  - Trustpilot: 1,348 reviews, 62% one-star; the TrustScore is suspended for a guideline breach. September 2026 reviews cite chatbot-only support, double charges, FRED data moving behind a paywall and limits on free-tier watchlists [S17].
- **Friction for authors:**
  - The moderation queue and publishing caps [S11].
  - Paid Spaces pays out only in USD via PayPal, sells only on the web and admits few applicants [S3][S4][S2].
- **Attack lines competitors already use:**
  - A flat price with data included: TakeProfit's $20 plan includes NYSE/Nasdaq real-time data [S70].
  - Free AI conversion of Pine indicators [S18].

## 7. Implications for the client (Analysis)
1. **Vendor behaviour.** At the literal reading, the fee takes 50 to 109% of per-user revenue at most top vendors' cheapest tiers. Expect:
   - price rises
   - lifetime plans withdrawn
   - free access grants pruned
   - more Paid Spaces applications
   - vendors selling on several platforms at once.
2. **Paid Spaces is TradingView's intended destination for vendors.** The 0% fee could change after Oct 1, and fewer than 5% of applicants get in, which leaves most vendors without a cheap route.
3. **Table stakes for a challenger:**
   - A near-exact Pine v6 runtime with protected source code and per-user access control.
   - An official access-management API with Whop, Stripe and Discord hooks.
   - Alert placeholders and webhook behaviour identical to TradingView's.
   - Low-cost bundled market data.
   - Merchant-of-record and sales-tax handling.
   - A marketplace fee below the 20 to 30% norm.
4. **Risks:**
   - TradingView could clarify the fee, exempt Paid Spaces or set its own Paid Spaces fee.
   - Licensing PineTS means depending on LuxAlgo, now a competing platform.
   - "Pine Script®" is a TradingView trademark.
   - I did not review TradingView's terms on reverse engineering.

## Sources
- S1 https://www.tradingview.com/policies/ (§22A; acc.)
- S2 https://www.tradingview.com/blog/en/tradingview-creator-program-60011/ (2026-08-12)
- S3 https://www.tradingview.com/support/solutions/43000772177-tradingview-creator-program-paid-spaces-terms/ (acc.)
- S4 https://www.tradingview.com/support/solutions/43000790233-how-to-create-a-paid-space/ (acc.)
- S5 https://www.tradingview.com/support/solutions/43000765878-can-i-offer-my-paid-pine-scripts-right-on-tradingview/ (acc.)
- S6 https://www.tradingview.com/spaces/ (acc.)
- S7 https://www.tradingview.com/blog/en/paid-indicators-strategies-on-tradingview-54934/ (2025-11-13)
- S8 https://www.tradingview.com/creator-program/ (acc.)
- S9 https://www.tradingview.com/pricing/ (acc.)
- S10 https://www.tradingview.com/support/solutions/43000549951-vendor-requirements/ (acc.)
- S11 https://www.tradingview.com/blog/en/updated-script-publishing-60116/ (2026-08-14)
- S12 https://www.tradingview.com/pine-script-docs/welcome/ (acc.)
- S13 https://www.tradingview.com/support/solutions/43000529348-about-webhooks/ (acc.)
- S14 https://www.tradingview.com/support/solutions/43000481368-strategy-alerts/ (acc.)
- S15 https://www.tradingview.com/support/solutions/43000487233-how-to-import-and-export-watchlists/ (acc.)
- S16 https://chartinglens.com/blog/tradingview-price-increase-2026 (2026-08-22)
- S17 https://www.trustpilot.com/review/tradingview.com (acc.)
- S18 https://chartinglens.com/blog/best-tradingview-alternatives (2026-05-14)
- S19 https://www.tradingview.com/u/LuxAlgo/ (acc.)
- S20 https://www.tradingview.com/spaces/BigBeluga/ (acc.)
- S21 https://www.tradingview.com/spaces/ChartPrime/ (acc.)
- S22 https://www.tradingview.com/chart/BTCUSDT/2Kfqz7TE-Revisiting-Automatic-Access-Management-API-for-Vendors/ (2023-11-03)
- S23 https://www.financemagnates.com/forex/products/ctrader-adds-subscriptions-as-trading-platforms-court-paid-tool-creators/ (2026-08-05)
- S24 https://blog.ctrader.com/try-more-commit-less-subscriptions-arrive-in-ctrader-store/ (2026-07-28)
- S25 https://www.spotware.com/news/ctrader-store-affiliate-programme/ (2026-03-26)
- S26 https://ctrader.com/ (acc.)
- S27 https://www.mql5.com/en/market/rules (acc.)
- S28 https://www.metatrader5.com/en/terminal/help/market/market_rent (acc.)
- S29 https://www.mql5.com/ (acc.)
- S30 https://ninjatrader.com/pricing/ (acc.)
- S31 https://ninjatrader.com/ (acc.)
- S32 https://developer.ninjatrader.com/blog/the-continued-evolution-of-the-ninjatrader-ecosystem (2025-02-13)
- S33 https://ninjatraderecosystem.com/ (acc.)
- S34 https://www.tradovate.com/pricing/ (acc.)
- S35 https://www.tradovate.com/platform/custom-indicators-api/ (acc.)
- S36 https://www.stockbrokers.com/review/tools/trendspider (2026-07-28)
- S37 https://www.financialtechwiz.com/post/trendspider-pricing/ (2026-08-29)
- S38 https://trendspider.com/store-developer-terms/ (search excerpt, acc.)
- S39 https://help.trendspider.com/kb/sharing-content/publishing-content-to-trendspider-store (acc.)
- S40 https://trendspider.com/developers/code-conversion/ (search excerpt, acc.)
- S41 https://www.sierrachart.com/index.php?page=doc/Packages.php (acc.)
- S42 https://www.sierrachart.com/index.php?page=doc/DevelopingCustomStudiesAndSystems.php (acc.)
- S43 https://www.quantower.com/pricing (acc.)
- S44 https://www.motivewave.com/products.htm (acc.)
- S45 https://www.motivewave.com/marketplace.htm (acc.)
- S46 https://propfirmapp.com/trading-tools/motivewave (2026)
- S47 https://www.quantvps.com/blog/multicharts-explained (2026-01-02, updated 2026-09-18)
- S48 https://www.multicharts.com/features/easylanguage/ and https://www.multicharts.com/discussion/viewtopic.php?t=11017 (search excerpt)
- S49 https://help.tradestation.com/10_00/eng/tradestationhelp/desktop/tradingapp_store.htm (acc.)
- S50 https://emini-watch.com/tradestation/tradestation-data-feed/ (2026-08)
- S51 https://brokersdb.com/learn/thinkorswim-review (2026-02-21)
- S52 https://usethinkscript.com/threads/protect-source-code-in-thinkorswim.9048/ (2021-11-27 to 2022-02-12)
- S53 https://www.tc2000.com/pricing (acc.)
- S54 https://www.prorealtime.com/en/prices (acc.)
- S55 https://www.prorealcode.com/topic/prorealcode-marketplace-sell-your-trading-products-to-thousands-of-prorealtime-users/page/35/ (2019 to 2023)
- S56 https://gocharting.com/pricing (acc.)
- S57 https://gocharting.com/developers/lipi and https://gocharting.com/docs/scripting/welcome (acc.)
- S58 https://atas.net/pricing/ (acc.)
- S59 https://bookmap.com/pricing (acc.)
- S60 https://bookmap.com/knowledgebase/docs/KB-Help-FAQs-Marketplace (acc.)
- S61 https://tickblaze.com/platform/ (acc.)
- S62 https://fundedtrading.com/platform-provider/tickblaze/ (2026-08)
- S63 https://help.topstepx.com/components/tradingview-tm-charts (acc.)
- S64 https://help.topstep.com/en/articles/14434175-topstepx (acc.)
- S65 https://docs.pickmytrade.io/docs/connect-projectx-to-topstep-api/ (2026-09-03)
- S66 https://www.koyfin.com/pricing-llm-info/ (2026-09-15)
- S67 https://www.koyfin.com/llm-info/ (2026-07-27)
- S68 https://takeprofit.com/ (acc.)
- S69 https://takeprofit.com/monetization (acc.)
- S70 https://takeprofit.com/posts/the-best-tradingview-alternative-for-real-time-us-stock-data-in-2026-95 (2026-08-17)
- S71 https://takeprofit.com/docs/indie/What-is-Indie (acc.)
- S72 https://businessconnectindia.in/best-tradingview-alternative-for-trading/ (2026-04-24; claims a "15% platform fee" for Paid Spaces, which conflicts with S3/S23)
- S73 https://coruzant.com/fintech/creator-economy-for-traders-platforms/ (2026-03-10)
- S74 https://www.luxalgo.com/blog/luxalgo-charting-platform/ (2026-08-31)
- S75 https://www.luxalgo.com/features/charts/ (acc.)
- S76 https://www.luxalgo.com/pricing/ (acc.)
- S77 https://www.luxalgo.com/about/ (acc.)
- S78 https://www.luxalgo.com/blog/run-pine-script-outside-tradingview/ (2026-09-22)
- S79 https://github.com/LuxAlgo/PineTS (acc.)
- S80 https://docs.luxalgo.com/platform/algos/access-on-tradingview (acc.)
- S81 https://docs.luxalgo.com/docs/getting-started/faq (acc.)
- S82 https://pineforge.dev/en/faq/ (acc.)
- S83 https://pynesys.io/ (acc.)
- S84 https://pynecore.org/ and https://pypi.org/project/pynesys-pynecore/ (search excerpt)
- S85 https://algoalpha.io/ and https://algoalpha.io/pricing (acc.)
- S86 https://algoalpha.io/blog/algoalpha-vs-luxalgo-2026-comparison (2026-06-07)
- S87 https://chartprime.com/ (acc.)
- S88 https://www.zeiierman.com/ (acc.)
- S89 https://bigbeluga.ai/ (acc.; bigbeluga.com redirects to a GoDaddy for-sale page)
- S90 https://marketciphertrading.com/pricing/ (acc.)
- S91 https://www.tradingalpha.io/ (acc.)
- S92 https://www.quantvue.io/pricing (acc.)
- S93 https://smrtalgo.com/ (acc.)
- S94 https://www.fluxcharts.com/ (acc.)
- S95 https://www.patreon.com/jdehorty/posts/important-update-143430324 (search excerpt; 2025-12-07)
- S96 https://www.ruzuku.com/learn/articles/whop-pricing (updated 2026-09-13)
- S97 https://dodopayments.com/blogs/whop-fees-explained (2026-03-11)
- S98 https://whop.com/blog/selling-tradingview-indicators/ (2023-09-20)
- S99 https://stat-map.com/resources/how-to-claim-access-to-tradingview-indicators-on-whop (2025-01-22)
- S100 https://gumroad.com/pricing (acc.)
- S101 https://www.launchpass.com/ (acc.)
- S102 https://stripe.com/pricing (acc.)
- S103 https://github.com/trendoscope-algorithms/Tradingview-Access-Management/ (acc.)
- S105 https://www.pineconnector.com/ (acc.)
- S106 https://www.pineconnector.com/pages/pricing (acc.)
- S107 https://traderspost.io/pricing (acc.)
- S108 https://traderspost.io/ (acc.)
- S109 https://docs.traderspost.io/docs/core-concepts/webhooks (acc.)
- S110 https://3commas.io/pricing (acc.)
- S111 https://3commas.io/signal-bot (acc.)
- S112 https://wundertrading.com/en/pricing (acc.)
- S113 https://alertatron.com/ (acc.)
- S114 https://tickerly.net/ (acc.)
- S115 https://pickmytrade.io/pricing (acc.)
- S116 https://crosstrade.io/pricing (acc.)
