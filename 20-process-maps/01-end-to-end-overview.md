---
title: "End-to-End Process Overview"
status: draft
created: 2026-02-07
updated: 2026-02-11
tags: [process, overview, master]
---

# End-to-End Process Overview

## Process Overview

- **Purpose:** Transform finished (dyed) cloth received from vendors into branded, packed bales ready for customer dispatch, while tracking inventory at every stage.
- **Trigger:** Finished material received at Miroli from vendor (MRL generated at first inbound receipt).
- **End condition:** Finished bales dispatched to customer via Delivery Form.
- **Frequency:** Continuous — multiple lots in various stages at any given time.
- **Typical duration:** ~1 week from inbound receipt to dispatch for normal lots. Can extend to months/years for decision-pending exceptions.

## Master Process Flow

```
┌─────────────────────────────────────────────────────────────────────┐
│                        RG FAITH — MIROLI FACILITY                   │
│                                                                     │
│                              ┌──────────────────┐                   │
│                              │  VENDOR MILL     │                   │
│                              │  (External)      │                   │
│                              │  Dyeing process  │                   │
│                              └────────┬─────────┘                   │
│                                       │                             │
│                                       │ Gate Pass + finished cloth   │
│                                       ▼                             │
│  ┌──────────────────────────────────────────────────┐               │
│  │ INBOUND RECEIPT                                   │               │
│  │ (Process 02)                                      │               │
│  │                                                   │               │
│  │ • Receive goods + Gate Pass                       │               │
│  │ • Generate MRL Number (first receipt)             │               │
│  │ • Record Avak Date, metres, vendor-reported       │               │
│  │   pending greige balance                          │               │
│  │ • Store as RECEIVED inventory                     │               │
│  └────────────────────┬─────────────────────────────┘               │
│                       │                                              │
│                       ▼                                              │
│  ┌──────────────────────────────────────────────────┐               │
│  │ FOLDING & MEASUREMENT                             │               │
│  │ (Process 03)                                      │               │
│  │                                                   │               │
│  │ • Fold each roll (standard fold)                  │               │
│  │ • Measure and record metres per roll              │               │
│  │ • Record Chadat (separate event,                  │               │
│  │   must be before gradation)                       │               │
│  └────────────────────┬─────────────────────────────┘               │
│                       │                                              │
│                       ▼                                              │
│  ┌──────────────────────────────────────────────────┐               │
│  │ TONE & FINISH CLASSIFICATION                      │               │
│  │ (Process 04)                                      │               │
│  │                                                   │               │
│  │ • Rough visual inspection                         │               │
│  │ • Send samples to head office                     │               │
│  │ • HO confirms tone + finish                       │               │
│  │ • Factory worker records classification           │               │
│  │ • Two attributes: tone (e.g., O1W)                │               │
│  │   and finish (e.g., 01, 02, 03)                   │               │
│  └────────────────────┬─────────────────────────────┘               │
│                       │                                              │
│                       ▼                                              │
│  ┌──────────────────────────────────────────────────┐               │
│  │ PACKING PROGRAM & EXECUTION                       │               │
│  │ (Process 05)                                      │               │
│  │                                                   │               │
│  │ • Manager creates program: which rolls            │               │
│  │   (cross-lot), fold type, brand, trade,           │               │
│  │   cut metres, bale count (advisory)               │               │
│  │ • Phase 1: Cut + fold → thaan (logged)            │               │
│  │ • Phase 2: Assemble thaans → bale                 │               │
│  │ • Gradation: non-Fresh thaans logged              │               │
│  │   with grade (embedded in execution)              │               │
│  │ • Assign Bale Number, generate Packing Slip       │               │
│  └──┬──────┬──────────────────────┬─────────────────┘               │
│     │      │                      │                                  │
│  FRESH  NON-FRESH              NOT ACCEPTABLE                        │
│  thaans  thaans                 material                             │
│     │      │                      │                                  │
│     │      │                      └──► NOT ACCEPTABLE                │
│     │      │                          RESOLUTION                     │
│     │      │                          (Process 08)                   │
│     │      │                                                         │
│     │      └──► ACCUMULATE for TODIYA                                │
│     │           (Process 07)                                         │
│     │                                                                │
│     ▼                                                                │
│  ┌──────────────────────────────────────────────────┐               │
│  │ DISPATCH                                          │               │
│  │ (Process 06)                                      │               │
│  │                                                   │               │
│  │ • Create Delivery Form                            │               │
│  │ • Schedule pickup                                 │               │
│  │ • Load bales, dispatch to customer                │               │
│  └──────────────────────────────────────────────────┘               │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

> **Note:** Packaging Material Management is deferred to a future phase.

## Inventory States Through the Process

| State | Stage | Unit | Process |
|---|---|---|---|
| **Received** | Finished material arrived at Miroli from vendor | Meters | 02 - Inbound |
| **Folded** | Measured by RG Faith per roll | Meters | 03 - Folding |
| **Awaiting Classification** | Samples sent to HO, waiting for tone/finish confirmation | Meters | 04 - Classification |
| **Classified** | Tone and finish assigned per roll/lot | Meters | 04 - Classification |
| **Awaiting Program** | Classified, ready for packing program allocation | Meters | — |
| **Packing Program Assigned** | Allocated to a packing program | Meters | 05 - Packing |
| **Thaan (Fresh)** | Cut and folded piece, logged | Meters | 05 - Packing |
| **Thaan (Non-Fresh)** | Good Cut / Fent / Rags / Chindi, logged during gradation | Metres or Kg | 05 - Packing |
| **Packed (Bale)** | Thaans assembled into bale | Pieces + Meters | 05 - Packing |
| **Pickup Scheduled** | Bale scheduled for dispatch | Pieces + Meters | 06 - Dispatch |
| **Dispatched** | Shipped to customer | Pieces + Meters | 06 - Dispatch |
| **Accumulated (Todiya)** | Non-Fresh bales awaiting buyer | Metres / Kg | 07 - Todiya |
| **Decision Pending** | Quality unclear, awaiting decision | Meters | — |

## Key Identifiers Through the Process

```
MRL Number ──────────────────────────────────────────────────────►
(Created at first inbound receipt, used through entire lifecycle)

