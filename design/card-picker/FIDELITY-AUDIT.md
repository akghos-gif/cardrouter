# Card picker fidelity audit

Status: **Finalized.** Audited at a 390×844 CSS-pixel viewport against all seven reference
screens.

## Method and scope

- Every authored numeric or color-bearing CSS value in the seven UI screens is represented
  below. Repeated declarations are consolidated only when the semantic element and shipping
  selector are identical; the relevant screens are named in the element column.
- A shorthand, gradient, shadow, ratio, or transform is treated as one authored CSS value and
  is kept intact in the value column. Utility-like implementation rules are resolved to their
  computed px/hex values.
- `#fff` is normalized to `#ffffff`; `.10`, `.12`, and similar alpha spellings remain equivalent
  numeric values.
- The outer 390×844 reference size is audited. The 44px device radius, 1px device border,
  `0 20px 60px rgba(0,0,0,.12)` device shadow, and `#e9ebef` design canvas are excluded because
  the README explicitly calls the device frame presentation-only.
- The search screenshot's 290px keyboard, key colors, key radii, key-grid fractions, and key
  padding are excluded because the README explicitly calls that block a keyboard mock rather
  than UI.
- Each `MISMATCH` cites a corresponding entry in `DEVIATIONS.md`. There are no unexplained
  mismatches.

## Shared shell, header, title, and navigation

| design file value | element it came from | implementation value | file:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| 390px | all seven screen widths | 390px at audited viewport; responsive `width:100%` | index.html:303 | MATCH |
| 844px | all seven screen heights | 844px audited viewport; `100dvh` shell | index.html:249 | MATCH |
| `#f4f5f7` | page background, all screens | `#f4f5f7` | index.html:20 | MATCH |
| `#1a1d21` | primary text, all screens | `#1a1d21` | index.html:20 | MATCH |
| system font stack | all screen text | `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif` | index.html:45 | MATCH |
| `54px 18px 12px` | app-header padding, screens 1/1b | `max(54px, safe-area-top) 18px 12px`; 54/18/12 at audit size | index.html:233 | MATCH |
| 11px | app-header icon/copy gap | 11px | index.html:48 | MATCH |
| 42px × 42px | app icon | 42px × 42px | index.html:51 | MATCH |
| 11px | app-icon radius | 11px | index.html:51 | MATCH |
| `0 3px 10px rgba(37,99,235,.35)` | app-icon shadow | `0 3px 10px rgba(37,99,235,.35)` | index.html:26,235 | MATCH |
| `linear-gradient(180deg,rgba(37,99,235,.10),transparent)` | app-header background | same gradient | index.html:26,233 | MATCH |
| 20px | app-title size | 20px | index.html:53 | MATCH |
| 800 | app-title weight | 800 | index.html:53 | MATCH |
| -0.02em | app-title tracking | -0.02em | index.html:53 | MATCH |
| 1.1 | app-title line height | 1.1 | index.html:53 | MATCH |
| 12px | app subtitle | 12px | index.html:54 | MATCH |
| `#6b7280` | app subtitle color | `#69717f` | index.html:20,236 | MISMATCH (D08) |
| 1px | app subtitle top margin | 1px | index.html:54 | MATCH |
| `6px 18px 8px` | My cards title-row padding | `6px 18px 8px` | index.html:55 | MATCH |
| 8px | title/hint gap | 8px | index.html:55 | MATCH |
| 22px | screen title, every screen | 22px | index.html:57,313 | MATCH |
| 700 | screen-title weight | browser `<h1>` bold = 700 | index.html:57,313 | MATCH |
| -0.02em | screen-title tracking | -0.02em | index.html:57,313 | MATCH |
| 0 | screen-title margin | 0 | index.html:57,313 | MATCH |
| 13px | “order breaks ties” | 13px | index.html:58 | MATCH |
| `#6b7280` | title hint color | `#69717f` | index.html:20,255 | MISMATCH (D08) |
| 38px × 38px | header plus surface | 38px × 38px visual surface | index.html:256 | MATCH |
| 99px | header-plus radius | 99px | index.html:257 | MATCH |
| `#2563eb` | header-plus fill | `#2563eb` | index.html:23,257 | MATCH |
| `#ffffff` | header-plus glyph | `#ffffff` | index.html:257 | MATCH |
| 24px / 300 / 1 | header-plus glyph size/weight/line-height | 24px / 300 / 1 | index.html:258 | MATCH |
| `0 3px 10px rgba(37,99,235,.3)` | header-plus shadow | same | index.html:258 | MATCH |
| 0px | title-row plus padding/border | 0px | index.html:257 | MATCH |
| 44px × 44px | required plus hit target (not drawn in source) | 44px × 44px via 3px owned inset extension | index.html:260 | MISMATCH (D07) |
| `left:0; right:0; bottom:0` | tab-bar screen anchoring | left/right/bottom 0, fixed to viewport | index.html:90 | MATCH |
| 2px | tab-item gap | 2px | index.html:90 | MATCH |
| `#ffffff` | tab-bar surface | `#ffffff` | index.html:20,237 | MATCH |
| `1px solid #e5e7eb` | tab-bar top border | `1px solid #e5e7eb` | index.html:21,237 | MATCH |
| `7px 6px 28px` | tab-bar padding | 7px / 6px / 28px at audit viewport | index.html:238 | MATCH |
| `max(28px,7px + safe-area-bottom)` | device-safe tab padding (source has fixed 28px) | 28px in screenshots; larger only where device inset requires | index.html:238 | MISMATCH (D24) |
| `0 -6px 18px rgba(0,0,0,.08)` | tab-bar shadow | same | index.html:28,238 | MATCH |
| 10.5px / 600 | tab labels | 10.5px / 600 | index.html:93 | MATCH |
| 3px | tab icon/label gap | 3px | index.html:94 | MATCH |
| 54px × 30px | tab pill | 54px × 30px | index.html:95 | MATCH |
| 99px | tab-pill radius | 99px | index.html:96 | MATCH |
| 19px / 1 | tab glyph size/line-height | 19px / 1 | index.html:95 | MATCH |
| `rgba(125,125,125,.10)` | inactive-tab pill | same | index.html:28,240 | MATCH |
| `#6b7280` | inactive-tab label | `#69717f` | index.html:20,239 | MISMATCH (D08) |
| `1.5px solid transparent` | inactive-tab pill border | `1.5px solid transparent` | index.html:96 | MATCH |
| `grayscale(1)` | inactive-tab icon | `grayscale(1)` | index.html:98 | MATCH |
| 0.75 | inactive-tab opacity | 0.75 | index.html:98 | MATCH |
| `#2563eb` | active-tab label/border | `#2563eb` | index.html:22,241-242 | MATCH |
| `#eef2ff` | active-tab fill | `#eef2ff` | index.html:24,242 | MATCH |
| `0 1px 8px rgba(37,99,235,.28)` | active-tab shadow | same | index.html:29,242-243 | MATCH |
| `flex:1` | five equal tab items | `flex:1` | index.html:93 | MATCH |

