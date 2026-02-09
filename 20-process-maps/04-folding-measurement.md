---
title: "Process 04 — Folding & Measurement"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, folding, measurement, chadat, reconciliation]
---

# Process 04 — Folding & Measurement

## Overview

| Field | Value |
|---|---|
| **Purpose** | Physically unfold, measure, and fold incoming fabric into standard 2-metre folds — converting vendor-reported grey metres into RG Faith-verified folding metres. Calculate the Chadat (metres-to-kg conversion factor for Fent, Rags, and Chindi) for the lot. |
| **Trigger** | Grey material selected for processing from storage. |
| **End condition** | All material in the lot is folded into 2m folds and measured. Folding metres recorded. Chadat calculated. |
| **Frequency** | Continuous during working hours. |
| **Typical duration** | A 6,000-metre lot likely takes a full day or more. |

## Roles

| Role | Responsibility |
|---|---|
| Folding workers (3–7) | Physically unfold, measure, and fold fabric into 2m folds. Scale varies with workload. |
| Supervisor | Oversees process, handles metre reconciliation, records Chadat. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Grey material (unprocessed) | Miroli storage area | Physical rolls/bundles | Selected from stored inventory. |
| Gate Pass | Paper file | Physical document | Retrieved from filing. Provides vendor metre counts for reconciliation. |
| MRL reference | Paper records | Reference number | Links to the outbound/inbound records. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| 2-metre folds | Grading area | Physical fabric folds | Standard unit of work for quality inspection. |
| Folding metre records | Paper register | Handwritten | Per-roll and per-lot measurements. |
| Metre reconciliation | Paper notebook | Handwritten | Folding metres vs factory (Gate Pass) metres comparison. |
| Chadat value | Records / Gradation Report | Number | Metres-per-kg conversion factor for this lot. Used for converting Fent, Rags, and Chindi between metres and kg. |

## Process Steps

### Main Flow

```
START — Lot selected from grey storage
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Retrieve lot and Gate Pass       │
│    • Select a lot from grey storage │
│    • Retrieve the filed Gate Pass   │
│    • Note: vendor metres, lot no,   │
│      quality code from Gate Pass    │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Unfold and fold into 2m folds    │
│    • Incoming rolls can be 1,000m+  │
│    • Fold each roll into standard   │
│      2-metre folds                  │
│    • Folding is a measurement and   │
│      handling step, not cutting     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Measure every section            │
│    • Physically handle and measure  │
│      each fold                      │
│    • Record metre count per section │
│    • These are "folding metres" —   │
│      RG Faith's own verified count  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Calculate Chadat                 │
│    • Weigh a known length of fabric │
│    • Chadat = metres ÷ kilograms    │
│    • Used for converting Fent, Rags,│
│      and Chindi between metres & kg │
│    • Lot-specific: varies by fabric │
│      density / GSM                  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 5. Reconcile metres                 │
│    • Compare folding metres against │
│      factory (Gate Pass) metres     │
│    • Track shrinkage:               │
│      Grey metres → Folding metres   │
│    • Purpose: progress tracking,    │
│      not trust verification         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 6. Record all data                  │
│    • Folding metres (per roll and   │
│      lot total)                     │
│    • Chadat value                   │
│    • Reconciliation (folding vs     │
│      factory metres)                │
│    • Material now ready for grading │
└──────────────┬──────────────────────┘
               │
               ▼
END — Material folded and measured.
      Note: Folding and grading are independent
      activities — grading may happen before,
      after, or concurrently with folding.
```

### Note on Folding vs Cutting

Folding is a measurement and handling step — fabric is folded into standard 2-metre folds for easier handling and measurement. The fold could be of any total length (1,000m+ is common). **Folding is not cutting.** Cutting of fabric happens during grading (to separate defective sections) or during packing program execution (to cut to specified lengths).

### Exceptions

| Exception | How Handled |
|---|---|
| Gate Pass missing or misplaced | Search filing system. Contact vendor if needed. Do not process without reference data. |
| Severe quality issue visible during unfolding | Note the issue. May be flagged as Decision Pending at grading. Full roll may be rejected before grading. |
| Measurement discrepancy beyond expected shrinkage | Record as-is. Not commercially actionable (trusted vendor relationship). |

## State Transition

```
Grey ──► Folded (measured by RG Faith, Chadat calculated)
```

## Key Metrics

| Metric | Description | Source |
|---|---|---|
| Folding metres | RG Faith's own verified measurement | Measured during folding |
| Factory metres (Gate Pass) | Vendor's reported measurement | Gate Pass document |
| Shrinkage | Grey metres → Folding metres loss | Calculated (difference) |
| Chadat | Metres per kilogram for this lot (used for Fent, Rags, Chindi) | Calculated from weighing a known length of fabric |

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | [03 — Inbound Receipt](03-inbound-receipt.md) | Grey material comes from storage after inbound receipt. |
| **Independent** | [05 — Quality Grading](05-quality-grading.md) | Folding and grading are independent activities — neither requires the other as a prerequisite. They may happen in any order or concurrently. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Measuring tape / metre stick | Measure fabric lengths. |
| Weighing scale | Weigh a fold to calculate Chadat. |
| Paper registers | Record folding metres, reconciliation. |
| Future system | Digital entry of fold measurements, auto-reconciliation, Chadat capture. |

## Known Issues

| Issue | Impact |
|---|---|
| Folding metres recorded only on paper | Data not queryable, not backed up, hard to aggregate. |
| Metre reconciliation is manual | Tedious and error-prone for large lots. |
| No real-time visibility into folding progress | Cannot plan downstream work based on what's been folded. |
| Chadat not systematically recorded | Calculated ad-hoc; system should enforce capture for every lot. |
