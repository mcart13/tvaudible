# Running Pine Script outside TradingView: what exists, what's missing and the legal limits (as of 2026-09-29)

> Research notes compiled on 29 September 2026. They are the evidence behind [the teardown](../tradingview-teardown.md). Claims keep the labels used during research (VERIFIED, UNVERIFIED, NOT FOUND and similar). Punctuation was normalized afterwards; the wording is otherwise as researched.

VERIFIED means I read the source on 2026-09-29; source IDs [S#] map to URLs at the end, with document dates where the source shows one. "Self-reported" means the project makes the claim and I did not reproduce it. ESTIMATE means my own judgement, with the basis stated. This is not legal advice.

## Bottom line
- **Feasible, but a large build.** Pine v6 changes almost every month and has unusual semantics: every function call keeps its own state, the live bar is rolled back and re-run on each tick, `varip` survives that rollback, requests can see future data ("lookahead") and the strategy engine simulates fills in detail.
- **Best evidence of matching TradingView's (TV's) output:**
  - PyneCore plus its PyneComp compiler. The runtime is Python; the Pine-to-Python compiler is a closed paid service.
  - PineForge. C++, strategies only; its transpiler's licence bars commercial use without a separate deal.
  - PineTS, the most-starred JavaScript engine, is AGPL-3.0 or a paid licence from LuxAlgo and its published evidence of matching TV is weaker.
- **What nobody supplies.** None of these projects gives you the platform around the engine: TV-grade chart rendering, the inputs UI, a 24/7 alert service, the strategy report, market data feeds or vendor access control. You build those whichever engine you pick.
- **Legal.** Re-implementing a language and its built-in functions is defensible (SAS v World Programming; Google v Oracle). The risks are the registered "PINE SCRIPT" mark and TV's Terms, which bar copying TV's software and docs and bar commercial or automated use of its services. The biggest exposure is using TV accounts to generate reference output for parity testing. In the closest precedent, SAS won a US$79.1M contract and fraud verdict against a competitor that did something similar.
- **Why vendors might move.** TV's Terms §22A now charge invite-only vendors US$29.95 per active user per month once they exceed 100 users [S11] VERIFIED; the effective date is UNVERIFIED. TV's own "Paid Spaces" marketplace currently takes a 0% platform fee [S14] VERIFIED.

## 1. Pine Script in 2026: language and platform scope
**Version.** v6 is current.
- It launched in November 2024, and every 2025 to 2026 feature is v6-only; the manual still covers v5, v4 and v3 [S1] VERIFIED.
- Code in the wild is mixed. Of the 819 popular open-source scripts PyneSys tested, 298 are v4, 319 v5 and 202 v6 [S27].
- v6 changed behaviour, not just syntax: dynamic requests by default, `bool` can never be `na`, `and`/`or` short-circuit, `when` was removed and `for` bounds are re-evaluated [S9] VERIFIED.
- An engine therefore needs per-version rules or an up-converter.

**Execution model** [S2] VERIFIED.
- **Historical bars.** The script runs once per bar and commits its state after each one; `[]` reads that committed history.
- **Per-call state.** Each function call site keeps its own state. Variables inside skipped branches get an "inconsistent history".
- **Live bar.** Indicators re-run on every tick after rolling back to the last committed state; `varip` variables escape the rollback.
- **Strategies.** They run only at bar close unless `calc_on_every_tick`, `calc_on_order_fills` or `calc_on_every_history_tick` (new July 2026) is set.
- **Reloads.** On reload, bars that were live become historical, so results can "repaint".
- **History buffers.** Up to 5,000 bars (10,000 for OHLC and time). TV sizes them automatically from the first 244 bars and restarts the load on overflow; `max_bars_back()` overrides. Overflowing on a live bar is a runtime error.
- **Caching.** Results are cached per combination of inputs, properties and chart settings.

**Type system** [S2, S1].
- Base types are int, float, bool, color and string, with const/input/simple/series qualifiers.
- On top of those: user-defined types, methods, enums, arrays, matrices, maps, `chart.point`, drawing IDs and `footprint`/`volume_row` (January 2026).
- `int` is really a 64-bit floating-point double at runtime [S29] (PyneSys measurement, 2026-08-30).

**How many built-ins (approximate).** A January 2026 third-party copy of the v6 reference manual has about 940 entries: 475 functions, 161 variables, 239 constants, 20 types, 15 keywords, 21 operators and 10 annotations [S10] (VERIFIED as counts of that copy; other projects count 884 [S32] and 878 [S22]). Functions per namespace:

