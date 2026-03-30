# Banking Data Expansion Wishlist V2

## Overview

This wishlist documents **25 new data sources** for the Banking Master Dataset. All items have been verified as NOT already collected in existing modules. Items are prioritized by analytical value and implementation feasibility.

**Version**: 2.0
**Created**: January 2026
**Total Items**: 25
**Status**: Active

---

## Summary by Priority

| Priority | Items | Description | Est. Total Records |
|----------|-------|-------------|-------------------|
| P1 | 5 | High value, API-available | 500,000+ |
| P2 | 5 | Regulatory framework data | 15,000+ |
| P3 | 5 | Enforcement and risk data | 5,000+ |
| P4 | 5 | International regulator documents | 500+ |
| P5 | 5 | Market and credit risk data | 50,000+ |

---

## Priority 1: High-Value, API-Available

### W1. FFIEC Uniform Bank Performance Reports (UBPR)

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | FFIEC Central Data Repository |
| **URL** | https://cdr.ffiec.gov/public/PWS/UbprReports.aspx |
| **API Available** | Yes (bulk download) |
| **Estimated Records** | 4,363 banks x 20 quarters = 87,000+ |
| **Effort** | 8 hours |
| **Data Format** | PDF, CSV (via CDR) |

**Description**: The UBPR provides standardized financial ratios and peer group comparisons for every FDIC-insured bank. It's the primary tool bank examiners use to evaluate bank performance.

**Key Metrics**:
- Peer group comparisons (asset size, charter type)
- Trend analysis (5-year history)
- Risk indicators (liquidity, credit, interest rate)
- Profitability ratios
- Capital adequacy measures

**Value Proposition**:
- Official examiner analysis tool
- Pre-calculated ratios save processing time
- Peer benchmarking capabilities
- Enhances early warning system

**Implementation Notes**:
- CDR bulk download available
- Focus on Tier 0-2 banks initially (50 banks)
- Parse PDF or use structured data exports
- Create `API_MODULES/UBPR_DATA/`

---

### W2. OCC Quarterly Report on Bank Trading and Derivatives

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Office of the Comptroller of the Currency |
| **URL** | https://www.occ.gov/publications-and-resources/publications/quarterly-report-on-bank-trading/index.html |
| **API Available** | No (PDF reports) |
| **Estimated Records** | 8 G-SIBs x 40 quarters = 320 |
| **Effort** | 6 hours |
| **Data Format** | PDF |

**Description**: Quarterly report on trading revenue and derivatives activities of the largest US commercial banks. Essential for understanding trading risk in G-SIBs.

**Key Metrics**:
- Trading revenue by risk type (interest rate, FX, equity, commodity, credit)
- Notional derivatives by type
- Credit exposure from derivatives
- Credit derivatives (bought/sold protection)
- VaR trends

**Value Proposition**:
- Only public source for bank-level trading revenue breakdown
- Derivatives exposure monitoring
- Trading risk concentration analysis
- Complements stress test data

**Implementation Notes**:
- PDF extraction required (use HDARP)
- Data tables are standardized across quarters
- Focus on 8 largest trading banks
- Historical data back to 1995

---

### W3. Federal Reserve Y-9C Reports (Holding Company Data)

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Reserve / FFIEC |
| **URL** | https://www.ffiec.gov/npw/ |
| **API Available** | Yes (bulk download) |
| **Estimated Records** | 500 BHCs x 20 quarters = 10,000+ |
| **Effort** | 10 hours |
| **Data Format** | CSV, SAS |

**Description**: Consolidated financial statements for bank holding companies. Provides holding company-level view that complements bank-level Call Reports.

**Key Metrics**:
- Consolidated assets, liabilities, equity
- Non-bank subsidiary activities
- Intercompany transactions
- Holding company capital ratios
- Off-balance sheet exposures

**Value Proposition**:
- Complete holding company picture
- Links to SEC filings via RSSD
- Required for G-SIB analysis
- Captures non-bank subsidiaries

**Implementation Notes**:
- Bulk download from FFIEC NPW
- Use existing RSSD mappings
- Focus on top 100 BHCs by assets
- Create `API_MODULES/FED_Y9C_DATA/`

---

