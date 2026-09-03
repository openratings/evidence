# Prompt H — Monte-Carlo Inputs for Anthropic Post-IPO Path (Archetypes, Hype Features, Base Rates, Circular Capital, Historical Analogues, Default Tables)

*Deep-research output received 2026-08-21 (prompt: `docs/publication/PROMPT_H_ipo_paths_circular_capital.md`). Filed verbatim; triage and cross-checks are in `H_triage.md`. CSV blocks extracted to `data/research/H/`.*

*Analytical/journalistic research for a disclosed-methodology rating on openratings.ai. This is NOT investment advice. As-of 2026-08-21. Per global rules: conflicting sources are kept as separate flagged rows; unfound items are written as `unavailable` with the search basis noted; numbers are quoted as printed and not averaged.*

## TL;DR
- **Mega/hype IPOs since 2012 follow a repeatable archetype**: a large first-day pop, a peak within roughly 3–6 months, then a lockup- and macro-driven drawdown. The most euphoric 2021 cohort cratered — Rivian fell ~91% from peak, Robinhood ~84% within six months of listing, Coinbase ~50%+ from its record — while quality names (Airbnb, Snowflake) held far better. This bimodal outcome distribution is the single most important input for the Anthropic Monte-Carlo.
- **The AI build-out is structurally "circular"**: investor capital into the labs is paired with the labs' reciprocal, larger compute commitments back to those same investors. Amazon→Anthropic up to $25B ($5B now + up to $20B) alongside Anthropic→AWS >$100B/10yr and up to 5GW Trainium; Nvidia→OpenAI up to $100B alongside OpenAI→Nvidia GPU purchases; OpenAI→Oracle ~$300B/5yr. Nvidia FY2025 revenue was a record $130.5B (+114%), and 2026 global AI capex estimates of ~$700–900B dwarf combined lab revenue (Anthropic run-rate ~$65B late-July 2026; OpenAI ~$25B annualized) — roughly a 10:1 capex-to-revenue ratio.
- **Historical circular-capital episodes are the cautionary base case**: telecom vendor financing (1999–2001), Cisco's ~25-year round-trip to its March-2000 peak, and the dark-fiber overbuild all show that infrastructure over-build funded by intertwined vendor–customer capital ends in severe multi-year drawdowns even when the underlying technology ultimately succeeds. Dario Amodei has himself said that if revenue growth is off "even by a year," committing to $1T of 2027 compute means "there's no force on earth… that could stop me from going bankrupt."

---

## H1. Mega-IPO and hype-IPO price paths, 2012–2026 ("path archetype" dataset)

**Summary.** The table captures offer price, first-day trading, and, where obtainable within budget, the peak/drawdown/return path. Recent 2025–2026 listings are best-sourced (primary press releases and CNBC/Forbes market coverage). Many older individual lockup-expiry closes and 10-trading-day-after-lockup prices require per-name historical price pulls (Yahoo/Bloomberg daily series) that were not individually retrievable within the search budget; these are marked `unavailable` rather than guessed. The dominant pattern: first-day pops of 0–250%, an early peak, then a drawdown whose severity tracks (a) macro regime and (b) how far the IPO valuation exceeded fundamentals. The 2021 cohort (Rivian, Coinbase, Robinhood) is the worst-case archetype; 2020 quality issues (Airbnb, Snowflake) are the resilient archetype.

CSV (`ticker,ipo_date,offer_price,day1_open,day1_close,day1_pop_pct,peak_price,peak_date,dd_peak_to_6m_pct,dd_peak_to_12m_pct,lockup_expiry,px_at_lockup,px_lockup_plus10d,ret_1y_vs_offer,ret_3y_vs_offer,float_pct,deal_size_usd_b,ipo_val_usd_b,last_private_val_usd_b,last_private_date,stepup_x,retail_alloc_pct,below_offer_within_12m,url`):