| Namespace | Functions | Also |
|---|---|---|
| ta | 59 | 10 variables |
| array | 55 | |
| matrix | 49 | |
| strategy | 47 | 35 variables, 14 constants |
| global (plot*, fill, hline, bgcolor, barcolor, alert, alertcondition, time…) | 41 | |
| box | 29 | |
| math | 24 | |
| table | 22 | |
| label, line | 21 each | |
| str | 18 | |
| input | 13 | |
| map, request | 11 each | |
| ticker, footprint | 9 each | |
| volume_row | 8 | |
| color | 7 | |
| chart | 5 | 11 variables |
| linefill | 5 | |
| log | 3 | |
| timeframe | 3 | 11 variables |
| polyline | 2 | |
| syminfo | 2 | 40 variables |
| runtime | 1 | |
| barstate | n/a | 7 variables |
| session | n/a | 7 variables |

**request.\* functions** [S5, S3] VERIFIED.
- **The functions:** security, security_lower_tf, currency_rate, dividends, splits, earnings, financial (FactSet data), economic, seed (Pine Seeds; no new repos accepted) and footprint (January 2026; Premium/Ultimate plans; one call per script). `quandl` still appears in the limits list.
- **Lookahead.** With `lookahead_on`, a higher-timeframe request returns future values unless the expression is offset with `[1]`.
- **Gaps and confirmation.** `gaps` controls whether values are filled between updates. Higher-timeframe values confirm only when that bar closes, so live values repaint.
- **Dynamic requests (v6).** Symbol and timeframe can change bar to bar. Requests can sit inside loops, conditionals and library exports and nested requests inherit their context.
- **Limits.** 40 unique calls (64 on the Ultimate plan), 127 tuple elements and 100k to 200k lower-timeframe bars depending on plan.

**Strategy engine** [S4, S1] VERIFIED.
- **Fill model.** On historical bars the simulator assumes the price went open→high→low→close if the open was nearer the high, otherwise open→low→high→close. There are no gaps inside a bar, and an order crossed in a gap between bars fills at the next open.
- **Orders and costs.** Market, limit, stop and stop-limit orders; pyramiding; one-cancels-all (OCA) groups; commission; slippage. Margin calls liquidate 4× the shortfall.
- **July 2026 overhaul.** "Bar detalization" replaced the bar magnifier; `calc_on_every_history_tick` follows documented four-tick price paths; leverage inputs and limit-fill and order-delay settings were added.
- **Trade limits.** The oldest trades are trimmed after 9,000; Deep Backtesting keeps up to 1,000,000 orders.

**Plots, drawings, inputs, alerts and libraries** [S3, S6 to S8] VERIFIED.
- **Plots.** 64 plot counts per script; one call can use up to 7, and `hline` and drawings don't count.
- **Drawings.** Up to 500 lines, boxes or labels and 100 polylines, placed from 10,000 bars back to 500 bars forward. One table per screen position (9 positions).
- **Inputs.** 13 `input.*` types, with `group`, `inline`, `confirm` (the user clicks on the chart to pick a value) and `active` (July 2025).
- **Alerts.** `alert()` fires once per bar, once at bar close or on every call. `alertcondition()` works in indicators only. TV alerts "run 24x7 on our servers".
- **Libraries.** Libraries are always published open-source, and public scripts can import only public libraries.

**Execution limits** [S3] VERIFIED.
- **Time.** 2-minute compile; 20 s (basic plan) or 40 s total run time; 500 ms per loop per bar.
- **Size.** 100,256 compiled tokens per script and 1M across imported libraries; 1,000 variables per scope.
- **Data.** Collections up to 100,000 elements; strings up to 40,960 characters (since August 2025); 5k to 40k chart bars depending on plan.

**What was added in 2025 to 26** [S1] VERIFIED.

| Month | Additions |
|---|---|
| Feb 2025 | `bid`/`ask`; no limit on the number of scopes |
| Mar 2025 | `box.set_xloc`; dynamic `for` bounds |
| Jun 2025 | libraries can export `const` values |
| Jul 2025 | `active` on inputs; `syminfo.current_contract` |
| Sep 2025 | `linestyle` on `plot` |
| Oct 2025 | `timeframe_bars_back` |
| Nov 2025 | `syminfo.isin` |
| Jan 2026 | `request.footprint` |
| Apr 2026 | multiline strings; sorting arrays of user-defined types |
| Jul 2026 | strategy overhaul |
| Aug 2026 | `once` keyword; binary search on user-defined types; invite-only scripts in the Pine Screener |

