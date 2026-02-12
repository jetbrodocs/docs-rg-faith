# User Journeys — RG Faith Miroli Inventory System

This document describes how real users experience the system day-to-day. It is structured in four parts:

1. **Roles** — who uses the system and what they are responsible for
2. **A Day at Miroli** — a full timeline narrative following all roles through a typical day, showing how actions flow between people
3. **Role Reference** — per-role task breakdowns for quick reference
4. **Edge Cases and Error Scenarios** — how the system handles non-standard situations

---

## Part 1: Roles

| Role | Person | Location | Responsibility | Primary Screens |
|---|---|---|---|---|
| **Facility Manager** | Ramesh | Miroli floor | Decision-maker. Creates packing programs and Todiya instructions. Creates delivery forms and confirms dispatch (two-step). Reviews dashboards. Handles vendor issues. | Dashboards, Create Packing Program, Create Todiya Instruction, Ready for Dispatch, Scheduled Pickups, Reprocess List |
| **Supervisor** | Kiran | Miroli floor (folding/classification/packing areas) | Operational lead. Records inbound receipts (creates MRLs on first receipt). Records per-roll folding measurements and Chadat. Records tone and finish classification or marks material as Not Acceptable. Logs thaans during packing. | Record Inbound Receipt, Record Folding, Record Chadat, Record Classification, Log Thaan |
| **Receiving Worker** | Anil | Miroli receiving area | Unloads trucks. Assists with bale loading for dispatch. | (physical — no primary screens in current scope) |
| **Packing Worker** | Deepa | Miroli packing area | Executes packing programs — logs thaans (cut + fold + grade) in Phase 1, then registers bales in Phase 2. | Log Thaan, Register Bale, Packing Program Detail |
| **Head Office User** | Priyanka | Ahmedabad head office (New Cloth Market) | Remote monitoring. Reviews dashboards and reports. Answers management queries. | Stage-wise Dashboard, Gradation Reports, Dispatch Dashboard |

All factory roles use a shared tablet or phone on the floor. Workers are multi-skilled — the same person may fold, classify, and pack depending on the day. The system roles above represent the *typical* primary responsibility, not rigid assignments.

---

## Part 2: A Day at Miroli

A single day at the facility, told chronologically. Every action by every role, in the order it happens. This is one continuous narrative — follow it from morning to evening to understand how the system knits together.

---

### 6:30 AM — Shift starts, Ramesh checks the state of the world

Ramesh arrives at Miroli and opens the system on the shared tablet near the office area. He navigates to the **Stage-wise Inventory Dashboard**. The numbers refresh from last night's closing state:

- Received inventory: 12,400 metres across 4 MRLs awaiting processing
- Folded (pending classification): 3,200 metres
- Classified (available for packing): 8,750 metres across 3 lots
- Packing programs in progress: 2 programs, 320 thaans logged, 14 bales completed of 22 planned
- Packed bales awaiting dispatch: 31 bales for 4 customers
- Scheduled pickups (not yet dispatched): 1 delivery form, 8 bales for customer VS

He switches to **Vendor Greige Pending**. FY26-MRL-0542 shows 2,800 metres of vendor-reported greige pending at Kalapurna Mills — it has been 9 days since that Gate Pass note. He makes a mental note to call them after breakfast.

He checks the **Decision Pending** screen. One entry has a red flag: "No activity for 16 days" — 100 metres from FY26-MRL-0531 with a remark about tone variation between rolls. He will need to look at the physical material later.

He checks the **Reprocess List**. Three open entries. One is 47 days old with no comments — FY26-MRL-0526 at PSJC, 1,408 metres of rejected fabric.

---

### 7:00 AM — Truck arrives from Kalapurna Mills

RG Faith's truck returns from Kalapurna Mills with dyed cloth. **Anil** is at the gate. He helps the driver unload 6 rolls of fabric from the truck and stacks them in the received storage area. The driver hands over the Gate Pass — a printed form from Kalapurna listing roll-by-roll metres, lot number 7993, quality code 44x45P6, 5,826.00 total metres. The Gate Pass also notes that 8,200 greige metres were originally sent and 2,374 greige metres remain pending.

