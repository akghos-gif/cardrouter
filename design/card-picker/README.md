# Handoff: Add-a-card redesign (ChooseMyCard)

## Goal
Replace the current "add a card" experience — one long alphabetical list of every supported
card — with a searchable, browsable **Add a card** page pushed from the **My cards** tab.

Seven screens define the whole flow: the My cards tab (unfiltered and with a filter chip
engaged), the Add a card page, an issuer sub-page, search results, a category sub-page, and the
custom-card step.

## About these files
`design/Card Picker.dc.html` is a **design reference built in HTML** — a prototype of intended
look and behavior, not production code to port. Recreate these screens in the app's own
components and patterns. The markup is a design-tool format (inline styles, `<sc-for>` /
`<sc-if>` template tags); read it as a spec of structure and exact values.

`design/support.js` is the prototype runtime. Ignore it entirely.

**Fidelity: high.** Colors, typography, spacing, radii, and copy are final. Card art and issuer
logos are final assets. Substitute the codebase's own primitives (buttons, list rows, fields)
where they exist, but match the values.

All screens are specified at **390 × 844** (iPhone 14/15 class). The 44px-radius device frame
in the design file is presentation only, not part of the UI.

**One deliberate inconsistency:** screens 1 and 1b show a seven-card wallet so that every
filter-chip category appears; screens 2–6 show a three-card wallet (Sapphire Preferred, Amex Gold, Citi
Double Cash). The `✓ In my cards` / `✓ Added` states on those screens are relative to the
three-card wallet. Both are sample data, not a spec.

---

## 1. My cards tab (`1 My cards tab`)
Top to bottom:

1. **App header** — 54px top padding, 18px sides, 12px bottom; app icon 42 × 42, radius 11,
   shadow `0 3px 10px rgba(37,99,235,.35)`; title "ChooseMyCard" 20px/800 `-0.02em`;
   subtitle "your rewards butler" 12px `#6b7280`. Background
   `linear-gradient(180deg, rgba(37,99,235,.10), transparent)`.
2. **Title row** — padding `6px 18px 8px`. `My cards` 22px/700 `-0.02em` with inline hint
   "order breaks ties" 13px `#6b7280`; on the right, the **+ button**: 38 × 38, radius 99,
   `#2563eb`, glyph `+` 24px/300 white, shadow `0 3px 10px rgba(37,99,235,.3)`. This replaces
   the old full-width "add a card" bar, so the held list owns the screen.
3. **Filter chips** — one row, padding `0 18px 2px`, 6px gap, horizontally scrolling, no wrap.
   Chip: white, 1px `#e5e7eb`, radius 99, padding `6px 11px`, 13px/500, 6px gap, with either a
   15 × 15 issuer logo (radius 3, `object-fit:contain`) or a 13px category glyph.
   **Only the categories present in this wallet render** — with the sample wallet that is
   Chase, Amex, Citi, Airline cards, Store cards, Business cards, Other. On this screen every
   chip is in its **off** state; the engaged state is screen 1b.
4. **Held cards list** — white card, 1px `#e5e7eb`, radius 16, padding `2px 16px 0`,
   margin `8px 0`, inside 14px screen side padding; the list fills the remaining height with
   100px bottom padding to clear the tab bar. Each row: 11px vertical padding, 1px bottom
   divider, 11px gap; priority number (16px wide, 12px/700 `#6b7280`, centered) · card art
   58 × 37 radius 5 `object-fit:cover` · name 14.5px/600 · best-for line 12px `#6b7280`
   (2px above) · drag handle `⋮⋮` 16px `#9ca3af`, `letter-spacing:-2px`.
   Rows are drag-reorderable; order sets tie-break priority.
5. **List footer hint** — "Drag to reorder · tap to edit rates" 12px `#9ca3af`,
   padding `12px 0`, pinned to the bottom of the list card (`margin-top:auto`).
