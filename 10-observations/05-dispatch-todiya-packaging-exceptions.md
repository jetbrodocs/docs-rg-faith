---
title: "Dispatch, Todiya, Packaging Materials, and Exception Handling"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [observation, dispatch, todiya, packaging, exceptions, reprocess, decision-pending]
---

# Dispatch, Todiya, Packaging Materials, and Exception Handling

## Location / Station

- **Area:** Miroli facility — dispatch area, accumulation area, packaging storage
- **Station/Cell:** No fixed stations. Open floor plan.
- **Address/Building:** Miroli facility, Ahmedabad

## Overview

This observation covers four related but distinct operational areas that complete the end-to-end process at Miroli:

1. **Dispatch** — Shipping finished bales to customers
2. **Todiya (Toria)** — Reassigning and repacking accumulated leftover material
3. **Packaging Materials** — Tracking the consumable materials used during packing
4. **Exception Handling** — Managing rejected lots (Not Acceptable) and decision-pending lots

---

## Section 1: Dispatch

### Activity

Dispatch is the final step in the process — getting finished bales out the door and to the customer. It's triggered by completed packing programs and involves generating a delivery form, loading bales onto a truck, and sending them to the designated customer (Haste).

### The Delivery Form

The **Delivery Form** is the primary dispatch document. It is a pre-printed form from "RG Faith Creations Pvt. Ltd. / Ramgopal Girdharilal / Shree Shubhlaxmi Textile Mills" with the following fields:

#### Delivery Form Structure (from scan pages 10 and 17)

| Field | Purpose | Example Values |
|---|---|---|
| INWARD No | Delivery form serial number | 065, 890 |
| Date | Dispatch date | 13/6/26, 17/1/26 |
| From/Firm | Sender | R.G. Faith Creations |
| Godown | Source warehouse | Miroli |
| Delivered to | Customer name | P.M. Chhapti Tarat, S.P. |
| Haste | "For" — the party | Mohan Ram |
| P/L | Packing list reference | — |
| Bale No | Individual bale numbers | 34804, 33700, 36426, 34196, 36792, 17414 |
| Lot No | Vendor lot reference | — |
| Trade No | Product SKU reference | 58072, Princy, Beri Beri, Pulscar, Goylord, AmbiFit |
| SST Sec | Section / classification | Fresh, 11 |
| Pcs/Kg/Samples | Count | 6, 15, 14, 7, 9, 12 |
| Mts | Total meters per bale | 342, 518, 499, 294, 370, 356 |
| Del. Form No | Cross-reference | 890 |
| Total bales | Total in this delivery | 6 |

#### Key Observations from Delivery Forms

**Multiple brands on one delivery (scan page 17):**
A single delivery form (No. 890) shows 6 bales going to customer "S.P.", each with a different trade number / product:
- 58072 (Fresh, 6 pcs, 342m)
- Princy (15 pcs, 518m)
- Beri Beri (14 pcs, 499m)
- Pulscar (7 pcs, 294m)
- Goylord (9 pcs, 370m)
- AmbiFit (12 pcs, 356m)

This confirms that a single customer delivery can include multiple product brands.

**Quality issues on delivery (scan page 10):**
The delivery form includes Hindi notes: "Maal mein US type ariyaan hain" (the material has defects/issues). This particular delivery might be a return/reprocess shipment rather than a customer dispatch.

### Dispatch Process — Step by Step

1. **Packing is complete** — Bales are packed, labeled, and packing slips generated.
2. **Delivery Form created** — Lists all bales in the shipment with bale numbers, trade numbers, pieces, and meters.
3. **Bales loaded** — Physical loading onto truck/transport.
4. **Delivery Form signed** — "Ok", "Office", "Recd./Date", "Made by" fields signed off.
5. **Truck dispatched** — Goods leave Miroli to the customer.

### Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Finished bales | Packing area | Physical boxes | Ready for dispatch |
| Customer/order reference | Sales team / Packing Program | Verbal or paper | Identifies who gets what |

### Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Loaded truck | Customer location | Physical goods | Bales shipped |
| Delivery Form (original) | Customer | Physical document | Accompanies the goods |
| Delivery Form (office copy) | Filed at Miroli | Physical document | Retained for records |

