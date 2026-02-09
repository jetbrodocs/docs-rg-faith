---
title: "Process 09 — Not Acceptable Resolution"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [process, not-acceptable, reprocess, vendor, exception, resolution]
---

# Process 09 — Not Acceptable Resolution

## Overview

| Field | Value |
|---|---|
| **Purpose** | Track and resolve material graded as "Not Acceptable" — rejected fabric that needs to be returned to the vendor mill. Functions as an informal issue tracker. |
| **Trigger** | Material classified as Not Acceptable during quality grading (Process 05). |
| **End condition** | Vendor picks up the rejected material, OR material remains at Miroli indefinitely (unresolved). |
| **Frequency** | Occasional — varies by vendor quality. |
| **Typical duration** | Days to months. Some entries remain open for over a year. |

## Roles

| Role | Responsibility |
|---|---|
| Grading workers / supervisor | Classify material as Not Acceptable. Record on Reprocess List. |
| Manager | Contacts vendor, manages back-and-forth discussion. |
| Vendor mill | Expected to arrange pickup of rejected material. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Not Acceptable material | Quality grading (Process 05) | Physical fabric (metres) | Rejected during inspection. Either full roll or cut-out section. Always measured in metres. |
| Rejection reason / remark | Grading team | Free text (often Hindi) | Describes the quality issue. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Reprocess List entry | Paper register | Handwritten | Tracks pending returns. |
| Returned material (when resolved) | Vendor mill | Physical fabric | Vendor arranges pickup. |
| Updated status | Internal records | Status change | Open → Resolved or Unresolved. |

## Process Steps

### Main Flow

```
START — Material graded as Not Acceptable (Process 05)
  │
  ▼
┌─────────────────────────────────────┐
│ 1. Record on Reprocess List         │
│    • MRL Number                     │
│    • Avak Date (original arrival)   │
│    • Lot Number                     │
│    • Quality code                   │
│    • Tone                           │
│    • Metres / kg rejected           │
│    • Remark (reason for rejection)  │
│    • Mill name (vendor)             │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Store separately                 │
│    • Rejected material stored       │
│      separately from normal         │
│      inventory                      │
│    • Clearly identified as          │
│      Not Acceptable                 │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Contact vendor                   │
│    • Inform vendor of the rejection │
│    • Describe the quality issue     │
│    • Request pickup arrangement     │
│    ★ No formal dispute mechanism    │
│    ★ No credit notes or penalties   │
│    ★ Entirely trust-based           │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Back and forth                   │
│    • Vendor may request more info   │
│    • Discussion about the defect    │
│    • Vendor decides whether to      │
│      pick up                        │
│    • Timeline: days to months       │
└──────────────┬──────────────────────┘
               │
               ▼
        ┌──────┴──────┐
        │             │
        ▼             ▼
┌──────────────┐ ┌──────────────────┐
│ RESOLVED     │ │ UNRESOLVED       │
│              │ │                  │
│ Vendor       │ │ Vendor doesn't   │
│ arranges     │ │ pick up.         │
│ pickup.      │ │ Material stays   │
│ Material     │ │ at Miroli        │
│ returned.    │ │ indefinitely.    │
└──────────────┘ └──────────────────┘
```

### Reprocess List (from scan page 2)

The "Ready For Sending Reprocess List" tracks all pending Not Acceptable items, grouped by mill:

| MRL No | Avak Date | Lot No | Quality | Tone | MTR | Remark | Mill |
|---|---|---|---|---|---|---|---|
| 526 | 9/6/24 | — | RC-8001 | — | 1408 | (Hindi) | PSJC |
| 826 | 11/8/25 | — | Lancer W/R | — | — | (Hindi) | PSJC |
| 1403 | 11/11/25 | — | Liverpool | — | V9850 | (Hindi) | PSJC |
| 1097 | 11/9/24 | — | Unifoom | — | F13 | (Hindi) | (other) |
| 2392 | 6/13/25 | — | PCW/MQ | — | 930 | (Hindi) | (other) |

Some entries date back over a year — resolution can be very slow.

### Exceptions

| Exception | How Handled |
|---|---|
| Vendor disputes the rejection | Back-and-forth discussion. No formal arbitration. Trust-based resolution. |
| Vendor never picks up | Material remains at Miroli. Entry stays on Reprocess List. |
| Material deteriorates while waiting | Not formally tracked. Physical risk of extended storage. |
| Not Acceptable from a partial cut-out (small quantity) | Same process applies regardless of quantity. Even small cut-outs are tracked. |

## State Transition

```
Not Acceptable ──► Open (on Reprocess List)
               ──► In Discussion (vendor contacted)
               ──► Resolved — Picked Up (vendor took it back)
               ──► Unresolved — Remains at Facility
```

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | [05 — Quality Grading](05-quality-grading.md) | Material graded as Not Acceptable enters this process. |
| **Related** | [02 — Outbound to Vendor](02-outbound-to-vendor.md) | Vendor is the same mill that originally processed the fabric. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Reprocess List (paper register, current) | Track all pending Not Acceptable items. |
| Verbal communication (current) | Contact vendor for pickup. Record expected pickup date. |
| Future system | Digital Not Acceptable record with status tracking, aging alerts, vendor-wise view, commentary log. |

## Known Issues

| Issue | Impact |
|---|---|
| No formal resolution mechanism | Relies entirely on vendor goodwill. |
| Entries remain open for months/years | Rejected material occupies storage space indefinitely. |
| No aging visibility | Old entries get buried in the paper list. |
| Remarks in Hindi — not standardised | Difficult to analyse rejection patterns across vendors. |
| No vendor quality tracking | Cannot identify vendors with higher rejection rates. |
