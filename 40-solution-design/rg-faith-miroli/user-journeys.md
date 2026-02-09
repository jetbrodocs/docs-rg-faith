# User Journeys — RG Faith Miroli Inventory System

This document describes how real users experience the system day-to-day. It is structured in three parts:

1. **Roles** — who uses the system and what they are responsible for
2. **A Day at Miroli** — a full timeline narrative following all roles through a typical day, showing how actions flow between people
3. **Role Reference** — per-role task breakdowns for quick reference

---

## Part 1: Roles

| Role | Person | Location | Responsibility | Primary Screens |
|---|---|---|---|---|
| **Facility Manager** | Ramesh | Miroli floor | Decision-maker. Creates MRLs, packing programs, delivery forms. Reviews dashboards. Handles vendor issues. | Dashboards, MRL Register, Create Packing Program, Ready for Dispatch, Reprocess List |
| **Supervisor** | Kiran | Miroli floor (folding/grading/packing areas) | Operational lead. Records inbound receipts, folding data, grading entries. Registers bales. Manages Decision Pending entries. | Record Inbound, Record Folding, Record Grading, Register Bale, Decision Pending |
| **Receiving Worker** | Anil | Miroli receiving area | Unloads trucks. Records packaging material GRNs. | Record Packaging GRN, Packaging Stock |
| **Packing Worker** | Deepa | Miroli packing area | Executes packing programs — cuts, folds, stamps, packs. Registers completed bales. | Packing Program Detail, Register Bale |
| **Head Office User** | Priyanka | Ahmedabad head office (New Cloth Market) | Remote monitoring. Reviews dashboards and reports. Answers management queries. | Stage-wise Dashboard, Gradation Reports, Dispatch history |

All factory roles use a shared tablet or phone on the floor. Workers are multi-skilled — the same person may fold, grade, and pack depending on the day. The system roles above represent the *typical* primary responsibility, not rigid assignments.

---

## Part 2: A Day at Miroli

A single day at the facility, told chronologically. Every action by every role, in the order it happens. This is one continuous narrative — follow it from morning to evening to understand how the system knits together.

---

### 6:30 AM — Shift starts, Ramesh checks the state of the world

Ramesh arrives at Miroli and opens the system on the shared tablet near the office area. He navigates to the **Stage-wise Inventory Dashboard**. The numbers refresh from last night's closing state:

- Grey inventory: 12,400 metres across 4 MRLs awaiting processing
- Folded (pending grading): 3,200 metres
- Fresh (available for packing): 8,750 metres across 3 lots
- Packing programs in progress: 2 programs, 14 bales completed of 22 planned
- Packed bales awaiting dispatch: 31 bales for 4 customers
- Accumulated stock (Todiya): 18.5 kg Good Cut, 7.2 kg Fent

He switches to **Vendor Pending Balances**. MRL-0542 shows 2,800 metres outstanding at Kalapurna Mills — it has been 9 days since dispatch. He makes a mental note to call them after breakfast.

He checks the **Decision Pending** screen. One entry has a red flag: "No activity for 16 days" — 100 metres from MRL-0531 with a remark about colour variation. He will need to look at the physical material later.

He checks the **Reprocess List**. Three open entries. One is 47 days old with no comments — MRL-0526 at PSJC, 1,408 metres of rejected fabric.

---

### 7:00 AM — Truck arrives from Kalapurna Mills

RG Faith's truck returns from Kalapurna Mills with dyed cloth. **Anil** is at the gate. He helps the driver unload 6 rolls of fabric from the truck and stacks them in the grey storage area. The driver hands over the Gate Pass — a printed form from Kalapurna listing roll-by-roll metres, lot number 7993, quality code 44x45P6, 5,826.00 total metres.

**Kiran** arrives at the receiving area with the tablet. She opens **Record Inbound Receipt** and selects MRL-0538 from the dropdown (this was the outbound record Ramesh created when the cloth was sent to Kalapurna 12 days ago). She enters the Gate Pass data:

- Avak Date: today
- Lot Number: 7993
- Grey Metres: 5,826.00
- Quality Code: 44x45P6
- GSM: 120
- Width: 58"
- Rolls: 6
- Gate Pass Reference: KM-2026-4421

She clicks Submit. Receipt IR-2026-0042 is created. MRL-0538 status changes to FULLY_RECEIVED — all 5,826 metres accounted for. The grey inventory at MIROLI-GREY increases by 5,826 metres.