## 2. Independent implementations
Stars, commit counts and last-commit dates come from the GitHub API and my own clones on 2026-09-29. Licences come from each repo's LICENSE file and package manifest (VERIFIED). Parity and performance figures are self-reported unless marked otherwise.

| Project (language; maintainer) | Licence (SPDX) | Stars; activity | Accepts | Coverage, evidence of matching TV, gaps |
|---|---|---|---|---|
| **PineTS** + pinets-cli (TS; Alaa-eddine K.; copyright moved to LuxAlgo in a 2026-08-14 commit) [S22 to S24] | AGPL-3.0-only (CLI: AGPL-3.0-or-later). Commercial: US$1,199 per developer per year or US$20k/year "Business" | 706★; 733 commits; last 2026-09-25 (v0.10.0) | Pine v5/v6 source ("experimental") or its own JavaScript syntax | Claims 98% coverage of 878 API names, but only 3 of 11 `request.*` functions. Its parser has no `import` statement, so it can't use Pine libraries (I read the code). `varip` behaves like `var`. Its docs say 12 of 31 reference strategies match TV to tolerance. Regression tests compare against its own earlier output, not TV's. Transpiled code runs through `new Function`, with no sandbox. A third party measured 486 ms for a 10-indicator script [S30]. |
| **PyneCore** + **PyneComp** (Python; Adam Wallner / PyneSys) [S26 to S29] | Runtime Apache-2.0. PyneComp is a closed paid service: US$8 to 45/month for 5 to 300 conversions/day | 194★; 988 commits; last 2026-09-28 | Runs a Python dialect ("Pyne"). Real Pine v4 to v6 must first go through PyneComp, which PyneSys says is a deterministic compiler, "not an LLM" | Tested on 819 published scripts, all compiled and ran. 770 match TV; 22 were set aside because TV's output depends on lookahead, 1 lacks data, 26 have no TV reference. 99.717% of 99.9M plotted values are bit-identical, and 296,924 strategy trades match (2026-09-28). Every `ta.*` function (67) is implemented. My check: 795 of the 819 ran only on BINANCE:BTCUSDT 30-minute bars. It computes drawings but doesn't render them. No data for the financial, economic, earnings, dividends, splits, seed or footprint requests. Median 0.089 ms per bar (my calculation from its results). |
| **PineForge** engine + code generator (C++17 / Python; "PineForge", 4pass.com.tw) [S30, S31] | Engine Apache-2.0. Code generator PolyForm-Noncommercial-1.0.0 plus a personal-trading permission; commercial use needs a licence | 188★; 1,517 commits since May 2026; last 2026-09-29 | Pine v6 strategies, transpiled to C++ | Compared trade lists with TV on 4,190 tests: 4,182 "excellent", 8 "strong". The tests cover 312 public strategies and 413 community scripts across 15 markets and timeframes. No support for plots, drawings or alerts. Median 603k bars/s per strategy. |
| **piner** (TS; Phat Huynh; runs fractalchart.com) [S32] | AGPL-3.0-only | 22★; last 2026-08-22 | Pine v6, including library imports | Implements 852 of 884 manual entries; 399 of 408 manual examples run. 509 tests. Checked only against the manual and against PineTS (about 120 cases), never against TV. Missing: live and cross-symbol `request.security`, OCA groups. |
| **resin** (TS; nullarch; runs wavealgo.com) [S33] | Apache-2.0 | 4★; 145 commits since 2026-08-09; last 2026-09-28 | Pine v5/v6 | 99.5% of 2,979 GitHub scripts run, but their output values weren't checked. Reproduces all 19 strategy and 72 indicator TV exports that PyneCore published. 10,311 tests. Built by an autonomous AI agent loop; about a quarter of its source lines were Korean comments. It was first built against an unnamed "sibling implementation" whose origin I couldn't verify. |
| **pinecone** (Rust; Ferran Borreguero) [S34] | MPL-2.0 | 18★; last 2026-09-08 | Pine v4/v5 | Interpreter, language server and linter. No evidence of matching TV. Includes a verbatim copy of TV's reference manual. |
| **pinescription** (Go; Woodstock K.K.) [S35] | AGPL-3.0-only, plus a commercial licence | 19★; last 2026-07-06 | A Pine-like dialect | `strategy.*` and `request.security` don't work unless the host application supplies them. |
| **OpenPineScript** (TS) [S36] | GPL-3.0 | 56★; last 2026-08-17 | Pine v1/v2 only | 393 tests. |
| **pine-transpiler** (TS; Opus Aether AI) [S37] | MIT | 36★; last 2026-07-15 | Part of v5/v6, converted to indicators for TV's commercial Charting Library | 1,400+ unit tests. Using the output requires a TV Charting Library licence. |
| **Pine-A-Script** (JS; MeridianAlgo) [S38] | MIT | 8★; last 2026-06-29 | v5 and "early v6" | Claims 240+ function mappings. No evidence of matching TV. |
| **PYNE** (Python; HOOX) [S39] | AGPL-3.0-or-later | 2★; last 2026-09-29 | Pine | 2,466 scripts pass a 50-bar test run. |
| **pynescript** (Python; Yunseong Hwang) [S40] | LGPL-3.0-or-later | 92★; last 2025-12-18 | Pine v5 | Parser only; it doesn't run scripts. |

