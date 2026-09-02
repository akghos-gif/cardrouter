# Card picker fidelity audit

Status: Finalized for the section 2a implementation.

Audit target: light mode at a 390 × 844 CSS-pixel viewport, after push/pop motion settles. CSS variables and utility-like rules are resolved below to computed px/hex/RGBA values. Repeated declarations are consolidated only when the same element pattern and value recur across 2a screens; every numeric or color declaration in those patterns is represented by a row. The 44 px-radius phone shell is explicitly excluded from the product UI by the handoff.

## Canvas, header, and hub title

| Design file value | Element it came from | Implementation value | File:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| 390px | All six 2a frame widths | 390px test viewport | `tests/radar-tests.html:292` | MATCH |
| 844px | All six 2a frame heights | 844px test viewport | `tests/radar-tests.html:292` | MATCH |
| `#f4f5f7` | Page/frame background | `#f4f5f7` | `index.html:20` | MATCH |
| `#1a1d21` | Page primary text | `#1a1d21` | `index.html:20` | MATCH |
| 44px | Presentation-frame radius | N/A; frame intentionally omitted | `index.html:48` | MATCH |
| `0 20px 60px rgba(0,0,0,.12)` | Presentation-frame shadow | N/A; frame intentionally omitted | `index.html:48` | MATCH |
| `1px solid #e5e7eb` | Presentation-frame border | N/A; frame intentionally omitted | `index.html:48` | MATCH |
| 11px | App-header item gap | 11px | `index.html:51` | MATCH |
| `54px 18px 12px` | App-header padding | `54px 18px 12px` at reference viewport | `index.html:240` | MATCH |
| `linear-gradient(180deg, rgba(37,99,235,.10), transparent)` | App-header background | `linear-gradient(180deg, rgba(37,99,235,.10), transparent)` | `index.html:240` | MATCH |
| 42px | App-icon width | 42px | `index.html:54` | MATCH |
| 42px | App-icon height | 42px | `index.html:54` | MATCH |
| 11px | App-icon radius | 11px | `index.html:54` | MATCH |
| `0 3px 10px rgba(37,99,235,.35)` | App-icon shadow | `0 3px 10px rgba(37,99,235,.35)` | `index.html:242` | MATCH |
| 20px | App-title size | 20px | `index.html:56` | MATCH |
| 800 | App-title weight | 800 | `index.html:56` | MATCH |
| -0.02em | App-title tracking | -0.02em | `index.html:56` | MATCH |
| 1.1 | App-title line height | 1.1 | `index.html:56` | MATCH |
| 12px | App-subtitle size | 12px | `index.html:57` | MATCH |
| `#6b7280` | App-subtitle color | `#6b7280` | `index.html:20` | MATCH |
| 1px | App-subtitle top margin | 1px | `index.html:57` | MATCH |
| `6px 18px 8px` | Hub title-row padding | `6px 18px 8px` | `index.html:58` | MATCH |
| 8px | Hub title-row gap | 8px | `index.html:58` | MATCH |
| 22px | “My cards” size | 22px | `index.html:59` | MATCH |
| 0 | “My cards” margin | 0 | `index.html:59` | MATCH |
| -0.02em | “My cards” tracking | -0.02em | `index.html:59` | MATCH |
| 13px | Priority-hint size | 13px | `index.html:61` | MATCH |
| `#6b7280` | Priority-hint color | `#6b7280` | `index.html:243` | MATCH |
| `0 14px` | Main screen-side padding | `0 14px` | `index.html:65` | MATCH |

## Held cards and add row