### W4. Federal Reserve SR Letters and Supervisory Guidance

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Reserve Board |
| **URL** | https://www.federalreserve.gov/supervisionreg/srletters.htm |
| **API Available** | No (HTML + PDF) |
| **Estimated Records** | 200+ documents |
| **Effort** | 8 hours |
| **Data Format** | HTML, PDF |

**Description**: SR Letters provide supervisory guidance to bank examiners and regulated institutions. Essential for understanding regulatory expectations.

**Key Categories**:
- SR Letters (binding guidance)
- CA Letters (application procedures)
- Supervisory guidance
- Frequently asked questions

**Value Proposition**:
- Regulatory interpretation source
- Policy evolution tracking
- Compliance requirement documentation
- Examiner expectation clarity

**Implementation Notes**:
- Web scraping for index
- PDF download for full text
- Categorize by topic (capital, liquidity, risk management)
- Create searchable index

---

### W5. FHFA House Price Index Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Housing Finance Agency |
| **URL** | https://www.fhfa.gov/data |
| **API Available** | Yes (CSV download) |
| **Estimated Records** | 50 states x 200 quarters = 10,000+ |
| **Effort** | 4 hours |
| **Data Format** | CSV, Excel |

**Description**: Official house price indices used in stress testing and real estate analysis. More granular than Case-Shiller.

**Key Data**:
- State-level HPI (purchase-only, all-transactions)
- MSA-level HPI (400+ metros)
- Census division indices
- Seasonally adjusted and non-adjusted

**Value Proposition**:
- Official stress test input
- Regional real estate risk assessment
- Mortgage portfolio stress analysis
- More granular than national indices

**Implementation Notes**:
- Direct CSV downloads available
- Historical data back to 1975
- Easy integration with existing data
- Use for regional bank analysis

---

## Priority 2: Regulatory Framework Data

### W6. FSB G-SIB Assessment Methodology Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Financial Stability Board |
| **URL** | https://www.fsb.org/work-of-the-fsb/policy-development/addressing-sifis/ |
| **API Available** | No (PDF + Excel) |
| **Estimated Records** | 29 G-SIBs x 10 years x 5 categories = 1,450 |
| **Effort** | 6 hours |
| **Data Format** | PDF, Excel |

**Description**: Detailed G-SIB indicator scores used to determine bucket assignments and capital surcharges.

**Key Metrics (12 Indicators)**:
- Size (total exposures)
- Interconnectedness (intra-financial assets/liabilities/securities)
- Substitutability (payments, assets under custody, underwriting)
- Complexity (OTC derivatives, Level 3 assets, trading securities)
- Cross-jurisdictional activity (claims, liabilities)

**Value Proposition**:
- Official G-SIB scoring methodology
- Track systemic importance trends
- Predict bucket changes
- Compare US vs international G-SIBs

**Implementation Notes**:
- Annual disclosure in November
- Historical data since 2012
- Link to existing G-SIB table
- Create indicator time series

---

### W7. Basel III Monitoring Reports

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Bank for International Settlements |
| **URL** | https://www.bis.org/bcbs/qis/ |
| **API Available** | No (PDF + Excel) |
| **Estimated Records** | Semi-annual x 10 years = 20 reports |
| **Effort** | 8 hours |
| **Data Format** | PDF, Excel |

**Description**: BIS monitoring of Basel III implementation across member jurisdictions. Aggregate data on capital and liquidity.

**Key Metrics**:
- CET1, Tier 1, Total Capital by region
- LCR and NSFR compliance
- Leverage ratio distribution
- RWA composition

**Value Proposition**:
- Global implementation progress
- Cross-jurisdiction comparison
- Regulatory capital trends
- Liquidity compliance tracking

**Implementation Notes**:
- Semi-annual reports
- Aggregate (not bank-level)
- Useful for regulatory comparison analysis
- Complements existing `27_regulatory_comparison.csv`

---

### W8. FDIC Quarterly Banking Profile (Expanded)

| Attribute | Value |
|-----------|-------|
| **Status** | Partial (aggregate only) |
| **Source** | FDIC |
| **URL** | https://www.fdic.gov/analysis/quarterly-banking-profile/ |
| **API Available** | Yes (CSV) |
| **Estimated Records** | 40 quarters x 100 metrics = 4,000 |
| **Effort** | 4 hours |
| **Data Format** | CSV, PDF |

**Description**: While we have QBP aggregates, the full historical time series with all metrics is not fully integrated.

