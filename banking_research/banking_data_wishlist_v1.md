# Banking Data Expansion Wishlist

## Overview

This wishlist documents planned data sources for the Banking Master Dataset and Economic Data Platform banking modules. Items are prioritized by value and implementation effort. All items have been verified as NOT already collected in existing modules.

**Version**: 1.0
**Created**: January 2026
**Total Items**: 26
**Status**: Active

---

## Summary by Priority

| Priority | Items | Description | Est. Total Effort |
|----------|-------|-------------|-------------------|
| P1 | 5 | High value, easy to implement | 20-40 hours |
| P2 | 5 | High value, moderate effort | 40-80 hours |
| P3 | 6 | International expansion | 60-120 hours |
| P4 | 6 | Specialized/niche data | 30-60 hours |
| P5 | 4 | Aspirational (commercial) | N/A (commercial) |

---

## Priority 1: High Value, Easy to Implement

These items have APIs or bulk downloads, free access, and significant analytical value.

### 1. FDIC Problem Bank List Indicators

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | FDIC |
| **URL** | https://www.fdic.gov/resources/resolutions/bank-failures/failed-bank-list/ |
| **API Available** | Partial (BankFind API has some indicators) |
| **Estimated Effort** | 4-6 hours |
| **Data Format** | CSV, JSON |

**Description**: While we have the failure history, we don't have the leading indicators that identify banks approaching problem status. The FDIC's CAMELS-based indicators and problem bank count can be derived from Call Report data we already have, or extracted from FDIC publications.

**Value Proposition**:
- Enhance early warning system with FDIC's own problem indicators
- Track problem bank count over time (currently ~40-50 banks)
- Compare our composite risk score with FDIC classification

**Implementation Notes**:
- May need to derive from existing Call Report data (FFIEC)
- Check if FDIC publishes aggregate problem bank statistics
- Could enhance `13_early_warning_indicators.csv`

---

### 2. Fed CCAR/DFAST Scenario Parameters API

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Reserve Board |
| **URL** | https://www.federalreserve.gov/supervisionreg/stress-tests-capital-planning.htm |
| **API Available** | No (PDF extraction required) |
| **Estimated Effort** | 6-8 hours |
| **Data Format** | PDF → CSV |

**Description**: Automated extraction of scenario parameters from Fed publications. Currently we have `05_scenario_parameters.csv` with 15 years of data, but updates require manual extraction.

**Value Proposition**:
- Automate annual scenario updates
- Track scenario variable changes over time
- Enable scenario-based analysis automation

**Implementation Notes**:
- Fed publishes scenarios in February each year
- Use HDARP for PDF table extraction
- Create Python script to normalize extracted parameters

---

### 3. OECD Banking Statistics (Expanded)

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | OECD.Stat |
| **URL** | https://stats.oecd.org/ |
| **API Available** | Yes (SDMX REST API) |
| **Estimated Effort** | 4-6 hours |
| **Data Format** | JSON, CSV |

**Description**: We have partial OECD data in `DATA/OECD/` but not the specific banking statistics tables (bank profitability, income statements, balance sheets by country).

**Value Proposition**:
- Cross-country banking sector comparison (38 OECD countries)
- Standardized metrics for international benchmarking
- Time series data back to 1990s

**Key Datasets**:
- Bank Profitability Statistics (BPF)
- Structural Business Statistics (SBS) - Finance sector
- Financial Accounts (SNA)

**Implementation Notes**:
- Existing `collect_oecd_data.py` can be extended
- SDMX API requires dataset IDs
- Focus on: BPF_BNK_PROFIT, STES_BNK_ASSET

---

### 4. World Bank Global Financial Development Database (GFDD)

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | World Bank |
| **URL** | https://www.worldbank.org/en/publication/gfdr/data/global-financial-development-database |
| **API Available** | Yes (World Bank API) |
| **Estimated Effort** | 4-6 hours |
| **Data Format** | CSV, Excel |

**Description**: Comprehensive database covering financial system characteristics for 200+ countries. Includes bank concentration, credit-to-GDP, NPL ratios, and more.