**Kiran** arrives at the receiving area with the tablet. She opens **Record Inbound Receipt** and sees two options: "New MRL" and "Existing MRL." She has not received material from Kalapurna against this quality before, so she chooses **New MRL** (Path A). She enters the data:

- Vendor: Kalapurna Mills
- Quality Code: 44x45P6
- Avak Date: today
- Lot Number: 7993
- Received Metres: 5,826.00
- GSM: 120
- Width: 58"
- Rolls: 6
- Gate Pass Reference: KM-2026-4421
- Vendor Reported Greige Sent: 8,200 (from Gate Pass note)
- Vendor Reported Greige Pending: 2,374 (from Gate Pass note)

She clicks Submit. The system creates **FY26-MRL-0548** (new MRL, status ACTIVE) and receipt **FY26-IR-0042** together in one operation. The received inventory at MIROLI-RECEIVED increases by 5,826 metres. Material state is RECEIVED.

Kiran files the physical Gate Pass in the paper folder (old habit, still useful as backup). The digital record is now the source of truth.

---

### 7:30 AM — Folding team starts on yesterday's received lot

The folding workers pick up a lot that arrived yesterday — FY26-MRL-0535, Lot 7890, 4,200 received metres. They begin folding the rolls using a standard fold (~95-100cm) and measuring each roll as they go. This is physical, continuous work that takes most of the morning.

Meanwhile, **Kiran** opens **Pending Folding** on her tablet. She sees the lot the team is working on, plus the lot that just arrived (FY26-MRL-0548, 5,826 metres) — that one will be next.

---

### 9:00 AM — Head office checks in

At the Ahmedabad head office, **Priyanka** opens the **Stage-wise Inventory Dashboard**. She sees the same real-time data as Ramesh — including the 5,826 metres that Kiran just received 2 hours ago. No waiting for paper.

She checks **Total dispatch volume this month** — 847 bales, 86,420 metres across 23 delivery forms. She opens **Vendor Greige Pending** — 42,600 metres of vendor-reported greige outstanding across 8 vendors. She makes a note for the weekly management report.

Management asks her: "How much did we ship to customer S.P. this month?" She opens **Delivery Forms**, filters by customer = S.P. and date range = this month. The answer is immediate: 12 delivery forms, 74 bales, 7,820 metres.

---

### 9:30 AM — Head office calls with a sales order

Ramesh receives a phone call from head office. Customer Rame needs 5 bales of Officer brand — 20m cut, Book fold, SSTM stamp, trade number S8072-58".

He opens **Classified Material Available**. He sees material that has been classified (tone and finish assigned) and is eligible for packing programs:
- FY26-MRL-0533, Lot 7801: 5,644 metres, Tone O1W, Finish 01
- FY26-MRL-0530, Lot 7756: 2,100 metres, Tone O1W, Finish 01
- FY26-MRL-0528, Lot 7702: 1,006 metres, Tone O1W, Finish 02

He chooses FY26-MRL-0533. He clicks **Create Program from this lot** and fills in the **Create Packing Program** form. He selects source rolls from the lot (the system shows individual rolls with their measured metres from folding), sets the fold type to Book at the program level, and enters the line item:

- Line 1: Brand = SSTM, Product = Officer, Trade Number = S8072-58", Customer = Rame, Cut Length = 20m, Pieces/Bale = 15, Planned Bales = 5

The system calculates: 20m x 15 pieces x 5 bales = 1,500 metres allocated across the selected source rolls.

Ramesh reviews and clicks Submit. Program **PP-2026-0087** is created. The selected source rolls move from CLASSIFIED to PROGRAM_ASSIGNED at MIROLI-PACK.

He walks to the packing area and tells the team: "PP-2026-0087, five bales, Officer for Rame."

---

### 10:00 AM — Packing team starts execution: Phase 1 (Log Thaans)

