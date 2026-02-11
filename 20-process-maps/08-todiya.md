---
title: "Process 08 — Todiya (Leftover Repacking)"
status: draft
created: 2026-02-07
updated: 2026-02-11
tags: [process, todiya, toria, leftover, accumulation, unpack, repack]
---

# Process 08 — Todiya (Leftover Repacking)

## Overview

| Field | Value |
|---|---|
| **Purpose** | Unpack existing bales and repack unchanged thaans into new bales when a buyer is found for accumulated leftover material. Todiya is strictly unpack + repack — no re-cutting or re-folding. |
| **Trigger** | Sales team finds a buyer for accumulated leftover stock. |
| **End condition** | Todiya bales packed. Original bales marked as unpacked. Thaans reassigned to new bales. |
| **Frequency** | Periodic — when enough leftovers accumulate and a buyer is available. |
| **Typical duration** | Shorter than regular packing — no cutting or folding involved. |

## Context

"Todiya" (or "Toria") comes from the Hindi/Gujarati word for "breaking." The process involves physically unpacking existing bales and repacking the unchanged thaans into new bales for a different buyer. **Todiya does NOT involve cutting or folding** — thaans retain their original identity (same metres, same source roll).

## Roles

| Role | Responsibility |
|---|---|
| Sales team | Finds a buyer for leftover stock. (Out of scope for the system.) |
| Facility manager | Creates the Todiya instruction. |
| Packing workers | Execute the unpack and repack. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Existing bales to unpack | Storage / accumulation area | Physical bales | Bales containing non-Fresh thaans (Good Cut, Fent, Rags, etc.) from previous packing programs. |
| Buyer requirements | Sales team | Verbal | What the Todiya buyer wants. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Todiya bales | Dispatch area → Customer | Physical boxes | Repacked thaans for the buyer. New bale numbers assigned. |
| Unpacked bale records | System records | Status update | Original bales marked as "unpacked." |
| Updated thaan-to-bale mapping | System records | Updated references | Thaans reassigned from old bale(s) to new Todiya bale(s). |

## Process Steps

### The Accumulation Cycle

```
Normal packing programs produce cutting waste
  │
  ▼
┌─────────────────────────────────────┐
│ ACCUMULATION AREA                   │
│                                     │
│ Good Cut:  +2.3 m (from Program A)  │
│            +1.8 m (from Program B)  │
│            +3.1 m (from Program C)  │
│            ────────                 │
│            = 7.2 m accumulated      │
│                                     │
│ Fent:      +4.5 kg (from Program A) │
│            +2.1 kg (from Program B) │
│            ────────                 │
│            = 6.6 kg accumulated     │
│                                     │
│ (Continues growing over weeks/months│
│  until enough volume for a sale)    │
└─────────────────────────────────────┘
```

### The Todiya Unpack & Repack Flow

```
START — Buyer found for accumulated leftovers
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Assess available stock           │
│    • Check accumulated bales / thaans│
│      by grade (G/C, Fent, Rags,     │
│      Chindi)                        │
│    • May span material from         │
│      multiple original MRLs         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Create Todiya instruction        │
│    • Marked as Todiya type          │
│    • Specify which bales to unpack  │
│    • May mix grades in one bale     │
│      (e.g., "G/C + Fent")          │
│    • May combine material from      │
│      multiple MRLs / bales          │
│    • Specific instructions per      │
│      buyer's requirements           │
│    • Example note: "Good cut only!" │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Unpack existing bale(s)          │
│    • Physically open selected bales │
│    • Mark original bale(s) as       │
│      "unpacked" in the system       │
│    • Remove thaans — thaans retain  │
│      their original identity        │
│    • NO re-cutting or re-folding    │
│    • Thaans are unchanged: same     │
│      metres, same source roll       │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Repack thaans into new bale(s)   │
│    • Assemble selected thaans into  │
│      new Todiya bale(s)             │
│    • Thaans from multiple unpacked  │
│      bales can go into one new bale │
│    • Assign new bale number         │
│    • Apply brand and packaging      │
│    • Generate packing slip          │
│    • Update thaan-to-bale mapping   │
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
      Original bales marked unpacked.
      Thaan-to-bale mapping updated.
```

### Todiya vs Regular Packing Program

| Aspect | Regular (Process 06) | Todiya (Process 08) |
|---|---|---|
| Material source | Classified rolls (Awaiting Program) | Existing bales (accumulated non-Fresh) |
| Trigger | Sales order (~95%) or proactive (~5%) | Buyer found for leftovers |
| Involves cutting | Yes — rolls cut to specified lengths | No — thaans are unchanged |
| Involves folding | Yes — fold type specified by program | No — thaans retain original fold |
| Grades used | Fresh (non-Fresh goes to accumulation) | Good Cut, Fent, Rags (may be mixed) |
| MRL reference | Single or multiple MRLs (cross-lot) | May combine multiple MRLs / bales |
| Grade mixing | Never | Often ("G/C + Fent" in one bale) |
| Thaan identity | Created during cutting | Unchanged — same metres, same source roll |

### Exceptions

| Exception | How Handled |
|---|---|
| Accumulated stock insufficient for buyer's order | Wait for more to accumulate, or negotiate smaller quantity. |
| Buyer wants only one grade (e.g., "Good cut only!") | Todiya instruction specifies grade filter. Only bales with matching thaans unpacked. |
| Material from too many MRLs — hard to reconcile | Thaan-to-bale mapping maintains traceability even across multiple MRL sources. |

## State Transition

```
Packed (Bale, non-Fresh) ──► Unpacked ──► Todiya Packed (new Bale) ──► Pickup Scheduled ──► Dispatched

Thaan lifecycle through Todiya:
  Thaan in Bale A ──► Bale A unpacked ──► Thaan repacked into Bale B (unchanged)
  (same metres, same source roll, same identity)
```

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream (non-Fresh from packing)** | [06 — Packing Program & Execution](06-packing-program-execution.md) | Non-Fresh material identified during gradation goes to accumulation, eventually packed into bales available for Todiya. |
| **Downstream** | [07 — Dispatch](07-dispatch.md) | Todiya bales dispatched via normal dispatch process. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Todiya account register (current) | Track Todiya transactions per party. |
| Future system | Todiya workflow (unpack/repack), thaan reassignment, accumulated stock dashboard, Todiya dispatch records. |

## Known Issues

| Issue | Impact |
|---|---|
| Accumulated stock quantities are estimates | No precise tracking of how much leftover material exists. |
| No visibility into accumulation trends | Cannot proactively find buyers when stock reaches a threshold. |
| Multiple MRL sources make reconciliation difficult | Todiya bales hard to trace back to original lots. |
| Todiya account tracking is informal | No systematic view of Todiya sales history per party. |
