# Reports — RG Faith Miroli Inventory System

This document defines all analytical and printable reports in the system. These are separate from the operational screens (lists, forms, dashboards) defined in each module PRD. Operational screens answer "what do I need to do next?" — reports answer "what happened, how are we performing, and where should we focus?"

Reports are available to the Facility Manager, Supervisor, and Head Office User. All reports support date range filtering, export to CSV/PDF, and printing.

---

## Report Categories

| Category | Audience | Purpose |
|---|---|---|
| **System-wide** | Manager, Head Office | Cross-module views spanning the entire material lifecycle |
| **Vendor** | Manager, Head Office | Vendor inbound volumes, quality performance, pending greige |
| **Processing** | Manager, Supervisor | Folding shrinkage, classification distribution, gradation yields |
| **Packing & Output** | Manager, Head Office | Thaan logging, bale production, packing program performance |
| **Dispatch** | Manager, Head Office | Scheduled pickups, shipment volumes, customer-wise delivery history |
| **Exception** | Manager | Decision Pending aging (classification uncertainty), Not Acceptable aging, Todiya candidates |
| **Packaging Materials** | Manager, Supervisor | DEFERRED — packaging stock, consumption, GRN history |

---

## System-wide Reports

### R01 — Stage-wise Inventory Report

**Question:** "How much material is at each stage right now?"

| Field | Description |
|---|---|
| **Type** | Dashboard + drillable report |
| **Audience** | Manager, Head Office |
| **Frequency** | Real-time (viewed daily, start of shift) |

**Content:**

| Stage | Metric | Source |
|---|---|---|
| Received (unprocessed) | Total metres at MIROLI-RECEIVED | `fabric_inventory` (state = RECEIVED) |
| Folded (pending classification) | Total metres folded but not yet classified | `fabric_inventory` (state = FOLDED) |
| Classified (awaiting program) | Total metres at MIROLI-CLASSIFIED | `fabric_inventory` (state = CLASSIFIED) |
| Program Assigned (in packing) | Total metres allocated to packing programs | `fabric_inventory` (state = PROGRAM_ASSIGNED) |
| Packed (awaiting dispatch) | Total bales + metres at MIROLI-FG-OUT | `bales` (status = PACKED) |
| Todiya Candidates (bales with non-Fresh thaans) | Count of bales + total non-Fresh thaan metres/kg | `bales` (status = PACKED, containing non-Fresh thaans) |
| Decision Pending | Total metres in DECISION_PENDING state | `fabric_inventory` (state = DECISION_PENDING) |
| Not Acceptable | Total metres at MIROLI-NA | `fabric_inventory` (state = NOT_ACCEPTABLE) |

**Drill-down:** Each row links to the relevant module's list screen (e.g., clicking "Received" opens the Pending Folding list).

---

### R02 — MRL Lifecycle Report

**Question:** "Show me the complete history of MRL #526 from first receipt to dispatch."

| Field | Description |
|---|---|
| **Type** | Detail report (single MRL) |
| **Audience** | Manager, Supervisor, Head Office |
| **Input** | MRL number |

**Content:**

| Section | Fields |
|---|---|
| **Header** | MRL number, vendor, quality code, date of first inbound receipt |
| **Inbound Receipts** | List of all receipts: avak date, lot number, received metres (vendor-reported), roll count, Gate Pass reference |
| **Folding** | Per-roll folding metres, shrinkage vs received metres, fold type |
| **Chadat** | Chadat value, date recorded |
| **Classification** | Tone and finish assigned per roll/lot, classification date, Decision Pending entries (if any) |
| **Gradation** | Grade breakdown from packing execution: Fresh, Good Cut, Fent, Rags, Chindi, NA — with metres and kg as applicable |
| **Thaans** | List of thaans cut from this MRL's rolls: thaan ID, grade, metres, source roll, bale assignment |
| **Packing Programs** | Programs using rolls from this MRL: program number, customer, bales planned/actual |
| **Bales Produced** | Bale numbers, brand, product, customer, metres, thaan count |
| **Dispatch** | Delivery form numbers, pickup scheduled dates, dispatch dates, customer |
| **Exceptions** | Decision Pending entries (classification uncertainty), Not Acceptable entries with status |
| **Event Timeline** | Full chronological event log from `INBOUND_RECEIVED` to `DELIVERY_DISPATCHED` |