| Design file value | Element it came from | Implementation value | File:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `#ffffff` | Held-list surface | `#ffffff` | `index.html:20` | MATCH |
| `1px solid #e5e7eb` | Held-list border | `1px solid #e5e7eb` | `index.html:251` | MATCH |
| 16px | Held-list radius | 16px | `index.html:251` | MATCH |
| `2px 14px` | Held-list padding | `2px 14px` | `index.html:251` | MATCH |
| `8px 0` | Held-list margin | `8px 0` | `index.html:252` | MATCH |
| 10px | Held-row gap | 10px | `index.html:253` | MATCH |
| `7px 0` | Held-row vertical padding | `7px 0` on the row's primary button | `index.html:256` | MATCH |
| `1px solid #e5e7eb` | Held-row divider | `1px solid #e5e7eb` | `index.html:253` | MATCH |
| 20px | Priority-number width | 20px | `index.html:259` | MATCH |
| `#6b7280` | Priority-number color | `#6b7280` | `index.html:259` | MATCH |
| 12px | Priority-number size | 12px | `index.html:259` | MATCH |
| 700 | Priority-number weight | 700 | `index.html:259` | MATCH |
| 44px | Held card-art width | 44px | `index.html:260` | MATCH |
| 28px | Held card-art height | 28px | `index.html:260` | MATCH |
| 4px | Held card-art radius | 4px | `index.html:260` | MATCH |
| 1 | Held-copy flex factor | 1 | `index.html:256` | MATCH |
| 0 | Held-copy minimum width | 0 | `index.html:256` | MATCH |
| 14.5px | Held-card name size | 14.5px | `index.html:261` | MATCH |
| 600 | Held-card name weight | 600 | `index.html:261` | MATCH |
| 12.5px | Held best-for size | 12.5px | `index.html:262` | MATCH |
| `#6b7280` | Held best-for color | `#6b7280` | `index.html:262` | MATCH |
| 1px | Held best-for top margin | 1px | `index.html:262` | MATCH |
| `#9ca3af` | Drag-handle color | `#9ca3af` | `index.html:263` | MATCH |
| 16px | Drag-handle glyph size | 16px | `index.html:264` | MATCH |
| -2px | Drag-handle glyph tracking | -2px | `index.html:264` | MATCH |
| `6px 4px 6px` | Add-row margin | `6px 4px 6px` | `index.html:268` | MATCH |
| 16px | “Add a card” size | 16px | `index.html:269` | MATCH |
| 700 | “Add a card” computed `<h2>` weight | 700 | `index.html:269` | MATCH |
| 0 | “Add a card” margin | 0 | `index.html:269` | MATCH |
| 13px | “+ Custom card” size | 13px | `index.html:270` | MATCH |
| 500 | “+ Custom card” weight | 500 | `index.html:271` | MATCH |
| `#2563eb` | “+ Custom card” color | `#2563eb` | `index.html:270` | MATCH |

## Search and results

