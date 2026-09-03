# H follow-up: EDGAR primary pulls (2026-08-21)

Four pulls against SEC EDGAR (submissions JSON, companyfacts XBRL, filing documents). Every CSV row carries URL, as-of date and a confidence flag. Secondary/press sources are used only where no filing exists (private companies, earnings-call guidance) and are flagged as such. Web-search budget was exhausted late in the session; a few press items are therefore SINGLE-SOURCE.

Outputs:
- `data/research/H/H7_2_coreweave_debt.csv` (43 rows: CoreWeave 25, Nebius 9, Lambda 4, Crusoe 5)
- `data/research/H/H7_3_hyperscaler_capex_debt.csv` (74 quarterly rows, FY2022–Q2 2026)
- `data/research/H/H7_5_alphabet_raise.csv` (7 rows)
- `data/research/H/H8_5_lucent_nortel_vendor_financing.csv` (31 rows)

---

## 1. CoreWeave / Nebius / Lambda / Crusoe debt by tranche

**CoreWeave (CIK 1769628).** Source of record is the Q2-2026 10-Q (filed 2026-08-12, Note 10 "Debt"), cross-checked to the FY2025 10-K (filed 2026-03-02), the 424B4 IPO prospectus (2025-03-31) for lender names, and six 2026 8-Ks (DDTL 4.0 Mar 30; 9.75% notes + $4B convert Apr 9/14; DDTL 5.0 May 15; 9.625% USD + 8.50% EUR notes Jun 18; DDTL 5.5 Aug 7).

As of 2026-06-30, as printed (USD millions): total principal **$35,551** (vs $21,615 at 2025-12-31 and $8,033 at 2024-12-31). Recourse debt net $31,405; non-recourse net $3,663. Maturity ladder: remainder-2026 $4,413; 2027 $6,184; 2028 $4,416; 2029 $2,421; 2030 $3,221; thereafter $14,896. Contractual interest Q2-26 $592M (net of capitalised interest $558M).

