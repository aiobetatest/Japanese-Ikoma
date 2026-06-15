# Project Guardrails — Japanese Practice app

**Read this at the start of every iteration.** This file captures hard rules learned the hard way. Skipping any of these has cost us versions, frustration, and trust.

---

## Rule 0 — No corner-cutting on cross-cutting changes

When a user reports a problem on screen X, **audit the pattern across every screen, mode, and view where that pattern occurs**. Do not just fix the one screenshot.

Bad: "user complained about Family Learn → fix Family Learn."
Good: "user complained about Family Learn → audit all 8 Shukudai Learn views (Counters/Numbers/Money/Time/Dates/Family/Professions/Places) → fix all of them at once."

**Trigger phrases that should make you audit-all-occurrences instead of one-fix:**
- "consistent", "match", "same as", "uniform", "all", "throughout", "everywhere"
- Anything about typography, layout, fonts, colours, spacing
- Anything about feature parity (e.g., "should also have romaji")
- Anything visual the user describes as "looks weird / different / off"

**Concrete process** when you receive such a complaint:
1. Identify what component / pattern is at fault (e.g., `.ltable` vs `.review-row`).
2. Grep the template for every place that pattern is used.
3. List them explicitly before patching.
4. Patch all of them in one version bump.
5. Verify each location in the build output.

If you're unsure whether the user means "this one screen" or "all of them", **ask once before starting**. Don't ask after.

---

## Rule 1 — Cross-device testing is non-negotiable

Every change MUST work seamlessly on:
- **iOS Safari** (regular browser tab)
- **iOS PWA** (Add to Home Screen — different status-bar and viewport behaviour)
- **Android Chrome** (latest stock browser)
- **Samsung Internet** (significant Samsung Galaxy user base, has subtle CSS / TTS quirks)
- **Firefox Android** (smaller share but still important)
- **Desktop browsers** (Chrome / Safari / Firefox / Edge — the GitHub Pages URL is shareable)

**Checklist before declaring any version "done":**

### CSS
- [ ] No `-webkit-` only property without a non-prefixed fallback (or `@supports` gate)
- [ ] No `backdrop-filter` without an opaque colour fallback
- [ ] No gradient text without a solid `color:` fallback PLUS `@supports` for `background-clip: text`
- [ ] No `aspect-ratio` without checking browser support (use fallback padding-bottom if needed)
- [ ] No `position: sticky` element near the top without `env(safe-area-inset-top)` padding
- [ ] All touch targets ≥ 44 px on mobile
- [ ] All `input`, `select`, `textarea` use `font-size: 16px` on mobile to prevent iOS zoom-on-focus
- [ ] All hover effects gated by `@media (hover: hover) and (pointer: fine)` so touch devices don't see stuck hover states

### JS
- [ ] `speechSynthesis.getVoices()` has retry logic (Android often returns `[]` on first call)
- [ ] Voice picker has a default + a hint banner for "no Japanese voice installed"
- [ ] Audio unlock on first user gesture (`pointerdown`/`touchstart`/`click` once)
- [ ] Canvas drawing uses Pointer Events when available, with touch+mouse fallback
- [ ] `localStorage` writes wrapped in try/catch (private mode can throw)
- [ ] No reliance on optional chaining `?.` in places that need to work on very old browsers (Samsung Internet 9 etc.)
- [ ] Every `getElementById` call followed by a null check before use

### iOS-specific
- [ ] `<meta name="viewport" ... viewport-fit=cover>` for notch devices
- [ ] `<meta name="apple-mobile-web-app-capable" content="yes">`
- [ ] Header padding respects `env(safe-area-inset-top)`
- [ ] Container padding respects `env(safe-area-inset-left/right)` in landscape
- [ ] First TTS call doesn't auto-play (iOS blocks it) — first audio must be on user tap

### Android-specific
- [ ] Voice retry loop (Samsung Internet sometimes takes ~1 s to populate `getVoices()`)
- [ ] Test that gradient text falls back to solid colour on older Samsung Internet
- [ ] Test that canvas drawing doesn't trigger page scroll (`touch-action: none` set in JS)

### Functional
- [ ] All `display: none` toggles tested in every relevant mode (no element accidentally hidden in a mode where the user needs it)
- [ ] All states persist correctly across page reloads
- [ ] Empty / edge states render without crashing
- [ ] Switching between modes doesn't leave stale UI from the previous mode

---