| Design file value | Element it came from | Implementation value | File:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| 42px | Search field visible height | 42px (`44px` shell with `1px` top/bottom inset) | `index.html:274` | MATCH |
| 8px | Search field content gap | 8px | `index.html:274` | MATCH |
| `0 12px` | Search field side padding | `0 12px` | `index.html:274` | MATCH |
| `#ffffff` | Search field fill | `#ffffff` | `index.html:277` | MATCH |
| `1px solid #e5e7eb` | Resting search border | `1px solid #e5e7eb` | `index.html:276` | MATCH |
| 12px | Search field radius | 12px | `index.html:277` | MATCH |
| `#9ca3af` | Search placeholder/icon color | `#9ca3af` | `index.html:21` | MATCH |
| 15px | Search input/icon size | 15px | `index.html:281` | MATCH |
| `1.5px solid #2563eb` | Focused search border | `1.5px solid #2563eb` | `index.html:278` | MATCH |
| `0 0 0 3px rgba(37,99,235,.12)` | Focused search ring | `0 0 0 3px rgba(37,99,235,.12)` | `index.html:278` | MATCH |
| 10px | Focused-field visual top margin | 10px (`9px` shell margin + `1px` inset) | `index.html:311` | MATCH |
| 1.5px | Synthetic caret width | Platform-controlled native caret | `index.html:282` | MISMATCH |
| 18px | Synthetic caret height | Platform-controlled native caret | `index.html:282` | MISMATCH |
| `#2563eb` | Caret color | `#2563eb` | `index.html:283` | MATCH |
| -3px | Synthetic caret vertical alignment | Platform-controlled native caret | `index.html:282` | MISMATCH |
| 1px | Synthetic caret left margin | Platform-controlled native caret | `index.html:282` | MISMATCH |
| 18px | Clear-control width | 18px | `index.html:287` | MATCH |
| 18px | Clear-control height | 18px | `index.html:287` | MATCH |
| 99px | Clear-control radius | 99px | `index.html:287` | MATCH |
| `#d1d5db` | Clear-control fill | `#d1d5db` | `index.html:27` | MATCH |
| `#ffffff` | Clear-control glyph | `#ffffff` | `index.html:27` | MATCH |
| 11px | Clear-control glyph size | 11px | `index.html:288` | MATCH |
| `#ffffff` | Results-card surface | `#ffffff` | `index.html:290` | MATCH |
| `1px solid #e5e7eb` | Results-card border | `1px solid #e5e7eb` | `index.html:290` | MATCH |
| 16px | Results-card radius | 16px | `index.html:290` | MATCH |
| `2px 14px` | Results-card padding | `2px 14px` | `index.html:291` | MATCH |
| 10px | Results-card top margin | 10px | `index.html:291` | MATCH |
| 10px | Search-result row gap | 10px | `index.html:292` | MATCH |
| `9px 0` | Search-result row padding | `9px 0` | `index.html:292` | MATCH |
| `1px solid #e5e7eb` | Search-result divider | `1px solid #e5e7eb` | `index.html:293` | MATCH |
| 56px | Result card-art width | 56px | `index.html:294` | MATCH |
| 36px | Result card-art height | 36px | `index.html:294` | MATCH |
| 5px | Result card-art radius | 5px | `index.html:294` | MATCH |
| 1 | Search-result copy flex factor | 1 | `index.html:295` | MATCH |
| 0 | Search-result copy minimum width | 0 | `index.html:295` | MATCH |
| 14.5px | Search-result name size | 14.5px | `index.html:296` | MATCH |
| 600 | Search-result name weight | 600 | `index.html:296` | MATCH |
| `#fef3c7` | Match-highlight fill | `#fef3c7` | `index.html:297` | MATCH |
| 3px | Match-highlight radius | 3px | `index.html:297` | MATCH |
| 12.5px | Result best-for size | 12.5px | `index.html:298` | MATCH |
| `#6b7280` | Result best-for color | `#6b7280` | `index.html:298` | MATCH |
| 1px | Result best-for top margin | 1px | `index.html:298` | MATCH |
| 76px | Add/Added action width | 76px | `index.html:299` | MATCH |
| 99px | Add/Added action radius | 99px | `index.html:299` | MATCH |
| `6px 0` | Add/Added action padding | `6px 0` | `index.html:299` | MATCH |
| `1px solid #2563eb` | Search Add border | `1px solid #2563eb` | `index.html:300` | MATCH |
| `#2563eb` | Search Add text | `#2563eb` | `index.html:300` | MATCH |
| 13.5px | Search Add size | 13.5px | `index.html:301` | MATCH |
| 600 | Search Add weight | 600 | `index.html:301` | MATCH |
| `rgba(4,120,87,.12)` | Search Added fill | `rgba(4,120,87,.12)` | `index.html:24` | MATCH |
| `#047857` | Search Added text | `#047857` | `index.html:24` | MATCH |
| 12.5px | Search Added size | 12.5px | `index.html:304` | MATCH |
| 600 | Search Added weight | 600 | `index.html:301` | MATCH |
| 13px | Custom search-prompt size | 13px | `index.html:307` | MATCH |
| `#6b7280` | Custom search-prompt color | `#6b7280` | `index.html:307` | MATCH |
| 1.45 | Custom search-prompt line height | 1.45 | `index.html:307` | MATCH |
| `12px 4px` | Custom search-prompt margin | `12px 4px` | `index.html:307` | MATCH |
| `#2563eb` | Custom search-prompt link color | `#2563eb` | `index.html:308` | MATCH |
| 6 | README visible-result row count | 6-row (336px) scrolling region; all matches retained | `index.html:290` | MATCH |

## Typing-screen keyboard reference

The following values belong to the operating-system keyboard drawn into the static reference. They are audited as mismatches because the app correctly invokes a native keyboard rather than rendering these pixels. The corresponding rationale is recorded in `DEVIATIONS.md`.

