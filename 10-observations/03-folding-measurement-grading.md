---
title: "Folding, Measurement, and Tone/Finish Classification"
status: draft
created: 2026-02-07
updated: 2026-02-11
tags: [observation, folding, measurement, classification, tone, finish, chadat]
---

# Folding, Measurement, and Tone/Finish Classification

## Location / Station

- **Area:** Miroli facility — folding and inspection area
- **Station/Cell:** No fixed station. The folding area expands or contracts based on workload and season.
- **Address/Building:** Miroli facility, Ahmedabad

## Activity

The folding station is the **first real processing step** at Miroli. Two things happen here:

1. **Folding & Measurement** — Every roll of incoming fabric is physically handled, folded, and measured by RG Faith's own team. This is a simple step: fold the roll, record the metres per roll.
2. **Tone & Finish Classification** — After folding, samples are sent to head office. Based on the sample review, tone and finish attributes are assigned to each roll (or group of rolls).

> **Important terminology distinction:** "Classification" refers to the tone/finish assignment step documented here. "Gradation" or "grading" refers to quality sorting (Fresh, Good Cut, Fent, Rags, Chindi) which happens later as a byproduct of packing execution. These are separate processes with separate terminology.

## Part 1: Folding & Measurement

### The Folding Process — Step by Step

#### Step 1: Pick Up a Lot

The folding team selects a lot from the stored received material. They retrieve the corresponding Gate Pass that was filed at the inbound stage. The Gate Pass tells them:
- How many metres the vendor reports
- The lot number
- The quality code of the incoming fabric
- Roll-by-roll measurements from the vendor

#### Step 2: Fold and Measure

Every roll of fabric is physically handled and folded. This is a standard fold — there is no variation in fold type at this step (fold types like Book, Roof, etc. are specified later in the packing program). The fold length is standard (~95-100cm) and is not tracked.

As they fold, they:
- Measure and record the metres for each roll
- The metres recorded here are the **"folding metres"** — RG Faith's own verified count

A roll may physically be a roll or a lump (badly folded piece). The system term is "roll" regardless of physical form.

**Note on folding vs cutting:** Folding at this stage is purely a measurement and handling step. Cutting of fabric happens during packing execution.

#### Step 3: Record Folding Metres

The measurements are recorded per roll. The metre reconciliation between Gate Pass metres and folding metres happens naturally — the system has both figures and any discrepancy is visible.

The folding metres figure is significant because it transitions the material from a vendor-reported quantity to a **facility-verified quantity**.

#### Step 4: Status → Awaiting Classification

Once a roll is folded and measured, its status becomes **"Awaiting Classification"** — samples need to be sent to head office for tone and finish determination.

### Chadat — Metres to Kilograms Conversion

The **Chadat** is a conversion factor between metres and kilograms, **specific to each lot**.

