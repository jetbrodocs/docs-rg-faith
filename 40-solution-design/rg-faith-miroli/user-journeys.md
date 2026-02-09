# User Journeys — RG Faith Miroli Inventory System

This document describes how real users experience the system day-to-day. Each role gets a narrative walkthrough of their typical tasks, what they see, and what success looks like.

---

## Facility Manager (Ramesh)

### Who they are
Ramesh is the facility manager at Miroli. He oversees all operations — from deciding which cloth goes to which vendor for dyeing, to creating packing programs, to approving dispatches. He is the primary decision-maker on the factory floor.

### Their typical workflow

**Morning: Check the dashboard**

1. Ramesh opens the system on his phone or a shared tablet at the start of his shift.
2. He navigates to the **Stage-wise Inventory Dashboard**. He sees:
   - Grey inventory: 12,400 metres across 4 MRLs awaiting processing
   - Folded (pending grading): 3,200 metres
   - Fresh (available for packing): 8,750 metres across 3 lots
   - Packing programs in progress: 2 programs, 14 bales completed of 22 planned
   - Packed bales awaiting dispatch: 31 bales
   - Accumulated stock (Todiya): 18.5 kg Good Cut, 7.2 kg Fent
3. He checks the **Vendor Pending Balances** screen — sees MRL-0542 has 2,800 metres outstanding at Kalapurna Mills. He makes a mental note to call and check on this.

**Mid-morning: Create a packing program**

1. Ramesh receives word from head office (phone call) that customer Rame needs 5 bales of Officer brand, 20m cut, Book fold.
2. He opens **Fresh Material Available** and sees MRL-0538, Lot 7993 has 5,644 metres of Fresh at MIROLI-FRESH.
3. He clicks **Create Program from this lot** and fills in:
   - Line 1: Brand = SSTM, Product = Officer, Trade Number = S8072-58", Fold Type = Book, Customer = Rame, Cut Length = 20m, Pieces/Bale = 15, Planned Bales = 5
4. The system calculates: 20m × 15 pieces × 5 bales = 1,500 metres allocated.
5. Ramesh reviews and clicks Submit. Program PP-2026-0087 is created. The 1,500 metres move from GRADED_FRESH to PROGRAM_ASSIGNED.
6. He tells the cutting team to start on PP-2026-0087.

**Afternoon: Create an MRL for outbound**

1. Woven cloth has arrived at Miroli from the weaving facility. Ramesh needs to send it to RSK Industries for dyeing.
2. He opens **Create MRL**, selects Vendor = RSK Industries, enters Metres Sent = 8,200, Quality Code = 44x45P6, Date Sent = today.
3. MRL-0548 is created. The system shows 8,200 metres at status SENT_TO_VENDOR.

**Late afternoon: Review Reprocess List**

1. Ramesh opens the **Reprocess List** screen. He sees 3 open entries, one of which has been open for 47 days with no activity.
2. He opens the stale entry (MRL-0526 at PSJC, 1,408 metres rejected). He adds a comment: "Called PSJC — they said pickup next week."
3. The aging clock resets.

**End of day: Check dispatch readiness**

1. Ramesh opens **Ready for Dispatch**. He sees 31 packed bales grouped by customer.
2. Customer Rame has 5 bales ready (the ones just packed from PP-2026-0087). Customer S.P. has 6 bales ready.
3. He creates a Delivery Form for Rame: selects the 5 bales, enters today's date, clicks Submit. DF-2026-0123 is generated.
4. He tells the loading team to prepare the truck.

### What success looks like
At the end of each day, Ramesh can see exactly where every metre of material is — how much is at vendors, how much is Grey, how much is being processed, how much is ready to ship. He creates packing programs confidently because he knows the Fresh inventory in real time. Dispatch is documented digitally. The head office can query the system instead of waiting for paper to arrive by courier.

---

## Supervisor (Kiran)

### Who they are
Kiran is a shift supervisor at Miroli. She oversees the folding/grading area and the packing area. She records inbound receipts, folding data, grading entries, and registers bales.

### Their typical workflow

**Morning: Process inbound receipts**

1. RG Faith's truck returns from Kalapurna Mills with dyed cloth and a Gate Pass.
2. Kiran opens **Record Inbound Receipt** on her tablet. She selects MRL-0538 from the dropdown.
3. She enters the Gate Pass data:
   - Avak Date: today
   - Lot Number: 7993
   - Grey Metres: 5,826.00 (from Gate Pass)
   - Quality Code: 44x45P6
   - GSM: 120
   - Width: 58"
   - Rolls: 6
   - Gate Pass Reference: KM-2026-4421
