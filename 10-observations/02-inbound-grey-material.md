---
title: "Inbound Process — Finished Material Receipt"
status: draft
created: 2026-02-07
updated: 2026-02-11
tags: [observation, inbound, finished-material, gate-pass, mrl, vendor]
---

# Inbound Process — Finished Material Receipt

## Location / Station

- **Area:** Miroli facility — receiving/unloading area
- **Station/Cell:** No fixed station. Open area where trucks are unloaded.
- **Address/Building:** Miroli facility, Ahmedabad

## Activity

When finished (dyed) cloth returns from vendor mills, it is received at the Miroli facility. The inbound process captures the arrival, generates an MRL number (on first receipt), and files the accompanying documentation. No inspection, measurement, or rejection happens at this stage — the material is simply taken in and stored until the folding station is ready to process it.

## The MRL Number — Origin and Purpose

The MRL (Miroli) number is the central tracking identifier for a lot through all processing stages. The MRL number is **created at inbound receipt** — specifically, it is generated when the first GRN (Goods Receipt Note) is recorded for a lot.

### MRL Lifecycle

```
1. RG Faith sends greige cloth to vendor for dyeing
   └── Greige Challan No / L.R. No assigned (outbound — NOT tracked in the system)

2. Vendor processes the cloth (dyeing)
   └── Vendor assigns their own Lot Number

3. Vendor returns finished (dyed) cloth to RG Faith
   └── Gate Pass accompanies the shipment
   └── Gate Pass notes: metres returned, total greige metres sent, pending balance
   └── On first receipt: MRL Number generated (this is the "birth" of the MRL)
   └── On subsequent receipts: matched to existing MRL Number

4. Material is tracked through all stages using the MRL Number
   └── Folding, classification, packing, dispatch
```

The MRL number is therefore an **inward identifier** — it is born when material first arrives at Miroli. The system does not track the outbound dispatch of greige cloth to vendors.

> **Note on pending greige metres:** The vendor's Gate Pass carries a note of how much greige was originally sent and how much is still pending (e.g., "You sent 6,000 metres, I'm returning 2,000 metres, 4,000 metres remaining"). This is captured as a vendor-reported note — not computed from an outbound record.

### Partial Shipments

A single lot may return in multiple shipments. For example:
- Vendor received 6,000 metres of greige
- First shipment returns with 2,000 metres of finished material → MRL generated
- Second shipment (weeks later) returns with 2,000 metres → matched to existing MRL
- Gate Pass each time notes the remaining pending balance

The system needs to track:
- **Metres received per shipment**
- **Vendor-reported pending balance** (from Gate Pass)
- **Total metres received to date** (sum of all shipments for this MRL)

Most of the time, one shipment covers the entire lot. Partial returns are the exception but do occur regularly enough to require proper tracking.

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Finished cloth (dyed material) | Vendor mill (Kalapurna, RSK, PSJC, ATP, BKT, Shaim, Shyam, Shreeji, Om Shakthi, etc.) | Physical rolls/bundles on a truck | Arrives in bulk. Not counted or measured at this stage. A roll may physically be a roll or a lump (badly folded piece). |
| Gate Pass / Ready Goods Report | Vendor mill | Printed form (standard format across mills) | Accompanies the truck. Contains roll-by-roll data, metres, quality code, lot number, and vendor's note of total greige sent + pending balance. See detailed breakdown below. |

## The Gate Pass — Detailed Breakdown

The Gate Pass (also called "Ready Goods Report" by some mills) is the **primary inbound document**. It is a standard-format printed form that every vendor mill provides when shipping goods back to RG Faith. One copy accompanies the truck; the mill retains a copy.

### Gate Pass Contents (from scan page 12 — RSK Industries example)