**Value Proposition**:
- 200+ countries coverage (vs our 25)
- 100+ financial development indicators
- Time series from 1960s to present
- Perfect complement to IMF FSI data

**Key Indicators**:
- Bank concentration (5-bank asset share)
- Bank credit to private sector (% GDP)
- Bank NPL to gross loans
- Bank regulatory capital ratio
- Bank Z-score (distance to default)

**Implementation Notes**:
- World Bank API is well-documented
- Existing `collect_wdi_data.py` can be extended
- Filter for banking-specific indicators

---

### 5. OpenFIGI/Bloomberg Open Symbology (BSYM)

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Bloomberg (free tier) |
| **URL** | https://www.openfigi.com/api |
| **API Available** | Yes (free, rate-limited) |
| **Estimated Effort** | 3-4 hours |
| **Data Format** | JSON |

**Description**: Free identifier mapping service linking tickers, CUSIPs, ISINs, and LEIs for financial instruments including bank stocks and bonds.

**Value Proposition**:
- Cross-reference our bank tickers with global identifiers
- Map to LEI (Legal Entity Identifier) for regulatory data
- Enable joining across SEC, EBA, ECB datasets

**Implementation Notes**:
- 25 lookups per request, 100 requests per minute (free tier)
- Create lookup for our 58 bank tickers
- Store mapping in `API_MODULES/MARKET_DATA/DATA/`

---

## Priority 2: High Value, Moderate Effort

These items require registration, data wrangling, or multiple API calls.

### 6. FDIC ResearchConnect Academic Datasets

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | FDIC |
| **URL** | https://www.fdic.gov/resources/data-tools/research/ |
| **API Available** | No (bulk download with registration) |
| **Estimated Effort** | 8-12 hours |
| **Data Format** | SAS, CSV |

**Description**: FDIC provides academic researchers access to more granular historical data than the public API, including branch-level data and historical Call Reports.

**Value Proposition**:
- Historical Call Reports back to 1976
- Branch-level deposit data
- Failed bank cost analysis
- Deposit insurance assessments

**Implementation Notes**:
- Requires academic affiliation/registration
- Large files (multi-GB for full history)
- Focus on key tables for banking research

---

### 7. SEC 13F Institutional Holdings

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | SEC EDGAR |
| **URL** | https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&type=13F |
| **API Available** | Yes (EDGAR API) |
| **Estimated Effort** | 10-15 hours |
| **Data Format** | XML, JSON |

**Description**: Quarterly reports of institutional investment managers holding $100M+ in US equities. Shows who owns bank stocks.

**Value Proposition**:
- Track institutional ownership of major banks
- Identify concentrated holders
- Monitor ownership changes around stress events

**Key Analysis**:
- Top holders of each G-SIB
- Ownership concentration trends
- Pre/post SVB ownership changes

**Implementation Notes**:
- Extend existing `sec_client.py`
- Parse 13F-HR XML format
- Filter for bank-related holdings (SIC codes 6020-6029)

---

### 8. Federal Reserve NIC Structure Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Reserve National Information Center |
| **URL** | https://www.ffiec.gov/npw/Institution/TopHoldings |
| **API Available** | Partial (bulk download) |
| **Estimated Effort** | 8-12 hours |
| **Data Format** | CSV, XML |

**Description**: Complete relationship mapping of bank holding companies and their subsidiaries. Shows corporate structure of complex BHCs.

**Value Proposition**:
- Map holding company → subsidiary relationships
- Understand IHC structure for foreign banks
- Track M&A activity through structure changes

**Key Data**:
- Entity relationships (parent-child)
- Entity attributes (type, charter, regulator)
- Historical structure snapshots

**Implementation Notes**:
- Module stub exists at `API_MODULES/NIC_STRUCTURE_DATA/`
- Need to implement download and parsing
- Link to FDIC CERT and SEC CIK

---

### 9. CDS Spreads for Major Banks

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Multiple (IHS Markit, ICE, Bloomberg) |
| **URL** | Various (commercial) |
| **API Available** | Commercial only |
| **Estimated Effort** | 20-40 hours |
| **Data Format** | CSV |