---

### R03 — Monthly Throughput Report

**Question:** "What was our total processing output this month?"

| Field | Description |
|---|---|
| **Type** | Summary report with period filter |
| **Audience** | Manager, Head Office |
| **Filters** | Date range (default: current month) |

**Content:**

| Metric | Value | Source |
|---|---|---|
| Inbound receipts | Count + total metres | `inbound_receipts` |
| Lots folded | Count + total metres | `folding_records` |
| Lots classified | Count | `classification_records` |
| Average Fresh yield % | Percentage | `gradation_reports` |
| Thaans logged | Count + total metres | `thaans` |
| Non-Fresh thaans logged (embedded gradation) | Count + total metres/kg by grade | `thaans` (grade != FRESH) |
| Packing programs completed | Count | `packing_programs` (status = COMPLETED) |
| Bales packed | Count + total metres | `bales` |
| Bales dispatched | Count + total metres | `delivery_forms` |
| Delivery forms created | Count | `delivery_forms` |

---

### R04 — End-to-End Cycle Time Report

**Question:** "How long does it take from inbound receipt to dispatch?"

| Field | Description |
|---|---|
| **Type** | Analytical report |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, vendor |

**Content:**

| Metric | Calculation |
|---|---|
| Receipt to Folding complete | Time between `INBOUND_RECEIVED` and `FOLDING_COMPLETED` |
| Receipt to Classification | Time between `INBOUND_RECEIVED` and `CLASSIFICATION_RECORDED` |
| Classification to Packing program | Time between `CLASSIFICATION_RECORDED` and `PACKING_PROGRAM_CREATED` |
| Packing program to First thaan logged | Time between `PACKING_PROGRAM_CREATED` and first `THAAN_LOGGED` |
| Packing program to All bales packed | Time between `PACKING_PROGRAM_CREATED` and last `BALE_REGISTERED` |
| Packing to Dispatch | Time between `BALE_REGISTERED` and `DELIVERY_DISPATCHED` |
| **Total: Receipt to Dispatch** | End-to-end time |

Shown as: average, median, min, max for the selected period. Optionally broken down by vendor or lot.

---

## Vendor Reports

### R05 — Vendor-Reported Greige Pending

**Question:** "What greige material is reportedly pending at each vendor?"

| Field | Description |
|---|---|
| **Type** | Informational summary |
| **Audience** | Manager, Head Office |
| **Filters** | Vendor (optional) |

**Content:**

| Column | Description |
|---|---|
| Vendor | Mill name |
| Reported greige metres | Vendor-reported pending greige from Gate Pass notes and vendor communications |
| Last updated | Date of most recent vendor communication or Gate Pass note |
| Notes | Free-text remarks from Gate Pass or manual entry |

Note: This is an informational report only. The system does not track outbound sending of grey cloth to vendors. Greige pending figures are based on vendor-reported data captured in Gate Pass notes, not computed from system balances.

---

### R06 — Vendor-wise Inbound Summary

**Question:** "How much did we receive from each vendor this month?"

| Field | Description |
|---|---|
| **Type** | Period summary |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, vendor |

**Content:**

| Column | Description |
|---|---|
| Vendor | Mill name |
| MRLs created | Count of MRLs with first receipt in period |
| Receipts recorded | Count received in period |
| Total metres received | Sum of received metres |
| Total rolls received | Sum of rolls across all receipts |
| Average lot size (metres) | Average metres per MRL |

---

### R07 — Vendor Quality Performance Report

**Question:** "Which vendors have the highest rejection rates?"

| Field | Description |
|---|---|
| **Type** | Analytical report |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, vendor |

