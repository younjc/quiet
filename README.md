# Quiet — a private journal

A single-file, local-first personal journal with AI-powered insights. No accounts, no cloud, no data ever leaves your machine (except to your own AI server).

---

## What it is

Quiet is a self-contained HTML file you open directly in your browser. Everything is stored in your browser's `localStorage`. The only network calls it makes are to your own local AI server (LM Studio or Open WebUI).

---

## Getting started

1. Save `quiet-journal.html` to your computer
2. Open it in any modern browser (double-click, or drag it into a browser tab)
3. The Settings panel will open automatically on first launch
4. Configure your AI server connection (see below)
5. Start writing

> Do not open it inside Claude.ai — the embedded preview can't reach your local AI server due to browser security restrictions. Always open it as a local file.

---

## AI server setup

Quiet works with any OpenAI-compatible local AI server. Two common options:

### LM Studio
- Download from [lmstudio.ai](https://lmstudio.ai)
- Load a model, then enable the local server under the **Local Server** tab
- Base URL: `http://localhost:1234/v1`
- API key: leave blank
- Model name: leave blank (uses whatever is loaded), or paste the model ID

### Open WebUI
- Base URL: `http://your-server-address:3000/api` (replace with your actual host, e.g. `http://ubuntu.local:3000/api`)
- API key: generate one at **Settings → Account → API Keys** in Open WebUI. If you don't see that section, an admin needs to enable it at **Admin Panel → Settings → General → Enable API Keys**
- Model name: use the Ollama model ID exactly as shown in Open WebUI (e.g. `gemma3:12b`). You can find all available IDs by visiting `http://your-server:3000/api/models` in your browser

### Finding your model name
Visit `http://your-server/api/models` in your browser and look for the `"id"` field on each model. Copy that value exactly into the Model name field in Settings.

---

## Sections

### Dashboard
Today's summary across all tracked areas: mood score, food score, exercise minutes, current cycle phase, overdue relationships, and tasks due today. Includes sparkline charts for the last 14 days and a daily AI-generated insight that synthesizes patterns across all domains.

### Journal
Daily notes with basic rich text (bold, italic, lists). After saving, the AI analyzes each entry and returns a mood score (1–10), a sentiment classification (Thriving / Stable / Low / Depressed), and a short thematic reflection. A mood trend chart shows the last 30 days.

### Food
Log meals by type (breakfast, lunch, dinner, snack). The AI scores each meal's healthiness (1–10) and flags broad macro patterns (e.g. high protein, high sugar). Daily average score is tracked with a 30-day trend chart.

### Movement
Log workouts with type, duration, and intensity. Includes a weekly summary of total minutes broken down by activity type, and a 7-day bar chart.

### Cycle
Track period start/end, ovulation, symptoms, and flow. Predicts your next period and ovulation window from your history. Displays a color-coded monthly calendar showing period days, ovulation window, luteal phase, and follicular phase.

### People
Add contacts with a relationship type and desired check-in frequency. Log interactions with a quality rating. The app flags anyone overdue for contact based on their last interaction. An on-demand AI insight reflects on your connection patterns over the last 30 days.

### Goals
Hierarchical goal tracking across six time horizons: 5-Year, 1-Year, Quarterly, Monthly, Weekly, and Daily. Goals at lower tiers can be linked to a parent goal one tier up. Progress is qualitative — each goal has a free-text status note rather than a percentage. An on-demand AI insight reflects on whether your daily activity aligns with your longer-horizon goals.

### To-Do
Fast task entry (press Enter to add). Tasks can have an optional due date, priority (high/medium/low), and a link to a Goal. Views: Today (due today or overdue), All, and Completed. No AI on this section — kept intentionally fast and friction-free.

---

## Data & privacy

- All data is stored in your browser's `localStorage` under the domain the file is opened from
- Nothing is sent anywhere except to your configured AI server
- The AI server receives only the text of the specific entry or log being analyzed — no other personal data is included in the request
- Clearing your browser's site data will erase everything — export regularly

### Export & import
Settings → **Export all data** downloads a single JSON file containing everything. **Import data** restores from a previously exported file (replaces all current data).

> Keep regular backups. localStorage is not a database — browser updates, clearing cache, or switching browsers will lose your data if you haven't exported.

---

## Tips

- **JSON output quality varies by model.** Instruction-following models (Mistral Instruct, Qwen Instruct, Gemma variants) tend to return cleaner JSON than base models. If AI analysis keeps failing or returning garbled text, try a different model.
- **The daily insight is cached.** It generates once per day and won't re-run until the next day unless you hit Refresh manually.
- **Relationship and Goal AI insights are on-demand only** — they only run when you click the button, not automatically on every save.
- **Mobile works** — the layout adapts to narrow screens with a slide-out sidebar.

---

## Technical notes

- Single HTML file, ~1500 lines, vanilla JavaScript only
- Chart.js loaded from CDN (requires internet on first load; cached after)
- No build tools, no frameworks, no dependencies to install
- Compatible with any modern browser (Chrome, Firefox, Safari, Edge)
