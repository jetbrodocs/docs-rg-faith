# Reports — RG Faith Miroli Inventory System

This document defines all analytical and printable reports in the system. These are separate from the operational screens (lists, forms, dashboards) defined in each module PRD. Operational screens answer "what do I need to do next?" — reports answer "what happened, how are we performing, and where should we focus?"

Reports are available to the Facility Manager, Supervisor, and Head Office User. All reports support date range filtering, export to CSV/PDF, and printing.

---

## Report Categories

| Category | Audience | Purpose |
|---|---|---|
| **System-wide** | Manager, Head Office | Cross-module views spanning the entire material lifecycle |
| **Vendor** | Manager, Head Office | Vendor performance, pending balances, rejection rates |
| **Processing** | Manager, Supervisor | Folding shrinkage, grading yields, processing throughput |
| **Packing & Output** | Manager, Head Office | Bale production, packing program performance, waste analysis |
| **Dispatch** | Manager, Head Office | Shipment volumes, customer-wise delivery history |
| **Exception** | Manager | Decision Pending aging, Not Acceptable aging, accumulation trends |
| **Packaging Materials** | Manager, Supervisor | Packaging stock, consumption, GRN history |

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
| Sent to Vendor | Total metres outstanding at all vendors | `mrls` (status != FULLY_RECEIVED) |
| Grey (received, unprocessed) | Total metres at MIROLI-GREY | `fabric_inventory` (state = GREY) |
| Folded (pending grading) | Total metres folded but not yet graded | `fabric_inventory` (state = FOLDED) |
| Graded — Fresh (available) | Total metres at MIROLI-FRESH | `fabric_inventory` (state = GRADED_FRESH) |
| Program Assigned (in cutting) | Total metres allocated to packing programs | `fabric_inventory` (state = PROGRAM_ASSIGNED) |
| Packed (awaiting dispatch) | Total bales + metres at MIROLI-FG-OUT | `bales` (status = PACKED) |
| Accumulated (Todiya stock) | Total kg by grade at MIROLI-ACCUM | `accumulation_stock` |
| Decision Pending | Total metres in DECISION_PENDING state | `fabric_inventory` (state = DECISION_PENDING) |
| Not Acceptable | Total metres at MIROLI-NA | `fabric_inventory` (state = NOT_ACCEPTABLE) |

**Drill-down:** Each row links to the relevant module's list screen (e.g., clicking "Grey" opens the Pending Folding list).

---

### R02 — MRL Lifecycle Report

**Question:** "Show me the complete history of MRL #526 from creation to dispatch."

| Field | Description |
|---|---|
| **Type** | Detail report (single MRL) |
| **Audience** | Manager, Supervisor, Head Office |
| **Input** | MRL number |

**Content:**

| Section | Fields |
|---|---|
| **Header** | MRL number, vendor, metres sent, date sent, quality code |
| **Inbound Receipts** | List of all receipts: avak date, lot number, grey metres, Gate Pass reference |
| **Pending Balance** | Metres sent - metres received |
| **Folding** | Folding metres, shrinkage, Chadat (per lot) |
| **Grading** | Grade breakdown per lot: Fresh %, Good Cut, Fent, Rags, Chindi, NA |
| **Packing Programs** | Programs using this MRL: program number, customer, bales planned/actual |
| **Bales Produced** | Bale numbers, brand, product, customer, metres |
| **Dispatch** | Delivery form numbers, dates, customer |
| **Exceptions** | Decision Pending entries, Not Acceptable entries with status |
| **Event Timeline** | Full chronological event log from MRL_CREATED to DELIVERY_CREATED |

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
| MRLs created (outbound) | Count + total metres | `mrls` |
| Inbound receipts | Count + total metres | `inbound_receipts` |
| Lots folded | Count + total metres | `folding_records` |
| Lots graded | Count + total metres | `grading_entries` (aggregated) |
| Average Fresh yield % | Percentage | `gradation_reports` |
| Packing programs completed | Count | `packing_programs` (status = COMPLETED) |
| Bales packed | Count + total metres | `bales` |
| Bales dispatched | Count + total metres | `delivery_forms` |
| Delivery forms created | Count | `delivery_forms` |
| Cutting waste generated | Total kg | `packing_programs` (cutting_waste_kg) |

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
| Receipt → Folding start | Time between `INBOUND_RECEIVED` and `FOLDING_COMPLETED` |
| Receipt → Grading complete | Time between `INBOUND_RECEIVED` and last `GRADING_RECORDED` for lot |
| Grading → Packing program | Time between last `GRADING_RECORDED` and `PACKING_PROGRAM_CREATED` |
| Packing program → All bales packed | Time between `PACKING_PROGRAM_CREATED` and last `BALE_REGISTERED` |
| Packing → Dispatch | Time between `BALE_REGISTERED` and `DELIVERY_CREATED` |
| **Total: Receipt → Dispatch** | End-to-end time |

