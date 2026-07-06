# tr.acker
https://kasviii.github.io/tr.acker/

A dark, minimal expense and habit tracker that runs entirely in a single HTML file. No backend, no build step, no dependencies to install — just open it in a browser.

---

## Features

### Expenses
- Add transactions with a category, amount, date, and note
- Doughnut chart showing spend by category for the current month
- Bar chart showing the last 6 months of spending
- Filter transactions by category or month
- All amounts in ₹ INR (trivially adjustable in the source)

### Habits
- Create custom habits with individual color coding
- Daily checklist to mark habits done
- GitHub-style contribution heatmap per habit, spanning the last 52 weeks
- Five shade levels from least to most consistent

### General
- All data persisted to `localStorage` — survives page refreshes and browser restarts
- Zero network requests after initial load (fonts + Chart.js load from CDN on first open)
- Fully offline-capable once cached

---

## File Structure

```
tracker.html   ← the entire app (HTML + CSS + JS, ~400 lines)
README.md
```

---

## Customization

All tweaks are in the `<style>` block at the top of `tracker.html`.

| What | Where |
|---|---|
| Currency symbol | Search `₹`, replace with your symbol |
| Accent colors | `--accent` and `--accent2` in `:root` |
| Background / surface colors | `--bg`, `--surface`, `--surface2` in `:root` |
| Categories | `const CATS` and the `<select id="expCat">` options |
| Habit color palette | `const HABIT_COLORS` array |

---

## Data & Privacy

Everything lives in your browser's `localStorage` under three keys:

- `tr_expenses` — array of transaction objects
- `tr_habits` — array of habit objects
- `tr_logs` — object mapping habit IDs to date → boolean maps

No data leaves your device. Clearing your browser's site data will erase it, so export the JSON from the console if you need a backup:

```js
// Paste in DevTools console to export
copy(JSON.stringify({
  expenses: JSON.parse(localStorage.tr_expenses || '[]'),
  habits:   JSON.parse(localStorage.tr_habits   || '[]'),
  logs:     JSON.parse(localStorage.tr_logs     || '{}')
}))
```

To restore, paste and run:

```js
const data = /* paste exported JSON here */;
localStorage.tr_expenses = JSON.stringify(data.expenses);
localStorage.tr_habits   = JSON.stringify(data.habits);
localStorage.tr_logs     = JSON.stringify(data.logs);
location.reload();
```

---

## Browser Support

Works in any Chromium or Firefox-based browser from the last 3 years. Safari 15+. Does not work in IE.

---

## Dependencies (CDN)

| Library | Version | Purpose |
|---|---|---|
| Chart.js | 4.4.1 | Doughnut + bar charts |
| Inter | — | UI font |
| JetBrains Mono | — | Numbers + labels |

---

## License

MIT — do whatever you want with it.