**Description**: Credit default swap spreads provide market-implied credit risk for major banks. 5-year senior CDS is the benchmark.

**Value Proposition**:
- Market-based credit risk indicator
- Real-time stress signal (CDS spikes)
- Complement fundamental analysis

**Alternative Sources**:
- FRED has some historical bank CDS (limited)
- Academic datasets (WRDS if accessible)
- News sources for spot quotes

**Implementation Notes**:
- Commercial data is expensive
- Check if any free historical sources exist
- May need to scrape financial news for spot rates

---

### 10. S&P Global Market Intelligence (Commercial)

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | S&P Global |
| **URL** | https://www.spglobal.com/marketintelligence/ |
| **API Available** | Yes (commercial) |
| **Estimated Effort** | Variable |
| **Data Format** | Various |

**Description**: Commercial platform with verified bank financials, ratings, and analytics. The "gold standard" for bank data.

**Value Proposition**:
- Verified, cleaned data
- Global coverage
- Historical back to 1980s
- M&A transaction data

**Implementation Notes**:
- Requires subscription ($$$)
- Academic access possible through university
- Consider for validation of our data

---

## Priority 3: International Expansion

These items fill gaps in our international coverage.

### 11. Japanese FSA Banking Statistics

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Japan Financial Services Agency (FSA) |
| **URL** | https://www.fsa.go.jp/en/statistics/ |
| **API Available** | No (bulk download) |
| **Estimated Effort** | 10-15 hours |
| **Data Format** | Excel, PDF |

**Description**: Financial data for Japanese banks including the 3 G-SIBs (MUFG, SMFG, Mizuho).

**Value Proposition**:
- 3 G-SIBs with $8T+ combined assets
- Complete Asia G-SIB coverage
- Stress test results (BoJ)

**Key Data**:
- Banking sector statistics
- Individual major bank data
- NPL trends
- Capital adequacy

**Implementation Notes**:
- Some data in Japanese only
- PDF extraction may be needed
- Link to existing EBA/ECB data for comparison

---

### 12. APRA Australian Banking Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Australian Prudential Regulation Authority |
| **URL** | https://www.apra.gov.au/statistics |
| **API Available** | No (bulk download) |
| **Estimated Effort** | 8-12 hours |
| **Data Format** | Excel, CSV |

**Description**: Australian Big Four banks (CBA, Westpac, ANZ, NAB) are among largest in Asia-Pacific.

**Value Proposition**:
- Big Four = $3.5T AUD combined assets
- Well-regulated developed market
- Stress test results available

**Key Data**:
- ADI Statistics (monthly)
- Banking Statistics (quarterly)
- Stress test disclosures

**Implementation Notes**:
- Good English documentation
- Relatively straightforward download
- Add to `API_MODULES/APRA_DATA/`

---

### 13. HKMA Hong Kong Banking Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Hong Kong Monetary Authority |
| **URL** | https://www.hkma.gov.hk/eng/data-publications-and-research/data-and-statistics/ |
| **API Available** | Partial |
| **Estimated Effort** | 8-12 hours |
| **Data Format** | Excel, CSV |

**Description**: Hong Kong is major Asian financial center with significant cross-border banking.

**Value Proposition**:
- Gateway to China banking
- Major international banks present
- Cross-border exposure data

**Key Data**:
- Banking sector statistics
- Authorized institutions
- Cross-border positions

**Implementation Notes**:
- English documentation available
- Good statistical portal
- Complement BIS cross-border data

---

### 14. Swiss FINMA Banking Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Swiss Financial Market Supervisory Authority |
| **URL** | https://www.finma.ch/en/finma-public/financial-market-statistics/ |
| **API Available** | No (bulk download) |
| **Estimated Effort** | 6-10 hours |
| **Data Format** | Excel, PDF |

**Description**: Swiss G-SIBs (UBS, and historical Credit Suisse data).

**Value Proposition**:
- UBS is major G-SIB (Bucket 1)
- Credit Suisse failure case study
- Wealth management concentration

**Key Data**:
- Banking statistics
- UBS regulatory disclosures
- CS resolution documentation