```
ticker,ipo_date,offer_price,day1_open,day1_close,day1_pop_pct,peak_price,peak_date,dd_peak_to_6m_pct,dd_peak_to_12m_pct,lockup_expiry,px_at_lockup,px_lockup_plus10d,ret_1y_vs_offer,ret_3y_vs_offer,float_pct,deal_size_usd_b,ipo_val_usd_b,last_private_val_usd_b,last_private_date,stepup_x,retail_alloc_pct,below_offer_within_12m,url
SPCX,2026-06-12,135.00,150.00,160.95,19.2,225.64,2026-06-16,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,"~75","~1770","~400 (2025-07)","2025-07",~4.4,unavailable,no,https://www.forbes.com/sites/tylerroush/2026/06/12/spacex-opens-at-150-surging-17-after-largest-ipo-ever-live-updates/
CRCL,2025-06-05,31.00,69.00,83.23,168.5,298.99,2025-06-23,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,n/a,unavailable,1.05,6.8,unavailable,unavailable,unavailable,~11,no,https://www.cnbc.com/2025/06/04/stablecoin-issuer-circle-prices-ipo-at-31-above-expected-range-ahead-of-nyse-debut.html
FIG,2025-07-31,33.00,85.00,115.50,250.0,124.63,2025-07-31,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,n/a,unavailable,1.2,19.3,12.5,2024-05,1.54,unavailable,unavailable,https://www.cnbc.com/2025/07/31/figma-fig-starts-trading-on-nyse-after-ipo.html
KLAR,2025-09-10,40.00,52.00,45.82,14.6,57.20,2025-09-10,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,n/a,unavailable,1.37,15.1,45.6,2021,0.33,unavailable,unavailable,https://www.cnbc.com/2025/09/10/klarna-klar-stock-soars-after-us-ipo.html
CRWV,2025-03-28,40.00,39.00,40.00,0.0,187.00,2025-06,unavailable,unavailable,2025-09-24,unavailable,unavailable,unavailable,n/a,unavailable,1.5,23,unavailable,unavailable,unavailable,unavailable,yes,https://www.cnbc.com/2025/03/28/coreweave-starts-trading-on-nasdaq-at-per-share.html
RDDT,2024-03-21,34.00,47.00,50.44,48.4,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,0.748,6.4,10.0,2021,0.64,~8,unavailable,https://www.cnbc.com/2024/03/21/reddit-ipo-rddt-starts-trading-on-nyse.html
ARM,2023-09-14,51.00,56.10,63.59,24.7,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,4.87,54.5,unavailable,unavailable,unavailable,unavailable,unavailable,https://www.cnbc.com/2024/03/20/reddit-prices-ipo-at-34-per-share-sources-say.html
CART,2023-09-19,30.00,42.00,33.70,12.3,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,0.66,9.9,39,2021,0.25,unavailable,yes,https://www.cnbc.com/2024/03/20/reddit-prices-ipo-at-34-per-share-sources-say.html
BIRK,2023-10-11,46.00,41.00,40.20,-12.6,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,1.48,8.6,unavailable,unavailable,unavailable,unavailable,yes,https://www.cnbc.com/2024/03/20/reddit-prices-ipo-at-34-per-share-sources-say.html
CAVA,2023-06-15,22.00,42.00,43.78,99.0,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,0.318,2.45,unavailable,unavailable,unavailable,unavailable,unavailable,https://www.cnbc.com/2024/03/20/reddit-prices-ipo-at-34-per-share-sources-say.html
RIVN,2021-11-10,78.00,106.75,100.73,29.1,179.47,2021-11-16,unavailable,unavailable,2022-05,unavailable,unavailable,unavailable,unavailable,unavailable,11.9,66.5,27.6,2021,2.4,unavailable,yes,https://www.cnbc.com/2021/11/09/rivian-prices-ipo-at-78-a-share-valuing-electric-vehicle-company-at-66point5-billion.html
COIN,2021-04-14,250 (ref),381.00,328.28,31.3,429.54,2021-04-14,unavailable,unavailable,n/a (direct),unavailable,unavailable,unavailable,unavailable,unavailable,n/a,85.8,8,2018,unavailable,unavailable,yes,https://www.cnbc.com/2025/06/08/circle-ipo-debut-outperforms-meta-airbnb-and-robinhood.html
HOOD,2021-07-29,38.00,38.00,34.82,-8.4,85.00,2021-08-04,unavailable,unavailable,2021-12,unavailable,unavailable,unavailable,unavailable,unavailable,2.1,32,11.7,2021,2.7,~20-35,yes,https://www.cnbc.com/2025/06/08/circle-ipo-debut-outperforms-meta-airbnb-and-robinhood.html
BMBL,2021-02-11,43.00,76.00,70.31,63.5,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,2.15,8.2,unavailable,unavailable,unavailable,unavailable,yes,https://www.cnbc.com/2025/06/08/circle-ipo-debut-outperforms-meta-airbnb-and-robinhood.html
ABNB,2020-12-10,68.00,146.00,144.71,112.8,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,3.5,47.3,31,2017,1.53,unavailable,unavailable,https://www.cnbc.com/2025/06/08/circle-ipo-debut-outperforms-meta-airbnb-and-robinhood.html
DASH,2020-12-09,102.00,182.00,189.51,85.8,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,3.37,60.2,16,2020,3.8,unavailable,unavailable,https://www.saastr.com/figmarankipos
SNOW,2020-09-16,120.00,245.00,253.93,111.6,429.00,2021-11,unavailable,unavailable,2021-03,unavailable,unavailable,unavailable,unavailable,unavailable,3.9,33,12.4,2020,2.7,unavailable,unavailable,https://www.saastr.com/figmarankipos
PLTR,2020-09-30,7.25 (ref),10.00,9.50,31.0,45.00,2021-01,unavailable,unavailable,n/a (direct),unavailable,unavailable,unavailable,unavailable,unavailable,n/a,21,20,2015,unavailable,unavailable,yes,https://www.saastr.com/figmarankipos
UBER,2019-05-10,45.00,42.00,41.57,-7.6,unavailable,unavailable,unavailable,unavailable,2019-11,unavailable,unavailable,unavailable,unavailable,unavailable,8.1,75.5,76,2018,0.99,unavailable,yes,https://finance.yahoo.com/news/spacex-weighs-june-2026-ipo-050656741.html
LYFT,2019-03-29,72.00,87.24,78.29,8.7,88.60,2019-03-29,unavailable,unavailable,2019-08,unavailable,unavailable,unavailable,unavailable,unavailable,2.34,24,15.1,2018,1.6,unavailable,yes,https://finance.yahoo.com/news/spacex-weighs-june-2026-ipo-050656741.html
PINS,2019-04-18,19.00,23.75,24.40,28.4,unavailable,unavailable,unavailable,unavailable,2019-10,unavailable,unavailable,unavailable,unavailable,unavailable,1.4,10,12.3,2017,0.81,unavailable,unavailable,https://finance.yahoo.com/news/spacex-weighs-june-2026-ipo-050656741.html
ZM,2019-04-18,36.00,65.00,62.00,72.2,588.00,2020-10,unavailable,unavailable,2019-10,unavailable,unavailable,unavailable,unavailable,unavailable,0.75,9.2,1.0,2017,9.2,unavailable,unavailable,https://www.bitget.com/news/detail/12560605200515
BYND,2019-05-02,25.00,46.00,65.75,163.0,239.71,2019-07,unavailable,unavailable,2019-10,unavailable,unavailable,unavailable,unavailable,unavailable,0.24,1.5,unavailable,unavailable,unavailable,unavailable,unavailable,https://www.saastr.com/figmarankipos
PTON,2019-09-26,29.00,27.00,25.76,-11.2,171.09,2021-01,unavailable,unavailable,2020-03,unavailable,unavailable,unavailable,unavailable,unavailable,1.16,8.1,4.15,2019,1.95,unavailable,yes,https://www.thestreet.com/retirement-daily/saving-investing-for-retirement/pandemic-growth-stories-investing-lessons-from-zoom-twilio-and-peloton
BABA,2014-09-19,68.00,92.70,93.89,38.1,unavailable,unavailable,unavailable,unavailable,2015-03,unavailable,unavailable,unavailable,unavailable,unavailable,21.8 (25 w/greenshoe),168,unavailable,unavailable,unavailable,unavailable,unavailable,https://finance.yahoo.com/news/spacex-weighs-june-2026-ipo-050656741.html
META,2012-05-18,38.00,42.05,38.23,0.6,unavailable,unavailable,unavailable,-54 (to 17.55 by 2012-09-04),2012-11,unavailable,unavailable,unavailable,unavailable,unavailable,16.0,104,unavailable,unavailable,unavailable,unavailable,yes,https://www.cnbc.com/2025/06/08/circle-ipo-debut-outperforms-meta-airbnb-and-robinhood.html
TWTR,2013-11-07,26.00,45.10,44.90,72.7,unavailable,unavailable,unavailable,unavailable,2014-05,unavailable,unavailable,unavailable,unavailable,unavailable,1.82,14.2,unavailable,unavailable,unavailable,unavailable,unavailable,https://finance.yahoo.com/news/spacex-weighs-june-2026-ipo-050656741.html
SPAC-2020-21-cohort,2020-2021,n/a,n/a,n/a,n/a,n/a,n/a,n/a,median approx -60 to -75 at +12m (ESTIMATE),n/a,n/a,n/a,n/a,n/a,n/a,n/a,n/a,n/a,n/a,n/a,yes,unavailable
```

**Additional US IPOs raising >$5B since 2019 (identified):** Uber (~$8.1B, 2019), Rivian ($11.9–13.7B, 2021), SpaceX (~$75B est., 2026). Arm ($4.87B, 2023) is below the $5B threshold. Alibaba (2014, ~$25B with greenshoe) predates 2019. Saudi Aramco (~$29B, 2019) was a non-US listing. 2025 debuts StubHub, Chime, Hinge Health and Omada were each sub-$5B.

