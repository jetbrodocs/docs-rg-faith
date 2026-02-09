---
title: "Process Map Review — Round 1"
status: resolved
created: 2026-02-07
updated: 2026-02-07
tags: [review, process-maps, gaps, questions]
---

# Process Map Review — Round 1

Cross-document review of all 10 process maps against the 5 observation documents. Identifies inconsistencies, gaps, and new questions.

---

## Inconsistencies to Fix

These will be resolved based on answers below and then updated in the process maps.

| # | Issue | Status |
|---|---|---|
| I1 | Folding/Grading split vs observation that they happen simultaneously — is "Folded" a real inventory state? | **RESOLVED (Q1):** Yes, Folded is real. Folding and grading are independent — no enforced sequence. |
| I2 | Good Cut routing contradiction — docs say it can pack with Fresh, but Process 08 says regular programs "Never" mix grades | **RESOLVED (Q2):** Regular = Fresh only. Good Cut always goes to accumulation/Todiya. Fix incorrect docs. |
| I3 | "Accumulated" state has no formal entry point in any process map | **RESOLVED:** Material enters "Accumulated" when weighed and stored in accumulation area after grading or cutting. Add explicit state transition. |
| I4 | Gate Pass fields (Ready Mtr, Shortage/Shrinkage) missing from Process 03 data model but needed for Gradation Report | **RESOLVED (Q5):** Our model: metres sent (MRL) → metres received (Gate Pass) → shrinkage → grade breakdown. Capture received metres in Process 03. |
| I5 | Transport contradiction — Obs 01 says RG Faith owns all transport, Obs 02 says vendor arranges inbound transport | **RESOLVED (Q4):** RG Faith owns transport. Vendor confirms readiness, RG Faith sends own vehicles. Fix Obs 02. |
| I6 | Missing glossary terms (GRN, Decision Pending, Trade Number, GSM, Fold Type, etc.) | **RESOLVED:** Added 11 new terms to CLAUDE.md glossary + 9 new project rules. |

---

## Questions

### Q1. Is "Folded" a real inventory state?

**Context:** Observation 03 says folding, measurement, and grading happen simultaneously by the same workers. The process maps split them into Process 04 and 05 with a "Folded" inventory state in between. Does material ever actually sit in a "Folded but not yet Graded" state?

**Answer:** Yes, Folded is a real inventory state. But folding and grading are **independent activities** — it is not necessary that folding happens before grading or vice versa. The system should keep this open. Material could be graded before folded, folded before graded, or both done together.

**Resolution:** Update Process 04 and 05 to remove the strict sequential dependency. Neither process should require the other as a prerequisite. The state model should allow Grey → Folded, Grey → Graded, or Grey → Folded + Graded in any order. Update the End-to-End Overview (Process 01) accordingly. Update I1 status.

---

### Q2. Can Good Cut be included in a regular (non-Todiya) packing program alongside Fresh?

**Context:** Multiple docs say Good Cut "can sometimes be packed with Fresh." But Process 08's comparison table says regular programs use "Fresh only" and "Never" mix grades. Under what conditions does Good Cut enter a regular packing program?

**Answer:** No. Regular packing programs use Fresh only. Everything that is not Fresh goes through accumulation and Todiya. The references to "can sometimes be packed with Fresh" in other documents are incorrect.

**Resolution:** Remove "can be mixed with Fresh in some cases" from Observation 03 (line 98), Observation 01 (line 129), and Process 05 (line 42). Good Cut always routes to accumulation → Todiya. Process 08's comparison table is the correct reference.

---

### Q3. Can a Packing Program be cancelled or modified after creation?

**Context:** Process 06 shows material physically moved to the cutting area when a program is created. No process map documents what happens if a program is abandoned. Is there a reverse state transition from "Packing Program Assigned" back to "Graded — Fresh"?

**Answer:** They say it won't happen in practice, but we should keep it open. Allow the reversal in the system — don't block it — but no need to design a formal cancellation process around it.

**Resolution:** Add a note in Process 06 that the system should allow reversal of Packing Program assignment (back to Graded — Fresh) but this is not a formal process. No dedicated workflow needed. Just don't lock the state transition.

---

### Q4. Who arranges transport for inbound deliveries?

**Context:** Observation 01 says "RG Faith owns its own transport. No external logistics." Observation 02 says "Vendor arranges transport" for returning dyed cloth. Which is correct?

