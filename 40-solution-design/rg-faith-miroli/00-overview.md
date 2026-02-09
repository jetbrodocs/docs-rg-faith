# RG Faith Miroli — Inventory Tracking System

## System Description

This system is a factory-level inventory tracking application for RG Faith Creations Pvt. Ltd. at their Miroli processing facility in Ahmedabad. It tracks the lifecycle of semi-finished dyed cloth from the moment it is sent to vendor mills for dyeing, through inbound receipt, folding, quality grading, packing into branded bales, and final dispatch to customers. The system also tracks packaging materials consumed during packing and manages two exception flows: Todiya (repacking accumulated leftover material) and Not Acceptable resolution (returning rejected fabric to vendors).

The system replaces an entirely paper-based operation. All current registers, forms, and notebooks will be digitised. The head office has a separate ERP — this system is independent, with future import/export utility planned but out of scope for the initial build. No financial data (pricing, billing, invoicing) is tracked. Inventory quantities are measured in metres, kilograms, or pieces depending on the material state.

The facility has ~50 multi-skilled workers operating on an open floor plan with no fixed stations. Annual throughput is ~14 million metres. The system serves the Miroli facility exclusively — all users are on-site.

## Modules

| # | Module | PRD | What It Covers |
|---|---|---|---|
| 1 | Master Data | [01-master-data.md](01-master-data.md) | Vendors, customers (Haste), brands, products, fold types, tone codes, quality codes, trade numbers, packaging SKUs — all user-configurable |
| 2 | Outbound & Inbound | [02-outbound-inbound.md](02-outbound-inbound.md) | Grey lot lifecycle: send grey cloth to vendor for dyeing (assign MRL number), receive dyed cloth back with Gate Pass, track pending balances |
| 3 | Folding & Measurement | [03-folding-measurement.md](03-folding-measurement.md) | Fold fabric (standard 2m folds, though any length is possible), measure, calculate Chadat (metres-to-kg conversion for Fent/Rags/Chindi), reconcile against Gate Pass metres |
| 4 | Quality Grading | [04-quality-grading.md](04-quality-grading.md) | Inspect and classify into 6 grades (Fresh, Good Cut, Fent, Rags, Chindi, Not Acceptable). Fresh, Good Cut, and Not Acceptable are in metres; Fent, Rags, and Chindi are in kg. Produce progressive Gradation Report, manage Decision Pending |
| 5 | Packing Program | [05-packing-program.md](05-packing-program.md) | Create packing programs (work orders), execute cutting/folding/branding, register bales, generate packing slips, track cutting waste |
| 6 | Dispatch | [06-dispatch.md](06-dispatch.md) | Create Delivery Forms, dispatch finished bales to customers, track shipments |
| 7 | Todiya | [07-todiya.md](07-todiya.md) | Track accumulated leftovers (Good Cut in metres; Fent, Rags, Chindi in kg), create Todiya packing programs, dispatch to Todiya buyers |
| 8 | Not Acceptable Resolution | [08-not-acceptable-resolution.md](08-not-acceptable-resolution.md) | Reprocess List, vendor communication tracking, aging alerts, resolution workflow |
| 9 | Packaging Materials | [09-packaging-materials.md](09-packaging-materials.md) | GRN for packaging supplies, stock levels, consumption tracking during packing |

## End-to-End Flow

```
                                         ┌─────────────────┐
                                         │  Master Data (1) │
                                         │  Vendors, Brands,│
                                         │  Products, etc.  │
                                         └────────┬────────┘
                                                  │ referenced by all modules
                                                  ▼
┌──────────────────┐  MRL_CREATED   ┌──────────────────┐
│ Outbound &       │───────────────►│ Vendor Mill      │
│ Inbound (2)      │                │ (External)       │
│                  │◄───────────────│ Dyeing process   │
│ MRL lifecycle    │ INBOUND_       └──────────────────┘
│                  │ RECEIVED
└────────┬─────────┘
         │ Material at Miroli (Grey)
         ▼
┌──────────────────────────────────────────────────────┐
│ Folding & Measurement (3)  ◄──►  Quality Grading (4) │
│                                                       │
│ Independent activities — can happen in any order       │
│                                                       │
│ (3): 2m folds, Chadat         (4): 6 quality grades   │
│      calculation                    Gradation Report   │
└──┬──────────┬──────────┬──────────┬──────────────────┘
   │          │          │          │
   │ Fresh    │ G/C,Fent │ N/A      │ Decision
   │          │ Rags,Chi │          │ Pending
   ▼          ▼          ▼          ▼
┌────────┐ ┌────────┐ ┌──────────┐ ┌──────────────┐
│Packing │ │Todiya  │ │Not Accept│ │Awaiting      │
│Program │ │(7)     │ │Resolution│ │decision      │
│(5)     │ │        │ │(8)       │ │(14-day flag) │
└───┬────┘ └───┬────┘ └──────────┘ └──────────────┘
    │          │
    ▼          ▼
┌──────────────────┐     ┌──────────────────┐
│ Dispatch (6)     │     │ Packaging        │
│ Delivery Forms   │◄────│ Materials (9)    │
│ Ship to customer │     │ Consumed during  │
└──────────────────┘     │ packing          │
                         └──────────────────┘
```

