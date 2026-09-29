# Market Data Licensing & Charting Library Research: Web Charting Platform (TradingView competitor)

> Research notes compiled on 29 September 2026. They are the evidence behind [the teardown](../tradingview-teardown.md). Claims keep the labels used during research (VERIFIED, UNVERIFIED, NOT FOUND and similar). Punctuation was normalized afterwards; the wording is otherwise as researched.

**Research date:** 2026-09-29. Every source was accessed on that date; a document's own date is given where it shows one.

**How claims are labelled**
- **VERIFIED:** I read it on the cited primary page or document.
- **UNVERIFIED:** it comes from a search snippet, a third party or my own inference.
- **NOT PUBLISHED:** no public price exists; the contact is named.
- **Estimates** are my arithmetic on VERIFIED list prices. They exclude vendor feed fees, connectivity, taxes and audit exposure.

**Limits on this research**
- cmegroup.com blocks automated access. It returned 403 citing its website terms, so I did not work around it. CME figures come from the CME fee list copy hosted by Databento [S1] and from CME forms hosted by brokers [S2].
- The session's web-search quota ran out partway through. The rest of the work used direct page fetches.
- Some pages could not be read: Binance's current Terms, Bybit's full API T&C, Barchart, Schwab's developer portal and the Nasdaq Data Link product page.

---

## Key findings

1. **CME real-time data is the biggest cost.** VERIFIED [S1]
   - To distribute all four CME Group exchanges you need four real-time distribution licences at $29,280/yr each, about $9,760/mo in total. The fee list says "fees are assessed per exchange".
   - On top of that, each non-pro user costs $4.65/mo (top-of-book bundle) or $36.50/mo (depth bundle).
2. **CME's non-professional definition may exclude a charting-only site.** It requires "an active futures trading account" and access through a terminal "capable of routing orders to the CME Globex Platform". VERIFIED [S2]. Sierra Chart requires a funded futures account plus a monthly connection to it for non-pro CME data (Oct 2025, VERIFIED [S3]).
3. **Delayed CME data is not free for a distributor.** The delayed distribution licence is $21,840/yr per exchange; the per-device fee is $0. VERIFIED [S1]
4. **US stocks**
   - The cheapest official real-time options are Cboe One Summary ($0.25/user) and Nasdaq Basic ($1.00/user plus $2,140/mo). VERIFIED [S19][S20]
   - The full SIP costs $3/user plus about $6,500/mo fixed until 2027-03-31.
   - The SIP is replaced by the **CT Plan on 2027-04-01**. New agreements must be signed by 2027-03-01. Non-pro fees become tiered from $0.90 down to $0.25 per tape, and delayed redistribution stops being fee-liable. VERIFIED [S17][S18]
5. **Crypto exchanges' free public APIs are not licensed for commercial display.** Coinbase, OKX and Kraken require written consent or a licence (VERIFIED). Binance's terms, last read in their 2021 wording, bar profiting from its data without consent (UNVERIFIED as current). A licensed aggregator is the practical route: CoinAPI permits display in your app on any paid plan from $79/mo.
6. **TradingView's free Advanced Charts licence cannot be used for this product.** It is "a free offering only" and forbids using the library "to develop any competing offerings". VERIFIED [S53]. Lightweight Charts (Apache-2.0) is usable but has no built-in drawing tools or indicators. KLineChart (Apache-2.0) ships with 28 indicators and 16 drawing overlays.
7. **Letting users bring their own broker/data account moves exchange fees to the user's broker.** The broker and vendor API terms become the constraint instead. For example, the NinjaTrader/Tradovate API licence bars using the API "to build a competitive product or service".
8. **TradingView itself does not avoid exchange licensing.** Its broker verification only stops it charging the user a second time. VERIFIED [S8][S10]
9. **Market context: TradingView now charges invite-only script vendors.** Section 22A of its Terms of Use sets a "Technology Fee" of **US$29.95 per user per month** once a vendor has more than 100 users. VERIFIED [S10]. This bears directly on your paid-Pine-indicator audience.

---

## Table 1: Estimated monthly data cost per non-professional user (real-time unless noted)

