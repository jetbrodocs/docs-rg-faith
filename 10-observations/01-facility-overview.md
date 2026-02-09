---
title: "Facility Overview and Material Lifecycle"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [observation, overview, facility, lifecycle]
---

# Facility Overview and Material Lifecycle

## Location / Station

- **Area:** Entire Miroli facility
- **Station/Cell:** N/A — open floor plan, no fixed stations
- **Address/Building:** RG Faith Creations Pvt. Ltd., New Block/Survey No. 514, Khata No. 879, 6.80 km South from Kamod Circle on Dholka-Ahmedabad Highway, Miroli, Taluka: Daskroi, District: Ahmedabad 382425, Gujarat, India. (Note: the 506/511 New Cloth Market address on letterheads is the head office, not the factory.)

## Company Structure

RG Faith operates under a multi-layered identity structure that is important to understand because it appears across all documents:

| Entity | Type | Notes |
|---|---|---|
| **RG Faith Creations Pvt. Ltd.** | Legal entity (company) | The registered company. Appears on formal documents, packing slips, and delivery forms. |
| **Ramgopal Girdharilal** | Legacy trade name | The founder/family trade name. Appears on letterheads alongside the company name. |
| **Shree Shubhlaxmi Textile Mills (SSTM)** | Brand | The primary brand (~90% of output). Stamped on finished goods. Appears on bale labels, packing slips, and delivery forms. |
| **Other brands (TBD)** | Brand(s) | There may be other brands beyond SSTM. The system must support multiple brands. |

