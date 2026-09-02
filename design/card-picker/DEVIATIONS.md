# Card picker implementation deviations

Status: Finalized for the section 2a implementation.

This log uses the agreed conflict rule: the README controls behavior and the design markup controls values. A design-tool screenshot cannot show scrolling, focus, transitions, timing, or state changes, so those behaviors follow the README even when the static markup appears inert.

## Product and data decisions

| Source value or state | Implementation | Why |
| --- | --- | --- |
| The prototype catalog contains the 28 production entries plus 23 entries flagged `isNew` or `t2`. The populated 2a mock therefore shows 8 Chase tiles, 17 airline cards, and 4 Delta cards. | Only the 28 cards already backed by production rewards data ship. Chase has 6 production cards; the airline page has one United and one Southwest card; Delta currently ends in only its custom-card tile. | Explicit product decision: a card without trusted rewards data is worse than an absent card. Catalog expansion is separate work. |
| The prototype `BEST` map contains hand-written, unverified reward summaries. | `bestForCard()` derives every subtitle deterministically from the app's production rate table, point valuations, and category metadata. | Explicit product decision; no unproven rewards claims are shipped. |
| 66 source PNG card faces, generally about 1200 × 757 and averaging about 670 KB. | The production subset is encoded as transparent WebP at 112 px and 360 px wide, preserving the 1.586 aspect ratio. The 56 generated files total 392,406 bytes. | Explicitly approved optimization. All 56 outputs were probed as alpha-bearing `yuva420p`; extracted alpha planes contained both 0 and 255, confirming transparency survived. |
| The reference tree includes logos and art for proposed cards and unused historical screens. | Only the 14 logos and 28 card faces needed by the shipping catalog and the six 2a states are copied under `assets/card-picker/`. | Avoid shipping unused proposal assets while keeping the relocated design package intact as reference. |
| The existing persisted schema had no browse metadata for custom cards. | Schema version 4 stores `{issuer, brand, hotel, store, biz, other}` on each custom card. The editor exposes structured issuer/airline selects and category checkboxes; older custom cards migrate to `other: true`. | Explicit product decision so custom cards participate in browse filters exactly like catalog cards while preserving old local data. |

## Source conflicts and behavior

| Source value or state | Implementation | Why |
| --- | --- | --- |
| Airline chip markup says `overflow:hidden`; README says horizontally scrolling. | `overflow-x:auto`, hidden scrollbar, `-webkit-overflow-scrolling:touch`, horizontal overscroll containment, and focus-triggered `scrollIntoView`. The source bleed remains exactly `margin:4px -14px 0; padding:0 14px`. | Resolved in favor of README behavior. `flex:none` plus `white-space:nowrap` makes hidden overflow unreachable; the bleed geometry confirms a scrolling row was intended. |
| Prototype search data uses `.slice(0, 6)`; README intent is a six-row scrolling region. | All matches remain in the DOM in a `max-height:336px; overflow-y:auto` region. | Explicit clarification: six visible rows is a viewport limit, not a result cap. |
| The static typing frame always has a non-empty query. | Focusing an empty search keeps/restores the hub; typing swaps the held list and browse grid for results; Clear or Escape restores the hub. | README behavior and explicit clarification. |
| Static held rows show only content and a handle. | Clicking/tapping the rest of a row opens its rate editor; Remove lives inside that editor. The visible handle supports pointer drag plus Arrow Up/Down keyboard reorder with live announcements. | Explicit interaction decision. Opening the editor from the row is design-unspecified and therefore recorded here. Keyboard operation and announcements satisfy the repository's accessibility requirements. |
| Static sub-pages cannot show navigation motion. | Push and pop use 200 ms `cubic-bezier(.16,1,.3,1)`, 18 px horizontal travel, and opacity 0.5→1. | README behavior; numeric easing/travel details were design-unspecified. Reduced-motion preference collapses the duration to 0.01 ms. |
| Static toast is already visible and cannot dismiss. | The toast enters over 200 ms from 8 px below with a fade, stays for 4,000 ms, then dismisses. Undo removes the card even if the user has changed tabs. | README behavior and timing; the 8 px travel was design-unspecified. |
| Static selected airline chip cannot demonstrate state changes. | Tapping a brand filters in place; the selected chip includes the `✕`, applies the 1 px white logo backing, and tapping it or All clears the filter. | README behavior. Values and element order come from the markup. |
| The previous production UI pulsed the first card and displayed a long priority-coaching toast. | Both legacy coaching treatments are removed; the persistent “priority order breaks ties” hint is the only coaching. | README says nothing else animates, and the explicit product decision retired both treatments. |
| The README says section and airline group headings are 16 px/600, while the markup uses semantic `<h2>` elements with no weight override (computed 700). | Both headings are explicitly 16 px/700. | Value conflict resolved in favor of the markup, per the agreed rule. |

## Adaptive and accessibility additions

