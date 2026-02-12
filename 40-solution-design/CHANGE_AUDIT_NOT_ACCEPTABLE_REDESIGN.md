# Change Audit: NOT_ACCEPTABLE Redesign

**Date:** 2026-02-12
**Purpose:** Move NOT_ACCEPTABLE from packing execution (Module 05) to classification (Module 04)

## Executive Summary

This audit documents all files and specific changes required to implement the NOT_ACCEPTABLE redesign. The core change moves quality rejection from packing execution to the classification stage, with an issue-tracker resolution workflow.

### Key Design Decisions

1. **DECISION_PENDING state removed entirely** — only one "unacceptable" outcome at classification
2. **NOT_ACCEPTABLE assigned at Classification (Module 04)**, not Packing (Module 05)
3. **Remove NOT_ACCEPTABLE grade from packing execution** — thaan grades: Fresh, Good Cut, Fent, Rags, Chindi only
4. **NOT_ACCEPTABLE is NOT terminal** — transitions to: RETURNED_TO_VENDOR, DISPOSED, or CLASSIFIED
5. **Terminal states:** RETURNED_TO_VENDOR (out), DISPOSED (out), CLASSIFIED (continues to packing)
6. **Location:** NOT_ACCEPTABLE material → **MIROLI-HOLD** (new location)
7. **Module 08 repurposed:** triggered by classification, not packing
8. **Resolution types:** RETURNED_TO_VENDOR, DISPOSED, RECLASSIFIED
9. **Reclassification:** Single NA_ENTRY_RESOLVED event with tone_code_id + finish_code_id
10. **Gradation Report:** NOT_ACCEPTABLE tracked separately from packing gradation hierarchy
11. **CLASSIFICATION_RECORDED event:** `is_not_acceptable` boolean flag distinguishes classified vs not acceptable

---

## Files Requiring Changes

### Critical Files (Major Changes)

1. **00-overview.md** — State machines, locations, events, module descriptions
2. **04-quality-grading.md** — Add NOT_ACCEPTABLE outcome to classification
3. **05-packing-program.md** — Remove NOT_ACCEPTABLE from thaan grades
4. **08-not-acceptable-resolution.md** — Repurpose: triggered by classification, add RECLASSIFIED resolution
5. **reports.md** — Update R17 (remove), R18, R19, R01, R02, R07
6. **user-interactions.md** — Update classification interaction, remove NA from packing
7. **user-journeys.md** — Update classification and packing journeys

### Supporting Files (Minor Changes)

8. **01-master-data.md** — No changes expected (review only)
9. **02-outbound-inbound.md** — No changes expected (review only)
10. **03-folding-measurement.md** — No changes expected (review only)
11. **06-dispatch.md** — No changes expected (review only)
12. **07-todiya.md** — No changes expected (review only)
13. **09-packaging-materials.md** — No changes expected (deferred)

---

## Detailed Change Specifications

---

## FILE 1: 00-overview.md

**File:** `/Users/sharva/Workspaces/rg-faith/40-solution-design/rg-faith-miroli/00-overview.md`

### Section 1.1: Module Descriptions Table (Lines 17-27)

**Current Line 22:**
```
| 4 | Tone & Finish Classification | [04-quality-grading.md](04-quality-grading.md) | Assign tone code and finish code to folded material. Involves factory inspection and optional Head Office confirmation. Decision Pending for classification uncertainty. Not gradation — that happens embedded in Module 05 packing execution. |
```

**Change to:**
```
| 4 | Tone & Finish Classification | [04-quality-grading.md](04-quality-grading.md) | Assign tone code and finish code to folded material, OR mark as Not Acceptable if material is rejected. Involves factory inspection and optional Head Office confirmation. Not Acceptable material enters resolution workflow (Module 08). Not gradation — that happens embedded in Module 05 packing execution. |
```

**Current Line 23:**
```
| 5 | Packing Program | [05-packing-program.md](05-packing-program.md) | Create packing programs (cross-lot roll selection), execute in two phases: Phase 1 logs thaans with embedded gradation (Fresh/Good Cut/Fent/Rags/Chindi/NA), Phase 2 assembles Fresh thaans into bales. Gradation Report produced here. |
```

**Change to:**
```
| 5 | Packing Program | [05-packing-program.md](05-packing-program.md) | Create packing programs (cross-lot roll selection), execute in two phases: Phase 1 logs thaans with embedded gradation (Fresh/Good Cut/Fent/Rags/Chindi), Phase 2 assembles Fresh thaans into bales. Gradation Report produced here. |
```

**Current Line 26:**
```
| 8 | Not Acceptable Resolution | [08-not-acceptable-resolution.md](08-not-acceptable-resolution.md) | Reprocess List, vendor communication tracking, aging alerts, resolution workflow. NA material identified during packing execution (Module 05). |
```

**Change to:**
```
| 8 | Not Acceptable Resolution | [08-not-acceptable-resolution.md](08-not-acceptable-resolution.md) | Reprocess List, vendor communication tracking, aging alerts, resolution workflow. NA material identified at classification (Module 04). Three resolution paths: vendor pickup (RETURNED_TO_VENDOR), manager reclassifies (RECLASSIFIED), or write-off (DISPOSED). |
```

### Section 1.2: End-to-End Flow Diagram (Lines 29-105)

**Current Lines 77-82:**
```
                                   │ Tone + Finish    │
                                   │ assigned         │
                                   │ CLASSIFICATION_  │
                                   │ RECORDED         │
                                   └──┬───────────┬───┘
                                      │           │
                                      │           │ Decision
                                      │           │ Pending
                                      │           │ (14-day flag)
                                      ▼           ▼
                         ┌──────────────────┐  ┌──────────────┐
                         │ Packing Program  │  │ Awaiting     │
                         │ (5)              │  │ classification│
                         │                  │  │ decision     │
                         │ Phase 1: Thaans  │  └──────────────┘
                         │ (embedded grade) │
                         │ Phase 2: Bales   │
                         └──┬──────┬────┬───┘
```

**Change to:**
```
                                   │ Tone + Finish    │
                                   │ assigned OR      │
                                   │ Not Acceptable   │
                                   │ CLASSIFICATION_  │
                                   │ RECORDED         │
                                   └──┬───────────┬───┘
                                      │           │
                                      │           │ Not Acceptable
                                      │           │ (Module 08)
                                      ▼           ▼
                         ┌──────────────────┐  ┌──────────────┐
                         │ Packing Program  │  │ Not Acceptable│
                         │ (5)              │  │ Resolution   │
                         │                  │  │ (8)          │
                         │ Phase 1: Thaans  │  │              │
                         │ (embedded grade) │  │ Reprocess    │
                         │ Phase 2: Bales   │  │ List         │
                         └──┬──────┬────────┘  └──────────────┘
```

**Current Lines 91-94:**
```
                            │      │    │
                ┌───────────┘      │    └──────────────┐
                │ Fresh bales      │ Non-Fresh thaans  │ NA thaans
                ▼                  ▼                   ▼
```

