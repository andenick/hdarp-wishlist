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
│   ├── comprehensive_literature_wishlist.md  # 332 items across 20 research topics
│   ├── banking_data_wishlist_v1.md # 26 banking data expansion items
│   ├── banking_data_wishlist_v2.md # 25 new data source items (V2)
│   ├── wishlist_status_tracker_v1.csv  # Status tracker for V1 items
│   ├── wishlist_status_tracker_v2.csv  # Status tracker for V2 items
│   ├── comprehensive_wishlist_catalog.csv  # 180+ items — master acquisition catalog
│   └── deprecated_data_wishlist.md # Older wishlist (historical reference)
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

Wishlists covering banking sector literature, regulatory documents, and data sources for stress testing, financial stability, and systemic risk research.

**Key files:**
- `comprehensive_literature_wishlist.md` — the largest single wishlist (332 items, 20 topic sections, prioritized by CRITICAL/HIGH/MEDIUM/LOW)
- `comprehensive_wishlist_catalog.csv` — master CSV with acquisition statuses
- `banking_data_wishlist_v2.md` — data API sources (FFIEC UBPR, Fed CCAR, OECD banking, etc.)

### Political Economy (`political_economy/`)

Online data source wishlists for extending heterodox economics replication work — BEA, FRED, and BLS API sources needed to bridge historical book data (1948-1989) to the present.

### Municipal Research (`municipal_research/`)

County budget documents and municipal data PDFs needed for local government analysis.

---

## File Formats

| Format | Count | Use |
|--------|-------|-----|
| `.md` | 9 | Narrative wishlists with priorities, descriptions, and context |
| `.csv` | 6 | Structured trackers with columns: item, author, priority, status, URL |
| `.json` | 3 | Machine-readable inventories (HDARP processing metadata, API sources) |

---

## How to Use

1. **Find what you need**: Browse by domain folder, or search across all files for specific authors/topics
2. **Check acquisition status**: Most files include status columns (ACQUIRED, NEEDED, PENDING, etc.)
3. **Prioritize**: Files use CRITICAL/HIGH/MEDIUM/LOW or P1-P5 priority schemes
4. **Download sources**: URLs are provided where available (NBER, JSTOR, BEA, BLS, FRED, etc.)
5. **Queue for HDARP**: Acquired PDFs can be processed using HDARP extraction pipeline

---

## Statistics

- **Total wishlist items**: ~650+ across all files
- **Domains covered**: 4 (national accounts, banking, political economy, municipal)
- **File count**: 18 catalog files
- **Total size**: ~330 KB

---

*Generated 2026-03-30. All internal project references have been replaced with descriptive names.*