**Answer:** Transport is owned by RG Faith. But they need the vendor's confirmation before sending their vehicles to pick up the goods. RG Faith arranges transport; vendor confirms readiness.

**Resolution:** Fix Observation 02 (line 147) — change "Vendor arranges transport" to "RG Faith sends own vehicles after vendor confirms goods are ready." Observation 01 is correct. Update Process 03 to reflect that RG Faith's own transport picks up from vendor.

---

### Q5. What is "Grey U/S Mtrs" on the Gradation Report?

**Context:** The Gradation Report shows "Grey U/S Mtrs: 6,006.80" as distinct from "Gate Pass Mtrs: 5,826.00." Is Grey U/S the original outbound metres from the MRL record (before vendor processing), as opposed to the Gate Pass metres (after processing)?

**Answer:** During the visit, they said both values should have been the same. The person explaining wasn't sure why they differ. For our system, the model is: **metres sent (from MRL outbound) → metres received (from Gate Pass) = shrinkage → then from what was received, how much became Fresh vs other grades.** We don't need to replicate the Grey U/S vs Gate Pass ambiguity.

**Resolution:** Our Gradation Report metre progression should be: (1) Metres sent (MRL outbound), (2) Metres received (Gate Pass), (3) Shrinkage = difference, (4) Grade breakdown of received metres. Update Process 03 to capture "Ready Mtr" / received metres from Gate Pass. Update Observation 03's Gradation Report section to note the Grey U/S anomaly and our simplified model. Resolves I4 partially.

---

### Q6. What triggers someone to revisit a Decision Pending lot?

**Context:** Decision Pending lots can sit for months/years. Is there any periodic review process, or does it happen only when someone remembers?

**Answer:** Decision Pending lots occupy inventory space — that's a cost. They would want to revisit if there's been no comment/activity for two weeks. Currently there's no system to enforce this, so lots get forgotten.

**Resolution:** Update Process 05 Decision Pending section: add a business rule — "lots with no comment/activity for 14 days should be flagged for revisit." System should auto-escalate or alert. This is a concrete threshold for the aging alerts already mentioned in the design implications. Update Observation 03 and 05 similarly.

---

### Q7. What is the relationship between "Delivered to" and "Haste" on the Delivery Form?

**Context:** Both fields appear on the Delivery Form with different values (e.g., Delivered to: "P.M. Chhapti Tarat, S.P." and Haste: "Mohan Ram"). Is one the physical address/entity and the other the account/party? Are they always different?

**Answer:** The difference is an artifact of not having a digital system — without unified customer records, two different names end up on the form. Haste is the meaningful identifier — the team knows what to do when they see the Haste name. In our system, both could mean the same thing. Haste is what matters operationally.

**Resolution:** In our system, use a single customer/party field (Haste). No need to replicate the "Delivered to" vs "Haste" split — that's a paper-form artifact. Update Process 07 to note that Haste is the primary customer identifier. The Delivery Form in the system uses one customer reference from the party master.

---

### Q8. Is Not Acceptable material measured in metres or kg?

**Context:** All documents say "metres or kg" but none clarify the rule. Does it depend on whether the rejection happened before cutting (full roll = metres) vs after cutting (cut-out section = kg)?

**Answer:** Metres. Always.

**Resolution:** Update all documents that say "metres or kg" for Not Acceptable to just "metres." Affected: Observation 01 (line 122), Observation 03 (line 102), Process 05 (line 46), Process 09 (line 33). The Reprocess List tracks Not Acceptable in MTR (metres) — consistent with scan page 2.

---

### Q9. Is there a return process for finished bales rejected by customers?

**Context:** Process 07 mentions "Customer rejects bales on receipt — Informal process — bales returned" as an exception. Does returned material re-enter inventory? At what state?

**Answer:** Out of scope. We don't need to accept returns.

**Resolution:** Remove the "Customer rejects bales" exception from Process 07. No return/inbound flow for finished goods needed in the system.

---

### Q10. What is "SST Sec" on the Delivery Form?

**Context:** The field appears with example values "Fresh" and "11." The name and values are unclear.

**Answer:** It's a variation/sub-classification of the trade number. In this case all Fresh, but a trade number can have variations. Think of it as a variant attribute on the finished product SKU.

