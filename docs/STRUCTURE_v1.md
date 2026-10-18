# CADTools structure — v1

Source: `docs/CADAI_Notes_v1.pdf` (handwritten-list notes, 17 Oct 2026). This file records how each note was mapped and what still needs a decision.

## 1. Navigation

| Section | Pages › sub-pages | From the notes |
|---|---|---|
| **Project** | Overview · Project info · Saved projects · Settings | "Ability to save project information / reuse and duplicate for new project" |
| **Earthworks** | Culverts & headwalls › RCP culvert, RBC culvert · Workshop & sheds · Stockpiles › Geometry, Live volume (bottom reclaim) · Turkey nest dams | Earthworks list |
| **Concrete** | Footings & pedestals · Drive-in sumps · Floor sumps · HD bolt geometry | Concrete list |
| **Structural** | Conveyor trestles · Conveyor gantries · Stair flights & towers · Ladders · Step ladders · Sump pump frame · Swing gates & handrails | Structural list |
| **Mechanical** | Sump pumps · Warman pumps · Pump hoppers › Square, Cylindrical, Tapered bottom, Conical · Tanks › Shell & baffles, Agitator platform, HD geometry, Hatches & manways, Roof, Clean-out doors · Conveyors › Profile & datasheet, Head chute, Head frame, Tail frame, Gravity take-up, Drive geometry, Pulleys & drive · Thickeners & underflow pumps · Reagent mix & storage | Mechanical list |
| **Process Equipment** | Gravity launders · Flotation cells · Grinding & milling › SAG mill, Ball mill · Classification › Cyclones · Wet screens › Feedbox, Oversize chute · ROM bin › ROM bin, Static grizzly, Hungry boards · Mill discharge hopper | Un-headed list after Mechanical (see 3a) |
| **Multi-discipline** | Sump, pump & frame · ROM bin, grizzly & hungry board | Multi-discipline list — assemblies that reference items from other registers |
| **Piping** | Pump suction · Hydrants · Sharkfin samplers library | Piping list |
| **Electrical** | Switchroom · Transformers · Cable tray › Block library, AutoCAD script · Lights · Control panels · Light & power reticulation · BESS farm | Electrical list |
| **Layout** | Dry plant · Stockpile & reclaim · Grinding · Conveyors · CIL · Thickeners · Reagents · Camp sizing · Asset library | Layout list |
| **Study Model** | Options register › All, Proposed, Selected, Rejected · Review & decide · Iterate | "In study model…" paragraph |

## 2. Each component page

Inputs (proposed) → Item register (`DPTable`, CSV) → Outputs (planned) → Exports (planned) → References & notes.

## 3. Assumptions to confirm

a. **Process Equipment** — the notes list gravity launder → mill discharge hopper with no heading after "Mechanical … With options". I put them in a new *Process Equipment* section rather than making Mechanical 20+ pages. Easy to move back.
b. **"Swing doors handrails"** — read as self-closing swing gates in handrails.
c. **Tanks** — "baffles and agitator platforms, HD geometry, inspection hatches, roofs, manways, clean-out doors" split into six sub-pages of one tank.
d. **Pump hoppers** — "square, cylindrical tapered bottom, conical" read as four types: square, cylindrical, cylindrical with tapered bottom, conical. If "cylindrical tapered bottom" was one type, drop *Cylindrical*.
e. **Reagents "with options"** — implemented as an Option field on the reagent page plus Layout › Reagents in the Study Model.
f. **Asset library** — v1 stores references (path / URL) only. Storing the drawings / models themselves needs file storage (see 5).
g. **Camp** placed under Layout (as in the notes) with its own sizing inputs.
h. **Standards** named in references (AS 1657, AS 2419.1, AS/NZS 1680, AS 1940, AS 3780, AS 1755, CEMA / ISO 5048) are from general knowledge, **not verified** for current edition or applicability. Confirm before any check is built.

## 4. Template fit

| Need | Fits template? | What v1 did | Proposed template extension |
|---|---|---|---|
| Navigation, header, tables | Yes | Used as-is | — |
| Input forms | **No form component** | Inline-styled label/input grid in the tool config | Add `.dp-form` / `.dp-field` (label + unit + input) to TEMPLATE CORE |
| Confirm before delete | Template bans `confirm()` | Click-twice within 4 s (`armed()`) + toast | Add a `DP.confirm(msg, onYes)` in-page panel to CORE |
| Header text length | Long pills wrap the header | Shortened labels; full name in tooltip | Optional `maxWidth` + ellipsis on `.hpill` |
| Project / file persistence | Template only stores UI state | Project JSON in `localStorage` + Export / Open | Shared `DP.project` save / open / export helper if other tools need it |
| Row click → edit form | `DPTable` has no row-click hook | Item picker dropdown above the form | `onRowClick(row)` option on `DPTable` |

## 5. Roadmap (proposed)

1. Pick 2–3 pilot components (suggest: Stockpile geometry + live volume, HD bolt geometry, Stair flights) and build the calcs with worked-example checks.
2. Output to AutoCAD: generate `.scr` scripts in the browser (works in any AutoCAD, no add-ins). Alternatives: DXF written directly (no AutoCAD needed to create, opens in AutoCAD / BricsCAD / Revit), or Python via pyautocad (needs Windows + full AutoCAD running).
3. Datasheet PDF per item (print stylesheet first; jsPDF if a fixed layout is needed).
4. Study Model generation: today options are logged by the designer. Automatic layout options need either rule-based placement in the tool or an AI step via the Claude API from a separate script / artifact — to scope once components have real geometry.
5. Project storage beyond one browser: JSON files in a project folder or GitHub (now), shared artifact storage or SharePoint (later).
