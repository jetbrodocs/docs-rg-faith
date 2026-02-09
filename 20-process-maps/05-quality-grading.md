---
title: "Process 05 — Quality Grading"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, grading, quality, gradation, fresh, good-cut, fent, rags, chindi, not-acceptable, decision-pending]
---

# Process 05 — Quality Grading

## Overview

| Field | Value |
|---|---|
| **Purpose** | Inspect each folded section for quality, classify into grades (Fresh, Good Cut, Fent, Rags, Chindi, Not Acceptable), and produce the Gradation Report — the core yield analysis for the lot. |
| **Trigger** | Grey or folded material selected for quality inspection. Grading does not require folding to happen first — the two are independent activities. |
| **End condition** | All material in the lot is classified into grades. Gradation Report updated. Material routed to appropriate next step. |
| **Frequency** | Continuous during working hours. Happens simultaneously with folding in practice. |
| **Typical duration** | Same as folding — a full lot can take a day or more. |

## Roles

| Role | Responsibility |
|---|---|
| Folding/grading workers (3–7) | Inspect fabric, identify defects, assign grades. Same workers who fold — multi-skilled. |
| Supervisor | Validates grading decisions. Handles borderline / Decision Pending cases. Inputs to Gradation Report. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Grey or folded material | Storage or folding process | Physical fabric rolls or folds | Grading can operate on material before or after folding. |
| Chadat value (if available) | Folding process (Process 04) | Number | Needed for converting Fent, Rags, and Chindi from kg to metres. May be calculated during grading if folding hasn't happened yet. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Fresh material | Graded storage → Packing (Process 06) | Physical fabric (metres) | Best quality. ~96–97% of lot. Ready for packing program. |
| Good Cut | Accumulation area → Todiya (Process 08) | Physical fabric (metres) | Minor defects. Always goes to accumulation for Todiya — never packed with Fresh in regular programs. |
| Fent | Accumulation area → Todiya (Process 08) | Physical fabric (kilograms) | Noticeable defects. ~50% considered loss. |
| Rags | Accumulation area → Todiya (Process 08) | Physical fabric (kilograms) | Significant defects. |
| Chindi | Accumulation area → Todiya (Process 08) | Physical fabric (kilograms) | Waste. 100% loss. |
| Not Acceptable | Separate storage → Resolution (Process 09) | Physical fabric (metres) | Rejected. Pending return to vendor. |
| Gradation Report | Head office / system | Computer-generated report | Progressive yield analysis. Updated as grading progresses. |

## Process Steps

### Main Flow

```
START — Material selected for quality inspection
        (may be grey or folded — no enforced sequence)
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Visual & tactile inspection      │
│    • Workers inspect each fold      │
│    • Look for: stains, discolour,   │
│      tears, holes, weaving defects, │
│      dyeing irregularities, width   │
│      inconsistencies                │
│    • Judgment-based — no automated  │
│      instruments, no quantitative   │
│      thresholds                     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Classify into grade              │
│                                     │
│    ┌─────────┐  Best quality        │
│    │ FRESH   │  ~96–97% of lot      │
│    │ (metres)│  → Packing           │
│    └─────────┘                      │
│    ┌──────────┐  Minor defects      │
│    │ GOOD CUT │  ~0.5–1%            │
│    │ (metres) │  → Accumulate/Pack  │
│    └──────────┘                     │
│    ┌──────────┐  Noticeable defects │
│    │ FENT     │  ~1–1.5%            │
│    │ (kg)     │  → Todiya           │
│    └──────────┘                     │
│    ┌──────────┐  Significant defects│
│    │ RAGS     │  ~0.1–0.2%          │
│    │ (kg)     │  → Todiya           │
│    └──────────┘                     │
│    ┌──────────┐  Waste              │
│    │ CHINDI   │  ~0.3–0.5%          │
│    │ (kg)     │  → Todiya           │
│    └──────────┘                     │
│    ┌───────────────┐  Rejected      │
│    │ NOT ACCEPTABLE│  Varies         │
│    │ (metres)      │  → Return to   │
│    │               │    vendor       │
│    └───────────────┘                │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Weigh/measure non-Fresh grades   │
│    • Good Cut: measured in metres   │
│    • Fent, Rags, Chindi: weighed    │
│      in kilograms                   │
│    • Use Chadat to calculate        │
│      equivalent metres for          │
│      Fent/Rags/Chindi reporting     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Route material by grade          │
│    • Fresh → graded storage         │
│    • Good Cut → accumulation area   │
│    • Fent/Rags/Chindi → accum area  │
│    • Not Acceptable → separate      │
│      storage (Process 09)           │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 5. Update Gradation Report          │
│    • Progressive — updates as       │
│      grading continues              │
│    • Metre progression:             │
│      Grey → Gate Pass → Folded →    │
│      Packed                         │
│    • Grade breakdown: % Fresh,      │
│      % Good Cut, % Fent, etc.       │
│    • Shrinkage + non-Fresh loss     │
│    • Uses Chadat for kg → metre     │
│      conversion (Fent/Rags/Chindi)  │
└──────────────┬──────────────────────┘
               │
               ▼
END — All material graded and routed.
      Gradation Report updated.
```

