# User Interactions — RG Faith Miroli Inventory System

Every discrete point where a user actively changes system state — submits a form, resolves an entry, adjusts a record. Organized by process flow, matching the material lifecycle.

Excludes dashboards, reports, and passive viewing (those are read-only and don't create or modify records).

---

## 1. Inbound — Record Inbound Receipt

Two paths exist depending on whether the MRL already exists.

### 1.1 Record Inbound Receipt (New MRL)

| Field | Value |
|---|---|
| **Action** | Record arrival of finished (dyed) material from a vendor when no MRL exists yet — creates the MRL and the first receipt in one operation |
| **Screen** | Record Inbound Receipt |
| **Role** | Supervisor |
| **Trigger** | Truck arrives from vendor mill with finished material and Gate Pass document; no prior MRL exists for this consignment |
| **Data captured** | Vendor (mill), Avak Date, Lot Number (from Gate Pass), Greige Metres Sent (informational, from Gate Pass), Greige Metres Pending (informational, from Gate Pass), Finished Metres Received, Quality Code, GSM, Width, Rolls count, per-roll metres and weight, Gate Pass Reference |
| **System effect** | MRL number auto-generated (FY-prefixed). Inbound receipt record created (e.g. IR-2026-0042). MRL status = ACTIVE, material state = RECEIVED at MIROLI-RECEIVED. Inventory at MIROLI-RECEIVED increases by received metres. |
| **Auto side-effects** | None |

### 1.2 Record Inbound Receipt (Existing MRL)

| Field | Value |
|---|---|
| **Action** | Record arrival of additional finished material against an existing active MRL |
| **Screen** | Record Inbound Receipt |
| **Role** | Supervisor |
| **Trigger** | Truck arrives from vendor mill with finished material referencing an MRL that already has at least one receipt |
| **Data captured** | MRL (selected from active MRLs), Avak Date, Lot Number (from Gate Pass), Greige Metres Sent (informational, from Gate Pass), Greige Metres Pending (informational, from Gate Pass), Finished Metres Received, Quality Code, GSM, Width, Rolls count, per-roll metres and weight, Gate Pass Reference |
| **System effect** | New inbound receipt record created and linked to existing MRL. Inventory at MIROLI-RECEIVED increases by received metres. MRL remains ACTIVE. |
| **Auto side-effects** | None |

---

## 2. Folding — Record Folding Completion

### 2.1 Record Folding Completion

| Field | Value |
|---|---|
| **Action** | Record per-roll folding measurements after folding is complete — each roll gets a roll number and its measured metres |
| **Screen** | Record Folding Completion |
| **Role** | Supervisor |
| **Trigger** | Folding team has completed folding a lot's rolls (standard fold ~95-100cm); supervisor records the measured metres per roll |
| **Data captured** | MRL (selected), per-roll entries: Roll Number, Metres (measured after folding) |
| **System effect** | Folding record created for each roll. Total folded metres calculated as sum of per-roll measurements — this becomes RG Faith's verified metre count. Shrinkage calculated (finished metres received vs folded metres). Material state transitions to FOLDED. |
| **Auto side-effects** | Shrinkage percentage auto-calculated and recorded |

### 2.2 Edit Folding Record

| Field | Value |
|---|---|
| **Action** | Correct a previously recorded per-roll folding measurement |
| **Screen** | Folding Record Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Error discovered in a roll's folding measurement entry |
| **Data captured** | Corrected metre value for the specific roll entry |
| **System effect** | Roll measurement updated. Lot totals recalculated. Shrinkage percentage recalculated. |
| **Auto side-effects** | None |

### 2.3 Record Chadat

| Field | Value |
|---|---|
| **Action** | Record the Chadat value (metres-per-kg conversion factor) for a lot — separate from folding |
| **Screen** | Record Chadat |
| **Role** | Supervisor |
| **Trigger** | Supervisor weighs material and calculates the metres-to-kg ratio. Must be recorded before any non-Fresh thaan (Fent, Rags, Chindi) can be logged during packing. |
| **Data captured** | MRL (selected), Chadat value (metres per kg) |
| **System effect** | Chadat value recorded and linked to the MRL. Value available for kg-based grade calculations during packing. |
| **Auto side-effects** | None |

### 2.4 Edit Chadat Record

| Field | Value |
|---|---|
| **Action** | Correct a previously recorded Chadat value |
| **Screen** | Chadat Record Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Error discovered in the recorded Chadat value |
| **Data captured** | Corrected Chadat value (metres per kg) |
| **System effect** | Chadat value updated. Any downstream kg calculations referencing this lot may be affected. |
| **Auto side-effects** | None |

---

## 3. Classification — Tone & Finish Assignment

### 3.1 Record Classification or Mark Not Acceptable

| Field | Value |
|---|---|
| **Action** | Assign tone code and finish code to material — classifies rolls or a lot after rough inspection and head office sample return, OR mark material as Not Acceptable if rejected |
| **Screen** | Record Classification |
| **Role** | Supervisor |
| **Trigger** | Sample has been sent to head office and returned with tone and finish determination; supervisor records the classification, OR material is rejected for quality issues |
| **Data captured** | MRL (selected), Classification Decision (radio button: "Classify" or "Mark Not Acceptable").<br><br>**If Classify:** Tone Code (from master data), Finish Code (from master data), Scope (roll / lot / partial — specifying which rolls or how many metres), Metres Classified, HO Sample Sent Date (optional), HO Sample Returned Date (optional).<br><br>**If Mark Not Acceptable:** Rejection Reason (text), Metres Rejected. |
| **System effect** | **If Classify:** Classification record created. Classified material is now available for packing program sourcing. Classification appears on lot detail and roll detail views.<br><br>**If Mark Not Acceptable:** Material state → NOT_ACCEPTABLE at MIROLI-HOLD. NA_ENTRY_CREATED event auto-triggered. Entry created on Reprocess List (Module 08). |
| **Auto side-effects** | **If Classify:** None<br><br>**If Mark Not Acceptable:** Reprocess List entry created. Gradation Report updated (not_acceptable_metres tracked separately). Inventory dashboard updated (material moved to Not Acceptable Hold). |

### 3.2 Update Classification (Re-classification)

| Field | Value |
|---|---|
| **Action** | Change the tone code and/or finish code on an existing classification record |
| **Screen** | Classification Record Detail |
| **Role** | Facility Manager only (RBAC-restricted) |
| **Trigger** | Classification error identified, or head office revises tone/finish determination |
| **Data captured** | Updated Tone Code and/or Finish Code, Reason for change |
| **System effect** | Classification record updated with new tone/finish codes. Previous values preserved in audit trail. Any downstream packing programs sourcing this material reflect the updated classification. |
| **Auto side-effects** | None. No approval workflow — RBAC restriction to Facility Manager is the sole control. |

---

## 4. Packing — Program Creation and Execution

### 4.1 Create Packing Program

| Field | Value |
|---|---|
| **Action** | Create a packing program — the master instruction document for transforming classified material into branded bales |
| **Screen** | Create Packing Program |
| **Role** | Manager |
| **Trigger** | Sales order from head office (~95%), proactive inventory advancement (~5%), or Todiya sale |
| **Data captured** | Source rolls (selected from classified material across 1 or more MRLs — cross-lot sourcing allowed), Fold Type (at program level), Line items — each with: Brand, Product, Trade Number, Customer (Haste), Cut Length (metres), Pieces per Bale, Planned Bales (advisory — actual count may differ) |
| **System effect** | Packing program created (e.g. PP-2026-0087). Source rolls allocated to program. Program status = CREATED. |
| **Auto side-effects** | None |

### 4.2 Log Thaan

| Field | Value |
|---|---|
| **Action** | Log a thaan — Phase 1 of packing execution (cut and fold). This is where embedded gradation happens: each thaan is graded as it is cut and folded. |
| **Screen** | Log Thaan |
| **Role** | Worker, Supervisor |
| **Trigger** | Worker cuts a piece from a source roll and folds it per program specifications; grades the piece during the process |
| **Data captured** | Packing Program (selected), Source Roll (selected from program's allocated rolls), Grade (Fresh / Good Cut / Fent / Rags / Chindi), Quantity — metres for Fresh, Good Cut; kg for Fent, Rags, Chindi (Chadat must already be recorded for the source MRL if grade is kg-based) |
| **System effect** | Thaan record created. Thaan number auto-assigned. All grades available for bale assembly — Fresh thaans into Fresh bales, non-Fresh thaans (Good Cut / Fent / Rags / Chindi) into separate non-Fresh bales. Gradation Report for the source MRL auto-updated. |
| **Auto side-effects** | Gradation Report percentages recalculated (Fresh yield vs losses). NOT_ACCEPTABLE is NOT a valid grade at packing — quality rejection happens at classification (Module 04). |

### 4.3 Register Bale

| Field | Value |
|---|---|
| **Action** | Register a bale — Phase 2 of packing execution (assemble thaans into a bale). Fresh thaans go into Fresh bales; non-Fresh thaans go into separate non-Fresh bales. Each bale contains one grade only. |
| **Screen** | Register Bale |
| **Role** | Supervisor, Worker |
| **Trigger** | Sufficient Fresh thaans have been logged for the program; worker assembles them into a physical bale with branding, stamping, and boxing |
| **Data captured** | Packing Program (selected), Fresh thaans to include (selected from program's available Fresh thaans) |
| **System effect** | Bale record created. Bale number auto-assigned (sequential). Packing slip generated (one copy for inside bale, one for office). Bale status = PACKED, dispatch-ready. Program progress updated (e.g. "3 of 5 bales complete"). If first bale: program status -> IN_PROGRESS. If final bale: program status -> COMPLETED. |
| **Auto side-effects** | — (Packaging material tracking is deferred to a future phase.) |

### 4.4 Cancel Packing Program

| Field | Value |
|---|---|
| **Action** | Cancel a packing program before execution begins |
| **Screen** | Packing Program Detail |
| **Role** | Manager |
| **Trigger** | Customer cancels order, or program no longer needed. Only possible if no thaans have been logged yet. |
| **Data captured** | Cancellation reason (text) |
| **System effect** | Program status -> CANCELLED. All allocated source rolls released back to classified material pool. Material reappears as available for other packing programs. |
| **Auto side-effects** | None |

---

## 5. Dispatch — Delivery Scheduling and Confirmation

### 5.1 Create Delivery Form (Schedule Pickup)

| Field | Value |
|---|---|
| **Action** | Create a delivery form and schedule pickup — select packed bales for a customer and set a scheduled date |
| **Screen** | Create Delivery Form |
| **Role** | Manager, Supervisor |
| **Trigger** | Packed bales ready for shipment; customer delivery needed |
| **Data captured** | Customer (Haste), Bales to include (selected from Ready for Dispatch list, checkboxes), Scheduled Pickup Date, Notes |
| **System effect** | Delivery form created (e.g. DF-2026-0123). All selected bales status -> PICKUP_SCHEDULED. Delivery form available for printing. |
| **Auto side-effects** | Stage-wise inventory dashboard auto-updates — packed bales awaiting scheduling count decreases |

### 5.2 Dispatch Delivery (Confirm Departure)

| Field | Value |
|---|---|
| **Action** | Confirm that the truck has departed with the scheduled bales |
| **Screen** | Delivery Form Detail |
| **Role** | Manager, Supervisor |
| **Trigger** | RG Faith's truck has been loaded and departs from Miroli |
| **Data captured** | Confirmation (acknowledge departure), Departure Date/Time, Vehicle details (optional), Notes (optional) |
| **System effect** | All bales on the delivery form status -> DISPATCHED. Bales removed from MIROLI-FG-OUT inventory. Delivery form status -> DISPATCHED. |
| **Auto side-effects** | Stage-wise inventory dashboard auto-updates — pickup-scheduled count decreases |

---

## 6. Todiya — Unpack and Repack

Todiya is the process of unpacking bales that contain non-Fresh thaans (accumulated Good Cut, Fent, Rags, Chindi) and repacking them into new bales for a specific buyer. No re-cutting or re-folding occurs — thaans pass through unchanged.

### 6.1 Create Todiya Instruction

| Field | Value |
|---|---|
| **Action** | Create a Todiya instruction — specify which accumulated non-Fresh thaans to repack and the target buyer/product details |
| **Screen** | Create Todiya Instruction |
| **Role** | Manager |
| **Trigger** | Buyer found for non-Fresh bales in finished goods |
| **Data captured** | Source bales (selected from non-Fresh bales at MIROLI-FG-OUT — Good Cut / Fent / Rags / Chindi), Buyer (Haste), Brand, Product, Trade Number |
| **System effect** | Todiya instruction created. Selected bales earmarked for unpacking. Instruction status = CREATED. |
| **Auto side-effects** | — |

### 6.2 Unpack Bale

| Field | Value |
|---|---|
| **Action** | Mark a bale as unpacked, releasing its thaans back into the available pool for Todiya repacking |
| **Screen** | Todiya Instruction Detail |
| **Role** | Supervisor, Worker |
| **Trigger** | Worker physically opens a bale that was designated in the Todiya instruction |
| **Data captured** | Todiya Instruction (selected), Bale to unpack (selected from instruction's source bales) |
| **System effect** | Bale record marked as UNPACKED. Individual thaans from the bale released into the Todiya available pool. Thaans retain their original grade, metres/kg, and source MRL. |
| **Auto side-effects** | None |

### 6.3 Register Todiya Bale

| Field | Value |
|---|---|
| **Action** | Assemble unpacked thaans into a new bale for the Todiya buyer |
| **Screen** | Register Todiya Bale |
| **Role** | Supervisor, Worker |
| **Trigger** | Worker assembles selected thaans from the unpacked pool into a new physical bale |
| **Data captured** | Todiya Instruction (selected), Thaans to include (selected from unpacked pool) |
| **System effect** | New bale record created. Bale number auto-assigned. Packing slip generated (one copy inside bale, one for office). Bale status = PACKED, dispatch-ready. |
| **Auto side-effects** | — (Packaging material tracking is deferred to a future phase.) |

### 6.4 Complete Todiya Instruction

| Field | Value |
|---|---|
| **Action** | Mark a Todiya instruction as complete |
| **Screen** | Todiya Instruction Detail |
| **Role** | Manager |
| **Trigger** | All designated material has been unpacked and repacked, or manager decides the instruction is fulfilled |
| **Data captured** | Completion confirmation, Notes (optional) |
| **System effect** | Todiya instruction status -> COMPLETED. Any unallocated thaans remaining in the unpacked pool stay as UNPACKED — available for a future Todiya Instruction. |
| **Auto side-effects** | — |

---

## 7. NA Resolution — Not Acceptable Material

### 7.1 Create NA Entry

| Field | Value |
|---|---|
| **Action** | Record a Not Acceptable entry on the Reprocess List (when not auto-created from packing execution) |
| **Screen** | Create NA Entry |
| **Role** | Supervisor |
| **Trigger** | Material identified as Not Acceptable outside the normal classification flow (rarely used — most NA entries are auto-created at classification) |
| **Data captured** | MRL Number, Lot Number, Metres rejected, Quality Code, Tone, Remark (reason for rejection) |
| **System effect** | NA entry created on Reprocess List. Material tracked at MIROLI-HOLD. Entry appears on Reprocess List with aging counter from creation date. |
| **Auto side-effects** | None |

Note: Most NA entries are auto-created during classification (Record Classification, section 3.1) when material is marked as Not Acceptable.

### 7.2 Add Comment (NA Entry)

| Field | Value |
|---|---|
| **Action** | Add a comment to an NA entry documenting vendor communication or investigation progress |
| **Screen** | NA Entry Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Vendor contacted, pickup discussed, or status update needed |
| **Data captured** | Comment text |
| **System effect** | Comment added to entry history. last_activity_at timestamp resets — aging clock restarts. |
| **Auto side-effects** | Aging timer resets |

### 7.3 Resolve NA Entry

| Field | Value |
|---|---|
| **Action** | Resolve an NA entry with one of three resolution outcomes |
| **Screen** | NA Entry Detail |
| **Role** | Supervisor, Manager |
| **Trigger** | Vendor arranges pickup, OR manager decides to write off/dispose, OR manager overrides rejection and reclassifies material |
| **Data captured** | Resolution type (Returned to Vendor / Disposed / Reclassified), Resolution notes.<br><br>**If Reclassified:** Tone Code (from master data), Finish Code (from master data). |
| **System effect** | NA entry removed from active Reprocess List. Entry marked RESOLVED.<br><br>**Returned to Vendor:** Material state → RETURNED_TO_VENDOR, location → OUT (material left facility)<br>**Disposed:** Material state → DISPOSED, location → OUT (material left facility)<br>**Reclassified:** Material state → CLASSIFIED, location → MIROLI-CLASSIFIED (material proceeds to packing) |
| **Auto side-effects** | Reprocess List count decreases. Vendor Rejection Summary stats updated. If reclassified: material becomes available for packing program allocation. |

---

## 8. Packaging Materials — Stock Management

> **DEFERRED** — Packaging material management is deferred to a later phase. The interactions below are documented for completeness but will not be implemented in the initial release.

### 8.1 Record Packaging GRN

| Field | Value |
|---|---|
| **Action** | Record receipt of packaging materials from a vendor |
| **Screen** | Record Packaging GRN |
| **Role** | Worker, Supervisor |
| **Trigger** | Packaging vendor delivers supplies (cardboard boxes, plastic sheets, stickers, etc.) |
| **Data captured** | SKU (from Packaging SKU master), Vendor, Quantity, Reference (vendor invoice number) |
| **System effect** | GRN record created. Packaging stock level for the SKU increases by received quantity. |
| **Auto side-effects** | None |

### 8.2 Stock Adjustment

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
| 1.1 | Inbound | Record Inbound Receipt (New MRL) | Record Inbound Receipt | Supervisor | MRL auto-generated; material at RECEIVED |
| 1.2 | Inbound | Record Inbound Receipt (Existing MRL) | Record Inbound Receipt | Supervisor | Receipt added to existing MRL |
| 2.1 | Folding | Record Folding Completion | Record Folding Completion | Supervisor | Per-roll metres recorded; shrinkage calculated |
| 2.2 | Folding | Edit Folding Record | Folding Record Detail | Supervisor, Manager | Roll totals recalculated |
| 2.3 | Folding | Record Chadat | Record Chadat | Supervisor | Chadat value available for kg-based grades |
| 2.4 | Folding | Edit Chadat Record | Chadat Record Detail | Supervisor, Manager | Chadat value corrected |
| 3.1 | Classification | Record Classification or Mark Not Acceptable | Record Classification | Supervisor | Tone & finish assigned OR material marked Not Acceptable |
| 3.2 | Classification | Update Classification | Classification Record Detail | Facility Manager | Tone/finish changed (RBAC-restricted) |
| 4.1 | Packing | Create Packing Program | Create Packing Program | Manager | Classified rolls allocated (cross-lot) |
| 4.2 | Packing | Log Thaan | Log Thaan | Worker, Supervisor | Thaan graded; all grades available for baling (Fresh/Good Cut/Fent/Rags/Chindi only) |
| 4.3 | Packing | Register Bale | Register Bale | Supervisor, Worker | Bale number assigned; packing slip generated |
| 4.4 | Packing | Cancel Packing Program | Packing Program Detail | Manager | Allocated rolls released (only if no thaans logged) |
| 5.1 | Dispatch | Create Delivery Form | Create Delivery Form | Manager, Supervisor | Bales -> PICKUP_SCHEDULED |
| 5.2 | Dispatch | Dispatch Delivery | Delivery Form Detail | Manager, Supervisor | Bales -> DISPATCHED |
| 6.1 | Todiya | Create Todiya Instruction | Create Todiya Instruction | Manager | Non-Fresh material allocated for repacking |
| 6.2 | Todiya | Unpack Bale | Todiya Instruction Detail | Supervisor, Worker | Thaans released from bale into pool |
| 6.3 | Todiya | Register Todiya Bale | Register Todiya Bale | Supervisor, Worker | New bale created; packing slip generated |
| 6.4 | Todiya | Complete Todiya Instruction | Todiya Instruction Detail | Manager | Instruction closed; unallocated thaans stay in unpacked pool |
| 7.1 | NA Resolution | Create NA Entry | Create NA Entry | Supervisor | Entry added to Reprocess List |
| 7.2 | NA Resolution | Add Comment (NA Entry) | NA Entry Detail | Supervisor, Manager | Aging timer resets |
| 7.3 | NA Resolution | Resolve NA Entry | NA Entry Detail | Supervisor, Manager | Entry removed from active Reprocess List; three resolution outcomes: returned/disposed/reclassified |
| 8.1 | Packaging (DEFERRED) | Record Packaging GRN | Record Packaging GRN | Worker, Supervisor | Packaging stock increases |
| 8.2 | Packaging (DEFERRED) | Stock Adjustment | Stock Adjustment | Supervisor | Stock reconciled to physical count |