| Design file value | Element it came from | Implementation value | File:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| 0 | Keyboard left edge | Native OS keyboard | `index.html:1889` | MISMATCH |
| 0 | Keyboard right edge | Native OS keyboard | `index.html:1889` | MISMATCH |
| 0 | Keyboard bottom edge | Native OS keyboard | `index.html:1889` | MISMATCH |
| 290px | Keyboard height | Native OS keyboard | `index.html:1889` | MISMATCH |
| `#d1d5db` | Keyboard tray fill | Native OS keyboard | `index.html:1889` | MISMATCH |
| `12px 12px 0 0` | Keyboard top radius | Native OS keyboard | `index.html:1889` | MISMATCH |
| `repeat(4,1fr)` | Keyboard row sizing | Native OS keyboard | `index.html:1889` | MISMATCH |
| 6px | Keyboard row gap | Native OS keyboard | `index.html:1889` | MISMATCH |
| `8px 4px 30px` | Keyboard tray padding | Native OS keyboard | `index.html:1889` | MISMATCH |
| 5px | Key gap | Native OS keyboard | `index.html:1889` | MISMATCH |
| `0 18px` | Second key-row inset | Native OS keyboard | `index.html:1889` | MISMATCH |
| `0 4px` | Third/fourth key-row inset | Native OS keyboard | `index.html:1889` | MISMATCH |
| 1 | Standard key flex factor | Native OS keyboard | `index.html:1889` | MISMATCH |
| `#ffffff` | Standard key fill | Native OS keyboard | `index.html:1889` | MISMATCH |
| 6px | Standard key radius | Native OS keyboard | `index.html:1889` | MISMATCH |
| 1.4 | Shift/delete key flex factor | Native OS keyboard | `index.html:1889` | MISMATCH |
| `#aeb3bc` | Shift/delete key fill | Native OS keyboard | `index.html:1889` | MISMATCH |
| 1.2 | Bottom modifier/enter flex factor | Native OS keyboard | `index.html:1889` | MISMATCH |
| 5 | Space-key flex factor | Native OS keyboard | `index.html:1889` | MISMATCH |
| `#2563eb` | Enter-key fill | Native OS keyboard | `index.html:1889` | MISMATCH |

## Browse grid and bottom navigation