Lot Number ────────────────────────────────────────────────────►
(Created by vendor, stays through entire lifecycle)

                    Roll ────────────────────────────────►
                    (Unit within a lot, tracked from folding)

                                        Thaan ──────────►
                                        (Created at packing execution)

                                              Bale Number ────►
                                              (Created at packing)

                                              Trade Number ───►
                                              (Assigned at packing)
```

## Process Index

### Main Flow

| # | Process | Trigger | Key Output |
|---|---|---|---|
| 02 | [Inbound Receipt](02-inbound-receipt.md) | Truck arrives from vendor with Gate Pass | MRL generated (first receipt), received inventory recorded |
| 03 | [Folding & Measurement](03-folding-measurement.md) | Received material selected for processing | Folding metres recorded per roll, Chadat recorded |
| 04 | [Tone & Finish Classification](04-tone-finish-classification.md) | Folded material awaiting classification | Tone and finish assigned, material classified and awaiting program |
| 05 | [Packing Program & Execution](05-packing-program-execution.md) | Sales order or proactive decision | Thaans logged, bales with brand/product/trade, gradation output |
| 06 | [Dispatch](06-dispatch.md) | Packed bales ready for customer | Pickup scheduled, Delivery Form, bales shipped |

### Sub-processes

| # | Process | Trigger | Key Output |
|---|---|---|---|
| 07 | [Todiya — Unpack & Repack](07-todiya.md) | Accumulated non-Fresh material finds a buyer | Existing bales unpacked, thaans repacked into new bales |
| 08 | [Not Acceptable Resolution](08-not-acceptable-resolution.md) | Material identified as Not Acceptable during packing | Vendor pickup or material remains at facility |

### Deferred

| # | Process | Status |
|---|---|---|
| ~~09~~ | ~~Packaging Material Management~~ | Deferred to future phase |

## Connected Processes

All processes feed the **real-time stage-wise inventory dashboard** — the core output of the system. Each state transition (received → folded → classified → packing program → packed → dispatched) updates the dashboard.

## Known Issues

| Issue | Impact | Current Workaround |
|---|---|---|
| No real-time visibility across stages | Manager relies on memory and physical checks | Manual registers, monthly summary to head office |
| Decision-pending lots forgotten | Material sits for months/years | Periodic manual review |
| Data travels to head office via physical courier | Delay between factory events and system updates | Courier/helper carries paper documents |
| Multiple paper documents per lot, no single source of truth | Confusion, lost data, reconciliation effort | Workers maintain parallel registers |