## My cards and filter state (screens 1 and 1b)

| design file value | element it came from | implementation value | file:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `0 18px 2px` | filter-row padding | `0 18px 2px` | index.html:264 | MATCH |
| 6px | filter-chip gap | 6px | index.html:264 | MATCH |
| 0px | filter-row margin | -7px top/bottom, 0 horizontal | index.html:264 | MISMATCH (D05) |
| `overflow:hidden` | static filter row | `overflow-x:auto`; scrollbar width 0/hidden | index.html:264-266 | MISMATCH (D04) |
| `6px 11px` | unselected chip padding | `6px 11px` content inset | index.html:267 | MATCH |
| `1px solid #e5e7eb` | unselected chip surface border | `1px solid #e5e7eb` inset surface | index.html:21,270-271 | MATCH |
| `#ffffff` | unselected chip surface | `#ffffff` inset surface | index.html:20,270-271 | MATCH |
| 99px | chip radius | 99px | index.html:268,271 | MATCH |
| 13px / 500 | chip text | 13px / 500 | index.html:269 | MATCH |
| 6px | chip icon/text gap | 6px | index.html:267 | MATCH |
| 44px | actual chip target (source surface computes near 30px) | 44px target; 30px inset visual surface | index.html:267,270 | MISMATCH (D05) |
| 15px × 15px | chip issuer logo | 15px × 15px | index.html:276 | MATCH |
| 3px | chip-logo radius | 3px | index.html:276 | MATCH |
| 13px / 1 | category-chip glyph | 13px / 1 | index.html:278 | MATCH |
| `#1a1d21` / `1px solid #1a1d21` | selected-chip fill/border | `#1a1d21` / `1px solid #1a1d21` | index.html:20,275 | MATCH |
| `#ffffff` | selected-chip text | `#ffffff` | index.html:20,274 | MATCH |
| `6px 10px 6px 11px` | selected-chip padding | same content inset | index.html:274 | MATCH |
| 600 | selected-chip weight | 600 | index.html:274 | MATCH |
| 11px | selected-chip close glyph | 11px | index.html:279 | MATCH |
| 0.8 | selected-chip close opacity | 0.8 | index.html:279 | MATCH |
| 2px | selected-chip close left margin | 2px | index.html:279 | MATCH |
| 1px | selected-logo padding | 1px | index.html:277 | MATCH |
| `#ffffff` | selected-logo backing | `#ffffff` | index.html:29,277 | MATCH |
| 0.6 | unselected-chip opacity while filtered | 0.6 | index.html:273 | MATCH |
| `0 14px 100px` | held-list outer clearance | 0/14/100px non-iOS; 0/14/19px plus fixed-nav height on iOS | index.html:280,467 | MISMATCH (D19) |
| `8px 0` | held-list card margin | `8px 0` | index.html:281 | MATCH |
| `2px 16px 0` | held-list card padding | `2px 16px 0` | index.html:281 | MATCH |
| `#ffffff` | held-list surface | `#ffffff` | index.html:20,283 | MATCH |
| `1px solid #e5e7eb` | held-list border | same | index.html:21,282 | MATCH |
| 16px | held-list radius | 16px | index.html:282 | MATCH |
| `flex:1; min-height:0` | list fills remaining height | same computed flex/min-height | index.html:280-282 | MATCH |
| 11px | held-row gap | 11px | index.html:284 | MATCH |
| `11px 0` | held-row vertical padding | `11px 0` on row's edit target | index.html:287-289 | MATCH |
| `1px solid #e5e7eb` | held-row divider | same | index.html:21,285 | MATCH |
| 16px | priority-number column | 16px | index.html:287,290 | MATCH |
| 12px / 700 | priority number | 12px / 700 | index.html:290 | MATCH |
| `#6b7280` | priority-number color | `#69717f` | index.html:20,290 | MISMATCH (D08) |
| 58px × 37px | held card art | 58px × 37px | index.html:291 | MATCH |
| 5px | held-art radius | 5px | index.html:291 | MATCH |
| 14.5px / 600 | held card name | 14.5px / 600 | index.html:292 | MATCH |
| 12px | held best-for subtitle | 12px | index.html:293 | MATCH |
| 2px | held-subtitle top margin | 2px | index.html:293 | MATCH |
| `#6b7280` | held-subtitle color | `#69717f` | index.html:20,293 | MISMATCH (D08) |
| 16px | drag glyph box/size | 16px glyph inside a 44px button | index.html:294-296 | MISMATCH (D06) |
| -2px | drag-glyph tracking | -2px | index.html:295 | MATCH |
| `#9ca3af` | drag-glyph color | `#69717f` | index.html:21,295 | MISMATCH (D08) |
| 44px × 44px | actual reorder target (not expressed by mock) | 44px × 44px, no overlap with Edit | index.html:294 | MISMATCH (D06) |
| `12px 0` | list-footer padding | `12px 0` | index.html:299 | MATCH |
| 12px | list-footer size | 12px | index.html:299 | MATCH |
| `#9ca3af` | list-footer color | `#69717f` | index.html:21,299 | MISMATCH (D08) |

