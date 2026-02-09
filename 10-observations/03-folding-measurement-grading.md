---
title: "Folding, Measurement, and Quality Grading"
status: draft
created: 2026-02-07
updated: 2026-02-07
tags: [observation, folding, grading, measurement, gradation, chadat, quality]
---

# Folding, Measurement, and Quality Grading

## Location / Station

- **Area:** Miroli facility — folding and inspection area
- **Station/Cell:** No fixed station. The folding area expands or contracts based on workload and season.
- **Address/Building:** Miroli facility, Ahmedabad

## Activity

The folding station is the **first real processing step** at Miroli and arguably the most important one. It's where three critical things happen simultaneously:

1. **Measurement** — Every meter of incoming fabric is physically handled and measured for the first time by RG Faith's own team.
2. **Quality inspection** — The fabric is visually inspected for defects, discoloration, and other quality issues.
3. **Grading** — Based on the inspection, the fabric is classified into quality grades (Fresh, Good Cut, Fent, Rags, Chindi, or Not Acceptable).

This is the stage where grey meters (unclassified, vendor-reported) become classified inventory with known quality and RG Faith-verified measurements.

## The Folding Process — Step by Step

### Step 1: Pick Up a Lot

The folding team selects a lot from the stored grey material. They retrieve the corresponding Gate Pass that was filed at the inbound stage. The Gate Pass tells them:
- How many meters the vendor claims to have sent
- The lot number
- The quality code of the incoming fabric
- Roll-by-roll measurements from the vendor

### Step 2: Unfold and Measure

Every meter of fabric is unfolded, laid out, and physically measured. This is manual work — workers handle the fabric piece by piece. Incoming rolls from vendors can be very long — **1,000 meters or more per roll**. The folding team cuts these long rolls into **standard 100-meter folds**. This 100m fold is the fundamental unit of work.

As they unfold and cut into 100m sections, they simultaneously:
- Count the meters (using their own measurement)
- Record the measurement for each roll/piece
- Note any defects, stains, tears, or other quality issues they observe

**Handling non-round numbers:** If a roll is 1,012 meters, it produces 10 full 100m folds plus a 12m remainder. The 12m tail piece is not long enough for a standard fold, so it gets classified as Good Cut, Fent, or Chindi depending on its quality — not because it's defective, but because it's too short for a standard unit.

### Step 3: Record Folding Meters

The measurements are recorded in a handwritten register. This is the **"folding meters"** figure — RG Faith's own count, as opposed to the vendor's "factory meters" from the Gate Pass.

#### Meter Reconciliation (Scan Page 8)

A dedicated reconciliation step matches folding meters against factory meters. This was observed in scan page 8, titled "Folding meters being matched against factory meters."

The reconciliation page shows paired numbers — the vendor's meter count alongside RG Faith's folding meter count for each piece:

```
Vendor (Factory)  |  RG Faith (Folding)
      188         |       138
      142         |       1425
      145         |       1460
      140         |       1415
      136         |       1360
      ...         |       ...
```

Despite the high-trust relationship with vendors (grey meters are accepted at face value on arrival), this reconciliation serves an important purpose: it tracks **how much of the lot has been processed**. It's a progress indicator, not a trust verification.

The totals from this reconciliation feed into the Gradation Report (see below).

### Step 4: Quality Inspection

During the folding process, workers inspect the fabric and identify quality issues. Common defects include:
- Stains or discoloration
- Tears or holes
- Weaving defects carried through from earlier stages
- Dyeing irregularities (uneven color, wrong tone)
- Dimensional issues (width inconsistency)

The inspection is visual and tactile — workers rely on experience and judgment. There are no automated quality testing instruments observed at this stage. Grading decisions are **judgment-based** with no specific quantitative thresholds.

**Two scenarios for Not Acceptable material:**

**Scenario 1 — Full roll rejection (before cutting):**
During initial inspection of the incoming roll, the team may decide the entire roll is Not Acceptable — e.g., severe discoloration across the whole fabric. The entire roll is rejected before any cutting into 100m folds happens.

