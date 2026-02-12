# RG Faith Miroli — Inventory Tracking System

## System Description

This system is a factory-level inventory tracking application for RG Faith Creations Pvt. Ltd. at their Miroli processing facility in Ahmedabad. It tracks the lifecycle of finished (dyed) material from the moment it arrives back from vendor mills, through folding, tone and finish classification, packing into branded bales, and final dispatch to customers. The system also manages two exception flows: Todiya (unpacking and repacking accumulated non-Fresh material) and Not Acceptable resolution (returning rejected fabric to vendors).

There is no outbound tracking — the system does not record when greige cloth is dispatched to vendors for dyeing. The process begins at inbound receipt when finished material arrives with a Gate Pass. Vendor-reported greige balances are captured as informational fields from the Gate Pass but are not independently tracked.

The system replaces an entirely paper-based operation. All current registers, forms, and notebooks will be digitised. The head office has a separate ERP — this system is independent, with future import/export utility planned but out of scope for the initial build. No financial data (pricing, billing, invoicing) is tracked. Inventory quantities are measured in metres, kilograms, or pieces depending on the material state.

Packaging material management is deferred to a future phase. The module design is retained for reference but is not in scope for the initial build.

The facility has ~50 multi-skilled workers operating on an open floor plan with no fixed stations. Annual throughput is ~14 million metres. The system serves the Miroli facility exclusively — all users are on-site.

## Modules

| # | Module | PRD | What It Covers |
|---|---|---|---|
| 1 | Master Data | [01-master-data.md](01-master-data.md) | Vendors, customers (Haste), brands, products, fold types, tone codes, finish codes, quality codes, trade numbers — all user-configurable. Packaging SKUs deferred. |
| 2 | Inbound Receipt | [02-outbound-inbound.md](02-outbound-inbound.md) | Inbound receipt of finished material from vendor mills. MRL number created at first receipt. Vendor-reported greige pending captured as informational field from Gate Pass. No outbound tracking. |
| 3 | Folding & Measurement | [03-folding-measurement.md](03-folding-measurement.md) | Standard fold (~95-100cm), per-roll metre measurement. Chadat (metres-to-kg conversion) recorded as a separate event. Reconcile folding metres against Gate Pass received metres. |
| 4 | Tone & Finish Classification | [04-quality-grading.md](04-quality-grading.md) | Assign tone code and finish code to folded material, OR mark as Not Acceptable if material is rejected. Involves factory inspection and optional Head Office confirmation. Not Acceptable material enters resolution workflow (Module 08). Not gradation — that happens embedded in Module 05 packing execution. |
| 5 | Packing Program | [05-packing-program.md](05-packing-program.md) | Create packing programs (cross-lot roll selection), execute in two phases: Phase 1 logs thaans with embedded gradation (Fresh/Good Cut/Fent/Rags/Chindi), Phase 2 assembles Fresh thaans into bales. Gradation Report produced here. |
| 6 | Dispatch | [06-dispatch.md](06-dispatch.md) | Two-step dispatch: create Delivery Form (PICKUP_SCHEDULED), then confirm departure (DISPATCHED). |
| 7 | Todiya | [07-todiya.md](07-todiya.md) | Unpack existing bales containing non-Fresh thaans, repack selected thaans into new Todiya bales. No re-cutting or re-folding — thaans pass through unchanged. |
| 8 | Not Acceptable Resolution | [08-not-acceptable-resolution.md](08-not-acceptable-resolution.md) | Reprocess List, vendor communication tracking, aging alerts, resolution workflow. NA material identified at classification (Module 04). Three resolution paths: vendor pickup (RETURNED_TO_VENDOR), manager reclassifies (RECLASSIFIED), or write-off (DISPOSED). |
| 9 | Packaging Materials (DEFERRED) | [09-packaging-materials.md](09-packaging-materials.md) | GRN for packaging supplies, stock levels, consumption tracking. Deferred to a future phase. |

## End-to-End Flow

