# HDARP Wishlist

**Consolidated PDF and Document Acquisition Wishlists**

A centralized collection of all document acquisition wishlists from across the research workspace. These files catalog PDFs, books, academic papers, regulatory documents, and online data sources that are desired for HDARP processing, knowledge base expansion, and research replication.

---

## Repository Structure

```
hdarp-wishlist/
├── README.md
├── CATALOG.md
├── national_accounts/              # National income accounting & political economy methodology
│   ├── acquisition_wishlist.csv    # 20 items — historical methodology PDFs with URLs
│   ├── methodology_wishlist.csv    # 24 items — OECD, BEA, BLS methodology sources
│   ├── methodology_kb_wishlist.csv # 48 items — comprehensive methodology PDF tracker
│   ├── pdf_wishlist.md             # Prioritized historical source books/PDFs
│   ├── historical_data_sources_wishlist.md  # Complete data sources + PDF wishlist
│   ├── hdarp_inventory.json        # HDARP processing inventory (page counts, sizes, densities)
│   ├── hdarp_inventory_corrected.json  # Corrected inventory with resolved paths
│   └── hdarp_figure_wishlist.csv   # HDARP figure metadata for visualization
├── banking_research/               # Banking sector, stress testing, financial regulation
│   ├── kb_wishlist_master_2026-03-29.csv   # ★ DEFINITIVE: 795 items — the master wishlist
│   ├── kb_wishlist_summary_2026-03-29.md   # Summary report (201 downloaded, 587 needed)
│   ├── kb_wishlist_update_2026-03-29.md    # Update notes inc. Second-HDARP (394 PDFs, 15.3 GB)
│   ├── kb_wishlist_2026-03-29.html         # HTML version for browser viewing
│   ├── kb_wishlist_2026-03-08.csv          # Prior version (775 items)
│   ├── kb_wishlist_summary_2026-03-08.md   # Summary with category breakdown
│   ├── comprehensive_kb_wishlist_452.csv   # 452-item comprehensive version (2026-02-25)
│   ├── wishlist_narrative_guide.md         # 841-line narrative across 45 categories
│   ├── unified_wishlist_407.csv            # 407-item unified wishlist with search queries
│   ├── comprehensive_literature_wishlist.md  # 332 items across 20 research topics
│   ├── comprehensive_wishlist_catalog.csv  # 180+ items — master acquisition catalog
│   ├── banking_data_wishlist_v1.md         # 26 banking data expansion items
│   ├── banking_data_wishlist_v2.md         # 25 new data source items (V2)
│   ├── wishlist_status_tracker_v1.csv      # Status tracker for V1 items
│   ├── wishlist_status_tracker_v2.csv      # Status tracker for V2 items
│   ├── pdf_acquisition_wishlist_stress_testing.md  # Stress test PDF acquisition targets
│   ├── data_enhancement_wishlist.md        # Data gaps and 147 banking ratios roadmap
│   ├── original_pdf_wishlist.md            # Original stress testing platform PDF wishlist
│   ├── dissertation_wishlist_update.md     # Dissertation-related wishlist reconciliation
│   └── deprecated_data_wishlist.md         # Older wishlist (historical reference)
├── political_economy/              # Heterodox economics & labor value theory
│   ├── online_sources_wishlist.md  # Online data sources for validation work
│   └── online_sources_wishlist.json  # Machine-readable version
└── municipal_research/             # County-level government data
    └── manual_download_wishlist.md # County budget PDFs and municipal sources
```

---

## Domain Descriptions

### National Accounts (`national_accounts/`)

Wishlists for acquiring historical economic methodology PDFs — NIPA construction papers, BLS handbooks, NBER monographs, OECD manuals, and classic texts on national income accounting. These support replication of long-run economic time series (GDP, capital stock, profit rates, price indices) from primary sources.

**Key files:**
- `methodology_kb_wishlist.csv` — the most comprehensive tracker (48 items with status)
- `historical_data_sources_wishlist.md` — narrative guide to all historical data sources
- `hdarp_inventory.json` — PDFs already acquired and queued for HDARP extraction

### Banking Research (`banking_research/`)

Wishlists covering banking sector literature, regulatory documents, and data sources for stress testing, financial stability, and systemic risk research. This is the largest section with 20 files spanning the full evolution of the wishlist from 180 items to 795 items.

**Key files:**
- `kb_wishlist_master_2026-03-29.csv` — **the definitive master wishlist** (795 items, 45 categories, with download statuses and source URLs)
- `wishlist_narrative_guide.md` — 841-line narrative guide across 45 thematic categories
- `kb_wishlist_update_2026-03-29.md` — documents 394 unprocessed PDFs (15.3 GB) in the Second-HDARP pipeline
- `data_enhancement_wishlist.md` — data gaps analysis and roadmap for 147 additional banking ratios

### Political Economy (`political_economy/`)

Online data source wishlists for extending heterodox economics replication work — BEA, FRED, and BLS API sources needed to bridge historical book data (1948-1989) to the present.

### Municipal Research (`municipal_research/`)

County budget documents and municipal data PDFs needed for local government analysis.

---

## File Formats

| Format | Count | Use |
|--------|-------|-----|
| `.md` | 17 | Narrative wishlists with priorities, descriptions, and context |
| `.csv` | 11 | Structured trackers with columns: item, author, priority, status, URL |
| `.json` | 3 | Machine-readable inventories (HDARP processing metadata, API sources) |
| `.html` | 1 | Browser-viewable wishlist page |

---

## Wishlist Evolution (Banking Research)

The banking research wishlists evolved over several months:

| Date | File | Items | Notes |
|------|------|-------|-------|
| 2025-10 | `original_pdf_wishlist.md` | ~100 | Original stress test PDF targets |
| 2025-12 | `pdf_acquisition_wishlist_stress_testing.md` | ~50 | Focused stress testing PDFs |
| 2026-01 | `banking_data_wishlist_v1/v2.md` | 26+25 | Banking data API sources |
| 2026-02-25 | `comprehensive_kb_wishlist_452.csv` | 452 | First comprehensive version |
| 2026-02-27 | `unified_wishlist_407.csv` | 407 | Unified with search queries |
| 2026-03-08 | `kb_wishlist_2026-03-08.csv` | 775 | Expanded with web research |
| **2026-03-29** | **`kb_wishlist_master_2026-03-29.csv`** | **795** | **Definitive — 201 downloaded, 587 needed** |

---

## How to Use

1. **Start with the master**: `banking_research/kb_wishlist_master_2026-03-29.csv` is the definitive list
2. **Check acquisition status**: Filter by `Status` column (DOWNLOADED, NEEDED, PARTIAL)
3. **Prioritize**: CRITICAL > HIGH > MEDIUM > LOW
4. **Find sources**: Each CSV row includes URLs (Anna's Archive, Archive.org, direct links, search queries)
5. **Read the narrative**: `wishlist_narrative_guide.md` explains each of the 45 categories
6. **Queue for HDARP**: Acquired PDFs can be processed using HDARP extraction pipeline

---

## Statistics

- **Total wishlist items**: ~795 in the master list (banking), ~650+ across all domains
- **Domains covered**: 4 (national accounts, banking, political economy, municipal)
- **File count**: 31 catalog files
- **Total size**: ~2.1 MB

---

*Updated 2026-03-30. All internal project references have been replaced with descriptive names.*
