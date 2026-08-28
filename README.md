# 💳 CardRouter — your rewards butler

A single-file web app that answers one question at the register: **"Which of my credit cards should I use for this purchase?"**

Tap a purchase category — dining, groceries, gas, flights, hotels, and more — and CardRouter ranks your cards by real earning power, factoring in rotating 5% categories, activation status, point valuations, and your own priority order. Add it to your iPhone home screen and it behaves like a native app.

> **What it is / isn't:** CardRouter is a *recommender*, not a payment router. It tells you which card to tap; the tap itself still happens with your physical card or wallet. (True automatic routing requires being a card issuer — the [full evaluation](#background) of why lives with this project's notes.)

## Features

- **Which card?** — tap a category and get a ranked answer. Points cards are compared against cash-back cards using cents-per-point valuations, so "3x Ultimate Rewards" and "5% cash back" compete on equal footing (shown as an effective ≈% for every card).
- **Built-in rules database** — earn rates for ~19 popular US rewards cards, verified July 2026, including the Chase Sapphire Reserve revamp, the Amex Gold refresh, the Prime Visa, and the Citi Custom Cash closure to new applicants.
- **Rotating 5% categories:** the current quarter's Chase Freedom Flex and Discover it categories are built in. Cards that need activation show an "activation required" warning until you check them off in Promos. When rates tie, activated rotating categories rank ahead of unactivated ones.
- **Benefit Radar:** the Promos tab is one urgency-first inbox for quarterly categories and verified calendar-based card benefits. Non-retroactive work comes first; other items follow by deadline. Open Benefit Radar to mark actions complete, use the quarterly-only filter, skip a period, hide benefits you do not use, or restore hidden and skipped work.
- **Shared completion status:** activation, enrollment, and benefit-use checkboxes stay synchronized across Benefit Radar, Benefits, and card recommendations. A completion remains in Benefit Radar until the period ends or for up to 30 days, whichever comes first, then remains in completion history for up to 24 months.
- **Recurring charge confirmations:** for four eligible monthly card benefits, confirm that a qualifying membership, subscription, or bill is charged to the card every month. The task leaves the active inbox immediately and remains manageable under Confirmed recurring charges in full Benefit Radar. Confirmation suppresses only that benefit's routine monthly reminder, never marks it used, and is reviewed again after six months. If you do not confirm within 30 days, monthly reminders return.
- **Priority tie-break** — when two cards earn the same, your hand-set card order decides (drag your true favorite to the top).
- **Location guessing** — optionally let the app read your location and guess the category from the nearest merchant (via OpenStreetMap; no API key, no tracking).
- **Everything is editable** — issuers change rules constantly. Tap ✎ on any card to override its rates, add custom cards, or adjust point valuations in Settings.
- **Quarterly reminders:** download a generic `.ics` calendar file with four recurring reminders and no card or activity data.
- **Per-device setups and setup links:** each person's setup lives in their own browser. A setup link carries cards, settings, benefit enrollments, recurring charge confirmations, items hidden from Benefit Radar, skipped periods, and current checkmarks. Imported recurring confirmations do not hide monthly reminders until confirmed again in Benefit Radar on the receiving device; completion history is omitted.

## Install on iPhone

1. Host `index.html` anywhere static — GitHub Pages works free:
   - Upload `index.html` to a repository.
   - Repo **Settings → Pages → Deploy from a branch → main / (root) → Save**.
   - Your app goes live at `https://<username>.github.io/<repo>/` in a minute or two.
2. Open that URL in **Safari** on your iPhone.
3. Pick your cards and set their priority order.
4. Tap **Share → Add to Home Screen**.

It launches full-screen with dark-mode support and safe-area padding for the notch/Dynamic Island. Android works too: open the URL in Chrome → menu → *Add to Home screen*.

## Sharing with family & friends

Send them the **plain URL** — nothing else. Each visitor gets a welcome screen, picks their own cards, and their setup is stored only on their own device. Your choices never affect theirs.

Two flavors of link exist:

| Link | What it does |
|---|---|
| Plain URL (`.../cardrouter/`) | Fresh start for a new person; remembers each device's own setup |
| Setup link (`.../cardrouter/#v2...`) | Imports a specific setup, removes the setup data from the address bar, and uses normal per-device storage |

Opening a setup link asks before replacing a setup already on that device. The link contains readable card and current-status data, so share the plain URL with other people and keep setup links private for your own backups.

## Using the app well

**Point valuations (Settings).** By default, transferable points (Chase UR, Amex MR, Citi TY, Capital One) are valued at 1.5¢ each and cash back at face value. If you redeem points differently — say, you only ever take 1¢ cash — lower the valuation and the rankings will honestly reflect it. This single setting changes many answers, so make it match reality.

**Portal vs. direct.** Several cards earn dramatically more through their bank's travel portal (e.g., Sapphire Reserve: 4x direct but 8x via Chase Travel; Prime Visa: 5% via Chase Travel but 1% direct). The rankings use the *direct* rate and the notes tell you when the portal beats it — read the note before booking travel.