**Deepa** opens **Packing Program Detail** for PP-2026-0087 on the tablet mounted near the cutting table. She sees the specifications clearly:

- SSTM / Officer / S8072-58" / Book fold / 20m cut / 15 pieces per bale / 5 bales planned
- Source rolls: 4 rolls from FY26-MRL-0533

She and two other workers begin cutting rolls into thaans. For each cut piece, Deepa opens the **Log Thaan** screen:

- Source Roll: Roll 1 (from MRL-0533)
- Grade: FRESH
- Metres: 20.00

She clicks Submit. The system auto-assigns thaan number **104832**. She continues logging thaans as each piece is cut and folded in Book style. Most pieces are Fresh. Occasionally the end of a roll yields a short piece or a section with a defect:

- Thaan 104847: Source Roll 2, Grade = GOOD_CUT, Metres = 4.25. Submit. (This Good Cut thaan will be assembled into a separate non-Fresh bale later.)
- Thaan 104851: Source Roll 3, Grade = FENT, Kilograms = 0.8. Submit. (Chadat was already recorded for this lot: 5.12 metres/kg. The system converts 0.8 kg to 4.10 equivalent metres and updates the Gradation Report.)

Each thaan logged updates the **Gradation Report** for FY26-MRL-0533 progressively — this IS the gradation. There is no standalone grading step.

---

### 10:30 AM — Folding in progress, Kiran records per-roll measurements

The folding team is working through lot FY26-MRL-0535, Lot 7890 (4,200 received metres). As the workers fold each roll at the standard fold (~95-100cm), **Kiran** records the metres for each roll on the **Record Folding** screen:

- Roll 1: 712.50 metres. Submit.
- Roll 2: 685.25 metres. Submit.
- Roll 3: 698.00 metres. Submit.
- ... (continues through the morning as each roll is completed)

By the time the team finishes the full lot (6 rolls), the total folding metres read **4,082.50 metres** — RG Faith's own verified count versus the vendor's reported 4,200 metres (shrinkage of 117.50 metres, 2.80%). The lot state changes from RECEIVED to FOLDED.

Kiran also records the **Chadat** as a separate event. She opens **Record Chadat**, selects the lot, and enters the value: 5.12 metres/kg (calculated by weighing a known length of fabric). This Chadat must be recorded before any non-Fresh thaan can be logged during future packing of this lot.

---

### 10:45 AM — Classification begins on the freshly folded lot

Workers inspect the folded material from Lot 7890 (FY26-MRL-0535). They assess the fabric visually and by feel, identifying the tone (colour shade) and finish (surface texture/hand). For this lot, the fabric appears uniformly Off-White with a standard finish.

A sample is cut and sent to head office for confirmation. **Kiran** notes this on the system — samples sent today.

Later in the morning, HO calls back: "Tone is O1W, Finish is 01 — confirmed."

**Kiran** opens **Record Classification** and enters:

- MRL: FY26-MRL-0535
- Tone Code: O1W
- Finish Code: 01
- Scope: LOT (the full lot has the same tone and finish)
- Metres Classified: 4,082.50
- HO Confirmed Date: today

She clicks Submit. The material state changes from FOLDED to CLASSIFIED at MIROLI-CLASSIFIED. This lot is now eligible for a packing program.

---

### 10:50 AM — Kiran marks defective material as Not Acceptable

While inspecting another freshly folded lot (FY26-MRL-0542, 1,800 metres), **Kiran** notices visible defects throughout the fabric — color bleeding and uneven dyeing. This material cannot be classified for normal use.

She opens **Record Classification** and selects:
- MRL: FY26-MRL-0542
- Classification Decision: "Mark Not Acceptable" (radio button)
- Rejection Reason: "Fabric has visible defects and color bleeding throughout - not suitable for packing"
- Metres Rejected: 1,800

She clicks Submit. The system updates:
- Material state → NOT_ACCEPTABLE at MIROLI-HOLD
- NA_ENTRY_CREATED event auto-triggers
- Entry NA-2026-0089 appears on the **Reprocess List**

