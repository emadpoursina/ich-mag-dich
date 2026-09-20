## Goal
Add one small, quiet closing credit to `index.html` so the page does not end abruptly after the no-path screen. The credit must be visible on every screen.

## Requirements (from task)
- Exactly one new footer element containing the exact German text: `Gebaut mit ❤️ — für dich`
- Styled small and muted (reuse existing pastel style variables, e.g. `--muted`).
- Must not overlap or push the existing screens.
- German only. No new files, no libraries, no network calls, no JavaScript changes.

## Change
1. In the `<style>` block, add a `.credit` rule:
   - `position: fixed` at the bottom center so it never displaces the screens in flow.
   - small `font-size`, muted `color: var(--muted)`, `pointer-events: none` so taps pass through.
   - offset with `env(safe-area-inset-bottom)` for phones.
2. Reserve vertical space for the fixed credit by extending the existing `body` padding with a
   bottom value (`calc(40px + env(safe-area-inset-bottom))`), so the credit cannot overlap
   screen content.
3. Add a single `<footer class="credit">Gebaut mit ❤️ — für dich</footer>` in `<body>`, after the
   last screen section (`#s-no`) and before the `<script>`, so it is present on every screen.

## Out of scope
- No changes to the quiz questions, rewards, reveal, ask, yes or no screens.
- No changes to any file other than `index.html` (plus this task's spec notes).