**Key Metrics**:
- Industry income and expense
- Asset quality trends
- Capital ratios distribution
- Problem bank count
- DIF fund balance

**Value Proposition**:
- Official industry health assessment
- Historical trend analysis
- Problem bank monitoring
- Deposit insurance fund status

**Implementation Notes**:
- Extend existing QBP data
- Full time series back to 1984
- All metrics (not just selected)
- Create comprehensive historical file

---

### W9. Federal Reserve Z.1 Financial Accounts

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Reserve Board |
| **URL** | https://www.federalreserve.gov/releases/z1/ |
| **API Available** | Yes (XML, CSV) |
| **Estimated Records** | 80 years x 4 quarters x 50 series = 16,000+ |
| **Effort** | 6 hours |
| **Data Format** | CSV, XML |

**Description**: The Flow of Funds accounts provide macro-level view of financial sector assets, liabilities, and flows.

**Key Tables**:
- L.110 (U.S.-Chartered Commercial Banks)
- L.111 (Foreign Banking Offices)
- L.115 (Bank Holding Companies)
- L.120 (Credit Unions)
- L.130 (Money Market Funds)

**Value Proposition**:
- Macro context for bank analysis
- System-wide leverage trends
- Funding market dynamics
- Long historical series (1945+)

**Implementation Notes**:
- Use FRED API or direct download
- Focus on banking sector tables
- Quarterly frequency
- Integrate with macro analysis

---

### W10. NCUA Credit Union Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | National Credit Union Administration |
| **URL** | https://www.ncua.gov/analysis/cuso-economic-data |
| **API Available** | Yes (bulk download) |
| **Estimated Records** | 4,700 CUs x 20 quarters = 94,000 |
| **Effort** | 8 hours |
| **Data Format** | CSV, XML |

**Description**: Credit unions compete with banks in consumer lending. Complete Call Report data available.

**Key Metrics**:
- Assets, deposits, loans
- Membership
- Net worth ratio
- Delinquency rates
- ROA, ROE

**Value Proposition**:
- Competitive landscape analysis
- Consumer lending comparison
- Alternative to bank financing trends
- Community bank competitor view

**Implementation Notes**:
- NCUA provides bulk Call Report data
- Similar structure to bank Call Reports
- Focus on largest 100 CUs
- Compare to community bank metrics

---

## Priority 3: Enforcement and Risk Data

### W11. FDIC Enforcement Actions Database

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | FDIC |
| **URL** | https://orders.fdic.gov/s/ |
| **API Available** | Yes (searchable database) |
| **Estimated Records** | 1,000+ actions |
| **Effort** | 12 hours |
| **Data Format** | HTML, PDF |

**Description**: Formal enforcement actions including consent orders, cease and desist orders, and civil money penalties.

**Action Types**:
- Consent Orders
- Cease and Desist Orders
- Civil Money Penalties
- Removal/Prohibition Orders
- Termination of Insurance
- Section 19 Orders

**Value Proposition**:
- Early warning of bank problems
- Regulatory violation patterns
- Compliance risk tracking
- Historical enforcement trends

**Implementation Notes**:
- FDIC Orders Portal is searchable
- PDF documents for each action
- Create structured database
- Link to bank CERT numbers

---

### W12. OCC Enforcement Actions

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Office of the Comptroller of the Currency |
| **URL** | https://www.occ.gov/topics/laws-and-regulations/enforcement-actions/index.html |
| **API Available** | No (HTML list) |
| **Estimated Records** | 800+ actions |
| **Effort** | 10 hours |
| **Data Format** | HTML, PDF |

**Description**: Enforcement actions against national banks and federal savings associations.

**Action Types**:
- Formal Agreements
- Consent Orders
- Cease and Desist Orders
- Civil Money Penalties
- Prompt Corrective Action
- Safety and Soundness Orders

**Value Proposition**:
- National bank compliance tracking
- Large bank enforcement history
- G-SIB regulatory issues (Wells Fargo, etc.)
- BSA/AML enforcement patterns

**Implementation Notes**:
- Web scraping required
- Searchable by bank name
- Historical data available
- Focus on large bank actions

---

### W13. Federal Reserve Enforcement Actions

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Reserve Board |
| **URL** | https://www.federalreserve.gov/supervisionreg/enforcement-actions.htm |
| **API Available** | No (HTML list) |
| **Estimated Records** | 600+ actions |
| **Effort** | 10 hours |
| **Data Format** | HTML, PDF |

