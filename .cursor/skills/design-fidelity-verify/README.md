# design-fidelity-verify

> Prove the running app matches its design spec by **measuring** rendered values — not by glancing at a screenshot.

This is the **second** of two composable skills. It consumes the design-spec table from [`figma-design-extract`](../figma-design-extract) and runs a bounded **vision + numeric feedback loop** (~3 iterations) that walks every spec row to a classified verdict, for **both web and mobile**.

## What it does

- **Preflight** the infra gates (env up, data shape, inspection tooling, build current, auth) before rebuilding. In practice most verify time goes here, not to the design diff.
- **Capture full-res** (web dpr ≥ 2 / mobile `scale: 1.0`) — blurry capture is the #1 reason drift slips through.
- **Numeric pass** — read the *actually rendered* values with a bundled reader and compare to the spec:
  - **Web:** `getComputedStyle` + `getBoundingClientRect` → [`scripts/web-style-read.js`](scripts/web-style-read.js), [`references/verify-web.md`](references/verify-web.md)
  - **Mobile:** the resolved style off the rendered React fiber, over Metro/CDP → [`scripts/rn-style-read.js`](scripts/rn-style-read.js), [`references/verify-mobile.md`](references/verify-mobile.md)
- **Classify, don't just diff.** Resolve every measured value back to a named token, then label the row `PASS` / `DRIFT` (naming both tokens) / `HARDCODED` (resolves to none) / `VARIANT` / `MISSING`, and tag whether the fix is theme-level or component-level → [`references/drift-classification.md`](references/drift-classification.md). A bare hex/px delta is not a finding.
- **Record navigation as a replayable flow** so every re-verify measures the same state.
- **Report residuals honestly** when a measurement channel is blocked, instead of claiming a false pass.

The reference files are loaded **on demand** — a web project never pulls the mobile mechanics and vice versa. The method is **tool-agnostic**; the reference files name specific MCPs only as examples. The one hard requirement is a channel that can evaluate JavaScript in the running app.

## Use it

Say "verify the design", "is this pixel-perfect", "check this against Figma", or run it right after building a screen with `figma-design-extract`. See [`SKILL.md`](SKILL.md) for the loop and [`examples/worked-example.md`](examples/worked-example.md) for a web + mobile run.

> **Track regressions with a baseline.** Commit the classified rows as a snapshot, and [`scripts/token-drift-diff.js`](scripts/token-drift-diff.js) will tell you which drift is *yours* (NEW, exit 1) versus what the app already had (PERSISTING). Without one, every run re-reports the existing drift as noise.

> **Complementary, not a replacement for visual regression.** The numeric pass verifies a *first build* (no baseline exists yet); for *ongoing* protection, snapshot the approved render as a baseline for a visual-regression tool (Playwright `toHaveScreenshot`, Chromatic, Percy, Applitools). A cheap structural check — Playwright `toMatchAriaSnapshot` (role/name/order) — pairs well with the element-mapping step.