| Asset class / source | Fixed monthly fees | Per-user fee | Est. per user, 1,000 users | Est. per user, 10,000 users | Basis |
|---|---|---|---|---|---|
| CME Group, all 4 exchanges, top of book | $9,760 (4 × $29,280/yr). Add $2,440 if the $610/mo real-time data-feed fee applies per exchange | $4.65 | $14.41 (up to $16.85) | $5.63 (up to $5.87) | Estimate from [S1] |
| CME Group, all 4 exchanges, depth of market | $9,760 | $36.50 | $46.26 | $37.48 | Estimate [S1] |
| CME + CBOT only (ES, NQ, RTY, YM), top of book | $4,880 | $3.10 | $7.98 | $3.59 | Estimate [S1] |
| CME delayed (10 min+), all 4 exchanges | $7,280 | $0 | $7.28 | $0.73 | Estimate [S1] |
| US stocks: Cboe One Summary | $5,000 distributor fee (user fees credited against it) + $1,000 consolidation fee | $0.25 | $6.00 ($1.25 during the 12-month vendor waiver) | $0.60 ($0.35 during waiver) | Estimate [S20] |
| US stocks: Nasdaq Basic (Nasdaq, NYSE and NYSE American listings) | $2,140 | $1.00 | $3.14 | $1.21 | Estimate [S19] |
| US stocks: full SIP, legacy (until 2027-03-31) | about $6,500 (3 × $1,000 redistribution + indirect access fees) | $3.00 | $9.50 | $3.65 | Estimate [S15][S16] |
| US stocks: full SIP, CT Plan (from 2027-04-01) | about $7,505 (3 × $1,155 + indirect access fees) | $2.70 for the first 2,000 users, then $2.25 | $10.21 | $3.09 | Estimate [S17][S18] |
| US stocks: 15-minute delayed SIP | Legacy about $271 (UTP $250/mo + $250/yr); CT Plan $0 | $0 | $0.27 | $0.03 | Estimate [S16][S17] |
| US stocks: vendor derived price, "no exchange fees" (Massive Stocks Business) | $2,499 (vendor fee) | $0 | $2.50 | $0.25 | Estimate [S22] |
| Crypto via licensed aggregator (CoinAPI Streamer or Pro) | $249 to $599 (vendor fee) | $0 | $0.25 to $0.60 | $0.02 to $0.06 | Estimate [S35]. Direct exchange licences NOT PUBLISHED |
| Forex, over-the-counter (Twelde Data business plans) | $149 to $1,099 (vendor fee) | $0 | $0.15 to $1.10 | $0.01 to $0.11 | Estimate [S24] |

**How to read this table**
- Vendor feed fees are extra in every exchange row. Examples: Databento Plus is $1,750/mo for CME external distribution; Massive's Nasdaq Basic add-on is $1,999/mo.
- **TradingView's retail benchmark** (VERIFIED [S6][S7]):
  - CME Group bundle (E-mini included): **$9.95/mo** non-pro, $548/mo pro.
  - US stock bundle: $9.95/mo non-pro.
  - NASDAQ, NYSE and NYSE Arca: $3/mo each non-pro.
  - OTC: $8/mo non-pro.
  - Cboe One: $0.
  - CME data is free with a 10-minute delay.
  - Third-party sites cite $7/mo for the CME bundle (UNVERIFIED).

---

## 1. Crypto

### Exchange terms

| Exchange | Commercial display to your users | Attribution rule | Status |
|---|---|---|---|
| **Coinbase** (Market Data Terms, last updated 2026-08-07) | Use is limited to "personal or research purposes" and "may not be used to build an application intended for use by end users". Data and derived charts may not be displayed to third parties without "prior express written consent". Coinbase lists authorised redistribution partners: Amberdata, CCData, Coin Metrics, CoinRoutes, Lukka, Massive, DAR, NinjaTrader, Architect, Kaiko, Tardis.dev. | None stated | VERIFIED [S30]. The terms are written for the Exchange Market Data API; whether they also govern Advanced Trade's public endpoints is UNVERIFIED |
| **OKX** (API Agreement, 2026-07-28) | "Personal, non-commercial" use only. No display to any third party without prior written consent. May not be used to build an "analytics platform". Being publicly accessible "does not grant any right". Commercial use needs a separate data licence. | None | VERIFIED [S31] |
| **Kraken** | Prior permission is required for "any non-personal commercial use of data from publicly accessible endpoints". Contact marketdata@kraken.com. Kraken's Terms of Service (2026-09-14) also bar third-party apps built on its content without consent. | None | VERIFIED [S32] |
| **Binance** | Terms §III.1.b.iv prohibit, without written consent, "data feeding or streaming services that make use of any market data of Binance" and sites or apps that "charge for or otherwise profit from market data obtained from Binance". The API terms page (modified 2026-09-28) defers to the main Product Terms. | None found | **UNVERIFIED as current wording** (text quoted from the 2021 version) [S33] |
| **Bybit** (API T&C, last updated 2026-01-16) | A search snippet says users "shall not commercially exploit the APIs". The full text could not be retrieved. | None found | UNVERIFIED [S34] |

