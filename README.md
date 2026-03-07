# Freelancer BizDev Dashboard

A private, offline-first business development dashboard for freelancers. Single HTML file — no build step, no server, no account required.

## Features

- **Pipeline kanban** — track leads, proposals, active projects, invoiced, and paid work; drag to reorder, keyboard accessible
- **Income tracker** — monthly bar chart with YTD total, best month, monthly average, and projected year-end; edit month-by-month manually
- **Time & capacity** — weekly hours by client, inline time logger, click-to-edit weekly hours
- **Next actions** — add/delete tasks manually with urgency levels; or describe them to AI
- **Ask AI** — describe changes in plain English and the dashboard updates automatically; works with Claude, Gemini, ChatGPT, Mistral, or Ollama
- **Undo** — one-level undo for any AI update
- **Settings** — profile, targets, currency, VAT, financial year end, AI providers, accent colours, data export/import
- **Privacy toggle** — hide all financial figures with one click
- **i18n** — English, Spanish, French, German, Italian; language change auto-switches currency

## Privacy & data

Everything lives in your browser's `localStorage`. Nothing is sent anywhere unless you actively use the Ask AI feature with a cloud provider API key. The dashboard works fully offline and without any AI key.

## Getting started

Download `index.html` and open it in any modern browser. That's it.

On first load you'll be walked through a short setup (name, currency, financial year end) and an optional guided tour.

## AI setup (optional)

Open Settings → AI Models and paste an API key for any supported provider:

| Provider | Where to get a key |
|---|---|
| Claude | console.anthropic.com |
| Gemini | aistudio.google.com |
| ChatGPT | platform.openai.com |
| Mistral | console.mistral.ai |
| Ollama | Run locally — no key needed |

Once a key is saved, the Ask AI panel lets you update your dashboard in plain English, e.g. _"I just landed a new project with Acme worth £4,500"_ or _"Move the Barnardo's project to invoiced"_.

## Keyboard accessibility

- **Pipeline cards** — Tab to focus, Enter/Space to open edit modal
- **Panel reorder** — Tab to drag handle, Arrow Up/Down to move
- **Settings accordion** — Tab to header, Enter/Space to open/close
- **Tour** — fully keyboard navigable, closes on Escape
- **All modals** — focus trapped, close on Escape, focus returns to trigger

## Exporting data

Settings → Data → Export JSON (full backup) or Export pipeline CSV.

## Tech

Vanilla HTML/CSS/JS, no framework, no build step. Chart.js loaded from CDN with SRI integrity hash. All data in `localStorage` under `bizdev-*` keys.

## Licence

MIT