6. **Tab bar** — 5 items (Which card?, My cards, Benefits, Promos, Settings), white,
   1px top border `#e5e7eb`, padding `7px 6px 28px`, shadow `0 -6px 18px rgba(0,0,0,.08)`.
   Active: label `#2563eb` 10.5px/600, pill 54 × 30 radius 99 `#eef2ff`, 1.5px `#2563eb`,
   shadow `0 1px 8px rgba(37,99,235,.28)`. Inactive: `#6b7280`, pill `rgba(125,125,125,.10)`,
   `filter:grayscale(1)`, `opacity:.75`.

## 1b. My cards, filter chip engaged (`1b Chip filter on`)
Tapping a chip filters the held list in place — it does not navigate, and it does not change
priority.

- **Selected chip** — fill `#1a1d21`, 1px `#1a1d21`, white text 13px/600, padding
  `6px 10px 6px 11px`, with a trailing ✕ 11px `opacity:.8` (2px left margin) that clears the
  filter. Its logo gets a white background with 1px padding (`box-sizing:content-box`) so it
  stays legible on dark.
- **Unselected chips** — unchanged off-state chip at `opacity:.6`.
- One chip at a time. There is no `All` chip: no selection *is* "all".
- **The list keeps the wallet's real priority numbers** (1, 4, 5, 6 in the sample) rather than
  renumbering 1-4 — the numbers mean priority across the whole wallet, so renumbering would lie.
- **Rows lose the drag handle while filtered.** Reordering a filtered subset is ambiguous;
  clear the filter to reorder.
- **List footer** replaces the drag hint with "Showing <n> of <total> · ✕ clears the filter"
  12px `#9ca3af`.

## 2. Add a card (`2 Add a card`)
A pushed page, not a sheet. Back affordance `‹ My cards` 16px `#2563eb` (chevron 26px),
padding `52px 14px 0`; title "Add a card" 22px/700 `-0.02em`, padding `4px 18px 4px`.

- **Search field** — 44px tall, white, 1px `#e5e7eb`, radius 12, 12px side padding, 8px gap,
  magnifier glyph 15px, placeholder "Search cards, banks, airlines…" 15px `#9ca3af`.
  **No autofocus** — forcing the keyboard up would cover the content below it.
- **"OR BROWSE"** — 12px/600 `#6b7280`, uppercase, `letter-spacing:.04em`,
  margin `16px 4px 8px`.
- **Browse grid** — `repeat(3, 1fr)`, 7px gap. Tile: white, 1px `#e5e7eb`, radius 14,
  padding `12px 4px 10px`, column flex, 6px gap, centered; issuer logo 34 × 34 radius 7
  `object-fit:contain`, or a category glyph in a 34px `#eef2ff` circle with `#3730a3` 18px text;
  label 12.5px/600 centered, line-height 1.2. No card counts.
  Order: **Chase, Amex, Citi, Capital One, Discover, US Bank, Wells Fargo, Airline cards,
  Hotel cards, Store cards, Business cards, Other** — Other always last.
- **Create a custom card row** — full-width list row under the grid, 9px above it:
  white, 1px `#e5e7eb`, radius 14, padding `13px 14px`, 11px gap; leading placeholder
  38 × 26, radius 5, 1.5px dashed `#9ca3af`, centered `+` 16px `#6b7280`; title
  "Create a custom card" 14.5px/600; sub-line "For a card that isn't listed" 12px `#6b7280`;
  trailing chevron `›` 19px `#9ca3af`. It pushes screen 6 with nothing pre-filled.

## 3. Issuer sub-page (`3 Chase issuer page`, Chase shown)
- Back `‹ Add a card`, 58px top padding.
- **Header** — issuer logo 28 × 28 radius 6 + title "Add a Chase card" 22px/700 `-0.02em`,
  `line-height:28px` so it optically centers against the logo, 10px gap, padding `8px 18px 2px`.
  The explicit "Add a…" verb is required — without it the page reads as cards already owned.