### Problems and Workarounds

| Problem | Frequency | Current Workaround | Impact |
|---|---|---|---|
| No digital record of dispatches | Always | Paper delivery forms only | Cannot query dispatch history, volumes, or customer shipment patterns |
| No tracking of goods in transit | Always | Phone calls | No visibility between dispatch and customer receipt |
| No confirmation of customer receipt | Always | Informal verbal confirmation | Disputes possible if bales are lost or miscounted |

### Design Implications

**Must Have:**
1. **Dispatch record** — Digital delivery form. Fields: date, customer (Haste), list of bale numbers with trade number, pieces, meters.
2. **Dispatch against packing program** — Link dispatch records back to the packing program that produced the bales.
3. **Dispatch register** — Searchable log of all outward shipments.

**Nice to Have:**
4. Delivery form printing — Generate and print delivery forms from the system.
5. Customer-wise dispatch history — View all shipments to a specific customer over time.

---

## Section 2: Todiya (Toria) — Leftover Inventory Reassignment

### Activity

Todiya (or Toria — from the Hindi/Gujarati word for "breaking") is the process of **reassigning and repacking accumulated leftover material** when a buyer is found.

Originally, Todiya was a physical process — workers would literally break open existing bales to repackage the contents for a new buyer. Today, it is more of a **software/accounting operation** — the inventory is reassigned in records, though some physical repacking may still occur.

### How Leftover Material Accumulates

During the normal packing process, cutting produces waste:
- **Good Cut** pieces — usable but not Fresh quality
- **Fent** pieces — noticeable defects
- **Rags** — significant defects
- **Chindi** — waste material

Good Cut is measured in metres; Fent, Rags, and Chindi are weighed in kilograms (using the Chadat for conversion to metres). All are stored in the **accumulation area**. Over time, enough volume builds up to make a sale worthwhile.

### The Todiya Cycle

```
Cutting waste produced (small quantities per packing program)
    │
    ▼
Accumulate in storage (weeks to months)
    │
    ▼
Sales team finds a buyer for the accumulated stock
    │
    ▼
Facility manager creates a TODIYA Packing Program
    │
    ▼
Material is repacked / reassigned per the new buyer's requirements
    │
    ▼
Dispatch to the Todiya buyer
```

### Todiya Packing Program (from scan page 14)

A Todiya Packing Program looks similar to a regular one but has key differences:
- **Material source:** Accumulated leftover stock, not a freshly graded lot
- **Grades may be mixed:** "G/C + Fent" (Good Cut and Fent together in one bale)
- **Multiple MRLs:** May combine leftovers from several original lots
- **Quality notes:** "Good cut only!" or grade-specific instructions
- **Trigger:** Buyer for leftovers, not a regular sales order

### Todiya Account Tracking

Scan page 17 has the note "Toshika ki Todiya khaata" — "Toshika's Todiya account." This suggests that Todiya transactions are tracked per party/account. Each customer who buys leftover material has their own Todiya ledger.

### Design Implications

**Must Have:**
1. **Todiya packing program type** — Flag to distinguish from regular packing programs.
2. **Accumulated stock tracking** — Running balance of Good Cut (in metres), Fent, Rags, Chindi (in kg), aggregated from cutting waste across all packing programs.
3. **Todiya dispatch records** — Same as regular dispatch but linked to Todiya programs.

**Nice to Have:**
4. **Accumulation alerts** — Notify when leftover stock exceeds a threshold (time to find a buyer).
5. **Todiya account per party** — Track Todiya sales history per customer.

---

## Section 3: Packaging Materials

### Activity

Packaging materials are the consumable supplies used during the packing process. They are tracked separately from the main fabric inventory. The notes explicitly state that RG Faith does **not want a purchase order system** — they just want to record what comes in, track quantities, and monitor consumption.

### Packaging Materials Used

| Material | Purpose | When Used | Type |
|---|---|---|---|
| Plastic sheets/layers | Protective wrapping per fold | During folding and packing | Consumable |
| Stickers / product labels | Product identification | Applied during packing | Consumable |
| Brand stamps | Brand impression on fabric | Applied during packing | **Reusable** |
| Cardboard boxes | Bale container | Final packaging step | Consumable |
| Thread / twine | Secure and tighten the box | Final packaging step | Consumable |
| Brochures / booklets | Marketing material for samples | When samples are included | Consumable |