The material will remain at MIROLI-HOLD until Ramesh contacts the vendor for pickup, decides to dispose of it, or (rarely) overrides the rejection and reclassifies it.

---

### 11:00 AM — Ramesh reviews Not Acceptable entry and reclassifies material

Between activities, Ramesh checks the **Reprocess List** and notices an entry from yesterday (FY26-MRL-0548, 180 metres) marked as Not Acceptable during classification with reason "fabric has minor color bleeding."

He walks to MIROLI-HOLD and physically inspects the material. After careful examination, he decides the quality is acceptable enough for certain lower-grade applications.

He opens **NA Entry Detail** on his phone and resolves the entry:
- Resolution Type: "Reclassified"
- Tone Code: O1W
- Finish Code: 02
- Notes: "Inspected material — bleeding is minor and isolated, acceptable for Reclassified use"

The system updates: Entry → RESOLVED, Material state → CLASSIFIED at MIROLI-CLASSIFIED. The 180 metres are now available for packing program allocation.

---

### 11:30 AM — Phase 1 continues, Phase 2 begins: first bale registered

Back at the packing area, **Deepa** and the team have logged enough Fresh thaans for the first bale from PP-2026-0087 — 15 thaans of 20 metres each. She switches to Phase 2.

She opens **Register Bale** on the tablet:

- Program: PP-2026-0087
- Line: Line 1 (SSTM / Officer / Rame)
- Selected Thaans: 15 Fresh thaans (104832, 104833, ... 104846)

She clicks Submit. The system auto-assigns bale number **37432**. The selected thaans change status from CREATED to BALED. A packing slip is generated — one copy will go inside the bale, the office copy is available for printing. The program shows progress: 1 of 5 bales complete. Status changes to IN_PROGRESS.

---

### 12:00 PM — Lunch break

Work pauses. The system state is frozen — everything recorded so far is persisted. When people return, they pick up exactly where they left off.

---

### 1:00 PM — Packing resumes: alternating Phase 1 and Phase 2

The team continues executing PP-2026-0087. **Deepa** alternates between logging thaans (Phase 1) and registering bales (Phase 2) as enough Fresh thaans accumulate for each bale:

- 1:30 PM: Bale 37433 registered (15 Fresh thaans). 2 of 5 complete.
- 2:15 PM: Bale 37434 registered. 3 of 5 complete.
- 3:00 PM: Bale 37435 registered. 4 of 5 complete.

Non-Fresh thaans logged during cutting (Good Cut ends, Fent offcuts, etc.) are assembled into separate non-Fresh bales. These bales sit at MIROLI-FG-OUT awaiting a future Todiya buyer. When a buyer is found, bales are unpacked and thaans repacked into new Todiya bales (Module 07).

---

### 3:30 PM — Classification wraps up, Gradation Report reviewed

**Kiran** checks the **Gradation Report** for FY26-MRL-0533 (the lot being packed today). The report has been updated progressively as Deepa logged thaans during packing:

| Grade | Metres | % |
|---|---|---|
| Fresh | 1,430.00 | 96.87% |
| Good Cut | 10.75 | 0.73% |
| Fent (1.2 kg = 6.14m via Chadat) | 6.14 | 0.42% |
| Rags (0.4 kg = 2.05m via Chadat) | 2.05 | 0.14% |
| Chindi (0.3 kg = 1.54m via Chadat) | 1.54 | 0.10% |
| **Total graded** | **1,450.48** | -- |
| Not Acceptable* | 0.00 | 0.00% |

*Not Acceptable is tracked separately — material rejected at classification (Module 04), not during packing. For this MRL, no material was marked NA at classification.

Note: This report is progressive. Not all of this MRL's material has been packed yet — only the portion allocated to PP-2026-0087. The remaining classified metres from this MRL will be graded when they are assigned to future packing programs. If worker encounters severely defective material during packing, they escalate to manager — quality rejection should happen at classification, not here.

---

### 3:45 PM — Ramesh contacts PSJC about the old rejection and schedules pickup

