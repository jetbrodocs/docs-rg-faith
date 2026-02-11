---
title: "Process 05 — Tone & Finish Classification"
status: draft
created: 2026-02-11
updated: 2026-02-11
tags: [process, classification, tone, finish, samples]
---

# Process 05 — Tone & Finish Classification

## Overview

| Field | Value |
|---|---|
| **Purpose** | Assign tone and finish attributes to folded rolls, enabling the material to be selected for packing programs. Classification is a two-attribute assignment (tone + finish), not a quality grading step. |
| **Trigger** | Rolls have been folded and measured (status = Awaiting Classification). |
| **End condition** | All rolls in the lot (or partial lot) have tone and finish attributes recorded. Status = Classified, then Awaiting Program once eligible for packing. |
| **Frequency** | Continuous — follows folding. |
| **Typical duration** | Variable. Factory-side inspection is quick, but the sample round-trip to HO can introduce delay. |

## Terminology Note

"Classification" refers specifically to the tone and finish assignment step. Do not confuse with "gradation" or "grading," which refers to quality sorting (Fresh, Good Cut, Fent, etc.) that happens during packing execution (Process 06).

## Roles

| Role | Responsibility |
|---|---|
| Factory worker | Performs rough visual inspection at the facility. Sends samples with metre data per tone to head office. Records final classification in the system after HO confirmation. |
| Head office (HO) | Receives samples, confirms tone and finish classification. |
| Supervisor | Oversees the process, handles re-classification requests. |

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Folded and measured rolls | Folding process (Process 04) | Physical rolls (Awaiting Classification) | Each roll has folding metres recorded. "Roll" is the system term — may physically be a roll or lump. |
| Folding metre data per roll | Folding records | Per-roll metre counts | Sent to HO with samples. |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Classified rolls | Storage → Packing (Process 06) | Physical rolls with tone + finish attributes | Ready for packing program assignment. |
| Classification records | System / paper register | Per-roll, per-lot, or partial-lot | Tone and finish attributes recorded. |

## Process Steps

### Main Flow

```
START — Rolls are folded and measured (Awaiting Classification)
  |
  v
+-----------------------------------------+
| 1. Rough visual inspection              |
|    - Factory worker inspects folded      |
|      rolls at the facility               |
|    - Initial assessment of tone and      |
|      finish characteristics              |
|    - Group rolls by apparent tone        |
+-------------------+---------------------+
                    |
                    v
+-----------------------------------------+
| 2. Send samples to Head Office          |
|    - Physical samples sent to HO        |
|    - Accompanied by metre data per      |
|      tone grouping                       |
|    - HO reviews samples against         |
|      their standards                     |
+-------------------+---------------------+
                    |
                    v
+-----------------------------------------+
| 3. HO confirms classification           |
|    - HO confirms or adjusts the tone    |
|      and finish assignment               |
|    - Communicates back to factory        |
+-------------------+---------------------+
                    |
                    v
+-----------------------------------------+
| 4. Record classification in system      |
|    - Factory worker records tone and     |
|      finish for each roll (or group)     |
|    - Two separate attributes:            |
|      * Tone (e.g., O1W, other codes)    |
|        — master data entity              |
|      * Finish (e.g., 01, 02, 03)        |
|        — master data entity              |
|    - Granularity is flexible:            |
|      * Per-roll                          |
|      * Per-lot (all rolls same)          |
|      * Partial lot (subset of rolls)     |
|    - Status: Classified                  |
+-------------------+---------------------+
                    |
                    v
END — Rolls classified with tone and finish.
      Status: Classified -> Awaiting Program.
      Ready for packing program assignment
      (Process 06).
```

### Two Classification Attributes

| Attribute | Description | Examples | Master Data |
|---|---|---|---|
| **Tone** | Colour/shade classification of the fabric | O1W (Off-White), and other tone codes | User-configurable tone code master list |
| **Finish** | Surface finish / hand-feel classification | 01, 02, 03 | User-configurable finish code master list |

Both tone and finish are independent master data entities. The combination of tone + finish determines how the material can be used in packing programs.

### Classification Granularity

Classification can be applied at different levels of granularity:

```
OPTION A: Per-roll classification
  Roll 1 → Tone: O1W, Finish: 01
  Roll 2 → Tone: O1W, Finish: 02
  Roll 3 → Tone: Cream, Finish: 01

OPTION B: Per-lot classification (all rolls same)
  Lot MRL 526 (all 12 rolls) → Tone: O1W, Finish: 01

OPTION C: Partial lot classification
  Rolls 1-8 → Tone: O1W, Finish: 01
  Rolls 9-12 → Tone: O1W, Finish: 02
```

The system should support all three granularities.

### Re-classification

Re-classification (changing tone or finish after initial classification) is allowed but requires role-based authorization. This handles cases where initial classification was incorrect or where HO revises their assessment.

### Exceptions

| Exception | How Handled |
|---|---|
| HO delays classification confirmation | Rolls remain in Awaiting Classification state. Variable wait time. |
| Disagreement between factory and HO assessment | HO decision takes precedence. Factory records what HO confirms. |
| Re-classification needed after initial recording | Allowed with role-based authorization. Previous classification logged. |
| Mixed tones within a single roll | Classify at the most specific level available. May require per-section notes. |

## State Transition

```
Awaiting Classification ──> Classified ──> Awaiting Program
```

Re-classification: `Classified ──> Classified` (with audit trail, requires authorization)

## Key Data Captured

| Field | Source | Description |
|---|---|---|
| Tone code | HO confirmation | Colour/shade classification (master data). |
| Finish code | HO confirmation | Surface finish classification (master data). |
| Classification date | Recorded at entry | When the classification was confirmed and recorded. |
| Classification granularity | Factory worker | Per-roll, per-lot, or partial lot. |
| Metres per tone grouping | Factory worker | Metre data sent with samples to HO. |

## Connected Processes

| Direction | Process | How Connected |
|---|---|---|
| **Upstream** | [04 — Folding & Measurement](04-folding-measurement.md) | Folded rolls with Awaiting Classification status enter this process. |
| **Downstream** | [06 — Packing Program & Execution](06-packing-program-execution.md) | Classified rolls (Awaiting Program) are available for packing program assignment. |

## Systems / Tools

| Tool | Purpose |
|---|---|
| Physical samples | Sent to HO for classification confirmation. |
| Paper registers (current) | Record tone and finish assignments. |
| Verbal / phone communication (current) | HO communicates classification decisions back to factory. |
| Future system | Digital classification entry, tone/finish master data management, re-classification workflow with authorization, audit trail. |

## Known Issues

| Issue | Impact |
|---|---|
| Variable classification wait time | Rolls can sit in Awaiting Classification for days depending on HO response time. |
| Sample round-trip delay | Physical samples must travel to HO and classification must be communicated back — no digital fast-track. |
| Classification not currently digitised | Cannot report on classification patterns, tone distribution, or finish distribution across lots. |
| No re-classification audit trail | Changes to classification not tracked in current paper-based system. |