**Important distinction:** Most packaging materials are **consumable** — they get used up and need restocking. **Brand stamps are reusable** — they are assets that don't deplete. The system needs to handle both: consumables tracked by stock level and consumption, stamps tracked as reusable assets (master list only, no inventory depletion).

### Inward Process

From the notes:
> "Vendors are called to send packaging material. The material arrives with an invoice. There's a GRN with invoice. They don't want a purchase system. They just want to record the inward of material that comes in and the quantity, both to track inventory and to track when quantities are being used for packaging."

The process:
1. **Vendor ships packaging material** with an invoice
2. **Material received at Miroli** — GRN (Goods Receipt Note) created against the invoice
3. **Quantities recorded** — what material, how much, from which vendor
4. **Material stored** in the packaging area

### Consumption Tracking

Packaging materials are consumed during the packing process. The consumption needs to be tracked to:
- Know current stock levels (do we need to reorder?)
- Monitor usage rates
- Identify if consumption is aligned with production volume

Currently, there is **no scan or document** in the inbox that shows the packaging material tracking process. This is noted as a gap — we have the description from the notes but no example form or register.

### Design Implications

**Must Have:**
1. **Packaging material SKU master** — User-configurable. Each packaging item is an SKU with attributes.
2. **Vendor master for packaging** — Who supplies what.
3. **Inward receipt record** — Date, vendor, material SKU, UOM, quantity, vendor reference. No purchase order — just receipt recording.
4. **Current stock view** — How much of each consumable packaging material is on hand.
5. **Consumption recording** — How much packaging material was used (possibly linked to packing programs or bales).
6. **Reusable asset list** — Master list of reusable items (stamps). No stock depletion tracking needed for these.

**Nice to Have:**
6. **Reorder alerts** — When stock drops below a minimum threshold.
7. **Consumption-per-bale metrics** — Average packaging material used per bale.
8. **Vendor-wise purchase history** — How much was ordered from each packaging vendor over time.

**Not Needed:**
- Purchase order system (explicitly declined)
- Invoice/payment tracking (no financial data)
- Approval workflows for packaging procurement

---

## Section 4: Exception Handling

### 4a. Not Acceptable Material — Return to Vendor

#### What It Is

When material is graded as "Not Acceptable" during the folding/grading process, it needs to be sent back to the vendor mill. This is tracked on the **"Ready For Sending Reprocess List"** (scan page 2).

#### The Reprocess List (from scan page 2)

The list tracks material pending return to vendors:

| Field | Purpose |
|---|---|
| MRL No | Miroli tracking number for the lot |
| Avak Date | When the material originally arrived |
| Lot Number | Vendor's lot reference |
| Quality | Inbound quality code |
| Tone | Color code |
| MTR | Meters of rejected material |
| Remark | Free text explaining the issue (often in Hindi) |
| Mill Name | Which vendor to return it to (grouped by mill) |

Example entries from the scan:
- MRL 526, arrived 9/6/24, RC-8001 quality, 1408 MTR — PSJC mill
- MRL 826, arrived 11/8/25, Lancer W/R quality — PSJC mill
- MRL 1403, arrived 11/11/25, Liverpool quality, V9850 MTR — PSJC mill
- MRL 1097, arrived 11/9/24, Unifoom quality, F13 MTR — (different mill)
- MRL 2392, arrived 6/13/25, PCW/MQ quality, 930 MTR — (different mill)

#### Resolution Process

There is **no formal process** for resolving not-acceptable material. It works like an informal issue tracker:

1. **Issue opened** — Material graded as Not Acceptable, added to the Reprocess List
2. **Back and forth** — RG Faith contacts the vendor, discusses the issue
3. **Resolution (typical)** — Vendor arranges pickup of the rejected quantity
4. **Resolution (fallback)** — Material stays at Miroli if the vendor doesn't pick it up

**Key characteristics:**
- No credit notes or financial transactions involved
- No formal dispute resolution mechanism
- Based entirely on trust and relationship
- Some entries on the Reprocess List date back over a year — resolution can be very slow
- Remarks are in Hindi and capture the specific quality issue

