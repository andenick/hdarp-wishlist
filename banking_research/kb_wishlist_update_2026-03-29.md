# Banking Research Wishlist Update & Second-HDARP Review

**Date:** 2026-03-29
**Previous Wishlist:** 2026-03-23 (775 items)
**Previous KB Version:** v6.0 (2,502 documents, declared 100% complete Feb 2026)

---

## 1. Executive Summary

### What's New Since March 23

Since the last wishlist update, two major unprocessed input sets have been identified:

1. **Second-HDARP** (`Inputs/Second-HDARP/`): 394 PDFs across 5 dated subfolders, totaling **15.3 GB**. Acquired Feb 26 -- Mar 8, 2026. **None processed through HDARP.** Contains major banking history texts, Fed oral histories, crisis narratives, academic papers, and classical economics.

2. **BHCF & MDRM Inputs** (`Inputs/2026.03.11 BHCF and MDRM Inputs/`): 144 CSV files totaling **1.3 GB**. Quarterly Bank Holding Company Financial Reports (1986 Q3 -- 2021 Q1) plus MDRM data dictionary (87 MB). **Structured data -- not for HDARP, for direct analysis.**

Neither was documented in `Inputs/README.md` (last updated Feb 24).

### Key Numbers

| Metric | March 23 | March 29 | Delta |
|--------|----------|----------|-------|
| Wishlist total items | 775 | 775 | 0 |
| DOWNLOADED (confirmed in KB) | 142 | 142 | 0 |
| NEEDED | 624 | 624 | 0 |
| PARTIAL | 9 | 9 | 0 |
| Unprocessed PDFs in pipeline | 0 | **394** | +394 |
| KB documents | 2,502 | 2,502 | 0 |

**Bottom line:** The wishlist CSV itself hasn't changed, but 394 PDFs sitting in `Inputs/Second-HDARP/` represent a massive second processing wave that will substantially increase KB coverage and satisfy many NEEDED wishlist items once processed.

---

## 2. Second-HDARP Inventory

### By Subfolder

| Subfolder | PDFs | Size | Content Type |
|-----------|------|------|-------------|
| `2026.02.26 Agent Downloads` | 89 | 360 MB | Historical banking texts (Knox 1900, Bolles 1886, Dewey 1934, Sumner 1896, Catterall 1903, White 1911); FDIC History of the Eighties (20 vols); FDIC Crisis Response 2008 (18 vols); FCIC Report; Fed supervision reviews |
| `2026.02.26 New Input Pdfs` | 56 | 856 MB | Banking/financial crisis academic papers, Forbes interviews, debt markets analysis |
| `2026.03.06 Inputs` | 215 | 6.5 GB | Meltzer *History of the Federal Reserve* (3 vols); Fed Oral History Project interviews (15+); FFIEC form instructions (Y-9C, Y-14); Conti-Brown *Power and Independence of the Fed*; classical economics (Ricardo, Thornton, Bagehot); shadow banking papers |
| `2026.03.08 Pdf Inputs` | 34 | 6.7 GB | Large books: Bernanke *Courage to Act*, Geithner memoirs, Lewis *Liar's Poker*/*Big Short*, Greenspan interviews, Basel Handbook, Banking Research *Keeping at It*, crisis narratives (Barofsky, McDonald, Sorkin analogues) |
| `2026.03.08 Knowledge_Base_Update` | 0 PDFs | 404 KB | Wishlist tracker files (CSV/HTML/XLSX) -- not for HDARP |

### Size Distribution

| Range | Count | % | Notes |
|-------|-------|---|-------|
| < 1 MB | 198 | 50% | Short papers, articles -- no chunking needed |
| 1-10 MB | 96 | 25% | Standard papers/reports -- chunking likely needed |
| 10-100 MB | 51 | 13% | Books and long reports -- mandatory chunking |
| > 100 MB | 49 | 12% | Major digitized books -- heavy chunking required |
| **Total** | **394** | | **15.3 GB** |

---

## 3. Cross-Reference Analysis

### Method
Automated keyword matching of Second-HDARP filenames against (a) 2,521 Knowledge Base directory names and (b) 775 wishlist CSV entries. Note: matching is approximate -- many Second-HDARP PDFs have opaque filenames (e.g., `bailouthowwashin0000baro_1.pdf` = Barofsky's *Bailout*, `bigshortinsidedo0000lewi_1.pdf` = Lewis's *The Big Short*) that defeat simple keyword matching.

### Results