Ramesh calls PSJC about the 47-day-old Reprocess List entry (FY26-MRL-0526, 1,408 metres marked NA at classification). The vendor confirms they will send a truck next week to collect the rejected material.

He opens **NA Entry Detail** for the entry and adds a comment: "Called PSJC. They confirmed pickup next week — tentatively Thursday." The last_activity_at resets. The aging clock restarts.

One week later, when the vendor truck arrives and collects the material, Ramesh resolves the entry:
- Resolution Type: "Returned to Vendor"
- Notes: "Material picked up by PSJC truck on 2026-02-19"
- System updates: Entry → RESOLVED, Material state → RETURNED_TO_VENDOR, location → OUT (left facility)

---

### 4:00 PM — Last bale completed

**Deepa** logs the final batch of thaans and registers the 5th and final bale from PP-2026-0087:

- Bale 37436. 15 Fresh thaans. Total Metres = 300. Submit.

The program status changes to COMPLETED. All 5 bales are packed and at MIROLI-FG-OUT.

---

### 4:30 PM — Ramesh creates the Delivery Form (Step 1: Schedule Pickup)

Ramesh opens **Ready for Dispatch**. He sees packed bales grouped by customer:

- Customer Rame: 5 bales (37432-37436) — the ones just packed
- Customer S.P.: 6 bales — from an earlier program
- Customer VS: 12 bales
- Customer CB: 8 bales

He creates a Delivery Form for Rame. He selects the 5 bales, enters today's date, and clicks Submit. **DF-2026-0123** is generated with status PICKUP_SCHEDULED.

He prints the Delivery Form. The bale list, metres, pieces — all correct. He tells **Anil** and the loading team to prepare the 5 bales for the truck.

The 5 bales now show status = PICKUP_SCHEDULED. They are earmarked for this delivery but the truck has not yet departed.

---

### 4:45 PM — Truck departs (Step 2: Confirm Dispatch)

Anil and another worker load the 5 bales. The truck is ready to depart.

Ramesh opens **DF-2026-0123** on the **Scheduled Pickups** screen and clicks **Confirm Dispatch**. He enters the dispatch date (today). The delivery status changes from PICKUP_SCHEDULED to DISPATCHED. The 5 bales now show status = DISPATCHED.

The truck departs with the original Delivery Form. The office copy stays at Miroli. The **Stage-wise Inventory Dashboard** updates: packed bales awaiting dispatch drops from 31 to 26.

---

### 5:00 PM — Priyanka checks the day's results from head office

**Priyanka** opens the system. She sees:

- 5 new bales dispatched to Rame today (DF-2026-0123)
- 1 new MRL created (FY26-MRL-0548, 5,826 metres from Kalapurna)
- Gradation Report for FY26-MRL-0533 in progress: 96.53% Fresh yield so far
- Classification completed for FY26-MRL-0535: Tone O1W, Finish 01, 4,082.50 metres

She updates her daily summary for management. Everything is visible in real time — no waiting for paper.

---

### 5:30 PM — Shift ends

Ramesh does a final check of the dashboard:

- Received inventory: 17,826 metres (up from morning — new inbound receipt added)
- Classified (available for packing): 12,231 metres (up — newly classified lot added, minus what was packed today)
- Packed awaiting dispatch: 26 bales
- Scheduled pickups: 0 (the Rame delivery was confirmed)
- Active MRLs: 6 (including the new FY26-MRL-0548)

Tomorrow, the folding team will start on the 5,826 metres that arrived today (FY26-MRL-0548, Lot 7993). Ramesh will check if any more sales orders come in from head office.

The day is done. Every transaction is recorded. Every metre is accounted for.

---

## Part 3: Role Reference

Quick reference for each role's tasks, organized for onboarding and training.

### Facility Manager (Ramesh)

