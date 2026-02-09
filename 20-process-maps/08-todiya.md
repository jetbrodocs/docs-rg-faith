---
title: "Process 08 — Todiya (Leftover Repacking)"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, todiya, toria, leftover, accumulation, repacking]
---

# Process 08 — Todiya (Leftover Repacking)

## Overview

| Field | Value |
|---|---|
| **Purpose** | Reassign and repack accumulated leftover material (Good Cut, Fent, Rags, Chindi) when a buyer is found, transforming accumulated waste stock into saleable bales. |
| **Trigger** | Sales team finds a buyer for accumulated leftover stock. |
| **End condition** | Todiya bales packed and dispatched. Accumulation stock reduced. |
| **Frequency** | Periodic — when enough leftovers accumulate and a buyer is available. |
| **Typical duration** | Same as regular packing — depends on quantity. |

## Context

"Todiya" (or "Toria") comes from the Hindi/Gujarati word for "breaking." Historically, this involved physically breaking open existing bales to repackage. Today, it is more of a **software/accounting operation** — inventory is reassigned in records, though some physical repacking may still occur.

## Roles

| Role | Responsibility |
|---|---|
| Sales team | Finds a buyer for leftover stock. (Out of scope for the system.) |
| Facility manager | Creates the Todiya Packing Program. |
| Cutting/packing workers | Execute the repacking. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Accumulated Good Cut | Accumulation area | Physical fabric (kg) | From cutting waste across multiple packing programs. |
| Accumulated Fent | Accumulation area | Physical fabric (kg) | From grading and cutting waste. |
| Accumulated Rags | Accumulation area | Physical fabric (kg) | From grading and cutting waste. |
| Accumulated Chindi | Accumulation area | Physical fabric (kg) | Waste material. 100% loss. |
| Buyer requirements | Sales team | Verbal | What the Todiya buyer wants. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Todiya bales | Dispatch area → Customer | Physical boxes | Packed leftover material for the buyer. |
| Updated accumulation stock | System records | Updated quantities | Reduced by amount packed/dispatched. |

## Process Steps

### The Accumulation Cycle

```
Normal packing programs produce cutting waste
  │
  ▼
┌─────────────────────────────────────┐
│ ACCUMULATION AREA                   │
│                                     │
│ Good Cut:  +2.3 kg (from Program A) │
│            +1.8 kg (from Program B) │
│            +3.1 kg (from Program C) │
│            ────────                 │
│            = 7.2 kg accumulated     │
│                                     │
│ Fent:      +4.5 kg (from grading)   │
│            +2.1 kg (from cutting)   │
│            ────────                 │
│            = 6.6 kg accumulated     │
│                                     │
│ (Continues growing over weeks/months│
│  until enough volume for a sale)    │
└─────────────────────────────────────┘
```

### The Todiya Packing Flow

```
START — Buyer found for accumulated leftovers
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Assess available stock           │
│    • Check accumulated quantities   │
│      by grade (G/C, Fent, Rags,     │
│      Chindi)                        │
│    • May span material from         │
│      multiple original MRLs         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Create Todiya Packing Program    │
│    • Marked as Todiya type          │
│    • Material source: accumulated   │
│      stock (not a freshly graded    │
│      lot)                           │
│    • May mix grades in one bale     │
│      (e.g., "G/C + Fent")          │
│    • May combine material from      │
│      multiple MRLs                  │
│    • Specific instructions per      │
│      buyer's requirements           │
│    • Example note: "Good cut only!" │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Execute packing                  │
│    • Same physical process as       │
│      regular packing (Process 06)   │
│    • Cut, fold, brand, box          │
│    • Assign bale numbers            │
│    • Generate packing slips         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Update accumulation stock        │
│    • Reduce accumulated quantities  │
│      by what was packed             │
│    • Track which MRLs contributed   │
│      to the Todiya bales            │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 5. Dispatch to Todiya buyer         │
│    • Same dispatch process as       │
│      regular orders (Process 07)    │
│    • Delivery Form created          │
│    • Todiya account per party       │
│      may be tracked                 │
└──────────────┬──────────────────────┘
               │
               ▼
END — Todiya bales dispatched.
      Accumulation stock reduced.
```

### Todiya vs Regular Packing Program

| Aspect | Regular (Process 06) | Todiya (Process 08) |
|---|---|---|
| Material source | Fresh-graded lot | Accumulated leftovers |
| Trigger | Sales order (~95%) or proactive (~5%) | Buyer found for leftovers |
| Grades used | Fresh only | Good Cut, Fent, Rags (may be mixed) |
| MRL reference | Single MRL / lot | May combine multiple MRLs |
| Grade mixing | Never | Often ("G/C + Fent" in one bale) |
| Example | Scan page 13 | Scan page 14 |

### Exceptions

| Exception | How Handled |
|---|---|
| Accumulated stock insufficient for buyer's order | Wait for more to accumulate, or negotiate smaller quantity. |
| Buyer wants only one grade (e.g., "Good cut only!") | Todiya program specifies grade filter. |
| Material from too many MRLs — hard to reconcile | Todiya programs may reference "Lot Pending" rather than specific MRLs. |

## State Transition

```
Graded — Good Cut  ──► Accumulated ──► Todiya Packed (Bale) ──► Dispatched
Graded — Fent      ──► Accumulated ──► Todiya Packed (Bale) ──► Dispatched
Graded — Rags      ──► Accumulated ──► Todiya Packed (Bale) ──► Dispatched
Graded — Chindi    ──► Accumulated ──► Todiya Packed (Bale) ──► Dispatched
```

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream (waste from cutting)** | [06 — Packing Program & Execution](06-packing-program-execution.md) | Cutting waste feeds into accumulation stock. |
| **Upstream (waste from grading)** | [05 — Quality Grading](05-quality-grading.md) | Non-Fresh grades routed to accumulation area. |
| **Downstream** | [07 — Dispatch](07-dispatch.md) | Todiya bales dispatched via normal dispatch process. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Todiya account register (current) | Track Todiya transactions per party. |
| Packing Program form (current) | Todiya programs use same form as regular programs. |
| Future system | Todiya packing program type, accumulated stock dashboard, Todiya dispatch records. |

## Known Issues

| Issue | Impact |
|---|---|
| Accumulated stock quantities are estimates | No precise tracking of how much leftover material exists. |
| No visibility into accumulation trends | Cannot proactively find buyers when stock reaches a threshold. |
| Multiple MRL sources make reconciliation difficult | Todiya bales hard to trace back to original lots. |
| Todiya account tracking is informal | No systematic view of Todiya sales history per party. |
