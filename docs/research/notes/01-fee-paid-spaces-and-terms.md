# TradingView "Technology Fee" and Paid Spaces: research report (as of 2026-09-29)

> Research notes compiled on 29 September 2026. They are the evidence behind [the teardown](../tradingview-teardown.md). Claims keep the labels used during research (VERIFIED, UNVERIFIED, NOT FOUND and similar). Punctuation was normalized afterwards; the wording is otherwise as researched.

**How this was checked.** I fetched every TradingView page live on 2026-09-29. The Terms of Use and Help Center articles show no date, so they are cited as "undated, accessed 2026-09-29". Some sources were blocked from this environment: Reddit (HTTP 403, and the search tool refuses reddit.com), X (HTTP 402), the Wayback Machine, archive.today and Common Crawl. The web-search quota also ran out near the end, so social and news coverage is thinner than intended. Raw copies of the Terms and fetched pages were kept locally during research and are not retained here. Section 22A is quoted in full below, which matters because the Terms are undated and can change at any time.

## Key findings
1. The client's quote is real and word-for-word. It is paragraph 1 of **Section 22A of TradingView's Terms of Use**. I found no announcement, effective date or FAQ for it.
2. Read literally, once a vendor has more than 100 users the fee applies to **every** user, not just those above 100. Nothing in the text exempts Paid Spaces subscribers or free/trial access grants.
3. The Paid Spaces platform fee is **currently 0% for everyone**. TradingView has not published any rate for authors approved on or after April 1, 2026. 47 Paid Spaces are live.
4. I found no public reaction to the fee. The nearest competitive moves (LuxAlgo's own charting platform and open-source Pine runtime, OpenMarket's price attack) don't mention it.
5. "PINE SCRIPT" is a registered US trademark of TradingView (Reg. No. 7,559,746).

---

## 1. Primary source of the Technology Fee

**VERIFIED:** The source is the TradingView Terms of Use, **Section 22A, "Technology Fee for invite-only indicators"**, https://www.tradingview.com/policies/ (undated; accessed 2026-09-29). The rest of the section reads:

> "TradingView will determine the number of users with access to your invite-only scripts as at the last day of each calendar month, based on its own records of access grants and script usage. TradingView will issue an invoice for the preceding calendar month within 30 days of the end of that month to the email address associated with your account. Each invoice is payable within 14 days of the date of the invoice. TradingView may collect payment by issuing an invoice for direct payment or by charging any payment method held on your account. The Technology Fee is non-refundable."
>
> "If the Technology Fee is not paid when due, TradingView may, at its sole discretion, on written notice and with immediate effect: (a) block new access grants to your invite-only scripts; (b) hide, restrict or revoke access to any of your scripts, including existing access; (c) remove any script, publication or profile content; (d) withdraw your vendor privileges; (e) suspend or terminate your account under Section 18; and/or (f) recover unpaid fees together with interest and costs. This Section 22A applies to all invite-only scripts and users, including existing scripts and existing vendors."

- **VERIFIED:** Section 18 (Termination) was also changed. Its list of grounds for termination now includes "(g) any failure to pay a Technology Fee when due under Section 22A" (same URL and date).
- **VERIFIED:** Section 22A also appears in the localized Terms (de, es, fr, it, pl, br, id, jp, kr, ru and tr subdomains, `/policies/`, accessed 2026-09-29).
  - The ru version is still in English, and the tr heading is untranslated. That suggests a recent insertion, but this is my inference.
  - The German version mistranslates "may change the Technology Fee" as "kann die Technologiegebühr … einfordern" ("may demand").