**Change to:**
```
                            │      │
                ┌───────────┘      │
                │ Fresh bales      │ Non-Fresh thaans
                ▼                  ▼
```

**Remove Lines 95-98** (NA thaans branch from packing):
```
        ┌────────────┐    ┌────────────┐      ┌──────────────┐
        │ Dispatch    │    │ Todiya (7) │      │ Not Acceptable│
        │ (6)         │    │            │      │ Resolution   │
        │             │    │ Unpack +   │      │ (8)          │
```

**Change to:**
```
        ┌────────────┐    ┌────────────┐
        │ Dispatch    │    │ Todiya (7) │
        │ (6)         │    │            │
        │             │    │ Unpack +   │
```

### Section 1.3: Shared Event Types Table (Lines 131-158)

**Remove Lines 142-144** (DECISION_PENDING events):
```
| `DECISION_PENDING_CREATED` | Classification (4) | Inventory projection | Flags material with uncertain classification. 14-day aging alert. |
| `DECISION_PENDING_COMMENTED` | Classification (4) | Classification projection | Adds comment to Decision Pending entry. Resets 14-day aging clock. |
| `DECISION_PENDING_RESOLVED` | Classification (4) | Inventory projection, Classification projection | Resolves classification uncertainty by assigning tone and finish. |
```

**Update Line 140:**
```
| `CLASSIFICATION_RECORDED` | Classification (4) | Inventory projection | Assigns tone and finish to material. State → CLASSIFIED at MIROLI-CLASSIFIED. |
```

**Change to:**
```
| `CLASSIFICATION_RECORDED` | Classification (4) | Inventory projection | Assigns tone and finish to material (State → CLASSIFIED), OR marks as Not Acceptable (State → NOT_ACCEPTABLE at MIROLI-HOLD). Event payload includes is_not_acceptable boolean flag. |
```

**Update Line 146:**
```
| `THAAN_LOGGED` | Packing Program (5) | Inventory projection, Gradation Report | Logs a thaan with grade. Fresh thaans → Fresh bales. Non-Fresh → non-Fresh bales (Todiya candidates). NA → Reprocess List. |
```

**Change to:**
```
| `THAAN_LOGGED` | Packing Program (5) | Inventory projection, Gradation Report | Logs a thaan with grade. Fresh thaans → Fresh bales. Non-Fresh → non-Fresh bales (Todiya candidates). Grades: FRESH, GOOD_CUT, FENT, RAGS, CHINDI only. |
```

**Update Line 156:**
```
| `NA_ENTRY_CREATED` | NA Resolution (8) | NA projection | Records rejected material on Reprocess List (also auto-created from THAAN_LOGGED when grade = NA) |
```

**Change to:**
```
| `NA_ENTRY_CREATED` | NA Resolution (8) | NA projection | Records rejected material on Reprocess List (auto-created from CLASSIFICATION_RECORDED when is_not_acceptable = true) |
```

**Update Line 158:**
```
| `NA_ENTRY_RESOLVED` | NA Resolution (8) | NA projection, Inventory projection | Resolves entry: vendor pickup or unresolved write-off |
```

**Change to:**
```
| `NA_ENTRY_RESOLVED` | NA Resolution (8) | NA projection, Inventory projection | Resolves entry with resolution_type: RETURNED_TO_VENDOR (material leaves), DISPOSED (write-off, material leaves), or RECLASSIFIED (includes tone_code_id + finish_code_id, transitions to CLASSIFIED) |
```

### Section 1.4: Locations Table (Lines 194-208)

**Add new location after Line 205** (after MIROLI-FG-OUT):
```
| Not Acceptable Hold | zone | `MIROLI-HOLD` | Material marked as Not Acceptable at classification, awaiting resolution (vendor pickup, disposal, or reclassification). |
```

**Update Line 206:**
```
| Not Acceptable Storage | zone | `MIROLI-NA` | Rejected material awaiting vendor return. |
```

**Change to:**
```
| Not Acceptable Storage | zone | `MIROLI-NA` | DEPRECATED — replaced by MIROLI-HOLD. Material marked as Not Acceptable during classification now uses MIROLI-HOLD. |
```

### Section 1.5: Fabric Inventory States Table (Lines 216-224)

**Remove Line 221:**
```
| `DECISION_PENDING` | MIROLI-FG | Classification (4) | Classification uncertain — samples sent to HO, 14-day aging alert |
```

**Update Line 224:**
```
| `NOT_ACCEPTABLE` | MIROLI-NA | Packing (5) | Rejected during cutting — entry on Reprocess List (Module 8) |
```

**Change to:**
```
| `NOT_ACCEPTABLE` | MIROLI-HOLD | Classification (4) | Rejected at classification — entry on Reprocess List (Module 08). NOT terminal — can transition to RETURNED_TO_VENDOR, DISPOSED, or CLASSIFIED. |
```

**Add new terminal states after Line 224:**
```
| `RETURNED_TO_VENDOR` | OUT (not at facility) | NA Resolution (8) | Material returned to vendor — terminal state, material left facility |
| `DISPOSED` | OUT (not at facility) | NA Resolution (8) | Material written off / disposed — terminal state, material left facility |
```

### Section 1.6: State Transition Diagram (Lines 243-268)

**Current Lines 247-253:**
```
Fabric Inventory:
  RECEIVED ──FOLDING_COMPLETED──► FOLDED
  FOLDED ──CLASSIFICATION_RECORDED──► CLASSIFIED
  FOLDED ──DECISION_PENDING_CREATED──► DECISION_PENDING
  DECISION_PENDING ──DECISION_PENDING_RESOLVED──► CLASSIFIED
  CLASSIFIED ──PACKING_PROGRAM_CREATED──► PROGRAM_ASSIGNED
  PROGRAM_ASSIGNED ──PACKING_PROGRAM_CANCELLED──► CLASSIFIED (reversal)
  PROGRAM_ASSIGNED ──THAAN_LOGGED (grade=NA)──► NOT_ACCEPTABLE (terminal)
```

**Change to:**
```
Fabric Inventory:
  RECEIVED ──FOLDING_COMPLETED──► FOLDED
  FOLDED ──CLASSIFICATION_RECORDED (is_not_acceptable=false)──► CLASSIFIED
  FOLDED ──CLASSIFICATION_RECORDED (is_not_acceptable=true)──► NOT_ACCEPTABLE
  NOT_ACCEPTABLE ──NA_ENTRY_RESOLVED (type=RECLASSIFIED)──► CLASSIFIED
  NOT_ACCEPTABLE ──NA_ENTRY_RESOLVED (type=RETURNED_TO_VENDOR)──► RETURNED_TO_VENDOR (terminal)
  NOT_ACCEPTABLE ──NA_ENTRY_RESOLVED (type=DISPOSED)──► DISPOSED (terminal)
  CLASSIFIED ──PACKING_PROGRAM_CREATED──► PROGRAM_ASSIGNED
  PROGRAM_ASSIGNED ──PACKING_PROGRAM_CANCELLED──► CLASSIFIED (reversal)
```