### Paid aggregators

| Provider | Price | Can you show the data to your users? | Status |
|---|---|---|---|
| CoinAPI | Pay-as-you-go; Startup $79/mo; Streamer $249/mo; Pro $599/mo (annual billing $69 / $199 / $499); Enterprise custom | "Displaying real-time and historical data in your UI is fully permitted with any paid plan." Raw-data redistribution is not allowed on any plan and no licence for it is sold. | VERIFIED [S35] |
| Amberdata | $5,000/yr per exchange data subscription | The standard licence allows commercial use, but "redistribution, reselling or sublicensing... strictly prohibited". A custom licence is available through sales. | VERIFIED [S40] |
| Kaiko | NOT PUBLISHED (custom plans). A third-party estimate of $12k to $55k/yr is UNVERIFIED. Contact Kaiko sales. | Licence types: standard, indices, custom | VERIFIED [S38] |
| CoinDesk Data (formerly CCData/CryptoCompare) | NOT PUBLISHED. The free Personal plan is CC BY-NC-SA 4.0 (non-commercial). Commercial and Bespoke plans go through sales. | Commercial plan carries a "predefined business/commercial license agreement" | VERIFIED [S39] |
| CoinGecko | Basic $35 ($29 billed annually); Analyst $129; Lite $499; Pro $999/mo | Commercial use allowed. **Attribution required: "Data provided by CoinGecko" with a link.** No resale or redistribution of the API; Enterprise plan has a redistribution licence. Prices are aggregated, not per-exchange. | VERIFIED [S36] |
| CoinMarketCap | Builder $29; Startup $79; Growth $299; Professional $699/mo | Commercial use in your own product, up to 100k users per product. No standalone redistribution. | VERIFIED [S37] |

**Caveat.** An aggregator's display rights are only as good as its own agreements with the exchanges. Get warranties or indemnities from the aggregator (my recommendation).

---

## 2. US equities

### Consolidated tape (SIP)

**Legacy CTA/UTP plans, in force until 2027-03-31**

| | CTA (Networks A and B) [S15] | UTP (Tape C, Sept 2023 policies) [S16] |
|---|---|---|
| Non-pro fee | $1.00/mo per network | $1.00/mo, "licensed only for personal use" |
| Professional fee | Network A $45 / $27 / $23 / $19 by tier; Network B $23 | $24 |
| Redistribution fee | $1,000/mo per network | External real-time redistributor $1,000/mo |
| Access fees (monthly) | Direct: A last sale $1,250, bid-ask $1,750; B last sale $750, bid-ask $1,250. Indirect: A $750 / $1,250; B $400 / $600 | Direct $2,500; Indirect $500 |
| Delayed data | No delayed-fee line appears in the schedule; my reading that delayed is free is UNVERIFIED | 15-minute delay; subscriber fees "not fee liable"; external delayed redistributor $250/mo plus $250/yr admin; a delay message must be shown |

The CTA schedule is undated. Both sets are VERIFIED.

**CT Plan, from 2027-04-01** (SEC Release 34-105778, 2026-06-26): VERIFIED [S17][S18]
- **Timeline:** licensing portal opens 2026-10-01; agreements due 2027-03-01; plan goes live 2027-04-01.
- **Non-pro fee per tape**, applied like tax brackets:

  | Users | Fee per user per tape |
  |---|---|
  | 1 to 2,000 | $0.90 |
  | 2,001 to 50,000 | $0.75 |
  | 50,001 to 250,000 | $0.60 |
  | 250,001 to 1,000,000 | $0.40 |
  | Over 1,000,000 | $0.25 |

- **Professional fees:** Tape A $26 flat, Tape B $23, Tape C $24.
- **Real-time redistributor:** $1,155 per tape.
- **Indirect access fees:**
  - Last sale: A $865, B $460, C $230.
  - Bid-ask: A $1,445, B $695, C $345.
- **Delayed and end-of-day:** redistribution "is not fee liable on any Tape but still must be explicitly licensed".
- **Service facilitators:** a named exemption category.

### Exchange feeds