#### Design Implications

**Must Have:**
1. **Not Acceptable record** — When material is graded Not Acceptable: MRL, lot, vendor, metres, reason (remark).
2. **Status tracking** — Open / In Discussion / Resolved (Picked Up) / Unresolved (Remains at facility).
3. **Aging visibility** — Show how long each Not Acceptable entry has been open.

**Nice to Have:**
4. **Vendor-wise view** — All open Not Acceptable items grouped by vendor.
5. **Aging alerts** — Notify when items have been pending beyond a threshold.
6. **Commentary log** — Record back-and-forth discussions with the vendor.

### 4b. Decision Pending Lots

#### What It Is

Decision-pending lots are material that has arrived at Miroli but has **not yet been graded**. The quality is unclear, and no one has made a classification decision. These lots sit in limbo until someone takes action.

#### The Problem

As documented in the folding/grading observation, decision-pending lots can sit for **months to years**. Scan page 3 shows lots from mid-2024 still pending in January 2026. The reasons vary:
- Borderline quality that's hard to classify
- Unusual defect types
- Nobody takes ownership
- Small lot size doesn't justify effort
- Manager hasn't gotten around to it

#### Current Tracking (from scan page 3)

The "Decision Pending Lots In Miroli" register tracks these with the same fields as the Reprocess List: MRL No, Avak Date, Lot Number, Quality, Tone, MTR, Remark, grouped by Mill name.

#### The Opportunity

This is one of the clearest areas where the system can add immediate value. Currently, these lots are invisible — they exist in a paper register that nobody actively monitors. A digital system can:
- Make them visible on a dashboard
- Track how long they've been pending
- Send aging alerts when lots exceed thresholds
- Force a resolution path (escalation to manager)
- Report on decision-pending volume as a KPI

#### Design Implications

**Must Have:**
1. **Decision-pending status** — A distinct inventory state between "Grey/Received" and "Graded."
2. **Remark field** — Free text describing why the lot is pending.
3. **Resolution workflow** — Move from Pending → Graded (any grade) or → Not Acceptable.
4. **Aging tracking** — Days pending, with configurable alert thresholds.

**Nice to Have:**
5. **Decision-pending dashboard** — Top-level visibility into all pending lots.
6. **Escalation rules** — Auto-assign to manager after X days.
7. **Decision-pending KPI** — Track volume and average resolution time.

---

## Cross-Cutting Observations

### The Paper-to-Digital Gap

Across all four areas in this observation, a consistent pattern emerges: **critical operational data exists only on paper**, making it invisible for reporting, planning, and management oversight.

| Area | Paper Document | What's Lost |
|---|---|---|
| Dispatch | Delivery Form | Dispatch history, customer volumes, shipment tracking |
| Todiya | Todiya account register | Leftover accumulation trends, Todiya sale history |
| Packaging | GRN register (if any) | Stock levels, consumption rates, reorder timing |
| Not Acceptable | Reprocess List | Vendor quality trends, resolution times |
| Decision Pending | Pending Lots register | Aging, volume, resolution rates |

The new system's primary value proposition is making this data **visible, queryable, and actionable**.

### The Configurable System Principle

Across all observations, a consistent design principle has emerged from discussions:

> **Build an open, configurable system first. Constrain later.**

This means:
- Master data (brands, products, fold types, tone codes, quality codes, SKU attributes, packaging material SKUs) should all be user-definable
- Business rules and validations should be addable over time, not hardcoded from day one
- The system should not enforce mappings that the business doesn't enforce (e.g., no BOM, no lot-to-brand rules)
- Start with data capture and visibility; add constraints and automation as the team matures into the system

---

## Key Reports Required

The following reports have been identified as priorities for the system:

| # | Report | Description | Replaces |
|---|---|---|---|
| 1 | **Real-time Stage-wise Inventory Dashboard** | How much material is at each stage: grey → folded → graded → packing program → packed → dispatched. Quantities in meters and kg. | No current equivalent — this is the core value proposition |
| 2 | **Gradation Report** | Progressive yield analysis per lot. Shows: meter progression, grade breakdown (Fresh %, Good Cut %, etc.), shrinkage, loss. Updates as the lot is processed. | Head office ERP-generated report (scan page 16) |
| 3 | **Fresh Pending Lots Report** | All lots graded as Fresh but not yet in a packing program or packed. Filterable by width, quality, mill. | Handwritten register (scan pages 6-7) |
| 4 | **Decision Pending Lots Report** | All lots awaiting grading decision. With aging (days pending), remarks, and mill. Aging alerts at configurable thresholds. | Handwritten register (scan page 3) |
| 5 | **Packed Bales Register** | All bales packed, with bale number, brand, product, trade number, meters, pieces, date. Searchable and filterable. | Monthly handwritten bale list (scan page 1) |
| 6 | **Reprocess / Not Acceptable List** | All Not Acceptable items pending vendor pickup. With status, aging, vendor, remarks. | Handwritten reprocess list (scan page 2) |
| 7 | **Packaging Material Stock** | Current stock levels of all consumable packaging materials. | No current equivalent |

---

## Summary of All Scan References

For completeness, here is the full mapping of all 21 scan pages to their roles in the process:

| Page | Document | Process Area |
|---|---|---|
| 1 | Packed Bales List (Dec 2025) | Packing output tracking |
| 2 | Ready For Sending Reprocess List | Not Acceptable / exception handling |
| 3 | Decision Pending Lots In Miroli | Decision-pending / exception handling |
| 4 | Packed Bales Stock Report (computer) | Inventory report (existing system) |
| 5 | Ready Goods Report (handwritten) | Folding / measurement |
| 6 | Fresh Pending Lots In Miroli 36" (pg 1) | Graded inventory tracking |
| 7 | Fresh Pending Lots In Miroli 36" (pg 2) | Graded inventory tracking |
| 8 | Folding meters vs factory meters | Folding / meter reconciliation |
| 9 | Kalapurna Mills Meter Report | Inbound / vendor document |
| 10 | RG Faith Delivery Form (with quality note) | Dispatch / possible return |
| 11 | Packing Steps (working notes) | Packing execution |
| 12 | RSK Industries Gate Pass | Inbound / vendor document |
| 13 | Packing Program — Form 1 (Uniform) | Packing program |
| 14 | Packing Program — Form 2 (Todiya) | Todiya packing program |
| 15 | Packing Program — Form 3 (Multi-MRL) | Packing program |
| 16 | Gradation Report (computer) | Grading / yield analysis |
| 17 | Delivery Form (finished goods, multi-brand) | Dispatch |
| 18 | Bale Label (Shree Shubhlaxmi) | Packing / bale identification |
| 19 | Packing Slip (computer, office copy) | Packing / bale identification |
| 20 | Packing Program — Form 4 (KT-11000) | Packing program |
| 21 | Cutting/Packing Tally Sheet | Packing execution tracking |

## Open Questions

1. ~~Is there a packaging material GRN book?~~ **RESOLVED:** No scan available, but the process is standard: record inward SKU, UOM, quantity, vendor reference. No POs.
2. ~~How does the sales team communicate orders?~~ **RESOLVED:** Head office sends a packing slip (driven by sales order) to the factory in 95% of cases. However, 5% of packing programs are proactive — manager packs material to move inventory forward without a sales order. The packing program is NOT always tied to a sales order.
3. ~~Is there a return delivery form for Not Acceptable pickups?~~ **RESOLVED:** No document — verbal confirmation only. System should track: Not Acceptable item → expected pickup date → actual pickup confirmed.
4. ~~Are any packaging materials reusable?~~ **RESOLVED:** Stamps are reusable (asset-like). Everything else is consumable. System should handle both: consumables tracked by stock/consumption, stamps as reusable assets.
5. ~~How are Todiya buyers found?~~ **RESOLVED:** Sales is out of scope.
6. ~~Typical accumulation time for Todiya?~~ **RESOLVED:** Not critical for design. Skipped.
7. ~~Any existing reporting/MIS?~~ **RESOLVED:** Key reports identified: (1) Gradation Report — progressive yield analysis per lot, (2) Fresh Pending Lots Report, (3) Decision Pending Lots Report, (4) Real-time stage-wise inventory dashboard, (5) Packed Bales List (replaced by real-time data), (6) Reprocess List — Not Acceptable items pending vendor pickup.