I left out toy prototypes such as tradesdontlie/pinescript-compiler (no licence file, 4 commits) [S52].

**Conflicting claims.**
- PineForge benchmarked 200 strategies and reports PyneCore "excellent" on 84 of 100 public ones and 49 of 101 closed ones. It blames most misses on its test window and on `request.security` [S30].
- The same benchmark says PineTS "runs indicators only". PineTS's changelog shows a strategy engine since v0.9.17 (2026-06-02) [S22].
- Treat both as a competitor's claims.

## 3. Commercial platforms and converters
**Platforms that run Pine through one of these engines.**
- **LuxAlgo** [S24, S25] VERIFIED.
  - Its Vela Pro charting product "ships the PineTS runtime built in and commercially licensed" with a Pine v6 editor.
  - LuxAlgo launched its own charting platform on 2026-08-31. Its "Quant" AI agent "auto-debugs Pine Script®".
  - UNVERIFIED: whether users can run arbitrary third-party Pine on it. LuxAlgo also publishes its own tools on TV.
- **PyneSys**: converts Pine to Python through a web app, command-line tool and Discord bot [S28].
- **PineForge**: offers a hosted backtesting service for AI agents [S30].
- **fractalchart.com** runs on piner [S32], and **wavealgo.com** runs on resin [S33]. Both come from the repos; I didn't inspect either site.

**Converters.** VERIFIED unless marked:
- **Pine2Expert**: a deterministic Pine v6 → MetaTrader 5 (MQL5) transpiler; €25 to 199 one-time [S44].
- **ChartingLens**: AI converts pasted Pine into native indicators and test-runs the result ("self-validating"); US$14.99 or US$29.99 per month [S41].
- **TrendSpider**: the editor's AI translates pasted code and "works well in the majority of cases" [S42]. A paid human conversion service is UNVERIFIED [S50].
- **TakeProfit**: AI converts Pine to its own "Indie" language [S43].
- **HorizonAI**: AI converts between Pine, MQL5 and NinjaScript [S45].
- **Strategy Converter**: AI converts between Pine and MQL. UNVERIFIED [S51].

**Ruled out.** GoCharting's own LipiScript page makes no claim of Pine compatibility [S46] VERIFIED. I found no other platform running third-party Pine natively; UNVERIFIED, because my web-search budget ran out.

## 4. Legal constraints (not legal advice)
**(a) Trademark.**
- **US registration** [S15] VERIFIED: "PINE SCRIPT" is US Reg. No. 7,559,746, filed 2022-03-07, registered 2024-11-05 in Class 42, owned by TradingView, Inc. "SCRIPT" is disclaimed, so "PINE" is the protected element.
- **EU**: status UNVERIFIED; the EUIPO registry was unreachable from here.
- **How others describe compatibility.** Third parties write "Pine Script®/™ is a trademark of TradingView… not affiliated". PineTS, PyneCore, PYNE and pine-transpiler all do this [S22, S26, S37, S39] VERIFIED.
- **Legal basis for naming the language.**
  - US nominative fair use: the three-part *New Kids on the Block* test (9th Cir. 1992) [S17].
  - UK Trade Marks Act 1994 s.11(2)(c): allows use "necessary to indicate the intended purpose… in accordance with honest practices" [S16] VERIFIED.
  - EU: Art. 14(1)(c) of the EU Trade Mark Regulation is the equivalent; UNVERIFIED here.
