# Project Configuration

## Project Description

Factory-level inventory tracking system for RG Faith Creations Pvt. Ltd. at their Miroli facility in Ahmedabad. The system tracks grey material, packaging material, and material at each processing stage (grey → folding → grading → packing → finished goods) with quantities in meters or kg. No financial data tracking. Independent system with future import/export utility for head office ERP.

## Domain Glossary

| Term | Definition |
|---|---|
| Miroli | RG Faith's processing facility — all operations happen here |
| MRL No | Miroli lot number — round-trip tracking ID assigned when sending goods to vendor for dyeing; vendor references it on return |
| Avak | Incoming/arrival — "Avak Date" = date material arrived at Miroli |
| Grey | Default classification of incoming fabric; ungraded/unprocessed state |
| Fresh | Highest quality grade — good quality fabric, measured in meters |
| Good Cut | Second quality grade, measured in kg (converted via Chadat) |
| Fent | Lower quality grade, measured in kg |
| Rags | Lower quality grade, measured in kg |
| Chindi | Lowest quality grade, 100% loss, measured in kg |
| Chadat | Conversion factor between meters and kg for a specific lot |
| Thaan | A piece of fabric (= "piece") |
| Haste | "For [party name]" — indicates which customer/party goods are destined for |
| Todiya / Toria | Breaking/reassigning inventory — now mostly a software operation for repacking accumulated leftovers. "Todiya" is the primary spelling used. |
| Gate Pass | Inbound reference document from the mill, accompanies the truck |
| SSTM | Shree Shubhlaxmi Textile Mills — primary brand name (~90%) under RG Faith |
| Bale | Final packed unit — cardboard box with plastic layers, stickers, brand stamps, thread |
| Packing Program | Instruction document specifying how to cut, fold, brand, and pack a lot. Three triggers: sales order (~95%), proactive inventory advancement (~5%), Todiya (leftovers). |
| Gradation Report | Progressive report showing yield analysis — Fresh % vs losses, shrinkage tracking |
| Trade Number | Finished product SKU reference assigned at packing time (e.g., S8072-58") |
| Fold Type | How fabric is folded during packing (Book, Roof, 2Fold, B1F, etc.) — user-configurable terminology |
| GRN | Goods Receipt Note — record of packaging materials received from vendors |
| GSM | Grams per Square Metre — fabric weight/density attribute on incoming cloth |
| Decision Pending | Inventory state for lots where quality is unclear and grading decision has not been made. Should be revisited if no activity for 14 days. |
| Fresh Pending | Graded Fresh material not yet assigned to a packing program — awaiting packing. |
| Reprocess List | Register tracking Not Acceptable material pending return to vendor |
| Cutting No | Identifier for individual packing programs when multiple appear on one physical form (Cutting No 1, 2, 3 = separate programs) |
| F.H. | Folding House — refers to the folding/grading area at Miroli. Appears on Gradation Report fields (e.g., F.H. Avak Mtrs, F.H. Fold Mtrs). |
| O1W | Off-White (tone code) |
| Not Acceptable | Rejected material — always measured in metres. Tracked on Reprocess List for vendor return. |

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
- Use "grey" spelling (not "gray")
- System is independent from head office ERP — future import/export utility only
- Master data (brands, products, fold types, tone codes, quality codes, SKU attributes) must be user-configurable
- Chadat is the conversion bridge between meters (Fresh) and kg (all other grades)
- Folding and grading are independent activities — no enforced sequence between them
- Regular packing programs use Fresh only; Good Cut and below always go to accumulation → Todiya
- Not Acceptable material is always measured in metres (never kg)
- Haste is the single customer/party identifier — no "Delivered to" vs "Haste" split in the system
- Customer returns are out of scope
- Packing slip generation = bale is dispatch-ready (no separate approval step)
- Decision Pending lots should be flagged for revisit after 14 days with no activity
- Transport is owned by RG Faith; vendor confirms readiness, RG Faith sends own vehicles