Kiran files the physical Gate Pass in the paper folder (old habit, still useful as backup). The digital record is now the source of truth.

---

### 7:15 AM — Packaging vendor delivers supplies

While the fabric truck is being unloaded, a packaging vendor's auto-rickshaw pulls up with boxes of cardboard and plastic sheets. **Anil** takes delivery. He opens **Record Packaging GRN** on the shared tablet and enters two receipts:

- SKU = Cardboard Box (large), Vendor = ABC Packaging, Quantity = 200 units, Reference = INV-4412. Submit.
- SKU = Plastic Sheet (standard), Vendor = ABC Packaging, Quantity = 500 sheets, Reference = INV-4412. Submit.

He checks **Packaging Stock** — cardboard boxes went from 45 to 245. Plastic sheets from 120 to 620. Enough for the day's packing work.

---

### 7:30 AM — Folding team starts on yesterday's grey lot

The folding workers pick up a lot that arrived yesterday — MRL-0535, Lot 7890, 4,200 grey metres. They begin unfolding the rolls, cutting them into standard 100-metre sections, and measuring each one. This is physical, continuous work that takes most of the morning.

Meanwhile, **Kiran** opens **Pending Folding** on her tablet. She sees the lot the team is working on, plus the lot that just arrived (MRL-0538, 5,826 metres) — that one will be next.

---

### 8:30 AM — Ramesh creates an MRL for outbound

Woven cloth has arrived from the weaving facility (separate location, out of scope). Ramesh needs to send 8,200 metres to RSK Industries for dyeing. He opens **Create MRL**:

- Vendor: RSK Industries
- Metres Sent: 8,200
- Quality Code: 44x45P6
- Date Sent: today

He clicks Submit. MRL-0548 is created — 8,200 metres at status SENT_TO_VENDOR. He tells the transport team to load the cloth and deliver it to RSK today.

---

### 9:00 AM — Head office checks in

At the Ahmedabad head office, **Priyanka** opens the **Stage-wise Inventory Dashboard**. She sees the same real-time data as Ramesh — including the 5,826 metres that Kiran just received 2 hours ago. No waiting for paper.

She checks **Total dispatch volume this month** — 847 bales, 86,420 metres across 23 delivery forms. She opens **Vendor Pending Balances** — 42,600 metres outstanding across 8 vendors. She makes a note for the weekly management report.

Management asks her: "How much did we ship to customer S.P. this month?" She opens **Delivery Forms**, filters by customer = S.P. and date range = this month. The answer is immediate: 12 delivery forms, 74 bales, 7,820 metres.

---

### 9:30 AM — Head office calls with a sales order

Ramesh receives a phone call from head office. Customer Rame needs 5 bales of Officer brand — 20m cut, Book fold, SSTM stamp, trade number S8072-58".