**Implementation Notes**:
- Some data in German/French
- CS data important for failure analysis
- Link to EBA data (European operations)

---

### 15. MAS Singapore Banking Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Monetary Authority of Singapore |
| **URL** | https://www.mas.gov.sg/statistics |
| **API Available** | Yes (MAS API) |
| **Estimated Effort** | 6-8 hours |
| **Data Format** | JSON, CSV |

**Description**: Singapore is major Asian financial hub with DBS among largest Asian banks.

**Value Proposition**:
- DBS is largest SE Asian bank
- Comprehensive statistics
- API available

**Key Data**:
- Banking statistics
- Financial stability indicators
- Cross-border banking

**Implementation Notes**:
- MAS has good API
- English documentation
- Similar structure to HKMA

---

### 16. China CBIRC/PBOC Banking Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | China Banking and Insurance Regulatory Commission / PBOC |
| **URL** | http://www.cbirc.gov.cn/en/ |
| **API Available** | No |
| **Estimated Effort** | 20-30 hours |
| **Data Format** | PDF, HTML (Chinese) |

**Description**: China's Big Four (ICBC, CCB, ABC, BoC) are world's largest banks by assets.

**Value Proposition**:
- 4 of world's 5 largest banks
- $25T+ combined assets
- Essential for global picture

**Challenges**:
- Limited English disclosure
- No standardized API
- Different accounting standards
- Annual reports available but require translation

**Implementation Notes**:
- Focus on annual reports (English versions)
- Extract key metrics manually
- Use existing BIS data for cross-border view

---

## Priority 4: Specialized/Niche Data

Academic datasets and specialized regulatory data.

### 17. NBER Banking Crises Database

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | NBER / Reinhart-Rogoff |
| **URL** | https://www.nber.org/research/data |
| **API Available** | No (bulk download) |
| **Estimated Effort** | 4-6 hours |
| **Data Format** | Excel |

**Description**: Historical database of banking crises across countries and centuries.

**Value Proposition**:
- 200+ years of crisis history
- Cross-country comparison
- Academic credibility

**Implementation Notes**:
- One-time download
- Static dataset (updated occasionally)
- Integrate with `07_historical_events.csv`

---

### 18. Laeven & Valencia Systemic Banking Crises Database

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | IMF |
| **URL** | https://www.imf.org/en/Publications/WP/Issues/2018/09/14/Systemic-Banking-Crises-Revisited-46232 |
| **API Available** | No (Excel download) |
| **Estimated Effort** | 3-4 hours |
| **Data Format** | Excel |

**Description**: IMF dataset of systemic banking crises with fiscal costs and policy responses.

**Value Proposition**:
- Fiscal costs of crises
- Policy intervention details
- Resolution methods
- Updated through 2017

**Implementation Notes**:
- Download and integrate with historical events
- Link to country-level quality data

---

### 19. Historical Bankscope/Orbis Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Bureau van Dijk (now Moody's) |
| **URL** | https://www.bvdinfo.com/en-us/our-products/data/international/orbis-bank-focus |
| **API Available** | Commercial only |
| **Estimated Effort** | N/A |
| **Data Format** | Various |

**Description**: The historical standard for bank-level international data (now Orbis Bank Focus).

**Value Proposition**:
- Standardized global bank data
- Historical back to 1990s
- Used in academic research

**Implementation Notes**:
- Commercial access only
- Check university library access
- May have historical snapshots available

---

### 20. FDIC/OCC Enforcement Actions

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | FDIC, OCC, Federal Reserve |
| **URL** | https://www.fdic.gov/resources/resolutions/formal-enforcement-actions/ |
| **API Available** | No (HTML scraping) |
| **Estimated Effort** | 10-15 hours |
| **Data Format** | PDF, HTML |

**Description**: Formal enforcement actions (consent orders, cease and desist) against banks.

**Value Proposition**:
- Early warning of bank problems
- Compliance risk tracking
- Historical enforcement patterns

**Key Data**:
- Consent orders
- Civil money penalties
- Removal orders
- MOU violations