| Design file value | Element it came from | Implementation value | File:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `repeat(3,1fr)` | Browse-grid columns | `repeat(3,1fr)` | `index.html:312` | MATCH |
| 7px | Browse-grid gap | 7px | `index.html:312` | MATCH |
| 8px | Browse-grid top margin | 8px | `index.html:312` | MATCH |
| 6px | Browse-tile internal gap | 6px | `index.html:313` | MATCH |
| `12px 4px 10px` | Browse-tile padding | `12px 4px 10px` | `index.html:314` | MATCH |
| `#ffffff` | Browse-tile surface | `#ffffff` | `index.html:315` | MATCH |
| `1px solid #e5e7eb` | Browse-tile border | `1px solid #e5e7eb` | `index.html:314` | MATCH |
| 14px | Browse-tile radius | 14px | `index.html:314` | MATCH |
| 34px | Browse-logo/glyph width | 34px | `index.html:317` | MATCH |
| 34px | Browse-logo/glyph height | 34px | `index.html:317` | MATCH |
| 7px | Browse-logo radius | 7px | `index.html:317` | MATCH |
| 99px | Browse-glyph circle radius | 99px | `index.html:318` | MATCH |
| `#eef2ff` | Browse-glyph fill | `#eef2ff` | `index.html:23` | MATCH |
| `#3730a3` | Browse-glyph color | `#3730a3` | `index.html:23` | MATCH |
| 18px | Browse-glyph size | 18px | `index.html:319` | MATCH |
| 12.5px | Browse-label size | 12.5px | `index.html:320` | MATCH |
| 600 | Browse-label weight | 600 | `index.html:320` | MATCH |
| 1.2 | Browse-label line height | 1.2 | `index.html:320` | MATCH |
| 0 | Nav left edge | 0 | `index.html:87` | MATCH |
| 0 | Nav right edge | 0 | `index.html:87` | MATCH |
| 0 | Nav bottom edge | 0 | `index.html:87` | MATCH |
| 2px | Nav item gap | 2px | `index.html:87` | MATCH |
| `#ffffff` | Nav surface | `#ffffff` | `index.html:244` | MATCH |
| `1px solid #e5e7eb` | Nav top border | `1px solid #e5e7eb` | `index.html:87` | MATCH |
| `7px 6px 28px` | Nav padding | `7px 6px 28px` at reference viewport | `index.html:244` | MATCH |
| `0 -6px 18px rgba(0,0,0,.08)` | Nav shadow | `0 -6px 18px rgba(0,0,0,.08)` | `index.html:245` | MATCH |
| 1 | Each nav item's flex factor | 1 | `index.html:90` | MATCH |
| `#6b7280` | Inactive nav label | `#6b7280` | `index.html:246` | MATCH |
| 10.5px | Nav-label size | 10.5px | `index.html:90` | MATCH |
| 600 | Nav-label weight | 600 | `index.html:90` | MATCH |
| 3px | Nav icon/label gap | 3px | `index.html:91` | MATCH |
| 19px | Nav icon size | 19px | `index.html:92` | MATCH |
| 1 | Nav icon line height | 1 | `index.html:92` | MATCH |
| 54px | Nav-pill width | 54px | `index.html:93` | MATCH |
| 30px | Nav-pill height | 30px | `index.html:93` | MATCH |
| 99px | Nav-pill radius | 99px | `index.html:93` | MATCH |
| `rgba(125,125,125,.10)` | Inactive nav-pill fill | `rgba(125,125,125,.10)` | `index.html:28` | MATCH |
| `1.5px solid transparent` | Inactive nav-pill border | `1.5px solid transparent` | `index.html:94` | MATCH |
| 1 | Inactive nav grayscale amount | 1 | `index.html:95` | MATCH |
| 0.75 | Inactive nav opacity | 0.75 | `index.html:95` | MATCH |
| `#2563eb` | Active nav label | `#2563eb` | `index.html:248` | MATCH |
| `#eef2ff` | Active nav-pill fill | `#eef2ff` | `index.html:249` | MATCH |
| `1.5px solid #2563eb` | Active nav-pill border | `1.5px solid #2563eb` | `index.html:94` | MATCH |
| `0 1px 8px rgba(37,99,235,.28)` | Active nav-pill shadow | `0 1px 8px rgba(37,99,235,.28)` | `index.html:249` | MATCH |

## Issuer/category card pages