| Category | Count | Description |
|----------|-------|-------------|
| Potential KB overlaps | ~122 | PDFs whose keywords match existing KB entries. **Many are false positives** (e.g., FDIC History of the Eighties 20 volumes all matched to generic "1997_NYFed_Banking_History" on shared words "history" + "banking"). True duplicates likely ~30-50. |
| Wishlist NEEDED now available | 2+ | Confirmed: Warburg *Federal Reserve System* (Row 643). Many more likely hidden in opaque filenames. |
| Wishlist DOWNLOADED confirmed | 22 | Already marked downloaded: Knox, White, Veblen, Battiston, Banking Research, Pozsar, Fed Oral History, FFIEC Y-9C instructions, Treaster, Greider, Lewis |
| New discoveries | ~248 | Not matched to KB or wishlist. Includes Fed oral history interviews, academic papers, and books not yet on the wishlist. **Manual review recommended.** |
| **Genuinely new PDFs** | **~272-344** | After subtracting true duplicates (est. 30-50 from the 122 potential overlaps) |

### Notable Content Identified in Second-HDARP

**Historical Banking Foundations:**
- Knox (1900) *History of Banking in the United States* (4 vols)
- Bolles (1886) *Financial History of the United States* (3 vols)
- Dewey (1934) *Financial History of the United States* (12th ed.)
- Catterall (1903) *Second Bank of the United States*
- FDIC *History of the Eighties* (20 chapters/volumes)
- FDIC *Crisis and Response: 2008* (18 chapters/volumes)

**Federal Reserve History:**
- Meltzer *History of the Federal Reserve* Vol. 1 (1913-1951), Vol. 2 Book 1 (1951-1969), Vol. 2 Book 2 (1970-1986)
- Conti-Brown *Power and Independence of the Federal Reserve* (2016)
- Fed Oral History Project interviews (15+ transcripts: Greenspan, Blinder, Rivlin, Brimmer, Siegman, etc.)
- Greider *Secrets of the Temple*
- Treaster *Paul Banking Research: Making of a Financial Legend*

**Crisis Narratives & Analysis:**
- Bernanke *Courage to Act*, *Firefighting*
- Lewis *Liar's Poker*, *The Big Short*
- Barofsky *Bailout*
- FCIC *Financial Crisis Inquiry Report*
- Basel Handbook (comprehensive guide)

**Academic Papers (2026.03.06 Inputs -- 215 files):**
- Shadow banking papers (Pozsar, Menand, Ricks analogues)
- Financial contagion and network models
- FFIEC form instructions (Y-9C, Y-14A, FR 2052a -- current as of 2025-12)
- Classical economics (Ricardo, Thornton, Bagehot)
- Clearinghouse origins and central banking history

---

## 4. BHCF & MDRM Inputs (Non-HDARP)

**Location:** `Inputs/2026.03.11 BHCF and MDRM Inputs/`
**Size:** 1.3 GB across 144 files

| Content | Files | Coverage |
|---------|-------|----------|
| BHCF quarterly reports (CSV) | ~141 | 1986 Q3 -- 2021 Q1 (35 years, quarterly) |
| MDRM data dictionary | 1 CSV (87 MB) | Machine-readable metadata for all regulatory fields |
| MDRM README | 1 TXT | Column headers and format documentation |

