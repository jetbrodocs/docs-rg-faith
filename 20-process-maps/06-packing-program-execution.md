---
title: "Process 06 — Packing Program & Execution"
status: draft
created: 2026-02-07
updated: 2026-02-11
tags: [process, packing, cutting, baling, brand, product, bale, packing-program, thaan, gradation]
---

# Process 06 — Packing Program & Execution

## Overview

| Field | Value |
|---|---|
| **Purpose** | Transform classified rolls into branded, packed bales — creating the finished product. The facility manager creates a Packing Program (work order) specifying which rolls to use, fold type, brand, trade, cut metres, and advisory bale count. During execution, thaans are tracked and gradation (quality sorting) happens as non-Fresh material is identified. |
| **Trigger** | (1) Sales order from head office (~95%), or (2) proactive inventory advancement (~5%). |
| **End condition** | Finished bales produced with bale-to-thaan mapping, bale number, brand stamp, product name, trade number, packing slip. Gradation data recorded for non-Fresh thaans. |
| **Frequency** | Continuous. Multiple programs may be pending or in execution. |
| **Typical duration** | Small orders (5 bales): hours. Large orders (50+ bales): days. |

## Roles

| Role | Responsibility |
|---|---|
| Facility manager / head supervisor | Creates the Packing Program — the master instruction document. Does all cutting calculations mentally. |
| Cutting workers (3–7) | Cut fabric to specified lengths. |
| Folding workers (2–4) | Fold cut pieces per specification (Book, Roof, 2Fold, B1F, etc.). |
| Packing workers (2–4) | Apply brand stamps, stickers, plastic layers, box into bales, thread wrapping. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Classified rolls | Classification output (Process 05) | Physical rolls (metres, with tone + finish) | Rolls in Awaiting Program status. Cross-lot selection allowed (program can pull rolls from multiple MRLs). |
| Sales order (when applicable) | Head office | Paper / verbal | Triggers the program in ~95% of cases. |
| Chadat value | Recorded as a separate event | Number | Must be recorded before any gradation entry. Chadat = metres / kg. Lot-specific. |
| Packaging materials | Packaging inventory (future scope) | Physical materials | Plastic, stickers, stamps, cardboard, thread, brochures. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Finished bales | Storage / dispatch area | Physical boxes | Ready for customer delivery (Process 07). Bale-to-thaan mapping tracked. |
| Packing slip (inside bale) | Inside the bale | Generated document | One copy sealed inside each bale. |
| Packing slip (office copy) | Filed | Generated document | Reference copy. |
| Bale label | On the bale | Printed label | External identification. |
| Thaan records | System / paper register | Per-thaan data | Each thaan: metres, source roll reference. One thaan = one roll source. |
| Non-Fresh material (gradation output) | Accumulation area | Physical fabric (Good Cut in metres; Fent/Rags/Chindi in kg) | Identified during cutting, logged with grade. Added to accumulation stock. |
| Gradation Report (progressive) | Head office / system | Computer-generated report | Updated as packing produces gradation data. |
| Cutting tally sheet | Filed | Handwritten | Execution record of what was cut and packed. |

## Process Steps

### Phase 1: Packing Program Creation

```
START — Trigger received (sales order / proactive)
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Manager identifies available     │
│    material                         │
│    • Check classified rolls in      │
│      Awaiting Program status        │
│    • Match to order requirements    │
│      (tone, finish, width, qty)     │
│    • Cross-lot selection allowed:   │
│      program can pull rolls from    │
│      multiple MRLs                  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Manager calculates cutting       │
│    pattern (mental math)            │
│    • Determine cut lengths per      │
│      piece (20m, 25m, 30m, etc.)   │
│    • Determine number of pieces     │
│      per bale                       │
│    • Determine number of bales      │
│      (advisory — actual may differ) │
│    • Calculate total metres needed  │
│    ★ Phase 2: system may assist     │
│      with calculations              │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Manager writes Packing Program   │
│                                     │
│  Single instruction entity with:    │
│    • Which rolls (cross-lot allowed)│
│    • Fold type (Book, Roof, 2Fold,  │
│      B1F, etc.)                     │
│    • Brand stamp (e.g., SSTM)      │
│    • Trade (product / SKU ref)     │
│    • Cut metres per piece           │
│    • Bale count (advisory)          │
│    • Haste (customer)               │
│                                     │
│  NOTES:                             │
│    Sample instructions, quality     │
│    notes, special packaging         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Material physically moved        │
│    • Classified rolls moved from    │
│      storage to cutting area        │
│    • Material is now "allocated"    │
│      to this packing program        │
└──────────────┬──────────────────────┘
               │
               ▼
Proceed to Phase 2: Execution
```

### Phase 2: Execution — Cut, Fold, and Create Thaans