## Add a card hub (screen 2)

| design file value | element it came from | implementation value | file:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `52px 14px 0` | My cards back row | 52px top plus existing 14px main inset | index.html:306-308 | MATCH |
| 2px | back chevron/label gap | 2px | index.html:306 | MATCH |
| 16px | back-label text | 16px | index.html:307 | MATCH |
| `#2563eb` | back-label color | `#2563eb` | index.html:22,307 | MATCH |
| 26px / 1 / -3px | back glyph size/line-height/top offset | 26px / 1 / -3px | index.html:310 | MATCH |
| `4px 18px 4px` | Add title row | 4px vertical plus 14px main + 4px margin = 18px sides | index.html:311 | MATCH |
| `0 14px` | Add-page content sides | existing main 14px | index.html:59 | MATCH |
| 44px | search-field height | 44px | index.html:316 | MATCH |
| `0 12px` | search-field padding | `0 12px` | index.html:316 | MATCH |
| 8px | search icon/text gap | 8px | index.html:316 | MATCH |
| `#ffffff` | search surface | `#ffffff` | index.html:20,317 | MATCH |
| `1px solid #e5e7eb` | idle search border | same | index.html:21,317 | MATCH |
| 12px | search radius | 12px | index.html:317 | MATCH |
| 15px | search icon and placeholder | 15px | index.html:318,322,325 | MATCH |
| `#9ca3af` | search placeholder | `#69717f` | index.html:21,327 | MISMATCH (D08) |
| `16px 4px 8px` | OR BROWSE margin | `16px 4px 8px` | index.html:332 | MATCH |
| 12px / 600 | OR BROWSE type | 12px / 600 | index.html:332 | MATCH |
| 0.04em | OR BROWSE tracking | 0.04em | index.html:333 | MATCH |
| `#6b7280` | OR BROWSE color | `#69717f` | index.html:20,332 | MISMATCH (D08) |
| `repeat(3,1fr)` | browse-grid columns | `repeat(3,1fr)` | index.html:334 | MATCH |
| 7px | browse-grid gap | 7px | index.html:334 | MATCH |
| `12px 4px 10px` | browse-tile padding | same | index.html:335-337 | MATCH |
| 6px | browse-tile vertical gap | 6px | index.html:335 | MATCH |
| `#ffffff` | browse-tile surface | `#ffffff` | index.html:20,337 | MATCH |
| `1px solid #e5e7eb` | browse-tile border | same | index.html:21,336 | MATCH |
| 14px | browse-tile radius | 14px | index.html:336 | MATCH |
| 34px × 34px | browse logo/glyph disc | 34px × 34px | index.html:339-340 | MATCH |
| 7px | browse-logo radius | 7px | index.html:339 | MATCH |
| 99px | browse category-disc radius | 99px | index.html:341 | MATCH |
| `#eef2ff` / `#3730a3` | category-disc fill/glyph | `#eef2ff` / `#3730a3` | index.html:24,341 | MATCH |
| 18px | browse category glyph | 18px | index.html:341 | MATCH |
| 12.5px / 600 / 1.2 | browse-tile label | 12.5px / 600 / 1.2 | index.html:342 | MATCH |
| 12 source tiles | full static browse grid | 11 rendered today; empty Hotel hidden | index.html:1963-1969 | MISMATCH (D03) |
| `9px 0 0` | custom-row margin | `9px 0 0` | index.html:343 | MATCH |
| `13px 14px` | custom-row padding | `13px 14px` | index.html:343 | MATCH |
| 11px | custom-row gap | 11px | index.html:343 | MATCH |
| `#ffffff` / `1px solid #e5e7eb` / 14px | custom-row surface/border/radius | same | index.html:21,344 | MATCH |
| 38px × 26px | custom-row placeholder | 38px × 26px | index.html:347 | MATCH |
| 5px | custom-row placeholder radius | 5px | index.html:348 | MATCH |
| `1.5px dashed #9ca3af` | custom-row placeholder border | 1.5px dashed `#69717f` | index.html:21,348 | MISMATCH (D08) |
| 16px / 1 | custom-row plus glyph | 16px / 1 | index.html:348 | MATCH |
| `#6b7280` | custom-row plus/subtitle | `#69717f` | index.html:20,348,351 | MISMATCH (D08) |
| 14.5px / 600 / 1.2 | custom-row title | 14.5px / 600 / 1.2 | index.html:350 | MATCH |
| 12px / 1.25 | custom-row subtitle | 12px / 1.25 | index.html:351 | MATCH |
| 19px / 1 / `#9ca3af` | custom-row chevron | 19px / 1 / `#69717f` | index.html:352 | MISMATCH (D08) |

