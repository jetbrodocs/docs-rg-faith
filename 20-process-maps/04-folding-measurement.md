---
title: "Process 04 — Folding & Measurement"
status: draft
created: 2026-02-07
updated: 2026-02-11
tags: [process, folding, measurement, reconciliation]
---

# Process 04 — Folding & Measurement

## Overview

| Field | Value |
|---|---|
| **Purpose** | Physically unfold, measure, and fold incoming fabric into standard folds — converting vendor-reported metres into RG Faith-verified folding metres per roll. |
| **Trigger** | Received material selected for processing from storage. |
| **End condition** | All rolls in the lot are folded and measured. Folding metres recorded per roll. Status = Awaiting Classification. |
| **Frequency** | Continuous during working hours. |
| **Typical duration** | A 6,000-metre lot likely takes a full day or more. |

## Roles

| Role | Responsibility |
|---|---|
| Folding workers (3–7) | Physically unfold, measure, and fold fabric into standard folds. Scale varies with workload. |
| Supervisor | Oversees process, handles metre reconciliation. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Received material (unprocessed) | Miroli storage area | Physical rolls/bundles | Selected from stored inventory. "Roll" is the system term — may physically be a roll or lump. |
| Gate Pass | Paper file | Physical document | Retrieved from filing. Provides vendor metre counts for reconciliation. |
| MRL reference | Paper records | Reference number | Links to the inbound receipt records. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Standard folds | Storage / classification area | Physical fabric folds | Folded and measured, awaiting tone and finish classification. |
| Folding metre records | Paper register | Handwritten | Per-roll and per-lot measurements. |
| Metre reconciliation | Paper notebook | Handwritten | Folding metres vs factory (Gate Pass) metres comparison. |

## Process Steps

### Main Flow

```
START — Lot selected from received storage
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Retrieve lot and Gate Pass       │
│    • Select a lot from storage      │
│    • Retrieve the filed Gate Pass   │
│    • Note: vendor metres, lot no,   │
│      quality code from Gate Pass    │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Fold and measure per roll        │
│    • Incoming rolls can be 1,000m+  │
│    • Fold each roll into standard   │
│      folds (~95–100cm fold length,  │
│      not tracked in system)         │
│    • Folding is a measurement and   │
│      handling step, not cutting     │
│    • Measure each roll and record   │
│      folding metres per roll        │
│    • These are "folding metres" —   │
│      RG Faith's own verified count  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Reconcile metres                 │
│    • Compare folding metres against │
│      factory (Gate Pass) metres     │
│    • Track shrinkage:               │
│      Received metres → Folding mtrs │
│    • Purpose: progress tracking,    │
│      not trust verification         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Record all data                  │
│    • Folding metres (per roll and   │
│      lot total)                     │
│    • Reconciliation (folding vs     │
│      factory metres)                │
│    • Material status → Awaiting     │
│      Classification                 │
└──────────────┬──────────────────────┘
               │
               ▼
END — Material folded and measured.
      Status: Awaiting Classification.
      Next step: Tone & Finish Classification
      (Process 05).
```

### Note on Folding vs Cutting

Folding is a measurement and handling step — fabric is folded into standard folds (~95-100cm fold length) for easier handling and measurement. The fold type (Book, Roof, etc.) is NOT determined at this step — fold type is specified later by the Packing Program. **Folding is not cutting.** Cutting happens during packing program execution (to cut to specified lengths).

### Note on Chadat

Chadat (the metres-to-kg conversion factor) is recorded as a separate event, not necessarily tied to folding. However, Chadat must be recorded before any gradation entry (which happens during packing execution). Chadat may be calculated at any point before packing but is lot-specific and varies by fabric density / GSM.

### Note on Rolls

"Roll" is the system term for an inbound fabric unit. Physically, it may be a roll or a lump. The system uses "roll" consistently regardless of physical form.

### Exceptions

| Exception | How Handled |
|---|---|
| Gate Pass missing or misplaced | Search filing system. Contact vendor if needed. Do not process without reference data. |
| Severe quality issue visible during unfolding | Note the issue. May be flagged for attention at classification or packing. |
| Measurement discrepancy beyond expected shrinkage | Record as-is. Not commercially actionable (trusted vendor relationship). |

## State Transition

```
Received ──► Folded ──► Awaiting Classification
```

## Key Metrics

| Metric | Description | Source |
|---|---|---|
| Folding metres | RG Faith's own verified measurement per roll | Measured during folding |
| Factory metres (Gate Pass) | Vendor's reported measurement | Gate Pass document |
| Shrinkage | Received metres → Folding metres loss | Calculated (difference) |

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | [03 — Inbound Receipt](03-inbound-receipt.md) | Received material comes from storage after inbound receipt. |
| **Downstream** | [05 — Tone & Finish Classification](05-tone-finish-classification.md) | Folded material proceeds to classification for tone and finish attributes. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Measuring tape / metre stick | Measure fabric lengths. |
| Paper registers | Record folding metres, reconciliation. |
| Future system | Digital entry of fold measurements, auto-reconciliation, Chadat capture. |

## Known Issues

| Issue | Impact |
|---|---|
| Folding metres recorded only on paper | Data not queryable, not backed up, hard to aggregate. |
| Metre reconciliation is manual | Tedious and error-prone for large lots. |
| No real-time visibility into folding progress | Cannot plan downstream work based on what's been folded. |
| No fold-type tracking at this step | Fold type is determined later during packing; this step uses a standard fold only. |