```
┌─────────────────────────────────────┐
│ 5. Cut and fold to create thaans    │
│    • Follow Packing Program specs   │
│    • Cut roll to specified length   │
│    • Fold per specification (fold   │
│      type from Packing Program:     │
│      Book, Roof, 2Fold, B1F, etc.) │
│    • Each cut+fold = one thaan      │
│    • Thaan data logged:             │
│      - Metres                       │
│      - Source roll reference        │
│    • One thaan = one roll source    │
│    • Example: "350 × 02 = 700"     │
│      means cut 2 thaans of 350m    │
│      from a roll                    │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 6. Embedded gradation (during       │
│    cutting)                         │
│    • Non-Fresh thaans identified    │
│      during cutting are logged with │
│      a grade:                       │
│      - Good Cut (metres)            │
│      - Fent (kg)                    │
│      - Rags (kg)                    │
│      - Chindi (kg)                  │
│      - Not Acceptable (metres)      │
│    • VALIDATION: Chadat must be     │
│      recorded before any gradation  │
│      entry (system enforced)        │
│    • Chadat used for kg ↔ metre     │
│      conversion (Fent, Rags, Chindi)│
│    • Non-Fresh material routed to   │
│      accumulation area              │
│    • Not Acceptable routed to       │
│      Process 09                     │
│    • Gradation Report updated       │
│      progressively as packing       │
│      produces data                  │
└──────────────┬──────────────────────┘
               │
               ▼
```

### Phase 3: Assemble Thaans into Bales

```
┌─────────────────────────────────────┐
│ 7. Apply brand and packaging        │
│    • Plastic layer added per fold   │
│    • Brand stamp applied (SSTM etc.)│
│    • Product stickers applied       │
│    • Brochure/booklet if sample     │
│    • Thaans placed in cardboard box │
│    • Thread wrapped around box      │
│    • Bale label attached externally │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 8. Assign Bale Number               │
│    • Unique bale number assigned    │
│    • Bale-to-thaan mapping tracked  │
│    • Bale identity recorded:        │
│      - Bale Number                  │
│      - Brand Stamp                  │
│      - Product Name                 │
│      - Trade Number (SKU ref)       │
│      - Fold Type                    │
│      - Tone, Finish, Width          │
│      - Haste (customer)             │
│      - Cut Length, Pieces per Bale  │
│      - Total Metres                 │
│      - List of thaans in this bale  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 9. Generate Packing Slip            │
│    • One copy inside bale (sealed)  │
│    • One copy filed (office copy)   │
│    • Fields: Case No, Trade No,     │
│      Width, Colour, Gradation,      │
│      Pieces, Quantity (metres),     │
│      Packing type, Description      │
└──────────────┬──────────────────────┘
               │
               ▼
END — Finished bales ready for dispatch.
      Thaan-to-bale mapping recorded.
      Gradation data captured for non-Fresh.
      Non-Fresh material accumulated.
```

### Multiple Programs on One Sheet

A single physical form can contain multiple packing programs:

```
Page of Packing Program form
  │
  ├── Cutting No (1) / A-Tape  ──→  Packing Program Record #1
  │     Line items for Customer A
  │
  ├── Cutting No (2) / B-Tape  ──→  Packing Program Record #2
  │     Line items for Customer B
  │
  └── Cutting No (3) / C        ──→  Packing Program Record #3
        Line items for Customer C
```

In the system, each cutting number is a **separate packing program record**.

### Exceptions

| Exception | How Handled |
|---|---|
| Not enough classified material for the order | Manager adjusts cutting pattern or waits for more material to be classified. |
| Sample required | Noted on Packing Program. Sample piece cut from same lot, packaged with brochure/booklet per manager's specification. |
| Manager wants to pack proactively (no sales order) | Allowed — program created without sales order reference. ~5% of cases. |
| Chadat not yet recorded for a lot | Gradation entries blocked until Chadat is recorded. Must be captured before packing begins for the lot. |

## State Transition

```
Classified (Awaiting Program) ──► Packing Program Assigned ──► Packed (Bale)
                                       │
                                       └──► (Reversal allowed) ──► Awaiting Program
                                            Rare in practice, but system should
                                            not block this transition.

Non-Fresh thaans identified during cutting:
  ──► Accumulated (Good Cut, Fent, Rags, Chindi → Process 08: Todiya)
  ──► Not Acceptable (→ Process 09: Resolution)
```

**Dispatch-ready trigger:** A bale is ready for dispatch once its packing slip has been generated. No separate approval step.

## Brand & Product Assignment

**No fixed rules.** Any lot can become any brand/product. The manager decides at Packing Program creation time.

```
Incoming Lot (MRL 1782, KT-11000)
  │
  └── Packing Program splits into:
      ├── 5 bales as SSTM / Officer      → Customer: Rame
      ├── 2 bales as SSTM / RG Special   → Customer: CB
      ├── 3 bales as SSTM / Sportsman    → Customer: VS
      └── 1 bale as SSTM / KT-11058      → Customer: L.K.Soul
```

