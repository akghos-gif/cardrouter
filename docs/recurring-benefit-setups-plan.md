# Benefit Radar Consolidation and Recurring Charge Confirmation

**Status: Finalized, implemented, verified, and independently reviewed**

Benefit Radar is the single urgency-first action inbox in Promos. The former Quarterly Actions destination has been removed, while quarterly categories remain available as a complete filtered inventory. Eligible monthly benefits use an explicit, reversible recurring-charge confirmation instead of reminder-oriented setup language.

## Benefit Radar

- Use **Benefit Radar** in page titles, visible labels, accessible names, help text, tests, and documentation.
- Order the full inbox as Priority, Due soon, Review recurring charges, Later, Recently completed, Confirmed recurring charges, then Hidden and completion history.
- Keep cadence in task metadata without splitting the main inbox into monthly, quarterly, or annual groups.
- Show a distinct **Quarterly categories** navigation row on the Promos overview only when applicable.
- Use the stateful **Quarterly only** / **Show all** filter in Benefit Radar. The filtered inventory includes incomplete, completed, skipped, closed, and temporarily unavailable current-quarter categories; incomplete work follows urgency ordering and completed work sorts last.
- Keep skipped quarterly categories visible and completable in quarterly-only mode.
- Keep **Download quarterly reminders** as a real download button on the overview and at the bottom of Benefit Radar.

## Recurring charge confirmation

- Allow only Amex Platinum Digital Entertainment, Sapphire Reserve Peloton, Business Platinum Wireless, and eligible monthly direct billing for Blue Cash Preferred Disney streaming. Each uses provider-specific qualification copy and its existing terms version.
- Present **Confirm recurring charge** as a full-width disclosure below the task footer. A terms mismatch uses **Review recurring charge**. Nothing auto-expands and no new prompt-presentation preference is written.
- Confirmation suppresses only routine monthly use reminders. It never completes the benefit, changes enrollment, or creates history.
- Retain a neutral **Recurring charge confirmed** row in its original overview slot or urgency group for the current Promos visit. It shows the review date and a direct **Remove confirmation** action.
- End visit-scoped state on reload or when leaving Promos. Later visits show active records in the flat **Confirmed recurring charges** section, with confirmation date, review date, terms, and removal visible on every row.
- Review due records appear under **Review recurring charges** with **Yes, still recurring**, **Remove confirmation**, and the exact reminder-return date.
- Removal and confirmation use the existing reversible mutation mechanism. Undo restores persisted state plus visit-scoped confirmation and review state only when the Promos visit token still matches.
- Card removal, enrollment removal, hiding, import, and terms changes continue to prevent silent reactivation.

## Secondary actions and navigation

- Use interval-specific skip labels such as **Skip August**, **Skip Q3**, **Skip Jan–Jun**, **Skip Jul–Dec**, and **Skip 2026**.
- Put **Hide from Benefit Radar** under a native **More options** disclosure and explain that it stops all reminders until restored from Hidden.
- Normalize legacy `{promosView:"quarterly"}` history to Benefit Radar with the quarterly filter active. Overview links push history; in-Radar filter changes replace the current entry; tab navigation resets to overview/all.
- Keep schema v3, recurring record formats, the `v2.` setup-link envelope, timing, import suspension, terms-version handling, and stale-tab protection unchanged.

## Accessibility and verification

- Recurring and More options disclosures synchronize `aria-expanded` and `aria-controls`; the quarterly filter uses `aria-pressed` and a polite result-count announcement.
- Benefit-and-card action names are unique, decorative chevrons are hidden from assistive technology, controls retain 44×44 minimum targets, and focus moves deterministically after confirmation, cancellation, removal, review, hiding, filter changes, and Undo.
- Responsive controls stack at narrow widths and high text zoom, and the Undo control is not removed while focused.
- The dependency-free browser harness passes 65 of 65 checks covering persistence, timing, full quarterly inventory, history compatibility, disclosure semantics, confirmation and removal, Undo, visit boundaries, suspension, focus, modal behavior, and copy-critical UI states.
- Browser verification passes at 320px, 390×844, desktop, 200% zoom, and light and dark color schemes without horizontal overflow or console errors.
- Independent engineering, product, accessibility, and copy reviews pass with no remaining P0–P2 findings.

Keep the work on `codex/credit-radar`. Preserve `PRODUCT.md`; do not push or merge before user approval.
