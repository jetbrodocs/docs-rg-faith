---
title: "Packing Program, Cutting, and Baling"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [observation, packing, cutting, baling, brand, sku, packing-program]
---

# Packing Program, Cutting, and Baling

## Location / Station

- **Area:** Miroli facility — cutting and packing area
- **Station/Cell:** No fixed station. Open area that scales based on workload.
- **Address/Building:** Miroli facility, Ahmedabad

## Activity

Once fabric has been folded and graded as Fresh (or in some cases, Good Cut), it enters the packing pipeline. This pipeline has two distinct phases:

1. **Packing Program creation** — A planning/instruction step where the facility manager defines how the material should be cut, folded, branded, and packed to fulfill a sales order.
2. **Cutting and baling execution** — The physical work of cutting fabric to specified lengths, folding it in the specified pattern, applying brand stamps, and boxing it into bales.

This is where raw, graded material transforms into a **branded finished product** — and it's where the most complexity lives. The same incoming lot can become multiple different branded products, in different cut lengths, with different fold patterns, for different customers, all specified in a single packing program (or multiple programs on one sheet of paper).

## The Packing Program — The Master Instruction Document

### What It Is

The Packing Program is a handwritten instruction document created by the **head supervisor or facility manager**. It is the single most important operational document at Miroli — it tells the cutting and packing team exactly what to do with a lot of fabric.

Think of it as a **work order** that specifies:
- Which lot(s) to process
- How to cut the fabric (lengths per piece)
- How to fold each piece (fold type)
- Which brand to stamp on each piece
- Which product/trade number to assign
- Which customer (Haste) each set of pieces is for
- Whether samples are required and what packaging SKU the sample needs
- The Chadat value for the lot (for reference during cutting)

### Who Creates It

The head supervisor or facility manager creates the Packing Program. It requires **mental math calculation** (no spreadsheets or tools — the manager is very experienced) based on:
- The sales order dispatch requirements (what the customer ordered), if applicable
- Available graded inventory (what Fresh material is available)
- The specific lot characteristics (width, quality, shrinkage, Chadat)

Cutting pattern calculation assistance is out of scope for Phase 1 — the system captures the manager's decisions but does not compute them. This is a candidate for Phase 2.

### What Triggers It

There are **three triggers** for a Packing Program:

**1. Sales order (~95% of cases):**
Head office sends a packing slip (driven by a sales order) to the factory. The manager creates a Packing Program to fulfill it:
1. Identifies available Fresh material that matches the order requirements
2. Calculates cutting patterns to meet the order specifications
3. Writes up the Packing Program

**2. Proactive inventory advancement (~5% of cases):**
Even without a sales order, the manager may proactively create a Packing Program to **move inventory forward** — converting graded Fresh material into finished bales so it's ready for dispatch when an order comes in. This is driven by the desire to keep material flowing and avoid buildup at the graded stage.

**3. Todiya (accumulated leftovers):**
When accumulated leftover material (Good Cut, Fent, etc.) finds a buyer, the manager creates a Todiya Packing Program to repackage the accumulated stock.

**Important:** The Packing Program is **not always tied to a sales order**. The system must allow creating packing programs without a sales order reference.

### Execution

Currently, packing programs are executed **one at a time**, but there may be pending programs queued up. The system should support **multiple concurrent packing programs**. When a packing program is created, Fresh material is **physically moved** from the graded storage area to the cutting area.

### Packing Program Form — Detailed Breakdown

The Packing Program uses a pre-printed form from "RG Faith Creations Pvt Ltd." The form has been observed across scan pages 13, 14, 15, and 20. Here is the full field breakdown:

#### Header Section

| Field | Purpose | Example Values |
|---|---|---|
| Date | Date the program was created | 6/11/26, 8/11/26, 12/11/26 |
| Process House | Which mill processed the fabric | Kalapurna, Goodwill |
| Lot No | Vendor's lot reference | 775, 4484, 7424, 1923 |
| Pcs | Number of pieces/rolls in the lot | 5, 30, 8, 46 |
| MRL No | Miroli tracking number | 1782, 1864, 1903, 1909 |
| Product | Inbound quality/product code | Uniform (Blue), Uniform-58", KT-11000 |
| Mtrs | Total meters to process | 5688, 1628, 143, 8785 |
| Shrinkage | Shrinkage factor for this lot | 5-12, 4.26, 8.57, 1.07 |
| Width | Fabric width | 1497M (149 CM), 89 CM |
| Whiteness | Tone/color | O1W (Off-White) |
| Chadat | Meters-to-kg conversion factor | 4.86, 5.37, 5.57 |

