# Handoff

## Session 4 — 2026-03-07

### What was done
- Dynamic `<html lang>` attribute: `setLang()` now updates `document.documentElement.lang`; `init()` sets it on page load from stored preference — screen readers now announce the correct language
- Page title updated from "Dashboard" to "BizDev Dashboard"
- `aria-live="polite" aria-atomic="true"` added to `#lastUpdate` (chat status) — screen readers now announce "Thinking…", errors, and success messages
- `role="alert"` added to `#settingsImportStatus` — import success/error now announced to screen readers
- Touch targets hardened: `.chat-gear`, `.chat-footer button`, `.action-delete`, `.action-row button` now all meet 44×44px minimum
- `.action-delete` button now also reveals on `:focus-visible` (not hover-only)
- All form `<label>` elements now have matching `for`/`id` associations: onboarding step 1 (name, role, currency, yearend), step 2 (target, vatnum, vatrate), settings VAT fields, Ollama fields, pipeline modal (client, project, value, dayrate, notes), income month inputs (dynamic IDs `income-month-{i}`)
- `urgencyLabel` translation key added to all 5 languages for action priority select `aria-label`
- `aria-expanded`/`aria-controls` added to all collapsible toggle buttons: Log time accordion, Add action form, Income month editor — state kept in sync on toggle and after programmatic changes
- Settings accordion headers converted to keyboard-navigable: `role="button"`, `tabindex="0"`, `aria-expanded`, `aria-controls`, Enter/Space activation, `:focus-visible` outline
- Timer +/- buttons: `aria-label="Increase/Decrease time by 15 minutes"`; duration display: `aria-live="polite"` so screen readers announce changes
- `.modal-close` buttons enlarged to 44×44px min touch target
- `undoBtn` inline `padding:0` removed — inherits chat-footer button min-height
- `.btn-danger` hardcoded `color: #fff` replaced with `var(--danger-text, #fff)`
- `#prof-saved` "Saved ✓" gets `role="status"` — announced to screen readers on save
- All four inline confirmation spans get `role="alert"`: import confirm, year-end confirm, clear data confirm, pipeline delete confirm — screen readers now announce the confirmation prompt when it appears
- Skip link (`<a class="skip-link">`) with CSS: hidden off-screen, appears on focus
- Input hardening across all forms:
  - `autocomplete="name"` on name fields, `autocomplete="organization-title"` on role fields
  - `autocomplete="off"` on VAT number, VAT rate, year-end, YTD, target, API keys, Ollama URL/model
  - `spellcheck="false"` on VAT number, API keys, Ollama URL/model (prevents red squiggles on technical values)
  - `inputmode="numeric"` on all integer number fields; `inputmode="decimal"` on income month amounts
  - `pattern="[0-9]{2}/[0-9]{2}"` on year-end date fields
  - `min="0" max="100"` on VAT rate fields
  - `aria-label` + `inputmode` + `autocomplete` on dynamically created week-hours editor input

- **Bug fix**: Tour tooltip positioning — `position:fixed` tooltip was incorrectly having `window.scrollY` added to all coordinates. Steps at the bottom of the page (e.g. "Ask AI") had the tooltip pushed far off-screen, with no visible Next button. Removed all `sy` additions; the tooltip now stays on-screen regardless of scroll position.
- `scrollIntoView` changed to `behavior:'instant'` so `getBoundingClientRect()` reads accurate coords immediately after scroll
- Skip link added (`<a href="#main-content" class="skip-link">`) — appears on Tab focus, styled with accent colour
- `<main id="main-content">` target for skip link
- Section `aria-label` attributes now set/updated in `renderAll()` for all 5 sections (pipeline, income, capacity, actions, chat)
- Income `<canvas>` now has `role="img"` and `aria-label` including the monthly average value
- Tour welcome step text updated in all 5 languages: data lives on device, offline, AI is optional