**Content:**

| Column | Description |
|---|---|
| Vendor | Mill name |
| Total metres received | From inbound receipts |
| Fresh metres | Sum of Fresh gradation for vendor's lots (from `gradation_reports`, Module 05) |
| Fresh yield % | Percentage |
| Not Acceptable metres | Sum of NA thaans logged during packing for vendor's lots |
| NA rate % | Percentage |
| Open NA entries | Count still unresolved |
| Average shrinkage % | From folding records for vendor's lots |

Note: Quality data is sourced from gradation reports generated during packing execution (Module 05), not from a separate grading step.

---

## Processing Reports

### R08 — Shrinkage Report

**Question:** "What is the shrinkage across all lots, and are any vendors consistently worse?"

| Field | Description |
|---|---|
| **Type** | List + summary |
| **Audience** | Manager, Supervisor |
| **Filters** | Date range, vendor, MRL |

**Content:**

| Column | Description |
|---|---|
| MRL Number | Lot identifier |
| Vendor | Source mill |
| Received metres | Vendor-reported (from Gate Pass) |
| Folding metres | RG Faith-measured (per-roll) |
| Shrinkage metres | Difference |
| Shrinkage % | Percentage |

**Summary row:** Average shrinkage % for the filtered period. Optional vendor grouping.

---

### R09 — Gradation Report (Printable)

**Question:** "Print the full Gradation Report for MRL #526."

| Field | Description |
|---|---|
| **Type** | Printable detail report (single MRL) |
| **Audience** | Manager, Supervisor, Head Office |
| **Input** | MRL number |
| **Module** | Packing Program (Module 05) |

**Content:** This is the printable version of the Gradation Report. Gradation data is generated progressively during packing execution as thaans are logged with their grades.

**Metre Progression:**
```
Received metres (Gate Pass):    5,826.00
Folding metres (RG Faith):     5,644.33
Total graded metres (thaans):  5,644.33
```

**Grade Breakdown:**

| Grade | Kg | Metres | % of Graded | Loss Factor | Loss % |
|---|---|---|---|---|---|
| Fresh | -- | 5,470.02 | 96.91% | 0% | 0% |
| Good Cut | -- | 52.00 | 0.92% | 0% | -- |
| Fent | 11.46 | 64.44 | 1.14% | 50% | 0.58% |
| Rags | 1.15 | 6.48 | 0.15% | 0% | -- |
| Chindi | 2.00 | 16.82 | 0.35% | 100% | 0.35% |
| Not Acceptable | -- | 0.00 | 0.00% | -- | -- |
| **Total** | | **5,644.32** | **100%** | | |

Note: Fresh, Good Cut, and Not Acceptable are measured directly in metres. Fent, Rags, and Chindi are measured in kg and converted to metres via Chadat. Grade data comes from thaan logging during packing execution (Module 05). The report is updated progressively as each thaan is logged.

**Metadata:** MRL number, vendor, lot number, quality code, Chadat, folding date, gradation progress (% of lot graded).

---

### R10 — Fresh Yield Trend Report

**Question:** "What is our Fresh yield trend over the past 3/6/12 months?"

| Field | Description |
|---|---|
| **Type** | Trend chart + table |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, vendor |

**Content:**

| Column | Description |
|---|---|
| Period (week/month) | Time bucket |
| Lots with gradation data | Count |
| Total metres graded (from thaans) | Sum |
| Fresh metres | Sum |
| Fresh yield % | Percentage |
| Non-Fresh breakdown | Good Cut %, Fent %, Rags %, Chindi %, NA % |

Visualised as a line chart (Fresh yield % over time) with a table below.

Note: Gradation data is sourced from `THAAN_LOGGED` events during packing execution (Module 05).

---

### R24 — Classification Summary Report

**Question:** "What is the tone and finish distribution across classified material?"

