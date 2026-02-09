---
title: "Process 06 — Packing Program & Execution"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, packing, cutting, baling, brand, product, bale, packing-program]
---

# Process 06 — Packing Program & Execution

## Overview

| Field | Value |
|---|---|
| **Purpose** | Transform graded Fresh material into branded, packed bales — creating the finished product. The facility manager creates a Packing Program (work order) specifying how to cut, fold, brand, and package the material, and the team executes it. |
| **Trigger** | (1) Sales order from head office (~95%), (2) proactive inventory advancement (~5%), or (3) Todiya (leftover repacking). |
| **End condition** | Finished bales produced with bale number, brand stamp, product name, trade number, packing slip. Cutting waste recorded. |
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
| Fresh-graded fabric | Grading output (Process 05) | Physical rolls (metres) | Best-quality material, ready for packing. |
| Accumulated leftovers (for Todiya) | Accumulation area | Physical pieces (metres/kg) | Good Cut (metres), Fent (kg) — only for Todiya programs. |
| Sales order / packing slip (when applicable) | Head office | Paper / verbal | Triggers the program in ~95% of cases. |
| Packaging materials | Packaging inventory (Process 10) | Physical materials | Plastic, stickers, stamps, cardboard, thread, brochures. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Finished bales | Storage / dispatch area | Physical boxes | Ready for customer delivery (Process 07). |
| Packing slip (inside bale) | Inside the bale | Generated document | One copy sealed inside each bale. |
| Packing slip (office copy) | Filed | Generated document | Reference copy. |
| Bale label | On the bale | Printed label | External identification. |
| Cutting waste (Good Cut, Fent, Chindi) | Accumulation area | Physical fabric (Good Cut in metres; Fent/Chindi in kg) | Leftover from cutting — added to Todiya stock. |
| Cutting tally sheet | Filed | Handwritten | Execution record of what was cut and packed. |

## Process Steps

### Phase 1: Packing Program Creation

```
START — Trigger received (sales order / proactive / Todiya)
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Manager identifies available     │
│    material                         │
│    • Check Fresh inventory          │
│    • Match to order requirements    │
│      (quality, width, quantity)     │
│    • For Todiya: check accumulated  │
│      leftover stock                 │
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
│    • Calculate total metres needed  │
│    ★ Phase 2: system may assist     │
│      with calculations              │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Manager writes Packing Program   │
│                                     │
│  HEADER:                            │
│    Date, Process House (mill),      │
│    Lot No, Pcs, MRL No, Product,   │
│    Mtrs, Shrinkage, Width,          │
│    Whiteness (tone), Chadat         │
│                                     │
│  BODY (per line item):              │
│    No., Fold type, Brand stamp,     │
│    Trade stamp (product), Metres    │
│    per piece × count, No of bales,  │
│    Total metres, Haste (customer)   │
│                                     │
│  NOTES:                             │
│    Sample instructions, quality     │
│    notes, special packaging         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Material physically moved        │
│    • Fresh material moved from      │
│      graded storage to cutting area │
│    • Material is now "allocated"    │
│      to this packing program        │
└──────────────┬──────────────────────┘
               │
               ▼
Proceed to Phase 2: Execution
```

### Phase 2: Cutting & Packing Execution

```
┌─────────────────────────────────────┐
│ 5. Cut to specified lengths         │
│    • Follow Packing Program specs   │
│    • Example: "350 × 02 = 700"     │
│      means cut 2 pieces of 350m    │
│    • Note leftover material         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 6. Fold per specification           │
│    • Apply the fold type from the   │
│      Packing Program                │
│    • Fold types (user-configurable):│
│      Book, Book 3 fold, Roof,       │
│      2Fold, B1F                     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 7. Apply brand and packaging        │
│    • Plastic layer added per fold   │
│    • Brand stamp applied (SSTM etc.)│
│    • Product stickers applied       │
│    • Brochure/booklet if sample     │
│    • Pieces placed in cardboard box │
│    • Thread wrapped around box      │
│    • Bale label attached externally │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 8. Assign Bale Number               │
│    • Unique bale number assigned    │
│    • Bale identity recorded:        │
│      - Bale Number                  │
│      - Brand Stamp                  │
│      - Product Name                 │
│      - Trade Number (SKU ref)       │
│      - Fold Type                    │
│      - Tone, Width                  │
│      - Haste (customer)             │
│      - Cut Length, Pieces per Bale  │
│      - Total Metres                 │
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
┌─────────────────────────────────────┐
│ 10. Record cutting waste            │
│     • Leftover material sorted:     │
│       Good Cut, Fent, Chindi        │
│     • Good Cut measured in metres;  │
│       Fent/Chindi weighed in kg     │
│     • Added to accumulation stock   │
│       for future Todiya             │
└──────────────┬──────────────────────┘
               │
               ▼
END — Finished bales ready for dispatch.
      Waste recorded and accumulated.
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
| Not enough Fresh material for the order | Manager adjusts cutting pattern or waits for more material to be graded. |
| Sample required | Noted on Packing Program. Sample piece cut from same lot, packaged with brochure/booklet per manager's specification. |
| Todiya packing program | Uses accumulated leftover stock. May mix grades (G/C + Fent). Different material source but same execution flow. |
| Manager wants to pack proactively (no sales order) | Allowed — program created without sales order reference. ~5% of cases. |

## State Transition

```
Graded — Fresh ──► Packing Program Assigned ──► Packed (Bale)
                          │
                          └──► (Reversal allowed) ──► Graded — Fresh
                               Rare in practice, but system should
                               not block this transition.
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
| Tone | Inherited from lot | O1W |
| Width | Inherited from lot | 58" |
| Haste (Customer) | Packing Program | Patawli |
| Cut Length | Packing Program | 20 metre cut |
| Pieces per Bale | Counted at packing | 15 |
| Total Metres | Sum of pieces | 342 |

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream (Fresh)** | [05 — Quality Grading](05-quality-grading.md) | Fresh-graded material is the primary input. |
| **Upstream (Todiya)** | [08 — Todiya](08-todiya.md) | Accumulated leftovers trigger Todiya packing programs. |
| **Upstream (Materials)** | [10 — Packaging Material Management](10-packaging-material-management.md) | Packaging materials consumed during execution. |
| **Downstream** | [07 — Dispatch](07-dispatch.md) | Finished bales shipped to customers. |

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