**Nasdaq Basic** (SR-NASDAQ-2026-076, Equity 7 §147): VERIFIED [S19]
- **Non-pro per user:** $0.50 for Nasdaq-listed, $0.25 for NYSE-listed and $0.25 for NYSE American-listed; $1.00 for Nasdaq Basic Plus.
- **Professional per user (2026):** $14.10 Nasdaq-listed; $7.20 each for the other two.
- **Distributor fee (2026):** external $2,140/mo, rising to $2,170 in 2027.
- **Other options:**
  - Derived data to unlimited non-pros: +$1,500/mo.
  - Media Enterprise licence: $100,000/mo.
- **Access through Nasdaq Data Link APIs:** pricing NOT PUBLISHED; contact Nasdaq.

**Cboe One** (price list v2026-07-30): VERIFIED [S20]
- **Summary feed:** external distribution $5,000/mo; non-pro $0.25; professional $10; data consolidation $1,000; Digital Media $15,000; Enterprise $50,000.
  - User fees are credited against the distributor fee.
  - A Data Vendor Waiver Program gives a **12-month distribution-fee waiver** to new vendors integrating the feed.
  - There is a 30-day trial.
  - A Small Retail Broker programme ($3,500 + $350) is limited to broker-dealers.
- **Premium feed:** non-pro $0.50; external distribution $12,500.

**NYSE BQT** (pricing guide dated 2026-05-14): VERIFIED [S21]
- Non-pro $1.00; professional $18; access $6,250/mo or $850 per-user access for display-only vendors; redistribution $2,500/mo; Enterprise $50,000; Digital Media $65,000.
- NYSE BBO and NYSE Trades are $0.20 non-pro each.

**Delayed proprietary feeds:** Nasdaq's and NYSE's delayed-data policies were not verified. Intrinio says its Cboe One Delayed feed has "no exchange fees" [S27].

### Vendors

| Vendor | Can you redistribute to your users, and at what tier | Status |
|---|---|---|
| **Massive** (Polygon.io renamed 2025-10-30 4 PM ET; api.polygon.io still works) | Individual plans are "Individual use, Non-pros only": Starter $29 and Developer $79 (15-min delayed), Advanced $199 (real-time). **Stocks Business $2,499/mo**: real-time derived "fair market value" price, "No Exchange Fees or Approvals". Exchange-feed add-ons at $1,999/mo each (Nasdaq Basic, Cboe EDGX, Full Market), IEX $499, Full Market Delayed $499, all with "additional exchange fees". Startups get 25%+ off the first year. | VERIFIED [S22] |
| **Databento** | Standard $199/mo; **Plus $1,750/mo (annual contract) adds "External distribution"**; Unlimited $4,500/mo. Exchange licence fees passed through "with no upcharge". Its US Equities Mini dataset supports external redistribution without per-user fees (blog 2025-02-01). Which plan tier that requires is UNVERIFIED. | VERIFIED [S11][S13] |
| **Alpaca** | Algo Trader Plus $99/mo is for the individual account holder. Broker API (for broker partners): tiers from Standard (included) to StandardPlus10000 $2,000/mo; all tiers are "real time IEX or 15 mins delayed SIP". | VERIFIED [S23] |
| **Twelve Data** | Individual plans are "personal, internal and non-commercial". **Venture from $149/mo includes external display**; Enterprise from $1,099/mo includes external distribution; Enterprise+ adds white-labelling. | VERIFIED [S24] |
| **Finnhub** | Free and All-in-One ($3,500/mo, billed annually) both say "Personal Use". Commercial licence NOT PUBLISHED; contact support@finnhub.io. | VERIFIED [S25] |
| **Tiingo** | $30/$50 plans are internal use only. **Display redistribution: $250/mo (startups) or $500/mo (enterprise)**, covering end-of-day and IEX data. | VERIFIED [S26] |
| **Intrinio** | Individual $150/mo; Startup $333/mo; Enterprise $1,250+/mo. EquitiesEdge (derived price, "no exchange fees") is on all plans. Nasdaq Basic, IEX and delayed SIP are Enterprise-only. Delayed SIP display costs "$250/year admin fee plus an additional $250/mo". | VERIFIED [S27] |
| **EODHD** | $19.99 to $99.99/mo plans are personal use; live prices are 15-min delayed. Commercial use goes through a "Startups & Enterprise" plan (contact). | VERIFIED [S28] |

---

## 3. US futures (CME Group)

### Fee list effective 2026-01-01 (per exchange): VERIFIED [S1]

