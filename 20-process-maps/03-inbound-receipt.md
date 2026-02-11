---
title: "Process 03 — Inbound Receipt"
status: draft
created: 2026-02-07
updated: 2026-02-11
tags: [process, inbound, receipt, gate-pass, mrl]
---

# Process 03 — Inbound Receipt

## Overview

| Field | Value |
|---|---|
| **Purpose** | Receive finished material returning from vendor mills, generate or match the MRL, record the arrival, capture vendor-reported pending greige balance, and file the Gate Pass for downstream processing. |
| **Trigger** | Truck arrives from a vendor mill carrying finished material and a Gate Pass. |
| **End condition** | Material stored at Miroli. Gate Pass filed. MRL generated (first receipt) or matched (subsequent receipt). Inventory state = Received. |
| **Frequency** | Multiple times per week. |
| **Typical duration** | 30–60 minutes per truck (unloading and filing). |

## Roles

| Role | Responsibility |
|---|---|
| Receiving workers (2–3) | Unload truck, store material on facility floor. |
| Supervisor / manager | Generate new MRL (first receipt) or match to existing MRL (subsequent receipt). File Gate Pass. Record avak (arrival) date. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Finished material (dyed cloth) | Vendor mill | Physical rolls/bundles on truck | Not counted or measured at this stage. |
| Gate Pass / Ready Goods Report | Vendor mill | Printed form (standard format) | Contains: lot number, roll-by-roll metres, metres, quality code, GSM, width, pending greige balance. |
| MRL Number (if subsequent receipt) | RG Faith records | Reference number | Only exists if this is a subsequent receipt against an existing MRL. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Stored received material | Miroli facility floor (waiting area) | Physical rolls/bundles | Awaiting folding station. |
| Filed Gate Pass | Paper file | Physical document | Referenced later during folding. |
| MRL record | Internal records | Paper register / future system | MRL generated (first receipt) or updated (subsequent). Avak date, metres received, lot number, Gate Pass ref, vendor-reported pending greige balance. |

## Process Steps

### Main Flow

```
START — RG Faith's truck returns from vendor mill
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Receive truck and Gate Pass      │
│    • RG Faith's own truck returns   │
│      from vendor with finished      │
│      material (dyed cloth)          │
│    • Gate Pass document collected   │
│    • No counting or measurement     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Unload and store material        │
│    • Unload rolls/bundles           │
│    • Store on open facility floor   │
│    • No inspection at this stage    │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Generate or match MRL            │
│    • FIRST RECEIPT: Generate a new  │
│      MRL Number for this material   │
│    • SUBSEQUENT RECEIPT: Identify   │
│      the existing MRL from the Gate │
│      Pass or prior records and      │
│      match this shipment to it      │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Record Avak (arrival)            │
│    • Record avak date               │
│    • Record metres received         │
│      (from Gate Pass — trusted)     │
│    • Record lot number (vendor's)   │
│    • Record Gate Pass reference     │
│    • Record vendor-reported pending │
│      greige balance (from Gate Pass)│
│    • Update MRL with received qty   │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 5. File Gate Pass                   │
│    • Gate Pass filed in paper       │
│      records                        │
│    • Will be retrieved at folding   │
└──────────────┬──────────────────────┘
               │
               ▼
END — Material stored as Received inventory.
      Awaiting folding station pickup.
```

### What Does NOT Happen at Receipt

- **No measurement** — Metres from Gate Pass accepted at face value.
- **No quality inspection** — Quality is assessed later during packing execution (gradation).
- **No rejection** — Material is always accepted at intake.
- **No immediate processing** — Material waits until folding picks it up.
- **No outbound tracking** — The system starts at inbound receipt. There is no outbound process in the system. Pending greige balance is a vendor-reported note on the Gate Pass, not a system-tracked outbound.

### Partial Shipments

A single MRL may return in multiple shipments:

```
MRL 526 — 6,000 metres sent to vendor
  │
  ├── Shipment 1: 4,000 metres received (Avak Date: Day X)
  │
  └── Shipment 2: 2,000 metres received (Avak Date: Day Y)
      │
      └── Pending balance: 0 metres (complete)
```

Each shipment creates its own receipt record against the same MRL. The vendor-reported pending greige balance on the Gate Pass indicates what remains with the vendor.

### Exceptions

| Exception | How Handled |
|---|---|
| Material arrives without a Gate Pass | Contact vendor. Do not process until Gate Pass is received. |
| Cannot identify the MRL for a subsequent shipment | Manager matches from memory/paper records. System will provide MRL lookup. |
| Partial shipment (not all metres returned) | Record what's received. Pending balance tracked. Second shipment expected later. |

## State Transition

```
[Not in system] ──► Received (MRL generated at first receipt, or matched on subsequent receipt)
```

## Key Data Captured

| Field | Source | Description |
|---|---|---|
| MRL Number | Generated at first receipt; matched on subsequent | System-generated identifier for the lot. The MRL is created at this inbound step (not at outbound). |
| Avak Date | Recorded at receipt | Date material arrived at Miroli. |
| Lot Number | From Gate Pass (vendor-assigned) | Vendor's internal reference. Stays with material through all stages. |
| Received Metres | From Gate Pass | Total metres in this shipment. Trusted at face value. |
| Quality Code | From Gate Pass | Inbound quality attribute (e.g., 44x45P6). User-configurable. |
| GSM | From Gate Pass | Grams per square metre — fabric weight. |
| Width | From Gate Pass | Fabric width (e.g., 58"). |
| Rolls / Pieces | From Gate Pass | Number of physical rolls in shipment. "Roll" is the system term (may physically be a roll or lump). |
| Gate Pass Reference | From Gate Pass | Vendor's dispatch document number. |
| Vendor-reported Pending Greige Balance | From Gate Pass | Greige metres still pending with the vendor. A vendor-reported note, not verified by the system. |

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | Vendor mill (external) | Vendor dyes the greige material and returns it as finished material. No outbound tracking in the system. |
| **Downstream** | [04 — Folding & Measurement](04-folding-measurement.md) | Received material picked up by folding team for processing. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Paper register (current) | Track arrivals, MRL matching. |
| Gate Pass (vendor document) | Primary reference document, filed on arrival. |
| Future system | Digital MRL receipt with Gate Pass data capture. |

## Known Issues

| Issue | Impact |
|---|---|
| No system to track inbound receipts | Risk of losing track of partial shipments and delayed MRL matching. |
| Gate Pass data not digitised | Cannot report on inbound volume, vendor performance, or pending lots. |
| No visibility into what's in transit | Cannot plan folding workload based on expected arrivals. |
| Partial shipments hard to reconcile | Pending metres can be forgotten. |