## Shared Entities

Entities that appear across multiple modules. The responsible module creates the entity; other modules reference it.

| Entity | Created By Module | Referenced By Modules | Notes |
|---|---|---|---|
| Vendor (Mill) | Master Data (1) | Outbound & Inbound (2), NA Resolution (8) | External dyeing mills |
| Customer (Haste) | Master Data (1) | Packing Program (5), Dispatch (6), Todiya (7) | Single party identifier |
| Brand | Master Data (1) | Packing Program (5) | e.g., SSTM |
| Product | Master Data (1) | Packing Program (5) | e.g., Officer, Sportsman |
| Fold Type | Master Data (1) | Packing Program (5) | e.g., Book, Roof, 2Fold |
| Tone Code | Master Data (1) | Packing Program (5), Outbound & Inbound (2) | e.g., O1W |
| Quality Code | Master Data (1) | Outbound & Inbound (2), Grading (4) | e.g., 44x45P6 |
| Trade Number | Master Data (1) | Packing Program (5), Dispatch (6) | SKU reference, e.g., S8072-58" |
| Packaging SKU | Master Data (1) | Packaging Materials (9) | Consumable and reusable items |
| MRL (reference number) | Outbound & Inbound (2) | Folding (3), Grading (4), Packing (5), Todiya (7), NA Resolution (8) | Facility reference number assigned at outbound; tracks grey lots through lifecycle |
| Bale | Packing Program (5) | Dispatch (6) | Finished product unit |
| Inventory Levels (fabric) | Updated by modules 2-7 | Queried by all modules | Stage-wise quantities |
| Inventory Levels (packaging) | Packaging Materials (9) | Packing Program (5) | Packaging stock |

## Shared Event Types

Events emitted in one module that are consumed by projections in other modules.

| Event Type | Emitted By | Consumed By | What It Does |
|---|---|---|---|
| `MRL_CREATED` | Outbound & Inbound (2) | Inventory projection | Creates MRL record, sets initial "Sent to Vendor" inventory for the grey lot |
| `INBOUND_RECEIVED` | Outbound & Inbound (2) | Inventory projection | Adds Grey inventory for the received grey lot, updates MRL pending balance |
| `FOLDING_COMPLETED` | Folding (3) | Inventory projection, Gradation Report projection | Updates material state to Folded, records folding metres and Chadat |
| `GRADING_RECORDED` | Quality Grading (4) | Inventory projection, Gradation Report projection, Accumulation projection | Splits material into grades (Fresh/Good Cut/NA in metres; Fent/Rags/Chindi in kg), routes to appropriate destination |
| `PACKING_PROGRAM_CREATED` | Packing Program (5) | Inventory projection | Allocates Fresh material, changes state to Program Assigned |
| `BALE_REGISTERED` | Packing Program (5) | Inventory projection | Creates finished bale, moves material to Packed state |
| `CUTTING_WASTE_RECORDED` | Packing Program (5) | Accumulation projection | Adds waste to accumulated Todiya stock |
| `DELIVERY_CREATED` | Dispatch (6) | Inventory projection | Moves bales to Dispatched state |
| `PACKAGING_GRN_CREATED` | Packaging Materials (9) | Packaging inventory projection | Increases packaging stock |
| `PACKAGING_CONSUMED` | Packing Program (5) | Packaging inventory projection | Decreases packaging stock |

## Build Order