## Issuer and category shelves (screens 3 and 5)

| design file value | element it came from | implementation value | file:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `58px 14px 0` | Add a card back row | 58px top plus existing 14px main inset | index.html:306 | MATCH |
| `8px 18px 2px` | shelf heading | 8px/2px vertical plus 14px main + 4px margin = 18px sides | index.html:380 | MATCH |
| 10px | heading logo/title gap | 10px | index.html:380 | MATCH |
| 28px × 28px | issuer logo/category disc | 28px × 28px | index.html:381-383 | MATCH |
| 6px | issuer-logo radius | 6px | index.html:381 | MATCH |
| 99px | category-disc radius | 99px | index.html:383 | MATCH |
| `#eef2ff` / `#3730a3` | category-disc fill/glyph | same | index.html:24,383 | MATCH |
| 15px | category-page glyph | 15px | index.html:383 | MATCH |
| 28px | shelf-title line height | 28px | index.html:384 | MATCH |
| `0 18px 6px` | shelf count | 0/6 vertical plus 14px main + 4px margin = 18px sides | index.html:385 | MATCH |
| 13px | shelf-count text | 13px | index.html:385 | MATCH |
| `#6b7280` | shelf-count color | `#69717f` | index.html:20,385 | MISMATCH (D08) |
| `1fr 1fr` | shelf grid columns | `1fr 1fr` | index.html:386 | MATCH |
| 8px | shelf grid gap | 8px | index.html:386 | MATCH |
| 4px | shelf grid top margin | 4px | index.html:386 | MATCH |
| `0 14px` | shelf screen sides | existing main 14px | index.html:59 | MATCH |
| 8px | card-tile padding | 8px | index.html:387 | MATCH |
| 6px | card-tile content gap | 6px | index.html:387 | MATCH |
| `#ffffff` | card-tile surface | `#ffffff` | index.html:20,388 | MATCH |
| `1px solid #e5e7eb` | card-tile border | same | index.html:21,388 | MATCH |
| 14px | card-tile radius | 14px | index.html:388 | MATCH |
| 100% | shelf card-art width | 100% | index.html:389 | MATCH |
| 1.586 | card-art and custom-placeholder ratio | 1.586 | index.html:389-390 | MATCH |
| 7px | card-art and placeholder radius | 7px | index.html:389-391 | MATCH |
| 13px / 600 / 1.25 | card-tile name | 13px / 600 / 1.25 | index.html:395 | MATCH |
| 11.5px / 400 / 1.25 | best-for/sub-line | 11.5px / 400 / 1.25 | index.html:396 | MATCH |
| `#6b7280` | card sub-line | `#69717f` | index.html:20,396 | MISMATCH (D08) |
| `#eef0f3` | custom-card placeholder fill | `#eef0f3` | index.html:21,391 | MATCH |
| `1.5px dashed #c7cbd1` | custom-card placeholder border | same | index.html:22,391 | MATCH |
| 28px / 300 / 1 | custom-card plus | 28px / 300 / 1 | index.html:392 | MATCH |
| `#9ca3af` | custom-card plus | `#69717f` | index.html:21,392 | MISMATCH (D08) |
| `1px solid #2563eb` | Add/Create action border | same | index.html:22,365 | MATCH |
| `#2563eb` | Add/Create action text | `#2563eb` | index.html:22,366 | MATCH |
| 99px | Add/Create/status radius | 99px | index.html:363 | MATCH |
| `6px 0` | Add/Create/status vertical padding | `6px 0` visual surface | index.html:364 | MATCH |
| 13px / 600 | shelf action | 13px / 600 | index.html:364,368 | MATCH |
| `rgba(4,120,87,.12)` | held-card status fill | same | index.html:25,371 | MATCH |
| `#047857` | held-card status text | `#047857` | index.html:25,371 | MATCH |
| 12.5px / 600 | held-card status | 12.5px / 600 | index.html:364,372 | MATCH |
| 44px | Add/Create hit height (source visual is smaller) | at least 44px via 7px owned extension | index.html:369 | MISMATCH (D07) |