- **Analysis.** Say "compatible with Pine Script®" with a non-affiliation disclaimer, and don't build the product name on "Pine". Several open projects do (PineTS, PineForge, Pinecone, piner), with no enforcement I could find (UNVERIFIED).

**(b) Copyright: can you re-implement a language and its function library?**
- **EU court, CJEU C-406/10 (2 May 2012).** A program's functionality, its programming language and its data formats are not protected expression. A licensee may observe, study and test the program. Copying elements of a manual can infringe [S18] VERIFIED (secondary source).
- **UK courts.**
  - SAS lost its software-copyright and licence claims: licence terms that stop a licensee working out a program's "ideas and principles" are void.
  - Upheld on appeal; final July 2014.
  - WPL's user manual was found to infringe SAS's manuals [S19, S18] VERIFIED.
- **US contract case** [S19] VERIFIED.
  - This is the part relevant to parity testing. WPL developers "ran SAS programs through both [SAS software] and WPS, and then modified WPS's code to make the two achieve more similar outputs". They did this under a click-through "Learning Edition" licence that banned "reverse engineering" and allowed only "non-production" use.
  - The federal court in North Carolina found breach of contract. A jury added fraudulent inducement and unfair-trade-practices liability, and US$26.4M in damages was trebled to US$79.1M.
  - The 4th Circuit upheld the judgment in 2017. Its 2020 opinion says WPL, "in violation of a license agreement… reverse engineered a SAS product to speed development of its own product".
- **US copyright case, Federal Circuit (6 April 2023).** SAS's claim that WPL copied its software's structure and behaviour failed. SAS couldn't show protectable expression once "mathematical and statistical elements" and "process, system and method elements" were filtered out [S20] VERIFIED.
- ***Google v. Oracle*, US Supreme Court (5 April 2021).** Copying about 11,500 lines of Java's API declarations to re-implement the API was fair use as a matter of law. The Court assumed the code was copyrightable without deciding it [S21] VERIFIED.
- **Analysis.**
  - An engine written from scratch that implements Pine's syntax, behaviour and built-in names is defensible.
  - Copying TV's text or code is the risk: manual prose, the reference implementations shown in the docs or built-in indicator source. pinecone and fractal-chart both include copies of TV's manual [S34, S32].
  - The second risk is contract: how TV accounts get used during development and testing.
  - UNVERIFIED: whether the EU/UK right to "observe, study and test" a program even applies to a hosted service like TV.

**(c) TradingView's Terms of Use** [S11]. The page shows no "last updated" date. VERIFIED text:
- **§3, scope of use.** Content is licensed for "display-only use", limited to "personal or internal business purposes". It bans non-display use, including "any machine-driven processes" and "creating products or services based on TradingView content, any processing of TradingView's content".
- **§3, copying.** You may not make "copies of any of the software or documentation… including… translating, decompiling, disassembling or creating derivative works" without written consent.
- **§3, commercial use.** "We do not permit commercial usage of any of our services or APIs" without a separate agreement. TV reserves the right to audit and sue.
- **What's absent.** I found no explicit non-compete clause and no explicit anti-scraping clause (I searched the full text). §20 makes the House Rules part of the Terms.
- **§22, scripts.**
  - Authors grant TV a "world-wide, irrevocable, perpetual, royalty-free, sub-licensable" licence. It isn't described as exclusive, so vendors can publish their own code elsewhere, though TV may keep hosting it.
  - A published script with no stated licence is licensed under MPL-2.0.
- **§27.** Disputes go to binding arbitration.
- **Analysis.** Automated comparison runs, bulk downloads of scripts or systematic data exports from TV accounts all carry SAS-style contract risk. Two existing projects show the exposure:
  - PineForge describes its test set as "TradingView-scraped" and keeps it "private under TradingView's Terms of Service" [S30].
  - resin says it submitted 1,085 scripts to "TradingView's own compiler" [S33].

**(d) TV's built-in indicators and community scripts.**
- **Built-in code.** TV's publishing rules call "All code from TradingView's built-in scripts and documentation", published library code and ports of classic indicators "public domain" for reuse on TV [S12] VERIFIED. That is a house rule, not a licence and it sits uneasily with the §3 copying ban. Re-implement standard indicators from their formulas rather than shipping TV's source.
- **Community scripts.** Licences in PyneSys's 819-script corpus [S27] VERIFIED:

  | Licence | Scripts |
  |---|---|
  | MPL-2.0 | 388 |
  | None stated (so MPL-2.0 under §22) | 294 |
  | Creative Commons | 129 (includes all 65 LuxAlgo scripts) |
  | GPL | 4 |
  | MIT | 4 |

  - MPL-2.0 allows commercial use; you must publish the source of the licensed files you ship.
  - LuxAlgo's scripts use CC BY-NC-SA 4.0 (the header appears in a PineTS test file [S22]), which forbids commercial use.