- **Distribution licences (annual):** real-time $29,280; delayed $21,840; historical $35,220. If you hold both real-time and delayed, only the real-time fee applies.
- **Display device fees (monthly):**

  | Package | Per exchange | Bundle, all 4 exchanges |
  |---|---|---|
  | Non-pro top of book | $1.55 | $4.65 |
  | Non-pro depth of market | $12.10 | $36.50 |
  | Professional real-time | $134.50 | n/a |
  | Delayed | $0 | n/a |

- **Data feed fees (monthly):** real-time $610; delayed $304.
- **Public Website licence:** $487/mo, for delayed and historical data only. Whether a paid platform that requires login qualifies is UNVERIFIED.
- **Non-display fees** start at $609/mo (Category A, one application). Server-side alerts or scripts might fall here; that classification is UNVERIFIED.
- The list says it "does not include all licensing options"; contact marketdata@cmegroup.com.
- 2025 fees were top of book $1.50 and depth $11.70 (UNVERIFIED, from a search snippet).

### Rules

- **Timing categories:**
  - Real-time: within 10 minutes.
  - Delayed: 10 minutes to 8 hours.
  - Historical: more than 8 hours.

  VERIFIED via [S4] (2024-04-22).
- **Non-pro criteria:** CME's non-pro definition includes a futures account and an order-routing-capable terminal, with at most two per distributor (VERIFIED [S2], 2023 copies). TradingView's own non-pro criteria do not mention a futures account [S10]. Whether CME grants TradingView an exception is **UNVERIFIED**; ask CME.

### How distributors handle it

- **Databento:** passes CME fees through. Non-pro depth bundle is $36.50 (2023-06-04 announcement [S12]). External distribution requires Plus [S11]. Whether you also need your own CME Information License Agreement is UNVERIFIED but likely.
- **dxFeed:** sells directly to users of Quantower, NinjaTrader, ATAS, MotiveWave and Bookmap, with pro/non-pro self-certification. Its order page lists CME Group top of book at $39/mo and depth at $99/mo. Which status those prices apply to is unclear (UNVERIFIED) [S14].
- **CQG and Rithmic:** delivered through futures brokers (FCMs). StoneX's retail pass-through is $2 per exchange or $6 bundle for Level 1, and $13 per exchange or $39 bundle for Level 2, plus a 10% admin fee. VERIFIED [S5]
- **Barchart:** NOT VERIFIED (page not retrievable); contact Barchart.

---

## 4. Forex and CFDs

Spot FX is traded over the counter, so there are no exchange fees. Licensing is contractual with the vendor or broker.

- **OANDA**: VERIFIED [S41]
  - The v20 trading API issues a personal token once the account holder accepts the API licence.
  - The commercial Exchange Rates API costs $450, $840, $1,160 or $1,680 per month or $4,850 to $17,000 per year. Streaming only comes from Premium Plus up. Rates "update every five seconds".
  - Redisplay is sold separately ("Redisplay Solutions"): NOT PUBLISHED; contact OANDA FX Data Services.
- **FXCM**: VERIFIED [S42]
  - Its APIs are free for account holders; the FIX API needs a $5,000 minimum balance.
  - GitHub historical data is "for personal use".
  - Redistribution: NOT PUBLISHED.
- **Twelve Data:** business plans as above [S24].
- **Massive currencies:** Starter $49/mo for real-time forex and crypto, "Individual use". Business pricing NOT PUBLISHED; contact sales@massive.com [S22].
- **TraderMade:** FX & Crypto £599/mo ("Business Use"); CFDs £599/mo (40 symbols). Redistribution and white-labelling are Enterprise only, custom priced [S43].

---

## 5. "Bring your own data" (user's own broker or data account)

### How the desktop platforms do it: VERIFIED

- MotiveWave: "Data is not included"; it lists 30+ supported brokers and data feeds [S48].
- Quantower: $70/mo All-in-One; its licence "does not include third-party market data that must be purchased additionally" [S47].
- Sierra Chart: "you will have to pay exchange fees" whichever data service you use [S49].
- ATAS: lower-tier plans cannot connect real-time futures data [S50].

### Does it avoid distributor licensing?: UNVERIFIED legal inference

- **Probably yes, if data never touches your servers.** That means the user's browser connects directly to the broker or vendor under the user's own entitlement, so the broker or vendor stays the licensed distributor and reports the user.
- **Probably no, if your servers ingest data.** Proxying, history caches, server-side alerts, screeners or script execution make you a redistributor and non-display fees likely apply.
- The CT Plan has a "Service Facilitator" exemption [S18]. Get written confirmation from CME and each data source before relying on any of this.