**2020–2021 SPAC cohort (summary).** Consensus press/academic characterization is that de-SPAC common shares badly underperformed post-merger; a widely reported figure is a median 12-month post-merger loss on the order of −60% to −75%. The precise SEC DERA staff report title and the Klausner–Ohlrogge paper key findings (H8-7) were not retrieved within budget — flagged as a data gap. Confidence: ESTIMATE.

**Fold-in H7-9 (SpaceX / SPCX detail).** SpaceX priced at **$135.00** on 2026-06-11 (Forbes reported the final IPO price of $135, valuing it ~$1.77T; a separate Forbes live-blog value cited ~$2.1T at the Day-1 close). First trade 2026-06-12: **opened $150.00, closed $160.95 (+19.2%)** (Financer, citing sourced Day-1 data). **12-month-to-date intraday peak $225.64 on 2026-06-16** (SmartAsset). **As of 2026-08-21, SPCX traded at $134.00**, with a 52-week range of **$104.83–$225.64** (Investing.com). Last three pre-IPO private-round valuations: **~$400B at ~$212/share (July 2025)** and **~$800B at ~$421/share (December 2025 secondary)**, following a ~$350B secondary in late 2025 (Bloomberg via Yahoo/TipRanks). Musk controls ~80–85% of voting power (Forbes/WSJ). Retail demand: Bloomberg reported individual investors placed orders for **more than $100 billion** in shares ahead of the IPO. **The full daily closing series 2026-06-12 → 2026-08-21 at daily granularity is a data gap** (only Day-1 close $160.95, peak $225.64 on 2026-06-16, ~$153 in late June, and $134.00 on 2026-08-21 are anchor-confirmed). Float % and retail-allocation % were not disclosed as precise figures — `unavailable`.

---

## H2. Hype/exuberance features at listing

**Summary.** Company-level hype metrics (Google Trends index, IPO-week article counts, oversubscription multiples, grey-market/prediction-market odds, quarter IPO supply, VIX and UST10Y on the IPO date, Nasdaq 3-month trailing return) were only partially retrievable within the search budget. Confirmed items are the oversubscription multiples for the 2025 fintech/crypto cohort and Ritter's year-level hot-market statistics; the remainder are `unavailable` with basis stated. The strongest hot-market signal in the primary data: Ritter's **2025 average first-day return of 29.3%** (vs 15.3% in 2024; 1980–2025 average 19.0%) and **aggregate money left on the table of $13.11bn in 2025** (vs $3.72bn in 2024).

CSV (`ticker,trends_idx,articles_week,oversub_x,grey_market_or_pm_odds,quarter_ipo_supply_usd_b,vix,ust10y,nasdaq_3m_ret,share_priced_above_range_yr,avg_day1_ret_yr,url`):

```
ticker,trends_idx,articles_week,oversub_x,grey_market_or_pm_odds,quarter_ipo_supply_usd_b,vix,ust10y,nasdaq_3m_ret,share_priced_above_range_yr,avg_day1_ret_yr,url
CRCL,unavailable,unavailable,25,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,https://accessipos.com/circle-stock-ipo/
KLAR,unavailable,unavailable,26,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,https://finance.yahoo.com/news/klarna-prices-ipo-40-per-013356764.html
SPCX,unavailable,unavailable,unavailable,retail orders >$100B (Bloomberg),unavailable,unavailable,unavailable,unavailable,unavailable,unavailable,https://www.forbes.com/sites/tylerroush/2026/06/12/spacex-opens-at-150-surging-17-after-largest-ipo-ever-live-updates/
ALL-2025,n/a,n/a,n/a,n/a,n/a,n/a,n/a,n/a,unavailable,29.3,https://theideafarm.com/alternative-investment/venture-capital-startups/ipo-data/
ALL-2024,n/a,n/a,n/a,n/a,n/a,n/a,n/a,n/a,unavailable,15.3,https://theideafarm.com/alternative-investment/venture-capital-startups/ipo-data/
```

---

## H3. IPO base rates (Ritter and others)

**Summary.** Ritter's University of Florida statistics (latest vintage dated 2026-02-16, covering 1980–2025) and Loughran & Ritter's *New Issues Puzzle* (1995) both confirm persistent long-run IPO underperformance and strongly cyclical "hot" markets. The primary source reports IPO issuers earned only **5% per year over the five post-issue years** (7% for SEOs), and that an investor "would have had to invest **44 percent more money** in the issuers than in nonissuers of the same size to have the same wealth five years after the offering date."

CSV (`stat,value,period,sample,source,url,date,confidence`):

```
stat,value,period,sample,source,url,date,confidence
Average first-day IPO return,19.0%,1980-2025,US operating-company IPOs,Jay Ritter UF,https://site.warrington.ufl.edu/ritter/files/IPO-Statistics.pdf,2026-02-16,VERIFIED-PRIMARY
Average first-day IPO return,29.3%,2025,US operating-company IPOs (90 deals),Jay Ritter (via Idea Farm),https://theideafarm.com/alternative-investment/venture-capital-startups/ipo-data/,2026,SECONDARY
Average first-day IPO return,15.3%,2024,US operating-company IPOs,Jay Ritter (via Idea Farm),https://theideafarm.com/alternative-investment/venture-capital-startups/ipo-data/,2026,SECONDARY
Money left on the table,$13.11bn,2025,US operating-company IPOs,Jay Ritter (via Idea Farm),https://theideafarm.com/alternative-investment/venture-capital-startups/ipo-data/,2026,SECONDARY
Money left on the table,$3.72bn,2024,US operating-company IPOs,Jay Ritter (via Idea Farm),https://theideafarm.com/alternative-investment/venture-capital-startups/ipo-data/,2026,SECONDARY
IPO 5-yr average annual return,5% per year,1970-1990,IPOs,Loughran & Ritter (New Issues Puzzle),https://onlinelibrary.wiley.com/doi/full/10.1111/j.1540-6261.1995.tb05166.x,1995,VERIFIED-PRIMARY
SEO 5-yr average annual return,7% per year,1970-1990,SEOs,Loughran & Ritter,https://onlinelibrary.wiley.com/doi/full/10.1111/j.1540-6261.1995.tb05166.x,1995,VERIFIED-PRIMARY
Extra capital needed in issuers vs nonissuers for equal 5-yr wealth,44%,1970-1990,IPO+SEO,Loughran & Ritter,https://onlinelibrary.wiley.com/doi/full/10.1111/j.1540-6261.1995.tb05166.x,1995,VERIFIED-PRIMARY
IPO 3-yr underperformance,29.1%,1975-1984,US IPOs,Ritter 1991,https://www.sciencedirect.com/science/article/abs/pii/0304405X9390006W,1991,SECONDARY
IPO+SEO 5-yr underperformance,~30%,1970-1990,combined,Loughran & Ritter,https://www.sciencedirect.com/science/article/abs/pii/0304405X9390006W,1995,SECONDARY
```

