# TradingView Platform Inventory (as of 2026-09-29)

> Research notes compiled on 29 September 2026. They are the evidence behind [the teardown](../tradingview-teardown.md). Claims keep the labels used during research (VERIFIED, UNVERIFIED, NOT FOUND and similar). Punctuation was normalized afterwards; the wording is otherwise as researched.

**How to read this report.** `[V:Sx]` means VERIFIED on source Sx. Every source's URL and date is in the source list at the end. `[UNVERIFIED]` means the claim came only from a third party or is my inference. **NOT FOUND** means I searched and found no figure. All tradingview.com pages were accessed on 2026-09-29. Blog and Help Center items carry their own publication dates.

**Method note.** I used TradingView's own pages. For the pricing matrix, I parsed the page HTML so that the check and cross icons map to the right plan column. A plain text summary of that page got several gates wrong. For example, it reported Basic as ad-free and put invite-only publishing on Essential. The corrected values are below.

---

## PART 1: PLANS AND PRICING

### 1.1 Plans and prices (USD) [V:S1]

| Plan | Monthly billing | Annual billing (per month) | Annual total vs. 12× monthly | Trial |
|---|---|---|---|---|
| Basic | $0 forever | n/a | n/a | n/a |
| Essential | $14.95 | $12.95 | $155.40 vs $179.40 (save $24) | 30 days |
| Plus | $34.95 | $29.95 | $359.40 vs $419.40 (save $60) | 30 days |
| Premium | $69.95 | $59.95 | $719.40 vs $839.40 (save $120) | 30 days |
| Ultimate | $239.95 | $199.95 | $2,399.40 vs $2,879.40 (save $480) | 14 days |

- Annual billing is advertised as "save up to 17%". The cards label the annual prices "Special price" [V:S1].
- **Professional users:** "Only the Ultimate plan is available for professional users" [V:S1]. The criteria are in [V:S36]: people registered with the SEC, CFTC, FINRA, NFA and similar bodies, business use and so on.
- **Expert (hidden or legacy professional tier).** It is in the pricing page's embedded shop config at $119.95/month or $99.95/month billed annually [V:S1, page source]. It is not shown in the visible plan grid. The Help Center and Pine docs still cite Expert limits: 25K bars, 125K intrabars, 10 watchlist alerts [V:S12, S17, S28].
- **Lite:** a mobile-only plan that does not work on the web [V:S32]. Price NOT FOUND.
- **Enterprise:** for 100+ subscriptions; contact sales [V:S1].
- **Educational Partner Program:** institutions get free paid plans for their students [V:S35].
- **Broker-sponsored plans:** these are broker promotions shown on the brokers page, for example OANDA "Free TradingView plan", moomoo "Free Premium Plan" and OKX "Unlock TradingView Plus" [V:S25]. Tickmill auto-assigns Essential, Plus or Premium based on monthly trading volume (Sep 17, 2026) [V:S38].
- **iOS in-app prices** are higher than the web prices. The App Store lists Essential $21.99, Plus $43.99 and Premium $87.99, plus Essential $219.99 and Premium $879.99 (the annual items) [V:S32]. The billing period is not stated on the listing.
- **Regional pricing:** the shop config holds prices in 17 currencies. EUR, GBP and CHF use the same numbers as USD. INR examples: Essential ₹1,295/₹995 and Ultimate ₹20,795/₹17,295 [V:S1 source].
- **Payment and refunds:** cards, PayPal, Apple Pay and crypto (via Triple-A or Binance Pay) are accepted. Refunds apply to annual plans only, within 14 days and never to market data [V:S1].
- **Discounts:** the config contains Black Friday 2025 codes: Essential 30%, Plus 40%, Premium 70%, Ultimate 80% [V:S1 source]. Actual campaign terms are [UNVERIFIED].
- **Referral:** $15 credit for the referrer and a $15 coupon for the friend [V:S36].
- **Partner/affiliate program:** Essential $10/$60, Plus $25/$100, Premium $50/$120, Ultimate $200/$400 (monthly/annual sale). The program has paid out "$15M+" [V:S35].
- **Gifts:** monthly or annual plans can be gifted, to free users only [V:S36].

### 1.2 Per-plan matrix (Basic / Essential / Plus / Premium / Ultimate) [V:S1 unless noted]