### What each vendor requires

- **Rithmic:** "Conformance testing required before production access". Its R|Protocol API works in any language and is aimed at "Web, mobile, cloud". Fees NOT PUBLISHED; request through rithmic.com's API contact form. [S44]
- **CQG:** Client APIs are "available to individual users" and must run on the same machine as CQG IC. Enterprise APIs (Web API: protobuf over WebSocket) are "limited to Enterprise systems for use by multiple users". Fees NOT PUBLISHED; contact CQG partners. [S45]
- **Tradovate / NinjaTrader** (NinjaTrader API License Agreement, September 2026) [S46]:
  - Individual API use requires a live account with more than $1,000 equity plus an "API Access" subscription (price not found).
  - The licence allows you to display market data to "Customers" through your app.
  - It prohibits:
    - resale or redistribution;
    - using the API "to build a competitive product or service";
    - steering customers to competing brokers;
    - GPL, LGPL or AGPL code.
  - Cached data must be refreshed or deleted within 24 hours, and exchanges get audit rights.
- **Alpaca:** see the vendor table [S23].
- **Interactive Brokers, Tradier, Schwab:** NOT VERIFIED in this session.
- **Crypto API keys:** public data needs no key, but the exchange terms above still apply.

### What TradingView gets through broker integrations: VERIFIED [S8][S10]

- TradingView calls itself "a vendor of official real-time market data from exchanges".
- Users who already pay for data at a supported broker connect in the Trading Panel. Verification lasts 7 days and renews each time they log in.
- Supported CME brokers include AMP, Ironbeam, Dorman, Optimus, StoneX, EdgeClear, Tradier Futures, Tradovate, NinjaTrader, IB, tastytrade, TradeStation and Webull.
- This only stops TradingView charging the user twice; TradingView still streams from its own licensed feed. How it settles this with the exchanges is NOT PUBLISHED.

---

## 6. Charting libraries

### Table 2: Library options

| Library | Version (release date) | Licence and cost | Drawing tools | Indicators | Large datasets | Status |
|---|---|---|---|---|---|---|
| **TradingView Lightweight Charts** | 5.2.1 (2026-08-12) | Apache-2.0, free. Must show the NOTICE ("TradingView Lightweight Charts™ Copyright (c) 2025 TradingView, Inc.") and a link to tradingview.com; the `attributionLogo` option satisfies the link. | None built in; you build them as plugins | None built in; examples only | 35 KB; multi-pane since v5; data conflation since v5.1 | VERIFIED [S51][S52][S60] |
| **TradingView Advanced Charts** | n/a | Proprietary; free with TradingView logo. Companies only, public web projects only. Agreement v.0626.FAC (2026-06): "free offering only", no "competing offerings", own data feed, must post a TradingView blog/promotion. | 80 to 110+ | 100+ | 670 KB | VERIFIED [S52][S53]: **not usable for this product** |
| **TradingView Trading Platform** | n/a | Paid; price NOT PUBLISHED. Must connect to a broker back-end. Licensing to a competitor is UNVERIFIED; contact TradingView. | 110+ | 100+ | 900 KB | Partly VERIFIED [S52] |
| **KLineChart** | 10.0.3 (2026-08-27) | Apache-2.0, free | 16 overlays (rays, segments, parallel lines, price channel, Fibonacci, brush, annotations) plus custom | 28 (MA, EMA, MACD, BOLL, RSI, KDJ, SAR, OBV…) plus custom | about 40 KB gzipped; performance at 100k bars untested | VERIFIED [S54][S60] |
| **SciChart.js** | 6.0.1 (2026-09-24) | 2D licence $1,349.66/yr per developer ($809.80 to $1,012.25/yr on multi-year terms); covers up to 15,000 end users and 5 web apps. Free Community edition is non-commercial only. | Annotations; full drawing set UNVERIFIED | UNVERIFIED | WebGL | Prices VERIFIED [S55] |
| **Highcharts Stock** | 13.1.1 (2026-09-20) | $366/seat Core plus $366/seat Stock. A SaaS licence covers 1 external app, SaaS+ covers 5. | "Stock Tools" annotation interface | 40+ | WebGL boost module, "millions of points" | VERIFIED [S56] |
| **ChartIQ** | n/a | Owned by S&P Global Market Intelligence (chartiq.com redirects there). Pricing NOT PUBLISHED. | UNVERIFIED | UNVERIFIED | n/a | VERIFIED ownership only [S57] |
| **Apache ECharts** | 6.1.0 (2026-05-19) | Apache-2.0, free | None | None | Incremental rendering, "millions of data points" | VERIFIED [S58] |
| **LightningChart JS Trader** | 4.1.2 (2026-06-10) | SaaS licence "from $2,750" (startup, 1 developer, 1 project); app licence from $3,500. Its FAQ says trading charts need a sales contact. | UNVERIFIED | UNVERIFIED | Vendor claims "millions or billions" of points | Partly VERIFIED [S59] |
| **DXcharts Lite** (Devexperts) | 2.7.37 (2026-09-22) | MPL-2.0; full DXcharts is commercial, pricing NOT PUBLISHED | UNVERIFIED | UNVERIFIED | n/a | Licence VERIFIED [S60] |