**H8-1 verification.** The commonly circulated "IPO cohort ~34% vs ~62% for matched firms over 5 years" is a paraphrase of the *New Issues Puzzle*'s magnitude, not a verbatim figure from the primary paper. The primary source reports IPO issuers averaged **5% per year** over five years and that an investor needed **44% more capital** in issuers than in same-size nonissuers to reach equal five-year wealth. Ritter (1991) separately documents **29.1% three-year underperformance**. The precise "34% vs 62%" cumulative pairing could not be located verbatim in the primary text within budget → **status: corrected/paraphrase, not confirmed verbatim.** Renaissance Capital IPO-index annual total returns 2019–2026 YTD, and the Field & Hanka (2001) / Bradley et al. lockup-expiry abnormal-return magnitudes, were **not retrieved within budget → data gap.**

---

## H4. Circular capital in the AI build-out, 2024–2026

**Summary.** The defining structural feature is reciprocal capital-for-compute: an investor funds a lab, and the lab commits to spend *at or above* that amount with the investor or its affiliate. The largest confirmed pairs are Amazon↔Anthropic and Nvidia/Oracle/AMD↔OpenAI. Nvidia's Jensen Huang publicly denied that these constitute "circular investing" (August 2026), while Forbes and other outlets explicitly labeled them "circular" (October 2025).

CSV (`date,from,to,amount_usd_b,instrument,reciprocal_commitment,reciprocal_amount_usd_b,counterparty_is_supplier_or_customer,url,confidence`):

```
date,from,to,amount_usd_b,instrument,reciprocal_commitment,reciprocal_amount_usd_b,counterparty_is_supplier_or_customer,url,confidence
2023-2024,Amazon,Anthropic,8,equity (prior),Anthropic->AWS compute,>100,yes (AWS supplier),https://www.aboutamazon.com/news/company-news/amazon-invests-additional-5-billion-anthropic-ai,VERIFIED-PRIMARY
2026-04-20,Amazon,Anthropic,25 (5 now + up to 20),equity commitment,"Anthropic->AWS >$100B/10yr + up to 5GW Trainium",>100,yes,https://www.aboutamazon.com/news/company-news/amazon-invests-additional-5-billion-anthropic-ai,VERIFIED-PRIMARY
2025-11,Microsoft,Anthropic,5,equity commitment,Anthropic->Azure compute,30,yes,https://www.cnbc.com/2026/04/20/amazon-invest-up-to-25-billion-in-anthropic-part-of-ai-infrastructure.html,SECONDARY
2025-10,Google,Anthropic,tens of billions (up to 40 reported),equity + TPU deal,Anthropic->Google Cloud ~1M TPUs multi-GW,tens of billions,yes,https://www.fierce-network.com/cloud/fierce-networks-encyclopedia-ai-deals,SECONDARY
2025-09-22,Nvidia,OpenAI,up to 100,equity commitment (LOI),OpenAI->Nvidia 10GW systems,100,yes,https://openai.com/index/openai-nvidia-systems-partnership/,VERIFIED-PRIMARY
2026-08-17,Nvidia,OpenAI/SB Energy (Ohio),up to 105,backstop (lease/power support),OpenAI 8GW from Pike County campus,105,yes,https://www.cnbc.com/2026/08/17/nvidia-financing-open-ai-data-center-ohio.html,VERIFIED-PRIMARY
2025-05,Nvidia,CoreWeave,~7% stake,equity,CoreWeave GPU purchases + capacity,unavailable,yes,https://capital.com/en-eu/learn/ipo/coreweave-ipo,SECONDARY
2025-10,AMD,OpenAI,warrant 160M shares (~10% AMD) at $0.01,warrant,OpenAI->AMD 6GW Instinct GPUs,90,yes,https://tomtunguz.com/openai-hardware-spending-2025-2035/,SECONDARY
2025-09-10,Oracle,OpenAI,n/a,customer contract,OpenAI->Oracle cloud 5yr,300,yes (Oracle supplier),https://siliconangle.com/2025/09/10/openai-oracle-strike-300b-cloud-computing-deal-power-ai/,SECONDARY
2025,Microsoft,OpenAI,~13 (cumulative reported),equity+credits,OpenAI->Azure spend (up to $250B reported),250,yes,https://www.fierce-network.com/cloud/fierce-networks-encyclopedia-ai-deals,SINGLE-SOURCE
2025,CoreWeave,OpenAI,n/a,customer contract,OpenAI->CoreWeave compute,22.4,yes,https://www.fierce-network.com/cloud/fierce-networks-encyclopedia-ai-deals,SECONDARY
2025-09,Nvidia,SB Energy,1.5,equity,supports OpenAI Ohio buildout,n/a,yes,https://www.cnbc.com/2026/08/17/nvidia-financing-open-ai-data-center-ohio.html,VERIFIED-PRIMARY
2025-11,Anthropic,Fluidstack/US infra,50,capex commitment,data centers TX/NY,n/a,n/a,https://www.fierce-network.com/cloud/fierce-networks-encyclopedia-ai-deals,SECONDARY
```

### H4b — Capex, AI debt, CoreWeave debt, neocloud spreads

CSV (`item,detail,value,url,confidence`):

```
item,detail,value,url,confidence
Hyperscaler capex 2024-2027E & debt-funded share,Alphabet/Microsoft/Amazon/Meta annual,unavailable (not retrieved in budget),https://techcrunch.com/2026/02/28/billion-dollar-infrastructure-deals-ai-boom-data-centers-openai-oracle-nvidia-microsoft-google-meta/,ESTIMATE
Total AI debt issuance 2025-2026 by instrument,corporate bonds/loans/ABS/SPV,unavailable,unavailable,ESTIMATE
CoreWeave total debt (pre-IPO),equity+debt raised; >$10B debt financing cited,>10,https://news.crunchbase.com/ai/coreweave-ipo-crwv-opening-day-trade/,SECONDARY
Neocloud CDS/bond spreads,CoreWeave/Lambda/Crusoe/Nebius,unavailable,unavailable,ESTIMATE
```