---

## FILE 2: 04-quality-grading.md

**File:** `/Users/sharva/Workspaces/rg-faith/40-solution-design/rg-faith-miroli/04-quality-grading.md`

### Section 2.1: Process Overview (Lines 1-30)

**Current Line 7:**
```
This module covers the assignment of two classification attributes — **Tone** and **Finish** — to material after folding at Miroli. Classification determines the visual and tactile characteristics of the fabric, which are required before packing programs can be issued. This module does **not** handle quality grading. Gradation (Fresh, Good Cut, Fent, Rags, Chindi, Not Acceptable) happens only as a byproduct of packing execution in Module 05.
```

**Change to:**
```
This module covers the assignment of two classification attributes — **Tone** and **Finish** — to material after folding at Miroli, OR the rejection of material as **Not Acceptable**. Classification determines the visual and tactile characteristics of the fabric, which are required before packing programs can be issued. Material marked as Not Acceptable at this stage enters a resolution workflow (Module 08) with three possible outcomes: vendor pickup, disposal, or manager reclassification. This module does **not** handle packing gradation. Gradation (Fresh, Good Cut, Fent, Rags, Chindi) happens only as a byproduct of packing execution in Module 05.
```

**Current Lines 13-14:**
```
Borderline or uncertain cases enter a "Decision Pending" state for classification uncertainty (not quality uncertainty). Decision Pending entries with no activity for 14 days are flagged for revisit.
```

**Remove these lines entirely.**

**Current Lines 17-28 (Flow diagram):**
```
Flow:

```
  Rough Inspection          HO Confirmation           Record Classification
     [ENTRY]                   [ENTRY]                    [ENTRY]
        |                         |                           |
  (visual inspection)        Samples sent to HO         CLASSIFICATION_RECORDED
        |                         |                           |
  identify candidate         HO confirms tone            (record in system)
  tone + finish               and finish                      |
        |                         |                     Material → CLASSIFIED
     [EXIT]                    [EXIT]                      [EXIT]
```
```

**Change to:**
```
Flow:

```
  Rough Inspection          HO Confirmation           Record Classification
     [ENTRY]                   [ENTRY]                    [ENTRY]
        |                         |                           |
  (visual inspection)        Samples sent to HO         CLASSIFICATION_RECORDED
        |                         |                           |
  Option 1: Classify        HO confirms tone            Option 1: tone + finish assigned
  (assign tone + finish)     and finish                      |
        |                         |                     Material → CLASSIFIED
  Option 2: Reject          Option 2: Material              |
  (mark Not Acceptable)      rejected                   Option 2: is_not_acceptable=true
        |                         |                           |
     [EXIT]                    [EXIT]                  Material → NOT_ACCEPTABLE
                                                             |
                                                        NA_ENTRY_CREATED
                                                        (Module 08 workflow)
                                                             |
                                                          [EXIT]
```
```

### Section 2.2: Entities (Lines 33-76)

**Remove "Decision Pending Entry" entity entirely (Lines 62-76).**

**Update Classification Record entity (Lines 44-60):**

**Add new field after finish_code_id (Line 52):**
```
| is_not_acceptable | boolean | True if material is marked as Not Acceptable (tone_code_id and finish_code_id will be null). False if normal classification. |
| rejection_reason | string | Reason for Not Acceptable marking (required if is_not_acceptable=true, null otherwise) |
```

### Section 2.3: Process Steps - Record Classification (Lines 84-180)

**Update event description (Lines 88-100):**

**Current:**
```
Event type: `CLASSIFICATION_RECORDED`

Trigger:
  Classification worker or supervisor opens the Record Classification screen, selects an MRL
  (filtered to material in FOLDED or AWAITING_CLASSIFICATION state), selects a tone code and
  finish code, specifies the scope (roll, lot, or partial lot), enters metres classified, and
  optionally records sample and HO confirmation dates. Clicks Submit.

Data points captured:
  - mrl_id: UUID — which MRL
  - inbound_receipt_id: UUID (optional) — which specific lot, if classification is lot-level
  - tone_code_id: UUID — selected from Tone Code master data
  - finish_code_id: UUID — selected from Finish Code master data
```

**Change to:**
```
Event type: `CLASSIFICATION_RECORDED`

Trigger:
  Classification worker or supervisor opens the Record Classification screen, selects an MRL
  (filtered to material in FOLDED or AWAITING_CLASSIFICATION state).

  Option 1 (Classify): Selects a tone code and finish code, specifies the scope (roll, lot, or partial lot), enters metres classified, and optionally records sample and HO confirmation dates. Sets is_not_acceptable = false.

  Option 2 (Mark Not Acceptable): Marks material as Not Acceptable, enters rejection reason, specifies metres. Sets is_not_acceptable = true, tone_code_id and finish_code_id remain null.

  Clicks Submit.

Data points captured:
  - mrl_id: UUID — which MRL
  - inbound_receipt_id: UUID (optional) — which specific lot, if classification is lot-level
  - is_not_acceptable: boolean — true if material rejected, false if classified
  - tone_code_id: UUID — selected from Tone Code master data (null if is_not_acceptable=true, required if false)
  - finish_code_id: UUID — selected from Finish Code master data (null if is_not_acceptable=true, required if false)
  - rejection_reason: string — reason for rejection (required if is_not_acceptable=true, null otherwise)
```

**Update Payload section (around Line 110):**

**Add after finish_code_id:**
```
  is_not_acceptable: boolean
  rejection_reason: string (if is_not_acceptable=true)
```

**Update Preconditions section (around Line 120):**

**Add:**
```
  - If is_not_acceptable = false: tone_code_id and finish_code_id must be provided
  - If is_not_acceptable = true: tone_code_id and finish_code_id must be null, rejection_reason required
```

**Update Side effects section (around Line 130):**

**Current:**
```
Side effects:
  - fabric_inventory: state → CLASSIFIED, location → MIROLI-CLASSIFIED
```

**Change to:**
```
Side effects:
  - If is_not_acceptable = false:
    * fabric_inventory: state → CLASSIFIED, location → MIROLI-CLASSIFIED
  - If is_not_acceptable = true:
    * fabric_inventory: state → NOT_ACCEPTABLE, location → MIROLI-HOLD
    * Auto-triggers NA_ENTRY_CREATED event (Module 08)
    * Entry created on Reprocess List
```

### Section 2.4: Remove Decision Pending Process Steps (Lines 193-263)

**Remove entirely:**
- Step: Create Decision Pending Entry (DECISION_PENDING_CREATED)
- Step: Comment on Decision Pending Entry (DECISION_PENDING_COMMENTED)
- Step: Resolve Decision Pending Entry (DECISION_PENDING_RESOLVED)

### Section 2.5: Reports (Lines 330-360)

**Remove R17 — Decision Pending Aging Report entirely.**

---

## FILE 3: 05-packing-program.md

