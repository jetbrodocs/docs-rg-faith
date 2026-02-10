# User Interactions — RG Faith Miroli Inventory System

Every discrete point where a user actively changes system state — submits a form, resolves an entry, adjusts a record. Organized by process flow, matching the material lifecycle.

Excludes dashboards, reports, and passive viewing (those are read-only and don't create or modify records).

---

## 1. Outbound — Create Grey Lot

### 1.1 Create Grey Lot

| Field | Value |
|---|---|
| **Action** | Create a new grey lot record for cloth being sent to a vendor mill for dyeing |
| **Screen** | Create Grey Lot |
| **Role** | Manager |
| **Trigger** | Woven cloth ready for dyeing; manager decides which vendor to send to |
| **Data captured** | Vendor (mill), Metres Sent, Quality Code, Date Sent |
| **System effect** | New grey lot created with status SENT_TO_VENDOR. MRL Number auto-assigned as lifetime tracking ID. Material appears on Vendor Pending Balances with full balance outstanding. |
| **Auto side-effects** | None |

---

## 2. Inbound — Record Inbound Receipt

### 2.1 Record Inbound Receipt

| Field | Value |
|---|---|
| **Action** | Record arrival of dyed cloth from vendor, matching it to an existing grey lot |
| **Screen** | Record Inbound Receipt |
| **Role** | Supervisor |
| **Trigger** | Truck arrives from vendor mill with dyed cloth and Gate Pass document |
| **Data captured** | Grey Lot (selected from dropdown), Avak Date, Lot Number (from Gate Pass), Grey Metres, Quality Code, GSM, Width, Rolls count, Gate Pass Reference. Optional: per-roll metres and weight. |
| **System effect** | Inbound receipt record created (e.g. IR-2026-0042). Grey lot pending balance reduced by received metres. If fully received: grey lot status → FULLY_RECEIVED. If partial: status → PARTIALLY_RECEIVED with remaining balance shown. Grey inventory at MIROLI-GREY increases by received metres. |
| **Auto side-effects** | Grey lot status auto-transitions based on whether pending balance reaches zero |

---

## 3. Folding — Record Fold Measurement

### 3.1 Record Fold Measurement

| Field | Value |
|---|---|
| **Action** | Record a measurement point during the folding process — captures cumulative metres at each fold |
| **Screen** | Record Fold Measurement |
| **Role** | Supervisor |
| **Trigger** | Folding team working through a grey lot; supervisor periodically records measured metres |
| **Data captured** | Grey Lot (selected), Cumulative Metres at this fold point |
| **System effect** | Fold measurement record created. When lot is fully folded: final measurement becomes RG Faith's verified metre count. Chadat value recorded (metres ÷ kg conversion factor for this lot). Lot status transitions from GREY to FOLDED. Shrinkage calculated (grey metres vs folding metres). |
| **Auto side-effects** | Chadat value locked for this lot — used later for kg-based grades (Fent, Rags, Chindi) |

### 3.2 Edit Folding Record

| Field | Value |
|---|---|
| **Action** | Correct a previously recorded fold measurement value |
| **Screen** | Folding Record Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Error discovered in a fold measurement entry |
| **Data captured** | Corrected metre value for the specific fold entry |
| **System effect** | Fold measurement updated. Lot totals recalculated. Chadat may be recalculated if total folding metres change. |
| **Auto side-effects** | None |

---

## 4. Grading — Quality Classification

### 4.1 Record Grading

| Field | Value |
|---|---|
| **Action** | Record a grading entry — classify a portion of material into a quality grade |
| **Screen** | Record Grading |
| **Role** | Worker, Supervisor |
| **Trigger** | Workers inspecting grey or folded material; grading entries submitted progressively as sections are assessed |
| **Data captured** | Grey Lot (selected), Grade (Fresh / Good Cut / Fent / Rags / Chindi / Not Acceptable), Quantity — metres for Fresh, Good Cut, Not Acceptable; kg for Fent, Rags, Chindi. Chadat auto-filled from lot record. |
| **System effect** | Grading record created. Material routed by grade: Fresh → GRADED_FRESH at MIROLI-FRESH (available for packing). Good Cut → accumulation stock (metres). Fent / Rags / Chindi → accumulation stock (kg, with equivalent metres via Chadat). Not Acceptable → MIROLI-NA. Gradation Report for this lot auto-updated with new entry. |
| **Auto side-effects** | If grade = NOT_ACCEPTABLE: auto-creates entry on Reprocess List with lot details and remark. Accumulation Dashboard totals auto-updated for Good Cut / Fent / Rags / Chindi. Gradation Report percentages recalculated. |

### 4.2 Create Decision Pending

| Field | Value |
|---|---|
| **Action** | Flag a portion of material where quality is unclear and grading decision cannot yet be made |
| **Screen** | Record Grading (grade = Decision Pending) |
| **Role** | Supervisor |
| **Trigger** | Quality ambiguity during grading — colour variation, subtle defect, unclear classification |
| **Data captured** | Grey Lot, Metres flagged, Remark describing the issue |
| **System effect** | Decision Pending entry created. Material remains in limbo — occupies inventory space but is not assigned to any grade. Entry appears on Decision Pending list with aging counter starting from creation date. |
| **Auto side-effects** | 14-day inactivity alert: if no comments or resolution for 14 days, entry flagged with red warning on Decision Pending screen |

### 4.3 Resolve Decision Pending

| Field | Value |
|---|---|
| **Action** | Resolve a pending quality decision by assigning a final grade |
| **Screen** | Decision Pending Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Manager inspects physical material and makes a quality determination |
| **Data captured** | Resolved Grade (Fresh / Good Cut / Fent / Rags / Chindi / Not Acceptable) |
| **System effect** | Decision Pending entry resolved and removed from active list. Material moves to the resolved grade's inventory location — e.g. if resolved as FRESH, metres move to GRADED_FRESH and appear on Fresh Material Available. Gradation Report updated. |
| **Auto side-effects** | Same downstream effects as Record Grading for the resolved grade (e.g. if resolved as Not Acceptable, auto-creates Reprocess List entry) |

### 4.4 Add Comment (Decision Pending)

| Field | Value |
|---|---|
| **Action** | Add a comment to a Decision Pending entry to document investigation progress |
| **Screen** | Decision Pending Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Ongoing investigation — noting observations, next steps, or partial findings |
| **Data captured** | Comment text |
| **System effect** | Comment added to entry's history. last_activity_at timestamp resets — aging clock restarts from this point. |
| **Auto side-effects** | 14-day inactivity alert timer resets |

---

## 5. Packing — Program Creation and Execution

### 5.1 Create Packing Program

| Field | Value |
|---|---|
| **Action** | Create a packing program — the master instruction document for transforming Fresh material into branded bales |
| **Screen** | Create Packing Program |
| **Role** | Manager |
| **Trigger** | Sales order from head office (~95%), proactive inventory advancement (~5%), or Todiya sale |
| **Data captured** | Source lot (selected from Fresh Material Available), Line items — each with: Brand, Product, Trade Number, Fold Type, Customer (Haste), Cut Length (metres), Pieces per Bale, Planned Bales |
| **System effect** | Packing program created (e.g. PP-2026-0087). System calculates total metres: cut length × pieces × bales. Allocated metres move from GRADED_FRESH to PROGRAM_ASSIGNED at MIROLI-PACK. Fresh Material Available reduced accordingly. Program status = CREATED. |
| **Auto side-effects** | None |

### 5.2 Register Bale

| Field | Value |
|---|---|
| **Action** | Register a completed bale — record that a physical bale has been packed and is ready |
| **Screen** | Register Bale |
| **Role** | Supervisor, Worker |
| **Trigger** | Packing team finishes cutting, folding, stamping, and boxing one bale per program specifications |
| **Data captured** | Program (selected), Line item, Pieces, Total Metres |
| **System effect** | Bale record created. Bale number auto-assigned (sequential). Packing slip generated (one copy for inside bale, one for office). Bale status = packed, dispatch-ready. Program progress updated (e.g. "3 of 5 bales complete"). If first bale: program status → IN_PROGRESS. If final bale: program status → COMPLETED. |
| **Auto side-effects** | Packaging materials auto-deducted from stock per product BOM (backflush) — e.g. 1 cardboard box, 2 plastic sheets, 1 sticker set per bale. Packaging Stock levels decrease automatically. |

### 5.3 Record Cutting Waste

| Field | Value |
|---|---|
| **Action** | Record waste generated during a packing program's cutting process |
| **Screen** | Record Cutting Waste |
| **Role** | Supervisor |
| **Trigger** | Packing program completed or waste ready to be recorded |
| **Data captured** | Program (selected), Waste by grade: Good Cut (metres), Fent (kg), Chindi (kg) |
| **System effect** | Cutting waste record created and linked to program. Waste quantities added to accumulation stock. |
| **Auto side-effects** | Accumulation Dashboard totals auto-updated — Good Cut, Fent, Chindi balances increase |

### 5.4 Cancel Packing Program

| Field | Value |
|---|---|
| **Action** | Cancel a packing program before completion |
| **Screen** | Packing Program Detail |
| **Role** | Manager |
| **Trigger** | Customer cancels order, or program no longer needed. Only possible if no bales have been registered yet. |
| **Data captured** | Cancellation reason (text) |
| **System effect** | Program status → CANCELLED. All allocated Fresh material returns from PROGRAM_ASSIGNED to GRADED_FRESH. Material reappears on Fresh Material Available for other programs. |
| **Auto side-effects** | None |

---

## 6. Dispatch — Create Delivery Form

### 6.1 Create Delivery Form

| Field | Value |
|---|---|
| **Action** | Create a delivery form to dispatch packed bales to a customer |
| **Screen** | Create Delivery Form |
| **Role** | Manager, Supervisor |
| **Trigger** | Packed bales ready for shipment; customer delivery needed |
| **Data captured** | Customer (Haste), Bales to include (selected from Ready for Dispatch list, checkboxes), Date, Notes |
| **System effect** | Delivery form created (e.g. DF-2026-0123). All selected bales status → DISPATCHED. Bales removed from Ready for Dispatch / MIROLI-FG-OUT inventory. Delivery form available for printing. |
| **Auto side-effects** | Stage-wise inventory dashboard auto-updates — packed bales awaiting dispatch count decreases |

---

## 7. Todiya — Leftover Repacking

### 7.1 Create Todiya Program

| Field | Value |
|---|---|
| **Action** | Create a Todiya packing program to repack accumulated leftover material for a buyer |
| **Screen** | Create Todiya Program |
| **Role** | Manager |
| **Trigger** | Buyer found for accumulated Good Cut / Fent / Rags stock |
| **Data captured** | Source grades (Good Cut / Fent / Rags / Chindi), Quantity (metres for Good Cut, kg for others), Line items — each with: Brand, Product, Trade Number, Customer (Haste) |
| **System effect** | Todiya program created (type = TODIYA). Selected quantities allocated from accumulation stock. Accumulation Dashboard balances decrease. Program follows same lifecycle as regular packing (Register Bale → Record Waste → Dispatch). |
| **Auto side-effects** | None. Downstream bale registration and dispatch follow the same interactions as sections 5.2, 5.3, and 6.1. |

---

## 8. NA Resolution — Not Acceptable Material

### 8.1 Create NA Entry

| Field | Value |
|---|---|
| **Action** | Record a Not Acceptable entry on the Reprocess List (when not auto-created from grading) |
| **Screen** | Create NA Entry |
| **Role** | Supervisor |
| **Trigger** | Material identified as Not Acceptable outside the normal grading flow |
| **Data captured** | MRL Number, Lot Number, Metres rejected, Quality Code, Tone, Remark (reason for rejection) |
| **System effect** | NA entry created on Reprocess List. Material tracked at MIROLI-NA. Entry appears on Reprocess List with aging counter from creation date. |
| **Auto side-effects** | None |

### 8.2 Add Comment (NA Entry)

| Field | Value |
|---|---|
| **Action** | Add a comment to an NA entry documenting vendor communication or investigation progress |
| **Screen** | NA Entry Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Vendor contacted, pickup discussed, or status update needed |
| **Data captured** | Comment text |
| **System effect** | Comment added to entry history. last_activity_at timestamp resets — aging clock restarts. |
| **Auto side-effects** | Aging timer resets |

### 8.3 Resolve NA Entry

| Field | Value |
|---|---|
| **Action** | Resolve an NA entry — vendor picked up rejected material, or entry written off |
| **Screen** | NA Entry Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Vendor arranges pickup, or manager decides to write off after extended non-response |
| **Data captured** | Resolution type (Pickup / Write-off), Resolution notes |
| **System effect** | NA entry removed from active Reprocess List. If Pickup: material leaves MIROLI-NA inventory. If Write-off: material remains at facility but is no longer tracked as pending resolution. Entry preserved in resolution history. |
| **Auto side-effects** | Reprocess List count decreases. Vendor Rejection Summary stats updated. |

---

## 9. Packaging Materials — Stock Management

### 9.1 Record Packaging GRN

| Field | Value |
|---|---|
| **Action** | Record receipt of packaging materials from a vendor |
| **Screen** | Record Packaging GRN |
| **Role** | Worker, Supervisor |
| **Trigger** | Packaging vendor delivers supplies (cardboard boxes, plastic sheets, stickers, etc.) |
| **Data captured** | SKU (from Packaging SKU master), Vendor, Quantity, Reference (vendor invoice number) |
| **System effect** | GRN record created. Packaging stock level for the SKU increases by received quantity. |
| **Auto side-effects** | None |

### 9.2 Stock Adjustment

| Field | Value |
|---|---|
| **Action** | Reconcile packaging stock — enter physical count to correct system balance against actual usage |
| **Screen** | Stock Adjustment |
| **Role** | Supervisor |
| **Trigger** | Periodic stock check, or suspected discrepancy between system (backflushed) quantities and physical stock |
| **Data captured** | SKU, Physical Count |
| **System effect** | System shows difference between recorded stock and physical count. Stock level adjusted to match physical count. Adjustment record created showing variance. |
| **Auto side-effects** | None |

---

## Summary Table

| # | Flow | Interaction | Screen | Role | Key Side-Effect |
|---|---|---|---|---|---|
| 1.1 | Outbound | Create Grey Lot | Create Grey Lot | Manager | MRL created at SENT_TO_VENDOR |
| 2.1 | Inbound | Record Inbound Receipt | Record Inbound Receipt | Supervisor | Grey inventory increases; lot status auto-transitions |
| 3.1 | Folding | Record Fold Measurement | Record Fold Measurement | Supervisor | Chadat locked; lot → FOLDED |
| 3.2 | Folding | Edit Folding Record | Folding Record Detail | Supervisor, Manager | Lot totals recalculated |
| 4.1 | Grading | Record Grading | Record Grading | Worker, Supervisor | Material routed by grade; Gradation Report updated |
| 4.2 | Grading | Create Decision Pending | Record Grading | Supervisor | 14-day inactivity alert activated |
| 4.3 | Grading | Resolve Decision Pending | Decision Pending Detail | Supervisor, Manager | Material moves to resolved grade's inventory |
| 4.4 | Grading | Add Comment | Decision Pending Detail | Supervisor, Manager | Aging timer resets |
| 5.1 | Packing | Create Packing Program | Create Packing Program | Manager | Fresh material allocated to program |
| 5.2 | Packing | Register Bale | Register Bale | Supervisor, Worker | Bale number assigned; packaging backflushed per BOM |
| 5.3 | Packing | Record Cutting Waste | Record Cutting Waste | Supervisor | Waste added to accumulation stock |
| 5.4 | Packing | Cancel Program | Packing Program Detail | Manager | Allocated material returns to GRADED_FRESH |
| 6.1 | Dispatch | Create Delivery Form | Create Delivery Form | Manager, Supervisor | Bales → DISPATCHED |
| 7.1 | Todiya | Create Todiya Program | Create Todiya Program | Manager | Accumulation stock allocated to program |
| 8.1 | NA Resolution | Create NA Entry | Create NA Entry | Supervisor | Entry added to Reprocess List |
| 8.2 | NA Resolution | Add Comment | NA Entry Detail | Supervisor, Manager | Aging timer resets |
| 8.3 | NA Resolution | Resolve NA Entry | NA Entry Detail | Supervisor, Manager | Entry removed from active Reprocess List |
| 9.1 | Packaging | Record Packaging GRN | Record Packaging GRN | Worker, Supervisor | Packaging stock increases |
| 9.2 | Packaging | Stock Adjustment | Stock Adjustment | Supervisor | Stock reconciled to physical count |