### Pine Script compatibility

- PineTS 0.10.0 (2026-09-25) is "an open-source transpiler and runtime" for running Pine Script in Node.js and the browser.
- It is licensed **AGPL-3.0-only**, which is a problem for a closed-source SaaS. It would also violate the NinjaTrader API licence's ban on copyleft code. VERIFIED [S60]
- TradingView's Terms of Use prohibit "creating derivative works" of its software [S10]. Get legal review before offering Pine compatibility.

---

## Next steps

1. **Launch mix to consider:**
   - Crypto through a licensed aggregator such as CoinAPI or a Coinbase-authorised partner.
   - FX through Twelve Data Venture or TraderMade.
   - US stocks through Cboe One (claim the vendor waiver), adding Nasdaq Basic later.
   - CME through bring-your-own-data (Rithmic, Tradovate or CQG partnerships) until the roughly $9,760/mo fixed CME licence is justified.
   - Sell real-time CME as a pass-through add-on, as TradingView does.
2. **Written confirmations to obtain:**
   - From CME (marketdata@cmegroup.com): non-pro eligibility without order routing; whether Public Website or historical display applies; how "per exchange" fees are counted.
   - From Cboe: the Data Vendor Waiver.
   - From the CT Plan administrator: sign the new agreements before 2027-03-01.
3. **Charting:** benchmark KLineChart, Lightweight Charts, Highcharts Stock and SciChart at 100k+ bars. Avoid TradingView Advanced Charts.

---

## Sources (all accessed 2026-09-29; document dates in brackets)

