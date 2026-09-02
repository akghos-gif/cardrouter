# Handoff: Add-a-card picker redesign (ChooseMyCard)

## Overview
Replaces the old "add a card" experience — one long alphabetical list of every supported
credit card — with a hub-and-browse flow that lives directly in the **My cards** tab:
a search field plus a 12-tile browse grid (7 issuers + Hotel / Airline / Store / Business + Other).
Tapping a tile opens a sub-page of card tiles showing real card art; adding a card returns the
user to the sub-page with a confirmation toast, so multiple cards can be added in a row.

The approved direction is **2a** (top section of the design file). Section 1a below it is the
earlier exploration, kept for history — **implement 2a only**.

## About the design files
The files in `design/` are **design references created in HTML** — prototypes showing intended
look and behavior, not production code to copy. The task is to recreate these screens in the
target codebase using its existing environment, component library, and patterns (if no app
environment exists yet, pick the appropriate framework for the platform and build them there).
The markup is a design-tool format (inline styles, `<sc-for>` / `<sc-if>` template tags); treat it
as a spec of structure and values, not as source to port.

## Fidelity
**High fidelity.** Colors, typography, spacing, radii, and copy are final. Card art and brand
logos are final assets. Recreate the UI closely, substituting the codebase's own primitives
(buttons, list rows, sheets) where they already exist.

## Screens

All screens are specified at a 390 × 844 pt viewport (iPhone 14/15 class). The design file wraps
each screen in a 44px-radius device frame — that frame is presentation only, not part of the UI.

### 1. My cards hub (`2a-1`)
The redesign lives in this existing tab. Top to bottom:

1. **App header** — 54px top padding, 18px sides, 12px bottom; app icon 42 × 42, radius 11,
   shadow `0 3px 10px rgba(37,99,235,.35)`; title "ChooseMyCard" 20px/800, `-0.02em`;
   subtitle "your rewards butler" 12px `#6b7280`. Background
   `linear-gradient(180deg, rgba(37,99,235,.10), transparent)`.
2. **Section title** — `My cards` 22px/700 `-0.02em`, with inline hint
   "priority order breaks ties" 13px `#6b7280`.
3. **Held cards list** — white card, 1px `#e5e7eb`, radius 16, side padding 14.
   Each row: 7px vertical padding, 1px bottom divider, 10px gap;
   priority number (20px wide, 12px/700, `#6b7280`, centered) · card art 44 × 28 radius 4
   `object-fit:cover` · name 14.5px/600 · **best-for line 12.5px `#6b7280`** · drag handle `⋮⋮`
   16px `#9ca3af`. Rows are drag-reorderable; order sets tie-break priority.
4. **"Add a card" row** — heading 16px/600, right-aligned link `+ Custom card` 13px `#2563eb`.
5. **Search field** — 42px tall, white, 1px `#e5e7eb`, radius 12, 12px side padding, 8px gap,
   magnifier glyph, placeholder "Search cards, banks, airlines…" 15px `#9ca3af`.