## Search results (screen 4)

| design file value | element it came from | implementation value | file:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `58px 14px 0` | searching-state back row | 58px plus existing 14px main inset | index.html:306 | MATCH |
| `6px 18px 6px` | searching-state title row | 6px vertical plus 14px main + 4px margin = 18px sides | index.html:312 | MATCH |
| `1.5px solid #2563eb` | focused search border | same | index.html:22,320 | MATCH |
| `0 0 0 3px rgba(37,99,235,.12)` | search focus ring | same | index.html:27,320 | MATCH |
| `#2563eb` | search caret | `caret-color:#2563eb` | index.html:22,324 | MATCH |
| 1.5px × 18px | mock caret geometry | native platform caret geometry | index.html:323-325 | MISMATCH (D23) |
| 18px × 18px | search clear surface | 18px × 18px | index.html:328 | MATCH |
| 99px | search-clear radius | 99px | index.html:328 | MATCH |
| `#d1d5db` / `#ffffff` | search-clear fill/glyph | `#d1d5db` / `#ffffff` | index.html:27,329 | MATCH |
| 11px / 18px | search-clear glyph/line-height | 11px / 18px | index.html:329 | MATCH |
| 44px × 44px | required clear target (source surface is 18px) | 44px × 44px via 13px owned extension | index.html:331 | MISMATCH (D07) |
| `#ffffff` | results-card surface | `#ffffff` | index.html:20,355 | MATCH |
| `1px solid #e5e7eb` | results-card border | same | index.html:21,355 | MATCH |
| 16px | results-card radius | 16px | index.html:355 | MATCH |
| `2px 14px` | results-card padding | `2px 14px` | index.html:354 | MATCH |
| 10px | results-card top margin | 10px | index.html:354 | MATCH |
| source content height | visible static rows | max-height 336px, all matches scroll | index.html:354 | MISMATCH (D10) |
| `9px 0` | result-row padding | `9px 0` | index.html:356 | MATCH |
| 10px | result-row gap | 10px | index.html:356 | MATCH |
| 54px computed | result-row minimum from 36px art + 18px padding | 54px minimum | index.html:356 | MATCH |
| `1px solid #e5e7eb` | result divider | same | index.html:21,357 | MATCH |
| 56px × 36px | search-result art | 56px × 36px | index.html:358 | MATCH |
| 5px | result-art radius | 5px | index.html:358 | MATCH |
| 14.5px / 600 | result name | 14.5px / 600 | index.html:360 | MATCH |
| `#fef3c7` | matched-text highlight | `#fef3c7` | index.html:25,361 | MATCH |
| 3px / 0px | match-highlight radius/padding | 3px / 0px | index.html:361 | MATCH |
| 12.5px | result best-for line | 12.5px | index.html:362 | MATCH |
| 1px | result best-for top margin | 1px | index.html:362 | MATCH |
| `#6b7280` | result best-for color | `#69717f` | index.html:20,362 | MISMATCH (D08) |
| 76px | result action width | 76px | index.html:367,373 | MATCH |
| 13.5px / 600 | result Add action | 13.5px / 600 | index.html:364,366 | MATCH |
| 12.5px / 600 | result Added status | 12.5px / 600 | index.html:364,372 | MATCH |
| `10px 4px` | custom-link exterior spacing | 0/4px margin + 10px vertical padding | index.html:376 | MISMATCH (D07) |
| 12.5px / `#2563eb` | custom-card link | 12.5px / `#2563eb` | index.html:22,377 | MATCH |
| 1.45 | custom-card link line height | 1.45 | index.html:377 | MATCH |
| 44px | custom-link target (not expressed by mock) | 44px minimum | index.html:376 | MISMATCH (D07) |
| 290px and keyboard colors/radii | grey keyboard mock | omitted; real platform keyboard | n/a | MISMATCH (D12) |