```
                                         ┌─────────────────┐
                                         │  Master Data (1) │
                                         │  Vendors, Brands,│
                                         │  Products, Tone, │
                                         │  Finish, etc.    │
                                         └────────┬────────┘
                                                  │ referenced by all modules
                                                  ▼
                                         ┌──────────────────┐
                                         │ Vendor Mill      │
                                         │ (External)       │
                                         │ Dyeing process   │
                                         └────────┬─────────┘
                                                  │ Finished material arrives
                                                  │ with Gate Pass
                                                  ▼
                                     ┌──────────────────┐
                                     │ Inbound Receipt  │
                                     │ (2)              │
                                     │                  │
                                     │ MRL created at   │
                                     │ first receipt    │
                                     │ INBOUND_RECEIVED │
                                     └────────┬─────────┘
                                              │ Material at Miroli (Received)
                                              ▼
                                     ┌──────────────────┐
                                     │ Folding &        │
                                     │ Measurement (3)  │
                                     │                  │
                                     │ Per-roll metres, │
                                     │ Chadat (separate)│
                                     │ FOLDING_COMPLETED│
                                     │ CHADAT_RECORDED  │
                                     └────────┬─────────┘
                                              │ Folded material
                                              ▼
                                     ┌──────────────────┐
                                     │ Tone & Finish    │
                                     │ Classification(4)│
                                     │                  │
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
                              │      │
                  ┌───────────┘      │
                  │ Fresh bales      │ Non-Fresh thaans
                  ▼                  ▼
          ┌────────────┐    ┌────────────┐
          │ Dispatch    │    │ Todiya (7) │
          │ (6)         │    │            │
          │             │    │ Unpack +   │
          │ Two-step:   │    │ Repack     │
          │ Schedule →  │    │            │
          │ Dispatch    │    │ Todiya     │
          └─────────────┘    │ bales →   │
                             │ Dispatch  │
                             └───────────┘
```

## Shared Entities

Entities that appear across multiple modules. The responsible module creates the entity; other modules reference it.

| Entity | Created By Module | Referenced By Modules | Notes |
|---|---|---|---|
| Vendor (Mill) | Master Data (1) | Inbound Receipt (2), NA Resolution (8) | External dyeing mills |
| Customer (Haste) | Master Data (1) | Packing Program (5), Dispatch (6), Todiya (7) | Single party identifier |
| Brand | Master Data (1) | Packing Program (5), Todiya (7) | e.g., SSTM |
| Product | Master Data (1) | Packing Program (5), Todiya (7) | e.g., Officer, Sportsman |
| Fold Type | Master Data (1) | Packing Program (5) | e.g., Book, Roof, 2Fold |
| Tone Code | Master Data (1) | Classification (4), Packing Program (5), Inbound Receipt (2) | e.g., O1W |
| Finish Code | Master Data (1) | Classification (4), Packing Program (5) | e.g., 01, 02, 03 |
| Quality Code | Master Data (1) | Inbound Receipt (2) | e.g., 44x45P6 |
| Trade Number | Master Data (1) | Packing Program (5), Dispatch (6), Todiya (7) | SKU reference, e.g., S8072-58" |
| MRL (reference number) | Inbound Receipt (2) | Folding (3), Classification (4), Packing (5), Todiya (7), NA Resolution (8) | Facility reference number created at first inbound receipt; tracks lots through lifecycle |
| Thaan | Packing Program (5) | Todiya (7) | Individual piece — cut from one roll, logged with grade and metres |
| Bale | Packing Program (5), Todiya (7) | Dispatch (6) | Finished product unit — assembled from thaans |
| Inventory Levels (fabric) | Updated by modules 2-7 | Queried by all modules | Stage-wise quantities |

## Shared Event Types

Events emitted in one module that are consumed by projections in other modules.