- **Count line** — "<n> cards to add · co-brands appear here and under their brand" 13px
  `#6b7280`, padding `0 18px 6px`. The count excludes cards already held.
- **Card grid** — 2 columns, 8px gap. Tile: white, 1px `#e5e7eb`, radius 14, padding 8,
  column flex, 6px gap; card art `width:100%`, `aspect-ratio:1.586`, radius 7,
  `object-fit:cover`; name 13px/600 line-height 1.25; best-for line 11.5px `#6b7280`
  line-height 1.25; action pinned to the tile bottom (`margin-top:auto`) so actions align
  across a row regardless of name length.
- Cards already held **stay in the grid** showing `✓ In my cards`
  (`rgba(4,120,87,.12)` fill, `#047857`, 12.5px/600, radius 99, 6px vertical) instead of
  `Add` (1px `#2563eb`, `#2563eb`, 13px/600, radius 99) — so nobody hunts for a card they own.
- **Last tile is always "Custom <issuer> card"** — card-shaped, with a placeholder in place of
  the art: `#eef0f3` fill, 1.5px dashed `#c7cbd1`, radius 7, same 1.586 ratio, centered `+`
  28px/300 `#9ca3af`; name "Custom Chase card"; sub-line "bank pre-filled" 11.5px `#6b7280`;
  button label `Create`. Opens screen 6 with the bank set.

Sub-pages exist for each issuer tile using this identical pattern.

## 4. Search results (`4 Search results`)
Typing in the field on screen 2 replaces the grid with results; the keyboard is up.

- Focused field: 1.5px `#2563eb`, radius 12, focus ring `0 0 0 3px rgba(37,99,235,.12)`,
  caret 1.5 × 18 `#2563eb`, trailing ✕ (11px white) in an 18px `#d1d5db` circle. Tapping ✕
  clears the query and restores the browse grid.
- Results in a white radius-16 card, padding `2px 14px`, 10px below the field. Row: padding
  `9px 0`, 1px bottom divider, 10px gap; card art 56 × 36 radius 5 · name 14.5px/600 with the
  matched substring highlighted `background:#fef3c7` radius 3 · best-for line 12.5px `#6b7280` ·
  trailing action. Matching is a case-insensitive substring match on the card name.
- **Action buttons share one width (76px, `box-sizing:border-box`)** so rows don't reflow when
  a card is added: `Add` = 1px `#2563eb`, `#2563eb`, 13.5px/600, radius 99, 6px vertical;
  `✓ Added` = `rgba(4,120,87,.12)` fill, `#047857`, 12.5px/600, `white-space:nowrap`, same box.
- Below the list: **"Create a custom card"** link 12.5px `#2563eb`, margin `10px 4px` — no
  "Not here?" preamble, and it does **not** pre-fill the typed text.
- The grey block at the bottom of this screen is a keyboard mock, not UI.

## 5. Category sub-page (`5 Business cards page`, Business shown)
Same pattern as the issuer page, with two differences:

- **Header** — category glyph in a 28px `#eef2ff` circle (15px glyph) + title "Business cards"
  22px/700, `line-height:28px`. Count line is just "<n> cards".
- **Last tile is "Custom card"** — same dashed card-shaped placeholder, no sub-line, button
  `Create`. Nothing is pre-filled.

Airline / Hotel / Store / Other pages use this same page with their own glyph and title.

## 6. Custom card step (`6 Custom card step`)
A step in the same navigation stack — **not** a modal stacked on the picker. Back affordance
names where you came from (`‹ Chase`); title "Custom card" 22px/700, padding `8px 18px 2px`.
Screen side padding 14, 12px between cards.

**Card 1 — identity.** White, 1px `#e5e7eb`, radius 16, padding 14, 13px gap.
- Field label 11.5px/600 `#6b7280`, uppercase, `letter-spacing:.03em`, 6px above its control.
- `CARD NAME` — 42px tall, radius 11, 1.5px `#2563eb`, focus ring
  `0 0 0 3px rgba(37,99,235,.12)`, 12px side padding; placeholder "e.g. Ink Business Premier"
  15px `#9ca3af` with a 1.5 × 18 caret. Focused on entry.