- **NOT FOUND:** the announcement date and the effective date. What I tried:
  - The Terms page itself: no date or revision marker, no Last-Modified header and no lastmod in TradingView's sitemap.
  - TradingView's blog: the latest Social posts are Aug 12 and Aug 14, 2026 and neither mentions the fee.
  - Help Center pages on vendors and Paid Spaces: no mention.
  - Exact-phrase searches in English, German, Spanish and Japanese: the only hit was the Terms page.
  - GitHub and ToS;DR: no copies or history.
  - Wayback snapshots exist but could not be read from here: 2026-07-01, 2026-08-01, 2026-09-01 and 2026-09-20 (e.g. http://web.archive.org/web/20260920145005/https://www.tradingview.com/policies/). **Comparing these snapshots by hand is the fastest way to date the insertion.**
  - Under §1 of the Terms, changes take effect as soon as they are posted: "If you continue to use TradingView after we post changes … you are signifying your acceptance."
- **Circumstantial evidence (my inference):** the clause looks very new.
  - The Pine Script manual still says: "TradingView does not benefit from script sales. Transactions concerning invite-only scripts are strictly between users and vendors; they do not involve TradingView." (https://www.tradingview.com/pine-script-docs/writing/publishing/, undated, accessed 2026-09-29.)
  - The Vendor Requirements page doesn't mention the fee.
  - If the clause is already in force, the first count would be on Sep 30, 2026, with the invoice due by about Oct 30 and payment 14 days later.

**Open questions.** TradingView has published no FAQ on any of these, so each point below is my reading of the verified text:

| Question | What the text says | My reading |
|---|---|---|
| All users, or only those above 100? | The fee is "per user whose access … is active". The 100 figure is only a trigger: it "applies only where the total … exceeds 100". There is no "in excess of 100" wording. | A cliff. 100 users costs $0; 101 users costs $3,024.95/mo; 1,000 users costs $29,950/mo. |
| Are Paid Spaces subscribers exempt? | Section 22A "applies to all invite-only scripts and users". Vendor Requirements calls Paid Space scripts "special invite-only scripts". The Creator Program terms mention only the platform fee. | NOT FOUND: no exemption. Needs confirmation from TradingView. |
| Do free, trial or complimentary grants count? | No carve-out. The test is "active access" at month-end. | NOT FOUND: no exemption. |
| How are users counted across several scripts? | "Per user whose access to **any** invite-only script published by you" and "total number of users … to your invite-only scripts". | Unique users per vendor account, not per script. Not explicitly defined. |
| Anti-circumvention? | Section 22A has nothing on multiple accounts or revoking access before month-end. It relies on TradingView's "own records of access grants and script usage". | General rules still apply (see below). |

- **VERIFIED, general rules that could reach circumvention:**
  - House Rules: "Don't create duplicate accounts. Or fake accounts, spam accounts or accounts to work around a ban" (https://www.tradingview.com/support/solutions/43000591638-our-house-rules/, undated).
  - Vendor Requirements: "using that same creativity to sidestep our rules will cause you much more trouble than any gains" (https://www.tradingview.com/support/solutions/43000549951-vendor-requirements/, undated).
- **VERIFIED observation:** US$29.95 is exactly the Plus plan price ("$29.95 / mo billed annually", https://www.tradingview.com/pricing/, accessed 2026-09-29).

## 2. Paid Spaces

- **Platform fee, VERIFIED.** The Creator Program Terms, §5 (https://www.tradingview.com/support/solutions/43000772177-tradingview-creator-program-paid-spaces-terms/, undated, accessed 2026-09-29) say:
  - "The platform fee is currently 0% per transaction."
  - "TradingView may change the platform fee, but only with advance notice to Authors."
  - "Authors whose Paid Space was approved before April 1, 2026 keep a 0% platform fee … including after any later change to the standard fee."
  - "How to create a Paid Space", Step 4, also says 0% (https://www.tradingview.com/support/solutions/43000790233-how-to-create-a-paid-space/, undated).
  - A separate or non-zero rate for authors approved after April 1: **NOT FOUND**.
- **UNVERIFIED:** search-engine snippets of the same Creator Program terms read "0% per transaction, at least until October 1, 2026". That phrase is not on the live page (checked the English page, 2 regional English copies and 11 localized versions on 2026-09-29). A Wayback snapshot from 2026-09-10 exists that could confirm it.
- **Limits, VERIFIED, but the two pages conflict:**
  - The Terms (§3) say "one Paid Space containing up to 50 scripts (publicly available invite-only scripts are only allowed)".
  - The how-to article says "up to 25".
- **Eligibility, VERIFIED:**
  - Participation is by invitation only.
  - The author needs a Premium or Ultimate plan while applying and for as long as the Paid Space is active, plus a Partner Program account with a valid payment method.
  - Some regions are excluded ("including … Iran, North Korea and Russia") (Terms §3).
  - To apply, the author needs "at least one invite-only indicator or strategy that is visible to everyone … published more than 3 months ago and has received 100+ boosts" (https://www.tradingview.com/support/solutions/43000765878-can-i-offer-my-paid-pine-scripts-right-on-tradingview/, undated).
- **Billing, VERIFIED:**
  - Subscriptions are monthly and can only be bought on the web.
  - "Free and paid TradingView users can subscribe."
  - Price changes apply to existing subscribers from their next billing cycle ("Prices are not grandfathered").
  - VAT is added, and TradingView is the merchant of record (Terms §4; how-to article).
- **Refunds, VERIFIED:** "Paid Spaces subscriptions are eligible for a refund if requested within 7 calendar days after the payment is made" (Terms of Use §13, https://www.tradingview.com/policies/). Refunds and chargebacks are deducted from the author's earnings (Creator Program Terms §5).
- **Payouts, VERIFIED:**
  - Paid once a month through the Partner Program account, after a settlement period of up to 30 days.
  - USD only, via PayPal, with a US$100 minimum withdrawal.
  - TradingView may require a W-9 or W-8 once annual earnings reach US$600 (Creator Program Terms §5 to 6).
- **Creators, VERIFIED:**
  - Aug 12, 2026 blog (modified Aug 17): "Paid Spaces are already home to 39 creators … DeMARK, ChartPrime, Zeiierman, Steve Nison's Candle Scanner and BigBeluga. Subscriptions range from $4.99 to $199 per month". It adds: "Over 1,000 people have applied" (https://www.tradingview.com/blog/en/tradingview-creator-program-60011/).
  - On 2026-09-29, **https://www.tradingview.com/scripts/marketplace/ showed 47 Paid Spaces** priced from $4.99 to $199/mo. Examples:
    - AlgoAlpha "Unfair Advantage Pack", $65.57
    - ChartPrime Plus, $117
    - BigBeluga Premium, $66.47
    - Zeiierman, $95.20
    - DeMARK 9-13, $29.99
    - Trendoscope, $69.99
    - LonesomeTheBlue, $49.99
    - loxx, $120
    - toodegrees, $120
    - NisonCandleScanner, $199
    - BullByte, $199
  - **LuxAlgo and Market Cipher are not listed.**
  - Paid Spaces launched on Nov 13, 2025 (https://www.tradingview.com/blog/en/paid-indicators-strategies-on-tradingview-54934/).
- **Positioned as the alternative to the fee?** An explicit link is **NOT FOUND**. The Creator Program page pitches "No external websites or manual access needed" and "Skip the admin. We handle billing, renewals, cancellations and access management" (https://www.tradingview.com/creator-program/, undated).
- **History, VERIFIED:** TradingView closed its original Marketplace in favour of invite-only scripts in 2020 ("without a Marketplace in the way", Mar 4, 2020, https://www.tradingview.com/blog/en/leveling-the-playing-field-for-indicator-vendors-17040/). The site footer now links a "Marketplace" again.

## 3. Reaction and market response

- **NOT FOUND:** any public reaction to the Technology Fee on Reddit, X, YouTube, TradingView posts, blogs or news. What I tried:
  - Searches for the fee name, exact phrases from Section 22A and "$29.95 per user" in 4 languages.
  - Searches limited to X and to YouTube.
  - The websites of LuxAlgo, ChartPrime, BigBeluga, Zeiierman and AlgoAlpha.
  - TradingView's August blog posts (they have no comments).
  - GitHub issues.
  - Two third-party 2026 guides don't mention the fee: SulamX (Jul 28, 2026) and checkthat.ai (May 29, 2026).
- **Named vendors, VERIFIED on 2026-09-29:**
  - AlgoAlpha, ChartPrime, BigBeluga and Zeiierman all run Paid Spaces.
  - Some still sell outside TradingView too, which would expose them to the fee depending on how the Paid Spaces question is answered:
    - ChartPrime: "Register your email with Chartprime" and then "Link your Discord and TradingView accounts" (https://chartprime.com/, undated).
    - Zeiierman grants access through its own dashboard (https://www.zeiierman.com/how-to-tradingview/access-invite-only-scripts, Aug 20, 2025).
  - Price increases or user caps tied to the fee: **NOT FOUND**.
- **Adjacent competitor moves, VERIFIED. None of them cites the fee:**
  - **LuxAlgo:**
    - It acquired the open-source Pine runtime PineTS (Jun 1, 2026, https://www.luxalgo.com/blog/luxalgo-acquires-pinets-to-bring-pine-script-r-everywhere/).
    - It announced "LuxAlgo Is Now a Charting Platform" (Aug 31, 2026, https://www.luxalgo.com/blog/luxalgo-charting-platform/).
    - It released the open-source Vela charting engine (Sep 3, 2026, https://www.luxalgo.com/blog/introducing-vela/). Vela is Apache-2.0; its Pine add-on is AGPL-3.0. The post offers "the entire LuxAlgo Library cleared for use in the products you sell".
    - Its Sep 22, 2026 guide (https://www.luxalgo.com/blog/run-pine-script-outside-tradingview/) says: "What you cannot do is extract or run protected and invite-only scripts whose source you do not have."
    - LuxAlgo still publishes "certain" tools on TradingView (https://www.luxalgo.com/pricing/).
  - **OpenMarket** posted on X on 2026-09-27 (date decoded from the post ID): "TradingView charges $2,399 a year to plot 16 charts on one screen. Starting today, you can do the same for free on OpenMarket." (https://x.com/openmarket_xyz/status/2104254223517106349). It uses its own kScript language and supports "protected scripts". I found no paid-script marketplace (https://openmarket.xyz/learn/indicators).
- **NOT FOUND:** any platform courting TradingView vendors specifically because of the fee.
- **Related TradingView changes, VERIFIED:**
  - From Aug 14, 2026, every new script needs moderator approval before it appears in community feeds. Publishing is capped at "up to 5 new public scripts within 24 hours, and up to 15 within 30 days" (https://www.tradingview.com/blog/en/updated-script-publishing-60116/, modified Sep 9, 2026).
  - Public chats are retired on Sep 30, 2026 (https://www.tradingview.com/support/solutions/43000591339-public-chats-are-being-retired-on-sep-30-2026/).

## 4. How invite-only scripts work today

- **Plan required, VERIFIED:** "You can publish invite-only scripts and manage their access only if you have a Premium or Ultimate account" (Vendor Requirements). The Pine manual says "Premium and higher-tier plans". Prices on 2026-09-29, billed annually: Premium $59.95/mo, Ultimate $199.95/mo (pricing page).
- **Public vs private, VERIFIED:**
  - "A maximum of five users can access invite-only scripts that you publish privately."
  - Private scripts are not moderated, and selling access to them is banned.
  - Only public invite-only scripts and Paid Space scripts may be sold (Vendor Requirements).
- **Granting and revoking access, VERIFIED:**
  - Vendors add users manually by username in the "Manage access" dialog (Pine manual).
  - Access can be given an expiry date or none, edited later and the user list can be sorted by expiry (May 29, 2020, https://www.tradingview.com/blog/en/expiration-to-user-access-for-invite-only-scripts-18594/).
  - Vendors must grant access "only to users who explicitly request access" and remove users who ask. During a ban, vendors "can't grant users access" (Vendor Requirements).
- **Third-party automation tools, VERIFIED:**
  - **Whop:** its Sep 20, 2023 guide now tells sellers to "use the TradingView app" (https://whop.com/blog/selling-tradingview-indicators/). A vendor's buyer guide (Jan 22, 2025, https://stat-map.com/resources/how-to-claim-access-to-tradingview-indicators-on-whop) has buyers enter their TradingView username and then "Claim Indicators".
  - **Trendoscope's Tradingview-Access-Management** (https://github.com/trendoscope-algorithms/Tradingview-Access-Management): created 2022-08-17, 66 stars, 71 forks, updated 2026-08-29. It needs the vendor's TradingView username and password.
  - **Mathieu2301/TradingView-API** (https://github.com/Mathieu2301/TradingView-API, 5,398 stars): its `PinePermManager.js` calls TradingView's internal endpoints `/pine_perm/add/`, `/pine_perm/list_users/`, `/pine_perm/modify_user_expiration/` and `/pine_perm/remove/`.
  - **Newer tools:**
    - Chrome extensions: jayadevrana/tradingview-invite-only-access-manager (created 2026-07-18) and timurinci10/tradingview-access-automation (2026-07-28).
    - A Playwright bot, michaelvrxoj/tradingview-playwright-auto-invite-bot (2025-12-07).
    - A WordPress membership plugin, dearvn/membership-pro-tdv.
  - **LaunchPass:** no TradingView-specific integration found. **Discord bots:** only generic Discord-plus-TradingView account linking found (e.g. ChartPrime).
- **TradingView's stance on automation:** an official statement is **NOT FOUND**. Related, VERIFIED:
  - Terms §3: "Except as otherwise expressly permitted by separate agreement, we do not permit commercial usage of any of our services or APIs."
  - Terms §2: TradingView doesn't "guarantee backward compatibility of our services and Application Programming Interface (API)".
  - Trendoscope, a third party writing on TradingView (Nov 3, 2023, https://www.tradingview.com/chart/BTCUSDT/2Kfqz7TE-Revisiting-Automatic-Access-Management-API-for-Vendors/):
    - "Do not commercialize these API calls … The mechanism is built on backend calls that are not officially supported by tradingview. While tradingview is tolerant on individual use, any malicious activity may force them to shut this down for everyone."
    - Users "should disable 2FA".
  - Paid Spaces is TradingView's own automated alternative: "All billing, access and renewals are managed automatically by TradingView" (Creator Program Terms §4).

## 5. Terms and House Rules that matter to a competitor and to vendors who leave

All quotes are from https://www.tradingview.com/policies/ (undated; accessed 2026-09-29) unless noted.

- **Building or benchmarking a competing product:**
  - I found no general non-compete or benchmarking clause (searched for "compet" and "benchmark").
  - The only "competing" clause is in §25 (AI Features): users must not "use output to develop competing products or services".
  - §3 is broader and more relevant:
    - "Such prohibited cases also include creating products or services based on TradingView content, any processing of TradingView's content…"
    - Users may not copy TradingView's software or documentation, "including … translating, decompiling, disassembling or creating derivative works".
    - Content is licensed "for exclusive display-only use", and redistribution "for any form of compensation" is forbidden.
    - Third-party products enabling non-display use (including via webhooks) are banned, and TradingView reserves the right to audit, seek injunctions and claim damages.
- **Scraping:**
  - The live Terms contain no "scrape", "crawl", "spider" or "robot" wording (keyword check).
  - **UNVERIFIED:** ToS;DR's bot lists "Spidering, crawling or accessing the site through any automated means is not allowed" (https://edit.tosdr.org/documents/5591, undated). It may reflect an older version of the Terms.
- **Promotion and links, VERIFIED:**
  - House Rules: "All content should be ad-free … this ban covers all advertisements, logos, links or references to any website, social media, messaging or email contacts, company names…". The one exception is the Signature field, open to "Premium, Expert and Ultimate subscribers".
  - Script Publishing Rules: "do not use your script's description, release notes, title, chart or code to share links or references to social media or other websites" (https://www.tradingview.com/support/solutions/43000590599-script-publishing-rules/, undated).
  - Vendor Requirements:
    - Prices may appear only in the "Author's instructions" field or the Signature.
    - Author's instructions may "include a link to your webpage where users can request access".
    - Vendors must not reference their Signature anywhere else.
  - Terms §5: "Unauthorized soliciting on TradingView is strictly prohibited."
- **Who owns published scripts, VERIFIED:**
  - Authors warrant that they hold the rights. TradingView gets a "world-wide, irrevocable, perpetual, royalty-free, sub-licensable license" that "survives termination" (§22).
  - After an account is closed, TradingView "may … continue to host, publish, display and make available any script you have published … including to users who had access before the termination … and to new users" (§22).
  - Default licence: without a stated licence, "your script is licensed under the Mozilla Public License 2.0" (§22).
  - Published scripts "will remain on the site at our discretion" even after the account is deleted (§18).
  - A public script can only be edited or deleted within 15 minutes of publishing (Pine manual).
  - TradingView's code-reuse rules "take precedence over any provisions from an open-source license" (Pine manual).
- **"Pine Script" trademark, VERIFIED:**
  - USPTO Reg. No. **7,559,746** (Serial 97298638), filed Mar 7, 2022 and registered Nov 5, 2024 on the Principal Register.
  - It covers Class 42 (online programming-language and software services). The word "SCRIPT" is disclaimed. The owner is TradingView, Inc. and the status is LIVE (https://tsdr.uspto.gov/statusview/sn97298638, generated 2026-09-29).
  - TradingView marks it "Pine Script®" across its site. LuxAlgo publishes a matching disclaimer that the names are TradingView's trademarks.
- **TradingView's charting code, VERIFIED:**
  - Lightweight Charts is Apache-2.0, but its licence "requires specifying TradingView as the product creator" with a link to tradingview.com (https://github.com/tradingview/lightweight-charts, README).
  - The free Advanced Charts licence agreement (https://s3.amazonaws.com/tradingview/charting_library_license_agreement.pdf) is an image-only PDF and was **NOT reviewed**.

---

## Source URLs

**TradingView**
- https://www.tradingview.com/policies/ (and localized copies, e.g. https://de.tradingview.com/policies/, https://ru.tradingview.com/policies/)
- https://www.tradingview.com/support/solutions/43000549951-vendor-requirements/
- https://www.tradingview.com/support/solutions/43000590599-script-publishing-rules/
- https://www.tradingview.com/support/solutions/43000591638-our-house-rules/
- https://www.tradingview.com/support/solutions/43000772177-tradingview-creator-program-paid-spaces-terms/
- https://www.tradingview.com/support/solutions/43000765878-can-i-offer-my-paid-pine-scripts-right-on-tradingview/
- https://www.tradingview.com/support/solutions/43000765877-what-s-a-paid-space/
- https://www.tradingview.com/support/solutions/43000790233-how-to-create-a-paid-space/
- https://www.tradingview.com/support/solutions/43000615189-private-invite-only-scripts/
- https://www.tradingview.com/support/solutions/43000614617-publishing-invite-only-scripts/
- https://www.tradingview.com/support/solutions/43000591339-public-chats-are-being-retired-on-sep-30-2026/
- https://www.tradingview.com/creator-program/
- https://www.tradingview.com/scripts/marketplace/
- https://www.tradingview.com/spaces/AlgoAlpha/
- https://www.tradingview.com/spaces/ChartPrime/
- https://www.tradingview.com/pricing/
- https://www.tradingview.com/pine-script-docs/writing/publishing/
- https://www.tradingview.com/blog/en/tradingview-creator-program-60011/ (Aug 12, 2026)
- https://www.tradingview.com/blog/en/updated-script-publishing-60116/ (Aug 14, 2026)
- https://www.tradingview.com/blog/en/paid-indicators-strategies-on-tradingview-54934/ (Nov 13, 2025)
- https://www.tradingview.com/blog/en/leveling-the-playing-field-for-indicator-vendors-17040/ (Mar 4, 2020)
- https://www.tradingview.com/blog/en/expiration-to-user-access-for-invite-only-scripts-18594/ (May 29, 2020)
- https://www.tradingview.com/chart/BTCUSDT/2Kfqz7TE-Revisiting-Automatic-Access-Management-API-for-Vendors/ (Nov 3, 2023)

**Trademark and licences**
- https://tsdr.uspto.gov/statusview/sn97298638
- https://github.com/tradingview/lightweight-charts
- https://edit.tosdr.org/documents/5591

**Competitors and vendors**
- https://www.luxalgo.com/pricing/
- https://www.luxalgo.com/blog/
- https://www.luxalgo.com/blog/luxalgo-acquires-pinets-to-bring-pine-script-r-everywhere/
- https://www.luxalgo.com/blog/luxalgo-charting-platform/
- https://www.luxalgo.com/blog/introducing-vela/
- https://www.luxalgo.com/blog/run-pine-script-outside-tradingview/
- https://x.com/openmarket_xyz/status/2104254223517106349
- https://openmarket.xyz/learn/indicators
- https://chartprime.com/
- https://www.zeiierman.com/how-to-tradingview/access-invite-only-scripts

**Access-automation tools**
- https://whop.com/blog/selling-tradingview-indicators/
- https://stat-map.com/resources/how-to-claim-access-to-tradingview-indicators-on-whop
- https://github.com/trendoscope-algorithms/Tradingview-Access-Management
- https://github.com/Mathieu2301/TradingView-API
- https://github.com/jayadevrana/tradingview-invite-only-access-manager
- https://github.com/timurinci10/tradingview-access-automation
- https://github.com/michaelvrxoj/tradingview-playwright-auto-invite-bot
- https://github.com/dearvn/membership-pro-tdv

**Wayback snapshots (exist but could not be read from here; worth checking by hand)**
- http://web.archive.org/web/20260701145005/https://www.tradingview.com/policies/
- http://web.archive.org/web/20260801155135/https://www.tradingview.com/policies/
- http://web.archive.org/web/20260901145005/https://www.tradingview.com/policies/
- http://web.archive.org/web/20260920145005/https://www.tradingview.com/policies/
- http://web.archive.org/web/20260910023154/https://www.tradingview.com/support/solutions/43000772177-tradingview-creator-program-paid-spaces-terms/