- **Vendors' own code.** Where a vendor's script reuses someone else's code, TV required "explicit permission… to reuse their code in a paid script" [S13] VERIFIED. That permission may not extend to your platform, so porting could need fresh consent.
- **Libraries.** Libraries are always open-source, and public scripts can import only public ones [S6]. So a vendor's library dependencies have known licences, but get the source from the vendor or the library's author, not by scraping TV.

## 5. Architecture considerations
**Where scripts should run.**
- TV runs scripts on its own servers ("each script uses computational resources in the cloud") [S3], and its alerts run server-side 24x7 [S7] VERIFIED.
- Browser engines like PineTS and piner would send the vendor's logic to the user's machine. Transpiling to JavaScript or WebAssembly (WASM) only obscures it; it doesn't protect it (analysis).
- So run invite-only scripts on the server and stream a serializable description of the plots and drawings to the client. piner, PyneCore (`--viz`) and resin already produce such output [S32, S26, S33]. Running open-source scripts in the browser is fine.
- Sandbox the server engine. PineTS runs generated code via `new Function` [S22]. Use isolated processes or V8 isolates, plus CPU, loop and memory limits like TV's [S3].

**Getting identical numbers everywhere.**
- **JavaScript isn't deterministic across browsers.** Its `Math` precision is "implementation-dependent… different browsers can give a different result" [S47] VERIFIED.
- **WASM is.** WASM arithmetic is deterministic apart from NaN bit patterns, relaxed SIMD and shared-memory threads [S48] VERIFIED.
- **Analysis.** Build one Rust or C++ core with its own bundled math library, compiled natively for servers and to WASM for browsers. PineForge compiles with `-ffp-contract=off` and says it gets bit-identical results on Linux and macOS [S30].
- **Matching TV bit-for-bit** also requires TV's exact summation order, EMA stepping, number formatting and int-as-double behaviour. PyneSys got there by measuring "TradingView's arithmetic function by function" [S28, S29].
- **Exact comparisons.** Even last-bit differences can flip exact comparisons such as crossovers [S26].
- **Decision needed.** Decide whether to reproduce TV's lookahead leaks. PyneCore deliberately doesn't [S26].

**Semantics that drive the engine design** [S2, S5].
- Give every function call site its own state slot, allocated at compile time.
- Size history buffers the way TV does (the 244-bar rule).
- Make per-tick rollback cheap, via snapshots or undo logs, even with 100k-element collections.
- Treat each multi-timeframe request as a separate execution in the requested symbol and timeframe. It must handle alignment, lookahead, gaps, confirmation, dynamic and nested requests and exchange calendars.
- Current engines solve multi-timeframe requests differently [S26, S22, S30]:
  - PyneCore runs one process per context with shared memory.
  - PineTS "slices" out the part of the script the request needs.
  - PineForge uses a calendar-aware state machine.

**Running alerts at scale (ESTIMATE).**
- **Instances and restarts.** Share one engine instance across identical alerts (same script version, inputs, symbol and timeframe) and shard by symbol. Checkpoint engine state so a restart doesn't replay 5k to 40k bars.
- **Compute.** At PyneCore's median of 0.089 ms per bar execution [S27], one core handles about 11,000 executions per second.
  - 10,000 alerts evaluated at each 1-minute close need about 170 executions per second, which is trivial.
  - Evaluating every tick at 10 ticks per second needs about 100,000 per second. That's roughly 9 cores for a Python-speed engine, or well under one core at PineForge's self-reported 603k bars/s.
- **Implication.** An interpreted engine needs tick coalescing.

## 6. Feasibility assessment
**How often public scripts use the hard features.** Share of about 12,736 public v6 `.pine` files on GitHub (GitHub code search, 2026-09-29, approximate counts) [S49]:

| Feature | Share of files |
|---|---|
| `strategy.entry` | 27% |
| `request.security` | 25% |
| `table.new` | 24% |
| `label.new` | 22% |
| `line.new` | 17% |
| `box.new` | 11% |
| library `import` | ≤5.6% |
| `request.security_lower_tf` | 1.6% |
| `varip` | 1.2% |
| `request.financial` | 0.3% |