**Caps.** Cards with spending caps (Amex Gold's $25k supermarket cap, Custom Cash's $500/cycle, rotating cards' $1,500/quarter) show a ⚠ note. The app doesn't track your spend against caps — it trusts you to know when you've blown through one.

**Benefit Radar completion.** Issuers do not report completion back to this app. Use the labeled checkboxes after you activate, enroll, select, or use a benefit. Uncheck any status to correct it. If you check a quarterly action after its cutoff, you are confirming that you completed it by the displayed deadline. Benefit Radar records both that deadline and the date you checked it. A completion remains in the main list until the period ends or for up to 30 days, whichever comes first, then remains in completion history for up to 24 months.

**Benefit Radar coverage.** Benefit Radar intentionally tracks only benefits with issuer-verified terms, a clear calendar reset, and a working issuer or partner page for the action. Other perks remain available in Benefits without becoming recurring tasks. Benefit terms were checked in August 2026 and can still change.

**Confirmed recurring charges.** The app can remember when you confirm that an eligible monthly membership, subscription, or bill is charged to the benefit's card. This suppresses only the routine monthly reminder. It does not mark the benefit used, verify a charge or statement credit, or replace enrollment. You confirm each charge again every six months; terms changes, card or enrollment removal, hiding, and setup imports require confirmation again.

**Quarterly upkeep (5 minutes, 4× a year).** At each quarter's start: activate rotating categories (Promos tab links), re-check the new categories are reflected (see below), and re-pick US Bank Cash+ choices if you hold it.

## Maintaining the rules data

Card rules drift. Three maintenance points:

1. **Any card's rates** — no code needed: tap ✎ on the card in the app and type the new rate (`3x` or `5%`). Overrides persist on your device.
2. **Rotating categories for a new quarter** — edit the `ROTATING` table near the top of the `<script>` in `index.html`:

```js
const ROTATING = {
  '2026-Q3': {
    freedom_flex: {cats:['gas','transit','entertain','united_way'], label:'Gas & EV, public transit, live entertainment, United Way donations'},
    discover_it:  {cats:['gas','flights','transit','drugstores'], label:'Gas & EV, airlines & transit, drugstores'},
  },
  '2026-Q4': null, // ← fill in when announced (usually mid-quarter before)
};
```

Valid category ids: `dining, groceries, gas, flights, hotels, transit, streaming, drugstores, online, entertain, phone, shipping, united_way, rent, other`.

3. **Quarterly action deadlines** — verify the `QUARTERLY_ACTIONS` table whenever issuer terms change. Freedom uses an exclusive cutoff on the 15th day of the quarter's final month, so the last activation day is the 14th. Cash+ closes five calendar days before quarter-end. A quarter-specific `actionEnds` value can override either policy when an issuer publishes a different date.

## Privacy

- No account, no server, no analytics, no cookies. The app is one static HTML file.
- Your card selections, benefit enrollments, and recurring charge confirmations (never card numbers, because the app doesn't know them) are stored in your browser's local storage on your device only.
- The only network calls are: (a) loading the page itself, and (b) one reverse-geocoding request to OpenStreetMap **only when you tap the location button**, sending coordinates and nothing else.
- The hosted file is public if you use GitHub Pages, but it contains only the generic card database — nothing about you.

## Limitations

- It recommends; it doesn't route. You still tap the card yourself.
- No logged-in promo scraping (Amex Offers, Chase Offers) — those live behind issuer logins, and automating them is fragile and against issuer terms. The Promos tab reminds you where to look; MaxRewards Gold automates it commercially if you want that.
- Benefit Radar completion and recurring-charge confirmation are manual. It cannot verify issuer activation, enrollment, selection, charges, or statement-credit usage.
- No spend-cap tracking.
- Location guessing is a guess — OpenStreetMap data quality varies by area.
- Clearing Safari website data wipes your setup — keep a setup link as backup.

## Tech notes

Single self-contained production `index.html` (no dependencies, no build step): vanilla JS, CSS custom properties with automatic dark mode, versioned `localStorage` persistence with verified session fallback, allowlisted config export via a compact base64url hash, generic `.ics` reminders with no card or activity data, browser-history Promos subviews, geolocation + [Nominatim](https://nominatim.org/) reverse geocoding. Works from any static host.

Pure Radar date, migration, task-building, and calendar helpers are exposed through the internal `CardRouterRadar` namespace. Serve the repository locally and open `tests/radar-tests.html` to run the dependency-free test harness.

## Background

This app is the pragmatic outcome of a bigger question: *could you build a true NFC "card router" that automatically pays with the optimal card at the terminal?* Short answer: not without becoming a card issuer — the merchant category code that determines "optimal" only reaches the **issuer** during authorization, never the phone at tap time, and Apple's Secure Element entitlements are limited to licensed payment providers. Curve, the one company that did true routing (by fronting your cards with its own), shut its US program in 2024 and was acquired by Lloyds in 2025. Hence: a butler, not a router.

## Disclaimer

Earn rates verified against public sources in July 2026 and **will go stale** — always confirm against your issuer's current terms. This project is not affiliated with, endorsed by, or connected to any card issuer or network. Nothing here is financial advice; card strategy is personal, and annual fees, sign-up bonuses, and redemption habits matter more than any single swipe.