**Significance for Dissertation:** These are the raw FR Y-9C data files needed for **Method 1** (Shaikh's real competition empirical test on banking microdata). Combined with the existing `2026.01 FFIEC Bulk Downloads/` (111 BHCF files, 2000-2019), coverage extends from 1986 to 2021 -- a 35-year panel.

**Note:** Duplicate MDRM files exist in 3 locations:
1. `2026.03.11 BHCF and MDRM Inputs/MDRM/MDRM_CSV.csv` (primary, most current)
2. `2026.01.29 filing inputs/MDRM/MDRM_CSV.csv`
3. `2026.01 FFIEC Bulk Downloads/MDRM_CSV.csv`

---

## 5. Wishlist Status Assessment

### Current Priority Distribution (Unchanged from March 23)

| Priority | NEEDED | PARTIAL | DOWNLOADED | Total |
|----------|--------|---------|------------|-------|
| CRITICAL | 68 | 0 | 5 | 73 |
| HIGH | 329 | 7 | 5 | 341 |
| MEDIUM | 210 | 2 | 7 | 219 |
| LOW | 9 | 0 | 0 | 9 |
| (unlabeled) | 8 | 0 | 125 | 133 |
| **Total** | **624** | **9** | **142** | **775** |

### Items from March 23 Wishlist Still Pending

**CRITICAL NEEDED (from March 23 update):**

| Row | Author | Title | In Second-HDARP? |
|-----|--------|-------|-----------------|
| 754 | Kindleberger | *Manias, Panics, and Crashes* | Likely (check opaque filenames) |
| 755 | Bernanke | "Nonmonetary Effects of the Financial Crisis" (1983) | Likely in 2026.03.06 |
| 756 | Goodwin | "A Growth Cycle" (1967) | Unknown |
| 757 | Minsky | "FIH: An Interpretation of Keynes" (1977 Nebraska) | Unknown |
| 760 | Tarullo | Stress testing dynamism vs. predictability WP (2024) | Unknown |

**HDARP Enrichment Candidates (7 existing KB entries, from March 23):**

| KB Entry | Priority | Status |
|----------|----------|--------|
| BPI Stress Testing Response (2024) | CRITICAL | Not enriched |
| Minsky Financial Instability Revisited (91pp) | HIGH | Not enriched |
| Gorton Banking Panics (1988) | HIGH | Not enriched |
| Calomiris & Gorton Origins of Banking Panics (1991) | HIGH | Not enriched |
| Mehrling Minsky-Kindleberger Connection (2023) | HIGH | Not enriched |
| Avgouleas/Goodhart Living Wills (2010) | MEDIUM | Not enriched |
| Minsky WP74 (1992) | MEDIUM | Not enriched |

---

## 6. HDARP Processing Plan for Second-HDARP

### Recommended Approach

The 394 PDFs should be processed in **priority waves** rather than all at once:

#### Wave 1: Dissertation-Critical (Priority: Immediate)
- **Target:** PDFs matching CRITICAL and HIGH wishlist items
- **Estimated count:** ~50-80 PDFs
- **Action:** Manual triage of Second-HDARP against CRITICAL wishlist items, then `/preparehdarp` + `/sphdarp`

#### Wave 2: Historical Banking Foundations
- **Target:** `2026.02.26 Agent Downloads/` (89 PDFs, 360 MB)
- **Content:** Knox, Bolles, Dewey, FDIC histories
- **Note:** FDIC History of the Eighties (20 vols) and Crisis Response (18 vols) are multi-volume -- treat each volume as separate document

#### Wave 3: Fed History & Oral Histories
- **Target:** Meltzer volumes, Conti-Brown, Fed Oral History interviews from `2026.03.06 Inputs/`
- **Estimated count:** ~30-40 PDFs
- **Note:** Meltzer volumes are very large (100-300 MB each) -- heavy chunking required

#### Wave 4: Academic Papers & Remaining
- **Target:** Remaining academic papers from `2026.03.06 Inputs/` and `2026.02.26 New Input Pdfs/`
- **Estimated count:** ~200+ PDFs
- **Note:** Many are small (<1 MB) and can be batch-processed quickly

#### Wave 5: Large Books
- **Target:** `2026.03.08 Pdf Inputs/` (34 PDFs, 6.7 GB)
- **Note:** These are mostly 100+ MB digitized books -- each needs density-aware chunking via `pdf_splitter_orchestrator.py`

### Pre-Processing Checklist
1. **Deduplicate:** Remove confirmed duplicates against existing KB (~30-50 files)
2. **Rename opaque files:** Many `2026.03.08 Pdf Inputs/` files have archive.org hash names -- rename for clarity before processing
3. **Run `/preparehdarp`** on each wave to chunk PDFs >10 pages or >1 MB
4. **Process with `/sphdarp N`** (Smart Parallel HDARP with batch sizing)

### Also Process: 7 KB Enrichment Candidates
Run `/enrichhdarp` on the 7 existing KB entries flagged in the March 23 wishlist (BPI, Minsky, Gorton, Calomiris/Gorton, Mehrling, Avgouleas/Goodhart, Minsky WP74). These are already in the KB but lack enrichment metadata.

---

## 7. Documentation Updates Needed

| File | Update | Status |
|------|--------|--------|
| `Inputs/README.md` | Add Second-HDARP and BHCF/MDRM sections | **Done this session** |
| `Handoffs/CURRENT_STATUS.md` | Add March 29 activity entry | **Done this session** |
| Wishlist CSV | No changes needed yet -- update after Second-HDARP processing | Pending |

---

## 8. Recommended Next Actions

1. **Manual triage of Second-HDARP** (1-2 hours): Review the 248 "new discovery" PDFs against wishlist by opening folders and checking titles. Many opaque filenames hide known wishlist items.

2. **Begin Wave 1 processing**: Identify ~50-80 dissertation-critical PDFs, run `/preparehdarp`, then `/sphdarp`.

3. **Run `/enrichhdarp audit`** on existing KB to check quality of the 7 enrichment candidates.

4. **Reconcile BHCF data**: Merge `2026.03.11 BHCF and MDRM Inputs/` with `2026.01 FFIEC Bulk Downloads/` to build complete 1986-2021 panel for Method 1.

5. **Update wishlist CSV** after Wave 1 processing to move items from NEEDED to DOWNLOADED.

---

*Generated 2026-03-29 by Claude (Banking Research /readystart session)*