**File:** `/Users/sharva/Workspaces/rg-faith/40-solution-design/rg-faith-miroli/05-packing-program.md`

### Section 3.1: Process Overview (Lines 1-34)

**Current Line 9:**
```
**Gradation is embedded in packing execution.** There is no standalone grading step. During Phase 1, as each roll is cut, the majority produces Fresh thaans. Any non-Fresh material (Good Cut, Fent, Rags, Chindi) is logged as non-Fresh thaans with the appropriate grade — this IS the gradation. The Gradation Report is a progressive projection updated every time a thaan is logged. Not Acceptable material identified during cutting is logged in metres and creates an entry on the Reprocess List (Module 08).
```

**Change to:**
```
**Gradation is embedded in packing execution.** There is no standalone grading step. During Phase 1, as each roll is cut, the majority produces Fresh thaans. Any non-Fresh material (Good Cut, Fent, Rags, Chindi) is logged as non-Fresh thaans with the appropriate grade — this IS the gradation. The Gradation Report is a progressive projection updated every time a thaan is logged. Material rejected for quality issues is marked as Not Acceptable at the classification stage (Module 04), not during packing.
```

### Section 3.2: Thaan Entity (Lines 96-109)

**Current Line 104:**
```
| grade | string | FRESH, GOOD_CUT, FENT, RAGS, CHINDI, or NOT_ACCEPTABLE |
```

**Change to:**
```
| grade | string | FRESH, GOOD_CUT, FENT, RAGS, or CHINDI |
```

**Current Lines 105-106:**
```
| metres | decimal | For Fresh, Good Cut, and Not Acceptable thaans (always in metres) |
| kilograms | decimal | For Fent, Rags, and Chindi thaans (always in kg; metres derived via Chadat) |
```

**Change to:**
```
| metres | decimal | For Fresh and Good Cut thaans (always in metres) |
| kilograms | decimal | For Fent, Rags, and Chindi thaans (always in kg; metres derived via Chadat) |
```

### Section 3.3: Gradation Report Entity (Lines 135-157)

**Current Line 152:**
```
| not_acceptable_metres | decimal | Sum of NOT_ACCEPTABLE thaans in metres |
```

**Change to:**
```
| not_acceptable_metres | decimal | Material rejected at classification (Module 04), tracked separately from packing gradation. Not part of packing yield calculation. |
```

**Add note after Line 157:**
```
**Note:** not_acceptable_metres is populated from CLASSIFICATION_RECORDED events (Module 04) where is_not_acceptable=true, NOT from THAAN_LOGGED events. This field tracks material rejected before it reaches packing, displayed separately in the Gradation Report.
```

### Section 3.4: Event - THAAN_LOGGED (Lines 256-319)

**Current Line 273:**
```
  - grade: string — FRESH, GOOD_CUT, FENT, RAGS, CHINDI, or NOT_ACCEPTABLE
```

**Change to:**
```
  - grade: string — FRESH, GOOD_CUT, FENT, RAGS, or CHINDI
```

**Current Line 274:**
```
  - metres: decimal — for Fresh, Good Cut, and Not Acceptable (in metres)
```

**Change to:**
```
  - metres: decimal — for Fresh and Good Cut (in metres)
```

**Current Line 296:**
```
  - For FRESH, GOOD_CUT, NOT_ACCEPTABLE: metres must be > 0, kilograms = 0
```

**Change to:**
```
  - For FRESH, GOOD_CUT: metres must be > 0, kilograms = 0
```

**Remove Lines 306-308** (NOT_ACCEPTABLE side effects):
```
  - If grade = NOT_ACCEPTABLE:
    - fabric_inventory: state → NOT_ACCEPTABLE, location → MIROLI-NA
    - Creates NA_ENTRY_CREATED event on Reprocess List (Module 08)
```

**Update Line 315:**
```
  - not_acceptable_entries: if grade = NOT_ACCEPTABLE, new row on Reprocess List
```

**Remove this line entirely.**

### Section 3.5: Flow Diagram (Lines 567-573)

**Current:**
```
    D -->|"Grade = FRESH"| E["Fresh Thaan\n(CREATED)"]
    D -->|"Grade = GOOD_CUT /\nFENT / RAGS / CHINDI"| F["Non-Fresh Thaan\n→ Baled separately\n→ MIROLI-FG-OUT\n→ Todiya (Module 7)"]
    D -->|"Grade = NOT_ACCEPTABLE"| G["NA Thaan\n→ MIROLI-NA\n→ Reprocess List\n(Module 8)"]
```

**Change to:**
```
    D -->|"Grade = FRESH"| E["Fresh Thaan\n(CREATED)"]
    D -->|"Grade = GOOD_CUT /\nFENT / RAGS / CHINDI"| F["Non-Fresh Thaan\n→ Baled separately\n→ MIROLI-FG-OUT\n→ Todiya (Module 7)"]
```

---

## FILE 4: 08-not-acceptable-resolution.md

**File:** `/Users/sharva/Workspaces/rg-faith/40-solution-design/rg-faith-miroli/08-not-acceptable-resolution.md`

### Section 4.1: Process Overview (Lines 1-28)

**Current Lines 1-9:**
```
# Module 08 — Not Acceptable Resolution

## 1. Process Overview

### Process: Tracking and Resolving Rejected Material

This module tracks material identified as "Not Acceptable" during packing execution (Module 05) — rejected fabric that needs to be returned to the vendor mill. It functions as an **issue tracker**: rejected material is recorded on the Reprocess List, the vendor is contacted, back-and-forth discussion occurs, and eventually the vendor either picks up the material or it remains at Miroli indefinitely.
```

**Change to:**
```
# Module 08 — Not Acceptable Resolution

## 1. Process Overview

### Process: Tracking and Resolving Rejected Material

This module tracks material identified as "Not Acceptable" at the classification stage (Module 04) — rejected fabric that cannot proceed to packing. It functions as an **issue tracker**: rejected material is recorded on the Reprocess List, the vendor is contacted, back-and-forth discussion occurs, and eventually one of three outcomes occurs: (1) the vendor picks up the material (RETURNED_TO_VENDOR), (2) the material is written off / disposed (DISPOSED), or (3) the manager overrides the rejection and reclassifies the material with tone and finish codes (RECLASSIFIED), allowing it to proceed to packing.
```

**Current Lines 11-15:**
```
Material identified as NA during packing is always measured in **metres** (never kg) — per CLAUDE.md and domain glossary. NA is distinct from other non-Fresh grades (Good Cut, Fent, Rags, Chindi), which are measured in kg and require Chadat conversion.

Timing is highly variable: some entries are resolved in days, others remain open for months or even years. There is no enforced SLA or aging escalation — entries simply appear on a report sorted by age.
```

**Change to:**
```
Material identified as NA at classification is always measured in **metres** (never kg) — per CLAUDE.md and domain glossary. NA is identified before packing execution and is entirely separate from packing gradation (Fresh, Good Cut, Fent, Rags, Chindi).

Timing is highly variable: some entries are resolved in days, others remain open for months or even years. There is no enforced SLA or aging escalation — entries simply appear on a report sorted by age.
```