- `newActionText` input: added `aria-label` (was placeholder-only, invisible to screen readers) and `autocomplete="off"`
- Onboarding action rows: `aria-label="Action N"` on text input, `aria-label="Priority for action N"` on urgency select
- `.onboarding-row` grid: changed from hard `1fr 1fr` to `repeat(auto-fit, minmax(180px, 1fr))` — wraps to single column on narrow viewports instead of squishing
- `<meta name="description">` added
- `will-change: transform` on `.progress-fill` and `.spinner` — promotes to compositor layer, avoids repaints on animation
- `saveData()` now catches `QuotaExceededError` / `NS_ERROR_DOM_QUOTA_REACHED` with `console.warn` (silent to user, prevents uncaught exception)
- `handleImport` hardened: `reader.onerror` handler added; storage-full distinguished from schema error with own message; status element color reset to `var(--teal)` on success (was staying red after a prior failed import)
- `<noscript>` element added — shows readable error message if JS is disabled
- `aria-invalid="true"` set on invalid inputs when validation fails, removed on success; `aria-describedby` links inputs to their error elements; CSS rule adds red border on `[aria-invalid="true"]`; focus moves to the first invalid field on form submit
- **`trapFocus` bug fix (event listener leak)**: Escape handler previously called `container.closest('.modal-overlay')?.remove()` without calling cleanup — document-level `keydown` listener was never removed and focus was never restored to trigger. Fixed: extracted shared `cleanup()` function; Escape now calls `cleanup()` first, then removes modal.
- **`trapFocus` bug fix (guide Escape)**: Guide tooltip is appended directly to `<body>` (not inside `.modal-overlay`), so old Escape handler silently did nothing — guide was impossible to close with keyboard. Fixed: added optional `onEscape` callback to `trapFocus`; guide passes its own `cleanup` function so Escape correctly tears down overlay, tooltip, and highlight.

### Current state
All audit recommendations and planned features are complete. Dashboard is fully i18n'd, keyboard-accessible, usable without AI, and resilient.

### Next steps
- No outstanding items from the original audit or plan
- Possible future: multi-currency income chart, client notes, recurring income entries

### Watch out for
- All PLAN.md items are checked off — verify before starting new work that you're not duplicating
- `lastDataSnapshot` is single-level undo only (last AI call); cleared after use

## Session 3 — 2026-03-07

### What was done
- Keyboard panel reorder: drag handles now keyboard-accessible (Tab to focus, ↑/↓ to move)
- `section:focus-within` makes handle visible when section is keyboard-focused
- CSV export: "Export pipeline CSV" button added to Data settings (all 5 columns, quoted fields)
- Removed last two `alert()` calls from handleImport; replaced with `#settingsImportStatus` element in modal
- Tour fully translated (all 5 languages): `getGuideSteps()` function uses `t()` for all step titles and text
- Tour tooltip 4-sided positioning: picks best side (below/above/right/left) by available space; centres when element fills screen
- Tour tooltip z-index raised to 920 (above guide-highlighted element at 910)
- AI error messages (`parseError`, `genericError`) added to all 5 language objects; `handleChatUpdate` uses `t()`
- Pipeline column totals confirmed already implemented (PLAN.md updated)

### Current state
All original audit recommendations addressed. Dashboard is fully i18n'd across all 5 languages including tour, error messages, and all UI strings. No remaining `alert()`/`confirm()` calls. Keyboard accessible throughout.

### Next steps
- Undo last AI update (complex — would need a DATA snapshot before each AI call)
- Responsive typography (clamp-based fluid font sizes)
- Consider adding week hours editor to Capacity (currently fixed at 35h, only editable by AI)

## Session 2 — 2026-03-07

### What was done
- Completed i18n for renderCapacity(), renderActions(), renderChat() — all strings use t()
- Removed "Reset to defaults" button from Ask AI panel permanently; cleaned from all translations
- No-key state in Ask AI now shows inline message with link; dashboard works without AI key
- Demo mode suppresses "Last update" text in Ask AI box
- Manual action add/delete — + button with inline form, hover-reveal × delete button per action
- Language switcher added to Settings Profile & Targets section (for live mode)
- setLang() auto-switches currency: non-English → €, English → £ (both directions)
- Tour steps now scroll highlighted element into view (scrollIntoView)
- AI system prompt updated: multilingual support, correct income schema, added 'paid' pipeline column
- Default accent colour changed to yellow (Aurora Yellow #ebcb8b moved to ACCENT_COLORS[0])
- Income manual editing — "Edit months" toggle reveals 12 number inputs, updates chart live
- Onboarding live data initialisation now includes paid: [] in pipeline
- noActionsEmpty translations updated in all languages to mention manual + button
- Project management files created: CLAUDE.md, PLAN.md, HANDOFF.md, slash commands in .claude/commands/

### Current state
All major audit recommendations are addressed. Dashboard is fully usable without an AI key. i18n covers all 5 languages throughout all render functions.

### Next steps
- Tour translations (GUIDE_STEPS titles/text still English-only)
- Keyboard-accessible panel reorder (drag handles only work with mouse)
- Export as CSV option
- Responsive typography (clamp-based fluid font sizes)
- Undo last AI update

### Watch out for
- `incomeEditOpen` is a module-level `let` — it persists across renderIncome() calls, which is intentional
- setLang() in header only auto-switches currency for €/£; Settings profile save does NOT auto-switch (user's explicit currency choice is respected)
- TRANSLATIONS object must have all keys in all 5 languages; missing key silently falls back to key string
- Pipeline system prompt schema now includes 'paid' column — keep in sync if adding more columns