| Source value or state | Implementation | Why |
| --- | --- | --- |
| Search field is visually 42 px high. | A 44 px interactive shell contains a pseudo-element inset 1 px top/bottom, so the visible field remains exactly 42 px. In the focused layout, the shell margin is 9 px and the visible border starts at the source's 10 px position. | Preserve the source geometry while meeting the 44 × 44 minimum touch target. |
| The static typing mock draws a synthetic caret at 1.5 × 18 px with `vertical-align:-3px` and `margin-left:1px`. | The real search input uses the platform caret with `caret-color:#2563eb`; its width, height, and vertical metrics remain browser/OS controlled. | A synthetic caret would duplicate or replace native text-editing behavior. Color fidelity is retained while platform input behavior wins. |
| Several visible controls are smaller than 44 px: 20 px drag handle, 18 px clear button, text links, compact chips, 76 px-wide action pills, and the toast Undo label. | Invisible pseudo-elements enlarge their hit areas: handle `-8px -12px`, clear `-13px`, custom link `-15px -4px`, chips/actions `-7px 0`, prompt link `-12px -3px`, and Undo `-15px -7px`. | WCAG/touch-target adaptation; visible measurements are unchanged. |
| The design only specifies the search field's focus ring. | Other interactive controls use a 3 px `#2563eb` focus outline with 2 px offset; the focused scroll region uses a 3 px inset outline. | Keyboard accessibility; design-unspecified. |
| Header top padding is 54 px; tab-bar bottom padding is 28 px; toast bottom is 104 px. | At the 390 × 844 reference viewport those compute to exactly 54 px, 28 px, and 104 px. Safe-area forms are `max(54px, env(safe-area-inset-top))`, `max(28px, 7px + env(safe-area-inset-bottom))`, and `max(104px, nav-height + 22px)`. | Preserve reference values while avoiding notches, home indicators, or a taller wrapped navigation bar. |
| Toast uses `left:14px; right:14px`. | It is centered with `width:calc(100vw - 28px)` and capped at 532 px; at 390 px its measured bounds are exactly x=14…376. | Same reference geometry plus a restrained desktop width. |
| The reference is a fixed 390 px canvas and its presentation frame clips overflow. | App content scrolls vertically and remains centered with the repository's existing 560 px content cap on wider viewports. The 44 px device-frame radius, border, and shadow are not implemented. | The brief excludes the device frame from UI, and real content must remain reachable at every supported viewport and text zoom. |
| The design is only specified at 390 × 844 and has no 200% text-zoom state. | At an effective width ≤260 px: held/search art is hidden; held padding is 10 px; held gap is 4 px; edit gap is 8 px; search padding is 8 px; result gap is 6 px; action width is 60 px; browse is 2 columns; card grids are 1 column; heading hints wrap with a 38 px indent; toast art is hidden; nav items wrap at a 30% basis. | Prevent one-character wrapping and horizontal overflow at 200% zoom while retaining every action and label. These rules do not affect the 390 px reference screens. |
| The typing reference includes a 290 px-high stylized keyboard with 6 px row gaps, 5 px key gaps, and mock colors `#d1d5db`, `#ffffff`, `#aeb3bc`, and `#2563eb`. | The web app relies on the platform keyboard and does not render a keyboard facsimile. | The keyboard is operating-system chrome, not application UI; reproducing it would be incorrect and inaccessible. |

## Dark mode (all design-unspecified)

The 2a source defines only light mode. Every dark value below is therefore a deviation requiring separate visual review.

| Token / element | Dark implementation value | Reason |
| --- | --- | --- |
| Page background | `#0f1115` | Existing app dark foundation. |
| Surface | `#191c22` | Existing app dark surface. |
| Primary text | `#f3f4f6` | High contrast on page and surface. |
| Secondary text | `#aeb6c2` | High contrast while preserving hierarchy. |
| Placeholder text | `#7f8896` | 4.77:1 against the surface. |
| Standard border | `#626b78` | 3.16:1 against the surface, keeping boundaries visible without color alone. |
| Placeholder fill | `#22262e` | Distinct recessed surface. |
| Dashed placeholder border | `#697381` | 3.16:1 against its fill. |
| Accent | `#3b82f6` | 5.14:1 against the page background. |
| Accent hover | `#60a5fa` | Brighter interactive state. |
| Accent tint | `#1e2a4a` | Dark selected/illustration surface. |
| Accent on tint | `#a5b4fc` | 7.09:1 against the tint. |
| Accent on dark / Undo | `#bfdbfe` | 9.46:1 against the toast. |
| Success | `#34d399` | 8.88:1 against the surface. |
| Success fill | `rgba(52,211,153,.14)` | Low-emphasis success background. |
| Search highlight | `#5f4b16` | Primary text remains 7.62:1 on the highlight. |
| Toast fill | `#2a2f38` | Raised dark surface. |
| Toast text | `#f3f4f6` | High contrast on toast fill. |
| Header gradient color | `rgba(59,130,246,.12)` | Dark-mode blue glow. |
| App-icon shadow color | `rgba(59,130,246,.45)` | Visible shadow on dark background. |
| Search focus-ring color | `rgba(59,130,246,.24)` | Visible but translucent focus halo. |
| Search-clear fill | `#46505d` | Distinct compact control. |
| Search-clear text | `#f3f4f6` | High contrast on clear fill. |
| Inactive-nav fill | `rgba(174,182,194,.08)` | Low-emphasis pill. |
| Nav shadow | `rgba(0,0,0,.38)` | Separation from page content. |
| Active-nav shadow | `rgba(59,130,246,.38)` | Visible selected-state glow. |
| Selected-chip logo backing | `#ffffff` | Required white backing for airline logo legibility. |
| Toast shadow | `rgba(0,0,0,.45)` | Raised-surface separation. |