**Why it's needed:**
- Fresh and Good Cut are tracked in metres
- Fent, Rags, and Chindi are tracked in kilograms (because they're sold by weight)
- To calculate the percentage breakdown of a lot (how much was Fresh vs waste), you need a common unit
- The Chadat provides that conversion: X metres = Y kilograms for this specific lot

**How it's calculated:**
The team weighs a known length of fabric from the current lot. This gives them the metres-per-kg ratio (the Chadat). For example:
- Chadat = 4.86 means 4.86 metres per kilogram for this lot
- Chadat = 5.37 means 5.37 metres per kilogram for this lot

**Recording Chadat:**
Chadat is recorded as a **separate event**. It does not have to happen during folding specifically, but it **must be recorded before any gradation entry** (since grades like Fent, Rags, Chindi need it for kg conversion). The system should enforce this as a validation rule.

The Chadat varies by lot because different fabric qualities have different weights. A denser fabric (higher GSM) will have a lower Chadat (fewer metres per kg), and vice versa.

---

## Part 2: Tone & Finish Classification

### What Happens After Folding

After folding is complete, the team does a rough visual inspection and identifies the different tones and finishes they observe across the rolls. They then send physical samples to the head office.

### The Classification Process

#### Step 1: Rough Inspection & Sample Selection

Workers visually inspect the folded rolls and identify distinct tones and finishes. They may see, for example:
- 3 different tones across the rolls in a lot
- Or the entire lot may be a single tone

The number of samples depends on how many distinct tones and finishes are visually identified — they might send 1, 2, 3, or more samples.

#### Step 2: Samples Sent to Head Office

Physical samples are sent to head office along with data:
- "Tone 1 — X metres, Tone 2 — Y metres, Tone 3 — Z metres"

At this point, the material status becomes **"Awaiting Classification"** in the system.

#### Step 3: Head Office Confirms Classification

Head office reviews the samples and confirms (or corrects) the tone and finish classification.

#### Step 4: Factory Worker Records Classification

After HO confirmation, the factory worker enters the classification in the system. Two separate attributes are set per roll (or group of rolls):

| Attribute | Description | Examples |
|---|---|---|
| **Tone** | Colour/shade classification | O1W (Off-White), and other tone codes |
| **Finish** | Surface treatment/quality classification | 01, 02, 03 (numeric codes) |

The classification can be set at flexible granularity:
- **Per-roll** — each roll gets its own tone and finish
- **Per-lot** — all rolls in the lot share the same tone and finish
- **Partial lot** — some rolls share one classification, others share a different one

This flexibility is necessary because multiple rolls may have the same tone and finish, or individual rolls within a lot may differ.

#### Step 5: Status → Classified → Awaiting Program

Once classification is entered, the material status becomes **"Classified"** and then **"Awaiting Program"** — it is ready to be assigned to a packing program.

### Re-Classification

Tone and finish classification can be changed at later stages, but only with **role-based authorization**. Certain authorized roles (e.g., supervisor, manager) can edit the classification directly. No approval workflow is needed.

---

## The Gradation Report — The Core Metrics Document

The **Gradation Report** is the single most important document in the process. It captures the complete yield analysis for a lot — how much of the material ended up as Fresh versus losses.

> **Note:** Gradation data is now produced during packing execution (not as a standalone grading step). However, the Gradation Report remains a progressive, lot-level summary that aggregates data from packing.

### Gradation Report Structure (from scan page 16)

The report is a **computer-generated** document. It contains:

#### Header Section
| Field | Example | Purpose |
|---|---|---|
| Bill No | 1905 | Folding jobwork bill reference |
| Bill Date | 22/01/2026 | Date of the report |
| Rate | 0.60 | Folding jobwork rate (per meter) |
| Net Amount | 3,387.00 | Total folding cost |
| Batch No | ML 26-Ant26-7993 | Batch reference (legacy ERP field — not replicated in our system) |
| Grey Quality | KT-11000 Grey | Inbound quality code |
| Finish Quality | KT 11000 | Finished quality code |
| Program Ref | #MRL-60986-06/01/2026 | MRL number and date |

#### Metre Progression Section

This tracks how metres diminish through processing:

```
Greige Mtrs (vendor-reported):  6,006.80
    │
    │  Shrinkage from dyeing
    ▼
Gate Pass Mtrs:                 5,826.00  (what arrived per Gate Pass)
    │
    ▼
Folding Mtrs:                   5,644.33  (RG Faith's measured count)
    │
    ▼
Grade breakdown from packing execution
```

#### Gradation Breakdown Section

| Gradation | Kg/Pcs | Meters | % of Total | @Loss% | Loss% |
|---|---|---|---|---|---|
| Fresh | — | 5,470.02 | 96.91% | 0.00% | 0.00% |
| Good Cut | — | 52.00 | 0.92% | 0.00% | — |
| Fent | 11.46 kg | 64.44 m | 1.14% | 50.06% | 0.58% |
| Rags | — | 6.48 | 0.15% | 0.00% | — |
| Chindi | 2.00 kg | 16.82 m | 0.35% | 100.00% | 0.35% |
| **Total** | | **5,644.32** | **100.00%** | | |

Note how Fent and Chindi show values in **both kg and metres** — the metre figure is derived using the Chadat conversion.

### Progressive Nature of the Gradation Report

The Gradation Report is **not a one-time final document**. It is a **progressive/running report** that updates as packing progresses and gradation data is produced.

For example, if an MRL covers 6,000 metres but only 4,000 metres have been through packing so far:
- The Gradation Report shows data for only those 4,000 metres
- As more of the lot is packed, the report updates
- The report reflects the **current state of processing**, not the final state

### Two Key Loss Metrics

**1. Shrinkage Loss**
- Greige metres → Finished metres (Gate Pass)
- Physical shrinkage from the dyeing process (vendor-reported)
- Tracked for visibility, no commercial consequences with vendors

**2. Non-Fresh Loss (Yield Loss)**
- Total metres packed → Fresh metres
- The remainder became Good Cut, Fent, Rags, or Chindi
- Quality-based loss identified during packing execution

---

## Decision Pending Lots — A Special Case

Not all lots move smoothly through the process. Some lots enter a **"Decision Pending"** state where the quality is unclear and no one is sure how to proceed.

### What Decision Pending Looks Like (from scan page 3)

The "Decision Pending Lots In Miroli" register shows lots from multiple mills sitting in limbo:

| MRL No | Avak Date | Mill | Quality | MTR | How Long Pending |
|---|---|---|---|---|---|
| 576 | 18/6/24 | BKT | Supersonic | 972 | ~19 months |
| 127 | 19/4/25 | Shaim | Supersonic | 233 | ~9 months |
| 1092 | 23/9/25 | PSJC | Trend/Twill | 246 | ~4 months |
| 1285 | 14/10/25 | Kalapurna | K790xx | 884 | ~3 months |
| 1392 | 3/13/25 | ATP | BHTS | 398 | ~10 months |

Some of these lots have been sitting for **over a year** with no decision.

### System Implications

Each decision-pending lot needs:
- A **remark field** — free text describing the issue
- A **resolution pipeline** — workflow to move from pending → decided
- **Aging alerts** — flag lots that have been pending beyond 14 days with no activity
- **Escalation** — notify supervisors or managers when lots are aging

---

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Received material (finished from vendor) | Miroli storage area | Physical rolls/bundles | Selected by the folding team from stored inventory |
| Gate Pass | Paper file | Physical document | Retrieved from where it was filed at inbound |
| MRL reference | System | Reference number | Links to the inbound receipt record |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Folding metre records | System | Per-roll measurements | Facility-verified metres |
| Chadat record | System | Lot-specific conversion factor | Recorded separately, must exist before gradation |
| Classified material (with tone + finish) | Awaiting packing program | Physical fabric | Ready for program allocation |
| Decision Pending material | Hold area | Physical fabric | Awaiting decision |

## People

| Role | Count | Shift/Schedule | Notes |
|---|---|---|---|
| Folding workers | 3-7 | During working hours | Scale varies with workload. Handle physical folding and measurement. |
| Supervisor | 1 | Oversight | Handles sample selection, classification entry after HO confirmation. |

## Timing

- **Frequency:** Continuous during working hours. Lots are processed one at a time or in parallel depending on staffing.
- **Duration:** Depends on lot size. A 6,000 metre lot likely takes a full day or more to fold completely.
- **Schedule:** Regular working hours. The folding area is one of the busiest in the facility.
- **Peak/Off-peak:** Follows inbound volume.

## Equipment and Tools

| Equipment | Purpose | Notes |
|---|---|---|
| Folding tables / work surface | Lay out and fold fabric | Part of the open floor area |
| Measuring tape / metre stick | Measure fabric lengths | Manual measurement tools |
| Weighing scale | Weigh known length for Chadat calculation | Used to determine metres-per-kg ratio |

## Handoffs

- **Comes from:** Inbound/storage area. Received material that has been stored.
- **Goes to (Classified):** Packing program allocation → packing execution.
- **Goes to (Decision Pending):** Hold area. Material stays here until someone decides what to do with it.

## Problems and Workarounds

| Problem | Frequency | Current Workaround | Impact |
|---|---|---|---|
| Folding metres recorded only on paper | Always | Handwritten registers | Data not queryable, not backed up |
| Decision-pending lots forgotten | Frequent | Periodic manual review of the register | Lots sit for months/years |
| No real-time visibility into folding progress | Always | Ask the folding team directly | Cannot plan packing programs based on what's ready |
| Chadat not systematically recorded | Sometimes | Calculated ad-hoc when needed | Inconsistent conversion between metres and kg |
| Classification wait time variable | Sometimes | Phone calls to head office | Unclear when HO will confirm tone/finish |

## Design Implications for the System

### Must Have
1. **Folding entry screen** — Workers record per-roll measurements as they fold. Links to the MRL/lot.
2. **Classification entry** — Record tone (master data) and finish (master data) per roll, per lot, or per partial lot. Flexible granularity.
3. **Classification states** — Track: Awaiting Classification → Classified → Awaiting Program.
4. **Chadat recording** — Capture the metres-to-kg conversion factor per lot as a separate event.
5. **Progressive Gradation Report** — Auto-generated, updates as packing produces gradation data. Shows: metre progression, grade breakdown (% Fresh, etc.), shrinkage, non-fresh loss.
6. **Decision-pending workflow** — Remark field, resolution pipeline, aging alerts (14 days).
7. **Re-classification** — Authorized roles can change tone/finish at later stages (RBAC).

### Nice to Have
8. **Auto-reconciliation** — Compare Gate Pass metres against folding metres. Highlight discrepancies.
9. **Classification dashboard** — Show lots awaiting classification, classified and awaiting programs.
10. **Historical Chadat tracking** — Track Chadat trends by quality code or vendor.

### Not Needed
- Automated quality testing integration (no instruments in use)
- Worker productivity tracking (not requested)
- Fold type tracking at folding step (fold types belong to packing programs)

## Photos / Diagrams

Relevant scan pages from `00-inbox/rg faith scans.pdf`:
- **Page 5:** Ready Goods Report (handwritten) — the detailed measurement form used after folding
- **Page 6:** Fresh Pending Lots In Miroli 36" (page 1) — register of classified Fresh lots
- **Page 7:** Fresh Pending Lots In Miroli 36" (page 2) — continuation
- **Page 8:** Folding metres matched against factory metres — reconciliation notebook
- **Page 16:** Gradation Report (computer-generated) — the yield analysis report

## Raw Notes

From `00-inbox/notes.md`:
> "The first process is folding. No matter what comes in, the team at the first station folds it. Every meter gets a fold. That's when they first check the measurement and record how many meters it is."

From `00-inbox/second_meeting.md`:
> "The first thing that happens with the inward is fold... usually by 95 centimeters. Then they do a simple meter check."
>
> "While doing this, they also send a sample to the head office. That sample comes back, and then they have tone and grade set for that particular roll or lot."

## Open Questions

1. ~~How exactly is the Chadat measured?~~ **RESOLVED:** By weighing a known length of fabric. System just captures the Chadat value.
2. ~~Is grading done by the same workers who fold?~~ **RESOLVED:** Grading (gradation) is no longer a standalone step — it happens during packing execution. Folding workers handle folding and measurement only.
3. ~~How does Gradation Report data get to head office?~~ **RESOLVED:** Our system generates the report directly, eliminating the paper round-trip.
4. ~~Do any lots skip folding?~~ **RESOLVED:** No. Every lot must be folded and classified before packing.