resin found 5.1 to 5.8% of GitHub scripts import libraries it didn't have [S33]. Closed vendor scripts probably use drawings and multi-timeframe requests more heavily (UNVERIFIED).

**ESTIMATES (low to moderate confidence).** Share of real vendor scripts that would run with no source changes and produce values or trades matching TV on the same data. Chart rendering is excluded, since you build it regardless.

| Engine | Estimate | Basis |
|---|---|---|
| PyneCore + PyneComp | 75 to 90% | 94% (770 of 819) verified against TV. Discounted because almost all tests ran on one crypto market, because it refuses to reproduce lookahead, because it has no fundamentals data and because of PineForge's 49-of-101 result. Vendor code would go to PyneSys's hosted compiler unless an on-premises deal exists (UNVERIFIED). |
| PineForge | Strategies 85 to 95%; indicators about 0% | All 3,881 closed-set tests rated excellent or strong (self-reported). Produces no visual output. |
| PineTS | 50 to 75% | No library imports, so about 5% fail outright. `varip` is treated as `var`. 8 of 11 `request.*` functions are missing, and only 12 of 31 reference strategies match. No published pass rate on real scripts, and core-behaviour fixes were still landing in September 2026. |
| resin | 55 to 80% | 99.5% of scripts run, but values were checked against TV on only 91 cases; the project is about 7 weeks old. |
| piner | 40 to 70% | Follows the manual closely but has never been checked against TV output. |
| pinecone, Pine-A-Script, pine-transpiler, PYNE | under 40% | Little or no evidence of matching TV; limited versions or targets. |
| pinescription, OpenPineScript, pynescript | about 0 to 10% | A dialect, v1 to v2 only and parser only, respectively. |

**Ceiling for every engine: data.** Output can match TV only where your market data matches TV's: the same bars, sessions, price adjustments and futures rolls and none of TV's own "derived data" [S11 §11]. Data only TV has (FactSet financials, economic data, footprint, Pine Seeds) can't be matched at all.

**What you must build whichever engine you choose:**
- A chart renderer covering every plot, fill, shape and drawing type and its limits.
- The inputs UI, including `confirm` (click on the chart to pick a value).
- The data layer: sessions and calendars, adjustments, non-standard chart types, currencies, `syminfo`, fundamentals, tick data.
- A live-bar engine with rollback and `varip`.
- The strategy report and deep backtesting.
- A 24/7 alert service with message placeholders and webhooks.
- Invite-only access control, billing, library hosting and editor error messages.
- A way to handle v4/v5 scripts.
- Sandboxing.
- A way to check parity against TV that is legally clean.

**Suggested path (analysis).**
1. Collect 50 to 100 real vendor scripts, with the vendors' consent, plus each vendor's own TV exports of its own scripts. Have counsel review this against §3 of TV's Terms first.
2. Benchmark PyneCore/PyneComp, PineTS (under the commercial licence) and resin on that set.
3. Then decide between licensing an engine and building your own permissively licensed Rust or C++ core (native plus WASM). Either way, budget for keeping up with TV's monthly changes.