| Field | Description |
|---|---|
| **Type** | Summary + detail |
| **Audience** | Manager, Head Office |
| **Module** | Tone & Finish Classification (Module 04) |
| **Filters** | Date range, vendor, tone code, finish |

**Content:**

**Summary:**

| Column | Description |
|---|---|
| Tone Code | Assigned tone (e.g., O1W) |
| Finish | Assigned finish attribute |
| Roll Count | Number of rolls with this tone/finish combination |
| Total Metres | Sum of metres for this tone/finish combination |
| % of Total | Proportion of all classified material |

**Detail (per roll):**

| Column | Description |
|---|---|
| MRL Number | Source MRL |
| Roll Number | Individual roll |
| Vendor | Source mill |
| Tone Code | Assigned tone |
| Finish | Assigned finish |
| Metres | Roll metres |
| Classification Date | When classified |

**Drill-down:** Click tone/finish row to see individual rolls.

---

### R25 — Thaan Register

**Question:** "Show me all thaans logged, with their grades, source rolls, and bale assignments."

| Field | Description |
|---|---|
| **Type** | List report |
| **Audience** | Manager, Supervisor |
| **Module** | Packing Program (Module 05) |
| **Filters** | Date range, MRL, grade, packing program, bale number |

**Content:**

| Column | Description |
|---|---|
| Thaan ID | System-generated identifier |
| MRL Number | Source MRL |
| Roll Number | Source roll (the roll from which this thaan was cut) |
| Grade | Fresh / Good Cut / Fent / Rags / Chindi / Not Acceptable |
| Metres | Thaan length in metres (for Fresh, Good Cut, NA) |
| Kg | Thaan weight in kg (for Fent, Rags, Chindi) |
| Packing Program | Program under which this thaan was logged |
| Bale Number | Bale this thaan was assembled into (if assigned) |
| Logged Date | When the thaan was logged (`THAAN_LOGGED` event) |
| Logged By | User who logged the thaan |

**Summary row:** Total thaans, total metres, total kg, breakdown by grade.

**Grouping options:** By MRL, by packing program, by grade, by bale.

---

## Packing & Output Reports

### R11 — Bale Production Report

**Question:** "How many bales did we pack this day/week/month?"

| Field | Description |
|---|---|
| **Type** | Summary + detail |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, brand, product, customer |

**Summary:**

| Metric | Value |
|---|---|
| Total bales packed | Count |
| Total metres packed | Sum |
| Total thaans packed | Sum |
| Programs completed | Count |
| Programs in progress | Count |

**Detail (per bale):**

| Column | Description |
|---|---|
| Bale Number | Running serial |
| Packing Date | When packed |
| Brand | Brand stamp |
| Product | Product name |
| Trade Number | SKU |
| Customer (Haste) | Destination |
| Thaan Count | Number of thaans in this bale |
| Pieces | Per bale |
| Metres | Per bale |
| Source MRLs | MRL numbers contributing rolls to this bale (supports cross-lot packing) |
| Program Number | Source packing program |

---

### R12 — Non-Fresh Thaan Report

**Question:** "What non-Fresh thaans have been logged during packing, and what is the trend?"

| Field | Description |
|---|---|
| **Type** | Summary + trend |
| **Audience** | Manager |
| **Filters** | Date range, MRL, grade |

**Content:**

| Column | Description |
|---|---|
| Packing Program | Program number |
| Source MRLs | MRL numbers (supports cross-lot) |
| Thaan ID | Individual thaan identifier |
| Grade | Good Cut / Fent / Rags / Chindi / Not Acceptable |
| Metres | Thaan metres (for Good Cut, NA) |
| Kg | Thaan weight (for Fent, Rags, Chindi) |
| Bale Number | Bale the thaan was packed into |
| Logged Date | When the thaan was logged |

**Summary:** Total non-Fresh thaans by grade for the period. Trend line showing non-Fresh thaan volume over time.

Note: Non-Fresh thaans logged during packing are the equivalent of what was previously tracked as "cutting waste." There is no separate waste concept — grading is embedded in the thaan logging step during packing execution.