**Description**: Enforcement actions against bank holding companies and state member banks.

**Action Types**:
- Written Agreements
- Cease and Desist Orders
- Civil Money Penalties
- Removal Orders
- Prompt Corrective Action

**Value Proposition**:
- BHC-level enforcement tracking
- G-SIB regulatory history
- Holding company compliance
- State member bank issues

**Implementation Notes**:
- Searchable by institution
- Link to RSSD numbers
- Historical data since 2000
- Create unified enforcement database

---

### W14. CFPB Enforcement Actions

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Consumer Financial Protection Bureau |
| **URL** | https://www.consumerfinance.gov/enforcement/actions/ |
| **API Available** | Yes (API available) |
| **Estimated Records** | 400+ actions |
| **Effort** | 6 hours |
| **Data Format** | JSON, HTML |

**Description**: Consumer protection enforcement against banks and non-bank financial companies.

**Common Violations**:
- Unfair, deceptive, abusive acts (UDAAP)
- Fair lending violations
- Mortgage servicing issues
- Credit card practices
- Debt collection violations

**Value Proposition**:
- Consumer compliance risk
- Reputational risk indicator
- Fair lending enforcement
- Large penalty tracking

**Implementation Notes**:
- CFPB has public API
- Structured data available
- Filter for banks only
- Track penalties by institution

---

### W15. SEC Bank-Related Enforcement

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Securities and Exchange Commission |
| **URL** | https://www.sec.gov/litigation/litreleases.htm |
| **API Available** | Partial (EDGAR) |
| **Estimated Records** | 300+ bank-related |
| **Effort** | 8 hours |
| **Data Format** | HTML, PDF |

**Description**: SEC enforcement actions against bank holding companies for securities violations.

**Common Issues**:
- Securities fraud
- Insider trading
- Disclosure violations
- Municipal bond issues
- Investment advisor violations

**Value Proposition**:
- Securities compliance risk
- Disclosure quality assessment
- Investment banking violations
- Broker-dealer issues

**Implementation Notes**:
- Filter litigation releases for banks
- Use SIC codes 6020-6029
- Link to CIK numbers
- Focus on BHC actions

---

## Priority 4: International Regulator Documents

### W16. EBA Pillar 3 Disclosures Hub

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | European Banking Authority |
| **URL** | https://www.eba.europa.eu/risk-analysis-and-data/pillar-3-disclosures |
| **API Available** | Yes (data portal) |
| **Estimated Records** | 100+ banks x 10 years |
| **Effort** | 10 hours |
| **Data Format** | Excel, CSV |

**Description**: Standardized risk disclosures for EU banks under Basel III Pillar 3 requirements.

**Key Disclosures**:
- Capital composition
- RWA by risk type
- Credit risk exposures
- Market risk metrics
- Leverage ratio details

**Value Proposition**:
- Granular EU bank risk data
- Standardized across banks
- Complements stress test data
- Historical comparability

**Implementation Notes**:
- EBA data portal has structured data
- Annual disclosure frequency
- Focus on G-SIBs and large EU banks
- Link to existing EBA data

---

### W17. ECB Banking Supervision Annual Reports

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | ECB Banking Supervision |
| **URL** | https://www.bankingsupervision.europa.eu/press/publications/html/index.en.html |
| **API Available** | No (PDF) |
| **Estimated Records** | 10 annual reports |
| **Effort** | 6 hours |
| **Data Format** | PDF |

**Description**: Annual reports on SSM supervision activities, priorities, and findings.

**Key Content**:
- Supervisory priorities
- SREP results (aggregate)
- Thematic reviews
- Risk assessments
- Enforcement statistics

**Value Proposition**:
- ECB supervisory focus areas
- EU bank risk assessment
- Policy evolution tracking
- Supervisory intensity metrics

**Implementation Notes**:
- PDF extraction for key statistics
- Annual since 2015
- Create structured summary
- Track supervisory priorities

---

### W18. Bank of England Financial Stability Reports

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Bank of England |
| **URL** | https://www.bankofengland.co.uk/financial-stability-report |
| **API Available** | Partial (data downloads) |
| **Estimated Records** | 20+ reports |
| **Effort** | 8 hours |
| **Data Format** | PDF, Excel |