| Event Type | Emitted By | Consumed By | What It Does |
|---|---|---|---|
| `INBOUND_RECEIVED` | Inbound Receipt (2) | Inventory projection | Creates MRL (first receipt) or adds receipt to existing MRL. Creates Received inventory at MIROLI-RECEIVED. |
| `MRL_UPDATED` | Inbound Receipt (2) | MRL projection | Corrects MRL details (vendor, quality code, vendor-reported greige values) |
| `MRL_CLOSED` | Inbound Receipt (2) | MRL projection | Marks MRL as closed — no more material expected |
| `FOLDING_COMPLETED` | Folding (3) | Inventory projection | Updates material state to Folded, records per-roll folding metres, calculates shrinkage |
| `CHADAT_RECORDED` | Folding (3) | Gradation Report projection | Records metres-to-kg conversion factor. Required before non-Fresh thaans can be logged. |
| `FOLDING_UPDATED` | Folding (3) | Inventory projection | Corrects a folding record (roll measurements). Recalculates shrinkage. |
| `CHADAT_UPDATED` | Folding (3) | Gradation Report projection | Corrects a Chadat record. May trigger Gradation Report recalculation. |
| `CLASSIFICATION_RECORDED` | Classification (4) | Inventory projection | Assigns tone and finish to material (State → CLASSIFIED), OR marks as Not Acceptable (State → NOT_ACCEPTABLE at MIROLI-HOLD). Event payload includes is_not_acceptable boolean flag. |
| `CLASSIFICATION_UPDATED` | Classification (4) | Inventory projection | Re-classifies material (changes tone/finish). RBAC only. |
| `PACKING_PROGRAM_CREATED` | Packing Program (5) | Inventory projection | Allocates classified rolls (cross-lot), changes state to PROGRAM_ASSIGNED |
| `THAAN_LOGGED` | Packing Program (5) | Inventory projection, Gradation Report | Logs a thaan with grade. Fresh thaans → Fresh bales. Non-Fresh → non-Fresh bales (Todiya candidates). Grades: FRESH, GOOD_CUT, FENT, RAGS, CHINDI only. |
| `BALE_REGISTERED` | Packing Program (5) | Inventory projection | Assembles Fresh thaans into a bale. State → PACKED. Packing slip generated. |
| `PACKING_PROGRAM_CANCELLED` | Packing Program (5) | Inventory projection | Returns allocated rolls to previous state |
| `DELIVERY_CREATED` | Dispatch (6) | Inventory projection | Creates Delivery Form. Bales → PICKUP_SCHEDULED. |
| `DELIVERY_DISPATCHED` | Dispatch (6) | Inventory projection | Confirms truck departure. Bales → DISPATCHED. |
| `DELIVERY_CANCELLED` | Dispatch (6) | Inventory projection | Cancels scheduled delivery. Bales revert PICKUP_SCHEDULED → PACKED. |
| `TODIYA_INSTRUCTION_CREATED` | Todiya (7) | Todiya projection | Creates instruction to unpack specified bales |
| `BALE_UNPACKED` | Todiya (7) | Bale projection, Thaan projection | Unpacks a bale, releases its thaans for repacking |
| `BALE_REGISTERED` (source=TODIYA) | Todiya (7) | Bale projection, Thaan projection | Repacks selected thaans into a new Todiya bale (same event as Module 05, source field distinguishes) |
| `TODIYA_INSTRUCTION_COMPLETED` | Todiya (7) | Todiya projection | Marks instruction as complete |
| `NA_ENTRY_CREATED` | NA Resolution (8) | NA projection | Records rejected material on Reprocess List (auto-created from CLASSIFICATION_RECORDED when is_not_acceptable = true) |
| `NA_ENTRY_COMMENTED` | NA Resolution (8) | NA projection | Adds vendor communication update. Resets aging clock. |
| `NA_ENTRY_RESOLVED` | NA Resolution (8) | NA projection, Inventory projection | Resolves entry with resolution_type: RETURNED_TO_VENDOR (material leaves), DISPOSED (write-off, material leaves), or RECLASSIFIED (includes tone_code_id + finish_code_id, transitions to CLASSIFIED) |

## Build Order

