# Benefit Radar Consolidation and Recurring Charge Confirmation

**Status: Implemented and browser-verified; phone validation pending**

Benefit Radar is the single urgency-first action inbox in Promos. The former Quarterly Actions destination has been removed, while quarterly categories remain available as a complete filtered inventory. Eligible monthly benefits use an explicit, reversible recurring-charge confirmation instead of reminder-oriented setup language.

## Benefit Radar

- Use **Benefit Radar** in page titles, visible labels, accessible names, help text, tests, and documentation.
- Keep the Promos overview visually direct: **View all** sits beside **Promos & activations**, with no duplicate Benefit Radar heading, explanatory line, or generated urgency summary above the preview cards.
- Order the full inbox as Priority, Due within 30 days, Review recurring charges, Later, Recently completed, Confirmed recurring charges, then Hidden and completion history.
- Keep cadence in task metadata without splitting the main inbox into monthly, quarterly, or annual groups.
- Show a distinct **Quarterly categories** navigation row on the Promos overview only when applicable.
- Use a native **Quarterly only** checkbox in Benefit Radar. Checked shows the complete current-quarter inventory; unchecked shows all radar items. The filtered inventory includes incomplete, completed, skipped, closed, and temporarily unavailable current-quarter categories; incomplete work follows urgency ordering and completed work sorts last.
- Keep skipped quarterly categories visible and completable in quarterly-only mode.
- Keep **Download quarterly reminders** as a real download button on the overview and at the bottom of Benefit Radar.

## Recurring charge confirmation

- Allow only Amex Platinum Digital Entertainment, Sapphire Reserve Peloton, Business Platinum Wireless, and eligible monthly direct billing for Blue Cash Preferred Disney streaming. Each uses provider-specific qualification copy and its existing terms version.
- Present recurring setup as a compact direct action below the task footer, before Hide. Use **Recurring charge set up?** with a one-sentence direct-billing explanation and **Confirm setup**. A terms mismatch uses **Recurring charge still set up?**, concise changed-terms guidance, **Reconfirm**, and **Check updated terms** in place of the usual top-right benefit link label. Do not use a card-level disclosure, inline eligibility wall, modal, or new prompt-presentation preference; the existing external benefit link carries detailed eligibility terms.
- Confirmation suppresses only routine monthly use reminders. It never completes the benefit, changes enrollment, or creates history.
- Remove a newly confirmed charge from the Promos overview and active urgency groups immediately. Confirm with a polite Undo message instead of leaving a completed row in the action inbox.
- Show active records only in the flat **Confirmed recurring charges** section of full Benefit Radar, with confirmation date, review date, terms, and removal visible on every row.
- Review due records appear under **Review recurring charges** with **Yes, still recurring**, **Remove confirmation**, and the exact reminder-return date.
- Removal and confirmation use the existing reversible mutation mechanism. Undo restores persisted state plus review-session state only when the Promos visit token still matches.
- Card removal, enrollment removal, hiding, import, and terms changes continue to prevent silent reactivation.

## Secondary actions and navigation

- Use interval-specific skip labels such as **Skip August**, **Skip Q3**, **Skip Jan–Jun**, **Skip Jul–Dec**, and **Skip 2026**.
- Remove the More options disclosure. Show **Hide from Benefit Radar** directly as a quiet tertiary button in an attached secondary-action footer inside its benefit row. Pair it with “Stops reminders. Restore anytime from Hidden.” Keep the pair side by side at 390px and above, stacking only below 350px.
- Normalize legacy `{promosView:"quarterly"}` history to Benefit Radar with the quarterly filter active. Overview links push history; in-Radar filter changes replace the current entry; tab navigation resets to overview/all.
- Keep schema v3, recurring record formats, the `v2.` setup-link envelope, timing, import suspension, terms-version handling, and stale-tab protection unchanged.

## Accessibility and verification

- Recurring setup controls are direct buttons with unique benefit-and-card names; the quarterly-only filter is a native labeled checkbox with a polite result-count announcement.
- Benefit-and-card action names are unique, decorative chevrons are hidden from assistive technology, controls retain 44×44 minimum targets, and focus moves deterministically after confirmation, cancellation, removal, review, hiding, filter changes, and Undo. Focused controls are scrolled fully above the fixed bottom navigation.
- Responsive controls stack at narrow widths and high text zoom, and the Undo control is not removed while focused.
- The Promos header carries no global quarter label because the page mixes monthly, quarterly, half-year, and annual work. Current-quarter context appears only on the **Quarterly categories** row and quarterly-only view.
- The bottom navigation tracks the visual viewport from its top edge to avoid misplaced fixed-bottom rendering in iPhone WebKit browsers.
- The dependency-free browser harness passes 66 of 66 checks covering persistence, timing, full quarterly inventory, history compatibility, disclosure semantics, confirmation and removal, Undo, visit boundaries, suspension, focus, mobile viewport anchoring, modal behavior, and copy-critical UI states.
- Browser verification passes at 320px, 390×844, desktop, 200% zoom, and light and dark color schemes without horizontal overflow or console errors.
- Earlier engineering, product, accessibility, and copy reviews passed with no remaining P0–P2 findings. The latest overview hierarchy, 30-day heading, direct recurring setup, direct Hide footer, quarterly checkbox, and bottom-navigation focus clearance passed independent design/visual review with no remaining P0–P2 findings; final confirmation on the user’s phone is still pending.

Keep the work on `codex/credit-radar`. Preserve `PRODUCT.md`; do not push or merge before user approval.