#### Instruction Line

Every Packing Program starts with a general instruction like:
> "Folding and Tapewise - Finish wale cutting"
> "Roof Folding Tape wise - Finish wale cutting, Fold (Hyd)"

This tells the team the general folding approach and that they should cut along the finish/tape direction.

#### Body — Cutting and Packing Specifications

The body is structured as numbered items, each specifying a complete cutting-to-packing instruction:

| Field | Purpose | Example Values |
|---|---|---|
| No. | Item number (circled) | 1, 2, 3, 4, 5... |
| Fold | Fold type | Fold, Roof, 2Fold, B1F |
| Brand Stamping | Brand to stamp on the product | SSTM |
| Trade Stamping | Product name / trade number | Officer, RG Special, Sportsman, KT-11058, Diamond, KT-21000, KT-555 |
| Mtrs | Meters per piece and total | "250 01 250" = 1 piece of 250m; "350 02 700" = 2 pieces of 350m = 700m total |
| No of Bales | How many bales this produces | 01, 02, 05 |
| Total | Total meters for this line item | 250, 350, 700, 1750 |
| Haste | Customer/party this is for | Rame, CB, VS, L.K.Soul, Jay Shree, P.C., N.M., Agra, Amit |
| Ok | Sign-off | Checkmark or initials |

Additional notes may appear inline:
- **Cut length specification:** "(21/22 MTR Cut)", "(20 MTR Cut)", "(25 to 30 MTR Cut)", "(30 MTR Cut)"
- **Sample instructions:** "Sample in Bale" — include a sample piece in the bale
- **Quality instructions:** "Good cut only!" — only use Good Cut material for this line
- **Special packaging:** "Packing slip at Ropean Cream field" — specific packaging instructions

### Multiple Packing Programs on One Sheet

A critical discovery from the brainstorming session: what appears as **one form with multiple "Cutting No" entries** is actually **multiple separate packing programs** written on the same sheet of paper.

For example, on scan page 14:
- **Cutting No (1)** = Packing Program 1
- **Cutting No (2)** = Packing Program 2
- **Cutting No (3)** = Packing Program 3

Each cutting number is a distinct set of instructions, potentially for different customers, different brands, or different material grades. The labels "A-Tape", "B-Tape", "C" are just identifiers to distinguish them on the same page.

**In the system, these must be modeled as separate packing program records**, even though they may reference the same MRL or lot.

### Two Types of Packing Programs

#### 1. Regular Packing Program (Fresh material)

Triggered by a sales order. Uses Fresh-graded material. The typical flow:
- Sales order comes in
- Manager identifies available Fresh lots
- Creates cutting/packing instructions
- Team executes

Example: Scan page 13 — Uniform fabric from Kalapurna, 5688 meters, being cut into various lengths for different customers (Rame, CB, VS, L.K.Soul, Jay Shree) under the SSTM brand with product names Officer, RG Special, Sportsman, and KT-11058.

#### 2. Todiya Packing Program (Leftover/accumulated material)

Triggered by accumulated leftovers finding a buyer. Uses Good Cut, Fent, or other non-Fresh grades that have been sitting in the accumulation area.

Example: Scan page 14 — "Lot Pending" range, with instructions mixing Good Cut and Fent ("G/C + Fent"), and explicit note "Good cut only!" for certain lines. This is repacking accumulated leftover material for a buyer.

Key differences from regular programs:
- Material comes from accumulated stock, not a freshly graded lot
- Multiple grades may be mixed in a single bale (G/C + Fent)
- May reference multiple MRLs combined together
- Triggered by finding a buyer for the leftovers, not by a specific sales order

## Brand and Product Assignment — No Fixed Rules

One of the most important observations about the packing process is that **there are no fixed rules for brand/product assignment**.

The same incoming lot of fabric can be split across any number of brands and product names. The assignment is entirely at the **discretion of the facility manager** when creating the Packing Program. There is no BOM (Bill of Materials), no recipe, no mapping between raw material quality codes and finished product brands.

What this means for the system:
- **No BOM or product-material mapping needed**
- Brand and product are simply **attributes assigned at packing time**
- The system should allow free selection from the configured brand and product masters
- Any lot can become any product — the system should not enforce restrictions (open first, constrain later principle)

### Product Identity of a Finished Bale

A finished bale has multiple identity attributes, all assigned during packing:

| Attribute | Source | Example |
|---|---|---|
| Bale Number | Auto-assigned at packing | 37432 |
| Brand Stamp | Selected by manager in Packing Program | SSTM (Shree Shubhlaxmi Textile Mills) |
| Product Name | Selected by manager in Packing Program | Sportsman |
| Trade Number | Finished product SKU reference | S8072-58" |
| Fold Type | Specified in Packing Program | Book 3 fold |
| Tone | Inherited from lot | O1W (Off-White) |
| Width | Inherited from lot | 58" |
| Haste | Customer assignment | Patawli |
| Cut Length | From Packing Program | 20 meter cut |
| Pieces per Bale | Counted during packing | 15 |
| Total Meters | Sum of all pieces | 342 |

## Cutting and Packing Execution

### Step 1: Receive Packing Program

The cutting team receives the handwritten Packing Program from the manager.

### Step 2: Retrieve Material

The team retrieves the specified lot(s) of Fresh material from the graded inventory area.

### Step 3: Cut to Specified Lengths

Following the Packing Program, the fabric is cut into pieces of the specified lengths. For example:
- 9 pieces of 20m, 1 of 30m, 2 of 25m, 1 of 22m, 1 of 29m, 1 of 31m = 15 pieces totaling 342 meters (from scan page 18, bale label)
- Or: 43m, 48m, 38m, 35m, 28m, 26m, 33m, 36m, 24m = 9 pieces totaling 311m (from scan page 11, packing steps)

### Step 4: Fold per Specification

Each cut piece is folded according to the specified fold type. Known fold types (user-configurable):
- **Book fold** — folded like a book
- **Book 3 fold** — three-fold book style
- **Roof fold** — folded from the top
- **2Fold** — two-fold
- **B1F** — user-defined fold type notation (likely a book fold variant)

The fold type affects the final appearance and dimensions of the packed product. Different customers or markets may prefer different folds.

### Step 5: Apply Brand and Packaging

For each piece/set:
1. **Plastic layer** added per fold
2. **Brand stamp** applied (e.g., SSTM)
3. **Product stickers** applied
4. **Brochure/booklet** inserted (if sample or as specified)
5. Pieces placed into **cardboard box**
6. **Thread** wrapped around the box to secure and tighten
7. **Bale label** attached externally (see below)

### Step 6: Assign Bale Number and Generate Packing Slip

Each completed bale gets:

**Bale Label (physical, from scan page 18):**
- Sort No, Cms, Metres, Pieces breakdown
- Trade number and fold type
- Tone, width, Haste (customer)

**Packing Slip (computer-generated, from scan page 19):**
- Case No (system reference, e.g., ML 26-34804)
- Trade No, Width, Colour, Gradation, Pieces, Quantity (meters)
- Packing type, Description ("Blended Fabric")
- Quality sign-off
- Bale Code

One copy of the packing slip goes **inside the bale** physically. The other is filed.

Note: The packing slip is generated by the head office system, and workers add handwritten notes for details the system doesn't capture (format code, exact cut length, Haste, new bale number). This is a gap the new system should fill.

### Step 7: Record Leftover Material

After cutting is complete, any leftover material (from the Fresh lot) is sorted into:
- **Good Cut** pieces
- **Fent** pieces
- **Chindi** waste

These leftovers are weighed (in kg), recorded, and added to the accumulation stock for future Todiya sale.

The waste calculations appear at the bottom of Packing Programs (e.g., scan page 15 and 20):
```
Total lot: 8785 meters
Packed as Fresh: 5558 meters
Fent: 166.99 meters equivalent
Chindi: 20.44 meters equivalent
Good Cut: 50 meters equivalent
```

## Cutting/Packing Tally Sheet (Execution Tracking)

Scan page 21 shows a handwritten **tally sheet** that tracks the execution of cutting and packing across multiple runs or "Finishes."

### Structure

The sheet is divided into sections by "Finish" run:
- **(A) Finish** — Columns for different product brands (KT-555, KT-11000), with piece counts per cutting number
- **(B) Finish** — Different products (Diamond, KT-21000, KT-11000), same structure
- **Hyd** — Products going to Hyderabad, same structure

Each section tracks:
- Case/bale numbers (e.g., T41503, T41505)
- Piece lengths (40x6 = 6 pieces of 40m)
- Running totals

The tally sheet is the **execution record** that maps to the Packing Program. It shows what was actually cut and packed versus what was planned.

### "Bale Thaan Adjustment"