```
Phase 1: Foundation
  └── Master Data (1) — must be built first; all other modules reference it

Phase 2: Core Inbound (depends on Phase 1)
  └── Inbound Receipt (2) — creates MRLs at first receipt, tracks inbound finished material

Phase 3: Processing (depends on Phase 2 for MRL and Received inventory)
  ├── Folding & Measurement (3) — operates on Received material; per-roll metres, Chadat
  └── Tone & Finish Classification (4) — operates on Folded material; assigns tone and finish

Phase 4: Packing & Dispatch (depends on Phase 3 for Classified material)
  ├── Packing Program (5) — consumes classified rolls (cross-lot), logs thaans with embedded
  │                          gradation, assembles Fresh thaans into bales, produces Gradation Report
  └── Dispatch (6) — two-step: schedule pickup, then confirm dispatch

Phase 5: Exception Flows (depends on Phase 4 for bales and thaans)
  ├── Todiya (7) — unpacks bales with non-Fresh thaans, repacks into new Todiya bales
  └── Not Acceptable Resolution (8) — manages NA material identified during packing

Phase 6: Deferred
  └── Packaging Materials (9) — deferred to a future phase
```

**Dependencies:**
- Phase 1 must complete before anything else begins.
- Phase 2 can begin immediately after Phase 1.
- Phase 3 requires Phase 2 (needs MRL and Received inventory data).
- Phase 4 requires Phase 3 (needs Classified material and Chadat for gradation).
- Phase 5 requires Phase 4 (needs bales and thaans from packing, NA entries from thaan logging).
- Packaging Materials (9) is deferred entirely.

## Locations

The entire system operates at a single facility: Miroli. There are no distinct physical stations — the floor plan is open and fluid. For this system, we define:

| Location | Type | Code | Purpose |
|---|---|---|---|
| Miroli Facility | warehouse | `MIROLI` | The sole processing facility. Parent location for all operations. |
| Received Storage | zone | `MIROLI-RECEIVED` | Where finished material sits after inbound receipt, awaiting folding. |
| Folding/Classification Area | zone | `MIROLI-FG` | Where folding and classification happen (open area, same space). |
| Classified Storage | zone | `MIROLI-CLASSIFIED` | Classified material awaiting packing program assignment. |
| Cutting/Packing Area | zone | `MIROLI-PACK` | Where packing programs are executed — rolls moved here on allocation, thaans cut and bales assembled. |
| Finished Goods | zone | `MIROLI-FG-OUT` | Packed bales awaiting dispatch. Also where Todiya unpack/repack happens. |
| Not Acceptable Hold | zone | `MIROLI-HOLD` | Material marked as Not Acceptable at classification, awaiting resolution (vendor pickup, disposal, or reclassification). |
| Not Acceptable Storage (DEPRECATED) | zone | `MIROLI-NA` | DEPRECATED — replaced by MIROLI-HOLD. Material marked as Not Acceptable during classification now uses MIROLI-HOLD. |

Note: These are logical zones for inventory tracking purposes. Physically, the facility has no walls or marked boundaries between areas. Packaging Materials Store (`MIROLI-PKGMAT`) is deferred.

## Centralized State Machines

### Fabric Inventory States

Material progresses through these states as it moves across modules. Each transition is triggered by a specific event in a specific module.

| State | Location | Module | Description |
|---|---|---|---|
| `RECEIVED` | MIROLI-RECEIVED | Inbound (2) | Material arrived, awaiting folding |
| `FOLDED` | MIROLI-FG | Folding (3) | Folding complete, awaiting classification |
| `AWAITING_CLASSIFICATION` | MIROLI-FG | Classification (4) | Folded, classification in progress |
| `CLASSIFIED` | MIROLI-CLASSIFIED | Classification (4) | Tone and finish assigned, available for packing program |
| `PROGRAM_ASSIGNED` | MIROLI-PACK | Packing (5) | Allocated to a packing program, physically moved to cutting area |
| `NOT_ACCEPTABLE` | MIROLI-HOLD | Classification (4) | Rejected at classification — entry on Reprocess List (Module 08). NOT terminal — can transition to RETURNED_TO_VENDOR, DISPOSED, or CLASSIFIED. |
| `RETURNED_TO_VENDOR` | OUT (not at facility) | NA Resolution (8) | Material returned to vendor — terminal state, material left facility |
| `DISPOSED` | OUT (not at facility) | NA Resolution (8) | Material written off / disposed — terminal state, material left facility |