| Field | Example Value | Purpose |
|---|---|---|
| Date | 18/1/2026 | Date the mill dispatched the goods |
| Pcs (Bales) | 58 | Number of physical rolls/pieces in the shipment |
| Quality | 44x45P6 | Inbound quality code — describes the type of cloth. User-configurable in the system. |
| Lot No | 3402 | Vendor's own lot identifier. Stays with the material through all downstream processes. |
| GSM | 192 | Grams per Square Meter — fabric weight/density. One of many possible SKU attributes. |
| Width | 58" | Fabric width. Another SKU attribute. |
| Grey Mtr | 6822 | Total greige metres originally sent to vendor (vendor-reported note). |
| Ready Mtr | 6281 | Metres of finished material in this shipment. |
| Shortage/Shrinkage | -7,931 | Difference between greige and ready metres. Tracked for visibility, no commercial penalties. |
| Party | R.G. Faith | Confirms the shipment is destined for RG Faith. |
| L.R. No | 96005x58 | Lorry Receipt / Greige Challan reference — outbound transport reference. |
| Roll-by-roll data | Roll No, Meter, Weight | Individual roll measurements. Detailed breakdown per physical roll. |

### Gate Pass from Other Mills

Different mills use slightly different formats but contain the same core data. For example:

**Kalapurna Mills Meter Report (scan page 9):**
- Pre-printed form with Hindi header ("Shri Mahaveeraya Namah")
- Fields: Lot No, Date, L.P. No, and a numbered grid of "Tayar Meter" (Ready Meter) values per roll
- Simpler format than RSK but captures the same essential data: lot number, per-roll meters, totals

The system should be flexible enough to capture Gate Pass data regardless of the vendor's specific format — the core fields are universal.

## What Happens at Receipt

The inbound process at Miroli is deliberately simple:

### Step 1: Truck arrives
A truck (RG Faith's own transport) arrives at Miroli with finished cloth and a Gate Pass document.

### Step 2: Unload and store
The material is unloaded and stored in the open area. No counting, no measurement, no inspection at this point.

### Step 3: File the Gate Pass
The Gate Pass is taken and filed. It will be referenced when recording the inbound in the system and later at the folding station.

### Step 4: Record inbound receipt and generate/match MRL
- **First shipment for a lot:** A new MRL number is generated. The system records: vendor, lot number, metres received, quality code, Gate Pass data, avak date, and the vendor's note of total greige metres and pending balance.
- **Subsequent shipment for an existing lot:** Matched to the existing MRL. Additional metres added. Pending balance updated from vendor's Gate Pass.

### What does NOT happen at receipt:
- **No measurement** — metres from the Gate Pass are accepted as-is
- **No quality inspection** — that happens later during packing (gradation)
- **No rejection** — material is always accepted at intake
- **No immediate processing** — material waits until folding station picks it up

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Stored finished material | Miroli facility floor (waiting area) | Physical rolls/bundles | Awaiting processing at folding station |
| Filed Gate Pass | Paper file at Miroli | Physical document | Referenced later during folding |
| MRL record (new or updated) | System | Digital record | New MRL on first receipt; updated with additional metres on subsequent receipts |

## People

| Role | Count | Shift/Schedule | Notes |
|---|---|---|---|
| Receiving workers | 2-3 | As trucks arrive | Handle unloading and storage |
| Supervisor / manager | 1 | Oversight | Records inbound, generates/matches MRL, files Gate Pass |

## Timing

- **Frequency:** Multiple times per week. Depends on how many lots are out for dyeing and vendor processing times.
- **Duration:** Unloading a truck takes roughly 30-60 minutes (estimated from volume — 58 rolls per shipment is typical).
- **Schedule:** During working hours. Not shift-based for receiving.
- **Peak/Off-peak:** Receiving volume follows dyeing output, which may have seasonal patterns (TBD).

## Equipment and Tools

| Equipment | Purpose | Notes |
|---|---|---|
| Truck / transport vehicle | Delivers goods from vendor | RG Faith's own vehicles. Vendor confirms readiness, RG Faith sends transport. |
| Storage area | Holds unprocessed material | Part of the open facility floor |

## Systems

| System | Used For | Notes |
|---|---|---|
| Paper registers | Tracking MRL numbers and arrivals | No digital system at factory currently |
| Gate Pass (vendor document) | Reference document for inbound material | Filed on arrival, referenced at folding |

## Handoffs

- **Comes from:** Vendor mill (external). The mill completes dyeing and dispatches back to RG Faith.
- **Goes to:** Folding station (internal). Material sits in storage until the folding team picks it up for processing.

## The Vendor Relationship

RG Faith works with 9+ vendor mills for dyeing. Key characteristics of these relationships:

- **High trust** — Metre counts from vendors are accepted without verification. No re-measurement at intake.
- **No penalties** — Shrinkage and quality issues are tracked for visibility but do not trigger financial penalties or credit notes.
- **Long-standing** — The vendor relationships are mature and stable.
- **Standard documentation** — All vendors provide a Gate Pass / Ready Goods Report in a standard format.
- **Vendor picks up rejects** — If material is later graded as "Not Acceptable," the vendor is expected to arrange pickup. This is handled through an informal back-and-forth process (see observation on exceptions).

## Problems and Workarounds

| Problem | Frequency | Current Workaround | Impact |
|---|---|---|---|
| No system to track inbound receipts | Always | Paper registers and memory | Risk of losing track of partial shipments |
| Partial shipments hard to reconcile | Occasional | Manual tracking of what's outstanding | Pending metres can be forgotten or lost |
| Gate Pass data not digitized | Always | Physical filing only | Cannot easily report on inbound volume, vendor performance, or pending lots |
| No visibility into what's in transit | Always | Phone calls to vendor | Cannot plan folding station workload based on expected arrivals |

## Design Implications for the System

### Must Have
1. **MRL record** — Generated at first inbound receipt (GRN). Records: vendor name, quality code, lot number, avak date, metres received. Subsequent shipments add to the same MRL.
2. **Inbound receipt record** — Logged per shipment. References the MRL. Records: avak date, metres received, lot number (from vendor), Gate Pass reference, vendor-reported pending greige balance.
3. **Pending balance visibility** — Display vendor-reported pending balance from Gate Pass. Updated on each subsequent receipt.
4. **Gate Pass data capture** — Fields for: vendor, lot number, quality code, ready metres, rolls/pieces count, greige metres (vendor-reported), and configurable SKU attributes (GSM, width, etc.).

### Nice to Have
5. **Multi-shipment tracking** — Show all receipts against a single MRL with running totals.
6. **Vendor master** — List of all mills with contact details and capabilities.
7. **Inbound dashboard** — View of recently received lots and lots awaiting folding.

### Not Needed
- Outbound tracking (greige dispatch to vendor is not in system scope)
- Purchase order system (explicitly declined by RG Faith)
- Inbound quality inspection workflow (no inspection at receipt)
- Approval/rejection at intake (everything is accepted)
- Financial tracking on inbound (no pricing, invoicing)

## Photos / Diagrams

Relevant scan pages from `00-inbox/rg faith scans.pdf`:
- **Page 9:** Kalapurna Mills Meter Report — mill-side document format
- **Page 12:** RSK Industries Ready Goods Report (Gate Pass) — primary inbound reference document

## Raw Notes

From `00-inbox/notes.md`:
> "When material comes in, we're tracking everything. That includes both the packaging material and the main semi-finished goods."
>
> "A truck arrives with a reference document listing what was originally sent out for dyeing and what's now being returned. Everything is measured in meters."
>
> "Material comes back in partial shipments as it gets processed."
>
> "Once it comes in, it's not measured immediately. It's just taken in. There's no rejection at this stage. We just have the reference number."

## Open Questions

1. ~~When an MRL is created, what information is recorded?~~ **RESOLVED:** Generated at first GRN. Vendor name + metres received + lot number + quality code + avak date. Vendor's Gate Pass also notes total greige sent and pending balance.
2. ~~Is there a standard naming convention for MRL numbers?~~ **RESOLVED:** System will use its own numbering scheme. FY prefix + code generation noted for implementation time.
3. ~~How many inbound shipments per week?~~ **RESOLVED:** Unknown. Not critical for design.
4. ~~Is there a physical receiving log?~~ **RESOLVED:** Yes, a physical register exists. Our system replaces it.
5. ~~Does the transport company provide documentation?~~ **RESOLVED:** No. Transport is owned by RG Faith. Trusted parties, no external logistics docs needed.