6. **Browse grid** — `repeat(3, 1fr)`, 7px gap. Tile: white, 1px `#e5e7eb`, radius 14,
   padding `12px 4px 10px`, column flex, 6px gap, centered; brand logo 34 × 34
   `object-fit:contain` radius 7; label 12.5px/600 centered, line-height 1.2. No card counts.
   Tile order: **Chase, Amex, Citi, Capital One, Discover, US Bank, Wells Fargo,
   Airline cards, Hotel cards, Store cards, Business cards, Other** — "Other" is always last
   and uses an `…` glyph in a 34px `#eef2ff` circle with `#3730a3` text (same treatment for the
   four category tiles' emoji glyphs).
7. **Tab bar** — 5 items (Which card?, My cards, Benefits, Promos, Settings), white,
   1px top border `#e5e7eb`, padding `7px 6px 28px`, shadow `0 -6px 18px rgba(0,0,0,.08)`.
   Active item: label `#2563eb` 10.5px/600, pill 54 × 30 radius 99 `#eef2ff`, 1.5px `#2563eb`
   border, shadow `0 1px 8px rgba(37,99,235,.28)`. Inactive: `#6b7280`, pill
   `rgba(125,125,125,.10)`, `filter:grayscale(1)`, `opacity:.75`.

### 2. Search / typing (`2a-2`)
Focusing the search field **hides the held-cards list and the browse grid** and shows results;
the keyboard is up.

- Focused field: 1.5px `#2563eb`, radius 12, focus ring `0 0 0 3px rgba(37,99,235,.12)`,
  caret 1.5px `#2563eb`, trailing ✕ in an 18px `#d1d5db` circle. Tapping ✕ clears the query and
  restores the held list + grid.
- Result rows in a white radius-16 card: card art 56 × 36 radius 5 · name 14.5px/600 with the
  matched substring highlighted `background:#fef3c7` radius 3 · best-for line 12.5px `#6b7280` ·
  trailing action. Matching is a case-insensitive substring match on the card name; cap the
  visible list at 6 with scroll.
- **Action buttons share one width (76px, `box-sizing:border-box`)** so rows don't reflow
  when a card is added: `Add` = 1px `#2563eb`, `#2563eb`, 13.5px/600, radius 99, 6px vertical;
  `✓ Added` = `rgba(4,120,87,.12)` fill, `#047857`, 12.5px/600, same box.
- Below the list: "Not listed? **Create a custom card** named “<query>”." 13px `#6b7280`,
  link `#2563eb`, pre-filling the typed text as the card name.

### 3. Issuer sub-page (`2a-3`, Chase shown)
- Back affordance `‹ My cards` 16px `#2563eb`, 58px top padding.
- **Header: issuer logo 28 × 28 radius 6 + title "Add a Chase card"** 22px/700 `-0.02em`,
  `line-height:28px` so it optically centers against the logo. The explicit "Add a…" verb is
  required — without it the page reads as a list of cards the user already owns.
- **Card grid** — 2 columns, 8px gap. Tile: white, 1px `#e5e7eb`, radius 14, padding 8,
  column flex, 7px gap; card art `width:100%`, `aspect-ratio:1.586`, radius 7, `object-fit:cover`;
  name 13px/600 line-height 1.25; action pinned to the bottom of the tile (`margin-top:auto`)
  so actions align across a row regardless of name length.
- Cards the user already holds **stay in the grid** and show `✓ In my cards`
  (`rgba(4,120,87,.12)` / `#047857`, 12.5px/600, radius 99) instead of `Add`
  (1px `#2563eb`, 13px/600) — so the user isn't confused looking for a card they've added.
- **Last tile is always "Custom <issuer> card"**, styled as a card tile with a placeholder in
  place of the art: `#eef0f3` fill, 1.5px dashed `#c7cbd1`, radius 7, same 1.586 aspect ratio,
  centered `+` 28px `#9ca3af`; name "Custom Chase card" with sub-line
  "not listed? issuer pre-filled" 11.5px `#6b7280`; button label `Create`. Opening it takes the
  user to the custom-card form with the issuer already set.

Sub-pages exist for each issuer tile (Chase, Amex, Citi, Capital One, Discover, US Bank,
Wells Fargo, Other) and for Hotel / Store / Business, all using this identical pattern.

### 4. After tapping Add (`2a-4`)
Same page; the tapped card's button flips to `✓ In my cards` in place, and a toast appears
above the tab bar: `left/right:14px`, `bottom:104px`, `#1a1d21` fill, `#f4f5f7` text, padding
`12px 14px`, radius 14, shadow `0 8px 24px rgba(0,0,0,.25)`; card art 40 × 26 radius 3, message
**"Freedom Flex added"** 14px, trailing `Undo` `#93c5fd` 13px/600. Auto-dismiss ~4s; `Undo`
removes the card and restores the `Add` button. Keep the message to the short form — no card
count, no priority explanation.

### 5. Airline cards (`2a-5`)
There is **no brand-selection step**. The page lists every airline card, grouped by airline.

- Header "Add an airline card" + hint "grouped by airline".
- **Jump chips** — horizontally scrolling row, 6px gap, bleeding to the screen edges
  (`margin:4px -14px 0; padding:0 14px`). `All` chip active by default: `#1a1d21` fill,
  white text, radius 99, padding `5px 12px`, 13px/600. Brand chips: white, 1px `#e5e7eb`,
  padding `5px 11px 5px 6px`, 13px/500, with an 18 × 18 `object-fit:contain` logo, radius 4.
- **Group headers** — airline logo 22 × 22 radius 5, name 16px/600, and a
  "<program> · <issuing bank>" sub-line 12.5px `#6b7280` (e.g. "Delta SkyMiles · Amex"),
  margins `14px 4px 6px`. Cards below in the same 2-column tile grid as issuer pages.

### 6. Airline chip selected (`2a-6`, Delta)
Tapping a brand chip filters in place — it does not navigate.

- Header hint becomes "filtered to Delta". The `All` chip drops to the inactive style; the
  selected chip becomes `#1a1d21` fill / white text with a trailing ✕ (11px, `opacity:.8`)
  that clears the filter; its logo gets a white 1px-padded background so it stays legible on
  dark. Unselected chips render at `opacity:.6`.
- Only the selected airline's group renders, ending in the **"Custom Delta card"** tile
  (same card-shaped treatment as the issuer pages, sub-line "not listed? airline pre-filled").

## Interactions & behavior
| Trigger | Result |
| --- | --- |
| Focus search field | Hide held list + browse grid, show live results, raise keyboard |
| Tap ✕ in search | Clear query, restore held list + browse grid |
| Type | Case-insensitive substring match on card name; highlight the match; max 6 visible |
| Tap browse tile | Push issuer / category sub-page |
| Tap `Add` | Append card to My cards (lowest priority), flip button to `✓ In my cards`, show toast |
| Tap `Undo` in toast | Remove the card, restore `Add` |
| Tap `✓ In my cards` | No-op (or navigate to that card in My cards) |
| Tap brand chip (airline page) | Filter in place to that airline; chip gains ✕ |
| Tap `All` or chip ✕ | Clear the filter |
| Tap `Create` on a custom tile | Open custom-card form with issuer or airline pre-filled |
| Tap `+ Custom card` on hub | Open custom-card form, nothing pre-filled |
| Drag a held row | Reorder priority |
| Tap `‹ My cards` | Pop back to the hub |

Motion: standard platform push/pop for sub-pages; toast slides up and fades
(~200ms ease-out, ~4s dwell). Nothing else animates.

## State
- `heldCards: string[]` — ordered card ids; order **is** the tie-break priority.
- `query: string` — search text; empty means "show held list + browse grid".
- `route` — `hub` | `{issuer}` | `airline` | `hotel` | `store` | `business` | `other` | `custom`.
- `airlineFilter: string | null` — selected airline on the airline page.
- `toast: {cardId, timerId} | null` — supports Undo.
- Card catalog is static app data (see below); no fetch is required for this flow.

## Design tokens
Colors
- Page background `#f4f5f7`; canvas behind device frames `#e9ebef`
- Surface `#ffffff`; border `#e5e7eb`; dashed placeholder border `#c7cbd1`;
  placeholder fill `#eef0f3`
- Text primary `#1a1d21`; secondary `#6b7280`; placeholder `#9ca3af`
- Accent / links `#2563eb` (hover `#1d4ed8`); accent tint `#eef2ff`; accent-on-tint `#3730a3`;
  accent-on-dark `#93c5fd`
- Success `#047857` on `rgba(4,120,87,.12)`
- Search highlight `#fef3c7`
- Keyboard mock `#d1d5db` / keys `#ffffff` / modifiers `#aeb3bc`

Type — system stack (`-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`)
- App title 20/800 `-0.02em` · Screen title 22/700 `-0.02em` · Section 16/600
- List row name 14.5/600 · secondary 12.5/400 · tile name 13/600 (1.25)
- Body/field 15 · hint 13 · micro 11.5–12 · tab label 10.5/600

Spacing — screen side padding 14 (18 for headers); grid gaps 7 (hub) / 8 (cards);
tile padding 8; list row padding 7–9 vertical.

Radii — 44 device frame · 16 list card · 14 tile · 12 field · 7 card art ·
5–6 logo · 99 pill.

Shadows — device `0 20px 60px rgba(0,0,0,.12)` · tab bar `0 -6px 18px rgba(0,0,0,.08)` ·
toast `0 8px 24px rgba(0,0,0,.25)` · focus ring `0 0 0 3px rgba(37,99,235,.12)`.

Card art aspect ratio: **1.586** (ISO/IEC 7810 ID-1).

## Assets
`design/assets/` — all first-party artwork, provenance recorded per file in the
`uploads/credit-card-asset-replacements-*/sources.csv` files in this project.

- `assets/cards/card-<id>.png` — 66 card faces, transparent-background official issuer
  marketing art, ~1200 × 757. Filenames match the card ids in the catalog.
- `assets/logos/issuer-*.svg|png` — Chase, Amex, Citi, Capital One, Discover, US Bank,
  Wells Fargo, Bilt, Apple, Costco, Target, Bank of America.
- `assets/logos/airline-*.svg|png` — United (plus a white-reverse variant), Delta, American,
  Southwest, Alaska, JetBlue, Hawaiian, Spirit.
- `assets/logos/hotel-*.svg|png` — Marriott, Hilton, Hyatt, IHG, Wyndham, Choice.

Notes for implementation:
- The Amex SVG originally referenced CSS classes with no stylesheet and rendered as a black
  box; the copy here has explicit `fill` attributes (`#006fcf` box, `#ffffff` lettering).
  Watch for the same class-reference issue if you re-export any logo.
- `issuer-discover.svg` is the orange disc mark only (no wordmark), per the official source.
- These are third-party trademarks. Card art and brand logos are used for card identification;
  confirm the permissions your app needs before shipping.

## Card catalog
The prototype carries the catalog inline in `design/Card Picker.dc.html` (the `CARDS` array in
the `<script data-dc-script>` block at the bottom of the file). Each entry:

```js
{ id, name, issuer, prog, type, brand?, hotel?, store?, biz?, other? }
```

`id` keys both the art file (`assets/cards/card-<id>.png`) and the best-for string.
`brand` (airline), `hotel`, `store`, `biz`, `other` are the flags that populate the four
category tiles and the Other tile. The `BEST` map in the same block holds the best-for
strings shown under card names ("3× dining & travel", "2% on everything", …) — these are
**design placeholders written for the mock and not verified reward terms**; replace them with
values from the app's real rewards data before shipping.

Entries flagged `isNew` / `t2` were added to the prototype so the Airline / Hotel / Store /
Business groups aren't near-empty; they are proposals, not part of the current shipping catalog.

## Files
```
design/Card Picker.dc.html   the design — section #2a is the approved flow, #1a is history
design/support.js            runtime for the design file (viewing only, do not port)
design/assets/               card art and brand logos
design/apple-touch-icon.png  app icon used in the mock header
screenshots/                 2x PNG of each screen, filenames match the screen names above
```

Open `design/Card Picker.dc.html` in a browser to see all six screens side by side; the
`data-screen-label` attribute on each device frame matches the screen names above.