### Thaan States

| State | Location | Module | Description |
|---|---|---|---|
| `CREATED` | MIROLI-PACK | Packing (5) | Thaan cut and logged, available for bale assembly |
| `BALED` | MIROLI-FG-OUT | Packing (5) / Todiya (7) | Assembled into a bale |
| `UNPACKED` | MIROLI-FG-OUT | Todiya (7) | Released from unpacked bale, available for repacking |

### Bale States

| State | Location | Module | Description |
|---|---|---|---|
| `PACKED` | MIROLI-FG-OUT | Packing (5) / Todiya (7) | Bale assembled with packing slip, dispatch-ready. Source field: REGULAR or TODIYA. |
| `PICKUP_SCHEDULED` | MIROLI-FG-OUT | Dispatch (6) | Assigned to a Delivery Form, truck not yet departed |
| `DISPATCHED` | — | Dispatch (6) | Truck departed, bale left facility |
| `UNPACKED` | MIROLI-FG-OUT | Todiya (7) | Bale physically opened, thaans released for repacking (terminal for this bale) |

### State Transition Diagram

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

Thaan:
  (new) ──THAAN_LOGGED──► CREATED
  CREATED ──BALE_REGISTERED──► BALED
  BALED ──BALE_UNPACKED──► UNPACKED
  UNPACKED ──BALE_REGISTERED (source=TODIYA)──► BALED (in new bale)

Bale:
  (new) ──BALE_REGISTERED──► PACKED
  (new) ──BALE_REGISTERED (source=TODIYA)──► PACKED
  PACKED ──DELIVERY_CREATED──► PICKUP_SCHEDULED
  PICKUP_SCHEDULED ──DELIVERY_DISPATCHED──► DISPATCHED (terminal)
  PICKUP_SCHEDULED ──DELIVERY_CANCELLED──► PACKED (reversal)
  PACKED ──BALE_UNPACKED──► UNPACKED (terminal for this bale)
```

## Cross-Module Reports

Reports that span multiple modules and are better defined at the overview level.

| # | Business Question | Data Sources | Updated By |
|---|---|---|---|
| 1 | "Show me the real-time stage-wise inventory dashboard" | All modules (2-7) | Every state-changing event |
| 2 | "What is the full lifecycle of MRL #526?" | Modules 2, 3, 4, 5, 6 | Event store query (aggregate stream) |
| 3 | "What is our overall Fresh yield percentage this month?" | Packing (5) — Gradation Reports | `THAAN_LOGGED` events |
| 4 | "How much material is sitting at each stage right now?" | All modules | Every state-changing event |
| 5 | "What is the vendor-reported greige pending across all vendors?" | Inbound Receipt (2) | `INBOUND_RECEIVED`, `MRL_UPDATED` |
| 6 | "What bales with non-Fresh thaans are available for Todiya?" | Packing (5), Todiya (7) | `THAAN_LOGGED`, `BALE_REGISTERED`, `BALE_UNPACKED` |
| 7 | "What is the end-to-end cycle time from inbound to dispatch?" | Modules 2, 6 | `INBOUND_RECEIVED`, `DELIVERY_DISPATCHED` |

## Companion Documents

- **Reports:** [reports.md](reports.md) — analytical and printable reports across system-wide, vendor, processing, packing, dispatch, and exception categories. Packaging reports deferred.
- **Screen List:** [screen-list.csv](screen-list.csv) — consolidated list of all screens (operational + reports + printable documents) across all modules.
- **User Journeys:** [user-journeys.md](user-journeys.md) — timeline narrative of a full day at Miroli showing all roles interacting, plus per-role reference tables.
- **User Interactions:** [user-interactions.md](user-interactions.md) — every discrete point where a user actively changes system state.