- **S1** CME Group Fee List [eff. 2026-01-01], Databento copy: https://api.databento.com/static/licensing/cme/cme-market-data-fee-list.pdf (original: https://www.cmegroup.com/market-data/files/january-2026-market-data-fee-list.pdf)
- **S2** CME Non-Professional definition: https://bookmap.com/agreements/cme_nonpro_pro_definition.pdf [2023-07-24]; https://assets.tastyworks.com/production/documents/cme_market_data_subscriber_agreement.pdf [2023]
- **S3** https://www.sierrachart.com/SupportBoard.php?ThreadID=102157 [2025-09-30]
- **S4** https://www.ipug.org/cme-group-are-going-to-charge-for-delayed-data/ [2024-04-22]
- **S5** https://futures.stonex.com/market-data-pricing
- **S6** https://www.tradingview.com/cme/
- **S7** https://www.tradingview.com/data-coverage/
- **S8** https://www.tradingview.com/support/solutions/43000479666-how-can-i-get-real-time-data-from-exchanges-that-i-have-already-purchased-with-my-broker/
- **S9** https://www.tradingview.com/pricing/ (Essential $12.95, Plus $29.95, Premium $59.95, Ultimate $199.95 per month billed annually)
- **S10** https://www.tradingview.com/policies/
- **S11** https://databento.com/pricing
- **S12** https://roadmap.databento.com/announcements/live-cme-data-is-now-open-to-all-users-starting-at-3265month [2023-06-04]
- **S13** https://databento.com/blog/databento-us-equities-mini-now-available [2025-02-01]
- **S14** https://get.dxfeed.com/orders/new/quantower
- **S15** https://www.nyse.com/publicdocs/ctaplan/notifications/trader-update/Schedule%20Of%20Market%20Data%20Charges.pdf
- **S16** https://www.utpplan.com/DOC/datapolicies.pdf [Sept 2023]; https://www.utpplan.com/
- **S17** https://consolidatedtape.com/fees; https://consolidatedtape.com/
- **S18** https://cdn.databp.com/tenants/datact/Order-Approving-CT-Plan-Fee-Schedule.pdf [2026-06-26]
- **S19** https://www.sec.gov/files/rules/sro/nasdaq/2026/34-106336-ex5.pdf
- **S20** https://cdn.cboe.com/resources/membership/US_Market_Data_Product_Price_List.pdf [v2026-07-30]
- **S21** https://www.nyse.com/publicdocs/nyse/data/NYSE_Market_Data_Pricing.pdf [2026-05-14]
- **S22** https://massive.com/pricing; https://massive.com/business; https://massive.com/pricing?product=currencies; https://massive.com/blog/polygon-is-now-massive [2025-10-30]
- **S23** https://docs.alpaca.markets/us/docs/about-market-data-api
- **S24** https://twelvedata.com/pricing; https://twelvedata.com/pricing-business
- **S25** https://finnhub.io/pricing
- **S26** https://www.tiingo.com/about/pricing; https://www.tiingo.com/products/iex-api
- **S27** https://intrinio.com/pricing; https://intrinio.com/financial-market-data/stock-prices-delayed-sip; https://intrinio.com/financial-market-data/nasdaq-basic
- **S28** https://eodhd.com/pricing
- **S29** https://data.nasdaq.com/databases/NB; https://www.nasdaq.com/solutions/data/nasdaq-data-link/api (503 at fetch)
- **S30** https://www.coinbase.com/legal/market_data [2026-08-07]; https://www.coinbase.com/institutional/market-data
- **S31** https://www.okx.com/en-us/help/okx-api-agreement [2026-07-28]
- **S32** https://docs-legacy.kraken.com/api/docs/guides/global-intro/; https://www.kraken.com/legal/global-terms [2026-09-14]
- **S33** https://developers.binance.com/docs/binance-spot-api-docs/PROD-TERMS-OF-USE [2026-09-28]; https://github.com/Superalgos/Superalgos/issues/1019 [2021-05-28]
- **S34** https://www.bybit.com/en/legal/service-specific-terms/API-Terms [2026-01-16]
- **S35** https://www.coinapi.io/products/market-data-api/pricing; https://www.coinapi.io/blog/coinapi-data-commercial-use-policy
- **S36** https://www.coingecko.com/en/api/pricing
- **S37** https://coinmarketcap.com/api/pricing/
- **S38** https://www.kaiko.com/about-kaiko/pricing-and-contracts
- **S39** https://developers.coindesk.com/pricing/
- **S40** https://www.amberdata.io/online-market-data-ordering-faq; https://intelligence.amberdata.com/plans
- **S41** https://www.oanda.com/foreign-exchange-data-services/en/exchange-rates-api/api-plans/; https://developer.oanda.com/rest-live-v20/introduction/
- **S42** https://www.fxcm.com/markets/algorithmic-trading/api-trading/; https://github.com/fxcm/MarketData
- **S43** https://tradermade.com/pricing
- **S44** https://www.rithmic.com/apis
- **S45** https://www.cqg.com/products/cqg-apis; https://partners.cqg.com/api-resources/web-api
- **S46** https://api.tradovate.com/ (NinjaTrader API License Agreement, Sept 2026); https://www.tradovate.com/pricing/
- **S47** https://www.quantower.com/pricing
- **S48** https://www.motivewave.com/
- **S49** https://www.sierrachart.com/index.php?page=doc/Packages.php
- **S50** https://atas.net/pricing/
- **S51** https://github.com/tradingview/lightweight-charts; https://raw.githubusercontent.com/tradingview/lightweight-charts/master/NOTICE; https://tradingview.github.io/lightweight-charts/docs/plugins/intro
- **S52** https://www.tradingview.com/free-charting-libraries/; https://www.tradingview.com/trading-platform/
- **S53** https://s3.amazonaws.com/tradingview/charting_library_license_agreement.pdf [v.0626.FAC, 2026-06-15]
- **S54** https://github.com/klinecharts/KLineChart; https://klinecharts.com/en-US/guide/indicator; https://klinecharts.com/en-US/guide/overlay
- **S55** https://www.scichart.com/shop/
- **S56** https://shop.highcharts.com/; https://www.highcharts.com/products/stock/
- **S57** https://www.chartiq.com/ (redirects to https://www.spglobal.com/marketintelligence/en/solutions/chartiq)
- **S58** https://echarts.apache.org/en/feature.html
- **S59** https://lightningchart.com/js-charts/trader/pricing/
- **S60** npm registry, https://registry.npmjs.org/ (lightweight-charts, klinecharts, echarts, highcharts, scichart, @lightningchart/lcjs-trader, @devexperts/dxcharts-lite, pinets)