**Update Flow diagram (Lines 18-28):**

**Current:**
```
Flow:

```
  Packing Execution         Create NA Entry         Vendor Communication      Resolution
      [ENTRY]                   [ENTRY]                   [ENTRY]             [ENTRY]
         |                         |                         |                    |
  Thaan logged as NA       NA_ENTRY_CREATED         NA_ENTRY_COMMENTED     NA_ENTRY_RESOLVED
  (THAAN_LOGGED)                  |                         |                    |
         |                   Reprocess List          Vendor contacted      Vendor picks up OR
     [EXIT]                  entry created            Discussion ongoing    write-off (unresolved)
                                  |                         |                    |
                               [EXIT]                    [EXIT]                [EXIT]
```
```

**Change to:**
```
Flow:

```
  Classification            Create NA Entry         Vendor Communication      Resolution
      [ENTRY]                   [ENTRY]                   [ENTRY]             [ENTRY]
         |                         |                         |                    |
  Material marked NA        NA_ENTRY_CREATED         NA_ENTRY_COMMENTED     NA_ENTRY_RESOLVED
  (CLASSIFICATION_                |                         |                    |
   RECORDED,                Reprocess List          Vendor contacted      Option 1: Vendor pickup
   is_not_acceptable=true)  entry created            Discussion ongoing         (RETURNED_TO_VENDOR)
         |                         |                         |                    |
     [EXIT]                      |                         |                Option 2: Write-off
                                 |                         |                     (DISPOSED)
                               [EXIT]                    [EXIT]                  |
                                                                            Option 3: Manager override
                                                                                 (RECLASSIFIED)
                                                                                   |
                                                                                [EXIT]
```
```

### Section 4.2: Not Acceptable Entry Entity (Lines 35-57)

**Add new fields after resolution_type (Line 51):**
```
| reclassified_tone_code_id | UUID (FK) | If resolution_type = RECLASSIFIED: which tone code was assigned (null otherwise) |
| reclassified_finish_code_id | UUID (FK) | If resolution_type = RECLASSIFIED: which finish code was assigned (null otherwise) |
```

### Section 4.3: Event - NA_ENTRY_CREATED (Lines 66-110)

**Current Lines 72-75:**
```
Trigger:
  When a thaan is logged with grade NOT_ACCEPTABLE during packing execution (Module 05), the
  system automatically creates a Reprocess List entry. Alternatively, a supervisor can manually
  create one from the Not Acceptable screen.
```

**Change to:**
```
Trigger:
  When material is marked as Not Acceptable during classification (Module 04), via CLASSIFICATION_RECORDED
  event with is_not_acceptable=true, the system automatically creates a Reprocess List entry.
  Alternatively, a supervisor can manually create one from the Not Acceptable screen.
```

**Update Line 104:**
```
  - fabric_inventory: state already set to NOT_ACCEPTABLE by packing module (THAAN_LOGGED with grade = NA)
```

**Change to:**
```
  - fabric_inventory: state already set to NOT_ACCEPTABLE by classification module (CLASSIFICATION_RECORDED with is_not_acceptable=true, location=MIROLI-HOLD)
```

### Section 4.4: Event - NA_ENTRY_RESOLVED (Lines 139-223)

**Current Lines 139-141:**
```
Event type: `NA_ENTRY_RESOLVED`

Trigger:
```

**Keep event type, update entire section:**

**Replace Lines 139-223 with:**
```
Event type: `NA_ENTRY_RESOLVED`

Trigger:
  Facility Manager or authorized supervisor opens a Reprocess List entry and chooses one of three
  resolution options:

  Option 1 (Vendor Pickup): Vendor has physically picked up the material. Material leaves facility.

  Option 2 (Dispose): Write-off — material is disposed of or remains at facility but will not be
  processed further. Material leaves facility or is scrapped.

  Option 3 (Reclassify): Manager overrides the Not Acceptable marking, assigns tone code and finish
  code, and allows material to proceed to packing as CLASSIFIED.

Data points captured:
  - na_entry_id: UUID
  - resolution_type: string — RETURNED_TO_VENDOR, DISPOSED, or RECLASSIFIED
  - resolution_notes: string — optional notes about the resolution
  - reclassified_tone_code_id: UUID (required if resolution_type = RECLASSIFIED, null otherwise)
  - reclassified_finish_code_id: UUID (required if resolution_type = RECLASSIFIED, null otherwise)

Payload:
  id: UUID (na_entry_id)
  resolution_type: string
  resolution_notes: string
  reclassified_tone_code_id: UUID (if applicable)
  reclassified_finish_code_id: UUID (if applicable)
  resolved_at: datetime (now)

Aggregate: NotAcceptableEntry / id

Location: MIROLI-HOLD

Preconditions:
  - Entry must exist with status = OPEN or IN_DISCUSSION
  - If resolution_type = RECLASSIFIED: reclassified_tone_code_id and reclassified_finish_code_id must be provided
  - If resolution_type = RETURNED_TO_VENDOR or DISPOSED: reclassified fields must be null

Side effects:
  - If resolution_type = RETURNED_TO_VENDOR:
    * fabric_inventory: state → RETURNED_TO_VENDOR, location → OUT (material left facility)
  - If resolution_type = DISPOSED:
    * fabric_inventory: state → DISPOSED, location → OUT (material left facility)
  - If resolution_type = RECLASSIFIED:
    * fabric_inventory: state → CLASSIFIED, location → MIROLI-CLASSIFIED
    * Material now eligible for packing programs
    * Tone and finish codes recorded in fabric_inventory record

Projections updated:
  - not_acceptable_entries: status → RESOLVED, resolution_type set, resolved_at → now, reclassified fields populated if applicable
  - fabric_inventory: state and location updated per resolution_type

Permissions:
  - events:NA_ENTRY_RESOLVED:emit (FACILITY_MANAGER, SUPERVISOR with authorization)

Business rules:
  - RECLASSIFIED resolution requires both tone and finish codes
  - Once resolved, entry cannot be reopened (resolution is permanent)
  - Material that is RETURNED_TO_VENDOR or DISPOSED exits the system entirely
```

### Section 4.5: Flow Diagram (Lines 312-322)

**Current:**
```
flowchart TD
    A["Material identified as\nNOT_ACCEPTABLE\nduring packing (Module 5)"] -->|"NA_ENTRY_CREATED"| B["Reprocess List Entry\n(OPEN)"]
    B -->|"NA_ENTRY_COMMENTED\n(vendor contacted)"| C["In Discussion\n(IN_DISCUSSION)"]
    C -->|"NA_ENTRY_COMMENTED\n(ongoing discussion)"| C
    C -->|"Vendor arranges pickup"| D["Resolved: Vendor Pickup\n(RESOLVED)"]
    C -->|"Material remains at facility"| E["Resolved: Unresolved\n(RESOLVED)"]
```