## Sources (all accessed 2026-09-29)
- S1 Release notes: https://www.tradingview.com/pine-script-docs/release-notes/
- S2 Execution model: https://www.tradingview.com/pine-script-docs/language/execution-model/
- S3 Limitations: https://www.tradingview.com/pine-script-docs/writing/limitations/
- S4 Strategies: https://www.tradingview.com/pine-script-docs/concepts/strategies/
- S5 Other timeframes and data: https://www.tradingview.com/pine-script-docs/concepts/other-timeframes-and-data/
- S6 Libraries: https://www.tradingview.com/pine-script-docs/concepts/libraries/
- S7 Alerts: https://www.tradingview.com/pine-script-docs/concepts/alerts/
- S8 Inputs: https://www.tradingview.com/pine-script-docs/concepts/inputs/
- S9 v6 migration guide: https://www.tradingview.com/pine-script-docs/migration-guides/to-pine-version-6/
- S10 Third-party copy of the v6 reference manual (committed 2026-01-29): https://github.com/ferranbt/pinecone/tree/main/crates/pine-reference/spec
- S11 TradingView Terms of Use: https://www.tradingview.com/policies/
- S12 Script Publishing Rules: https://www.tradingview.com/support/solutions/43000590599-script-publishing-rules/
- S13 Vendor Requirements: https://www.tradingview.com/support/solutions/43000549951-vendor-requirements/
- S14 Paid Spaces terms: https://www.tradingview.com/support/solutions/43000772177-tradingview-creator-program-paid-spaces-terms/
- S15 USPTO record, serial 97298638: https://tsdr.uspto.gov/statusview/sn97298638
- S16 UK Trade Marks Act 1994 s.11: https://www.legislation.gov.uk/ukpga/1994/26/section/11
- S17 Nominative use (Wikipedia): https://en.wikipedia.org/wiki/Nominative_use
- S18 SAS v World Programming (Wikipedia): https://en.wikipedia.org/wiki/SAS_Institute_Inc_v_World_Programming_Ltd
- S19 SAS v WPL, 4th Cir., 12 Mar 2020: https://www.ca4.uscourts.gov/Opinions/191290.P.pdf
- S20 SAS v WPL, Fed. Cir., 6 Apr 2023: https://www.cafc.uscourts.gov/opinions-orders/21-1542.OPINION.4-6-2023_2106573.pdf
- S21 Google v. Oracle (5 Apr 2021): https://www.supremecourt.gov/opinions/20pdf/18-956_d18f.pdf
- S22 PineTS (README, CHANGELOG, LICENSE-COMMERCIAL.md, docs/api-coverage/strategy.md, src/transpiler/index.ts); formerly QuantForgeOrg/PineTS: https://github.com/LuxAlgo/PineTS
- S23 pinets-cli: https://github.com/LuxAlgo/pinets-cli
- S24 LuxAlgo Vela / PineTS pricing: https://www.luxalgo.com/vela/pine-script/ and https://www.luxalgo.com/vela/pro/
- S25 LuxAlgo platform launch, 31 Aug 2026: https://www.luxalgo.com/blog/luxalgo-charting-platform/
- S26 PyneCore (README; compatibility page, last modified 2026-09-26): https://github.com/PyneSys/pynecore and https://pynecore.org/docs/overview/compatibility/
- S27 Pyne in the Wild (snapshot 2026-09-28): https://github.com/PyneSys/pyne-in-the-wild and https://wild.pynesys.io/
- S28 PyneSys plans and news: https://pynesys.io/llms.txt and https://pynesys.io/news/2026-08-04-pynecore-now-matches-tradingview-down-to-the-last-digit/
- S29 "Pine Script has no integers" (2026-08-30): https://pynesys.io/blog/pine-script-has-no-integers/
- S30 PineForge engine: https://github.com/pineforge-4pass/pineforge-engine
- S31 PineForge code generator: https://github.com/pineforge-4pass/pineforge-codegen-oss
- S32 piner: https://github.com/heyphat/piner
- S33 resin: https://github.com/nullarch/resin
- S34 pinecone: https://github.com/ferranbt/pinecone
- S35 pinescription: https://github.com/woodstock-tokyo/pinescription
- S36 OpenPineScript: https://github.com/be-thomas/OpenPineScript
- S37 pine-transpiler: https://github.com/Opus-Aether-AI/pine-transpiler
- S38 Pine-A-Script: https://github.com/MeridianAlgo/Pine-A-Script
- S39 PYNE: https://github.com/hoox-sh/pyne
- S40 pynescript: https://github.com/elbakramer/pynescript
- S41 ChartingLens: https://chartinglens.com/features/ai-assistant
- S42 TrendSpider help: https://help.trendspider.com/kb/indicators/custom-indicators-js-scripting
- S43 TakeProfit Indie: https://takeprofit.com/docs/indie/What-is-Indie
- S44 Pine2Expert: https://www.pine2expert.com/en
- S45 HorizonAI: https://www.horizontrading.ai/docs/convert-pinescript-to-mt5
- S46 GoCharting Lipi: https://gocharting.com/developers/lipi
- S47 MDN, JavaScript Math: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math
- S48 WebAssembly nondeterminism: https://github.com/WebAssembly/design/blob/main/Nondeterminism.md
- S49 GitHub code search (queries such as `"@version=6" extension:pine`, `"@version=6" "request.security" extension:pine`): https://docs.github.com/en/rest/search/search#search-code
- S50 TrendSpider code conversion (couldn't retrieve): https://trendspider.com/developers/code-conversion/
- S51 Strategy Converter (search snippet only): https://www.strategyconverter.com/
- S52 tradesdontlie/pinescript-compiler: https://github.com/tradesdontlie/pinescript-compiler
