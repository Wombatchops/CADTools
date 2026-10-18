# CLAUDE.md — CADTools

Design Process single-file HTML tool. Follows the standard in [Wombatchops/Template](https://github.com/Wombatchops/Template): read its highest `docs/TEMPLATE_STANDARD_vN.md` and `template/DP_Tool_Template_vN.html` before changing this tool.

## Rules

- Work on the highest `CADTools_vN.html`. Each release: copy to `_v(N+1)`, bump `APP.version`, add a `VERSION_HISTORY` entry at the top, move the old file to `archive/`.
- Edit only the **1. TOOL CONFIG** block. The **2. TEMPLATE CORE** block must stay identical to the template version it came from (currently `DP_Tool_Template_v1`). Core changes go to the Template repo first.
- Components are defined once in `DEF` (section → page → subpage, each leaf has `c: { d, p, o, x, r }`). `NAV` and `PAGES` are generated from `DEF` — add a component there, not in `NAV`.
- Field shorthand: `'key|Label|unit'`; a select is `'key|Label||A/B/C'`. Keep keys stable once projects exist (saved items are keyed by them).
- Every table is a `DPTable`. No `alert` / `confirm` / `prompt` — use `DP.toast()` or the click-twice `armed()` pattern.
- Storage via `LS` only (try/catch). Never commit real project data.
- Supporting docs carry `_vN` (e.g. `docs/STRUCTURE_v1.md`). `README.md` and `CLAUDE.md` are the exception.
- Test in a browser before committing: every page renders, both nav layouts, add/update/delete item, option select/reject/iterate, save/duplicate, 390px width without sideways scroll.

## The user's preferences

- Direct, honest answers. Flag assumptions, gaps and anything not verified — especially engineering inputs and standards.
- If something isn't possible, give the logical path forward plus up to two alternatives.
- Versioned file names (`_vN`) for anything produced.
- End every reply with the date and time in the user's local time (AEST, Brisbane, UTC+10).