Tranches outstanding (principal, maturity, effective rate as printed): DDTL 1.0 $1,300 / Mar-2028 / 15% (Blackstone Tactical Opportunities + Magnetar, cap $2.3B); DDTL 2.0 $3,190 / Aug-2030 / 11% (Blackstone Alternative Credit et al., cap $7.6B, includes IG tranches); DDTL 2.1 $3,000 / Mar-2031 / 9%; DDTL 3.0 $2,215 / Aug-2030 / 9% (cap $2.6B); DDTL 5.0 $1,101 / Nov-2031 / SOFR+4.50%, eff 9% (cap $3.1B; Morgan Stanley/MUFG; Ba2/BB+; first publicly syndicated GPU-backed DDTL); **DDTL 4.0 (non-recourse) $2,837 / Mar-2032 / SOFR+2.25% floating, Treasury+2.00% (~5.9%) fixed, eff 7%** (cap $8.5B; MUFG agent; **A3 Moody's / A(low) DBRS — first investment-grade GPU-backed facility**; secured by $3.3B of CCAC VIII assets); 2030 Senior Notes 9.25% $2,000; 2031 9.00% $1,750; 2031 9.75% $2,750 (Apr-26); 2032 9.625% $1,250 (Jun-26); 2032 EUR 8.50% EUR2.0B = $2,279 (Jun-26); 2031 convert 1.75% $2,588 (conv $107.80); 2032 convert 1.75% $4,000 (conv $119.60, capped call to $230); revolver $2.5B capacity, $0 drawn ($533M LCs); OEM/software vendor financing $4,220 recourse + $882 non-recourse (10–11% eff., maturities to Jul-2030); Magnetar loan $189. DDTL 5.5 ($2.6B, JPMorgan agent, Ba2/BB+, ~5-yr vs ~3-yr customer contracts) closed 2026-08-07, after quarter end. All DDTLs are GPU-collateralised: borrowing capacity is "constrained by the purchase price of assets ... based upon the depreciable cost of GPU servers", secured by sub equity + substantially all sub assets; SPV subs held $18.2B non-current + $2.6B current assets pledged at 6/30/26.

Bond pricing in filings: fair value of the five senior-note series $10.0B vs ~$10.03B principal (≈ par); converts $7.5B FV vs $6.588B principal. Ratings are **not** in the 10-Q/10-K; DDTL ratings come from 8-K Ex.99.1 press releases (PRIMARY); issuer ratings (S&P B+, Moody's Ba3 CFR; unsecured notes S&P B) are SECONDARY (spglobal/cbonds search snippets).

**Nebius (CIK 1513845, 20-F filer).** Source: 6-K of 2026-08-12 Ex.99.2 (Q2-26 financial statements, Note 12), 20-F FY2025 (2026-04-30), 6-Ks of 2026-03-20, 2026-07-17, 2026-08-20. All debt is unsecured convertible notes until July 2026: six series, accreted principal **$10,041.8M, carrying $8,499.0M** at 2026-06-30 (2.00% Jun-2029 $587.5; 3.00% Jun-2031 $612.5; 1.00% Sep-2030 $1,818.4; 2.75% Sep-2032 $1,818.4; 1.25% Mar-2031 $3,105.0; 2.625% Mar-2033 $2,100.0; all accrete 115–120% to maturity; effective rates 4.15–7.06%). Cash $8,042.1M. Post-period: ~$775M senior secured term loan (MUFG; Term SOFR+2.50%; Oct-2030; asset-backed, non-recourse to parent) signed 2026-07-10; $5.0B converts priced 2026-08-19 ($3.0B 0.50% 2030 + $2.0B 4.50% 2034, +$750M greenshoe) with $800M exchange of 2029/2031 notes into ~15.8M shares.

**Lambda / Crusoe (private).** Press only. Lambda: $500M GPU-backed (Macquarie + IDF, Apr-2024, BusinessWire); $275M JPM-led facility (Aug-2025); upsized to $1B (May-7-2026, lambda.ai PR); ~$917–926M term loan B reported Aug-10-2026 as first IG-rated neocloud TLB (Bloomberg/DCD — pages 403; SINGLE-SOURCE). Crusoe: Abilene/Stargate JV $11.6B debt+equity (May-2025; Crunchbase), of which $9.6B JPMorgan debt (Sacra; SECONDARY); $7.1B JPM-led Phase-2 construction loan via Newmark (Sacra; SINGLE-SOURCE); $750M Brookfield secured facility (Jun-2025; crusoe.ai PR + Norton Rose); $225M Upper90; $175M Victory Park (Sacra). Crusoe project debt sits at JV level, not at Crusoe corporate — do not add to a "neocloud corporate debt" total without that caveat.

---

## 2. Hyperscaler capex and debt issuance, FY2022–Q2 2026

Method: EDGAR companyfacts XBRL (tags as printed in each company's cash-flow statement), quarterly values taken directly where a 3-month duration is tagged, otherwise YTD-minus-prior-YTD (Q4 = FY minus 9M); Alphabet FY2023 Q4 revenue = FY minus Q1–Q3 because of a tag change. Tags: capex = `PaymentsToAcquirePropertyPlantAndEquipment` (Alphabet, Microsoft, Meta) / `PaymentsToAcquireProductiveAssets` (Amazon); revenue = `Revenues` (Alphabet) / `RevenueFromContractWithCustomerExcludingAssessedTax` (others); debt = Alphabet `ProceedsFromDebtNetOfIssuanceCosts` (CP + term debt, gross), Amazon `ProceedsFromIssuanceOfLongTermDebt` + `ProceedsFromShortTermDebt` (gross), Meta `ProceedsFromIssuanceOfLongTermDebt`, Microsoft `ProceedsFromDebtMaturingInMoreThanThreeMonths` + net short-term debt. Microsoft fiscal year ends June (FY2026 Q4 = Jun-2026). Companies omit zero-valued tags in some 10-Qs; those are recorded as 0 and labelled. Microsoft capex is "additions to property and equipment" excluding finance leases, as tagged.

Headline capex (as printed, $B): Alphabet 2025 = 17.2 / 22.4 / 24.0 / 27.9 (FY 91.4); Q1-26 35.7, **Q2-26 44.9**. Microsoft FY2026 (Jul-25–Jun-26) = 19.4 / 29.9 / 30.9 / **35.8** (FY 115.9). Amazon 2025 = 25.0 / 32.2 / 35.1 / 39.5 (FY 131.8); Q1-26 44.2, **Q2-26 54.2**. Meta 2025 = 12.9 / 16.5 / 18.8 / 21.4 (FY 69.7); Q1-26 19.0, **Q2-26 30.1**. Capex/revenue Q2-26: Alphabet 37.5%, Microsoft 39.8%, Amazon 27.0%, Meta 49.5%.

Notable issuance, from 8-Ks (all VERIFIED-PRIMARY): Alphabet May-2025 $5B + EUR6.75B; Nov-6-2025 $17.5B + EUR6.5B; Feb-13-2026 $20B + GBP5.5B; May-11-2026 EUR9B + C$9.5B; May-21-2026 JPY576.9B; Aug-10-2026 $25B. Meta Aug-2024 $10.5B; Nov-3-2025 $30B; May-4-2026 $25B. Amazon Apr-2022 $12.75B; Dec-2022 $8.25B; Nov-20-2025 $15B; Mar-13-2026 $37B USD (11 tranches) + Mar-16-2026 EUR14.5B; Jun-8-2026 $17.5B senior unsecured delayed-draw term loan (Citibank agent); Jun-12-2026 C$14B; Jul-9-2026 $25B. Microsoft: no 8-K-reported note offerings 2022–2026.

Debt-funded share of capex (gross debt proceeds as tagged / capex, by fiscal year — note Alphabet and Amazon figures include commercial-paper roll so FY2022 ratios overstate term funding):

| Company | FY2022 | FY2023 | FY2024 | FY2025 | FY2026 YTD |
|---|---|---|---|---|---|
| Alphabet | 168% (CP-heavy) | 33% | 26% | 71% | 70% (H1) |
| Amazon | 99% (CP-heavy) | 34% | 6% | 19% | 84% (H1) |
| Meta | 32% | 31% | 28% | 43% | 51% (H1) |
| Microsoft (Jun FY) | 0% | 0% | 67% (Activision-period ST debt) | −9% (net CP repayment) | 0% |

Capex guidance (SECONDARY, from Q2-26 call coverage: futurex.capital, uncoveralpha.com; conflicting figures noted): Alphabet 2026 raised to $195–205B (from $180–190B; the $180–190B and "2027 to significantly increase" are PRIMARY in Alphabet's 2026-06-01 press release); Microsoft ~$175B CY2026 restated for lease reclassification (aiweekly earlier: ~$190B) and ">$50B" for the Sep-26 quarter; Meta $135–145B (futurex) / $130–145B (uncoveralpha); Amazon ~$220B (from ~$200B). No company-stated numeric 2027 guidance found beyond Alphabet's "significantly increase" and Amazon's "lion's share of 2027 capacity already reserved".

---

## 3. Alphabet June-2026 ~$85B equity raise — CONFIRMED

The reviewer's claim is correct. Filings: S-3ASR (333-296395, 2026-06-01); 424B5s (2026-06-02/04); 8-K 2026-06-04 (Items 1.01/7.01/8.01; Ex.99.1 press release 2026-06-01 "Proposed $80 Billion Equity Capital Raise", Ex.99.2 press release 2026-06-02 "Upsize and Pricing of $84.75 Billion Equity Capital Raise"); 8-K 2026-06-05 (Items 1.01/3.03/5.03; certificates of designations, deposit agreements, capped calls); 8-A12B for GOOGM/GOOGN.

Components: (i) underwritten common: 25,459,689 Class A @ $355.1982 + 25,459,689 Class C @ $351.8018 = ~$18.0B, greenshoe 3,818,953 each exercised in full (≈+$2.7B), closed 2026-06-04; (ii) 6.25% Series A/B Mandatory Convertible Preferred via depositary shares ($50 = 1/20 of $1,000), 167.5M + 167.5M = $16.75B, greenshoe 25M each exercised (+$2.5B), mandatory conversion ~May-15-2029 (2.2520–2.8160 A shares per $1,000), capped calls to $532.67/$527.80, closed 2026-06-05; (iii) $10B Berkshire Hathaway private placement (14,212,035 A @ ~$351.81 + 14,359,656 C @ ~$348.20); (iv) $40B ATM program (GS/JPM/MS), to begin Q3-26, ~$30B earmarked for 2026 employee-equity tax obligations. Stated total $84.75B (base); ≈$89.95B including greenshoes. Use of proceeds: general corporate purposes including capex to scale AI infrastructure and global compute; capped-call cost. Underwriters/reps: Goldman Sachs, J.P. Morgan, Morgan Stanley. The press release also states >$85B of debt raised in the prior 12 months and total debt >$100B.

---

## 4. Lucent FY2001 / Nortel FY2001 customer financing

**Lucent 10-K405 FY2001 (filed 2001-12-28).** Customer financing commitments at 2001-09-30: total $5.3B (loans $4.6B, guarantees $0.7B); drawn $3.0B; available-not-drawn $1.4B; not available $0.9B. At 2000-09-30: total $8.1B (loans $6.7B, guarantees $1.4B); drawn $2.0B; available $3.9B; not available $2.2B. Provision for uncollectibles and customer financings: **FY2001 $2,249M; FY2000 $505M; FY1999 $66M**; ~$1.3B of FY2001 related to three projects incl. Winstar and One.Tel; reserves on drawn commitments $2.1B, net exposure ~$900M. Schedule II customer-financing reserves FY2001: $604 → +$1,787 charged, +$257 other, −$539 written off → $2,109; FY2000: $34 → +$260, +$432, −$122 → $604. FY2000 10-K (filed 2000-12-27) MD&A: loan commitments ~$6.7B (~$3.3B undrawn/available, ~$1.3B advanced), guarantees ~$1.4B (~$600M undrawn, ~$770M outstanding); $970M limited-recourse securitisation trust.

**Nortel Networks Limited 10-K405 FY2001 (filed 2002-03-11; CIK 1119664).** Drawn and outstanding customer financing, net of provisions: $464M at 2001-12-31 (provisions $887M) vs $1,081M at 2000-12-31 (provisions $433M); undrawn commitments $1,611M vs $4,087M; total $2,075M vs $5,168M. Long-term receivables $203M less provisions of $828M (2000: $1,116M less $383M). Schedule II provision for uncollectibles FY2001: $746 → +$1,498 → −$761 → $1,483 (FY2000: $581 → +$253 → −$88 → $746). Discontinued access-solutions disposal loss included $600M receivable provisions. Nortel does not break out a single "customer financing provision" P&L line; the $887M/$433M netting and Schedule II are the closest printed figures.

---

## Gaps / caveats
- CoreWeave lender lists for DDTL 2.1/3.0 and the revolver are not named in the 10-Q/10-K; DDTL 1.0/2.0 lenders come from the 424B4. Issuer credit ratings are SECONDARY.
- Lambda TLB ($917–926M) and Crusoe $9.6B/$7.1B JPM figures are from blocked or single secondary pages.
- Capex guidance is SECONDARY and sources disagree on Microsoft ($175B vs $190B) and Meta ($130 vs $135B lower bound).
- Hyperscaler "debt issued" is gross proceeds as tagged (includes CP for Alphabet/Amazon); for a term-funding view use the notable-issuance column.