The note "8 Bale Thaan Adjustment" at the bottom of the tally sheet indicates that 8 bales' worth of pieces (Thaan = piece) required adjustment — possibly recount, recut, or repack.

## Samples

Samples are handled within the normal packing process, not as a separate flow. When a customer requires a sample:

1. The **Packing Program** notes "Sample in Bale" on the relevant line item
2. The manager specifies what **packaging SKU** to use for the sample (e.g., brochure, booklet)
3. During packing, the sample piece is cut from the same lot
4. The sample gets different packaging than the main bales (may include brochures or other marketing material)
5. The sample is included alongside or within the main shipment

The system should support sample instructions as an attribute of each packing program line item.

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Fresh-graded fabric | Grading output | Physical rolls | From the folding/grading stage |
| Accumulated leftovers (for Todiya) | Accumulation area | Physical rolls/pieces (weighed in kg) | Good Cut, Fent, etc. |
| Sales order (conceptual) | Sales team / head office | Verbal or paper | Triggers the packing program. System does not manage sales orders. |
| Packing Program | Facility manager | Handwritten form | The master instruction document |
| Packaging materials | Packaging inventory | Physical materials | Plastic, stickers, stamps, cardboard, thread, brochures |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Finished bales | Storage / dispatch area | Physical boxes | Ready for customer delivery |
| Packing slip (inside bale) | Inside the bale | Computer-generated print | One copy sealed inside |
| Packing slip (office copy) | Filed | Computer-generated print | Reference copy |
| Bale label | On the bale | Printed label | External identification |
| Leftover material | Accumulation area | Physical fabric | Good Cut, Fent, Chindi from cutting waste |
| Packed Bales List entry | Monthly register | Handwritten | Bale number recorded in monthly packed bales register |
| Cutting tally sheet | Filed | Handwritten | Execution record of what was cut and packed |

## People

| Role | Count | Shift/Schedule | Notes |
|---|---|---|---|
| Facility manager / head supervisor | 1 | Creates Packing Programs | Does the math, writes the instructions |
| Cutting workers | 3-7 | During working hours | Cut fabric to specified lengths |
| Folding workers | 2-4 | During working hours | Fold cut pieces per specification |
| Packing workers | 2-4 | During working hours | Apply stamps, package, box, thread |

## Timing

- **Frequency:** Continuous during working hours. Multiple packing programs may be in execution simultaneously.
- **Duration:** Varies greatly by order size. A small order (5 bales) may take hours. A large order (50+ bales) may take days.
- **Schedule:** Regular working hours.
- **Peak/Off-peak:** Follows sales order volume.

## Equipment and Tools

| Equipment | Purpose | Notes |
|---|---|---|
| Cutting tables / surfaces | Lay out and cut fabric | Manual cutting |
| Cutting tools | Cut fabric to length | Scissors, rotary cutters, etc. |
| Folding surfaces | Fold cut pieces | Manual folding |
| Brand stamps | Apply brand impressions | Physical stamps (SSTM, etc.) |
| Stickers / labels | Product identification | Pre-printed |
| Cardboard boxes | Bale container | Various sizes |
| Thread / twine | Secure and tighten bales | Wound around boxes |
| Plastic sheets | Protective layer per fold | Cut to size |
| Weighing scale | Weigh leftover material | For kg measurement of waste |

## Systems

| System | Used For | Notes |
|---|---|---|
| Packing Program (handwritten) | Master instruction document | Created by facility manager |
| Head office ERP | Generates packing slips | Data entered at head office |
| Paper registers | Monthly packed bales list | Handwritten bale number log |
| Cutting tally sheet | Execution tracking | Handwritten during packing |

## Handoffs

- **Comes from:** Folding/grading station (Fresh material) or accumulation area (Todiya material).
- **Goes to:** Dispatch area (finished bales) or accumulation area (cutting waste/leftovers).

## Problems and Workarounds

| Problem | Frequency | Current Workaround | Impact |
|---|---|---|---|
| Packing Program is handwritten — hard to reference later | Always | Physical filing of the form | Cannot search or report on past packing programs |
| Packing slip doesn't capture all details | Always | Workers add handwritten notes to the printed slip | Gap between system data and operational reality |
| No real-time tracking of packing execution progress | Always | Tally sheets and verbal updates | Manager doesn't know what's been completed vs pending |
| Cutting waste not systematically tracked | Sometimes | Ad-hoc weighing and notes at bottom of Packing Program | Accumulation stock quantities are estimates |
| Multiple packing programs on one sheet of paper | Always | Labels like "Cutting No 1, 2, 3" | Confusing — hard to track separately |
| No visibility into how much Fresh material has been allocated to packing programs vs still available | Always | Manager checks physically or from memory | Risk of over-allocation or under-utilization |