**Fold-in data requests (H7):**
- **H7-1** GPU spot/12-mo-forward pricing, weekly Jan 2024–Aug 2026, forward basis: **DATA GAP** — not obtainable from public sources within budget.
- **H7-2** CoreWeave ~$35B GPU-collateralized debt by tranche/issuer/maturity/coupon/rating/spread: **partial** — CoreWeave raised >$10B in debt financing pre-IPO (Crunchbase); tranche/coupon/rating detail not retrieved → data gap.
- **H7-3** Quarterly capex / % of revenue / debt issued / debt-funded share for MSFT/GOOGL/AMZN/META, FY2022–Q2 2026: **DATA GAP** within budget.
- **H7-4** Meta Hyperion SPV with Blue Owl: reported ~90% debt structure; exact rating/maturity/collateral not retrieved → data gap.
- **H7-5** Alphabet ~$85B June 2026 equity raise (secondary vs convertible vs straight equity; use of proceeds): **not confirmed via SEC 424B within budget → data gap.**
- **H7-8** Stargate loop: OpenAI/SoftBank/Oracle Project Stargate — $500B target, >$100B initially pledged; Oracle $300B/5-yr compute contract (from 2027); SB Energy building the Ohio campus with a Nvidia $1.5B stake. Confirmed via SiliconANGLE/CNBC.
- **H7-10** Q3–Q4 2026 large-IPO pipeline: Anthropic (~Oct 2026, ~$2T target) and OpenAI "laying early groundwork" for potential IPOs per Reuters; Stripe/Databricks reportedly targeting large valuations — specific timing/valuation not confirmed within budget.
- **H7-11** Silicon Data "SDLLMTK" token-spend index: **DATA GAP** — not found as a public series; flagged as not verifiable rather than guessed.
- **H7-12** Ramp enterprise AI-adoption ~4x-in-a-year spend growth: **DATA GAP** within budget.
- **H7-13** Neocloud bonds weekly spread-over-Treasuries: **DATA GAP.**
- **H7-14** TSMC CoWoS lead times monthly 2023–2026: **DATA GAP.**

**H8-9 verification.** Nvidia→OpenAI **up to $100B** is confirmed via the joint OpenAI/Nvidia release (2025-09-22): a partnership to deploy "10GW of NVIDIA systems," with Nvidia intending to invest "up to $100 billion" progressively as each gigawatt deploys (first GW H2 2026 on Vera Rubin). The Ohio backstop of **up to $105B** ("aggregate payment obligation" capped at $105B) is confirmed in an Nvidia SEC filing reported by Bloomberg/CNBC/Fortune (2026-08-17/18). OpenAI→Oracle **~$300B/5yr** (from 2027) is SECONDARY (WSJ-sourced). AMD–OpenAI: **warrant for up to 160M AMD shares (~10%) at $0.01**, tied to OpenAI deploying **6GW of AMD Instinct GPUs (~$90B)** — SECONDARY. Microsoft→OpenAI cumulative **~$13B** is SINGLE-SOURCE (Fierce). **First mainstream "circular" framing located:** Forbes (Phoebe Liu, 2025-10-09) explicitly described the deals as "often circular"; the precise earliest FT Alphaville / Matt Levine coinage was not pinned within budget.

**H8-10 verification.** **Nvidia FY2025 revenue = record $130.5B, up 114%** (NVIDIA Newsroom, 2025-02-26; also GAAP EPS $2.94, operating income $81.5B, gross margin 75.0%) — **VERIFIED-PRIMARY.** Against 2026 global AI capex estimates of ~$700–900B, combined AI-lab revenue is far smaller: **Anthropic run-rate ~$9B end-2025 → crossed $30B in April 2026 → $47B in May → topped $65B by late July 2026** (Bloomberg/Reuters via Yahoo; Series H closed 2026-05-29 at a $965B post-money valuation); **OpenAI ~$25B annualized as of early 2026, up from ~$13B in 2025** (Epoch AI/PYMNTS). This yields roughly the **10:1 capex-to-revenue ratio** some commentators cite; the specific author who originated the "10:1" framing was not attributable within budget.

---

## H5. Historical circular-capital episodes (Lehman/Lucent mapping)

**Summary.** The clearest analogues to today's vendor-financed AI buildout are the 1999–2001 telecom/vendor-financing bust and Cisco's dot-com round-trip. Confirmed figures below; UK Railway Mania, Enron/Lehman rating timing, and structured-finance rating-transition detail were not retrieved within budget and are flagged as gaps.

CSV (`episode,metric,value,date_or_period,source,url,confidence`):

```
episode,metric,value,date_or_period,source,url,confidence
Telecom vendor financing,Nortel total customer financing,$2.1B,end FY2001,Globe and Mail / Nortel 10-K,https://www.theglobeandmail.com/report-on-business/nortel-clients-give-warning-of-finances/article20454748/,SECONDARY
Telecom bubble,Global telecom stock mkt-cap loss,>$2 trillion,2000-2002,thebubblebubble,https://www.thebubblebubble.com/telecom-bubble/,SECONDARY
Telecom bubble,US telecom cap loss (of $7T total decline),~$2 trillion,2000-2002,Princeton/Starr,https://www.princeton.edu/~starr/articles/articles02/Starr-TelecomImplosion-9-02.htm,SECONDARY
Global Crossing,Bankruptcy (assets/debt),assets $22.44B / debt $12.39B,2002-01-28,US House Financial Services,https://financialservices.house.gov/media/pdf/032102wm.pdf,VERIFIED-PRIMARY
Global Crossing,Goodwill write-down,$8B,2002-04,The Register,https://www.theregister.com/2002/04/12/global_crossing_takes_8bn_charge/,SECONDARY
WorldCom,Assets at bankruptcy,$103.8B,2002-07-21,CRS,https://www.everycrsreport.com/reports/RS21253.html,VERIFIED-PRIMARY
WorldCom,Market cap collapse,$150B -> <$150M,Jan2000-Jul2002,CRS,https://www.everycrsreport.com/reports/RS21253.html,VERIFIED-PRIMARY
Dark fiber,Share of US long-haul fiber lit,~10% (~1/10),2002-2004,Technostatecraft (citing Odlyzko),https://www.technostatecraft.com/p/dark-fiberan-archaeology-of-the-dot,SECONDARY
Cisco,Market cap peak,$555.4B ($80.06/sh),2000-03-27,Morningstar/Yahoo,https://www.morningstar.com/stocks/nvidia-2023-vs-cisco-1999-will-history-repeat,SECONDARY
Cisco,Trough price,$8.60,2002-10-08,Morningstar,https://www.morningstar.com/stocks/nvidia-2023-vs-cisco-1999-will-history-repeat,SECONDARY
Cisco,Years to reclaim 2000 peak,~25 yrs (record close $80.25),2000-2025 (2025-12-10),CNBC,https://www.cnbc.com/2025/12/10/ciscos-stock-closes-at-record-for-first-time-since-dot-com-peak-2000.html,VERIFIED-PRIMARY
SaaS de-rating,Snowflake peak,~$429,2021-11,Bitget,https://www.bitget.com/news/detail/12560605200515,SINGLE-SOURCE
SaaS de-rating,Zoom peak/trough,$588 -> ~$55,2020-2024,Bitget,https://www.bitget.com/news/detail/12560605200515,SINGLE-SOURCE
SaaS de-rating,Snowflake peak-to-trough,-56% (trough 2026-04-10),2021-2026,TIKR,https://www.tikr.com/blog/snowflake-stock-erased-a-56-drawdown-a-coding-agent-could-be-why,SECONDARY
```