---

### R13 — Packing Program Summary Report

**Question:** "Show me the full summary of packing program PP-2026-0087."

| Field | Description |
|---|---|
| **Type** | Printable detail report (single program) |
| **Audience** | Manager, Supervisor |
| **Input** | Program number |

**Content:**

| Section | Fields |
|---|---|
| **Header** | Program number, type (Regular/Todiya), date, quality, tone, width, Chadat |
| **Source Rolls** | List of rolls allocated to this program: MRL number, roll number, metres (supports cross-lot packing) |
| **Line Items** | Per line: brand, product, trade number, fold type, customer, cut length, pieces/bale, planned bales, actual bales, planned metres, actual metres |
| **Thaans Logged** | Per thaan: thaan ID, source roll, grade, metres/kg, bale assignment |
| **Gradation Summary** | Grade breakdown from thaans logged: Fresh metres, Good Cut metres, Fent kg, Rags kg, Chindi kg, NA metres, with percentages |
| **Bales Produced** | Bale number, packing date, thaan count, pieces, metres, packing slip reference |
| **Status** | Current status, completion date |

---

## Dispatch Reports

### R14 — Dispatch Register

**Question:** "List all dispatches for this period."

| Field | Description |
|---|---|
| **Type** | List report |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, customer, status (Pickup Scheduled / Dispatched) |

**Content:**

| Column | Description |
|---|---|
| Delivery Form No | Serial number |
| Customer (Haste) | Who receives the goods |
| Total Bales | Count per delivery |
| Total Metres | Sum per delivery |
| Total Pieces | Sum per delivery |
| Pickup Scheduled Date | Date pickup was scheduled (`PICKUP_SCHEDULED` status) |
| Dispatch Date | Actual dispatch date (`DISPATCHED` status) |
| Status | PICKUP_SCHEDULED / DISPATCHED |

**Summary row:** Total bales, metres, pieces for filtered period. Separate totals for scheduled vs. dispatched.

Note: Dispatch follows a two-step process. Delivery forms first move to PICKUP_SCHEDULED (vendor confirms readiness, RG Faith schedules vehicle), then to DISPATCHED when the vehicle departs.

---

### R15 — Customer-wise Dispatch Report

**Question:** "How much did we ship to customer X this month/quarter/year?"

| Field | Description |
|---|---|
| **Type** | Summary grouped by customer |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, customer |

**Content:**

| Column | Description |
|---|---|
| Customer (Haste) | Party name |
| Delivery Forms | Count (dispatched only) |
| Total Bales | Sum |
| Total Metres | Sum |
| Products shipped | List of distinct products |
| Pending Pickups | Count of delivery forms at PICKUP_SCHEDULED status |
| Last dispatch date | Most recent `DELIVERY_DISPATCHED` event |

**Drill-down:** Click customer to see individual delivery forms.

---

### R16 — Delivery Form (Printable)

**Question:** "Print Delivery Form DF-2026-0890."

| Field | Description |
|---|---|
| **Type** | Printable document |
| **Audience** | Manager, Supervisor |
| **Input** | Delivery form number |

**Content:** Matches the physical Delivery Form format.

| Section | Fields |
|---|---|
| **Header** | Delivery Form No, Date, From (RG Faith Creations), Godown (Miroli), Haste (Customer) |
| **Status** | Current status: PICKUP_SCHEDULED or DISPATCHED, with dates for each step |
| **Line Items** | Bale No, Lot No, Trade No, Pieces, Metres |
| **Footer** | Total bales, total metres, signature lines |

---

## Exception Reports

### R17 — Decision Pending Aging Report

**Question:** "What Decision Pending entries are overdue for review?"

| Field | Description |
|---|---|
| **Type** | List with aging buckets |
| **Audience** | Manager |
| **Filters** | Status (Pending only), age threshold |

**Content:**