**Implementation Notes**:
- Requires web scraping
- PDFs need HDARP extraction
- Create enforcement action timeline

---

### 21. Federal Reserve Discount Window Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Reserve |
| **URL** | https://www.federalreserve.gov/monetarypolicy/discountrate.htm |
| **API Available** | Partial (historical only) |
| **Estimated Effort** | 4-6 hours |
| **Data Format** | PDF, CSV |

**Description**: Discount window borrowing data (disclosed with 2-year lag since Dodd-Frank).

**Value Proposition**:
- Liquidity stress indicator
- Historical crisis usage
- Bank-level borrowing data

**Implementation Notes**:
- 2-year disclosure lag limits real-time use
- Historical data useful for crisis analysis
- Check FRED for aggregate series

---

### 22. Federal Home Loan Bank Advances Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | FHLB System |
| **URL** | https://www.fhlbanks.com/data-resources |
| **API Available** | No (bulk download) |
| **Estimated Effort** | 6-10 hours |
| **Data Format** | Excel |

**Description**: FHLB advances are major funding source for many banks (key in SVB failure).

**Value Proposition**:
- Critical funding indicator
- SVB relied heavily on FHLB
- Regional bank funding analysis

**Key Data**:
- Advances by member bank
- Regional FHLB statistics
- Member financial data

**Implementation Notes**:
- Aggregate data publicly available
- Member-level may require registration
- Important for early warning enhancement

---

## Priority 5: Aspirational (Commercial/Restricted)

These are commercial products or restricted access sources.

### 23. Bloomberg Terminal Banking Data

| Attribute | Value |
|-----------|-------|
| **Status** | Aspirational |
| **Source** | Bloomberg L.P. |
| **Cost** | ~$24,000/year |
| **Value** | Comprehensive real-time data |

**What We'd Get**:
- Real-time bank stock prices
- CDS spreads
- Bond pricing
- Analyst estimates
- Comprehensive financials

**Alternative**: Our Yahoo Finance + Alpha Vantage + Finnhub setup covers most needs.

---

### 24. Refinitiv/LSEG Eikon Banking Data

| Attribute | Value |
|-----------|-------|
| **Status** | Aspirational |
| **Source** | London Stock Exchange Group |
| **Cost** | ~$22,000/year |
| **Value** | Bloomberg alternative |

**What We'd Get**:
- Similar to Bloomberg
- Better for fixed income
- Regulatory data integration

---

### 25. Moody's Analytics BankFocus

| Attribute | Value |
|-----------|-------|
| **Status** | Aspirational |
| **Source** | Moody's Analytics (BvD) |
| **Cost** | Enterprise pricing |
| **Value** | Global bank database |

**What We'd Get**:
- 45,000+ banks worldwide
- Standardized financials
- Ownership data
- Historical back to 1990s

**Note**: This is the successor to Bankscope.

---

### 26. ICE/Markit CDS Pricing

| Attribute | Value |
|-----------|-------|
| **Status** | Aspirational |
| **Source** | ICE Data Services / IHS Markit |
| **Cost** | Enterprise pricing |
| **Value** | Definitive CDS data |

**What We'd Get**:
- Real-time CDS spreads
- Historical CDS curves
- Bank credit risk monitoring

---

## Implementation Roadmap

### Phase 1: Quick Wins (Priority 1)
**Timeline**: 2-3 weeks
**Focus**: Items 1-5

1. World Bank GFDD integration (extend existing WDI collector)
2. OECD Banking Statistics expansion
3. OpenFIGI identifier mapping
4. FDIC problem bank indicators (derive from Call Reports)
5. Fed scenario automation preparation

### Phase 2: High-Value Additions (Priority 2)
**Timeline**: 4-6 weeks
**Focus**: Items 6-10

1. SEC 13F institutional holdings
2. Fed NIC structure data
3. FDIC ResearchConnect (if accessible)
4. CDS spread alternatives research

### Phase 3: International Expansion (Priority 3)
**Timeline**: 6-8 weeks
**Focus**: Items 11-16

1. Japanese FSA data
2. APRA Australian data
3. HKMA Hong Kong data
4. FINMA Swiss data
5. MAS Singapore data
6. China CBIRC basics