**Description**: Semi-annual reports on UK and global financial stability risks.

**Key Content**:
- UK banking sector health
- Global risk assessment
- Stress test results
- Countercyclical buffer decisions
- Macroprudential policy

**Value Proposition**:
- UK systemic risk view
- CCyB decision rationale
- Global risk perspective
- Housing market assessment

**Implementation Notes**:
- Data annex available in Excel
- Semi-annual since 1996
- Key statistics in charts
- Extract CCyB history

---

### W19. APRA Insight Publications

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Australian Prudential Regulation Authority |
| **URL** | https://www.apra.gov.au/publications |
| **API Available** | No (PDF) |
| **Estimated Records** | 50+ publications |
| **Effort** | 6 hours |
| **Data Format** | PDF |

**Description**: APRA publications on supervisory approach, risk findings, and policy.

**Key Publications**:
- Insight articles
- Information papers
- Discussion papers
- Prudential standards
- Letters to ADIs

**Value Proposition**:
- Australian supervisory perspective
- "Unquestionably strong" implementation
- Housing risk views
- Big Four oversight

**Implementation Notes**:
- Focus on ADI-related publications
- Create publication index
- Extract key policy positions
- Track supervisory themes

---

### W20. BIS Basel Committee Publications

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Bank for International Settlements |
| **URL** | https://www.bis.org/bcbs/publications.htm |
| **API Available** | No (HTML + PDF) |
| **Estimated Records** | 500+ publications |
| **Effort** | 8 hours |
| **Data Format** | PDF |

**Description**: Basel Committee publications including standards, guidelines, and consultative documents.

**Key Categories**:
- Standards (binding)
- Guidelines (best practices)
- Consultative documents
- FAQ documents
- Quantitative impact studies

**Value Proposition**:
- Global regulatory standards source
- Policy evolution tracking
- Implementation guidance
- Future regulation preview

**Implementation Notes**:
- Create searchable publication index
- Categorize by topic (capital, liquidity, etc.)
- Track standard versions
- Link to implementation dates

---

## Priority 5: Market and Credit Risk Data

### W21. DTCC Global Trade Repository Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Depository Trust & Clearing Corporation |
| **URL** | https://pddata.dtcc.com/gtr/ |
| **API Available** | Yes (public data) |
| **Estimated Records** | Weekly x 10 years x 5 asset classes = 2,600 |
| **Effort** | 10 hours |
| **Data Format** | CSV |

**Description**: Aggregated derivatives trade data from DTCC swap data repositories.

**Key Data**:
- Notional outstanding by asset class
- Trade counts
- Gross/net exposures
- Cleared vs uncleared
- Maturity distribution

**Value Proposition**:
- Derivatives market structure
- Clearing trends
- Systemic risk monitoring
- OTC market transparency

**Implementation Notes**:
- Weekly data available
- Aggregate (not bank-level)
- Complements OCC trading report
- Create time series database

---

### W22. Fed Repo and Reverse Repo Data

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Federal Reserve Bank of New York |
| **URL** | https://www.newyorkfed.org/markets/desk-operations |
| **API Available** | Yes (CSV download) |
| **Estimated Records** | Daily x 10 years = 2,500+ |
| **Effort** | 6 hours |
| **Data Format** | CSV |

**Description**: Daily data on Fed's repo and reverse repo operations, including facility usage.

**Key Data**:
- RRP facility usage (daily)
- Repo operations
- Standing repo facility
- Counterparty counts
- Rate data

**Value Proposition**:
- Money market stress indicator
- Bank liquidity demand
- Fed facility reliance
- Rate floor implementation

**Implementation Notes**:
- Direct CSV downloads
- Daily frequency
- Historical since 2013
- Create liquidity stress indicators

---

### W23. Treasury TIC Data (Banking Sector)

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | U.S. Treasury |
| **URL** | https://home.treasury.gov/data/treasury-international-capital-tic-system |
| **API Available** | Yes (CSV download) |
| **Estimated Records** | Monthly x 20 years x 50 countries = 12,000 |
| **Effort** | 8 hours |
| **Data Format** | CSV |

**Description**: Cross-border banking claims and liabilities data.

**Key Reports**:
- TIC B forms (banking data)
- Claims on foreigners
- Liabilities to foreigners
- Country breakdown
- Bank vs non-bank