| Column | Description |
|---|---|
| MRL Number | Lot identifier |
| Roll / Lot Number | Specific roll or vendor lot |
| Metres | Pending decision |
| Classification Issue | Why tone/finish classification is uncertain |
| Created Date | When `DECISION_PENDING_CREATED` event was recorded |
| Comments | History of `DECISION_PENDING_COMMENTED` entries |
| Days Since Last Activity | Aging indicator |
| Status Flag | Green (< 7 days), Yellow (7-13 days), Red (14+ days) |

Note: Decision Pending is now for classification uncertainty — material where tone and/or finish cannot be confidently assigned. It is no longer related to quality grading. Resolved via `DECISION_PENDING_RESOLVED` event.

---

### R18 — Not Acceptable Aging Report

**Question:** "What rejected material has been sitting the longest?"

| Field | Description |
|---|---|
| **Type** | List with aging buckets |
| **Audience** | Manager |
| **Filters** | Status (Open/In Discussion), vendor, age |

**Content:**

| Column | Description |
|---|---|
| Entry Number | NA entry ID |
| MRL Number | Source MRL |
| Vendor | Which mill |
| Metres | Rejected amount |
| Remark | Rejection reason |
| Created Date | When thaan was logged as NA during packing execution (Module 05) |
| Days Open | Total age |
| Last Activity | Most recent comment date |
| Status | Open / In Discussion |

**Summary:** Grouped by vendor, showing total pending metres per vendor.

Note: Not Acceptable material is identified during packing execution (Module 05) when a thaan is logged with grade = Not Acceptable, not during a separate grading step.

---

### R19 — NA Resolution History Report

**Question:** "How are rejections getting resolved, and how long does it take?"

| Field | Description |
|---|---|
| **Type** | Analytical report |
| **Audience** | Manager, Head Office |
| **Filters** | Date range (resolved date), vendor |

**Content:**

| Column | Description |
|---|---|
| Entry Number | NA entry ID |
| MRL Number | Source MRL |
| Vendor | Which mill |
| Metres | Amount |
| Created Date | When NA thaan was logged during packing (Module 05) |
| Resolved Date | When closed |
| Days to Resolve | Duration |
| Resolution Type | Vendor Pickup / Unresolved |

**Summary:** Average resolution time, % resolved via pickup vs. unresolved, by vendor.

---

### R20 — Todiya Candidate Report

**Question:** "What bales contain non-Fresh thaans and are available for Todiya?"

| Field | Description |
|---|---|
| **Type** | List report |
| **Audience** | Manager |
| **Filters** | Grade, MRL, date range (bale creation) |

**Content:**

| Column | Description |
|---|---|
| Bale Number | Bale containing non-Fresh thaans |
| Packing Program | Program that created this bale |
| Source MRLs | MRL numbers contributing to this bale |
| Bale Status | PACKED (only PACKED bales are Todiya candidates) |
| Non-Fresh Thaan Count | Number of non-Fresh thaans in this bale |
| Grade Breakdown | Count and metres/kg by grade: Good Cut (m), Fent (kg), Rags (kg), Chindi (kg) |
| Bale Creation Date | When bale was registered |
| Days Since Packed | Aging indicator |

**Summary:** Total Todiya candidate bales, total non-Fresh thaans, breakdown by grade.

Note: Todiya is an unpack-and-repack operation. Candidate bales at PACKED status containing non-Fresh thaans can be unpacked (`BALE_UNPACKED`), thaans selected, and repacked into new Todiya bales (`TODIYA_BALE_REGISTERED`). There is no separate accumulation running balance — the bales themselves are the inventory.

---

## Packaging Materials Reports

> **STATUS: DEFERRED** — All packaging materials reports (R21, R22, R23) are deferred to a future phase. The definitions below are retained for reference but will not be implemented in the initial build.

### R21 — Packaging Stock Report [DEFERRED]

**Question:** "What is the current stock of all packaging items?"

| Field | Description |
|---|---|
| **Type** | List report |
| **Audience** | Manager, Supervisor |
| **Status** | DEFERRED |

**Content:**