## Custom card step (screen 6)

| design file value | element it came from | implementation value | file:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `58px 14px 0` | custom back row | 58px plus existing 14px main inset | index.html:306 | MATCH |
| `8px 18px 2px` | custom title row | 8px/2px vertical plus 14px main + 4px margin = 18px sides | index.html:399 | MATCH |
| `0 14px` | custom-page sides | existing main 14px | index.html:59 | MATCH |
| 12px | identity/rates/action stack gap | 12px | index.html:400 | MATCH |
| `#ffffff` / `1px solid #e5e7eb` / 16px | identity and rates cards | same | index.html:20-21,401-402 | MATCH |
| 14px | form-card padding | 14px | index.html:401 | MATCH |
| 13px | identity-card internal gap | 13px | index.html:401 | MATCH |
| 11px | rates-card internal gap | 11px | index.html:403 | MATCH |
| 6px | field-label/control gap | 6px | index.html:404 | MATCH |
| 11.5px / 600 / 0.03em | uppercase field labels | 11.5px / 600 / 0.03em | index.html:405-406 | MATCH |
| `#6b7280` | field-label color | `#69717f` | index.html:20,405 | MISMATCH (D08) |
| 42px | card-name visual field | 42px inset surface inside 44px target | index.html:407-408 | MATCH |
| 44px | card-name target (source is 42px) | 44px | index.html:407,412 | MISMATCH (D16) |
| 11px | card-name/bank field radius | 11px | index.html:409,413 | MATCH |
| `0 12px` | card-name and bank side padding | 0/12px | index.html:412,418 | MATCH |
| 15px | card-name and bank text | 15px | index.html:414,418 | MATCH |
| `1.5px solid #2563eb` | focused card-name border | same | index.html:22,410 | MATCH |
| `0 0 0 3px rgba(37,99,235,.12)` | card-name focus ring | same | index.html:27,410 | MATCH |
| `#9ca3af` | card-name placeholder | `#69717f` | index.html:21,415 | MISMATCH (D08) |
| 1.5px × 18px | mock card-name caret | native platform caret geometry | index.html:412-415 | MISMATCH (D23) |
| 42px | bank visual field | 42px inset surface inside 44px target | index.html:407-409 | MATCH |
| 44px | bank target (source is 42px) | 44px | index.html:407,423 | MISMATCH (D16) |
| `1px solid #e5e7eb` | bank border | same | index.html:21,409 | MATCH |
| `#f9fafb` | bank fill | `#f9fafb` | index.html:20,416 | MATCH |
| 20px × 20px | bank logo | 20px × 20px | index.html:420 | MATCH |
| 4px | bank-logo radius | 4px | index.html:420 | MATCH |
| 8px | bank logo/name gap | 8px | index.html:419 | MATCH |
| 12px | bank hint | 12px | index.html:422 | MATCH |
| `#9ca3af` | bank hint | `#69717f` | index.html:21,422 | MISMATCH (D08) |
| 10px | rates-header label/action gap | 10px | index.html:425 | MATCH |
| 12.5px / 500 / `#2563eb` | Add a rate | 12.5px / 500 / `#2563eb` | index.html:22,426-427 | MATCH |
| 44px | Add-rate hit height (source is text-only) | 44px minimum with -12px visual margins | index.html:426 | MISMATCH (D07) |
| `#f4f5f7` / `1px solid #e5e7eb` / 10px | unit-toggle surface | same visible surface | index.html:20-21,428-430 | MATCH |
| 2px | unit-toggle horizontal inset | 2px | index.html:428 | MATCH |
| roughly 34px | unit-toggle drawn surface | 34px surface inside 44px targets | index.html:428-434 | MATCH |
| 44px | unit-segment target (source visual is roughly 34px) | 44px | index.html:431 | MISMATCH (D16) |
| 13px / 600 | active unit segment | 13px / 600 | index.html:432,435 | MATCH |
| `#ffffff` / 8px | active segment fill/radius | `#ffffff` / 8px | index.html:20,434-436 | MATCH |
| `0 1px 3px rgba(0,0,0,.10)` | active-segment shadow | same | index.html:436 | MATCH |
| 13px / 500 / `#6b7280` | inactive unit segment | 13px / 500 / `#69717f` | index.html:20,431-433 | MISMATCH (D08) |
| 8px | rate-row gap | 8px | index.html:438 | MATCH |
| 38px | category/value visual control height | 38px inset surface | index.html:439,442 | MATCH |
| 44px | category/value target (source is 38px) | 44px | index.html:438-439,446,452 | MISMATCH (D16) |
| 74px | reward-value box width | 74px | index.html:441 | MATCH |
| 10px | rate-control radius | 10px | index.html:443 | MATCH |
| `1px solid #e5e7eb` | idle rate-control border | same | index.html:21,443 | MATCH |
| `1.5px solid #2563eb` / 3px ring | focused rate controls (not shown in static screen) | same focus treatment as card name | index.html:444-445 | MISMATCH (D20) |
| `0 11px` | category-select side padding | 0/11px left, 28px right to clear arrow | index.html:446-448 | MATCH |
| 14px | category/value text | 14px | index.html:448,454 | MATCH |
| 12px / `#9ca3af` | category arrow | 12px / `#69717f` | index.html:21,449-451 | MISMATCH (D08) |
| 14px / 600 | populated reward value | 14px / 600 | index.html:452-454 | MATCH |
| 3px | value/suffix visual gap | approximately 3px at reference `1.5` value | index.html:452-458 | MATCH |
| 12.5px / 400 / `#6b7280` | rate suffix | 12.5px / inherited 400 / `#69717f` | index.html:20,457-458 | MISMATCH (D08) |
| `#9ca3af` | empty category/value placeholders | `#69717f` | index.html:21,451,455 | MISMATCH (D08) |
| 48px | Save button height | 48px | index.html:461 | MATCH |
| `#2563eb` / `#ffffff` | Save fill/text | `#2563eb` / `#ffffff` | index.html:23,462 | MATCH |
| 14px | Save radius | 14px | index.html:462 | MATCH |
| 15.5px / 600 | Save label | 15.5px / 600 | index.html:463 | MATCH |
| `0 3px 10px rgba(37,99,235,.3)` | Save shadow | same | index.html:463 | MATCH |
| source custom-form height | 42/38/roughly-34px control layout | roughly 22px taller from real 44px controls | index.html:407-463 | MISMATCH (D16) |

