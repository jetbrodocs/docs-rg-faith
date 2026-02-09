---
title: "End-to-End Process Overview"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, overview, master]
---

# End-to-End Process Overview

## Process Overview

- **Purpose:** Transform semi-finished dyed cloth into branded, packed bales ready for customer dispatch, while tracking inventory at every stage.
- **Trigger:** Grey cloth sent to vendor for dyeing (MRL creation).
- **End condition:** Finished bales dispatched to customer via Delivery Form.
- **Frequency:** Continuous — multiple lots in various stages at any given time.
- **Typical duration:** ~1 week from inbound receipt to dispatch for normal lots. Can extend to months/years for decision-pending exceptions.

## Master Process Flow

```
┌─────────────────────────────────────────────────────────────────────┐
│                        RG FAITH — MIROLI FACILITY                   │
│                                                                     │
│  ┌──────────────┐                                                   │
│  │ OUTBOUND TO  │  Grey cloth sent to vendor for dyeing             │
│  │ VENDOR       │  MRL Number assigned                              │
│  │ (Process 02) │──────────────────────┐                            │
│  └──────────────┘                      │                            │
│                                        ▼                            │
│                              ┌──────────────────┐                   │
│                              │  VENDOR MILL     │                   │
│                              │  (External)      │                   │
│                              │  Dyeing process  │                   │
│                              └────────┬─────────┘                   │
│                                       │                             │
│                                       │ Gate Pass + dyed cloth      │
│                                       ▼                             │
│  ┌──────────────┐    ┌──────────────────────────┐                   │
│  │ PACKAGING    │    │ INBOUND RECEIPT           │                   │
│  │ MATERIAL     │    │ (Process 03)              │                   │
│  │ MANAGEMENT   │    │                           │                   │
│  │ (Process 10) │    │ • Receive goods + Gate Pass│                  │
│  │              │    │ • Match to MRL             │                   │
│  │ • Inward     │    │ • Record Avak Date         │                   │
│  │ • Stock      │    │ • File Gate Pass           │                   │
│  │ • Consume    │    │ • Store as GREY inventory   │                  │
│  └──────┬───────┘    └────────────┬───────────────┘                  │
│         │                         │                                  │
│         │                         ▼                                  │
│         │            ┌──────────────────────────────────────────┐    │
│         │            │ FOLDING & MEASUREMENT  ◄──► QUALITY GRADING│   │
│         │            │ (Process 04)               (Process 05)   │   │
│         │            │                                           │   │
│         │            │ Independent activities — can happen in    │   │
│         │            │ any order or concurrently                  │   │
│         │            │                                           │   │
│         │            │ 04: Fold into 2m folds, measure,          │   │
│         │            │     calculate Chadat, reconcile           │   │
│         │            │ 05: Inspect, classify into grades,        │   │
│         │            │     update Gradation Report               │   │
│         │            └──┬──────┬──────┬──────┬───────────────────┘   │
│         │               │      │      │      │                        │
│         │          FRESH │  G/C │  F/R/C│  N/A │                      │
│         │               │      │      │      │                        │
│         │               │      │      │      └──► NOT ACCEPTABLE      │
│         │               │      │      │          RESOLUTION           │
│         │               │      │      │          (Process 09)         │
│         │               │      │      │                               │
│         │               │      │      └──► ACCUMULATE                 │
│         │               │      │           for TODIYA                 │
│         │               │      │           (Process 08)               │
│         │               │      │                                      │
│         │               │      └──► ACCUMULATE                        │
│         │               │           for TODIYA                        │
│         │               │                                             │
│         │               ▼                                             │
│         │  ┌──────────────────────────┐                               │
│         │  │ PACKING PROGRAM &        │                               │
│         │  │ EXECUTION                │                               │
│         │  │ (Process 06)             │                               │
│         │  │                          │                               │
│         │  │ • Manager creates program │                              │
│         │  │ • Cut to lengths          │                              │
│         │  │ • Fold per spec           │                              │
│         │  │ • Brand stamp             │                              │
│         ├──► • Package with materials  │                              │
│         │  │ • Assign Bale Number      │                              │
│         │  │ • Generate Packing Slip   │                              │
│         │  └────────────┬─────────────┘                               │
│         │               │                                             │
│         │               ▼                                             │
│         │  ┌──────────────────────────┐                               │
│         │  │ DISPATCH                 │                               │
│         │  │ (Process 07)             │                               │
│         │  │                          │                               │
│         │  │ • Create Delivery Form    │                              │
│         │  │ • Load bales              │                              │
│         │  │ • Ship to customer        │                              │
│         │  └──────────────────────────┘                               │
│         │                                                             │
└─────────┴─────────────────────────────────────────────────────────────┘
```