**H8 verification fold-ins:**
- **H8-2 Facebook:** $38 offer, IPO 2012-05-18 confirmed; low ~$17.55 on 2012-09-04 (~−54% in ~15 weeks). Date it sustainably reclaimed $38 (mid-2013) not precisely pinned within budget.
- **H8-3 Rivian:** $78 offer, trading start 2021-11-10; peak $179.47 on 2021-11-16 confirmed. Subsequent 2022–2023 trough (~$11–13) not primary-confirmed within budget.
- **H8-4 Cisco:** ~$555.4B on 2000-03-27 confirmed; trough $8.60 (2002-10-08); reclaimed 2025-12-10 (~25 years). FY2000 revenue ~$18.9–19B; FY2003 comparison not primary-confirmed.
- **H8-5 Lucent/Nortel/GX/WorldCom:** Nortel $2.1B customer financing (FY2001); Global Crossing $12.39B debt (Jan 2002); WorldCom $103.8B assets (Jul 2002). Lucent's ~$3.7B FY2001 vendor-financing write-off **not primary-confirmed → corrected/partial**; US long-haul fiber lit ~10% (2002–2004).
- **H8-6 UK Railway Mania:** **not retrieved within budget → data gap.**
- **H8-7 SPAC cohort / SEC DERA report / Klausner–Ohlrogge:** **not retrieved within budget → data gap.**
- **H8-8 Enron BBB+ / Lehman A-A2 rating timing; structured-finance AAA downgrades by 2009:** **not retrieved within budget → data gap.**
- **H8-11 Snowflake/Twilio/Zoom/Peloton:** SNOW ~$429 → ~$110; ZM $588 → ~$55–60; PTON peak $171.09 (Jan 2021) → ~$4; TWLO ~$440 → ~$45 — magnitudes consistent with sources; exact troughs partially confirmed.
- **H8-12 Quotes:** Chuck Prince — "When the music stops, in terms of liquidity, things will be complicated. But as long as the music is playing, you've got to get up and dance. We're still dancing." — Financial Times interview, July 2007 (widely dated 2007-07-09/10). Interviewer **Francesco Guerrera not independently confirmed within budget → partial.** Greenspan "irrational exuberance" — AEI speech, **1996-12-05** (confirmed, primary quote text). Dario Amodei — "If my revenue is not $1 trillion dollars, if it's even $800 billion, there's no force on earth, there's no hedge on earth that could stop me from going bankrupt if I buy that much compute" — on the **Dwarkesh Patel podcast**, in the context of buying "$1 trillion of compute that starts at the end of 2027" (confirmed via Dwarkesh transcript).
- **H8-13 Perez/Kindleberger/Minsky:** **not retrieved within budget → data gap.**

---

## H6. Default-rate tables

**Summary.** S&P Table 26 (2024 study, published 2025-03-27) 5-year figures are **all confirmed verbatim against the primary source**, with the 10-year column added. Moody's full alphanumeric (Aa1…Caa3) detail sits behind the CreditView/Annual-Default-Study paywall; the broad-category 1983–2024 issuer-weighted figures are provided from Moody's own document server. Moody's idealized EL/PD tables and the Moody's/KMV EDF-to-rating map were not publicly retrievable → `unavailable`.

CSV (`agency,table,notch,y5,y10,url,date,confidence`):

```
agency,table,notch,y5,y10,url,date,confidence
S&P,Table 26,AAA,0.34,0.67,https://www.spglobal.com/ratings/en/research/articles/250327-default-transition-and-recovery-2024-annual-global-corporate-default-and-rating-transition-study-13452126,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,AA+,0.13,0.37,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,AA,0.33,0.83,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,AA-,0.27,0.59,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,A+,0.35,0.83,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,A,0.39,1.13,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,A-,0.42,1.07,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,BBB+,0.79,1.83,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,BBB,1.09,2.50,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,BBB-,2.40,4.50,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,BB+,2.90,5.51,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,BB,5.05,9.33,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,BB-,8.28,14.67,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,B+,12.88,19.62,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,B,14.69,21.04,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,B-,22.03,27.90,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,Table 26,CCC/C,46.53,50.43,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,summary,Investment grade,0.77,1.69,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,summary,Speculative grade,13.64,19.15,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
S&P,summary,All rated,6.00,8.67,https://maalot.co.il/Publications/FTS20250331162126.pdf,2025-03-27,VERIFIED-PRIMARY
Moody's,broad 1983-2024,Aaa,0.06,0.12,https://ratings.moodys.com/api/rmc-documents/427804,2025,SECONDARY
Moody's,broad 1983-2024,Aa,0.28,0.68,https://ratings.moodys.com/api/rmc-documents/427804,2025,SECONDARY
Moody's,broad 1983-2024,A,0.70,1.88,https://ratings.moodys.com/api/rmc-documents/427804,2025,SECONDARY
Moody's,broad 1983-2024,Baa,1.40,3.27,https://ratings.moodys.com/api/rmc-documents/427804,2025,SECONDARY
Moody's,broad 1983-2024,Ba,7.85,15.21,https://ratings.moodys.com/api/rmc-documents/427804,2025,SECONDARY
Moody's,broad 1983-2024,B,20.02,33.87,https://ratings.moodys.com/api/rmc-documents/427804,2025,SECONDARY
Moody's,broad 1983-2024,Caa-C,32.69,47.86,https://ratings.moodys.com/api/rmc-documents/427804,2025,SECONDARY
Moody's,idealized EL/PD,alphanumeric,unavailable,unavailable,unavailable (paywalled),n/a,ESTIMATE
Moody's/KMV,EDF-to-rating map,n/a,unavailable,unavailable,unavailable (not publicly published),n/a,ESTIMATE
```

*Note (S&P):* every one of the 17 candidate 5-year values in the prompt matched Table 26 exactly (AAA 0.34 through CCC/C 46.53); the 10-year column is newly added from the same table. S&P summary 5-yr: investment grade 0.77%, speculative grade 13.64%, all-rated 6.00%.

---

## FINAL: Consolidated verification table

CSV (`item,claim,verified_value,source,url,date,status`):