| Task | Screen | Frequency |
|---|---|---|
| Review stage-wise inventory | Stage-wise Dashboard | Daily (start of shift) |
| Check vendor-reported greige pending | Vendor Greige Pending | Daily |
| Review Decision Pending alerts (classification uncertainty) | Decision Pending list | Daily |
| Create packing program (select rolls from 1+ MRLs) | Create Packing Program | As needed (triggered by sales orders) |
| Create Todiya instruction (unpack + repack) | Create Todiya Instruction | Occasional (when buyer found for non-Fresh material) |
| Create delivery form (schedule pickup) | Create Delivery Form | Multiple times per week |
| Confirm dispatch (truck departs) | Scheduled Pickups / Delivery Form Detail | Multiple times per week |
| Review/comment on Reprocess List | Reprocess List, NA Entry Detail | Weekly |
| Resolve Decision Pending entries (classification) | Decision Pending Detail | As flagged |
| Cancel a packing program (rare) | Packing Program Detail | Rare |

### Supervisor (Kiran)

| Task | Screen | Frequency |
|---|---|---|
| Record inbound receipt (creates MRL on first receipt) | Record Inbound Receipt | Per truck arrival (multiple/week) |
| Record per-roll folding measurements | Record Folding | Per lot being folded (continuous) |
| Record Chadat (metres-to-kg conversion factor) | Record Chadat | Per lot (separate event, before non-Fresh thaan logging) |
| Record tone and finish classification | Record Classification | Per lot or per roll after folding |
| Log thaans during packing (cut + fold + grade) | Log Thaan | Continuous throughout packing |
| Register bales (assemble Fresh thaans) | Register Bale | Per bale completed (multiple/day) |
| Create Decision Pending entry (classification uncertainty) | Decision Pending | When tone/finish classification is unclear |
| Resolve Decision Pending | Decision Pending Detail | When decision is made |

### Receiving Worker (Anil)

| Task | Screen | Frequency |
|---|---|---|
| Assist with truck unloading | (physical — no screen) | Per truck arrival |
| Assist with bale loading for dispatch | (physical — no screen) | Per dispatch |

Note: Packaging material GRN tracking is deferred in the current system scope. Anil's role in the system is currently limited to physical operations.

### Packing Worker (Deepa)

| Task | Screen | Frequency |
|---|---|---|
| View packing program specs | Packing Program Detail | Start of each program |
| Log thaans (Phase 1 — cut roll, fold, assign grade) | Log Thaan | Per thaan produced (many per day) |
| Register bales (Phase 2 — assemble Fresh thaans into bale) | Register Bale | Per bale completed |
| Print packing slip | Bale Detail | Per bale |

### Head Office User (Priyanka)

| Task | Screen | Frequency |
|---|---|---|
| Review factory dashboard | Stage-wise Dashboard | Daily |
| Check dispatch volume | Delivery Forms, Dispatch Dashboard | Daily/weekly |
| Review Gradation Reports | Gradation Reports list | Per lot (progressive updates) |
| Check vendor-reported greige pending | Vendor Greige Pending | Weekly |
| Answer management queries | Various lists with filters | Ad hoc |

---

## Part 4: Edge Cases and Error Scenarios

### Partial shipment from vendor
- **7:00 AM:** Kiran records an inbound receipt for 4,000 of the expected 6,000 metres. This is the first receipt, so it creates a new MRL (Path A). The MRL status is ACTIVE. The Gate Pass note says 2,000 greige metres are still pending at the vendor.
- **9:00 AM:** Ramesh sees the MRL on the **Vendor Greige Pending** dashboard — 2,000 metres of vendor-reported greige outstanding. He calls the vendor.
- **Three days later:** The remaining material arrives. Kiran records another inbound receipt against the existing MRL (Path B — "Existing MRL"). The MRL stays ACTIVE (same status — more material could theoretically still arrive). The vendor-reported greige pending on the Gate Pass now shows 0.
- **Eventually:** Ramesh closes the MRL manually when he is satisfied no more material is expected.