**Value Proposition**:
- Cross-border exposure monitoring
- Country risk concentration
- Foreign bank presence in US
- Dollar funding flows

**Implementation Notes**:
- Monthly releases
- Country-level detail
- Bank-specific tables
- Link to BIS data

---

### W24. SIFMA Fixed Income Statistics

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | Securities Industry and Financial Markets Association |
| **URL** | https://www.sifma.org/resources/research/research-quarterly-us-fixed-income/ |
| **API Available** | No (Excel download) |
| **Estimated Records** | Quarterly x 10 years x 20 series = 800 |
| **Effort** | 6 hours |
| **Data Format** | Excel |

**Description**: Fixed income market statistics including bank debt issuance.

**Key Data**:
- Corporate bond issuance (by sector)
- Bank debt outstanding
- Secondary market trading volumes
- Spread trends
- Maturity profiles

**Value Proposition**:
- Bank funding market trends
- Debt issuance patterns
- Market access indicators
- Refinancing risk assessment

**Implementation Notes**:
- Quarterly reports
- Excel downloads
- Filter for financial sector
- Create issuance time series

---

### W25. ICE BofA Credit Indices (via FRED)

| Attribute | Value |
|-----------|-------|
| **Status** | Not Started |
| **Source** | ICE / Federal Reserve (FRED) |
| **URL** | https://fred.stlouisfed.org/categories/32413 |
| **API Available** | Yes (FRED API) |
| **Estimated Records** | Daily x 20 years x 10 series = 50,000+ |
| **Effort** | 4 hours |
| **Data Format** | CSV, JSON |

**Description**: Credit spread indices available free via FRED, including bank-relevant series.

**Key Series**:
- BAMLC0A4CBBB (BBB Corporate OAS)
- BAMLH0A0HYM2 (High Yield OAS)
- BAMLC0A1CAAA (AAA Corporate OAS)
- Financial sector sub-indices
- Bank bond spreads

**Value Proposition**:
- Free credit spread data
- Daily frequency
- Long history (1996+)
- Market stress indicator

**Implementation Notes**:
- Use existing FRED collector
- Add banking-specific series
- Create credit conditions index
- Link to stress scenarios

---

## Cross-Reference: Already Collected (DO NOT DUPLICATE)

| Source | Status | Records |
|--------|--------|---------|
| FDIC BankFind | Complete | 4,363 banks |
| FFIEC Call Reports | Complete | 240+ records |
| SEC EDGAR 10-K/10-Q | Complete | 110 filings |
| Fed H.8 | Complete | Sector snapshot |
| BIS Statistics | Complete | 23GB+ |
| EBA Transparency/Stress | Complete | 31 EU banks |
| ECB SDW | Complete | 11 countries |
| IMF FSI | Complete | 15 countries |
| World Bank GFDD | Complete | 11,636 records |
| OpenFIGI | Complete | 52 tickers |
| Laeven-Valencia Crises | Complete | 30 episodes |
| NBER Crises | Complete | 47 episodes |
| Japan FSA | Complete | 8 banks |
| Australia APRA | Complete | 8 banks |
| Singapore MAS | Complete | 3 banks |
| Hong Kong HKMA | Complete | 5 banks |
| Switzerland FINMA | Complete | 6 banks |
| China CBIRC | Complete | 10 banks |
| Global Stress Scenarios | Complete | 65 scenarios |
| Global Bank Stress Results | Complete | 133 bank-years |
| Stress Severity Index | Complete | 62 records |

---

## Implementation Roadmap

### Week 1: High-Value APIs
1. FHFA House Price Index (W5)
2. Fed Z.1 Financial Accounts (W9)
3. ICE BofA Credit Indices (W25)
4. Fed Repo/RRP Data (W22)

### Week 2: Regulatory Data
1. FDIC QBP Expansion (W8)
2. OCC Trading Report (W2)
3. FSB G-SIB Methodology (W6)

### Week 3: Enforcement Actions
1. FDIC Enforcement (W11)
2. CFPB Enforcement (W14)
3. OCC Enforcement (W12)
4. Fed Enforcement (W13)

### Week 4: Complex Sources
1. FFIEC UBPR (W1)
2. Fed Y-9C Reports (W3)
3. TIC Data (W23)

---

**Document Version**: 2.0
**Last Updated**: January 2026
**Maintainer**: Banking Research Project Team