## Rule 2 — Component reuse beats parallel implementations

The app has a canonical "row" component: `.review-row` with `.ren` (English/prompt), `.rjpwrap` containing `.rjp` (Japanese with gradient) + `.rromaji` (italic muted romaji), and `.rspeak` (speaker button).

**Use it everywhere a row of "label + Japanese + audio" is displayed.** Do not create parallel implementations like `.ltable` or `.counter-table` — they will inevitably drift from `.review-row`'s typography.

If a special variant is needed (e.g., yellow highlight for irregular readings), add a modifier class (`.learn-row.irregular`) that overrides specific properties — never fork the whole component.

---

## Rule 3 — Versioning discipline

Every change ships as a version. The version number in the footer is the source of truth.

- **PATCH** (1.0.0 → 1.0.1): bug fix, typo, polish, content addition inside existing structure.
- **MINOR** (1.0.0 → 1.1.0): new feature, new content category, new mode.
- **MAJOR** (1.0.0 → 2.0.0): architectural change.

Every version MUST:
1. Bump `appVersion` in `data/manifest.json`.
2. Add an entry at the top of `CHANGELOG.md` dated today, listing every change.
3. Be built via `build.py` (never hand-edit the HTML).
4. Pass the cross-device checklist above before being declared done.

---

## Rule 4 — Data integrity

- All vocab/sentences/shukudai items have **stable IDs** (`vocab:N:jp`, `sent:N:idx`, `shukudai:cat:idx`). Never change an existing ID — Leitner box history is keyed by ID.
- `manifest.json` counts are auto-synced by `build.py`. Don't hand-edit them.
- When adding new content (e.g., a new Lesson), append; never re-number existing items.

---

## Rule 5 — The build pipeline is the only path to deploy

1. JSONs (`data/*.json`) are the source of truth.
2. `build.py` composes them into `index.html` and `Japanese Practice.html` from the template at `outputs/templates/app.html.template`.
3. The user uploads `index.html` to their GitHub repo → GitHub Pages serves it.

**Never** hand-edit `Japanese Practice.html` or `index.html` directly. Those are build artefacts.

When making changes:
- Data → edit the relevant JSON, run `build.py`.
- UI / behaviour → edit the template, run `build.py`.
- Never touch the rendered HTML directly.

---

## Rule 6 — Refresh workflow for new lesson uploads

When the user uploads new PDFs (e.g., Dai_Ka 12.pdf) and says "refresh":

1. Read `data/manifest.json` to see what's been processed.
2. Scan the workspace for new/changed PDFs (compare size + mtime against manifest).
3. For each new PDF: render pages, read them via image OCR, extract vocab/sentences/drills.
4. **Append** to the relevant JSON files (never replace).
5. Update `manifest.json` with new file metadata + lesson coverage.
6. Bump version (MINOR for new lesson content).
7. Run `build.py`.
8. Report back: "added N vocab + M sentences from Dai_Ka 12.pdf".

---

## Rule 7 — When in doubt, ask once before starting; never ask after

If a request is ambiguous, ask exactly one clarifying question with concrete options. After you start, no more clarifying questions — finish what's been agreed.

---

## Common pitfalls (collected from past versions)

| Pitfall | Lesson |
|---|---|
| Edit tool truncates large files | Use `Write` for full file replacement, or split changes into small Edits |
| Bash `!` history expansion mangles file content | `set +H` at the start of every bash invocation |
| iOS PWA status-bar overlap | Header MUST have `padding-top: env(safe-area-inset-top)` |
| Android voice empty on first call | Voice loader needs retry loop |
| Hover state stuck on touch devices | Gate hover effects with `@media (hover: hover)` |
| Gradient text invisible on Samsung Internet | Solid `color:` fallback + `@supports` for transparent fill |
| Element hidden in mode where user needs it | When hiding rows by mode, list every mode and confirm the element isn't needed |
| Parallel components drift | Reuse `.review-row` — don't fork |
| Cut-corner fix to one screen | Audit all occurrences of the pattern before patching |
| Manifest counts go stale | `build.py` recomputes them from data on every build |

---

## Skill invocation note for Claude

When picking up this project at the start of any new session or new turn:
1. Read this file (`PROJECT_GUARDRAILS.md`) first.
2. Read `CHANGELOG.md` to see what version we're on and what just changed.
3. Read `data/manifest.json` to know what content is in.
4. Then address the user's request, with these guardrails active.
