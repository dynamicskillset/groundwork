# BizDev Dashboard — Plan

## Completed

### Core Dashboard
- [x] Single-file vanilla JS dashboard (index.html)
- [x] Demo / Live mode switching with onboarding flow
- [x] LocalStorage persistence (`bizdev-*` keys)
- [x] Pipeline kanban (5 columns: Leads, Proposals, Active, Invoiced, Paid)
- [x] Drag-and-drop pipeline cards + keyboard activation (Enter/Space)
- [x] Pipeline card edit/delete modal with inline confirm
- [x] Income section with Chart.js bar chart (YTD, best month, projected year-end)
- [x] Time & Capacity section with client bars and log-time accordion
- [x] Next Actions section
- [x] Ask AI section (Claude, Gemini, ChatGPT, Mistral, Ollama)
- [x] Panel drag-to-reorder

### Quality & Accessibility
- [x] XSS prevention via escapeHtml() throughout
- [x] Focus trap (trapFocus) on all modals
- [x] Keyboard navigation for pipeline cards
- [x] Screen reader only labels (.sr-only)
- [x] Focus-visible styles for keyboard nav
- [x] Mobile pipeline (scroll-snap horizontal)
- [x] Progress bar via transform:scaleX (no layout thrashing)
- [x] Accordion via max-height transition
- [x] SRI hash on Chart.js CDN script
- [x] confirm()/alert() replaced with inline confirm patterns
- [x] Dark-mode danger colours (CSS tokens)
- [x] Chart axis/grid colours from CSS tokens
- [x] Accent colour legibility (accentNeedsDarkText + --btn-on-accent)

### Features
- [x] Currency formatting (always 2 dp, dynamic currency symbol)
- [x] Privacy toggle (currency symbol with strikethrough when hidden)
- [x] Settings — Profile & Targets editing (name, role, currency, target, VAT, year-end, YTD)
- [x] Settings — Year End handling (income reset, archived to action note)
- [x] Settings — AI Models (5 providers + Ollama)
- [x] Settings — Appearance (accent colours, default yellow)
- [x] Settings — Data (export/import JSON, reset)
- [x] i18n (English, Spanish, French, German, Italian)
- [x] Language switcher in Demo header; Language field in Settings Profile
- [x] Language change auto-sets currency to € (non-English), £ reverts on English
- [x] Manual action add/delete (+ button + inline form, delete × on hover)
- [x] Dashboard usable without AI API key
- [x] Ask AI multilingual (system prompt updated)
- [x] Guided tour with scrollIntoView and all steps complete
- [x] Remove "Reset to defaults" from Ask AI panel (permanent)
- [x] Demo mode suppresses "Last update" in Ask AI panel
- [x] System prompt schema updated (paid column, correct income schema)

## Pending / Nice-to-have

- [x] Income manual editing (month-by-month actuals without AI)
- [x] Pipeline column totals in pipeline header (already implemented)
- [x] Tour translations (GUIDE_STEPS now uses t() for all 5 languages)
- [x] Tour tooltip positioning — 4-sided (below/above/right/left) + centred fallback
- [x] Keyboard-accessible panel reorder (Tab to handle, Arrow keys to move)
- [x] Export as CSV (pipeline CSV export added to Data settings)
- [x] AI error messages translated (parseError, genericError in all 5 languages)
- [x] Undo last AI update (snapshot before each call; Undo button in chat footer)
- [x] Responsive typography (clamp() on body, h1, stat values, capacity hours)
- [x] Week hours editor in Capacity (click the hours number to edit inline)
- [x] Dynamic `<html lang>` attribute (updated on init and on language change)
- [x] Descriptive page title (BizDev Dashboard)
- [x] `aria-live="polite"` on chat status element (#lastUpdate)
- [x] `role="alert"` on settings import status element
- [x] Touch targets: `.chat-gear`, `.chat-footer button`, `.action-delete`, `.action-row button` all min 44px
- [x] `.action-delete` reveals on keyboard focus-visible (not just hover)
- [x] All form labels now have matching `for`/`id` pairs (onboarding, settings, pipeline modal, income months)
- [x] `urgencyLabel` translation key added to all 5 languages
- [x] `aria-expanded` + `aria-controls` on all collapsible toggles (log time, add action, income edit)
- [x] Settings accordion headers: `role="button"`, `tabindex="0"`, `aria-expanded`, keyboard activation (Enter/Space), focus-visible style
- [x] Timer +/- buttons: `aria-label`; duration display: `aria-live="polite"`
- [x] Tour tooltip positioning bug fixed: `scrollY` was incorrectly added to `position:fixed` coordinates — tooltip now correctly stays within viewport on scrolled pages (fixes "Ask AI step stuck" bug)
- [x] `scrollIntoView` changed to `instant` so element position is accurate when tooltip is placed
- [x] Skip-to-main-content link added (visible on focus, styled with accent colour)
- [x] Section `aria-label` attributes set in `renderAll()` and kept in sync with current language
- [x] Income chart canvas: `role="img"` and `aria-label` with average monthly income
- [x] Tour welcome text updated: explains offline/privacy-by-design, AI is optional
- [x] `.modal-close` touch target fixed (44×44px with padding)
- [x] `undoBtn` inline `padding:0` removed (inherits `.chat-footer button` min-height)
- [x] `.btn-danger` `color: #fff` replaced with `var(--danger-text, #fff)`
- [x] `#prof-saved` "Saved ✓" gets `role="status"` for screen reader announcement
- [x] Inline confirmation spans (`settingsImportConfirm`, `yearEndConfirm`, `clearLiveConfirm`, `pf-delete-confirm`) get `role="alert"` so confirmations are announced when revealed
- [x] Skip link CSS added; section aria-labels set in renderAll()
- [x] Input attributes hardened: `autocomplete`, `inputmode`, `spellcheck`, `pattern`, `min`/`max` added across all forms (settings, onboarding, pipeline, income months, week-hours editor, API keys, Ollama fields)
- [x] `newActionText` gets `aria-label` and `autocomplete="off"`
- [x] Onboarding action rows get `aria-label` on both text input and urgency select
- [x] `onboarding-row` grid uses `repeat(auto-fit, minmax(180px, 1fr))` — wraps properly on narrow viewports
- [x] `<meta name="description">` added
- [x] `will-change: transform` on `.progress-fill` and `.spinner` for compositor hints
- [x] `saveData()` wrapped in try-catch for QuotaExceededError
- [x] `handleImport`: added `reader.onerror` handler, distinct storage-full error, status color reset on success
- [x] `<noscript>` fallback added
- [x] `aria-invalid` + `aria-describedby` on validated inputs (onboarding name/role, pipeline client); set/cleared on validation; visual CSS rule for invalid state
- [x] Validation errors now move focus to the invalid field
- [x] `trapFocus` bug fix: Escape handler now calls cleanup() before removing modal — event listeners no longer leak, focus always returns to trigger
- [x] `trapFocus` bug fix: guide tooltip couldn't close via Escape (not inside `.modal-overlay`) — fixed with optional `onEscape` callback; guide passes its own `cleanup` function