**Scenario 2 — Partial rejection (during cutting):**
While cutting a long roll into 100m folds, the team encounters a defect (e.g., a mark or stain). They cut out the defective section, which gets classified as Not Acceptable. The remaining sections continue as Fresh. Since everything must be measured in whole meters, the cut-out is always at meter boundaries.

### Step 5: Grading

Based on the inspection, each 100m fold (and any remainder pieces) is classified into a quality grade. The grading system has six categories:

| Grade | Quality Level | Measured In | Disposition | Typical % of Lot |
|---|---|---|---|---|
| **Fresh** | Best — no defects | Meters | Ready for packing program | ~96-97% |
| **Good Cut** | Minor defects, still usable | Kilograms | Accumulate for Todiya | ~0.5-1% |
| **Fent** | Noticeable defects | Kilograms | Accumulate for Todiya sale | ~1-1.5% |
| **Rags** | Significant defects | Kilograms | Accumulate for Todiya sale | ~0.1-0.2% |
| **Chindi** | Waste-level quality | Kilograms | Accumulate for Todiya sale (100% loss) | ~0.3-0.5% |
| **Not Acceptable** | Completely rejected | Meters | Send back to vendor mill | Varies |

**Key insight:** Fresh is measured in **meters** because it's the sellable product. All lower grades are measured in **kilograms** because they're sold by weight (as scrap, rags, etc.). The bridge between these two units is the **Chadat**.

### The Chadat — Meters to Kilograms Conversion

The **Chadat** (also sometimes spelled "Chaddat") is a critical concept. It is a conversion factor between meters and kilograms that is **specific to each lot**.