| Feature | Basic | Essential | Plus | Premium | Ultimate |
|---|---|---|---|---|---|
| Charts per tab | 1 | 2 | 4 | 8 | 16 |
| Saved chart layouts | 1 | 5 | 10 | Unlimited | Unlimited |
| Indicators per chart | 2 | 5 | 10 | 25 | 50 |
| Indicator-on-indicator | 1 | 1 | 9 | 24 | 49 |
| Financials per chart | 1 | 4 | 7 | 10 | 25 |
| Custom indicator templates | 1 | Unl. | Unl. | Unl. | Unl. |
| Historical bars (intraday) | 5K | 10K | 10K | 20K | 40K |
| Parallel chart connections | 2 | 10 | 20 | 50 | 200 |
| Chart types available | 17 | 17 | 17 | 21 | 21 |
| Custom time intervals | n/a | ✓ | ✓ | ✓ | ✓ |
| Custom range bars | n/a | ✓ | ✓ | ✓ | ✓ |
| Second-based intervals | n/a | n/a | n/a | ✓ | ✓ |
| Tick-based intervals | n/a | n/a | n/a | n/a | ✓ |
| Intraday Renko/Kagi/Line Break/P&F | n/a | n/a | ✓ | ✓ | ✓ |
| Intraday custom-formula (spread) charts | n/a | n/a | ✓ | ✓ | ✓ |
| Download chart data (CSV) | n/a | n/a | ✓ | ✓ | ✓ |
| Volume Profile indicators | n/a | ✓ | ✓ | ✓ | ✓ |
| TPO, Volume footprint, Volume candles | n/a | n/a | n/a | ✓ | ✓ |
| Auto chart patterns | n/a | n/a | n/a | ✓ | ✓ |
| Candlestick patterns, auto fib, MTF, compare, dividend adjustment, extended hours, 110+ drawings, 400+ built-ins | ✓ | ✓ | ✓ | ✓ | ✓ |
| Annual / quarterly financials on chart | 7y / 8y | 20y / 8y | 20y / 8y | 20y / 8y | 20y / 8y |
| Bar Replay: daily and higher | All | All | All | All | All |
| Bar Replay: minute data | n/a | 180 days | 365 days | All | All |
| Bar Replay: second data (since Aug 2022) | n/a | n/a | n/a | All | All |
| Bar Replay: tick data | n/a | n/a | n/a | n/a | 7 days |
| Indicators replay / trading in replay | ✓ | ✓ | ✓ | ✓ | ✓ |
| Pine calculation time limit | 20s | 40s | 40s | 40s | 100s |
| Strategy advanced metrics, CSV trades, XLSX report | n/a | ✓ | ✓ | ✓ | ✓ |
| Deep Backtesting; high bar detail; each-history-tick execution | n/a | n/a | n/a | ✓ | ✓ |
| Price alerts | 3 | 20 | 100 | 400 | 1,000 |
| Technical alerts | 0 | 20 | 100 | 400 | 1,000 |
| Watchlist alerts | 0 | 0 | 0 | 2 | 15 |
| Alert duration | 1 mo | 2 mo | 2 mo | Open-ended | Open-ended |
| Webhooks | n/a | ✓ | ✓ | ✓ | ✓ |
| Multi-condition alerts; alerts on financial metrics | n/a | n/a | ✓ | ✓ | ✓ |
| Second-based alerts | n/a | n/a | n/a | ✓ | ✓ |
| Watchlists / symbols per list | 1 / 30 | Unl. / 1,000 | Unl. / 1,000 | Unl. / 1,000 | Unl. / 1,000 |
| Flag colors; watchlist import/export | 1; n/a | 7; ✓ | 7; ✓ | 7; ✓ | 7; ✓ |
| Portfolios / holdings / transactions | 1/20/2,000 | 3/50/5,000 | 4/75/5,000 | 5/100/5,000 | 7/150/5,000 |
| Fundamental Graphs date range | ≤5y | ≤5y | ≤5y | All | All |
| AI Screener requests per month | n/a | 100 | 150 | 250 | 500 |
| Screener auto-refresh (10 s / 1 min); screener export | n/a | ✓ | ✓ | ✓ | ✓ |
| Screener timeframes | D/W/M | All | All | All | All |
| Pine Screener (beta) | n/a | n/a | n/a | ✓ | ✓ |
| Max market data subscriptions | 0 | 2 | 4 | 6 | Unlimited |
| Can buy professional market data | n/a | n/a | n/a | n/a | ✓ |
| "Fastest data flow"; dedicated backup feed | n/a | ✓ | ✓ | ✓ | ✓ |
| Broker trading, paper trading, chart trading, DOM | ✓ | ✓ | ✓ | ✓ | ✓ |
| Active community contests; public contests | 0; n/a | 3; n/a | 5; n/a | 10; ✓ | 25; ✓ |
| Publish public ideas/scripts, video ideas, Minds, comments | n/a | ✓ | ✓ | ✓ | ✓ |
| Publish protected scripts | n/a | ✓ | ✓ | ✓ | ✓ |
| Publish invite-only scripts | n/a | n/a | n/a | ✓ | ✓ |
| Signature/website fields; badge | n/a; n/a | n/a; ✓ | n/a; ✓ | ✓; ✓ | ✓; ✓ |
| Ad-free (charts and social) | n/a (ads) | ✓ | ✓ | ✓ | ✓ |
| Customer support | None | Regular | Priority | Priority | First Priority |
| MCP Server access [V:S7] | n/a | ✓ | ✓ | ✓ | ✓ |
| AI Copilot add-on eligible [V:S6] | n/a | ✓ | ✓ | ✓ | ✓ |
| Sell scripts (Creator Program) [V:S22] | n/a | n/a | n/a | ✓ | ✓ |

Notes:
- All plans get web, desktop and mobile access, 100% sync, native push alerts, iOS/Android widgets, desktop multi-monitor and tab linking [V:S1].
- Support tickets are answered Monday to Friday, 4 AM to 3 PM EST [V:S1 tooltip].
- Pine request limits: 40 unique `request.*()` calls, or 64 on Ultimate. Intrabars: 100K for non-pro plans, 125K Expert, 200K Ultimate. `request.footprint()` is Premium/Ultimate only [V:S12].

### 1.3 Add-ons
- **AI Copilot:** a separate monthly add-on for paid plans, including trials. It has a monthly usage cap and cannot be used on mobile [V:S6]. The pricing-page source lists an "AI Copilot" product at **USD 7.50** and an "AI Copilot Trial" at $0 [V:S1 source]. The price is not displayed publicly, so treat $7.50/month as [UNVERIFIED as shown to buyers].
- **Paid Spaces (third-party scripts):** $4.99 to $199 per month per creator space [V:S23].
- **TradingView coins:** sold in packs of 100 to 30,000 [V:S1 source]. Their purpose is NOT FOUND.
- **Real-time market data** is billed per month, needs a paid plan or trial and can be bought on the web only [V:S1, S3, S4, S19]:

| Feed | Non-pro | Pro | Free default |
|---|---|---|---|
| US Stock Markets bundle (NYSE, NASDAQ, NYSE Arca, NASDAQ GIDS, OTC) | $9.95 (saves $12.05) | N/A | n/a |
| NYSE / NASDAQ / NYSE Arca | $3 each | $48 / $27 / $25 | Cboe One real-time $0 |
| OTC Markets / NASDAQ GIDS | $8 / $5 | $50 / N/A | 15-min |
| OPRA (US options) | $4.95 | $35 | n/a |
| CME Group bundle (CME, CBOT, COMEX, NYMEX) | $9.95 | $548 (single exchange $142) | 10-min delay |
| Eurex | $2.00 | $73 | 15-min |
| ICE Futures US / ICE Europe Commodities / ICE Endex | $139 / $152 / $152 | same | n/a |
| Cboe CFE futures; Cboe Global Indices | $9.95; $9.95 | $9.95; $9.95 | 15-min |
| LSE (UK) / Euronext bundle / Deutsche Börse Xetra+FWB | $9.95 / $9.95 / $19.95 | $64 / $135 / $101 | 15-min |
| TSX+TSXV / ASX / TSE Japan / HKEX | $19.95 / $19.95 / $9.95 / $25 | $19.95 / $107 / $17 / $25 | 15 to 20 min |
| NSE India | $0 | $0 | real-time free |
| Blue Ocean ATS (US overnight) | $9 | $9 | n/a |
| S&P DJI indices | $10 | $20 | n/a |

---

## PART 2: FEATURE INVENTORY

### 2.1 Charting (Supercharts)
- **Layouts:** up to 16 charts per tab [V:S2]. May 2025 added 12 new grid options [V:S38].
- **Chart types: 21** [V:S2]: Bars, Candles, Hollow candles, Volume candles, Line, Line with markers, Step line, Area, HLC area, Baseline, Columns, High-low, Heikin Ashi, Renko, Line break, Kagi, Point & figure, Range, Volume footprint, TPO, Session volume profile.
- **Drawing tools: 110+** in 8 categories [V:S2, S14]:
  - Cursors: cross, dot, arrow, demonstration, magic, eraser.
  - Trend tools: 9 lines, 4 channels, 4 pitchforks.
  - Fibonacci and Gann: 11 Fibonacci tools and 4 Gann tools.
  - Patterns: XABCD, Cypher, H&S, ABCD, Triangle, Three drives, Elliott waves and 3 cycle tools.
  - Forecasting and measurement: long/short position (with leverage and currency options), position forecast, bars pattern, ghost feed, sector, anchored VWAP, fixed-range VP, anchored VP, price/date ranges.
  - Geometric shapes: 10 shapes plus brush, highlighter and arrows.
  - Annotation: text, note, price note, pin, table, callout, comment, price label, signpost, image, embedded X posts/ideas.
  - Icons: emojis and stickers.
  - Utilities: measure, zoom, magnets (strong, weak, snap to indicators), keep drawing, lock, hide, sync drawings, remove.
- **Indicators:** "400+ built-in indicators and strategies" and "100,000+ public indicators" [V:S2]. The Help Center documents 209 built-in indicators and 20 built-in strategies [V:S37]. There are 6 built-in indicator templates [V:S19].
- **Candlestick pattern recognition:** 44 documented patterns [V:S37].
- **Auto chart patterns:** 16 patterns plus an "All Chart Patterns" indicator [V:S37]. Premium and above.
- **Volume tools** [V:S37]:
  - 7 Volume Profile indicators: Fixed Range, Anchored/Auto-Anchored, Session, Session HD, Visible Range, Periodic.
  - TPO and Session TPO.
  - Footprint, which has modes, table summary and alerts.
- **Timeframes** [V:S17]:
  - Seconds: 1, 5, 10, 15, 30, 45.
  - Minutes: 1, 2, 3, 5, 10, 15, 30, 45.
  - Hours: 1, 2, 3, 4.
  - D, W, M, plus custom intervals.
  - Ticks: 1T, 10T, 100T, 1000T on nearly all exchanges since May 26, 2025 [V:S38].
- **Sync:** symbol, interval, crosshair, time and date range. Drawings sync on the same symbol. Emoji-tagged sync groups [V:S19].
- **Comparison and spreads:** compare symbols; custom spread formulas using +, −, ×, ÷ [V:S19]; currency conversion; dividend adjustment.
- **Sessions:** extended hours on all plans. A 24h overnight session is available for BOATS-supported US stocks (Jul 9, 2026) [V:S38].
- **Workspace tools:** timezone selection; price scale modes (log, percent, indexed to 100, inverted, auto, manual); object tree and data window (floating under the cursor since Jun 30, 2025) [V:S5].
- **Table views:** chart "table view" (Sep 30, 2025); Pine tables can move to a bottom panel (Sep 15, 2026) [V:S38].
- **Workflow:** command/quick search, keyboard shortcuts, snapshots, layout share links, autosave [V:S2, S14, S19]. Event markers on the chart for earnings, dividends, splits, economic events and news [V:S14].
- **Seasonals:** launched Jan 8, 2025; average line and table view added later [V:S30, S5].
- **Bar Replay:** 9 speeds, autoplay and step, selectable update intervals (1-second option added Aug 2025), random bar, synchronized multi-chart replay and trading in replay [V:S2, S5, S38].