| Design file value | Element it came from | Implementation value | File:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `58px 14px 0` | Back-row padding from viewport | `58px 14px 0` (14px main + 58px button top) | `index.html:326` | MATCH |
| 2px | Back glyph/label gap | 2px | `index.html:326` | MATCH |
| `#2563eb` | Back affordance color | `#2563eb` | `index.html:327` | MATCH |
| 16px | Back-label size | 16px | `index.html:327` | MATCH |
| 26px | Back-glyph size | 26px | `index.html:329` | MATCH |
| 1 | Back-glyph line height | 1 | `index.html:329` | MATCH |
| -3px | Back-glyph top adjustment | -3px | `index.html:329` | MATCH |
| `8px 18px 8px` | Issuer heading padding from viewport | `8px 18px 8px` (14px main + 4px margins) | `index.html:330` | MATCH |
| 10px | Issuer logo/title gap | 10px | `index.html:330` | MATCH |
| 28px | Issuer-logo width | 28px | `index.html:332` | MATCH |
| 28px | Issuer-logo height | 28px | `index.html:332` | MATCH |
| 6px | Issuer-logo radius | 6px | `index.html:332` | MATCH |
| 22px | Issuer-page title size | 22px | `index.html:335` | MATCH |
| 700 | Issuer-page title weight | 700 | `index.html:335` | MATCH |
| -0.02em | Issuer-page title tracking | -0.02em | `index.html:335` | MATCH |
| 28px | Issuer-page title line height | 28px | `index.html:335` | MATCH |
| 0 | Issuer-page title margin | 0 | `index.html:335` | MATCH |
| `1fr 1fr` | Card-grid columns | `1fr 1fr` | `index.html:337` | MATCH |
| 8px | Card-grid gap | 8px | `index.html:337` | MATCH |
| 6px | Issuer card-grid top margin | 6px | `index.html:337` | MATCH |
| `#ffffff` | Card-tile surface | `#ffffff` | `index.html:340` | MATCH |
| `1px solid #e5e7eb` | Card-tile border | `1px solid #e5e7eb` | `index.html:339` | MATCH |
| 14px | Card-tile radius | 14px | `index.html:340` | MATCH |
| 8px | Card-tile padding | 8px | `index.html:339` | MATCH |
| 7px | Card-tile internal gap | 7px | `index.html:339` | MATCH |
| 100% | Card-art width | 100% | `index.html:341` | MATCH |
| 1.586 | Card-art aspect ratio | 1.586 | `index.html:341` | MATCH |
| 7px | Card-art radius | 7px | `index.html:341` | MATCH |
| 13px | Card-tile name size | 13px | `index.html:347` | MATCH |
| 600 | Card-tile name weight | 600 | `index.html:347` | MATCH |
| 1.25 | Card-tile name line height | 1.25 | `index.html:347` | MATCH |
| `rgba(4,120,87,.12)` | In-my-cards fill | `rgba(4,120,87,.12)` | `index.html:303` | MATCH |
| `#047857` | In-my-cards text | `#047857` | `index.html:304` | MATCH |
| 99px | Tile action radius | 99px | `index.html:299` | MATCH |
| `6px 0` | Tile action padding | `6px 0` | `index.html:299` | MATCH |
| 12.5px | In-my-cards size | 12.5px | `index.html:350` | MATCH |
| 600 | In-my-cards weight | 600 | `index.html:301` | MATCH |
| `1px solid #2563eb` | Tile Add/Create border | `1px solid #2563eb` | `index.html:300` | MATCH |
| `#2563eb` | Tile Add/Create text | `#2563eb` | `index.html:300` | MATCH |
| 13px | Tile Add/Create size | 13px | `index.html:349` | MATCH |
| 600 | Tile Add/Create weight | 600 | `index.html:301` | MATCH |
| 100% | Custom placeholder width | 100% | `index.html:342` | MATCH |
| 1.586 | Custom placeholder aspect ratio | 1.586 | `index.html:342` | MATCH |
| 7px | Custom placeholder radius | 7px | `index.html:343` | MATCH |
| `#eef0f3` | Custom placeholder fill | `#eef0f3` | `index.html:343` | MATCH |
| `1.5px dashed #c7cbd1` | Custom placeholder border | `1.5px dashed #c7cbd1` | `index.html:343` | MATCH |
| `#9ca3af` | Custom placeholder plus color | `#9ca3af` | `index.html:344` | MATCH |
| 28px | Custom placeholder plus size | 28px | `index.html:344` | MATCH |
| 1 | Custom placeholder plus line height | 1 | `index.html:344` | MATCH |
| 300 | Custom placeholder plus weight | 300 | `index.html:344` | MATCH |
| 11.5px | Custom-tile subline size | 11.5px | `index.html:348` | MATCH |
| 400 | Custom-tile subline weight | 400 | `index.html:348` | MATCH |
| `#6b7280` | Custom-tile subline color | `#6b7280` | `index.html:348` | MATCH |
| 1px | Custom-tile subline top margin | 1px | `index.html:348` | MATCH |

## Added-card toast

