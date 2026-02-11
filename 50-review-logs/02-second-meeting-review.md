---
title: "Second Meeting Review — Change Register & Q&A"
status: resolved
created: 2026-02-11
updated: 2026-02-11
tags: [review, second-meeting, changes, questions]
---

# Second Meeting Review — Change Register & Q&A

Second client meeting produced significant changes to the process model. This document captures the raw feedback, the consolidated change register, and the Q&A session used to resolve ambiguities before updating project documents.

---

## Raw Feedback Summary

Source: `00-inbox/second_meeting.md` — notes from second client meeting plus team member notes.

Key themes:
1. MRL is an inward number, not outbound
2. Outbound tracking removed from system scope
3. Terminology shift: "greige" for raw material, "finished material" for what returns
4. Folding simplified — just fold and measure, no fold type variety at this step
5. New process step: Tone & Finish Classification (after folding, before packing)
6. Packing Program is the single instruction entity (no separate folding instructions)
7. Thaan as a tracked intermediate unit between roll and bale
8. Gradation happens only as byproduct of packing execution
9. Todiya simplified — unpack and repack only, no re-cutting
10. Packaging materials deferred to next phase

---

## Consolidated Change Register

| # | Change | Severity | Action |
|---|--------|----------|--------|
| C1 | MRL is inward number — generated with first GRN, not at outbound | Critical | Rewrite MRL lifecycle across all docs |
| C2 | "Greige" for outbound raw material; "finished material" for inbound returns | Medium | Update terminology across all docs |
| C3 | No outbound record in system — pending greige metres noted from vendor Gate Pass on first inward | Critical | Remove outbound process entirely. On first inward, capture vendor's note of total greige metres |
| C4 | FY prefix + code generation for all entity codes | Low | Note for implementation time — do not add to solution design now |
| C5 | Folding simplified — generic fold, record metres per roll, no fold type at this step. Status becomes "awaiting classification" | High | Rewrite folding process. Remove fold type variety from folding step |
| C6 | New step: Tone & Finish Classification — after folding, samples to HO, factory worker enters classification after HO confirms. Two separate attributes: tone (e.g. O1W) and finish (e.g. 01, 02, 03). States: Folded → Awaiting Classification → Classified → Awaiting Program | High | Add as new process across all doc layers |
| C7 | Single "Packing Program" concept — inputs: which rolls (can be cross-lot), fold type, brand, trade, cut metres, bale count (advisory). Fold type (Book, Roof, etc.) belongs here | High | Merge previous folding instruction + packing instruction into one entity |
| C8 | Cross-lot roll selection in packing program (covered by C7) | Medium | No separate change — handled by C7 |
| C9 | Packing execution: fold+cut → thaan (logged per unit, metres + source roll) → multiple thaans → bale. Bale-to-thaan mapping tracked. Gradation output from non-Fresh thaans | High | Add thaan as tracked intermediate unit. Embedded gradation |
| C10 | Chadat recorded as separate event, flexible timing, must exist before any gradation entry | Low | Validation rule only |
| C11 | Todiya is unpack + repack only — unpack existing bale (mark as unpacked), repack unchanged thaans into new bale. No re-cutting or re-folding | Medium | Simplify Todiya model |
| C12 | Packaging materials removed from current scope — deferred to next phase | Medium | Remove packaging materials module entirely |
| C13 | Dispatch: pickup scheduled → dispatched (two-step) | Low | Add scheduling step to dispatch |
| C14 | Roll is the system term; "roll/lump" on UI only | Low | Glossary note |
| C15 | Tone/finish classification can be changed later with role-based authorization | Low | Add re-classification with RBAC |
| C16 | Terminology distinction enforced: "Classification" = tone/finish step; "Gradation/Grading" = quality sorting during packing | Medium | Enforce across all docs |

---

## Q&A Session

### Q1. Generic term for "roll" vs "lump"

**Context:** Inbound units can be rolls (proper roll of cloth) or lumps (badly folded piece). Need a term that works for both.

**Answer:** Stick with "roll" as the system term. On the front-end UI, display as "roll/lump." The physical form doesn't affect processing logic — both are tracked the same way (a unit within a lot with metres).