**Change to:**
```
flowchart TD
    A["Material marked as\nNOT_ACCEPTABLE\nat classification (Module 4)"] -->|"NA_ENTRY_CREATED"| B["Reprocess List Entry\n(OPEN)"]
    B -->|"NA_ENTRY_COMMENTED\n(vendor contacted)"| C["In Discussion\n(IN_DISCUSSION)"]
    C -->|"NA_ENTRY_COMMENTED\n(ongoing discussion)"| C
    C -->|"NA_ENTRY_RESOLVED\n(RETURNED_TO_VENDOR)"| D["Material returned\nto vendor\n(RESOLVED)\nState: RETURNED_TO_VENDOR"]
    C -->|"NA_ENTRY_RESOLVED\n(DISPOSED)"| E["Material disposed\nof / written off\n(RESOLVED)\nState: DISPOSED"]
    C -->|"NA_ENTRY_RESOLVED\n(RECLASSIFIED)"| F["Manager overrides,\nassigns tone + finish\n(RESOLVED)\nState: CLASSIFIED"]
    F -->|"Material proceeds"| G["Available for\nPacking Programs"]
```

---

## FILE 5: reports.md

**File:** `/Users/sharva/Workspaces/rg-faith/40-solution-design/rg-faith-miroli/reports.md`

### Section 5.1: R01 — Stage-wise Inventory Report (Lines 25-48)

**Current Line 46:**
```
| Not Acceptable | Total metres at MIROLI-NA | `fabric_inventory` (state = NOT_ACCEPTABLE) |
```

**Change to:**
```
| Not Acceptable | Total metres at MIROLI-HOLD | `fabric_inventory` (state = NOT_ACCEPTABLE) |
```

### Section 5.2: R17 — Decision Pending Aging Report (Lines 545-569)

**Remove this report entirely.**

### Section 5.3: R18 — Not Acceptable Aging Report (Lines 572-599)

**Update description (Lines 574-575):**

**Current:**
```
**Purpose:** Identify rejected material (identified during packing) sitting longest, prioritize vendor communication for pickup.
```

**Change to:**
```
**Purpose:** Identify rejected material (identified at classification) sitting longest, prioritize vendor communication for pickup, disposal, or reclassification.
```

**Update content table (Lines 583-590):**

**Add column:**
```
| Column | Source | Description |
|---|---|---|
| ... existing columns ... |
| Possible Actions | Computed | "Vendor Pickup / Dispose / Reclassify" — three resolution options available |
```

### Section 5.4: R19 — NA Resolution History Report (Lines 602-626)

**Update resolution type values (Line 615):**

**Current:**
```
| Resolution Type | `not_acceptable_entries.resolution_type` | VENDOR_PICKUP or UNRESOLVED |
```

**Change to:**
```
| Resolution Type | `not_acceptable_entries.resolution_type` | RETURNED_TO_VENDOR, DISPOSED, or RECLASSIFIED |
```

**Update summary metrics (Lines 622-625):**

**Current:**
```
**Summary:**
- Average resolution time (days)
- % picked up vs. % unresolved
- By vendor: total resolutions, avg time, pickup rate
```

**Change to:**
```
**Summary:**
- Average resolution time (days)
- % returned to vendor vs. % disposed vs. % reclassified
- By vendor: total resolutions, avg time, breakdown by resolution type
- Reclassification rate (indicates quality of initial classification process)
```

### Section 5.5: R07 — Vendor Quality Performance Report (Lines 182-205)

**Update "Not Acceptable" description (Line 194):**

**Current:**
```
| Not Acceptable Metres | `thaans` | Sum of NA thaans logged (grade = NOT_ACCEPTABLE) |
```

**Change to:**
```
| Not Acceptable Metres | `fabric_inventory` | Sum of material marked NOT_ACCEPTABLE at classification (Module 04) |
```

---

## FILE 6: user-interactions.md

**File:** `/Users/sharva/Workspaces/rg-faith/40-solution-design/rg-faith-miroli/user-interactions.md`

### Section 6.1: Interaction 4.1 — Record Classification (Lines 150-165)

**Update entire section:**

**Current:**
```
### 4.1 Record Classification

| **Field** | **Value** |
|---|---|
| **Interaction** | Record tone and finish classification for folded material |
| **User** | Classification Worker, Supervisor |
| **Trigger** | Material folded and ready for classification; HO may have confirmed tone and finish |
| **Data captured** | MRL (selected), Tone Code (selected), Finish Code (selected), Scope (Roll / Lot / Partial Lot), Metres Classified, Samples Sent Date (optional), HO Confirmed Date (optional), Notes |
| **System effect** | Classification record created. Material state → CLASSIFIED at MIROLI-CLASSIFIED. Material now eligible for packing programs. |
| **Auto side-effects** | Classification Report updated. Inventory dashboard updated (material moved from Folded to Classified). |
```

**Change to:**
```
### 4.1 Record Classification or Mark Not Acceptable

| **Field** | **Value** |
|---|---|
| **Interaction** | Record tone and finish classification for folded material, OR mark material as Not Acceptable |
| **User** | Classification Worker, Supervisor |
| **Trigger** | Material folded and ready for classification; HO may have confirmed tone and finish, OR material is rejected for quality issues |
| **Data captured** | MRL (selected), Classification Decision (radio button: "Classify" or "Mark Not Acceptable").<br><br>**If Classify:** Tone Code (selected), Finish Code (selected), Scope (Roll / Lot / Partial Lot), Metres Classified, Samples Sent Date (optional), HO Confirmed Date (optional), Notes.<br><br>**If Mark Not Acceptable:** Rejection Reason (text), Metres Rejected. |
| **System effect** | **If Classify:** Classification record created. Material state → CLASSIFIED at MIROLI-CLASSIFIED. Material now eligible for packing programs.<br><br>**If Mark Not Acceptable:** Material state → NOT_ACCEPTABLE at MIROLI-HOLD. NA_ENTRY_CREATED event auto-triggered. Entry created on Reprocess List (Module 08). |
| **Auto side-effects** | **If Classify:** Classification Report updated. Inventory dashboard updated (material moved from Folded to Classified).<br><br>**If Mark Not Acceptable:** Reprocess List entry created. Gradation Report updated (not_acceptable_metres tracked separately). Inventory dashboard updated (material moved to Not Acceptable Hold). |
```

### Section 6.2: Remove Interaction 4.2 — Create Decision Pending Entry (Lines 167-172)

**Remove this interaction entirely.**

### Section 6.3: Remove Interaction 4.3 — Comment on Decision Pending Entry

**Remove this interaction entirely.**

### Section 6.4: Remove Interaction 4.4 — Resolve Decision Pending Entry

**Remove this interaction entirely.**

### Section 6.5: Interaction 5.2 — Log Thaan (Lines 176-180)

**Update entire section:**