### Decision Pending lot forgotten (classification uncertainty)
- **Day 1:** Kiran records a Decision Pending entry for 100 metres — subtle tone variation between rolls, unclear whether they should be classified as O1W or O2W.
- **Day 14:** No comments or resolution. The system flags the entry with a red warning: "No activity for 14 days."
- **Day 15:** Ramesh sees the alert on the **Decision Pending** screen during his morning review. He inspects the physical material, determines the tone is acceptable as O1W, and resolves the entry with Tone = O1W and Finish = 01. The 100 metres move to CLASSIFIED and become available for packing programs.

### Packing program cancelled
- **10:00 AM:** Ramesh creates PP-2026-0088 for customer CB — 3 bales of Sportsman. Source rolls are allocated and move to PROGRAM_ASSIGNED.
- **10:15 AM:** Head office calls — CB cancelled the order.
- **10:20 AM:** No thaans have been logged yet. Ramesh opens the program, clicks Cancel, enters reason: "Customer cancelled order." The allocated source rolls return from PROGRAM_ASSIGNED to their previous state (CLASSIFIED). The rolls are available for a different program.

### Not Acceptable material never picked up
- **Month 1:** FY26-MRL-0526 entry created on Reprocess List. 1,408 metres rejected at PSJC.
- **Month 2:** Ramesh adds comments documenting three phone calls. PSJC keeps promising pickup.
- **Month 6:** Ramesh decides they will never pick up. He resolves the entry as "Unresolved — vendor non-responsive after 6 months." The material remains at MIROLI-NA. It is no longer on the active Reprocess List but exists in the resolution history.

### Packaging material runs out mid-program
- **2:00 PM:** During bale registration, the team reaches for plastic sheets — none left. Phase 2 (bale assembly) pauses, but Phase 1 (thaan logging) can continue since thaan logging does not consume packaging materials.
- **2:05 PM:** Ramesh checks with the packaging vendor — confirms supplies are low. He calls the vendor for an emergency delivery.
- **3:00 PM:** Vendor delivers emergency stock. Stock replenishes. Bale registration resumes.
- Note: Packaging material tracking (GRN, stock levels, backflush) is deferred in the current system scope. This scenario describes the physical reality but the system tracking is not yet implemented.

### Cross-lot packing program
- **9:30 AM:** Ramesh needs to create a program for 8 bales, but no single MRL has enough classified material. FY26-MRL-0533 has 3,200 metres and FY26-MRL-0530 has 1,800 metres — together they cover the 4,800 metres needed.
- He opens **Create Packing Program** and selects source rolls from both MRLs. The system allows cross-lot selection as long as the quality code, tone, and finish match across the selected rolls.
- During Phase 1, Deepa logs thaans against specific source rolls — each thaan is traced to its source roll and therefore its source MRL. The Gradation Report updates for each MRL independently.

### Todiya sale opportunity (unpack and repack)
- **Morning:** A buyer calls asking for 40 metres of Good Cut fabric.
- Ramesh opens **Todiya Candidates** — a list of bales containing non-Fresh thaans. He sees 3 bales with Good Cut thaans totaling 53.25 metres.
- He creates a **Todiya Instruction**: selects the 3 source bales, enters buyer = Todiya Buyer X, brand = SSTM, product = KT-555.
- **Execution — Unpack:** Workers physically open the 3 source bales. Kiran opens **Unpack Bale** for each source bale and clicks Unpack. The bales move to UNPACKED status. Their thaans are released (status = UNPACKED) and available for repacking.
- **Execution — Repack:** From the pool of unpacked thaans, workers select the Good Cut thaans that add up to approximately 40 metres. Kiran opens **Register Todiya Bale**, selects the thaans, and clicks Submit. A new Todiya bale is created with a new bale number, packing slip, and the buyer's branding. The selected thaans move from UNPACKED to BALED (in the new bale).
- Any leftover unpacked thaans (e.g., Fent or Rags thaans from the same source bales) remain in the unpacked pool for a future Todiya instruction.
- The new Todiya bale is dispatch-ready — Ramesh creates a Delivery Form and dispatches it via the normal two-step process.
- No re-cutting or re-folding occurs. Thaans pass through unchanged — same metres, same source roll, same grade. Only the bale assignment changes.
