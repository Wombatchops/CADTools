# CADTools

Single-file HTML tool for parametric plant CAD components and layout studies — Design Process.

**Current version:** [`CADTools_v1.html`](CADTools_v1.html) — open it in any browser. No install, no build.

Built on the Design Process tool template ([Wombatchops/Template](https://github.com/Wombatchops/Template), `DP_Tool_Template_v1.html`). Only the **1. TOOL CONFIG** block was changed; the **2. TEMPLATE CORE** block is a verbatim copy.

## What v1 is

v1 is the **structure release**. It gives:

- **Navigation** for every item in the CADAI notes ([`docs/CADAI_Notes_v1.pdf`](docs/CADAI_Notes_v1.pdf)): 11 sections, 57 pages, 71 component pages. Default layout: Vertical.
- **A page per component** with a *proposed* input set, an item register (standard `DPTable`, CSV export), and the planned outputs and exports.
- **Projects**: working copy kept in the browser; **Save** stores a revision in the browser's project library; **Export** downloads `CADTools_<job>_vN.json`; **Open** loads one back; **Saved projects** reopens or duplicates a job for a new project.
- **Study Model**: option register per area, select one or more options, reject with notes and a required reason, create the next iteration from feedback.

**Not built yet:** calculations, drawings, DXF / AutoCAD script output, datasheets, automatic layout generation. Every input list is a proposal to review — nothing is engineering-checked.

Section-by-section mapping and open questions: [`docs/STRUCTURE_v1.md`](docs/STRUCTURE_v1.md).

## Header

| Item | Type | Colour | Does |
|---|---|---|---|
| Project · rev | pill | amber when unsaved | Current project, revision, unsaved flag |
| items · opts | pill | — | Item and option counts |
| New | button | ghost | Blank project (double-click within 4 s if unsaved) |
| Open | button | ghost | Load a CADTools project JSON |
| Export | button | blue (steel) | Download project JSON |
| Save | button | orange (amber) | Save a revision to the browser library |
| Nav | switch | — | Horizontal / Vertical (template standard) |

## Data

- Kept in browser `localStorage` under the `dpCADTools.` prefix. A different browser, PC or private window will not see it. **Export** for a durable copy.
- No real project data is committed to this repo.

## Releases

Copy to `CADTools_v(N+1).html`, bump `APP.version`, add a `VERSION_HISTORY` entry; move the old file to `archive/`.