### 2.2 Pine Script ecosystem
- **Version:** v6, released Dec 10, 2024, with a v6 conversion tool [V:S38]. Additions since then [V:S11]:
  - Feb 2025: `bid`/`ask` variables; the scope limit was removed.
  - Aug 2025: strings raised to 40,960 characters.
  - Jan 2026: `request.footprint()`.
  - Apr 2026: multiline strings and sorting of user-defined types.
  - Aug 2026: `once` keyword.
- **Pine Editor:** a cloud IDE that moved to the side panel in Aug 2025. It has autocomplete, a VS Code-style command palette, version history, word wrap and auto-parentheses (Jul 2026) [V:S2, S11]. **Pine Logs** and **Pine Profiler** are included [V:S2].
- **Libraries** can export functions, types, methods and constants. A script can import up to 1M tokens of libraries [V:S11, S12].
- **Publishing:**
  - Privacy: public or private. Visibility: open, protected (paid plans) or invite-only (Premium and above). Open source defaults to MPL 2.0. Public scripts can be edited for 15 minutes only [V:S13].
  - Since Aug 14, 2026, scripts are moderated before they reach feeds. Outcomes are Suggested, Profile-only or Hidden. Limits are 5 public scripts per 24h and 15 per 30 days [V:S23].
- **Limits** [V:S12]:
  - Compile 2 minutes; loops 500 ms per bar.
  - 64 plots; 500 lines, boxes and labels; 100 polylines; 9 tables.
  - 127 tuple elements; 100,256 tokens per script; 5 MB compile request.
  - 1,000 variables per scope; collections of 100K elements.
  - History buffer 5,000 bars (10,000 for OHLC and time).
  - Drawings up to 10K bars back and 500 bars forward.
  - 9,000 orders per backtest or 1,000,000 with Deep Backtesting.
- **Strategy report** (renamed from Strategy Tester in Jul 2026) [V:S11, S13, S18]:
  - Metrics tab: key stats, returns, trades analysis, run-ups/drawdowns, capital efficiency. Trades tab.
  - The Help Center documents 53 metric definitions [V:S37].
  - Deep Backtesting runs on any date range, up to 2M bars per calculation.
  - "Bar detalization" (formerly Bar Magnifier) uses intrabar data, for example 60m→10m and 1D→60m.
  - Other settings: every-history-tick execution, leverage inputs, Heikin Ashi mode, limit-fill assumptions, execution delay.
- **Pine Screener (beta, Premium and above)** [V:S16]:
  - Source: a watchlist or an index. The Help Center and release notes say up to 4,000 symbols; the Sep 1, 2026 blog says 3,500.
  - One indicator per screen; 10 fixed timeframes (1m to 1M); ≤5 `request.*()` calls; last 500 bars; no custom timeframes.
- **Monetization and community** [V:S22, S23, S38]:
  - Paid Spaces/Marketplace launched Nov 13, 2025. By Aug 2026 there were 39 creators and 1,000+ applicants.
  - Up to 50 scripts per space. Platform fee is currently 0%, locked for spaces approved before Apr 1, 2026. Payouts monthly via PayPal, $100 minimum. Creators must be on Premium or Ultimate.
  - Pine freelancers directory; Wizards program.
  - Editors' Picks: a 2023 pilot paid $100 per pick. Current status [UNVERIFIED].

### 2.3 Alerts
- **Types:** price, technical and watchlist [V:S15].
  - 13 built-in price conditions [V:S2].
  - Alerts can be set on indicators, strategies, drawings (rectangles with >/<, Fibonacci, long/short positions), chart patterns, TPO levels, footprint, financial and valuation metrics and news flows [V:S5, S28].
  - Multi-condition alerts: up to 5 conditions; each counts as one technical alert; Plus and above (Oct 23, 2025) [V:S28].
  - Watchlist alerts track symbols added to the list later and support extended hours [V:S15].
  - Pine `alert()` and `alertcondition()` [V:S13].
- **Channels:** app push, toast/popup, email, webhook, sound (40 sounds) and a "plain text" option (a free way to send text messages to your phone) [V:S15, S28].
- **Automation and scheduling:** alerts run server-side. Notification schedules (Jul 7, 2026) also mute webhooks. Up to 5 presets. News alerts on up to 10 flows for paid plans [V:S28].
- **Webhook rules:** 2FA required; ports 80 and 443 only; 3-second timeout; IPv4 only; 4 fixed source IPs; JSON or text body [V:S15].
- **Limits:** name 300 characters; message 4,000 (40,960 via `alert()`). Throttle is 15 triggers per 3 minutes, or 1,000 per 3 minutes for a whole watchlist alert [V:S15]. Alerts auto-deactivate after a year of inactivity [V:S15].

### 2.4 Screeners
- **Seven screeners:** Stock, ETF, Bond, Crypto coins, CEX pairs (40+ CEXs), DEX pairs and Pine (beta) [V:S1 nav, S2].
- **Scale** (the pages disagree):
  - Pricing page: "500+ fundamental and technical fields" and "150+ exchanges from 50+ countries".
  - Features page: "400+ filter fields" and "70+ stocks and 70+ crypto exchanges".