## Shipping behavior and data values that affect fidelity

| design file value | element it came from | implementation value | file:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| 28 cards | prototype production catalog | exactly the same 28 IDs, tested in the same picker order | index.html:859-864,1912-1914 | MATCH |
| BEST placeholder strings | all card subtitles | production `bestForCard()` strings | index.html:1386-1410,1948,1993,2054 | MISMATCH (D01) |
| roughly 1200×757 PNG | card-art source | transparent 112×71 and 360×227 WebP | index.html:1375-1380 | MISMATCH (D02) |
| 1.586 | required card-art aspect | 112/71 = 1.577 and 360/227 = 1.586 after integer rounding; CSS display ratio is exactly 1.586 | index.html:389 | MISMATCH (D02) |
| 6 visible result rows | search screenshot | 336px maximum region with every match retained | index.html:354,1989-1996 | MISMATCH (D10) |
| non-empty query in search screen | static search state | empty focus stays on browse; non-empty query enters results | index.html:1998-2015 | MISMATCH (D11) |
| no executable status action | `✓ In my cards` | non-focusable status/no-op | index.html:1982-1985 | MISMATCH (D15) |
| platform push/pop, unspecified numbers | page navigation | 200ms, 18px, opacity .5→1, cubic-bezier(.16,1,.3,1) | index.html:244-247,304-305 | MISMATCH (D13) |
| static row | held-card row | tap opens editor | index.html:2132-2137 | MISMATCH (D14) |
| static drag | held-row reordering | live midpoints; 44px edge zone; 10px/frame; pointer cancellation no-op | index.html:2143-2171 | MISMATCH (D20) |
| no live-region values | dynamic search/rate rows | result-count announcement and numbered rate-control names | index.html:2012-2013,2224-2227 | MISMATCH (D20) |
| three visible custom-form concepts | custom page | name, bank, rates only; metadata defaults null/false in model | index.html:2278,2291-2305 | MATCH |