**Resolution:** Update Process 07 to clarify "SST Sec" as a trade number variant. In the system, this can be modelled as an attribute of the bale/trade number — not a separate field. Add to the bale identity attributes in Process 06 if needed.

---

### Q11. Can packed bales sit undispatched for extended periods?

**Context:** Is there a significant gap between packing completion and dispatch, or are bales typically shipped immediately?

**Answer:** Fresh cut bales are typically shipped immediately. Exceptions are rare. For non-Fresh (Todiya) bales, it could take days — there's a Todiya khata (account) involved, so dispatch depends on the buyer arrangement.

**Resolution:** Note in Process 07 that Fresh bales are dispatched near-immediately. Todiya bales may sit longer pending buyer logistics. The system should track "Packed" as a distinct state from "Dispatched" to capture this gap, especially for Todiya bales.

---

### Q12. What is "Batch No" on the Gradation Report?

**Context:** Example: "ML 26-Ant26-7993." Appears alongside the MRL number but seems to be a different identifier. Who assigns it and what does it reference?

**Answer:** Don't need to worry about it. It's a head office ERP reference. We just need to track one MRL number.

**Resolution:** No action needed. Batch No is a legacy ERP field — not replicated in our system. MRL is the sole lot-level tracking identifier.

---

### Q13. What triggers the transition from "Packed" to "ready for dispatch"?

**Context:** Is dispatch automatic after packing completes, or is there an approval/release step?

**Answer:** The packing slip. Once a bale has a packing slip, it's ready for dispatch. No separate approval step.

**Resolution:** Note in Process 06 and 07 that packing slip generation marks a bale as dispatch-ready. This is the handoff trigger between packing and dispatch — no approval gate in between.

---

### Q14. What does the fold type "B1F" stand for?

**Context:** Referenced in multiple packing programs but meaning is unknown. Other fold types (Book, Roof, 2Fold) have clear names.

**Answer:** Probably a notation for a book fold variant. Doesn't matter to us — fold types are user-configurable. They define their own terminology.

**Resolution:** No action needed beyond what's already documented. Fold types are part of the configurable master data. Remove the "TBD" note from Observation 04 (line 213) and replace with "user-defined fold type notation."

---

## Changes Log

_Updates to process maps and observations based on resolved questions will be tracked here._

| Date | Question | Change Made | Files Updated |
|---|---|---|---|
| 2026-02-07 | Q1 (Folding/Grading independence) | Removed strict sequential dependency. Folding and grading are independent activities. | Process 01, 04, 05 |
| 2026-02-07 | Q2 (Good Cut routing) | Removed "can be mixed with Fresh." Good Cut always goes to accumulation/Todiya. | Obs 01, Obs 03, Process 05 |
| 2026-02-07 | Q3 (Packing Program reversal) | Added reversal note — system allows but rare in practice. | Process 06 |
| 2026-02-07 | Q4 (Transport) | Fixed to "RG Faith owns transport, vendor confirms readiness." | Obs 02, Process 03 |
| 2026-02-07 | Q5 (Grey U/S Mtrs) | Added note explaining anomaly. Simplified metre model for our system. | Obs 03 |
| 2026-02-07 | Q6 (Decision Pending threshold) | Added 14-day no-activity flag for revisit. | Process 05 |
| 2026-02-07 | Q7 (Haste as single customer ID) | Consolidated to single Haste field, removed Delivered to split. | Process 07 |
| 2026-02-07 | Q8 (Not Acceptable = metres) | Changed "metres or kg" to "metres" everywhere. | Obs 01, Obs 03, Process 05, Process 09 |
| 2026-02-07 | Q9 (Customer returns) | Removed customer returns exception. Out of scope. | Process 07 |
| 2026-02-07 | Q10 (SST Sec) | Clarified as trade number variant. | Process 07 |
| 2026-02-07 | Q11 (Dispatch timing) | Added Fresh = immediate, Todiya = may wait. | Process 07 |
| 2026-02-07 | Q12 (Batch No) | No action — legacy ERP field, not replicated. | — |
| 2026-02-07 | Q13 (Dispatch trigger) | Packing slip = dispatch-ready. No approval step. | Process 06, Process 07 |
| 2026-02-07 | Q14 (B1F) | Changed "TBD" to "user-defined fold type notation." | Obs 04 |
| 2026-02-07 | I6 (Missing glossary) | Added 11 new terms to CLAUDE.md glossary + 9 new project rules. | CLAUDE.md |
