---
title: "Inbound Process — Grey Material Receipt"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [observation, inbound, grey, gate-pass, mrl, vendor]
---

# Inbound Process — Grey Material Receipt

## Location / Station

- **Area:** Miroli facility — receiving/unloading area
- **Station/Cell:** No fixed station. Open area where trucks are unloaded.
- **Address/Building:** Miroli facility, Ahmedabad

## Activity

When dyed cloth returns from vendor mills, it is received at the Miroli facility. The inbound process captures the arrival, assigns tracking identifiers, and files the accompanying documentation. No inspection, measurement, or rejection happens at this stage — the material is simply taken in and stored until the folding station is ready to process it.

## The MRL Number — Origin and Purpose

The MRL (Miroli) number is the central tracking identifier for the entire material lifecycle. It is important to understand that the MRL number is **not created at inbound receipt**. It is created **earlier**, when RG Faith sends grey cloth out to a vendor for dyeing.

### MRL Lifecycle

```
1. RG Faith sends grey cloth to vendor for dyeing
   └── MRL Number assigned at this point (outbound)

2. Vendor processes the cloth (dyeing)
   └── Vendor assigns their own Lot Number

3. Vendor returns dyed cloth to RG Faith
   └── Gate Pass references the original MRL Number
   └── This is the "inbound" event we're documenting here

4. Material is tracked through all stages using the MRL Number
   └── Folding, grading, packing, dispatch
```

The MRL number is therefore a **round-trip identifier** — it links what was sent out to what came back. When a truck arrives at Miroli, the receiving team matches the incoming shipment to an existing MRL number.

### Partial Shipments

A single MRL may return in multiple shipments. For example:
- MRL 526 was sent out as 6,000 meters
- First shipment returns with 4,000 meters
- Second shipment (weeks later) returns with the remaining 2,000 meters

The system needs to track:
- **Total meters sent** (per MRL)
- **Meters received per shipment**
- **Pending balance** (auto-calculated: sent minus total received)

Most of the time, one shipment covers the entire MRL. Partial returns are the exception but do occur regularly enough to require proper tracking.

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Dyed cloth (semi-finished goods) | Vendor mill (Kalapurna, RSK, PSJC, ATP, BKT, Shaim, Shyam, Shreeji, Om Shakthi, etc.) | Physical rolls/bundles on a truck | Arrives in bulk. Not counted or measured at this stage. |
| Gate Pass / Ready Goods Report | Vendor mill | Printed form (standard format across mills) | Accompanies the truck. Contains roll-by-roll data, grey meters, quality code, lot number. See detailed breakdown below. |
| MRL Number (pre-existing) | RG Faith's own records | Reference number | Created when the cloth was originally sent out for dyeing. Used to match inbound to outbound. |

## The Gate Pass — Detailed Breakdown

The Gate Pass (also called "Ready Goods Report" by some mills) is the **primary inbound document**. It is a standard-format printed form that every vendor mill provides when shipping goods back to RG Faith. One copy accompanies the truck; the mill retains a copy.

### Gate Pass Contents (from scan page 12 — RSK Industries example)

| Field | Example Value | Purpose |
|---|---|---|
| Date | 18/1/2026 | Date the mill dispatched the goods |
| Pcs (Bales) | 58 | Number of physical rolls/pieces in the shipment |
| Quality | 44x45P6 | Inbound quality code — describes the type of cloth. This is a **semi-finished goods quality attribute**, not the final product brand. User-configurable in the system. |
| Lot No | 3402 | Vendor's own lot identifier. Stays with the material through all downstream processes. |
| GSM | 192 | Grams per Square Meter — fabric weight/density. One of many possible SKU attributes. |
| Width | 58" | Fabric width. Another SKU attribute. |
| Grey Mtr | 6822 | Total grey meters in this shipment. **Trusted at face value** — no re-verification by RG Faith. |
| Ready Mtr | 6281 | Meters after the vendor's processing (dyeing). |
| Shortage/Shrinkage | -7,931 | Difference between grey and ready meters. Tracked for visibility, no commercial penalties. |
| Party | R.G. Faith | Confirms the shipment is destined for RG Faith. |
| L.R. No | 96005x58 | Lorry Receipt number — transport reference. |
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
A truck from a vendor mill arrives at Miroli with dyed cloth and a Gate Pass document.

### Step 2: Unload and store
The material is unloaded and stored in the open area. No counting, no measurement, no inspection at this point.