Below the brand level sit **product names** (Officer, Diamond, Sportsman, KT-555, KT-21000, KT-No-one, RG Special, Princy, Beri Beri, Pulscar, Goylord, AmbiFit, DDT-58", Bluebird, etc.). These are not fixed to any specific raw material — any incoming lot can be assigned to any product name at the time of packing.

The hierarchy for the system is: **Company → Brand → Product**.

## The Core Business

RG Faith's end product is **white cotton cloth, rolled and folded into bundles (bales) for sale**. White cloth accounts for approximately 90% of their output. The remaining 10% follows the same process model — the final product is always cloth rolled into packs.

Their customers are **B2B** — they only take large orders. The typical unit of sale is the **bale**, which is a cardboard box containing cut and folded fabric pieces, sealed with plastic layers, stickers, brand stamps, and thread wrapping.

## The Miroli Facility

Miroli is RG Faith's **sole processing facility** where all operations happen — from receiving semi-finished goods to dispatching finished bales. Key characteristics:

- **Open floor plan** — no physically marked stations. The space is fluid; processes expand and contract based on season, peak time, and workload.
- **Staffing:** ~50 workers involved in the processes we're covering. 2-3 workers per process area at minimum, scaling up to 6-7 at busy areas during peak times. Workers are **multi-skilled** — no dedicated roles per station; anyone can work at any process area.
- **Capacity:** 1.4 crore meters (14 million meters) per year.
- **Current systems:** Entirely paper-based at the factory. The head office has a custom ERP, but the factory operates independently on handwritten registers, forms, and notebooks. Physical document copies are currently sent to head office via RG Faith's own courier/helper for data entry into the ERP.
- **Transport:** RG Faith owns its own transport vehicles. No external logistics companies involved.
- **No fixed production line** — work flows through logical stages (folding → grading → packing) but workers and material move freely within the open space.

The facility also serves as a **godown (warehouse)** for both incoming semi-finished goods and finished packed bales awaiting dispatch.

## The Three Processes

RG Faith runs three processes total, two in-house and one outsourced:

### 1. Weaving (In-house, out of scope)

Raw threads and yarns (both horizontal and main yarn) are fed into weaving machines to produce the first cloth. This happens at a separate facility and is **outside the scope** of this project.

### 2. Dyeing (Outsourced job work, partially in scope)

The woven cloth is sent out to external vendor mills for dyeing. RG Faith works with multiple mills:

| Mill Name | Notes |
|---|---|
| Kalapurna Mills | Frequent supplier. Has its own printed "Meter Report" form. |
| RSK Industries Pvt. Ltd. | Located at 168, Pirana Road, Piplaj, Ahmedabad. Uses "Ready Goods Report" form. |
| PSJC | Abbreviation — full name unknown |
| ATP | Abbreviation — full name unknown |
| BKT | Abbreviation — full name unknown |
| Shaim | — |
| Shyam | — |
| Shreeji | — |
| Om Shakthi | — |

The dyeing process itself is out of scope, but the **interfaces** are critical:
- **Outbound interface:** RG Faith assigns an MRL (Miroli) number when sending cloth to a vendor. This MRL number becomes the round-trip tracking identifier.
- **Inbound interface:** Vendor returns dyed cloth with a Gate Pass referencing the original MRL number. Material may return in partial shipments.

### 3. Finishing (In-house, primary scope)

This is the core of what we're documenting — everything that happens at Miroli from the moment dyed cloth returns from a vendor to the moment finished bales are dispatched to customers. The stages are:

```
INBOUND (receive dyed cloth from vendor)
    │
    ▼
FOLDING (unfold, measure every meter, record measurements)
    │
    ▼
GRADING (quality check, classify into grades)
    │
    ▼
PACKING PROGRAM (manager creates cutting/folding/branding instructions)
    │
    ▼
CUTTING & PACKING (cut to lengths, fold, brand stamp, box into bales)
    │
    ▼
DISPATCH (delivery form, bales go to customer)
```

Parallel to this main flow:
- **Packaging materials** — tracked separately (inward from vendors, consumption during packing)
- **Todiya** — reassignment/repacking of accumulated leftover material when a buyer is found
- **Not acceptable resolution** — informal issue/ticket workflow for rejected material sent back to mills
- **Decision pending** — lots awaiting quality decisions, can sit for extended periods

## Material Lifecycle and Inventory States

The material goes through the following **inventory states**, which are the heart of what the system needs to track:

### State 1: Grey (Unclassified)

All incoming material starts as **grey**. "Grey meters" is the default state for any fabric that has arrived at Miroli but has not yet been through folding and grading. The grey meter count comes from the vendor's Gate Pass and is trusted at face value — no re-verification on arrival.

Grey material can sit in this state for varying durations. Most lots move to folding within days, but some (especially those with quality concerns) can remain as grey/decision-pending for months or even years.

### State 2: Folded / Measured

After the folding station processes the material, every meter has been physically handled, unfolded, and measured. The **folding meters** are recorded and represent RG Faith's own measurement. At this point, the material transitions from a vendor-reported quantity to a facility-verified quantity.

### State 3: Graded

Quality inspection classifies the material into grades. This is where the material gets split:

| Grade | Unit | Disposition | Notes |
|---|---|---|---|
| **Fresh** | Meters | Ready for packing program | Best quality. Typically ~96-97% of a lot. |
| **Good Cut** | Metres | Accumulate for Todiya | Second grade. |
| **Fent** | Kilograms | Accumulate for Todiya | Lower grade. ~50% considered loss. |
| **Rags** | Kilograms | Accumulate for Todiya | Lower grade. |
| **Chindi** | Kilograms | Accumulate for Todiya | Lowest grade. 100% loss. |
| **Not Acceptable** | Meters | Send back to vendor | Rejected. Informal resolution process. |

**Critical concept — Chadat:** Fresh and Good Cut are measured in metres. Fent, Rags, and Chindi are measured in kilograms. The **Chadat** is a conversion factor between metres and kilograms, calculated for each specific lot. It's used to convert Fent, Rags, and Chindi from kg to metres for reporting, to determine the percentage breakdown of a lot and track loss.

### State 4: Packing Program Assigned

A packing program allocates graded material (typically Fresh) to specific cutting, folding, and branding instructions. In ~95% of cases, this is triggered by a sales order from head office. In ~5% of cases, the facility manager proactively creates a packing program to move inventory forward — converting graded material into finished bales so it's ready for dispatch when an order comes in. At this point, the material is committed and physically moved to the cutting area, but hasn't been cut/packed yet.

### State 5: Packed (Bale)

After cutting, folding, branding, and boxing, the material becomes a **bale** — the finished product unit. Each bale gets:
- A **Bale Number** (assigned at packing)
- A **Brand Stamp** (e.g., SSTM)
- A **Product Name** (e.g., Sportsman)
- A **Trade Number** (finished product SKU reference, e.g., S8072-58")
- A **Packing Slip** (computer-generated, one copy goes inside the bale)
- A **Bale Label** (attached externally)

### State 6: Dispatched

Bales leave the facility via a **Delivery Form** to the designated customer (identified by "Haste" — the party name).

## Key Identifiers

The material is tracked through several identifiers at different stages:

| Identifier | Created By | When | Purpose |
|---|---|---|---|
| **MRL Number** | RG Faith (Miroli) | When sending cloth to vendor for dyeing | Round-trip tracking. Links outbound grey cloth to inbound dyed cloth. |
| **Lot Number** | Vendor (mill) | During vendor's processing | Vendor's internal reference. Stays with material through all downstream processes at RG Faith. |
| **Gate Pass** | Vendor (mill) | When shipping back to RG Faith | Dispatch document with roll-by-roll measurements. Accompanies the truck. |
| **Bale Number** | RG Faith (Miroli) | At packing time | Identifies each finished bale. Physical label on the box. |
| **Trade Number** | RG Faith | At packing time | Finished product SKU reference. |

## Measurement Units

| What | Unit | Notes |
|---|---|---|
| Grey material (incoming) | Meters | From vendor's Gate Pass |
| Folded material | Meters | RG Faith's own measurement |
| Fresh grade | Meters | Primary output |
| Good Cut | Metres | Second grade, measured in metres |
| Fent, Rags, Chindi | Kilograms | Converted to metres via Chadat |
| Shrinkage | Meters (loss) | Grey meters minus finished meters |
| Chadat | Meters per kilogram | Lot-specific conversion factor |
| Finished bales | Pieces + meters | Pieces per bale and total meters per bale |
| Packaging materials | Various (units, kg, rolls) | Per SKU |

## Throughput and Scale

- **Annual capacity:** 1.4 crore meters (14 million meters)
- **Monthly (estimated):** ~1.17 lakh meters (~117,000 meters)
- **Bales packed per month:** ~1,296 (observed December 2025)
- **Average meters per bale:** ~90-110 meters (estimated from scan data)
- **Typical lot turnaround:** Within a week for normal lots
- **Decision-pending exceptions:** Can sit for months to years

## What the System Will Track

The project scope is an **inventory tracking system** for the Miroli facility. Three inventory domains:

1. **Grey material inventory** — what's been received from vendors, tracked by MRL number, lot number, and meters
2. **Stage-wise material inventory** — where material is in the process (grey → folded → graded → packing program assigned → packed → dispatched), how much, in meters or kg
3. **Packaging material inventory** — inward from vendors, current stock, consumption during packing

**Explicitly out of scope:**
- Financial data (pricing, billing, invoicing, credit notes)
- Sales order management
- Head office ERP integration (future import/export utility only)
- Weaving process
- Dyeing process (only the send/receive interfaces)

**Future scope (not for current phase):**
- Integration of dyeing process into the system
- Integration of weaving process into the system
- Cutting pattern calculation assistance
- No capacity expansion planned for the next few years

## Scan References

The following scanned documents from `00-inbox/rg faith scans.pdf` informed this observation:

| Page | Document | Relevance |
|---|---|---|
| 1 | Packed Bales List (Dec 2025) | Monthly output tracking, bale numbering |
| 4 | Packed Bales Stock Report (computer-generated) | Existing system output, product/grade inventory |
| 9 | Kalapurna Mills Meter Report | Vendor-side document format |
| 10 | RG Faith Delivery Form | Company structure, outward process |
| 12 | RSK Industries Ready Goods Report (Gate Pass) | Vendor-side document format, inbound reference |
| 17 | RG Faith Delivery Form (finished goods dispatch) | Multiple brands, bale details |
| 18 | Shree Shubhlaxmi Bale Label | Physical bale identification |
| 19 | Packing Slip (computer-generated) | System-generated output, bale tracking |

## Open Questions

1. ~~What is the exact address of the Miroli facility?~~ **RESOLVED:** New Block/Survey No. 514, Khata No. 879, Miroli, Taluka Daskroi, Ahmedabad 382425.
2. ~~Are there any seasonal patterns to throughput?~~ **RESOLVED:** No specific patterns. Design for peak at all times.
3. ~~How many total workers are employed at Miroli?~~ **RESOLVED:** ~50 workers involved in the processes we're covering. Multi-skilled — no dedicated roles per station.
4. ~~Are there plans to expand capacity?~~ **RESOLVED:** No capacity expansion planned for a few years. Plans to integrate dyeing and weaving into the system in the future.
5. ~~What is the full list of vendor mills?~~ **RESOLVED:** No data yet. They will input it as master data. User-configurable.