Shown as: average, median, min, max for the selected period. Optionally broken down by vendor or lot.

---

## Vendor Reports

### R05 — Vendor Pending Balance Report

**Question:** "What is the total outstanding material at each vendor?"

| Field | Description |
|---|---|
| **Type** | Summary report |
| **Audience** | Manager, Head Office |
| **Filters** | Vendor (optional) |

**Content:**

| Column | Description |
|---|---|
| Vendor | Mill name |
| Total MRLs outstanding | Count of MRLs with pending balance > 0 |
| Total metres sent | Sum of metres_sent for outstanding MRLs |
| Total metres received | Sum of metres_received |
| Pending balance | Total metres_sent - metres_received |
| Oldest MRL age | Days since oldest outstanding MRL was created |

**Drill-down:** Click vendor to see individual MRLs.

---

### R06 — Vendor-wise Sent/Received Summary

**Question:** "How much did we send to and receive from each vendor this month?"

| Field | Description |
|---|---|
| **Type** | Period summary |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, vendor |

**Content:**

| Column | Description |
|---|---|
| Vendor | Mill name |
| MRLs created | Count sent in period |
| Metres sent | Total metres dispatched to vendor |
| Receipts recorded | Count received in period |
| Metres received | Total metres received back |
| Average turnaround (days) | Average time from send to receive |

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
| Fresh metres | Sum of Fresh grading for vendor's lots |
| Fresh yield % | Percentage |
| Not Acceptable metres | Sum of NA grading |
| NA rate % | Percentage |
| Open NA entries | Count still unresolved |
| Average shrinkage % | From folding records for vendor's lots |

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
| Gate Pass metres | Vendor-reported |
| Folding metres | RG Faith-measured |
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

**Content:** This is the printable version of the Gradation Report screen from Module 04.

**Metre Progression:**
```
Metres sent (MRL outbound):     6,006.80
Gate Pass metres (received):    5,826.00
Folding metres (RG Faith):      5,644.33
Total graded metres:            5,644.33
```

**Grade Breakdown:**

| Grade | Kg | Metres | % of Graded | Loss Factor | Loss % |
|---|---|---|---|---|---|
| Fresh | — | 5,470.02 | 96.91% | 0% | 0% |
| Good Cut | — | 52.00 | 0.92% | 0% | — |
| Fent | 11.46 | 64.44 | 1.14% | 50% | 0.58% |
| Rags | 1.15 | 6.48 | 0.15% | 0% | — |
| Chindi | 2.00 | 16.82 | 0.35% | 100% | 0.35% |
| Not Acceptable | — | 0.00 | 0.00% | — | — |
| **Total** | | **5,644.32** | **100%** | | |

Note: Fresh, Good Cut, and Not Acceptable are measured directly in metres. Fent, Rags, and Chindi are measured in kg and converted to metres via Chadat.

**Metadata:** MRL number, vendor, lot number, quality code, Chadat, folding date, grading completion status.

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
| Lots graded | Count |
| Total metres graded | Sum |
| Fresh metres | Sum |
| Fresh yield % | Percentage |
| Non-Fresh breakdown | Good Cut %, Fent %, Rags %, Chindi %, NA % |

Visualised as a line chart (Fresh yield % over time) with a table below.

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
| Pieces | Per bale |
| Metres | Per bale |
| Program Number | Source packing program |

---

### R12 — Cutting Waste Report

**Question:** "How much waste are we generating, and is it increasing?"

| Field | Description |
|---|---|
| **Type** | Summary + trend |
| **Audience** | Manager |
| **Filters** | Date range, MRL |

**Content:**

| Column | Description |
|---|---|
| Program Number | Packing program |
| MRL / Lot | Source material |
| Metres allocated | Fresh metres input |
| Metres packed | Into bales |
| Good Cut (metres) | Waste grade — in metres |
| Fent (kg) | Waste grade — in kg |
| Chindi (kg) | Waste grade — in kg |
| Waste ratio | Waste quantity relative to metres packed |

**Summary:** Average waste ratio over the period, trend line.

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
| **Header** | Program number, type (Regular/Todiya), date, MRL, lot, quality, tone, width, Chadat |
| **Line Items** | Per line: brand, product, trade number, fold type, customer, cut length, pieces/bale, planned bales, actual bales, planned metres, actual metres |
| **Bales Produced** | Bale number, packing date, pieces, metres, packing slip reference |
| **Cutting Waste** | Good Cut (metres), Fent (kg), Chindi (kg) |
| **Status** | Current status, completion date |

---

## Dispatch Reports

### R14 — Dispatch Register

**Question:** "List all dispatches for this period."

| Field | Description |
|---|---|
| **Type** | List report |
| **Audience** | Manager, Head Office |
| **Filters** | Date range, customer |

**Content:**