He opens **Fresh Material Available**. He sees:
- MRL-0538, Lot 7993: 5,644 metres of Fresh at MIROLI-FRESH (this lot was graded yesterday, the receipt Kiran just recorded was for a different shipment against the same MRL — but in this case it's a lot graded earlier that is sitting as Fresh)
- MRL-0533, Lot 7801: 2,100 metres
- MRL-0530, Lot 7756: 1,006 metres

He chooses MRL-0538. He clicks **Create Program from this lot** and fills in the **Create Packing Program** form:

- Line 1: Brand = SSTM, Product = Officer, Trade Number = S8072-58", Fold Type = Book, Customer = Rame, Cut Length = 20m, Pieces/Bale = 15, Planned Bales = 5

The system calculates: 20m × 15 pieces × 5 bales = 1,500 metres allocated.

Ramesh reviews and clicks Submit. Program PP-2026-0087 is created. 1,500 metres move from GRADED_FRESH to PROGRAM_ASSIGNED at MIROLI-PACK.

He walks to the packing area and tells the team: "PP-2026-0087, five bales, Officer for Rame."

---

### 10:00 AM — Packing team starts execution

**Deepa** opens **Packing Program Detail** for PP-2026-0087 on the tablet mounted near the cutting table. She sees the specifications clearly:

- SSTM / Officer / S8072-58" / Book fold / 20m cut / 15 pieces per bale / 5 bales planned

She and two other workers begin cutting the fabric into 20-metre pieces. Each piece is folded in Book style. They apply the SSTM stamp, add product stickers, layer each piece with plastic, place 15 pieces into a cardboard box, and wrap the box with thread. The bale label is attached externally.

---

### 10:30 AM — Folding complete, Kiran records the data

The folding team finishes processing MRL-0535, Lot 7890. **Kiran** opens **Record Folding**:

- Inbound Receipt: MRL-0535 / Lot 7890
- Folding Metres: 4,082.50
- Chadat: 5.12 (100m fold weighed 19.53 kg → 100/19.53 = 5.12)
- Fold Count: 40 (40 × 100m folds)
- Remainder: 82.50 metres

She clicks Submit. The system calculates shrinkage: 4,200 - 4,082.50 = 117.50 metres (2.80%). The lot moves from GREY to FOLDED.

---

### 10:45 AM — Grading begins on the freshly folded lot

The same workers (multi-skilled) now start inspecting the folded sections from Lot 7890. As they work through each fold, **Kiran** records grading entries in real time on the **Record Grading** screen:

- Fold 1: Grade = FRESH, Metres = 100. Submit.
- Fold 2: Grade = FRESH, Metres = 100. Submit.
- Fold 3: Worker spots a stain at the 65-metre mark. Kiran records two entries:
  - Grade = FRESH, Metres = 65. Submit.
  - Grade = NOT_ACCEPTABLE, Metres = 5 (the stained section, cut out). Submit.
  - The remaining 30 metres continue as the next section.
- Fold 4: Some minor defects — 2.1 kg of fabric set aside. Grade = GOOD_CUT, Kilograms = 2.1. Chadat auto-fills as 5.12. Equivalent metres = 2.1 × 5.12 = 10.75m. Submit.

She continues through the morning. The **Gradation Report** for MRL-0535 updates incrementally with each entry — Fresh percentage starts at 100% and settles around 96.5% as non-Fresh sections are recorded.

The 5 metres of Not Acceptable fabric automatically creates an entry on the **Reprocess List**: NA-2026-0034, MRL-0535, 5 metres, remark "stain at fold 3, approx 65m mark."

The Good Cut goes to the accumulation area. The **Accumulation Dashboard** updates: Good Cut increases from 18.5 kg to 20.6 kg.

---

### 11:00 AM — Ramesh handles the stale Decision Pending entry

Between activities, Ramesh walks to the storage area and physically examines the 100 metres from MRL-0531 that has been sitting as Decision Pending for 16 days. He looks at the colour variation. It is subtle but acceptable.

He opens **Decision Pending Detail** on his phone and resolves the entry: Resolved Grade = FRESH. The 100 metres immediately move to GRADED_FRESH and appear in the **Fresh Material Available** screen.

---

### 11:30 AM — First bale completed

**Deepa** and the team finish the first bale from PP-2026-0087. She opens **Register Bale** on the tablet:

- Program: PP-2026-0087
- Line: Line 1 (SSTM / Officer / Rame)
- Pieces: 15
- Total Metres: 300

She clicks Submit. The system auto-assigns bale number **37432**. A packing slip is generated — one copy will go inside the bale, the office copy is available for printing. The program shows progress: 1 of 5 bales complete. Status changes to IN_PROGRESS.

---

### 12:00 PM — Lunch break

Work pauses. The system state is frozen — everything recorded so far is persisted. When people return, they pick up exactly where they left off.

---

### 1:00 PM — Packing resumes

The team continues executing PP-2026-0087. **Deepa** registers bales as they are completed:

- 1:30 PM: Bale 37433 registered. 2 of 5 complete.
- 2:15 PM: Bale 37434 registered. 3 of 5 complete.
- 3:00 PM: Bale 37435 registered. 4 of 5 complete.

---

### 3:30 PM — Grading wraps up for the day

**Kiran** finishes recording the last grading entries for MRL-0535, Lot 7890. She opens the **Gradation Report** and sees the final breakdown:

| Grade | Metres | % |
|---|---|---|
| Fresh | 3,938.50 | 96.47% |
| Good Cut (10.75m) | 10.75 | 0.26% |
| Fent (6.2 kg = 31.74m) | 31.74 | 0.78% |
| Rags (1.1 kg = 5.63m) | 5.63 | 0.14% |
| Chindi (0.8 kg = 4.10m) | 4.10 | 0.10% |
| Not Acceptable | 5.00 | 0.12% |
| **Total** | **3,995.72** | — |
| Unaccounted (shrinkage beyond folding) | 86.78 | 2.13% |

The lot is fully graded. 3,938.50 metres of Fresh are now available at MIROLI-FRESH for the next packing program.

---

### 3:45 PM — Ramesh contacts PSJC about the old rejection

Ramesh calls PSJC about the 47-day-old Reprocess List entry (MRL-0526, 1,408 metres). They say they will send a truck next week to pick it up.

He opens **NA Entry Detail** for the entry and adds a comment: "Called PSJC. They confirmed pickup next week — tentatively Thursday." The last_activity_at resets. The aging clock restarts.

---

### 4:00 PM — Last bale completed, waste recorded

**Deepa** registers the 5th and final bale from PP-2026-0087:

- Bale 37436. Pieces = 15. Total Metres = 300. Submit.

The program status changes to COMPLETED. All 5 bales are packed and at MIROLI-FG-OUT.

**Kiran** weighs the cutting waste: 1.8 kg Good Cut, 0.5 kg Fent. She opens **Record Cutting Waste** for PP-2026-0087 and enters the numbers. Submit. The accumulation stock updates: Good Cut now at 22.4 kg, Fent at 7.7 kg.

---

### 4:30 PM — Ramesh creates the Delivery Form

Ramesh opens **Ready for Dispatch**. He sees:

- Customer Rame: 5 bales (37432-37436) — the ones just packed
- Customer S.P.: 6 bales — from an earlier program
- Customer VS: 12 bales
- Customer CB: 8 bales

He creates a Delivery Form for Rame. He selects the 5 bales, enters today's date, and clicks Submit. **DF-2026-0123** is generated.

He prints the Delivery Form. The bale list, metres, pieces — all correct. He tells **Anil** and the loading team to load the 5 bales onto the truck.

---

### 4:45 PM — Truck departs

Anil and another worker load the 5 bales. The truck departs with the original Delivery Form. The office copy stays at Miroli.

The 5 bales now show status = DISPATCHED. The **Stage-wise Inventory Dashboard** updates: packed bales awaiting dispatch drops from 31 to 26.

---

### 5:00 PM — Priyanka checks the day's results from head office

**Priyanka** opens the system. She sees:

- 5 new bales dispatched to Rame today (DF-2026-0123)
- 1 new MRL created (MRL-0548 to RSK, 8,200 metres)
- 1 inbound receipt (IR-2026-0042, MRL-0538, 5,826 metres from Kalapurna)
- Gradation Report for MRL-0535 completed: 96.47% Fresh yield

She updates her daily summary for management. Everything is visible in real time — no waiting for paper.

---

### 5:30 PM — Shift ends

Ramesh does a final check of the dashboard:

- Grey inventory: 17,826 metres (up from morning — new inbound receipt, minus the lot that was folded/graded)
- Fresh available: 11,188.50 metres (up — new graded lot added, minus what was packed today)
- Packed awaiting dispatch: 26 bales
- MRLs pending at vendors: 6 (including the new MRL-0548)
- Accumulation: Good Cut 22.4 kg, Fent 7.7 kg

Tomorrow, the folding team will start on the 5,826 metres that arrived today (MRL-0538, Lot 7993). Ramesh will check if any more sales orders come in from head office.

The day is done. Every transaction is recorded. Every metre is accounted for.

---

## Part 3: Role Reference

Quick reference for each role's tasks, organized for onboarding and training.

### Facility Manager (Ramesh)

| Task | Screen | Frequency |
|---|---|---|
| Review stage-wise inventory | Stage-wise Dashboard | Daily (start of shift) |
| Check vendor pending balances | Vendor Pending Balances | Daily |
| Review Decision Pending alerts | Decision Pending list | Daily |
| Create MRL (outbound to vendor) | Create MRL | As needed (several per week) |
| Create packing program | Create Packing Program | As needed (triggered by sales orders) |
| Create Todiya program | Create Todiya Program | Occasional (when buyer found for leftovers) |
| Create delivery form (dispatch) | Create Delivery Form | Multiple times per week |
| Review/comment on Reprocess List | Reprocess List, NA Entry Detail | Weekly |
| Resolve Decision Pending entries | Decision Pending Detail | As flagged |
| Cancel a packing program (rare) | Packing Program Detail | Rare |

### Supervisor (Kiran)

| Task | Screen | Frequency |
|---|---|---|
| Record inbound receipt | Record Inbound Receipt | Per truck arrival (multiple/week) |
| Record folding completion | Record Folding | Per lot folded (daily) |
| Record grading entries | Record Grading | Continuous throughout day |
| Check Gradation Report progress | Gradation Report | Per lot being graded |
| Register bales | Register Bale | Per bale completed (multiple/day) |
| Record cutting waste | Record Cutting Waste | Per program completed |
| Create Decision Pending entry | Decision Pending | When quality is unclear |
| Resolve Decision Pending | Decision Pending Detail | When decision is made |
| Record packaging consumption | Record Consumption | End of day or per program |

### Receiving Worker (Anil)

| Task | Screen | Frequency |
|---|---|---|
| Record packaging GRN | Record Packaging GRN | Per vendor delivery |
| Check packaging stock levels | Packaging Stock | As needed |
| Assist with truck unloading | (physical — no screen) | Per truck arrival |
| Assist with bale loading | (physical — no screen) | Per dispatch |

### Packing Worker (Deepa)

| Task | Screen | Frequency |
|---|---|---|
| View packing program specs | Packing Program Detail | Start of each program |
| Register completed bale | Register Bale | Per bale completed |
| Print packing slip | Bale Detail | Per bale |

### Head Office User (Priyanka)

| Task | Screen | Frequency |
|---|---|---|
| Review factory dashboard | Stage-wise Dashboard | Daily |
| Check dispatch volume | Delivery Forms, Dispatch Dashboard | Daily/weekly |
| Review Gradation Reports | Gradation Reports list | Per completed lot |
| Check vendor pending balances | Vendor Pending Balances | Weekly |
| Answer management queries | Various lists with filters | Ad hoc |

---

## Part 4: Edge Cases and Error Scenarios

### Partial shipment from vendor
- **7:00 AM:** Kiran records inbound receipt for 4,000 of 6,000 metres against MRL-0540. MRL status changes to PARTIALLY_RECEIVED with 2,000 metres pending.
- **9:00 AM:** Ramesh sees MRL-0540 on the **Vendor Pending Balances** dashboard — 2,000 metres outstanding. He calls the vendor.
- **Three days later:** The remaining 2,000 metres arrive. Kiran records another receipt. MRL status changes to FULLY_RECEIVED.

### Decision Pending lot forgotten
- **Day 1:** Kiran records a Decision Pending entry for 100 metres — subtle colour variation.
- **Day 14:** No comments or resolution. The system flags the entry with a red warning: "No activity for 14 days."
- **Day 15:** Ramesh sees the alert on the **Decision Pending** screen during his morning review. He inspects the physical material, decides it is acceptable, and resolves it as FRESH. The 100 metres become available.

### Packing program cancelled
- **10:00 AM:** Ramesh creates PP-2026-0088 for customer CB — 3 bales of Sportsman.
- **10:15 AM:** Head office calls — CB cancelled the order.
- **10:20 AM:** No bales have been produced yet. Ramesh opens the program, clicks Cancel, enters reason: "Customer cancelled order." The allocated Fresh material returns to GRADED_FRESH and is available for a different program.

### Not Acceptable material never picked up
- **Month 1:** MRL-0526 entry created on Reprocess List. 1,408 metres rejected at PSJC.
- **Month 2:** Ramesh adds comments documenting three phone calls. PSJC keeps promising pickup.
- **Month 6:** Ramesh decides they will never pick up. He resolves the entry as "Unresolved — vendor non-responsive after 6 months." The material remains at MIROLI-NA. It is no longer on the active Reprocess List but exists in the resolution history.

### Packaging material runs out mid-program
- **2:00 PM:** During packing, the team reaches for plastic sheets — none left. Work pauses.
- **2:05 PM:** Ramesh checks **Packaging Stock** — confirms 0 plastic sheets. He calls the packaging vendor.
- **3:00 PM:** Vendor delivers emergency stock. **Anil** records the GRN: 200 plastic sheets. Stock replenishes. Packing resumes.

### Todiya sale opportunity
- **Morning:** A buyer calls asking for 15 kg of Good Cut fabric.
- Ramesh checks the **Accumulation Dashboard** — 22.4 kg Good Cut available.
- He creates a Todiya program: source = GOOD_CUT, 15 kg, customer = Todiya Buyer X, brand = SSTM, product = KT-555.
- The packing team executes it using the same workflow as regular packing. Bales are registered, waste recorded, delivery form created.
- Accumulation stock drops from 22.4 kg to 7.4 kg Good Cut.