**Current:**
```
### 5.2 Log Thaan

| **Field** | **Value** |
|---|---|
| **Interaction** | Cut a roll to specified length, fold it, and log the resulting thaan with a grade |
| **User** | Packing Worker |
| **Trigger** | Worker cuts a piece from a source roll and folds it per program specifications; grades the piece during the process |
| **Data captured** | Packing Program (selected), Source Roll (selected from program's allocated rolls), Grade (Fresh / Good Cut / Fent / Rags / Chindi / Not Acceptable), Quantity — metres for Fresh, Good Cut, Not Acceptable; kg for Fent, Rags, Chindi (Chadat must already be recorded for the source MRL if grade is kg-based) |
| **System effect** | Thaan record created. Thaan number auto-assigned. All grades available for bale assembly — Fresh thaans into Fresh bales, non-Fresh thaans (Good Cut / Fent / Rags / Chindi) into separate non-Fresh bales. Not Acceptable thaans create an entry on the Reprocess List. Gradation Report for the source MRL auto-updated. |
| **Auto side-effects** | If grade = NOT_ACCEPTABLE: auto-creates entry on Reprocess List with lot details. Gradation Report percentages recalculated (Fresh yield vs losses). |
```

**Change to:**
```
### 5.2 Log Thaan

| **Field** | **Value** |
|---|---|
| **Interaction** | Cut a roll to specified length, fold it, and log the resulting thaan with a grade |
| **User** | Packing Worker |
| **Trigger** | Worker cuts a piece from a source roll and folds it per program specifications; grades the piece during the process |
| **Data captured** | Packing Program (selected), Source Roll (selected from program's allocated rolls), Grade (Fresh / Good Cut / Fent / Rags / Chindi), Quantity — metres for Fresh, Good Cut; kg for Fent, Rags, Chindi (Chadat must already be recorded for the source MRL if grade is kg-based) |
| **System effect** | Thaan record created. Thaan number auto-assigned. All grades available for bale assembly — Fresh thaans into Fresh bales, non-Fresh thaans (Good Cut / Fent / Rags / Chindi) into separate non-Fresh bales. Gradation Report for the source MRL auto-updated. |
| **Auto side-effects** | Gradation Report percentages recalculated (Fresh yield vs losses). NOT_ACCEPTABLE is NOT a valid grade at packing — quality rejection happens at classification (Module 04). |
```

### Section 6.6: Interaction 8.2 — Resolve NA Entry (Lines 195-200)

**Update entire section:**

**Current:**
```
### 8.2 Resolve NA Entry

| **Field** | **Value** |
|---|---|
| **Interaction** | Close a Reprocess List entry once vendor picks up material or entry is deemed unresolved |
| **User** | Facility Manager |
| **Trigger** | Vendor has picked up the material, OR it's determined the material will remain at Miroli indefinitely |
| **Data captured** | NA Entry (selected), Resolution Type (Vendor Pickup / Unresolved), Resolution Notes |
| **System effect** | Entry marked RESOLVED. Material either removed from inventory (vendor pickup) or remains at MIROLI-NA (unresolved). |
| **Auto side-effects** | Reprocess List entry removed from active list. Resolution metrics updated (R19 report). |
```

**Change to:**
```
### 8.2 Resolve NA Entry

| **Field** | **Value** |
|---|---|
| **Interaction** | Close a Reprocess List entry with one of three resolution outcomes |
| **User** | Facility Manager, Authorized Supervisor |
| **Trigger** | Vendor has picked up material, OR material is written off/disposed, OR manager overrides and reclassifies material |
| **Data captured** | NA Entry (selected), Resolution Type (Returned to Vendor / Disposed / Reclassified), Resolution Notes.<br><br>**If Reclassified:** Tone Code (selected), Finish Code (selected). |
| **System effect** | Entry marked RESOLVED. Material state updated:<br>- **Returned to Vendor:** State → RETURNED_TO_VENDOR, location → OUT (left facility)<br>- **Disposed:** State → DISPOSED, location → OUT (left facility)<br>- **Reclassified:** State → CLASSIFIED, location → MIROLI-CLASSIFIED (proceeds to packing) |
| **Auto side-effects** | Reprocess List entry removed from active list. Resolution metrics updated (R19 report). If reclassified: material becomes available for packing program allocation. |
```

---

## FILE 7: user-journeys.md

**File:** `/Users/sharva/Workspaces/rg-faith/40-solution-design/rg-faith-miroli/user-journeys.md`

### Section 7.1: Classification Worker Journey

**Locate classification-related journey entries and update:**

**Current (example):**
```
10:30 AM — Records classification for MRL #531 (lot just folded)
  - Opens Record Classification screen
  - Selects MRL #531
  - Tone: O1W (Off-White), Finish: 01
  - Scope: Lot (entire lot has consistent tone/finish)
  - 2,150 metres classified
  - Notes: "HO confirmed via WhatsApp at 10:15 AM"
  - System: Material → CLASSIFIED, ready for packing
```

**Change to:**
```
10:30 AM — Records classification for MRL #531 (lot just folded)
  - Opens Record Classification screen
  - Selects MRL #531
  - Decision: "Classify" (material is acceptable)
  - Tone: O1W (Off-White), Finish: 01
  - Scope: Lot (entire lot has consistent tone/finish)
  - 2,150 metres classified
  - Notes: "HO confirmed via WhatsApp at 10:15 AM"
  - System: Material → CLASSIFIED, ready for packing

11:15 AM — Marks MRL #542 as Not Acceptable (quality issue identified)
  - Opens Record Classification screen
  - Selects MRL #542
  - Decision: "Mark Not Acceptable"
  - Rejection Reason: "Fabric has visible defects and color bleeding throughout"
  - 1,800 metres rejected
  - System: Material → NOT_ACCEPTABLE at MIROLI-HOLD
  - System: NA_ENTRY_CREATED (auto) — entry appears on Reprocess List
```

### Section 7.2: Facility Manager Journey

**Add new entry for NA resolution:**
```
2:45 PM — Reviews and resolves Not Acceptable entries
  - Opens Reprocess List (Module 08)
  - Reviews entry for MRL #542 (marked NA this morning)
  - Contacts vendor via phone — vendor agrees to pick up next week
  - Resolves entry: Resolution Type = "Returned to Vendor"
  - Notes: "Vendor will collect on 2026-02-19, truck ETA 2 PM"
  - System: Entry → RESOLVED, material state → RETURNED_TO_VENDOR

3:15 PM — Overrides Not Acceptable marking for MRL #548
  - Opens Reprocess List
  - Reviews entry for MRL #548 (marked NA yesterday)
  - Decides quality is acceptable after closer inspection
  - Resolves entry: Resolution Type = "Reclassified"
  - Assigns Tone: O1W, Finish: 02
  - System: Entry → RESOLVED, material state → CLASSIFIED
  - System: Material now available for packing programs
```

### Section 7.3: Packing Worker Journey

**Update packing entries to remove NOT_ACCEPTABLE grade:**