### Step 3: File the Gate Pass
The Gate Pass is taken and filed. It is not entered into any system (there is no system at the factory currently). It will be referenced later when the folding station begins processing this lot.

### Step 4: Match to MRL
The incoming shipment is matched to an existing MRL number — the one that was assigned when this cloth was originally sent out for dyeing. This linkage is currently done manually from memory or paper records.

### What does NOT happen at receipt:
- **No measurement** — grey meters from the Gate Pass are accepted as-is
- **No quality inspection** — that happens at the folding station
- **No rejection** — material is always accepted at intake
- **No system entry** — currently paper-only
- **No immediate processing** — material waits until folding station picks it up

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Stored semi-finished goods | Miroli facility floor (waiting area) | Physical rolls/bundles | Awaiting processing at folding station |
| Filed Gate Pass | Paper file at Miroli | Physical document | Referenced later during folding and grading |
| MRL record update (conceptual) | Internal tracking | Paper register / future system | Records that this MRL has received X meters back |

## People

| Role | Count | Shift/Schedule | Notes |
|---|---|---|---|
| Receiving workers | 2-3 | As trucks arrive | Handle unloading and storage |
| Supervisor / manager | 1 | Oversight | Matches shipment to MRL, files Gate Pass |

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
| Paper registers | Tracking MRL numbers and arrivals | No digital system at factory |
| Gate Pass (vendor document) | Reference document for inbound material | Filed on arrival, referenced at folding |

## Handoffs

- **Comes from:** Vendor mill (external). The mill completes dyeing and dispatches back to RG Faith.
- **Goes to:** Folding station (internal). Material sits in storage until the folding team picks it up for processing.

## The Vendor Relationship

RG Faith works with 9+ vendor mills for dyeing. Key characteristics of these relationships:

- **High trust** — Grey meter counts from vendors are accepted without verification. No re-measurement at intake.
- **No penalties** — Shrinkage and quality issues are tracked for visibility but do not trigger financial penalties or credit notes.
- **Long-standing** — The vendor relationships are mature and stable.
- **Standard documentation** — All vendors provide a Gate Pass / Ready Goods Report in a standard format.
- **Vendor picks up rejects** — If material is later graded as "Not Acceptable," the vendor is expected to arrange pickup. This is handled through an informal back-and-forth process (see observation on exceptions).

## Problems and Workarounds

| Problem | Frequency | Current Workaround | Impact |
|---|---|---|---|
| No system to track inbound receipts | Always | Paper registers and memory | Risk of losing track of partial shipments, delayed matching to MRL |
| Partial shipments hard to reconcile | Occasional | Manual tracking of what's outstanding | Pending meters can be forgotten or lost |
| Gate Pass data not digitized | Always | Physical filing only | Cannot easily report on inbound volume, vendor performance, or pending lots |
| No visibility into what's in transit | Always | Phone calls to vendor | Cannot plan folding station workload based on expected arrivals |

## Design Implications for the System

### Must Have
1. **MRL master record** — Created when cloth is sent to vendor. Records: vendor name, quality code, total grey meters sent, date sent.
2. **Inbound receipt record** — Logged when material returns. References the MRL. Records: avak date, meters received, lot number (from vendor), Gate Pass reference.
3. **Pending balance calculation** — Auto-calculated: total sent minus total received across all shipments for an MRL.
4. **Gate Pass data capture** — Fields for: vendor, lot number, quality code, grey meters, rolls/pieces count, and configurable SKU attributes (GSM, width, tone, etc.).

### Nice to Have
5. **Multi-shipment tracking** — Show all receipts against a single MRL with running totals.
6. **Vendor master** — List of all mills with contact details and capabilities.
7. **Inbound dashboard** — View of all pending MRLs (sent but not yet returned), recently received lots, and lots awaiting folding.

### Not Needed
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

1. ~~When an MRL is created, what information is recorded?~~ **RESOLVED:** Vendor name + meters sent. System can add configurable attributes later.
2. ~~Is there a standard naming convention for MRL numbers?~~ **RESOLVED:** System will use its own numbering scheme.
3. ~~How many inbound shipments per week?~~ **RESOLVED:** Unknown. Not critical for design.
4. ~~Is there a physical receiving log?~~ **RESOLVED:** Yes, a physical register exists. Most of the relevant data is captured in the scans. Our system replaces it.
5. ~~Does the transport company provide documentation?~~ **RESOLVED:** No. Transport is owned by RG Faith. Trusted parties, no external logistics docs needed.
