---
title: "Process 02 — Outbound to Vendor"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, outbound, vendor, mrl, dyeing]
---

# Process 02 — Outbound to Vendor

## Overview

| Field | Value |
|---|---|
| **Purpose** | Send grey (woven) cloth to external vendor mills for dyeing, and assign the MRL Number that tracks the material through its entire lifecycle. |
| **Trigger** | Woven cloth is ready for dyeing (weaving process complete). |
| **End condition** | Cloth dispatched to vendor mill. MRL Number assigned and recorded. |
| **Frequency** | Regular — multiple lots sent out per week. |
| **Typical duration** | Same-day (preparation and dispatch). |

## Roles

| Role | Responsibility |
|---|---|
| Facility manager / supervisor | Decides which cloth to send, selects vendor, assigns MRL Number. |
| Workers | Load cloth onto transport. |
| Transport team | RG Faith's own vehicles deliver to vendor. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Woven grey cloth | Weaving process (out of scope) | Physical rolls | Ready for dyeing. |
| Vendor selection | Manager's decision | N/A | Choice of which mill to send to (Kalapurna, RSK, PSJC, ATP, BKT, Shaim, Shyam, Shreeji, Om Shakthi, etc.). |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Dispatched cloth | Vendor mill | Physical rolls on truck | Cloth leaves Miroli for dyeing. |
| MRL Number | Internal records | Paper register / future system | Round-trip tracking identifier. Created at this point. |
| Outbound record | Internal records | Paper register / future system | Vendor name, MRL number, metres sent, date sent, quality code. |

## Process Steps

### Main Flow

```
START
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Select cloth for dyeing          │
│    • Identify grey woven cloth      │
│      ready for the dyeing process   │
│    • Determine quality code / type  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Select vendor mill               │
│    • Choose from available mills    │
│    • Based on capacity, suitability │
│      and relationship               │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Assign MRL Number                │
│    • Create a new MRL Number        │
│    • Record: MRL number, vendor     │
│      name, total metres sent,       │
│      date, quality code             │
│    ★ This is the origin of the MRL  │
│      — the central tracking ID      │
│      for the material lifecycle     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Load and dispatch                │
│    • Load cloth onto RG Faith's     │
│      own transport vehicle          │
│    • Dispatch to vendor mill        │
└──────────────┬──────────────────────┘
               │
               ▼
END — Cloth at vendor. MRL created.
```

### Exceptions

| Exception | How Handled |
|---|---|
| Vendor cannot accept the lot (capacity) | Manager selects a different mill. |
| Partial send (only part of the cloth goes to one vendor) | Multiple MRLs created — one per vendor/shipment. |

## State Transition

```
[Not in system] ──► Sent to Vendor (MRL assigned)
```

## Key Data Captured

| Field | Description |
|---|---|
| MRL Number | Unique identifier created at this step. Round-trip tracking ID. |
| Vendor / Mill | Which external mill receives the cloth. |
| Grey metres sent | Total metres dispatched under this MRL. |
| Date sent | When the cloth was dispatched to the vendor. |
| Quality code | Type/quality of the grey cloth being sent. |

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | Weaving (out of scope) | Provides the grey woven cloth. |
| **Downstream** | [03 — Inbound Receipt](03-inbound-receipt.md) | Vendor returns dyed cloth referencing this MRL. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Paper register (current) | Record MRL number and outbound details. |
| Future system | Digital MRL creation with vendor, metres, date. |

## Known Issues

| Issue | Impact |
|---|---|
| No digital tracking of what's been sent to vendors | Difficult to know total outstanding metres at all vendors at any given time. |
| Pending balance (sent minus received) not auto-calculated | Partial returns hard to reconcile. |
| No visibility into vendor processing status | Cannot predict when dyed cloth will return. |