```
item,claim,verified_value,source,url,date,status
H8-1,IPO 5yr underperformance ~34% vs 62% matched,"IPO issuers ~5%/yr; 44% more capital needed vs nonissuers; '34/62' not verbatim",Loughran & Ritter 1995,https://onlinelibrary.wiley.com/doi/full/10.1111/j.1540-6261.1995.tb05166.x,1995,corrected
H8-2,FB $38 offer 2012-05-18; low $17.55 2012-09-04,Confirmed offer $38 & date; low ~$17.55 (~-54%),iTiger/CNBC,https://www.cnbc.com/2025/06/08/circle-ipo-debut-outperforms-meta-airbnb-and-robinhood.html,2012,confirmed
H8-3,Rivian $78 offer; peak $179.47 2021-11-16,Confirmed offer $78 & peak date; trough not primary-confirmed,CNBC,https://www.cnbc.com/2021/11/09/rivian-prices-ipo-at-78-a-share-valuing-electric-vehicle-company-at-66point5-billion.html,2021,confirmed
H8-4,Cisco $555B 2000-03-27; trough 2002; reclaim year,Peak $555.4B; trough $8.60 2002-10-08; reclaimed 2025-12-10,Morningstar/CNBC,https://www.cnbc.com/2025/12/10/ciscos-stock-closes-at-record-for-first-time-since-dot-com-peak-2000.html,2025,confirmed
H8-5,Lucent $3.7B write-off; GX $12B; WorldCom $104B,GX $12.39B debt & WorldCom $103.8B assets confirmed; Lucent $3.7B unconfirmed,House FS/CRS,https://financialservices.house.gov/media/pdf/032102wm.pdf,2002,corrected
H8-6,Railway Mania capex % GDP; miles authorized vs built,Not retrieved,search attempted (Odlyzko/Campbell-Turner),unavailable,n/a,unavailable
H8-7,SPAC 2020-21 median de-SPAC return; SEC DERA report; Klausner-Ohlrogge,Not retrieved in budget,search attempted,unavailable,n/a,unavailable
H8-8,Enron BBB+ to 2001-11-28 Ch11 2001-12-02; Lehman A/A2 to 2008-09-15,Not primary-confirmed in budget,search attempted,unavailable,n/a,unavailable
H8-9,MSFT-OpenAI $13B; Nvidia-OpenAI $100B; Oracle $300B; AMD warrant,"Nvidia $100B & Ohio $105B VERIFIED; Oracle $300B & AMD 160M-share warrant SECONDARY; MSFT $13B single-source",OpenAI/Nvidia/CNBC,https://openai.com/index/openai-nvidia-systems-partnership/,2025-2026,confirmed
H8-10,Nvidia FY2025 rev $130.5B; AI capex $700-900B vs lab rev ~10:1,"Nvidia FY2025 rev $130.5B (+114%) VERIFIED-PRIMARY; ratio ~10:1 plausible",NVIDIA Newsroom / Fortune,https://fortune.com/2026/08/18/openai-data-center-deal-with-nvidia-comes-in-145-billion-lower-than-reportedsignaling-concerns-of-artificial-demand-for-chips/,2025-2026,confirmed
H8-11,SNOW/TWLO/ZM/PTON peaks & troughs,SNOW $429; ZM $588; PTON $171.09 peak; magnitudes confirmed,Bitget/Fool/TheStreet,https://www.bitget.com/news/detail/12560605200515,2021-2026,confirmed
H8-12,Prince/Greenspan/Amodei quotes,"Prince FT Jul2007 (interviewer unconfirmed); Greenspan AEI 1996-12-05; Amodei Dwarkesh confirmed",Dwarkesh/Wikipedia/CNBC,https://www.dwarkesh.com/p/dario-amodei-2,1996-2026,confirmed
H8-13,Perez/Kindleberger/Minsky Levy WP number,Not retrieved,search attempted,unavailable,n/a,unavailable
```

---

## Recommendations (for the Monte-Carlo build)

1. **Anchor the base-rate prior on Ritter, not on recent winners.** Seed the model's central tendency with IPO long-run underperformance (issuers ~5%/yr over 5 years; 44% wealth shortfall vs matched firms) and Ritter's hot-market flag for 2025 (29.3% average first-day return; $13.11bn left on the table). A ~$2T Anthropic listing into a hot market should carry a materially negative long-run drift prior. **Threshold that would change this:** if the IPO prices *below* range or the year's average first-day return normalizes toward the 19.0% long-run mean, relax the negative drift.

2. **Model the drawdown as bimodal, calibrated to the H1 archetypes.** Use two regimes: a "quality-resilient" path (Airbnb/Snowflake-like, drawdowns ~30–60% from peak, eventual recovery) and a "euphoria-unwind" path (Rivian ~−91%, Robinhood ~−84% within six months, Coinbase ~−50%+). Weight the euphoria-unwind regime higher the larger the private-to-IPO step-up and the hotter the concurrent IPO supply. **Benchmark to watch:** lockup expiry (~180 days) is the single most reliable near-term drawdown catalyst — build an explicit lockup-expiry price shock.

3. **Treat the circular-capital structure as a correlated-risk amplifier, not a demand signal.** Anthropic's revenue quality is entangled with the same hyperscalers (Amazon, Google, Microsoft) that fund it and sell it compute; the reciprocal >$100B AWS / $30B Azure / tens-of-billions Google TPU commitments mean a demand shock hits revenue, funding, *and* cost simultaneously. Map the H5 telecom-vendor-financing analogue directly onto this: the ~10:1 AI-capex-to-lab-revenue gap is the modern echo of dark fiber (~10% lit by 2002). **Threshold:** if AI-lab aggregate revenue growth decelerates below ~2x/yr while capex stays on the $700–900B trajectory, escalate the tail-risk weighting — this is precisely the "off by a year → bankruptcy" scenario Amodei himself described.

4. **Use the default tables (H6) for the debt-financed downside leg.** For scenarios where Anthropic or its neocloud/compute counterparties carry material leverage, apply S&P's 5-/10-year cumulative default curves (e.g., BB 5.05%/9.33%, B 14.69%/21.04%, CCC/C 46.53%/50.43%) as the credit-migration engine. Neoclouds funded with GPU-collateralized debt should be modeled toward the speculative end.

5. **Close the data gaps before publication (staged).** Priority-1 pulls: (a) per-name daily price series to fill lockup-expiry and 6/12-month drawdown cells in H1 (Yahoo/Bloomberg); (b) SpaceX daily close series 2026-06-12→2026-08-21; (c) hyperscaler quarterly capex and debt-funded share from 10-Q/10-K (H7-3); (d) CoreWeave debt tranche detail from the S-1/10-Q (H7-2); (e) Meta Hyperion SPV terms (H7-4) and the Alphabet June-2026 raise instrument (H7-5). Priority-2: Renaissance IPO-index returns, Field & Hanka lockup magnitudes, SPAC/DERA/Klausner-Ohlrogge, and the Enron/Lehman rating-timeline and structured-finance downgrade shares (H8-6/7/8/13).