## Finished Bale Identity

| Attribute | Source | Example |
|---|---|---|
| Bale Number | Auto-assigned at packing | 37432 |
| Brand Stamp | Packing Program | SSTM |
| Product Name | Packing Program | Sportsman |
| Trade Number | Packing Program | S8072-58" |
| Fold Type | Packing Program | Book 3 fold |
| Tone | From classification (Process 05) | O1W |
| Finish | From classification (Process 05) | 01 |
| Width | Inherited from lot | 58" |
| Haste (Customer) | Packing Program | Patawli |
| Cut Length | Packing Program | 20 metre cut |
| Pieces per Bale | Counted at packing | 15 |
| Total Metres | Sum of pieces | 342 |

## Thaan Tracking

The thaan is the unit created when a roll is cut and folded to specification:

```
Roll (source) ──► Cut + Fold ──► Thaan (logged: metres + source roll)
                                     │
                                     ▼
                                 Bale (assembly of thaans)
```

**Key rules:**
- One thaan comes from one roll (single source roll reference)
- Each thaan records: metres and source roll reference
- Bale-to-thaan mapping is tracked (which thaans are in which bale)
- Thaan identity persists through Todiya (unpack/repack does not change thaans)

## Gradation During Packing

Gradation (quality grading) is NOT a standalone process. It happens as an embedded step during packing execution. When a non-Fresh thaan is identified during cutting, it is logged with its grade:

| Grade | Unit | Destination |
|---|---|---|
| Fresh | metres | Into bale (normal flow) |
| Good Cut | metres | Accumulation area (Todiya) |
| Fent | kg | Accumulation area (Todiya) |
| Rags | kg | Accumulation area (Todiya) |
| Chindi | kg | Accumulation area (Todiya) — 100% loss |
| Not Acceptable | metres | Process 09 (vendor return) |

**Validation rule:** Chadat must be recorded before any gradation entry. The system should enforce this.

**Gradation Report:** A progressive report updated as packing produces data. Shows metre progression, grade breakdown, shrinkage, and Fresh yield percentage. See the Gradation Report section below.

### The Gradation Report

The Gradation Report is the **single most important document** in the process. It is a progressive, running report that captures data as packing execution proceeds:

#### Metre Progression
```
Grey U/S Mtrs:     6,006.80   (vendor's original measurement)
Gate Pass Mtrs:    5,826.00   (what arrived per Gate Pass)
F.H. Avak Mtrs:   5,825.00   (what reached folding area)
F.H. Fold Mtrs:   5,644.33   (after folding — RG Faith's count)
F.H. Plk Mtrs:    5,644.33   (after packing)
```

#### Grade Breakdown (example)
| Grade | Kg | Metres | % of Total | Loss Factor | Loss % |
|---|---|---|---|---|---|
| Fresh | — | 5,470.02 | 96.91% | 0% | 0% |
| Good Cut | — | 52.00 | 0.92% | 0% | — |
| Fent | 11.46 | 64.44 | 1.14% | 50% | 0.58% |
| Rags | — | 6.48 | 0.15% | 0% | — |
| Chindi | 2.00 | 16.82 | 0.35% | 100% | 0.35% |
| **Total** | | **5,644.32** | **100%** | | |

#### Progressive Nature
If only 4,000 of 6,000 metres have been packed, the report shows data for only those 4,000 metres. It updates as more material is processed.

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | [05 — Tone & Finish Classification](05-tone-finish-classification.md) | Classified rolls (Awaiting Program) are the primary input. |
| **Downstream (Fresh bales)** | [07 — Dispatch](07-dispatch.md) | Finished bales shipped to customers. |
| **Downstream (Non-Fresh)** | [08 — Todiya](08-todiya.md) | Non-Fresh material identified during gradation goes to accumulation for Todiya. |
| **Downstream (Not Acceptable)** | [09 — Not Acceptable Resolution](09-not-acceptable-resolution.md) | Rejected material identified during gradation enters return pipeline. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Packing Program form (handwritten, current) | Master instruction document. |
| Head office ERP (current) | Generates packing slips — data entered at head office. |
| Cutting tally sheet (handwritten, current) | Tracks execution against program. |
| Future system | Digital packing program, bale registration, auto-generated packing slips and labels, waste tracking, material allocation view. |

## Known Issues

| Issue | Impact |
|---|---|
| Packing Program is handwritten — hard to search or report on | No historical analysis of packing patterns. |
| Packing slip doesn't capture all details (workers add handwritten notes) | Gap between system and operational reality. |
| No real-time tracking of packing execution progress | Manager doesn't know what's completed vs pending. |
| Cutting waste not systematically tracked | Accumulation stock quantities are estimates. |
| Multiple programs on one sheet create confusion | Hard to track individually in paper-based system. |
| No visibility into Fresh material allocation | Risk of over-allocation or under-utilisation. |
