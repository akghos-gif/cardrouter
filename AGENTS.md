# CardRouter repository guidance

## Start here

- Read `README.md` for product behavior, maintenance notes, privacy constraints, and the test entry point.
- Read `PRODUCT.md` before making product, copy, interaction, or visual-design decisions.
- For Benefit Radar work, also read `docs/recurring-benefit-setups-plan.md` and inspect the current implementation and tests rather than relying on old task history.

## Architecture and data

- Keep the production app dependency-free and static. `index.html` contains the production HTML, CSS, and JavaScript; do not add a framework, package manager, server, or build step without explicit approval.
- Preserve local-first privacy: no accounts, analytics, issuer credentials, card numbers, or remote storage. Do not add network calls beyond behavior already documented in `README.md` without explicit approval.
- Treat stored and shared setup data as user data. Preserve schema migration, import/export validation, stale-tab protection, and backward compatibility when changing persistence.
- Verify card benefits, deadlines, eligibility rules, and external action links against current primary issuer or partner sources before changing rules data. Prefer direct enrollment, activation, or terms destinations over generic marketing pages.

## Product and interface quality

- Follow the principles in `PRODUCT.md`: show the next useful action, reveal detail progressively, earn interruptions, make value concrete, and preserve local-first privacy.
- Keep the interface calm, precise, and restrained. Avoid noisy dashboards, repeated controls, unexplained urgency, and copy that implies CardRouter can verify issuer activity.
- Target WCAG 2.2 AA. Preserve keyboard and screen-reader semantics, visible focus, color-independent states, reduced-motion behavior, and touch targets of at least 44 by 44 CSS pixels.
- For user-interface changes, verify narrow mobile layouts (including 320px and 390x844), desktop, 200% text zoom, light and dark modes, no horizontal overflow, and no console errors. Pay particular attention to iOS Safari scrolling, focus, overlays, and bottom-navigation anchoring.

## Verification and documentation

- Serve the repository locally and run every check in `tests/radar-tests.html` after behavior, persistence, navigation, or interface changes. There is no build step.
- Add or update regression coverage for changed behavior. Do not weaken existing assertions just to make a change pass.
- Update `README.md` when user-facing behavior, rules maintenance, privacy, storage, or setup changes. Update the focused plan when its implemented behavior or handoff status changes.

## Git workflow

- Preserve unrelated user changes and inspect `git status` before editing or committing.
- Use a `codex/` feature branch for new work. Do not force-push, merge, close a pull request, or delete a branch without explicit user approval.
- Push only when the user has explicitly approved it. Before pushing, review the diff, run relevant verification, and keep generated or temporary artifacts out of commits.