## Inventory States Through the Process

| State | Stage | Unit | Process |
|---|---|---|---|
| **Sent to Vendor** | Cloth at vendor mill for dyeing | Meters | 02 - Outbound |
| **Grey** | Received at Miroli, not yet processed | Meters | 03 - Inbound |
| **Folded** | Measured by RG Faith (independent of grading) | Meters | 04 - Folding |
| **Graded — Fresh** | Quality checked, best grade (independent of folding) | Meters | 05 - Grading |
| **Graded — Good Cut** | Quality checked, second grade | Metres | 05 - Grading |
| **Graded — Fent/Rags/Chindi** | Quality checked, lower grades | Kilograms | 05 - Grading |
| **Graded — Not Acceptable** | Rejected, pending return to vendor | Meters | 05 - Grading |
| **Decision Pending** | Awaiting grading decision | Meters | 05 - Grading |
| **Packing Program Assigned** | Allocated to a packing program | Meters | 06 - Packing |
| **Packed (Bale)** | Cut, folded, branded, boxed | Pieces + Meters | 06 - Packing |
| **Dispatched** | Shipped to customer | Pieces + Meters | 07 - Dispatch |
| **Accumulated (Todiya)** | Leftovers awaiting buyer | Metres (Good Cut) / Kilograms (Fent/Rags/Chindi) | 08 - Todiya |

## Key Identifiers Through the Process

```
MRL Number ──────────────────────────────────────────────────────►
(Created at outbound, used through entire lifecycle)

Lot Number ────────────────────────────────────────────────────►
(Created by vendor, stays through entire lifecycle)

                                              Bale Number ────►
                                              (Created at packing)

                                              Trade Number ───►
                                              (Assigned at packing)
```

## Process Index

### Main Flow

| # | Process | Trigger | Key Output |
|---|---|---|---|
| 02 | [Outbound to Vendor](02-outbound-to-vendor.md) | Woven cloth ready for dyeing | MRL Number assigned, cloth dispatched to mill |
| 03 | [Inbound Receipt](03-inbound-receipt.md) | Truck arrives from vendor with Gate Pass | Grey inventory recorded, Gate Pass filed |
| 04 | [Folding & Measurement](04-folding-measurement.md) | Grey material selected for processing | Folding meters recorded, Chadat calculated |
| 05 | [Quality Grading](05-quality-grading.md) | Folded material ready for inspection | Material classified into grades, Gradation Report updated |
| 06 | [Packing Program & Execution](06-packing-program-execution.md) | Sales order or proactive decision | Finished bales with brand, product, trade number |
| 07 | [Dispatch](07-dispatch.md) | Packed bales ready for customer | Delivery Form, bales shipped |

### Sub-processes

| # | Process | Trigger | Key Output |
|---|---|---|---|
| 08 | [Todiya — Leftover Repacking](08-todiya.md) | Accumulated leftovers find a buyer | Repacked bales from Good Cut/Fent/Rags |
| 09 | [Not Acceptable Resolution](09-not-acceptable-resolution.md) | Material graded as Not Acceptable | Vendor pickup or material remains at facility |
| 10 | [Packaging Material Management](10-packaging-material-management.md) | Packaging stock needed / received | Stock levels maintained, consumption tracked |

## Connected Processes

All processes feed the **real-time stage-wise inventory dashboard** — the core output of the system. Each state transition (grey → folded → graded → packing → packed → dispatched) updates the dashboard.

## Known Issues

| Issue | Impact | Current Workaround |
|---|---|---|
| No real-time visibility across stages | Manager relies on memory and physical checks | Manual registers, monthly summary to head office |
| Decision-pending lots forgotten | Material sits for months/years | Periodic manual review |
| Data travels to head office via physical courier | Delay between factory events and system updates | Courier/helper carries paper documents |
| Multiple paper documents per lot, no single source of truth | Confusion, lost data, reconciliation effort | Workers maintain parallel registers |
