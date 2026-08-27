# Recurring Benefit Setups

**Status: Implemented, verified, and independently reviewed**

Implement user-confirmed recurring benefit setups inside the existing My Radar page. The feature suppresses only routine monthly use reminders, never enrollment or completion, and asks the user to reconfirm each setup every six months.

## State and business rules

- Allow only Amex Platinum Digital Entertainment, Sapphire Reserve Peloton, Business Platinum Wireless, and eligible monthly direct billing for Blue Cash Preferred Disney streaming.
- Store recurring setup confirmations separately from completions. Preserve both the confirmation instant and the user's local confirmation date.
- Review each setup after six local calendar months. Monthly use reminders remain suppressed for 30 calendar days after review becomes due, then return if the user does not reconfirm.
- Removing a card, removing enrollment, hiding a benefit, importing a setup, or changing relevant terms prevents silent reactivation.
- Never mark a benefit used automatically or add recurring confirmations to completion history.

## Persistence

- Use schema v3 while continuing to accept and migrate v1 and v2.
- Keep the existing `v2.` setup-link encoding envelope.
- Export recurring setup records but import them as suspended until locally reconfirmed.
- Keep prompt presentation preferences device-local and out of setup links.
- Preserve unsupported newer local state, including when an older tab attempts to save.

## My Radar experience

- Offer one inline recurring-payment suggestion at a time on an eligible enrolled monthly-use row.
- Show active confirmations in **Benefits with recurring payments**, with **Manage benefit setups** revealing terms, inactive records, and resume controls.
- Show due confirmations after Priority and Due Soon actions but before Later items under **Confirm recurring benefit setups**.
- Keep external links top-right, keep `Mark used` separate, and never create another route, modal, or individual benefit page.

## Verification and handoff

- The dependency-free browser harness passes 52 of 52 checks covering schema, timing, lifecycle, validation, import, focus, and UI states.
- The 320px, 390×844, and desktop layouts were verified in light and dark modes with no console errors or horizontal overflow.
- Independent engineering, product, accessibility, and copy reviews report no remaining P0-P2 findings.
- Keep the implementation on `codex/credit-radar`. Do not push or merge before user approval.