4. She clicks Submit. IR-2026-0042 is created. MRL-0538 status changes to FULLY_RECEIVED (all metres accounted for). 5,826 metres appear as Grey inventory at MIROLI-GREY.

**Mid-morning: Record folding**

1. The folding team has finished processing Lot 7993. Kiran opens **Record Folding**.
2. She selects the lot and enters:
   - Folding Metres: 5,644.33
   - Chadat: 4.86 (100m fold weighed 20.6 kg → 100/20.6 = 4.86)
   - Fold Count: 56 (56 × 100m folds)
   - Remainder: 44.33 metres
3. She clicks Submit. The system calculates shrinkage: 5,826 - 5,644.33 = 181.67 metres (3.12%). The lot state changes to FOLDED.

**Throughout the day: Record grading entries**

1. As workers inspect folded sections, Kiran records each grading decision on the **Record Grading** screen.
2. For a 100m fold that passes inspection: Grade = FRESH, Metres = 100. Submit.
3. For a section with minor defects cut out (2.3 kg): Grade = GOOD_CUT, Kilograms = 2.3. Chadat auto-fills as 4.86. System calculates equivalent metres = 2.3 × 4.86 = 11.18m. Submit.
4. She repeats this throughout the day. Each entry incrementally updates the Gradation Report.
5. She checks the **Gradation Report** screen for MRL-0538 and sees the progressive breakdown — 96.91% Fresh so far, 0.92% Good Cut.

**Afternoon: Register bales**

1. The cutting/packing team is working on PP-2026-0087 (the 5 Officer bales for Rame).
2. As each bale is completed, Kiran opens **Register Bale**, selects the program line, enters: Pieces = 15, Total Metres = 300. Clicks Submit.
3. The system auto-assigns bale number 37432. A packing slip is generated.
4. She repeats for each bale. After the 5th bale, the program status changes to COMPLETED.

**Exception: Decision Pending**

1. A worker finds a section where quality is unclear — possible colour inconsistency but subtle.
2. Kiran opens **Record Decision Pending**, enters: Metres = 100, Remark = "Slight colour variation in middle section — unclear if customer would accept."
3. She clicks Submit. The 100 metres move to DECISION_PENDING state. The 14-day clock starts.
4. Two days later, she revisits the entry and adds a comment: "Showed to Ramesh — he says grade as Fresh." She resolves it: Resolved Grade = FRESH. The 100 metres move to GRADED_FRESH.

### What success looks like
Every fold is measured, every grade is recorded, every bale is registered — digitally, as it happens. No paper registers to transcribe later. The Gradation Report builds itself in real time as Kiran enters data. The head office can see yield percentages without waiting for paper.

---

## Receiving Worker (Anil)

### Who they are
Anil works at the receiving area. He unloads trucks, helps with packaging material receipts, and handles basic data entry.

### Their typical workflow

**Packaging material receipt**

1. A packaging vendor delivers a batch of cardboard boxes and plastic sheets.
2. Anil opens **Record Packaging GRN** on the shared tablet.
3. He enters two GRNs:
   - SKU = Cardboard Box (large), Vendor = ABC Packaging, Quantity = 200, Reference = INV-4412
   - SKU = Plastic Sheet (standard), Vendor = ABC Packaging, Quantity = 500, Reference = INV-4412
4. Stock levels update immediately. He can see on the **Packaging Stock** screen that cardboard boxes went from 45 to 245.

**Assist with truck unloading**

1. When a truck returns from a mill, Anil helps unload rolls and store them in the grey storage area. The supervisor (Kiran) handles the digital receipt recording.

### What success looks like
Packaging stock is always up to date. When the packing team starts a program, they know how many boxes and sheets are available. No surprises from running out mid-program.

---

## Packing Worker (Deepa)

### Who they are
Deepa works on the packing line. She cuts, folds, stamps, and packs fabric into bales. She also registers completed bales in the system.

### Their typical workflow

**Executing a packing program**

1. Ramesh tells the packing team to work on PP-2026-0087 (5 bales of Officer for Rame, 20m cut, Book fold).
2. Deepa opens **Packing Program Detail** for PP-2026-0087 and sees the specifications:
   - Line 1: SSTM / Officer / S8072-58" / Book fold / 20m cut / 15 pieces per bale / 5 bales
3. She and the team cut the fabric into 20m pieces, fold each piece in Book style, apply the SSTM stamp, add stickers, layer with plastic, place 15 pieces in a cardboard box, and wrap with thread.
4. After each bale is complete, Deepa opens **Register Bale**, selects Line 1, enters Pieces = 15, Total Metres = 300. The system assigns bale number 37432 and generates a packing slip. One copy goes inside the bale; she can print the office copy.
5. She repeats for all 5 bales. The program shows progress: 5 of 5 bales complete.