```
Phase 1: Foundation
  └── Master Data (1) — must be built first; all other modules reference it

Phase 2: Core Flow (can be built in parallel after Phase 1)
  ├── Outbound & Inbound (2) — creates MRLs and tracks grey lots through the send/receive cycle
  └── Packaging Materials (9) — independent domain, no dependencies beyond master data

Phase 3: Processing (depends on Phase 2 for MRL data)
  ├── Folding & Measurement (3) — operates on Grey material from inbound
  └── Quality Grading (4) — operates on Grey or Folded material (independent of folding)

Phase 4: Packing & Dispatch (depends on Phase 3 for graded material)
  ├── Packing Program (5) — consumes Fresh material, produces bales
  └── Dispatch (6) — ships finished bales

Phase 5: Exception Flows (can be built in parallel after Phase 3)
  ├── Todiya (7) — consumes accumulated non-Fresh material
  └── Not Acceptable Resolution (8) — manages rejected material
```

**Dependencies:**
- Phase 1 must complete before anything else begins.
- Phase 2 can begin immediately after Phase 1.
- Phase 3 requires Phase 2 (needs MRL and Grey inventory data).
- Phase 4 requires Phase 3 (needs graded material).
- Phase 5 requires Phase 3 (needs grading output) but is independent of Phase 4.
- Packaging Materials (9) can be built any time after Phase 1.

## Locations

The entire system operates at a single facility: Miroli. There are no distinct physical stations — the floor plan is open and fluid. For this system, we define:

| Location | Type | Code | Purpose |
|---|---|---|---|
| Miroli Facility | warehouse | `MIROLI` | The sole processing facility. Parent location for all operations. |
| Grey Storage | zone | `MIROLI-GREY` | Where unprocessed material sits after inbound receipt. |
| Folding/Grading Area | zone | `MIROLI-FG` | Where folding and grading happen (open area, same space). |
| Graded Storage (Fresh) | zone | `MIROLI-FRESH` | Fresh material awaiting packing program assignment. |
| Accumulation Area | zone | `MIROLI-ACCUM` | Good Cut, Fent, Rags, Chindi stored for Todiya. |
| Not Acceptable Storage | zone | `MIROLI-NA` | Rejected material awaiting vendor return. |
| Cutting/Packing Area | zone | `MIROLI-PACK` | Where packing programs are executed. |
| Finished Goods | zone | `MIROLI-FG-OUT` | Packed bales awaiting dispatch. |
| Packaging Materials Store | zone | `MIROLI-PKGMAT` | Packaging materials storage. |

Note: These are logical zones for inventory tracking purposes. Physically, the facility has no walls or marked boundaries between areas.

## Cross-Module Reports

Reports that span multiple modules and are better defined at the overview level.

| # | Business Question | Data Sources | Updated By |
|---|---|---|---|
| 1 | "Show me the real-time stage-wise inventory dashboard" | All modules (2-7) | Every state-changing event |
| 2 | "What is the full lifecycle of MRL #526?" | Modules 2, 3, 4, 5, 6 | Event store query (aggregate stream) |
| 3 | "What is our overall Fresh yield percentage this month?" | Grading (4) | `GRADING_RECORDED` events |
| 4 | "How much material is sitting at each stage right now?" | All modules | Every state-changing event |
| 5 | "What is the total pending balance at all vendors?" | Outbound & Inbound (2) | `MRL_CREATED`, `INBOUND_RECEIVED` |
| 6 | "How much accumulated stock do we have for Todiya?" | Grading (4), Packing (5), Todiya (7) | `GRADING_RECORDED`, `CUTTING_WASTE_RECORDED`, `TODIYA_PACKED` |
| 7 | "What is the end-to-end cycle time from inbound to dispatch?" | Modules 2, 6 | `INBOUND_RECEIVED`, `DELIVERY_CREATED` |

## Companion Documents

- **Reports:** [reports.md](reports.md) — 23 analytical and printable reports across 7 categories (system-wide, vendor, processing, packing, dispatch, exception, packaging materials).
- **Screen List:** [screen-list.csv](screen-list.csv) — consolidated list of all 83 screens (57 operational + 23 reports + 3 printable documents) across all modules.
- **User Journeys:** [user-journeys.md](user-journeys.md) — timeline narrative of a full day at Miroli showing all roles interacting, plus per-role reference tables.