- **Timeframes:** 1 minute to 1 month [V:S2].
- **Views:** table, chart (moving averages added Sep 11, 2026) and heatmap (Sep 9, 2026) [V:S5, S38].
- **AI Screener** (Aug 17, 2026; beta; Stock Screener only; prompts of 6 to 164 characters; Shift+A; templates don't count toward the quota) [V:S8].
- **Other features:** candlestick-pattern filters (Jul 15, 2026), shareable screens (Oct 24, 2025), autosave and undo (May 12, 2026), watchlists and flags as filters, currency conversion [V:S5, S37].

### 2.5 Market overview tools
- **Heatmaps:** stocks, ETFs and crypto, with size-by, color-by and group-by options and sharing. Forex and bond-yield heatmaps are in the Markets section [V:S1 nav].
- **Calendars:** economic, earnings, dividends and IPO (Nov 25, 2025) [V:S30].
- **News Flow:** filters by provider, sector, watchlist, country and more; 65+ news providers [V:S3, S37].
- **Other tools:** Yield Curves (May 12, 2025; 40+ economies) and Macro Maps (Sep 16, 2025; 2.0 on Mar 9, 2026) [V:S30].
- **Markets hub:** pages for countries, indices, stocks, crypto, futures, forex, government and corporate bonds, ETFs and the world economy, plus gainers/losers and pre/after-hours movers [V:S1 nav].

### 2.6 Fundamentals and research
- **Financial data:**
  - Income statement, balance sheet, cash flow and ratios; "100+ fundamental metrics" [V:S2].
  - Help Center topic counts: Statistics 124, Balance sheet 69, Income 55, Cash flow 46 [V:S37].
  - Fundamental Graphs (Aug 6, 2025): up to 9 symbols × 9 metrics [V:S30].
- **Estimates and ratings:**
  - Expanded analyst estimates, including EBITDA, EBIT, FCF, capex and debt (Jul 6, 2026). Tracking of price-target consensus changes (May 15, 2026) [V:S30, S5].
  - Fitch ratings (Mar 24, 2026) and Moody's ratings (Sep 8, 2026) [V:S5].
  - CFI codes and ISIN [V:S5, S11].
- **Documents:** transcripts, filings and presentations via Quartr (Sep 15, 2025), with AI summaries (Mar 26, 2026) [V:S30, S10].
- **Options** [V:S29]:
  - Chain with greeks and IV; strategy builder (unlimited legs, P&L and greeks profiles, what-if, broker-position import); strategy finder; volatility curves; volume heatmap; Options Volume Profile indicator (Sep 25, 2026).
  - Coverage includes OPRA, CME and Eurex options (Dec 2025), BIST and ASX (Jul 2026) and B3, Euronext, KRX and TFEX (Sep 2026) [V:S5].
- **ETFs, bonds and crypto:** ETF screener and heatmap; bond screener; global and ICE OTC government bond data; crypto fundamentals as indicators (Jan 6, 2026); derivatives metrics (Binance, Hyperliquid) [V:S5].
- **Economic data** (the sources disagree):
  - Help Center: "300 metrics … for 200 countries", with 318 indicator articles [V:S30, S37].
  - Features page: "400+ economic metrics, 80+ countries" [V:S2].

### 2.7 Trading
- **Brokers:** "100+" integrated brokers [V:S25]. A US visitor sees 33, including:
  - NinjaTrader, moomoo, OANDA, FOREX.com, OKX, Tradovate, AMP, TradeStation, Webull, Kraken, Interactive Brokers.
  - Coinbase Advanced, tastytrade, Fidelity (Sep 10, 2026), Public (Sep 22, 2026), Alpaca, TradeZero, Plus500US, Gemini, Bitstamp, Crypto.com.
  - The brokers page shows a counter of "436,496,688 trades with real money" [V:S25].
- **Order entry** [V:S25, S26]:
  - Market, limit, stop-market and stop-limit orders with TP/SL brackets.
  - On-chart order projection and drag-to-modify, with or without confirmation.
  - Size calculator (units, value, % balance, risk).
  - Hotkeys; order presets (10 per broker).
- **DOM:** needs a broker with Tier-2 data [V:S26].
- **Paper trading:** multi-asset; custom balance, commission, currency and leverage; multiple accounts [V:S26].
- **No native auto-trading:** "considering… no ETA" [V:S26].
- **Community:** broker comparison (upgraded May 19, 2026), Broker Awards, The Leap contests (for example 107,677 entrants in the Jul 2026 futures contest) [V:S5, S24].

### 2.8 Portfolios, watchlists and notes
- **Portfolios** (Jun 25, 2025) [V:S27]:
  - Import transactions, or start from a watchlist or Paper Trading.
  - Benchmark comparison, allocation, beta, Sharpe and Sortino.
  - Dividends (Sep 2025), split handling (Aug 2026), public read-only share link (Jul 1, 2026), chart sync (Apr 2026).
- **Watchlists** [V:S20]:
  - Sections, 7 flag colors, custom columns.
  - Advanced view with overview, earnings, dividends and news tabs.
  - .txt import/export; sharing; alerts on a whole list.
- **Notes:** per-symbol text notes [V:S20].

### 2.9 Social and community
- **Content:** Ideas (including video and educational ideas), Minds (per-symbol feeds), profiles, followers, boosts and comments [V:S21].
  - Comments need phone verification and can be edited for 15 minutes.
- **Moderation:** Editors' Picks, House Rules and volunteer moderators [V:S21].
- **Chats:** a new Chats experience launched in Aug 2026 with one-to-one and private group chats. **Public chats are retired Sep 30, 2026** [V:S21].
- **Contests:**
  - Community trading contests (Aug 7, 2026): run for 1 hour to 4 weeks; free to join [V:S24].
  - The Leap offers real-money prizes [V:S24].
- **Scale:** the social page shows a counter of "17,209,257" (the label is ambiguous) and "5,300 publications every day" [V:S35].
- **Streams (live video):** /streams/ returns 404, so the feature appears discontinued (around Apr 2024) [UNVERIFIED, S39].

### 2.10 Apps
- **Desktop** (Windows, macOS, Linux) [V:S31]:
  - Native multi-monitor support; synced crosshairs; tab linking by symbol, interval, time and date range.
  - Version 3.0 (Jan 20, 2026) added a customizable New Tab. Latest is 3.4.1 (Sep 8, 2026; Electron 41).
- **Mobile** [V:S32]:
  - iOS: 4.8★ from 414K ratings; version 2.141.0.
  - Android: 4.6★ from 949K reviews; 50M+ downloads; updated Sep 28, 2026.
  - 19 languages; push alerts; home-screen widgets.
  - **Parity gaps:** no AI Copilot and no AI Screener on mobile [V:S6, S8]. Market data, coupons and Paid Spaces can be bought on the web only [V:S19, S22].
- **Telegram mini app** (Apr 2, 2025) [V:S33].

### 2.11 AI features (2025 to 2026)
1. **AI Copilot add-on** (Sep 28, 2026) [V:S6]:
   - Lives in the chart side panel on web and desktop.
   - Uses TradingView quotes, indicators, financials, news, calendars and screener data.
   - Can act on the chart: change symbols and layouts, add indicators, draw levels, create alerts and watchlists and write and apply Pine.
2. **Chart Copilot browser extension** (public beta Apr 2, 2026; free; Chromium) [V:S9]. It is now being phased out. A third party reports a limit of 15 requests per day [UNVERIFIED, S39].
3. **MCP Server** (public beta Sep 16, 2026) [V:S7]:
   - Available on Essential and above; trials excluded. OAuth 2.1 sign-in.
   - 35 tools in 9 groups (watchlists 8, alerts 8, screener 5 and others).
   - About 100 requests per minute; market data is delayed.
   - Works with Claude, ChatGPT/Codex and any MCP client.
4. **AI Screener** (Aug 17, 2026) [V:S8].
5. **AI news summaries** of SEC filings such as 8-K, 10-K, 10-Q, Form 4, 13D and S-1 (Mar 27, 2026) [V:S10].
6. **AI document summaries** (Mar 26, 2026) [V:S10].

### 2.12 Market data coverage
- **Headline figures** [V:S1, S3]:
  - 3,539,722 instruments from "hundreds of data feeds".
  - 100+ stock and futures exchanges; 50+ brokerage feeds; 50+ crypto CEX/DEX venues; 65+ news providers; 187 years of gold data.
- **Market data page:** lists 428 data-source rows (my count).
- **Free defaults:**
  - Real-time is free "whenever allowed". Examples: US stocks via Cboe One, NSE India, crypto and broker FX/CFD feeds.
  - Otherwise delayed: CME 10 minutes; most stock exchanges 15 minutes; Japan 20 minutes [V:S3].
- **Reference data:** FactSet and ICE Data; filings from Quartr [V:S1 footer].

### 2.13 B2B products [V:S34 unless noted]
- **Free widgets:** 22: Advanced Chart, Symbol Overview, Mini Chart, Market Overview, Stock Market, Market Data, Ticker Tape, Ticker, Single Ticker, Stock/Crypto/ETF heatmaps, Forex Cross Rates, Forex Heatmap, Screener, Cryptocurrency Market, Symbol Info, Technical Analysis, Fundamental Data, Company Profile, Top Stories, Economic Calendar.
- **Lightweight Charts:**
  - Apache 2.0 license; 35 KB.
  - v5 (Mar 3, 2025) added multiple panes plus yield-curve and options chart types.
  - Latest npm release 5.2.1 (Aug 12, 2026); 17,384 GitHub stars.
- **Advanced Charts:**
  - Free on condition that the TradingView attribution stays visible and the deployment is public (not paywalled).
  - 670 KB; 110+ drawing tools; 100+ indicators; 13 chart types.
  - You must bring your own datafeed. Latest v32.2.0 (Sep 11, 2026).
- **Trading Platform:**
  - Proprietary and paid; 900 KB; 17 chart types; up to 8 charts.
  - Adds DOM, order ticket, watchlists, news and account manager.
- **Adoption:** libraries are "trusted by 40,000+ companies" and available in 30+ languages.
- **Broker integration program:** REST API spec shared after signing an agreement; 20K+ leads per month; 100+ integrated brokers [V:S25].

### 2.14 Other 2025 to 2026 launches (condensed) [V:S5, S11, S31]
- **2025 H1:**
  - Watchlist alerts (Jan 23); CEX Screener (Feb 20); Lightweight Charts v5 (Mar 3).
  - Telegram app (Apr 2); Yield Curves (May 12); tick charts expanded (May 26).
  - Portfolios (Jun 25); floating data window (Jun 30).
- **2025 H2:**
  - Fundamental Graphs (Aug 6); Quartr documents (Sep 15); Macro Maps (Sep 16); chart table view (Sep 30).
  - News alerts (Oct 20); multi-condition alerts (Oct 23); shareable screens (Oct 24).
  - Paid Spaces (Nov 13); footprint alerts (Nov 20); IPO calendar (Nov 25).
  - CME and Eurex options (Dec 24 to 25).
- **2026 H1:**
  - Crypto fundamentals as indicators (Jan 6); Desktop 3.0 (Jan 20); alert presets (Jan 29); TPO alerts (Feb 2).
  - Footprints in Pine (Mar 2); AI docs and news (Mar 26 to 27); AI Chart Copilot beta (Apr 2).
  - Multiple news alerts (May 11); screener autosave (May 12); valuation-metric alerts (Jun 29).
- **2026 H2:**
  - Portfolio sharing (Jul 1); alert scheduling (Jul 7); 24h overnight session (Jul 9); candlestick screener (Jul 15); strategy-report redesign (Jul).
  - Community contests (Aug 7); Creator Program hub (Aug 12); script pre-moderation (Aug 14); AI Screener (Aug 17); position-drawing alerts (Aug 28).
  - Pine Screener indices (Sep 1); Moody's ratings (Sep 8); screener heatmap (Sep 9); MCP Server (Sep 16); Options Volume Profile (Sep 25); AI Copilot (Sep 28); public chats retired (Sep 30).

### 2.15 Scale metrics
- **TradingView's own claims:**
  - "100 million traders" [V:S1, S2].
  - "200M+ monthly visits, 100M+ users, 190+ countries" [V:S35].
  - "16M+ traders use Supercharts every month" [V:S22].
  - 100K+ community scripts [V:S2].
  - Partner payouts of $15M+ [V:S35].
- **Third-party estimates:** 15M monthly active users, a $3B valuation (2021) and 2023 revenue of about $172.9M [UNVERIFIED, S39].

### 2.16 NOT FOUND
- Price of the Lite plan.
- Displayed price of AI Copilot and its usage cap.
- What TradingView coins are used for.
- Exact number of drawing tools (only "110+" is stated).
- Exact number of built-in indicators (only "400+" is stated).
- The date Streams ended.
- The date the Expert plan was withdrawn.
- Concurrent-device limits by plan (the pricing page shows only connection counts).

---

## Sources (all accessed 2026-09-29)
- S1 https://www.tradingview.com/pricing/ (visible matrix and page-source shop config)
- S2 https://www.tradingview.com/features/
- S3 https://www.tradingview.com/data-coverage/
- S4 https://www.tradingview.com/us-markets-bundle/ ; https://www.tradingview.com/cme/ ; https://www.tradingview.com/eurex/
- S5 https://www.tradingview.com/blog/en/ (index pages 1 to 30; dates per post)
- S6 https://www.tradingview.com/blog/en/ai-copilot-now-on-tradingview-61231/ (Sep 28, 2026)
- S7 https://www.tradingview.com/blog/en/tradingview-mcp-server-public-beta-60864/ (Sep 16, 2026) ; https://www.tradingview.com/mcp/docs
- S8 https://www.tradingview.com/blog/en/ai-screener-60101/ (Aug 17, 2026) ; https://www.tradingview.com/support/solutions/43000785770/
- S9 https://www.tradingview.com/blog/en/tradingview-ai-chart-copilot-beta-57730/ (Apr 2, 2026)
- S10 https://www.tradingview.com/blog/en/ai-powered-news-57454/ (Mar 27, 2026) ; https://www.tradingview.com/blog/en/ai-powered-documents-57510/ (Mar 26, 2026)
- S11 https://www.tradingview.com/pine-script-docs/release-notes/
- S12 https://www.tradingview.com/pine-script-docs/writing/limitations/
- S13 https://www.tradingview.com/pine-script-docs/writing/publishing/ ; https://www.tradingview.com/pine-script-docs/concepts/strategies/
- S14 https://www.tradingview.com/support/solutions/43000703396/ ; https://www.tradingview.com/support/solutions/43000746464/
- S15 https://www.tradingview.com/support/solutions/43000520149/ ; /43000529348/ ; /43000773947/ ; /43000690939/ ; /43000739708/
- S16 https://www.tradingview.com/support/solutions/43000742436/ ; https://www.tradingview.com/blog/en/pine-screener-update-60542/ (Sep 1, 2026)
- S17 https://www.tradingview.com/support/solutions/43000692816/ ; /43000480679/ ; /43000709225/ ; /43000762068/ ; /43000758617/ ; /43000703407/
- S18 https://www.tradingview.com/support/solutions/43000666199/ ; /43000668210/ ; /43000669285/ ; /43000764138/
- S19 https://www.tradingview.com/support/solutions/43000629992/ ; /43000746975/ ; /43000694474/ ; /43000537255/ ; /43000502298/ ; /43000543048/ ; /43000777718/
- S20 https://www.tradingview.com/support/solutions/43000611193/ ; /43000487233/ ; /43000771546/ ; /43000667897/
- S21 https://www.tradingview.com/support/solutions/43000591339/ ; /43000604448/ ; /43000690226/ ; /43000591638/ ; /43000591345/
- S22 https://www.tradingview.com/support/solutions/43000765877/ ; /43000772177/ ; https://www.tradingview.com/creator-program/ ; https://www.tradingview.com/scripts/marketplace/
- S23 https://www.tradingview.com/blog/en/updated-script-publishing-60116/ (Aug 14, 2026) ; https://www.tradingview.com/blog/en/tradingview-creator-program-60011/ (Aug 12, 2026) ; https://www.tradingview.com/blog/en/paid-indicators-strategies-on-tradingview-54934/ (Nov 13, 2025)
- S24 https://www.tradingview.com/blog/en/community-trading-contests-59895/ (Aug 7, 2026) ; https://www.tradingview.com/the-leap/
- S25 https://www.tradingview.com/brokers/ ; https://www.tradingview.com/trading/ ; https://www.tradingview.com/brokerage-integration/
- S26 https://www.tradingview.com/support/solutions/43000516459/ ; /43000516466/ ; /43000742711/ ; /43000785102/ ; /43000766334/ ; /43000690950/
- S27 https://www.tradingview.com/blog/en/introducing-portfolios-on-tradingview-52661/ (Jun 25, 2025) ; https://www.tradingview.com/blog/en/increased-limits-for-portfolios-54919/ (Nov 11, 2025) ; https://www.tradingview.com/blog/en/show-your-portfolio-59176/ (Jul 1, 2026)
- S28 https://www.tradingview.com/blog/en/multi-condition-alerts-54525/ (Oct 23, 2025) ; https://www.tradingview.com/blog/en/watchlist-alerts-on-tradingview-49839/ (Jan 23, 2025) ; https://www.tradingview.com/blog/en/notification-schedule-for-alerts-59369/ (Jul 7, 2026) ; https://www.tradingview.com/blog/en/alert-presets-56465/ (Jan 29, 2026) ; https://www.tradingview.com/blog/en/multiple-news-alerts-58198/ (May 11, 2026) ; https://www.tradingview.com/blog/en/new-alert-sounds-46455/ (Sep 23, 2024)
- S29 https://www.tradingview.com/support/solutions/43000707214/ ; /43000760837/ ; /43000774565/ ; /43000789608/ ; /43000790767/ ; https://www.tradingview.com/blog/en/options-volume-profile-indicator-61185/ (Sep 25, 2026)
- S30 https://www.tradingview.com/blog/en/macro-maps-on-tradingview-53883/ (Sep 16, 2025) ; https://www.tradingview.com/blog/en/updated-macro-maps-56960/ (Mar 9, 2026) ; https://www.tradingview.com/blog/en/tradingview-bond-yield-curves-52199/ (May 12, 2025) ; https://www.tradingview.com/blog/en/smarter-insights-with-fundamental-graphs-53091/ (Aug 6, 2025) ; https://www.tradingview.com/blog/en/tradingview-seasonality-charts-49444/ (Jan 8, 2025) ; https://www.tradingview.com/blog/en/ipo-data-and-calendar-on-tradingview-55228/ (Nov 25, 2025) ; https://www.tradingview.com/blog/en/tradingview-integrates-quartr-api-53775/ (Sep 15, 2025) ; https://www.tradingview.com/blog/en/more-analyst-estimates-59323/ (Jul 6, 2026) ; https://www.tradingview.com/support/solutions/43000643547/
- S31 https://www.tradingview.com/desktop/ ; https://www.tradingview.com/support/solutions/43000673888/ ; https://www.tradingview.com/blog/en/tradingview-desktop-updated-new-tab-and-sync-58473/ (May 18, 2026)
- S32 https://www.tradingview.com/mobile/ ; https://apps.apple.com/us/app/tradingview-track-all-markets/id1205990992 ; https://play.google.com/store/apps/details?id=com.tradingview.tradingviewapp ; https://www.tradingview.com/support/solutions/43000733673/
- S33 https://www.tradingview.com/blog/en/tradingview-mini-app-on-telegram-51366/ (Apr 2, 2025)
- S34 https://www.tradingview.com/widget/ ; https://www.tradingview.com/free-charting-libraries/ ; https://www.tradingview.com/lightweight-charts/ ; https://www.tradingview.com/advanced-charts/ ; https://www.tradingview.com/trading-platform/ ; https://www.tradingview.com/charting-library-docs/latest/introduction ; https://www.tradingview.com/charting-library-docs/latest/releases/release-notes/ ; https://www.tradingview.com/blog/en/tradingview-lightweight-charts-version-5-50837/ (Mar 3, 2025) ; https://registry.npmjs.org/lightweight-charts ; https://github.com/tradingview/lightweight-charts
- S35 https://www.tradingview.com/social-network/ ; https://www.tradingview.com/advertising-info/ ; https://www.tradingview.com/partner-program/ ; https://www.tradingview.com/students/
- S36 https://www.tradingview.com/support/solutions/43000677382/ ; /43000538302/ ; /43000739401/
- S37 Help Center article tree embedded in https://www.tradingview.com/support/whats-new/ (used for pattern and indicator counts)
- S38 https://www.tradingview.com/blog/en/heatmap-view-in-screener-60678/ (Sep 9, 2026) ; https://www.tradingview.com/blog/en/table-view-on-charts-54086/ (Sep 30, 2025) ; https://www.tradingview.com/blog/en/indicator-tables-below-the-chart-60840/ (Sep 15, 2026) ; https://www.tradingview.com/blog/en/overnight-session-59441/ (Jul 9, 2026) ; https://www.tradingview.com/blog/en/more-chart-layout-options-52228/ (May 14, 2025) ; https://www.tradingview.com/blog/en/expanded-tick-chart-support-52342/ (May 26, 2025) ; https://www.tradingview.com/blog/en/pine-script-v6-has-landed-48830/ (Dec 10, 2024) ; https://www.tradingview.com/blog/en/earn-rewards-for-ideas-and-scripts-program-38366/ (May 23, 2023) ; https://www.tradingview.com/blog/en/tickmill-free-tradingview-plans-60989/ (Sep 17, 2026)
- S39 (third party, UNVERIFIED) https://blog.traderspost.io/article/tradingview-ai-features-chart-copilot-documents-news (Apr 10, 2026) ; https://tw.tradingview.com/chart/SPX/zwZyljyY-Live-stream-Streams-are-Ending-tradingview-is-cancelling-all ; https://getlatka.com/companies/tradingview.com ; https://www.wowls.com/wiki/unicorns/tradingview