## Caveats
- **Budget-limited sourcing.** The web-search budget was exhausted before several quantitative sub-requests could be filled; every unfilled item is explicitly marked `unavailable` / DATA GAP with the search basis, per the global rules, rather than estimated or padded.
- **Forward-looking and promotional content flagged.** SpaceX price targets ($75–$450), "world's first trillionaire" framing, and analyst "Buy" tallies are speculation/marketing, not facts, and are excluded from the data rows. The ~$2T Anthropic valuation and October-2026 timing are prospective, per the task framing.
- **Secondary vs primary.** Several circular-capital amounts (Oracle $300B, AMD warrant, Microsoft $13B) rest on WSJ/press reporting rather than filings and are flagged SECONDARY/SINGLE-SOURCE; the Nvidia→OpenAI $100B, the $105B Ohio backstop, the Amazon→Anthropic terms, and Nvidia's FY2025 $130.5B revenue are VERIFIED-PRIMARY.
- **Moody's granularity.** The requested alphanumeric (Aa1…Caa3) 5-/10-year Moody's table is paywalled; only the broad-letter 1983–2024 issuer-weighted figures are provided, clearly labeled.
- **No averaging.** Where sources conflict (e.g., SpaceX valuation ~$1.77T vs ~$2.1T at Day-1 close; CoreWeave peak ~$187), both figures are preserved rather than blended.
- **Not investment advice.** This is analytical research feeding a published, disclosed-methodology rating of an upcoming IPO.

## Sources
- https://site.warrington.ufl.edu/ritter/files/IPO-Statistics.pdf
- https://theideafarm.com/alternative-investment/venture-capital-startups/ipo-data/
- https://onlinelibrary.wiley.com/doi/full/10.1111/j.1540-6261.1995.tb05166.x
- https://www.sciencedirect.com/science/article/abs/pii/0304405X9390006W
- https://www.nber.org/system/files/working_papers/w8505/w8505.pdf
- https://www.aboutamazon.com/news/company-news/amazon-invests-additional-5-billion-anthropic-ai
- https://www.anthropic.com/news/anthropic-amazon-compute
- https://www.cnbc.com/2026/04/20/amazon-invest-up-to-25-billion-in-anthropic-part-of-ai-infrastructure.html
- https://openai.com/index/openai-nvidia-systems-partnership/
- https://nvidianews.nvidia.com/news/openai-and-nvidia-announce-strategic-partnership-to-deploy-10gw-of-nvidia-systems
- https://www.cnbc.com/2026/08/17/nvidia-financing-open-ai-data-center-ohio.html
- https://fortune.com/2026/08/18/openai-data-center-deal-with-nvidia-comes-in-145-billion-lower-than-reportedsignaling-concerns-of-artificial-demand-for-chips/
- https://www.bloomberg.com/news/articles/2026-08-17/nvidia-to-invest-up-to-105-billion-for-openai-data-center-in-ohio
- https://siliconangle.com/2025/09/10/openai-oracle-strike-300b-cloud-computing-deal-power-ai/
- https://tomtunguz.com/openai-hardware-spending-2025-2035/
- https://www.fierce-network.com/cloud/fierce-networks-encyclopedia-ai-deals
- https://www.forbes.com/sites/phoebeliu/2025/10/09/-billionaires-oracle-openai-amd-nvidia-450-billion-richer-ai-infrastructure-deals/
- https://www.cnbc.com/2025/06/04/stablecoin-issuer-circle-prices-ipo-at-31-above-expected-range-ahead-of-nyse-debut.html
- https://accessipos.com/circle-stock-ipo/
- https://www.cnbc.com/2025/07/31/figma-fig-starts-trading-on-nyse-after-ipo.html
- https://www.saastr.com/figmarankipos
- https://www.cnbc.com/2025/09/10/klarna-klar-stock-soars-after-us-ipo.html
- https://finance.yahoo.com/news/klarna-prices-ipo-40-per-013356764.html
- https://www.cnbc.com/2025/03/28/coreweave-starts-trading-on-nasdaq-at-per-share.html
- https://news.crunchbase.com/ai/coreweave-ipo-crwv-opening-day-trade/
- https://capital.com/en-eu/learn/ipo/coreweave-ipo
- https://www.cnbc.com/2024/03/21/reddit-ipo-rddt-starts-trading-on-nyse.html
- https://www.cnbc.com/2024/03/20/reddit-prices-ipo-at-34-per-share-sources-say.html
- https://www.cnbc.com/2021/11/09/rivian-prices-ipo-at-78-a-share-valuing-electric-vehicle-company-at-66point5-billion.html
- https://www.forbes.com/sites/tylerroush/2026/06/12/spacex-opens-at-150-surging-17-after-largest-ipo-ever-live-updates/
- https://financer.com/invest/spacex-ipo/
- https://www.investing.com/equities/spacex
- https://smartasset.com/investing/spacex
- https://finance.yahoo.com/news/spacex-weighs-june-2026-ipo-050656741.html
- https://www.cnbc.com/2025/06/08/circle-ipo-debut-outperforms-meta-airbnb-and-robinhood.html
- https://www.morningstar.com/stocks/nvidia-2023-vs-cisco-1999-will-history-repeat
- https://www.cnbc.com/2025/12/10/ciscos-stock-closes-at-record-for-first-time-since-dot-com-peak-2000.html
- https://www.theglobeandmail.com/report-on-business/nortel-clients-give-warning-of-finances/article20454748/
- https://financialservices.house.gov/media/pdf/032102wm.pdf
- https://www.everycrsreport.com/reports/RS21253.html
- https://www.theregister.com/2002/04/12/global_crossing_takes_8bn_charge/
- https://www.technostatecraft.com/p/dark-fiberan-archaeology-of-the-dot
- https://www.princeton.edu/~starr/articles/articles02/Starr-TelecomImplosion-9-02.htm
- https://www.thebubblebubble.com/telecom-bubble/
- https://www.dwarkesh.com/p/dario-amodei-2
- https://www.datacenterdynamics.com/en/news/anthropic-ceo-the-way-you-buy-these-data-centers-if-youre-off-by-a-couple-years-can-be-ruinous/
- https://en.wikipedia.org/wiki/Irrational_exuberance
- https://www.cnbc.com/2017/07/07/ray-dalios-keep-dancing-advice-may-raise-some-bad-memories.html
- https://fortune.com/2026/06/04/jamie-dimon-gung-ho-exuberance-bubble-risk-like-2000-2007-1986-1972/
- https://www.bitget.com/news/detail/12560605200515
- https://www.tikr.com/blog/snowflake-stock-erased-a-56-drawdown-a-coding-agent-could-be-why
- https://www.thestreet.com/retirement-daily/saving-investing-for-retirement/pandemic-growth-stories-investing-lessons-from-zoom-twilio-and-peloton
- https://www.spglobal.com/ratings/en/research/articles/250327-default-transition-and-recovery-2024-annual-global-corporate-default-and-rating-transition-study-13452126
- https://maalot.co.il/Publications/FTS20250331162126.pdf
- https://ratings.moodys.com/api/rmc-documents/427804