### Phase 4: Specialized Data (Priority 4)
**Timeline**: Ongoing
**Focus**: Items 17-22

1. Academic crisis databases
2. Enforcement actions scraping
3. FHLB advances data

---

## Cross-Reference: What We Already Have

**DO NOT DUPLICATE** - These are already collected:

| Source | Location | Records |
|--------|----------|---------|
| FDIC BankFind | `API_MODULES/FDIC_BANKFIND_DATA/` | 4,363 banks |
| FFIEC Call Reports | `API_MODULES/FFIEC_CALL_REPORTS_DATA/` | 240 records |
| SEC EDGAR | `API_MODULES/SEC_BANKING_DATA/` | 110 10-Ks |
| Fed H.8 | `API_MODULES/FED_H8_DATA/` | Sector snapshot |
| BIS | `DATA/InternationalBanking/BIS/` + `API_MODULES/` | 23GB |
| EBA | `API_MODULES/EBA_DATA/` | 31 EU banks |
| ECB | `API_MODULES/ECB_DATA/` | 11 countries |
| IMF FSI | `API_MODULES/IMF_DATA/` | 15 countries |
| BoE | `DATA/BoE/` + `API_MODULES/BIS_DATA/` | UK stress tests |
| Canada OSFI | `API_MODULES/BIS_DATA/` | Big Six |
| Yahoo Finance | `API_MODULES/MARKET_DATA/` | 58 tickers |
| FDIC QBP | `DATA/FDIC/quarterly_banking_profile/` | Time series |
| Summary of Deposits | `DATA/FDIC/summary_of_deposits/` | 2020-2024 |
| JST Dataset | `DATA/JST/` | R6 |
| HMDA | `DATA/HMDA/` | 59M+ records |

---

## Wishlist Status Legend

| Status | Meaning |
|--------|---------|
| Not Started | Item identified, no work begun |
| In Progress | Active data collection |
| Blocked | External dependency or access issue |
| Complete | Data collected and integrated |
| Deferred | Postponed due to low priority or complexity |

---

---

## API Availability Research Summary

### Priority 1 Items - API Status

| Item | API | Auth | Rate Limits | Documentation |
|------|-----|------|-------------|---------------|
| FDIC Problem Indicators | BankFind REST | None | 1000/min | Good |
| Fed Scenario API | None (PDF) | N/A | N/A | PDF only |
| OECD Banking Stats | SDMX REST | None | 200/min | Good |
| World Bank GFDD | WDI REST | None | Unlimited | Excellent |
| OpenFIGI | REST | API Key (free) | 100 req/min | Good |

### Priority 2 Items - API Status

| Item | API | Auth | Effort | Notes |
|------|-----|------|--------|-------|
| FDIC ResearchConnect | Bulk download | Registration | Medium | Academic access |
| SEC 13F Holdings | EDGAR REST | None | Medium | XML parsing |
| Fed NIC Structure | Bulk CSV | None | Medium | Relationship data |
| CDS Spreads | Commercial | Subscription | High | Evaluate alternatives |

### Priority 3 Items - API Status

| Country | API | Language | Effort |
|---------|-----|----------|--------|
| Japan FSA | None | Japanese/English | High |
| APRA Australia | Bulk download | English | Medium |
| HKMA Hong Kong | Partial API | English | Medium |
| FINMA Swiss | None | German/English | Medium |
| MAS Singapore | REST API | English | Low |
| China CBIRC | None | Chinese | Very High |

### Recommended Implementation Order

Based on API availability and effort:

1. **World Bank GFDD** - Best API, highest coverage
2. **OECD Banking Stats** - Good API, extends existing collector
3. **OpenFIGI Mapping** - Simple API, immediate value
4. **MAS Singapore** - Good API, fills Asia gap
5. **SEC 13F Holdings** - Extends existing SEC client
6. **APRA Australia** - English docs, straightforward
7. **Fed NIC Structure** - Completes US data

---

**Document Version**: 1.0
**Last Updated**: January 2026
**Maintainer**: Banking Research Project Team