| Column | Description |
|---|---|
| SKU Code | Item identifier |
| Item Name | Description |
| Type | Consumable / Reusable |
| UOM | Unit of measure |
| Current Stock | Running balance |
| Last Received | Date of most recent GRN |
| Last Consumed | Date of most recent consumption |
| Status | Low stock warning if below threshold |

---

### R22 — Packaging GRN Register [DEFERRED]

**Question:** "What packaging materials did we receive this month?"

| Field | Description |
|---|---|
| **Type** | List report |
| **Audience** | Manager |
| **Filters** | Date range, vendor, SKU |
| **Status** | DEFERRED |

**Content:**

| Column | Description |
|---|---|
| GRN Number | Receipt ID |
| Date | Receipt date |
| SKU | Item name |
| Vendor | Supplier |
| Quantity | Amount received |
| UOM | Unit |
| Vendor Reference | Invoice number |

---

### R23 — Packaging Consumption Report [DEFERRED]

**Question:** "How much packaging material are we consuming, and for which programs?"

| Field | Description |
|---|---|
| **Type** | Summary + detail |
| **Audience** | Manager |
| **Filters** | Date range, SKU, packing program |
| **Status** | DEFERRED |

**Content:**

| Column | Description |
|---|---|
| SKU | Item name |
| Total Consumed | Sum for period |
| UOM | Unit |
| Programs Linked | Count of packing programs using this item |
| Average per Bale | Total consumed / bales packed in period (estimate) |

---

## Report Summary

| # | Report Name | Category | Type | Primary Audience | Status |
|---|---|---|---|---|---|
| R01 | Stage-wise Inventory | System-wide | Dashboard | Manager, Head Office | Active |
| R02 | MRL Lifecycle | System-wide | Detail | Manager, Head Office | Active |
| R03 | Monthly Throughput | System-wide | Summary | Manager, Head Office | Active |
| R04 | End-to-End Cycle Time | System-wide | Analytical | Manager, Head Office | Active |
| R05 | Vendor-Reported Greige Pending | Vendor | Informational | Manager, Head Office | Active |
| R06 | Vendor-wise Inbound Summary | Vendor | Period summary | Manager, Head Office | Active |
| R07 | Vendor Quality Performance | Vendor | Analytical | Manager, Head Office | Active |
| R08 | Shrinkage Report | Processing | List + summary | Manager, Supervisor | Active |
| R09 | Gradation Report (Printable) | Processing | Printable | Manager, Supervisor, Head Office | Active |
| R10 | Fresh Yield Trend | Processing | Trend | Manager, Head Office | Active |
| R11 | Bale Production Report | Packing & Output | Summary + detail | Manager, Head Office | Active |
| R12 | Non-Fresh Thaan Report | Packing & Output | Summary + trend | Manager | Active |
| R13 | Packing Program Summary | Packing & Output | Printable | Manager, Supervisor | Active |
| R14 | Dispatch Register | Dispatch | List | Manager, Head Office | Active |
| R15 | Customer-wise Dispatch | Dispatch | Summary | Manager, Head Office | Active |
| R16 | Delivery Form (Printable) | Dispatch | Printable | Manager, Supervisor | Active |
| R17 | Decision Pending Aging | Exception | List + aging | Manager | Active |
| R18 | Not Acceptable Aging | Exception | List + aging | Manager | Active |
| R19 | NA Resolution History | Exception | Analytical | Manager, Head Office | Active |
| R20 | Todiya Candidate Report | Exception | List | Manager | Active |
| R21 | Packaging Stock Report | Packaging | List | Manager, Supervisor | DEFERRED |
| R22 | Packaging GRN Register | Packaging | List | Manager | DEFERRED |
| R23 | Packaging Consumption | Packaging | Summary + detail | Manager | DEFERRED |
| R24 | Classification Summary | Processing | Summary + detail | Manager, Head Office | Active |
| R25 | Thaan Register | Packing & Output | List | Manager, Supervisor | Active |