### Two Not Acceptable Scenarios

```
Scenario 1: FULL ROLL REJECTION (before cutting)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Incoming roll inspected
      │
      ▼
  Severe defect across entire roll
  (e.g., major discolouration)
      │
      ▼
  Entire roll → NOT ACCEPTABLE
  (rejected as-is)
      │
      ▼
  → Process 09 (Not Acceptable Resolution)


Scenario 2: PARTIAL REJECTION (during grading)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  1,012m roll being graded
      │
      ├── Section 1 → FRESH ✓
      ├── Section 2 → FRESH ✓
      ├── Section 3: defect found at 65m mark
      │   ├── 65m → FRESH ✓
      │   ├── 5m → NOT ACCEPTABLE ✗ (cut out)
      │   └── 30m → continue as next section
      ├── ... more sections
      └── remaining material graded by quality
```

### Decision Pending — Special Case

```
Material arrives → Inspection → Quality unclear
                                      │
                                      ▼
                           ┌─────────────────────┐
                           │ DECISION PENDING     │
                           │                      │
                           │ • Remark recorded    │
                           │ • Awaits supervisor  │
                           │   decision           │
                           │ • Occupies inventory  │
                           │   space = cost        │
                           │ • Flag for revisit if │
                           │   no activity for 14  │
                           │   days                │
                           └──────────┬──────────┘
                                      │
                                      ▼
                           Eventually resolved to:
                           • Any grade (Fresh, G/C, etc.)
                           • Not Acceptable
```

### Exceptions

| Exception | How Handled |
|---|---|
| Borderline quality — hard to classify | Supervisor makes judgment call. If unresolved, enters Decision Pending state. |
| Full roll rejected before grading | Entire roll goes to Not Acceptable. |
| Defect found during grading | Defective section cut out (at metre boundaries) and classified separately. Cutting may happen during grading to separate defective sections. |
| Lot sits as Decision Pending beyond 14 days | Currently: periodic manual review. System: auto-flag lots with no comment/activity for 14 days. Escalate to manager. |

## State Transition

```
Grey or Folded ──► Graded — Fresh      (→ Process 06: Packing)
               ──► Graded — Good Cut   (→ Process 08: Todiya)
               ──► Graded — Fent       (→ Process 08: Todiya)
               ──► Graded — Rags       (→ Process 08: Todiya)
               ──► Graded — Chindi     (→ Process 08: Todiya)
               ──► Not Acceptable      (→ Process 09: Resolution)
               ──► Decision Pending    (→ Awaiting decision)

Note: Folding and grading are independent. Material can be
graded before, after, or concurrently with folding.
```

## The Gradation Report

The Gradation Report is the **single most important document** in the process. It is a progressive, running report that captures:

### Metre Progression
```
Grey U/S Mtrs:     6,006.80   (vendor's original measurement)
Gate Pass Mtrs:    5,826.00   (what arrived per Gate Pass)
F.H. Avak Mtrs:   5,825.00   (what reached folding area)
F.H. Fold Mtrs:   5,644.33   (after folding — RG Faith's count)
F.H. Plk Mtrs:    5,644.33   (after packing)
```

### Grade Breakdown (example)
| Grade | Kg | Metres | % of Total | Loss Factor | Loss % |
|---|---|---|---|---|---|
| Fresh | — | 5,470.02 | 96.91% | 0% | 0% |
| Good Cut | — | 52.00 | 0.92% | 0% | — |
| Fent | 11.46 | 64.44 | 1.14% | 50% | 0.58% |
| Rags | — | 6.48 | 0.15% | 0% | — |
| Chindi | 2.00 | 16.82 | 0.35% | 100% | 0.35% |
| **Total** | | **5,644.32** | **100%** | | |

### Progressive Nature
If only 4,000 of 6,000 metres have been graded, the report shows data for only those 4,000 metres. It updates as more material is processed.

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Independent** | [04 — Folding & Measurement](04-folding-measurement.md) | Folding and grading are independent — neither requires the other first. They may happen in any order or concurrently. |
| **Downstream (Fresh)** | [06 — Packing Program & Execution](06-packing-program-execution.md) | Fresh material enters packing pipeline. |
| **Downstream (G/C, Fent, Rags, Chindi)** | [08 — Todiya](08-todiya.md) | Non-Fresh grades accumulate for Todiya sale. |
| **Downstream (Not Acceptable)** | [09 — Not Acceptable Resolution](09-not-acceptable-resolution.md) | Rejected material enters return pipeline. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Weighing scale | Weigh Fent, Rags, and Chindi in kg. |
| Paper registers | Record grades per fold. |
| Head office ERP | Generates Gradation Report (computer-generated, data entered at head office). |
| Future system | Digital grading entry, auto-generated progressive Gradation Report, decision-pending workflow with aging alerts. |

## Known Issues

| Issue | Impact |
|---|---|
| Grading is judgment-based with no documented criteria | Inconsistency possible between workers, though experienced team mitigates this. |
| Gradation data entered at head office, not factory | Delay between grading and report availability. |
| Decision-pending lots forgotten | Material sits for months/years. No visibility or alerts. |
| No real-time visibility into grading progress | Cannot plan packing programs based on what's graded and available. |
