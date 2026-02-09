---
title: "Process 03 — Inbound Receipt"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, inbound, grey, gate-pass, receipt]
---

# Process 03 — Inbound Receipt

## Overview

| Field | Value |
|---|---|
| **Purpose** | Receive dyed cloth returning from vendor mills, match it to the original MRL, record the arrival, and file the Gate Pass for downstream processing. |
| **Trigger** | Truck arrives from a vendor mill carrying dyed cloth and a Gate Pass. |
| **End condition** | Material stored at Miroli. Gate Pass filed. MRL updated with received metres. Inventory state = Grey. |
| **Frequency** | Multiple times per week. |
| **Typical duration** | 30–60 minutes per truck (unloading and filing). |

## Roles

| Role | Responsibility |
|---|---|
| Receiving workers (2–3) | Unload truck, store material on facility floor. |
| Supervisor / manager | Match shipment to existing MRL. File Gate Pass. Record avak (arrival) date. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Dyed cloth (semi-finished goods) | Vendor mill | Physical rolls/bundles on truck | Not counted or measured at this stage. |
| Gate Pass / Ready Goods Report | Vendor mill | Printed form (standard format) | Contains: lot number, roll-by-roll metres, grey metres, quality code, GSM, width. |
| MRL Number (pre-existing) | RG Faith records | Reference number | Created at outbound (Process 02). Used to match inbound to outbound. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Stored grey material | Miroli facility floor (waiting area) | Physical rolls/bundles | Awaiting folding station. |
| Filed Gate Pass | Paper file | Physical document | Referenced later during folding. |
| MRL receipt record | Internal records | Paper register / future system | Avak date, metres received, lot number, Gate Pass ref. |

## Process Steps

### Main Flow

```
START — RG Faith's truck returns from vendor mill
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Receive truck and Gate Pass      │
│    • RG Faith's own truck returns   │
│      from vendor with dyed cloth    │
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
│ 3. Match to MRL                     │
│    • Identify the MRL Number from   │
│      the Gate Pass or prior records │
│    • Link this inbound shipment to  │
│      the original outbound MRL     │
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
END — Material stored as Grey inventory.
      Awaiting folding station pickup.
```

### What Does NOT Happen at Receipt

- **No measurement** — Grey metres from Gate Pass accepted at face value.
- **No quality inspection** — Happens at folding/grading (Process 04/05).
- **No rejection** — Material is always accepted at intake.
- **No immediate processing** — Material waits until folding picks it up.

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

Each shipment creates its own receipt record against the same MRL. The system auto-calculates the pending balance (total sent minus total received).

### Exceptions

| Exception | How Handled |
|---|---|
| Material arrives without a Gate Pass | Contact vendor. Do not process until Gate Pass is received. |
| Cannot identify the MRL for the shipment | Manager matches from memory/paper records. System will provide MRL lookup. |
| Partial shipment (not all metres returned) | Record what's received. Pending balance tracked. Second shipment expected later. |

## State Transition

```
Sent to Vendor ──► Grey (received at Miroli, not yet processed)
```

## Key Data Captured

| Field | Source | Description |
|---|---|---|
| MRL Number | Pre-existing (from outbound) | Links inbound to outbound. |
| Avak Date | Recorded at receipt | Date material arrived at Miroli. |
| Lot Number | From Gate Pass (vendor-assigned) | Vendor's internal reference. Stays with material through all stages. |
| Grey Metres | From Gate Pass | Total metres in this shipment. Trusted at face value. |
| Quality Code | From Gate Pass | Inbound quality attribute (e.g., 44x45P6). User-configurable. |
| GSM | From Gate Pass | Grams per square metre — fabric weight. |
| Width | From Gate Pass | Fabric width (e.g., 58"). |
| Rolls / Pieces | From Gate Pass | Number of physical rolls in shipment. |
| Gate Pass Reference | From Gate Pass | Vendor's dispatch document number. |

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | [02 — Outbound to Vendor](02-outbound-to-vendor.md) | MRL created at outbound; this process receives against it. |
| **Downstream** | [04 — Folding & Measurement](04-folding-measurement.md) | Grey material picked up by folding team for processing. |

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