**Why it's needed:**
- Fresh material is tracked in meters (because customers buy by the meter)
- Non-Fresh material (Good Cut, Fent, Rags, Chindi) is tracked in kilograms (because it's sold by weight)
- To calculate the percentage breakdown of a lot (how much was Fresh vs waste), you need a common unit
- The Chadat provides that conversion: X meters = Y kilograms for this specific lot

**How it's calculated:**
During the folding and cutting process, the team weighs a known length of fabric from the current lot — likely a standard 100-meter fold, since that's the easiest unit to weigh. This gives them the meters-per-kg ratio (the Chadat). For example:
- Chadat = 4.86 means 4.86 meters per kilogram for this lot
- Chadat = 5.37 means 5.37 meters per kilogram for this lot

**Where it appears:**
- On the Packing Program header (scan pages 13-15, originally misread as "Chalet")
- In the Gradation Report calculations
- Used whenever converting between meters and kg for the lot

The Chadat varies by lot because different fabric qualities have different weights. A denser fabric (higher GSM) will have a lower Chadat (fewer meters per kg), and vice versa.

## The Gradation Report — The Core Metrics Document

The **Gradation Report** is the single most important document in the process. It captures the complete yield analysis for a lot — how much of the grey material ended up as Fresh versus losses.

### Gradation Report Structure (from scan page 16)

The report is a **computer-generated** document from RG Faith's head office system (the only computer-generated report at the factory level for this process). It contains:

#### Header Section
| Field | Example | Purpose |
|---|---|---|
| Bill No | 1905 | Folding jobwork bill reference |
| Bill Date | 22/01/2026 | Date of the report |
| Rate | 0.60 | Folding jobwork rate (per meter) |
| Net Amount | 3,387.00 | Total folding cost |
| Batch No | ML 26-Ant26-7993 | Batch reference |
| Grey Quality | KT-11000 Grey | Inbound quality code |
| Finish Quality | KT 11000 | Finished quality code |
| Program Ref | #MRL-60986-06/01/2026 | MRL number and date |

#### Meter Progression Section

This is the heart of the report — it tracks how meters diminish through each stage:

```
Grey U/S Mtrs:     6,006.80  (existing report field — see note below)
    │
    │  Transit/handling loss: ~180m (~3%)
    ▼
Gate Pass Mtrs:    5,826.00  (what arrived per Gate Pass)
    │
    │  Minimal loss: ~1m
    ▼
F.H. Avak Mtrs:   5,825.00  (Folding House Arrival — what reached the folding area)
    │
    │  Folding/measurement loss: ~181m (~3%)
    ▼
F.H. Fold Mtrs:   5,644.33  (After folding — RG Faith's measured count)
    │
    │  No further loss at packing
    ▼
F.H. Plk Mtrs:    5,644.33  (After packing — final count)
```

**Note on Grey U/S Mtrs:** During the site visit, the team said Grey U/S Mtrs and Gate Pass Mtrs "should have been the same" but couldn't explain why they differ. For our system, the simplified metre progression model is:
1. **Metres sent** (from MRL outbound record)
2. **Metres received** (from Gate Pass)
3. **Shrinkage** = sent minus received
4. **Grade breakdown** of received metres (Fresh, Good Cut, Fent, etc.)

This progression shows where meters are "lost" — through shrinkage, handling, measurement differences, and quality rejection.

#### Gradation Breakdown Section

| Gradation | Kg/Pcs | Meters | % of Total | @Loss% | Loss% |
|---|---|---|---|---|---|
| Fresh | — | 5,470.02 | 96.91% | 0.00% | 0.00% |
| Good Cut | — | 52.00 | 0.92% | 0.00% | — |
| Fent | 11.46 kg | 64.44 m | 1.14% | 50.06% | 0.58% |
| Rags | — | 6.48 | 0.15% | 0.00% | — |
| Chindi | 2.00 kg | 16.82 m | 0.35% | 100.00% | 0.35% |
| **Total** | | **5,644.32** | **100.00%** | | |

**Reading this table:**
- Fresh at 96.91% is a good yield
- Fent has a 50% loss factor (half of Fent material is considered a loss)
- Chindi has a 100% loss factor (all Chindi is considered waste)
- The "Loss%" column shows the contribution to overall loss
- Non-Fresh percentage: 3.08% (everything that isn't Fresh)

Note how Fent and Chindi show values in **both kg and meters** — the meter figure is derived using the Chadat conversion.

### Progressive Nature of the Gradation Report

The Gradation Report is **not a one-time final document**. It is a **progressive/running report** that updates as a lot is processed.

For example, if an MRL covers 6,000 metres but only 4,000 metres have been through folding and grading so far:
- The Gradation Report shows data for only those 4,000 meters
- As more of the lot is processed, the report updates
- The report reflects the **current state of processing**, not the final state

This is critical for system design — the Gradation Report needs to:
- Track progress against the total lot (how much has been graded out of total grey meters)
- Update incrementally as more material is processed
- Show both the current snapshot and the percentage completion

### Two Key Loss Metrics

The Gradation Report captures two fundamentally different types of loss:

**1. Shrinkage Loss**
- Grey meters (6,006.80) → Finished meters (5,644.33)
- This is physical shrinkage from the dyeing and processing
- Tracked for visibility, no commercial consequences with vendors
- Varies by fabric type — observed range: 1% to 12%

**2. Non-Fresh Loss (Yield Loss)**
- Total graded meters (5,644.33) → Fresh meters (5,470.02)
- The remaining 174.31 meters (3.08%) became Good Cut, Fent, Rags, or Chindi
- This is quality-based loss — fabric that didn't meet the Fresh standard
- Also tracked for visibility, strategic decisions made infrequently

## Inputs

| Input | Source | Format | Notes |
|---|---|---|---|
| Grey material (unprocessed) | Miroli storage area | Physical rolls/bundles | Selected by the folding team from stored inventory |
| Gate Pass | Paper file | Physical document | Retrieved from where it was filed at inbound |
| MRL reference | Paper records | Reference number | Links to the outbound record |

## Outputs

| Output | Destination | Format | Notes |
|---|---|---|---|
| Folding meter records | Paper register | Handwritten | Per-roll and per-lot measurements |
| Meter reconciliation | Paper notebook | Handwritten | Folding meters vs factory meters comparison |
| Graded material — Fresh | Packing area / storage | Physical fabric | Ready for packing program allocation |
| Graded material — Good Cut | Accumulation area | Physical fabric (weighed in kg) | Held until enough volume for sale or Todiya |
| Graded material — Fent | Accumulation area | Physical fabric (weighed in kg) | Held for Todiya |
| Graded material — Rags | Accumulation area | Physical fabric (weighed in kg) | Held for Todiya |
| Graded material — Chindi | Accumulation area | Physical fabric (weighed in kg) | Waste. Held for Todiya. 100% loss. |
| Not Acceptable material | Separate storage | Physical fabric | Awaiting return to vendor mill |
| Gradation Report | Head office system → factory | Computer-generated printout | Progressive yield analysis |

## People

| Role | Count | Shift/Schedule | Notes |
|---|---|---|---|
| Folding workers | 3-7 | During working hours | Scale varies with workload. Handle the physical unfolding, measurement, and inspection. |
| Quality inspector | 1+ | During folding | May be the same workers or a dedicated person. Makes grading decisions. |
| Supervisor | 1 | Oversight | May create or authorize the Gradation Report inputs. Handles the meter reconciliation. |

## Timing

- **Frequency:** Continuous during working hours. Lots are processed one at a time or in parallel depending on staffing.
- **Duration:** Depends on lot size. A 6,000 meter lot likely takes a full day or more to fold, measure, and grade completely.
- **Schedule:** Regular working hours. The folding area is one of the busiest in the facility.
- **Peak/Off-peak:** Follows inbound volume. When many shipments arrive from vendors, the folding area scales up.

## Equipment and Tools

| Equipment | Purpose | Notes |
|---|---|---|
| Folding tables / work surface | Lay out and fold fabric | Part of the open floor area |
| Measuring tape / meter stick | Measure fabric lengths | Manual measurement tools |
| Weighing scale | Weigh non-Fresh grades in kg | Used for Good Cut, Fent, Rags, Chindi |
| Paper registers / notebooks | Record measurements and grades | Currently the only "system" |

## Systems

| System | Used For | Notes |
|---|---|---|
| Paper register (folding meters) | Recording per-roll measurements | Handwritten |
| Paper notebook (reconciliation) | Matching folding meters to factory meters | Handwritten |
| Head office ERP (Gradation Report) | Generating the yield analysis report | Computer-generated, but data entry happens at head office, not factory |

## Handoffs

- **Comes from:** Inbound/storage area. Grey material that was received and filed.
- **Goes to (Fresh):** Packing program allocation → cutting and packing.
- **Goes to (Good Cut, Fent, Rags, Chindi):** Accumulation area for Todiya.
- **Goes to (Not Acceptable):** Separate storage → reprocess/return pipeline.
- **Goes to (Decision Pending):** Hold area. Material stays here until someone decides what to do with it.

## Decision Pending Lots — A Special Case

Not all lots get graded immediately. Some lots enter a **"Decision Pending"** state where the quality is unclear and no one is sure how to classify the material.

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

### Why Lots Get Stuck

- Quality is borderline — not clearly Fresh but not clearly defective
- The defect type is unusual and no one knows how to grade it
- No one takes ownership of making the decision
- The lot is small and doesn't justify the effort of a detailed assessment
- The relevant supervisor or manager hasn't gotten around to it

### System Implications

Each decision-pending lot needs:
- A **remark field** — free text describing the issue
- A **resolution pipeline** — workflow to move from pending → decided
- **Aging alerts** — flag lots that have been pending beyond a threshold (e.g., 30 days, 90 days)
- **Escalation** — notify supervisors or managers when lots are aging

This is a clear pain point where the system can add immediate value — making pending lots visible and preventing them from being forgotten.

## Problems and Workarounds

| Problem | Frequency | Current Workaround | Impact |
|---|---|---|---|
| Folding meters recorded only on paper | Always | Handwritten registers | Data not queryable, not backed up, hard to aggregate |
| Gradation data entered at head office, not factory | Always | Factory sends paper data to head office for entry | Delay between grading and report generation |
| Decision-pending lots forgotten | Frequent | Periodic manual review of the register | Lots sit for months/years, tying up space and capital |
| No real-time visibility into grading progress | Always | Ask the folding team directly | Cannot plan packing programs based on what's ready |
| Chadat not systematically recorded | Sometimes | Calculated ad-hoc when needed | Inconsistent conversion between meters and kg |
| Meter reconciliation is manual | Always | Side-by-side comparison in notebook | Tedious, error-prone for large lots |

## Design Implications for the System

### Must Have
1. **Folding entry screen** — Workers record per-roll measurements as they fold. Links to the MRL/lot.
2. **Grading entry** — Classify each section as Fresh / Good Cut / Fent / Rags / Chindi / Not Acceptable.
3. **Chadat recording** — Capture the meters-to-kg conversion factor per lot.
4. **Progressive Gradation Report** — Auto-generated, updates as grading progresses. Shows: meter progression (grey → folded → graded), grade breakdown (% Fresh, etc.), shrinkage, non-fresh loss.
5. **Decision-pending workflow** — Remark field, resolution pipeline, aging alerts.
6. **Unit handling** — Fresh in meters, other grades in kg, with automatic Chadat conversion for reporting.

### Nice to Have
7. **Auto-reconciliation** — Import Gate Pass meters and compare against folding meters. Highlight discrepancies.
8. **Grading dashboard** — Show all lots in progress, % complete, and lots waiting to be graded.
9. **Historical Chadat tracking** — Track Chadat trends by quality code or vendor to spot patterns.
10. **Grade distribution analytics** — Show Fresh % trends over time, by vendor, by quality code.

### Not Needed
- Automated quality testing integration (no instruments in use)
- Worker productivity tracking (not requested, politically sensitive)
- Detailed defect categorization (grading is into 6 buckets, not detailed defect codes)

## Photos / Diagrams

Relevant scan pages from `00-inbox/rg faith scans.pdf`:
- **Page 5:** Ready Goods Report (handwritten) — the detailed measurement form used after folding
- **Page 6:** Fresh Pending Lots In Miroli 36" (page 1) — register of graded Fresh lots
- **Page 7:** Fresh Pending Lots In Miroli 36" (page 2) — continuation
- **Page 8:** Folding meters matched against factory meters — reconciliation notebook
- **Page 16:** Gradation Report (computer-generated) — the yield analysis report

## Raw Notes

From `00-inbox/notes.md`:
> "The first process is folding. No matter what comes in, the team at the first station folds it. Every meter gets a fold. That's when they first check the measurement and record how many meters it is."
>
> "After that, a quality check happens. They check how much of the lot is good or bad, then grade it. The grades are: Fresh grade (good quality), Four other grades: cut, fent, rags, and chindi, Not acceptable grade."
>
> "The not acceptable part gets cut from the fabric. We need to store that cut inventory separately because RG Faith needs to send it back to them."

From `00-inbox/note_2.md`:
> "Chadat is a conversion unit between meters and kilograms for the specific lot covered by the gradation report. Fresh cut is always measured in meters. Everything else, good cut, fent, rags, or chindi, is measured in kilograms."
>
> "The gradation report is a progressive report... the report itself should only cover the portion of the lot that has actually gone through the process up to whatever stage it's reached."

## Open Questions

1. ~~How exactly is the Chadat measured?~~ **RESOLVED:** Likely by weighing a 100-meter fold (standard fold length). System just captures the Chadat value; doesn't need to enforce the measurement method.
2. ~~Is grading done by the same workers who fold?~~ **RESOLVED:** Yes. Workers are multi-skilled, no dedicated roles per station.
3. ~~How is the "Not Acceptable" decision made?~~ **RESOLVED:** Judgment-based, no specific threshold. Two scenarios: (a) Full roll rejected before cutting — entire roll goes to Not Acceptable. (b) Defect found during cutting into 100m folds — defective section cut out and classified. Remainder continues as Fresh. Leftover short pieces (e.g., 12m tail of a 1012m roll) become Good Cut/Fent/Chindi based on quality.
4. ~~Is Not Acceptable physically cut out at this stage?~~ **RESOLVED:** Yes — either entire roll rejected before cutting, or defective section cut out during the 100m fold process.
5. ~~How does Gradation Report data get to head office?~~ **RESOLVED:** Physical document copies (packing slips, inward slips) are sent via RG Faith's own courier/helper to head office. Head office staff enters data into their ERP. Our system eliminates this round-trip.
6. ~~Do any lots skip grading?~~ **RESOLVED:** No, never. Every lot must go through folding and grading. System should enforce this sequence.