| Column | Description |
|---|---|
| Delivery Form No | Serial number |
| Date | Dispatch date |
| Customer (Haste) | Who received the goods |
| Total Bales | Count per delivery |
| Total Metres | Sum per delivery |
| Total Pieces | Sum per delivery |

**Summary row:** Total bales, metres, pieces for filtered period.

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
| Delivery Forms | Count |
| Total Bales | Sum |
| Total Metres | Sum |
| Products shipped | List of distinct products |
| Last dispatch date | Most recent delivery |

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
| Lot Number | Vendor lot |
| Metres | Pending decision |
| Remark | Why it's pending |
| Created Date | When entry was made |
| Days Since Last Activity | Aging indicator |
| Status Flag | Green (< 7 days), Yellow (7-13 days), Red (14+ days) |

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
| Created Date | When graded as NA |
| Days Open | Total age |
| Last Activity | Most recent comment date |
| Status | Open / In Discussion |

**Summary:** Grouped by vendor, showing total pending metres per vendor.

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
| Created Date | When opened |
| Resolved Date | When closed |
| Days to Resolve | Duration |
| Resolution Type | Vendor Pickup / Unresolved |

**Summary:** Average resolution time, % resolved via pickup vs. unresolved, by vendor.

---

### R20 — Accumulation Trend Report

**Question:** "Is our leftover stock growing or shrinking over time?"

| Field | Description |
|---|---|
| **Type** | Trend chart + table |
| **Audience** | Manager |
| **Filters** | Date range, grade |

**Content:**

| Column | Description |
|---|---|
| Date / Period | Time bucket (weekly/monthly) |
| Good Cut (metres) | Running balance — in metres |
| Fent (kg) | Running balance — in kg |
| Rags (kg) | Running balance — in kg |
| Chindi (kg) | Running balance — in kg |
| Total (metres equivalent) | Sum using Chadat conversion for kg grades |
| Inflow | Added from grading + cutting waste (metres for Good Cut, kg for others) |
| Outflow | Consumed by Todiya programs |

Visualised as a stacked area chart showing accumulation over time.

---

## Packaging Materials Reports

### R21 — Packaging Stock Report

**Question:** "What is the current stock of all packaging items?"

| Field | Description |
|---|---|
| **Type** | List report |
| **Audience** | Manager, Supervisor |

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

### R22 — Packaging GRN Register

**Question:** "What packaging materials did we receive this month?"

| Field | Description |
|---|---|
| **Type** | List report |
| **Audience** | Manager |
| **Filters** | Date range, vendor, SKU |

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

### R23 — Packaging Consumption Report

**Question:** "How much packaging material are we consuming, and for which programs?"

| Field | Description |
|---|---|
| **Type** | Summary + detail |
| **Audience** | Manager |
| **Filters** | Date range, SKU, packing program |

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

| # | Report Name | Category | Type | Primary Audience |
|---|---|---|---|---|
| R01 | Stage-wise Inventory | System-wide | Dashboard | Manager, Head Office |
| R02 | MRL Lifecycle | System-wide | Detail | Manager, Head Office |
| R03 | Monthly Throughput | System-wide | Summary | Manager, Head Office |
| R04 | End-to-End Cycle Time | System-wide | Analytical | Manager, Head Office |
| R05 | Vendor Pending Balance | Vendor | Summary | Manager, Head Office |
| R06 | Vendor Sent/Received Summary | Vendor | Period summary | Manager, Head Office |
| R07 | Vendor Quality Performance | Vendor | Analytical | Manager, Head Office |
| R08 | Shrinkage Report | Processing | List + summary | Manager, Supervisor |
| R09 | Gradation Report (Printable) | Processing | Printable | Manager, Supervisor, Head Office |
| R10 | Fresh Yield Trend | Processing | Trend | Manager, Head Office |
| R11 | Bale Production Report | Packing & Output | Summary + detail | Manager, Head Office |
| R12 | Cutting Waste Report | Packing & Output | Summary + trend | Manager |
| R13 | Packing Program Summary | Packing & Output | Printable | Manager, Supervisor |
| R14 | Dispatch Register | Dispatch | List | Manager, Head Office |
| R15 | Customer-wise Dispatch | Dispatch | Summary | Manager, Head Office |
| R16 | Delivery Form (Printable) | Dispatch | Printable | Manager, Supervisor |
| R17 | Decision Pending Aging | Exception | List + aging | Manager |
| R18 | Not Acceptable Aging | Exception | List + aging | Manager |
| R19 | NA Resolution History | Exception | Analytical | Manager, Head Office |
| R20 | Accumulation Trend | Exception | Trend | Manager |
| R21 | Packaging Stock Report | Packaging | List | Manager, Supervisor |
| R22 | Packaging GRN Register | Packaging | List | Manager |
| R23 | Packaging Consumption | Packaging | Summary + detail | Manager |