## Dark mode (design-unspecified)

The reference has no dark screens. Every shipping dark value is therefore a deliberate,
reviewable mismatch under D09 rather than a claim of fidelity.

| design file value | element it came from | implementation value | file:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| unspecified | page background | `#0f1115` | index.html:34 | MISMATCH (D09) |
| unspecified | surface | `#191c22` | index.html:34 | MISMATCH (D09) |
| unspecified | alternate field | `#20242b` | index.html:34 | MISMATCH (D09) |
| unspecified | primary text | `#f3f4f6` | index.html:34 | MISMATCH (D09) |
| unspecified | secondary text | `#aeb6c2` | index.html:34 | MISMATCH (D09) |
| unspecified | placeholder text | `#818b99` | index.html:35 | MISMATCH (D09) |
| unspecified | standard border | `#626b78` | index.html:35 | MISMATCH (D09) |
| unspecified | placeholder fill/border | `#22262e` / `#697381` | index.html:35-36 | MISMATCH (D09) |
| unspecified | accent/hover | `#3b82f6` / `#60a5fa` | index.html:36 | MISMATCH (D09) |
| unspecified | primary/hover | `#1d4ed8` / `#2563eb` | index.html:37 | MISMATCH (D09) |
| unspecified | accent tint/on-tint | `#1e2a4a` / `#a5b4fc` | index.html:38 | MISMATCH (D09) |
| unspecified | success/fill | `#34d399` / `rgba(52,211,153,.14)` | index.html:39 | MISMATCH (D09) |
| unspecified | search highlight | `#5f4b16` | index.html:39 | MISMATCH (D09) |
| unspecified | header glow/logo shadow | `rgba(59,130,246,.12)` / `rgba(59,130,246,.45)` | index.html:40 | MISMATCH (D09) |
| unspecified | focus ring | `rgba(59,130,246,.24)` | index.html:41 | MISMATCH (D09) |
| unspecified | search clear fill/text | `#46505d` / `#f3f4f6` | index.html:41 | MISMATCH (D09) |
| unspecified | inactive-nav fill/nav shadow | `rgba(174,182,194,.08)` / `rgba(0,0,0,.38)` | index.html:42 | MISMATCH (D09) |
| unspecified | active-nav shadow/logo backing | `rgba(59,130,246,.38)` / `#ffffff` | index.html:43 | MISMATCH (D09) |

## Rendered structural comparison at 390×844

| reference screenshot | comparison result | structural differences |
| --- | --- | --- |
| `1-my-cards-tab.png` | Same header, title/hint baseline, horizontally scrolling chips, ordered seven-row shelf, footer, and anchored five-item nav. | Production-derived subtitles wrap differently from BEST placeholders (D01). Secondary/tertiary text is slightly darker (D08). The 44px chip targets preserve the visible pill position via inset surfaces (D05). |
| `1b-chip-filter-on.png` | Same active chip with white logo backing/✕, muted peers, retained priorities 1/4/5/6, hidden drag controls, and filtered footer. | Same D01/D05/D08 differences as screen 1. |
| `2-add-a-card.png` | Same pushed-page order: back, title, search, browse heading/grid, custom row, nav. | Hotel is absent because the production shelf is empty, leaving eleven tiles (D03). |
| `3-chase-issuer-page.png` | Same issuer heading/count, two-column card grid, held statuses, actions, and custom issuer tile last. | Only the production-derived subtitle copy/wrapping differs (D01); status remains a no-op (D15). |
| `4-search-results.png` | Same focused search, result row structure, highlighting, fixed-width actions, and custom link. | Real native caret (D23), all results in a scrolling six-row region (D10), and real keyboard instead of mock (D12). |
| `5-business-cards-page.png` | Same generic category pattern, five production Business cards, and Custom last. | Production-derived subtitle copy/wrapping differs (D01). |
| `6-custom-card-step.png` | Same stack and ordering: back, title, identity card, earn-rates card, primary action; no metadata controls. | Form is roughly 22px taller because interactive controls have 44px targets while their inset surfaces preserve the drawn 42/38/roughly-34px sizes (D16). Native caret differs from the mock (D23). |

No screen produced document-level horizontal overflow at 390px, 320px, desktop 1280px, or
a 195px CSS viewport (390px phone at 200% browser zoom). The seven-screen interaction and
persistence suite passes in the browser; final result is recorded in the implementation handoff.