- `BANK` — 42px, radius 11, 1px `#e5e7eb`, fill `#f9fafb`; 20 × 20 issuer logo radius 4 +
  name; right side "pre-filled ▾" 12px `#9ca3af`. Editable, pre-filled when the user arrived
  from an issuer page.
- **There is no Type field.** The earn-rates toggle covers cash back vs. points, and Business
  is not a user-set attribute here.

**Card 2 — earn rates.** Same card treatment, 11px gap.
- Header row: `EARN RATES` label + `+ Add a rate` 12.5px/500 `#2563eb`.
- **Unit toggle** — segmented control, fill `#f4f5f7`, 1px `#e5e7eb`, radius 10, 2px padding;
  active segment white, radius 8, shadow `0 1px 3px rgba(0,0,0,.10)`, 13px/600
  ("% cash back"); inactive 13px/500 `#6b7280` ("× points").
- **Rate row** — 8px gap: category select `flex:1`, 38px tall, radius 10, 1px `#e5e7eb`,
  14px text, trailing `▾` 12px `#9ca3af`; value box 74 × 38, radius 10, 1px `#e5e7eb`,
  14px/600 with a `%` (or `×`) suffix 12.5px `#6b7280`. First row seeded
  "Everything else / 1.5%". The next, empty row shows placeholders
  "Pick a category" / "—" in `#9ca3af`.

**Primary action** — "Save to my cards", 48px tall, `#2563eb`, white, radius 14, 15.5px/600,
shadow `0 3px 10px rgba(37,99,235,.3)`. Saving appends the card to My cards at lowest priority
and pops back to the My cards tab.

---

## Interactions
| Trigger | Result |
| --- | --- |
| Tap `+` in My cards header | Push the Add a card page (screen 2) |
| Focus search field | Replace the browse grid with live results (screen 4), raise keyboard |
| Type | Case-insensitive substring match on card name; highlight the match |
| Tap ✕ in search | Clear query, restore the browse grid |
| Tap a browse tile | Push the issuer / category sub-page (screens 3, 5) |
| Tap `Add` | Append the card to My cards at lowest priority, flip the button to `✓ Added` / `✓ In my cards` in place |
| Tap `✓ In my cards` | No-op (or navigate to that card in My cards) |
| Tap `Create` on a custom tile | Push screen 6 with the bank pre-filled |
| Tap the custom-card row on screen 2 | Push screen 6, nothing pre-filled |
| Tap a filter chip (My cards) | Filter the held list to that category in place; chip gains ✕, others drop to `opacity:.6`, drag handles hide |
| Tap the ✕ on the selected chip | Clear the filter, restore drag handles |
| Drag a held row | Reorder priority |
| Tap a held row | Open that card's earn-rate editor (existing screen) |
| Tap `‹` | Pop one level |

Motion: standard platform push/pop for the sub-pages. Nothing else animates.

**Open question — empty shelves.** Against today's catalog three browse tiles are near-empty:
Hotel cards has no cards, Airline cards has two, and Other holds only Bilt, Apple Card and
Target Circle. Decide whether an empty shelf hides its tile or shows a count so the tap is
informed. Not resolved in this design.

## State
- `heldCards: string[]` — ordered card ids; the order **is** the tie-break priority.
- `query: string` — search text; empty means "show the browse grid".
- `chipFilter: string | null` — selected category chip on the My cards tab; `null` = show all.
- `route` — `myCards` | `addCard` | `{issuer}` | `{category}` | `custom`.
- Card catalog is static app data; no fetch is required for this flow.

## Design tokens
Colors
- Page background `#f4f5f7`; canvas behind the device frames `#e9ebef`
- Surface `#ffffff`; alt field fill `#f9fafb`; border `#e5e7eb`;
  dashed placeholder border `#c7cbd1` (card-shaped) / `#9ca3af` (row); placeholder fill `#eef0f3`
