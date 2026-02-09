---
title: "Process 07 — Dispatch"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, dispatch, delivery, shipping, customer]
---

# Process 07 — Dispatch

## Overview

| Field | Value |
|---|---|
| **Purpose** | Ship finished bales from Miroli to customers. Create Delivery Form documenting what was shipped. |
| **Trigger** | Packed bales ready for customer delivery. |
| **End condition** | Bales loaded, Delivery Form signed, truck dispatched. Inventory state = Dispatched. |
| **Frequency** | Multiple times per week. |
| **Typical duration** | Loading and dispatch: 1–2 hours per shipment. |

## Roles

| Role | Responsibility |
|---|---|
| Manager / supervisor | Creates Delivery Form, selects bales for shipment, sign-off. |
| Workers (2–4) | Load bales onto truck. |
| Transport team | RG Faith's own vehicles deliver to customer. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Finished bales | Packing output (Process 06) | Physical boxes | With bale labels and packing slips inside. |
| Customer / order reference | Sales team / Packing Program | Verbal or paper | Identifies who receives which bales. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Loaded truck | Customer location | Physical goods | Bales shipped. |
| Delivery Form (original) | Customer | Physical document | Accompanies the goods. |
| Delivery Form (office copy) | Filed at Miroli | Physical document | Retained for records. |

## Process Steps

### Main Flow

```
START — Packed bales ready for shipment
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Identify bales for dispatch      │
│    • Select bales based on customer │
│      order / Haste assignment       │
│    • May include multiple products  │
│      / brands in one shipment       │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Create Delivery Form             │
│                                     │
│  HEADER:                            │
│    Inward No (serial), Date,        │
│    From (RG Faith Creations),       │
│    Godown (Miroli),                 │
│    Haste (customer/party — single   │
│    customer identifier in system)   │
│                                     │
│  LINE ITEMS (per bale):             │
│    Bale No, Lot No, Trade No,       │
│    SST Sec (section/grade),         │
│    Pcs/Kg/Samples, Metres           │
│                                     │
│  FOOTER:                            │
│    Total bales, signatures          │
│    (Ok, Office, Recd./Date,         │
│    Made by)                         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Load bales onto truck            │
│    • Physical loading               │
│    • Verify count against           │
│      Delivery Form                  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Sign off and dispatch            │
│    • Delivery Form signed           │
│    • Truck departs Miroli           │
│    • Office copy filed              │
│    • Original accompanies shipment  │
└──────────────┬──────────────────────┘
               │
               ▼
END — Bales shipped to customer.
      Delivery Form filed.
```

### Example: Multi-Product Delivery

From scan page 17 — Delivery Form No. 890 to customer "S.P.":

| Bale No | Trade No | Pcs | Metres |
|---|---|---|---|
| 34804 | 58072 | 6 | 342 |
| 33700 | Princy | 15 | 518 |
| 36426 | Beri Beri | 14 | 499 |
| 34196 | Pulscar | 7 | 294 |
| 36792 | Goylord | 9 | 370 |
| 17414 | AmbiFit | 12 | 356 |
| **Total** | | **6 bales** | **2,379** |

A single delivery can include multiple product brands for the same customer.

### Exceptions

| Exception | How Handled |
|---|---|
| Bale missing or miscounted during loading | Recount. Adjust Delivery Form if needed. |
| Quality issue noted on delivery (e.g., scan page 10 Hindi note) | Remark added to Delivery Form. |

**Note:** Customer returns are out of scope. The system does not handle inbound returns of finished bales.

## State Transition

```
Packed (Bale) ──► Dispatched
```

**Dispatch-ready trigger:** A bale is dispatch-ready once its packing slip has been generated (no separate approval step).

**Dispatch timing:**
- **Fresh bales:** Typically dispatched immediately after packing.
- **Todiya bales:** May sit packed for days while buyer logistics are arranged (Todiya khata involved).

## Key Data Captured

| Field | Description |
|---|---|
| Delivery Form No | Serial number for the dispatch document. |
| Date | Dispatch date. |
| Haste (Customer/Party) | Who receives the goods. Single customer identifier in the system. |
| Bale Numbers | Individual bale identifiers in this shipment. |
| Trade Numbers | Product SKU references per bale. |
| Pieces per Bale | Number of fabric pieces in each bale. |
| Metres per Bale | Total metres in each bale. |
| Total Bales | Count of bales in this shipment. |

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | [06 — Packing Program & Execution](06-packing-program-execution.md) | Receives finished bales. |
| **Related** | [08 — Todiya](08-todiya.md) | Todiya bales also dispatched via same process. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Delivery Form (pre-printed, current) | Paper dispatch document. |
| Future system | Digital delivery form, dispatch register, customer dispatch history, link to packing programs. |

## Known Issues

| Issue | Impact |
|---|---|
| No digital record of dispatches | Cannot query dispatch history, volumes, or customer patterns. |
| No tracking of goods in transit | No visibility between dispatch and customer receipt. |
| No confirmation of customer receipt | Disputes possible if bales lost or miscounted. |
| Paper copies sent to head office via courier | Delay between dispatch and head office data entry. |