| Design file value | Element it came from | Implementation value | File:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| 14px | Toast left inset | 14px measured at 390px | `index.html:370` | MATCH |
| 14px | Toast right inset | 14px measured at 390px | `index.html:370` | MATCH |
| 104px | Toast bottom offset | 104px at reference viewport | `index.html:370` | MATCH |
| `#1a1d21` | Toast fill | `#1a1d21` | `index.html:25` | MATCH |
| `#f4f5f7` | Toast text | `#f4f5f7` | `index.html:25` | MATCH |
| `12px 14px` | Toast padding | `12px 14px` | `index.html:371` | MATCH |
| 14px | Toast radius | 14px | `index.html:371` | MATCH |
| 14px | Toast message size | 14px | `index.html:372` | MATCH |
| 10px | Toast content gap | 10px | `index.html:134` | MATCH |
| `0 8px 24px rgba(0,0,0,.25)` | Toast shadow | `0 8px 24px rgba(0,0,0,.25)` | `index.html:373` | MATCH |
| 40px | Toast card-art width | 40px | `index.html:376` | MATCH |
| 26px | Toast card-art height | 26px | `index.html:376` | MATCH |
| 3px | Toast card-art radius | 3px | `index.html:376` | MATCH |
| 1 | Toast message flex factor | 1 | `index.html:377` | MATCH |
| 1.3 | Toast message line height | 1.3 | `index.html:377` | MATCH |
| `#93c5fd` | Toast Undo color | `#93c5fd` | `index.html:23` | MATCH |
| 13px | Toast Undo size | 13px | `index.html:379` | MATCH |
| 600 | Toast Undo weight | 600 | `index.html:379` | MATCH |

## Airline page and filter chips

| Design file value | Element it came from | Implementation value | File:line | MATCH/MISMATCH |
| --- | --- | --- | --- | --- |
| `8px 18px 8px` | Airline heading padding from viewport | `8px 18px 8px` (14px main + 4px margins) | `index.html:330` | MATCH |
| 8px | Airline title/hint gap | 8px | `index.html:331` | MATCH |
| 22px | Airline-page title size | 22px | `index.html:335` | MATCH |
| 700 | Airline-page title weight | 700 | `index.html:335` | MATCH |
| -0.02em | Airline-page title tracking | -0.02em | `index.html:335` | MATCH |
| 13px | Airline-page hint size | 13px | `index.html:336` | MATCH |
| `#6b7280` | Airline-page hint color | `#6b7280` | `index.html:336` | MATCH |
| 6px | Jump-chip row gap | 6px | `index.html:351` | MATCH |
| `4px -14px 0` | Jump-chip row bleed margin | `4px -14px 0` | `index.html:351` | MATCH |
| `0 14px` | Jump-chip row inset padding | `0 14px` | `index.html:351` | MATCH |
| `1px solid #1a1d21` | Active All/brand chip border | `1px solid #1a1d21` | `index.html:359` | MATCH |
| `#1a1d21` | Active All/brand chip fill | `#1a1d21` | `index.html:359` | MATCH |
| `#ffffff` | Active All/brand chip text | `#ffffff` | `index.html:359` | MATCH |
| 99px | Jump-chip radius | 99px | `index.html:355` | MATCH |
| `5px 12px` | All-chip padding | `5px 12px` | `index.html:358` | MATCH |
| 13px | Jump-chip size | 13px | `index.html:356` | MATCH |
| 600 | Active jump-chip weight | 600 | `index.html:359` | MATCH |
| 6px | Brand-chip logo/text gap | 6px | `index.html:354` | MATCH |
| `1px solid #e5e7eb` | Inactive brand-chip border | `1px solid #e5e7eb` | `index.html:354` | MATCH |
| `#ffffff` | Inactive brand-chip fill | `#ffffff` | `index.html:355` | MATCH |
| `#1a1d21` | Inactive brand-chip text | `#1a1d21` | `index.html:355` | MATCH |
| `5px 11px 5px 6px` | Brand-chip padding | `5px 11px 5px 6px` | `index.html:355` | MATCH |
| 500 | Inactive brand-chip weight | 500 | `index.html:356` | MATCH |
| 18px | Jump-chip logo width | 18px | `index.html:361` | MATCH |
| 18px | Jump-chip logo height | 18px | `index.html:361` | MATCH |
| 4px | Jump-chip logo radius | 4px | `index.html:361` | MATCH |
| 1px | Selected-chip logo padding | 1px | `index.html:362` | MATCH |
| `#ffffff` | Selected-chip logo backing | `#ffffff` | `index.html:362` | MATCH |
| 11px | Selected-chip close size | 11px | `index.html:363` | MATCH |
| 0.8 | Selected-chip close opacity | 0.8 | `index.html:363` | MATCH |
| 2px | Selected-chip close left margin | 2px | `index.html:363` | MATCH |
| 0.6 | Unselected filtered-chip opacity | 0.6 | `index.html:360` | MATCH |
| 8px | Airline group-header gap | 8px | `index.html:364` | MATCH |
| `14px 4px 6px` | Airline group-header margin | `14px 4px 6px` | `index.html:364` | MATCH |
| 22px | Airline group-logo width | 22px | `index.html:365` | MATCH |
| 22px | Airline group-logo height | 22px | `index.html:365` | MATCH |
| 5px | Airline group-logo radius | 5px | `index.html:365` | MATCH |
| 16px | Airline group-name size | 16px | `index.html:366` | MATCH |
| 700 | Airline group-name computed `<h2>` weight | 700 | `index.html:366` | MATCH |
| 1.2 | Airline group-name line height | 1.2 | `index.html:366` | MATCH |
| 0 | Airline group-name margin | 0 | `index.html:366` | MATCH |
| 12.5px | Airline group metadata size | 12.5px | `index.html:367` | MATCH |
| `#6b7280` | Airline group metadata color | `#6b7280` | `index.html:367` | MATCH |
| 1.2 | Airline group metadata line height | 1.2 | `index.html:367` | MATCH |
| `1fr 1fr` | Airline card-grid columns | `1fr 1fr` | `index.html:337` | MATCH |
| 8px | Airline card-grid gap | 8px | `index.html:337` | MATCH |
| 0 | Airline group card-grid top margin | 0 | `index.html:338` | MATCH |