**Recording cutting waste**

1. After the program is done, there's leftover fabric. The supervisor weighs it: 1.8 kg Good Cut, 0.5 kg Fent.
2. Kiran (supervisor) opens **Record Cutting Waste** for PP-2026-0087 and enters: Good Cut = 1.8 kg, Fent = 0.5 kg, Chindi = 0 kg. Submit.
3. The accumulation stock increases by 1.8 kg Good Cut and 0.5 kg Fent.

### What success looks like
Deepa can see exactly what to pack — cut lengths, fold types, brand stamps — on the screen instead of deciphering handwritten instructions. Each bale gets a number instantly. The packing slip is generated by the system, not entered at head office days later.

---

## Head Office User (Priyanka)

### Who they are
Priyanka works at the RG Faith head office in Ahmedabad (New Cloth Market). She monitors factory operations remotely and reports to management.

### Their typical workflow

**Daily review**

1. Priyanka opens the **Stage-wise Inventory Dashboard**. She sees the same real-time view as Ramesh, but from the head office.
2. She checks **Total dispatch volume this month** — the system shows 847 bales, 86,420 metres dispatched across 23 delivery forms.
3. She opens the **Gradation Reports** list and reviews the latest completed report for MRL-0538: 96.91% Fresh yield. Good.
4. She checks **Vendor Pending Balances** — total 42,600 metres outstanding across 8 vendors.

**Report generation**

1. When management asks "how much did we ship to customer X this month?", Priyanka opens **Dispatch history for customer X** and gets the answer immediately — no waiting for paper.
2. When asked "what is our average Fresh yield?", she filters the Gradation Reports by date range and sees the trend.

### What success looks like
Priyanka has real-time visibility into factory operations without waiting for paper documents to arrive by courier. Reports that used to take hours to compile from registers are instant queries. Management gets timely answers.

---

## Handoffs Between Roles

The key handoff points in the system where one person's action becomes another's input:

| Handoff | From | To | What Happens |
|---|---|---|---|
| Inbound receipt → Folding | Kiran (records receipt) | Folding workers (pick up lot) | Lot appears in "Pending Folding" list |
| Grading → Packing | Kiran (records grades) | Ramesh (creates packing program) | Fresh material appears in "Fresh Material Available" |
| Packing program → Execution | Ramesh (creates program) | Deepa (executes packing) | Program appears in "Active Programs" with specs |
| Bale registration → Dispatch | Deepa (registers bales) | Ramesh (creates delivery form) | Bales appear in "Ready for Dispatch" grouped by customer |
| Grading → Todiya | Kiran (records non-Fresh grades) | Ramesh (creates Todiya program when buyer found) | Accumulated stock grows on dashboard |
| Grading → NA Resolution | Kiran (records Not Acceptable) | Ramesh (contacts vendor) | Entry appears on Reprocess List |
| Packaging receipt → Packing | Anil (records GRN) | Deepa (uses materials) | Stock levels increase, materials available for packing |

---

## Edge Cases and Error Scenarios

### Partial shipment from vendor
- Kiran records inbound receipt for 4,000 of 6,000 metres. MRL status changes to PARTIALLY_RECEIVED with 2,000 metres pending.
- Ramesh sees it on the Vendor Pending Balances dashboard and follows up with the vendor.
- When the remaining 2,000 metres arrive, Kiran records another receipt. MRL status changes to FULLY_RECEIVED.

### Decision Pending lot forgotten
- Kiran records a Decision Pending entry for 100 metres on a lot.
- 14 days pass with no comments or resolution.
- The system flags the entry on the Decision Pending screen with a warning: "No activity for 14 days."
- Ramesh sees the alert on his dashboard, reviews the material, and resolves it.

### Packing program cancelled
- Ramesh creates PP-2026-0088 but then receives word that the customer cancelled the order.
- No bales have been produced yet. He opens the program and clicks Cancel with reason "Customer cancelled order."
- The allocated Fresh material returns to GRADED_FRESH state and is available for a new program.

### Not Acceptable material never picked up
- An entry sits on the Reprocess List for 6 months. Multiple comments documenting calls to the vendor.
- Eventually Ramesh decides the vendor will not pick up. He resolves the entry as "Unresolved." The material remains at Miroli.

### Packaging material runs out mid-program
- During packing, the team runs out of plastic sheets.
- The packing program pauses. Ramesh checks **Packaging Stock** — sees 0 plastic sheets.
- He calls the packaging vendor. When the delivery arrives, Anil records the GRN. Stock replenishes. Packing resumes.