**Resolution:** Use "roll" in all system documentation. Add glossary note that a roll may physically be a lump.

---

### Q2. MRL number generation timing

**Context:** Is MRL created (a) with the first GRN, or (b) before the truck arrives?

**Answer:** (a) — MRL is created when the first inbound receipt (GRN) is recorded. No pre-existing record before goods physically arrive.

**Resolution:** MRL and first inbound receipt are created in the same action.

---

### Q3. Source of pending greige metres

**Context:** When recording the first inbound, where does the total greige metres figure come from?

**Answer:** The vendor's Gate Pass carries it. The vendor notes: "You sent me X metres, I'm returning Y metres, Z metres remaining." The system captures this as a note — no need for outbound tracking.

**Resolution:** Pending greige metres is a vendor-reported note on the Gate Pass, captured at first inbound receipt.

---

### Q4. Folding — what exactly is recorded

**Context:** Confirming the full scope of what's captured at folding.

**Answer:** Worker picks up a roll, folds it (standard fold), measures and records metres for that roll. Status becomes "awaiting classification." Fold length is not tracked — it's always standard. Metre reconciliation happens naturally (system has Gate Pass metres and folding metres; discrepancy is visible).

**Resolution:** Folding is: fold + measure + record metres per roll. No fold length tracking. No fold type at this step.

---

### Q5. Tone & Finish Classification — sample round-trip

**Context:** Clarifying the classification workflow and data model.

**Answer:**
- Track "sample sent" as a state — when samples are sent, status is "Awaiting Classification"
- Classification entered by factory worker after HO confirmation
- Once entered, status is "Classified" (then "Awaiting Program")
- Tone and finish are two separate attributes
  - Tone examples: O1W
  - Finish examples: 01, 02, 03

**Resolution:** States: Folded → Awaiting Classification → Classified → Awaiting Program. Two separate master data attributes: tone code and finish code.

---

### Q6. Fold type belongs to packing program

**Context:** Confirming that presentation fold type (Book, Roof, 2Fold, etc.) is a packing concern, not a folding concern.

**Answer:** Yes. Folding step is just generic fold for measurement. The presentation fold type is specified in the packing program and executed during packing.

**Resolution:** Fold type is a packing program attribute, not a folding step attribute.

---

### Q7. Thaan logging during packing execution

**Context:** Clarifying thaan data model and traceability.

**Answer:**
- Per thaan: metres + reference to source roll
- One thaan = one source roll (never from two rolls)
- Bale-to-thaan mapping is tracked (which bale contains which thaans)

**Resolution:** Full traceability chain: Roll → Thaan (metres, source roll) → Bale (contains specific thaans).

---

### Q8. Gradation only from packing

**Context:** Does gradation happen independently, or only as byproduct of packing?

**Answer:** Only as byproduct of packing. As workers cut and fold during packing execution, non-Fresh pieces (Good Cut, Fent, Chindi, Rags) are identified and logged as thaans with their grade. No standalone grading step before packing.

**Resolution:** Remove grading as an independent process. Gradation is embedded in packing execution — non-Fresh thaans are logged with grade as they're produced.

---

### Q9. Todiya — unpack and repack

**Context:** Clarifying the Todiya workflow.

**Answer:**
- Triggered by buyer being found for accumulated stock
- Unpack existing bale → mark original bale as "unpacked"
- Thaans from multiple unpacked bales can go into one new Todiya bale
- Thaans are unchanged (same metres, same identity) — just moved to new bale

**Resolution:** Todiya = buyer found → unpack bale(s) → repack unchanged thaans into new bale(s). No re-cutting, no re-folding.

---

### Q10. Authorization for tone/finish re-classification

**Context:** How is re-classification controlled?

**Answer:** Role-based permission. Certain roles can edit tone/finish classification directly. No approval workflow needed.

**Resolution:** RBAC — authorized roles can re-classify directly. No approval chain.

---

## Changes Log

_Updates to all project documents based on this review will be tracked here._

| Date | Change # | Action Taken | Files Updated |
|---|---|---|---|
| | | | |