## Structural and rendered comparison at 390 × 844

Final browser captures were compared with every PNG in `screenshots/` after animations settled.

| Reference screen | Structural result | Notes |
| --- | --- | --- |
| `2a-1-my-cards-hub.png` | MATCH with authorized content differences | Header, held rows, Add row, field, 12-tile order, 3-column geometry, and nav structure match. Best-for copy differs because it is generated from production rewards data. |
| `2a-2-typing.png` | MISMATCH — documented | The production query shown during comparison has 4 trusted matches rather than the mock's 6 because proposed Costco/Alaska entries are omitted. The real browser/OS owns the keyboard and caret. All matches remain reachable in the six-row scrolling region. |
| `2a-3-chase-cards.png` | MISMATCH — documented | The shipping page has 6 production Chase cards plus Custom; the mock has 8 plus Custom. Grid, art aspect, controls, title, and ordering pattern match. |
| `2a-4-after-add.png` | MISMATCH — documented | Same authorized catalog difference as 2a-3. The measured toast is x=14…376, 50px tall, and 104px above the bottom, with 40 × 26 art and the short message/Undo structure. |
| `2a-5-airline-cards.png` | MISMATCH — documented | The shipping catalog has one United and one Southwest card instead of 17 prototype airline cards. All eight chips are present and horizontally reachable; group and tile geometry match. |
| `2a-6-airline-delta-filter.png` | MISMATCH — documented | Delta has no production-backed card yet, so the filtered group contains only the Custom Delta tile instead of four proposal cards plus Custom. Selected/muted chip styling, close glyph, white logo backing, and in-place filter behavior match. |

Additional rendered checks:

- 390 × 844 light and dark: document width 390 px, no page-level horizontal overflow, no console errors.
- 320 px: no horizontal overflow; the hub remains three columns and all nav items remain reachable.
- 200% text-zoom equivalent (195 × 422 CSS px): document width 195 px; the first search row is x=23…172 and its visible children remain inside it; browse/card/nav adaptations preserve whole-word labels and all controls.
- 1024 px desktop: centered 560 px content cap, three-column hub, two-column card pages, no horizontal overflow.
- Airline focus test: chip scroller measured 735 px content / 390 px viewport; focusing Hawaiian moved it to `scrollLeft=345`, proving keyboard reachability and focus scroll-in-view.
- Card assets: all 56 WebPs have the approved 112 px or 360 px width, preserve 1.586 rendering, report alpha-capable `yuva420p`, and contain transparent and opaque alpha samples.

Every MISMATCH above is covered by `DEVIATIONS.md`; no unexplained mismatch remains.