- Text primary `#1a1d21`; secondary `#6b7280`; placeholder / tertiary `#9ca3af`
- Accent / links `#2563eb` (hover `#1d4ed8`); accent tint `#eef2ff`; accent-on-tint `#3730a3`
- Success `#047857` on `rgba(4,120,87,.12)`
- Search highlight `#fef3c7`
- Keyboard mock `#d1d5db` / keys `#ffffff` / modifiers `#aeb3bc`

Type — system stack (`-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`)
- App title 20/800 `-0.02em` · Screen title 22/700 `-0.02em` · Section 16/600
- List row name 14.5/600 · row secondary 12–12.5/400 · tile name 13/600 (1.25)
- Body / field 15 · hint 13 · field label 11.5/600 uppercase `.03em` · micro 11.5–12 ·
  tab label 10.5/600

Spacing — screen side padding 14 (18 for headers and titles); grid gaps 7 (browse) / 8 (cards);
tile padding 8; card padding 14; list row vertical padding 9–11.

Radii — 44 device frame · 16 list/section card · 14 tile, row, primary button · 12 search field ·
11 form field · 10 rate control · 7 card art · 5–6 logo · 99 pill.

Shadows — device `0 20px 60px rgba(0,0,0,.12)` · tab bar `0 -6px 18px rgba(0,0,0,.08)` ·
`+` button and primary button `0 3px 10px rgba(37,99,235,.3)` ·
focus ring `0 0 0 3px rgba(37,99,235,.12)` · active segment `0 1px 3px rgba(0,0,0,.10)`.

Card art aspect ratio: **1.586** (ISO/IEC 7810 ID-1).

## Card catalog
The prototype carries the catalog inline in `design/Card Picker.dc.html` (the `CARDS` array in
the `<script data-dc-script>` block). It is the **28 cards in the app today** — no proposed
additions. Each entry:

```js
{ id, name, issuer, prog, type, brand?, hotel?, store?, biz?, other? }
```

`id` keys the art file (`assets/cards/card-<id>.png`). `brand` (airline), `hotel`, `store`,
`biz` and `other` are the flags behind the four category tiles, the Other tile, and the filter
chips.

The `BEST` map in the same block holds the best-for strings shown under card names
("3× dining & travel", "2% on everything", …). These are **design placeholders written for the
mock, not verified reward terms** — the shipping strings should be derived from the app's real
earn rates (`bestForCard()`), not stored as copy.

## Assets
`design/assets/` — the art the six screens actually reference.

- `assets/cards/card-<id>.png` — 28 card faces, transparent-background official issuer
  marketing art, ~1200 × 757. Filenames match the catalog ids.
- `assets/logos/issuer-*.svg` — Chase, Amex, Citi, Capital One, Discover, US Bank, Wells Fargo.

Notes:
- Card art is raw marketing art (~670 KB each). Not shippable as-is; resize/compress for the
  44 × 28, 58 × 37 and ~180px render sizes.
- The Amex SVG originally referenced CSS classes with no stylesheet and rendered as a black
  box; this copy has explicit `fill` attributes (`#006fcf` box, `#ffffff` lettering). Watch for
  the same issue if you re-export any logo.
- `issuer-discover.svg` is the orange disc mark only (no wordmark), per the official source.
- These are third-party trademarks, used for card identification. Confirm the permissions the
  app needs before shipping.

## Files
```
design/Card Picker.dc.html   the design — seven screens, side by side
design/support.js            prototype runtime (viewing only, do not port)
design/assets/               card art and issuer logos
design/apple-touch-icon.png  app icon used in the mock header
screenshots/                 2× PNG of each screen; filenames match the screen names
```

Open `design/Card Picker.dc.html` in a browser to see all seven screens; each device frame's
`data-screen-label` matches the names above.