**Current (example):**
```
11:00 AM — Logs thaans for Program #125
  - Cuts roll #1: 25m piece → Grade: Fresh → Thaan #501 logged
  - Cuts roll #1: 25m piece → Grade: Fresh → Thaan #502 logged
  - Cuts roll #2: 18m piece → Grade: Good Cut → Thaan #503 logged (slightly shorter)
  - Cuts roll #3: 12m piece → Grade: Not Acceptable → Thaan #504 logged
    * System auto-creates NA entry on Reprocess List
  - Gradation Report updated: Fresh %, Good Cut, NA metres tracked
```

**Change to:**
```
11:00 AM — Logs thaans for Program #125
  - Cuts roll #1: 25m piece → Grade: Fresh → Thaan #501 logged
  - Cuts roll #1: 25m piece → Grade: Fresh → Thaan #502 logged
  - Cuts roll #2: 18m piece → Grade: Good Cut → Thaan #503 logged (slightly shorter)
  - Cuts roll #3: 3.2kg piece → Grade: Fent → Thaan #504 logged (measured in kg)
    * System calculates metres via Chadat
  - Gradation Report updated: Fresh %, Good Cut, Fent tracked

  Note: If worker encounters severely defective material during packing, escalates to manager — quality rejection should have happened at classification (Module 04), not here.
```

---

## Supporting Files — Review Only

These files are not expected to require changes, but should be reviewed to confirm:

### FILE 8: 01-master-data.md
**Review:** Confirm Finish Code entity exists. No other changes expected.

### FILE 9: 02-outbound-inbound.md
**Review:** No references to NOT_ACCEPTABLE expected. No changes.

### FILE 10: 03-folding-measurement.md
**Review:** No references to NOT_ACCEPTABLE or DECISION_PENDING expected. No changes.

### FILE 11: 06-dispatch.md
**Review:** No references to NOT_ACCEPTABLE expected. No changes.

### FILE 12: 07-todiya.md
**Review:** No references to NOT_ACCEPTABLE expected (Todiya handles non-Fresh thaans, not NA material). No changes.

### FILE 13: 09-packaging-materials.md
**Review:** Deferred module, no changes.

---

## Summary of Changes by Impact

### Critical Changes (Must Implement)

1. **State Machine Overhaul** (00-overview.md)
   - Remove DECISION_PENDING state and all transitions
   - Add NOT_ACCEPTABLE transitions from FOLDED (via CLASSIFICATION_RECORDED)
   - Add terminal states: RETURNED_TO_VENDOR, DISPOSED
   - Add transition: NOT_ACCEPTABLE → CLASSIFIED (via RECLASSIFIED)

2. **Classification Module Redesign** (04-quality-grading.md)
   - Add NOT_ACCEPTABLE outcome to CLASSIFICATION_RECORDED event
   - Add is_not_acceptable boolean flag and rejection_reason field
   - Remove all Decision Pending entities, events, and process steps
   - Update flow diagram to show two classification paths

3. **Packing Module Simplification** (05-packing-program.md)
   - Remove NOT_ACCEPTABLE from thaan grade enum
   - Update Gradation Report: not_acceptable_metres tracked from Module 04, not Module 05
   - Remove NA-related side effects from THAAN_LOGGED event

4. **NA Resolution Module Expansion** (08-not-acceptable-resolution.md)
   - Change trigger from packing to classification
   - Add three resolution types: RETURNED_TO_VENDOR, DISPOSED, RECLASSIFIED
   - Add reclassification fields (tone_code_id, finish_code_id) to resolution event
   - Update flow diagram with three resolution paths

### High-Priority Changes (User-Facing)

5. **User Interactions** (user-interactions.md)
   - Update 4.1 (Record Classification) to include Not Acceptable option
   - Remove Decision Pending interactions (4.2, 4.3, 4.4)
   - Update 5.2 (Log Thaan) to remove NOT_ACCEPTABLE grade
   - Update 8.2 (Resolve NA Entry) with three resolution types

6. **Reports** (reports.md)
   - Remove R17 (Decision Pending Aging Report)
   - Update R18 (NA Aging Report) — triggered by classification
   - Update R19 (NA Resolution History) — three resolution types
   - Update R01 (Stage-wise Inventory) — MIROLI-HOLD location
   - Update R07 (Vendor Quality) — NA from classification

7. **User Journeys** (user-journeys.md)
   - Add classification rejection journeys
   - Add NA resolution journeys (all three types)
   - Remove Decision Pending journeys
   - Update packing journeys to remove NA grade

### Low-Priority Changes (Consistency)

8. **Location Updates** (00-overview.md)
   - Add MIROLI-HOLD location
   - Deprecate MIROLI-NA (or repurpose)

9. **Event Table Updates** (00-overview.md)
   - Remove DECISION_PENDING_* events
   - Update CLASSIFICATION_RECORDED description
   - Update THAAN_LOGGED description
   - Update NA_ENTRY_CREATED trigger
   - Update NA_ENTRY_RESOLVED outcomes

---

## Implementation Checklist

- [ ] Update 00-overview.md (state machines, events, locations, module descriptions)
- [ ] Update 04-quality-grading.md (add NOT_ACCEPTABLE path, remove DECISION_PENDING)
- [ ] Update 05-packing-program.md (remove NOT_ACCEPTABLE grade from thaans)
- [ ] Update 08-not-acceptable-resolution.md (add RECLASSIFIED, update trigger to classification)
- [ ] Update reports.md (remove R17, update R18/R19/R01/R07)
- [ ] Update user-interactions.md (classification, packing, NA resolution)
- [ ] Update user-journeys.md (classification, NA resolution journeys)
- [ ] Review supporting files (01, 02, 03, 06, 07, 09) for unintended references

---

## Risk Assessment

### High Risk
- **Breaking change to THAAN_LOGGED event** — downstream consumers (Gradation Report, inventory projections) must handle removal of NOT_ACCEPTABLE grade
- **State machine logic change** — all state transition handlers must be updated

### Medium Risk
- **Report queries** — R17 removal, R18/R19 data source changes
- **User training** — classification workers now handle quality rejection

### Low Risk
- **Location renaming** — MIROLI-NA → MIROLI-HOLD (cosmetic)
- **Documentation updates** — user journeys, process maps

---

## Questions for Clarification

1. **Gradation Report not_acceptable_metres:** Currently populated from THAAN_LOGGED (Module 05). After redesign, should it be populated from CLASSIFICATION_RECORDED (Module 04) events where is_not_acceptable=true? **Assumed: Yes, per Q9.**

2. **MIROLI-NA location:** Should it be deprecated, repurposed, or removed? **Assumed: Deprecated, replaced by MIROLI-HOLD.**

3. **Reclassification permissions:** Should reclassification be restricted to FACILITY_MANAGER only, or also SUPERVISOR? **Assumed: Both, per Module 08 pattern.**

4. **Historical data:** What happens to existing NOT_ACCEPTABLE thaans logged from packing? **Out of scope for this audit — assume fresh implementation.**

---

**End of Change Audit**