## Design Implications for the System

### Must Have
1. **Packing Program record** — Digital version of the handwritten form. Fields: MRL, lot, meters, product, brand, fold type, trade number, Haste, cut lengths, pieces, sample instructions.
2. **Multiple programs per lot** — Support multiple packing programs against the same MRL/lot.
3. **Regular vs Todiya flag** — Distinguish between regular (Fresh) and Todiya (leftover) packing programs.
4. **Bale registration** — Assign bale number, record contents (pieces, meters, brand, product, trade no, fold type, Haste).
5. **Packing slip generation** — Replace the head office-generated slip with one that captures all fields (eliminating the need for handwritten additions).
6. **Waste/leftover tracking** — Record Good Cut, Fent, Chindi produced as cutting waste from each packing program.
7. **Packed bales register** — Digital version of the monthly packed bales list.

### Nice to Have
8. **Packing progress tracking** — Show which packing programs are in progress, completed, or pending.
9. **Material allocation view** — Show how much Fresh material is available vs allocated to packing programs vs already packed.
10. **Cutting pattern calculator** — Help the manager calculate optimal cutting patterns to minimize waste and meet order specifications.
11. **Bale label generation** — Print bale labels directly from the system.
12. **Sample tracking** — Track which bales contain samples and what packaging was used.

### Not Needed
- BOM or recipe management (no fixed material-to-product mappings)
- Sales order management (out of scope — packing programs reference orders but the system doesn't manage them)
- Pricing on bales (no financial data)

## Photos / Diagrams

Relevant scan pages from `00-inbox/rg faith scans.pdf`:
- **Page 1:** Packed Bales List (December 2025) — monthly register of all bales packed
- **Page 11:** Packing Steps — handwritten cutting specifications for a specific bale
- **Page 13:** Packing Program (Form 1) — Uniform fabric, multiple products and customers
- **Page 14:** Packing Program (Form 2) — Todiya program, multiple cutting numbers
- **Page 15:** Packing Program (Form 3) — Cross-referencing multiple MRLs
- **Page 18:** Shree Shubhlaxmi Bale Label — physical label on the finished bale
- **Page 19:** Packing Slip (computer-generated) — office copy with handwritten additions
- **Page 20:** Packing Program (Form 4) — KT-11000 product, multiple brands, Hyderabad destination
- **Page 21:** Cutting/Packing Tally Sheet — execution tracking across multiple finish runs

## Raw Notes

From `00-inbox/notes.md`:
> "In the packing order process, here's what currently happens. Based on the sales order, a packing order is issued. The packing order is a guide that specifies how much fabric to cut, in what lengths, and how many pieces."
>
> "The raw material doesn't have a brand name assigned to it initially. The finished goods get a brand name only when they're packed. The way the material is packed, folded, and cut becomes part of the final product definition. So the final product SKUs depend on the specific cut and fold configuration."
>
> "The final packed product is called a bale, which is essentially a box. There's quite a bit of packaging material involved. For each fold, they add a plastic layer. Then there are stickers, brand stamping, and packaging inside the cardboard box. They also use threads wrapped around the cardboard box to secure and tighten it."
>
> "Any leftover material gets sorted into Chindi stock, fresh cut, or rags. These quantities are small, so they're baled but not immediately ready for sale."

## Open Questions

1. ~~How does the facility manager calculate cutting patterns?~~ **RESOLVED:** All mental math. Very experienced manager. Cutting pattern calculation is out of scope for Phase 1 — the system captures his decisions, doesn't compute them. Phase 2 feature.
2. ~~How many packing programs in execution simultaneously?~~ **RESOLVED:** Currently one at a time with some pending. System should support parallel execution.
3. ~~Average bales per packing program?~~ **RESOLVED:** Unknown. Not critical for design.
4. ~~Are bale numbers sequential?~~ **RESOLVED:** System will use its own numbering scheme.
5. ~~Is the packed bales list reconciled?~~ **RESOLVED:** The monthly packed bales list (page 1) is a workaround for lack of a system — manual summary for head office. Our system replaces this with real-time visibility.
6. ~~Is Fresh material physically moved for packing?~~ **RESOLVED:** Yes, material is physically moved to the cutting area when a packing program is created.
