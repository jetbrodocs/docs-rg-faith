# Project Configuration

## Project Description

Factory-level inventory tracking system for RG Faith Creations Pvt. Ltd. at their Miroli facility in Ahmedabad. The system tracks finished material (returned from dyeing vendors) at each processing stage (inbound → folding → tone/finish classification → packing with embedded gradation → dispatch) with quantities in meters or kg. No financial data tracking. No outbound tracking — the system begins at inbound receipt. Packaging materials are deferred to a future phase. Independent system with future import/export utility for head office ERP.

## Domain Glossary

| Term | Definition |
|---|---|
| Miroli | RG Faith's processing facility — all operations happen here |
| MRL No | Miroli lot number — an inward number generated when the first inbound receipt (GRN) is recorded for a lot. Central tracking ID for the lot through all processing stages. |
| Greige | Raw/unprocessed fabric sent to vendor mills for dyeing. The outbound material. Industry-standard term preferred by client. |
| Finished Material | Dyed/processed cloth returned from vendor mills. The inbound material. |
| Avak | Incoming/arrival — "Avak Date" = date material arrived at Miroli |
| Roll | A unit of fabric within a lot. May physically be a roll or a lump (badly folded piece). "Roll" is the system term; UI displays "Roll/Lump." |
| Grey | Legacy term for unprocessed state of inbound material. In the updated model, inbound material is "finished material" from vendor, entering the system at receipt. |
| Fresh | Highest quality grade — good quality fabric, measured in meters |
| Good Cut | Second quality grade, measured in metres |
| Fent | Lower quality grade, measured in kg |
| Rags | Lower quality grade, measured in kg |
| Chindi | Lowest quality grade, 100% loss, measured in kg |
| Chadat | Conversion factor between metres and kg for a specific lot — used for grades measured in kg (Fent, Rags, Chindi). Recorded as a separate event; must exist before any gradation entry. |
| Thaan | A cut and folded piece of fabric produced during packing execution. Intermediate tracked unit between roll and bale. Each thaan has metres and a source roll reference. One thaan = one source roll. |
| Haste | "For [party name]" — indicates which customer/party goods are destined for |
| Todiya / Toria | Reassigning inventory — unpack existing bale(s), repack unchanged thaans into new bale(s) under a new program for a different buyer. No re-cutting or re-folding. "Todiya" is the primary spelling used. |
| Gate Pass | Inbound reference document from the vendor mill, accompanies the truck. Also carries vendor's note of total greige metres sent and pending balance. |
| SSTM | Shree Shubhlaxmi Textile Mills — primary brand name (~90%) under RG Faith |
| Bale | Final packed unit — cardboard box with plastic layers, stickers, brand stamps, thread. Contains specific thaans (bale-to-thaan mapping tracked). |
| Packing Program | Instruction document specifying which rolls to pick up (can be cross-lot), fold type, brand, trade, cut metres, and target bale count (advisory, not mandatory). Triggers: sales order (~95%), proactive inventory advancement (~5%), Todiya (leftovers). |
| Classification | The step where tone and finish are assigned to rolls after folding. Samples sent to head office; factory worker enters classification after HO confirmation. Distinct from gradation. |
| Gradation / Grading | Quality sorting that happens during packing execution — non-Fresh pieces (Good Cut, Fent, Chindi, Rags) identified and logged as thaans with their grade. Not a standalone process. Distinct from classification. |
| Gradation Report | Progressive report showing yield analysis — Fresh % vs losses, shrinkage tracking |
| Tone | Colour/shade attribute assigned during classification (e.g., O1W = Off-White). Master data entity. |
| Finish | Surface treatment/quality attribute assigned during classification (e.g., 01, 02, 03). Separate from tone. Master data entity. |
| Trade Number | Finished product SKU reference assigned at packing time (e.g., S8072-58") |
| Fold Type | How fabric is folded during packing (Book, Roof, 2Fold, B1F, etc.) — specified in the packing program, not at the folding step. User-configurable terminology. |
| GSM | Grams per Square Metre — fabric weight/density attribute on incoming cloth |
| Decision Pending | Inventory state for lots where quality is unclear and grading decision has not been made. Should be revisited if no activity for 14 days. |
| Fresh Pending | Classified Fresh material not yet assigned to a packing program — awaiting packing. |
| Reprocess List | Register tracking Not Acceptable material pending return to vendor |
| Cutting No | Identifier for individual packing programs when multiple appear on one physical form (Cutting No 1, 2, 3 = separate programs) |
| F.H. | Folding House — refers to the folding area at Miroli. Appears on Gradation Report fields (e.g., F.H. Avak Mtrs, F.H. Fold Mtrs). |
| O1W | Off-White (tone code example) |
| Not Acceptable | Rejected material — always measured in metres. Tracked on Reprocess List for vendor return. |
| Greige Challan No | Outbound reference number used when sending greige to vendor. Also referred to as L.R. No. System does not track outbound — this is a vendor-side reference. |

## Folder Structure

| Folder | Purpose |
|---|---|
| `00-inbox/` | Raw notes, uploads, unprocessed material |
| `10-observations/` | Structured observations from site visits |
| `20-process-maps/` | Process documentation built from observations |
| `30-analysis/` | Analysis documents, findings, comparisons |
| `40-solution-design/` | Requirements, data models, architecture, tech decisions |
| `50-review-logs/` | Review session logs with gaps and questions |

## Team

| Name | Role | Notes |
|---|---|---|
| <!-- Add team members --> | | |

## Project-Specific Rules

- No financial data tracking — inventory quantities only (meters and kg)
- Use "greige" for raw outbound material; "finished material" for what returns from vendor
- System is independent from head office ERP — future import/export utility only
- No outbound tracking — the system starts at inbound receipt. Pending greige metres are a vendor-reported note on the Gate Pass.
- MRL number is generated at the first inbound receipt (GRN), not at outbound
- Master data (brands, products, fold types, tone codes, finish codes, quality codes) must be user-configurable
- Chadat is the conversion bridge between metres and kg — needed for Fent, Rags, and Chindi (which are measured in kg). Fresh, Good Cut, and Not Acceptable are all measured in metres. Chadat must be recorded before any gradation entry.
- Folding is a measurement step only — no fold type variety. Fold type (Book, Roof, etc.) belongs to the packing program.
- After folding: Tone & Finish Classification is a separate step. Tone and finish are two separate attributes. Samples sent to HO; factory worker enters after HO confirmation.
- Classification (tone/finish assignment) is distinct from Gradation (quality sorting during packing). Do not mix these terms.
- Gradation happens only as a byproduct of packing execution — no standalone grading step. Non-Fresh thaans are logged with grade during packing.
- All thaans are baled during regular packing — Fresh into dispatch-ready bales, non-Fresh into separate non-Fresh bales that sit at MIROLI-FG-OUT until a Todiya buyer is found
- Packing programs can pick rolls from different lots (cross-lot selection)
- Thaan is the tracked intermediate unit: Roll → Thaan (cut+fold) → Bale. One thaan = one source roll. Bale-to-thaan mapping tracked.
- Not Acceptable material is always measured in metres (never kg)
- Haste is the single customer/party identifier — no "Delivered to" vs "Haste" split in the system
- Customer returns are out of scope
- Packing slip generation = bale is dispatch-ready (no separate approval step)
- Decision Pending lots should be flagged for revisit after 14 days with no activity
- Transport is owned by RG Faith; vendor confirms readiness, RG Faith sends own vehicles
- Todiya is unpack + repack only — no re-cutting or re-folding. Original bale marked as unpacked, unchanged thaans repacked into new bale(s).
- Packaging materials are deferred to a future phase — not in current scope
- Tone/finish classification can be changed later with role-based authorization
- Code generation (FY prefix, vendor codes embedded) is noted for implementation time — not in solution design yet
- Dispatch is two-step: pickup scheduled → dispatched
