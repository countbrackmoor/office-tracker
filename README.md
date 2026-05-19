# office.tracker

A self-contained, single-file office attendance tracker for hybrid work requirements. Built for situations where you have to be in the office a minimum number of times across rolling, overlapping date ranges — and you'd like to see at a glance how you're tracking against each one.

No accounts. No backend. No build step. One HTML file, your browser, and `localStorage`.

![Office Tracker preview](preview.png)

## Features

- **Year-at-a-glance calendar** — every weekday of the year, grouped by month, click to cycle through states.
- **Four-state day marking** — unmarked → ✓ in office → ✗ not in office → 🏖 exempt (holidays, PTO) → unmarked.
- **Overlapping requirement periods** — define any number of staggered date ranges, each with its own day-count requirement (e.g. "20 office days between Feb 16 and May 15"). Days that fall in multiple periods count toward each.
- **Color-coded dots** on each day show which period(s) it counts toward.
- **Live progress bars** per period with green checkmarks when requirements are met and amber warnings when a period ends unmet.
- **Add, edit, delete periods** through a slide-in drawer with date inputs, day-count targets, and a color picker (8 presets + custom).
- **Export & Import** your data as a `.json` save file. Import supports both **replace** and **merge** modes.
- **Reset controls** — clear just your check/X marks (keeping holidays and periods) or wipe everything.
- **Auto-saves** to `localStorage` as you click. Works offline. No data leaves your browser.
- **Responsive** — adapts from 4-column to 1-column layouts on smaller screens.

## Usage

1. Download `office-tracker.html`.
2. Open it in any modern browser. That's it.

Optionally, double-click to bookmark it, or drop it in a folder you sync across devices and re-open it anywhere.

### Marking days

Click any weekday cell to cycle:

| Click | State | Counts toward requirement? |
|-------|-------|----------------------------|
| 1×    | ✓ In office | Yes |
| 2×    | ✗ Not in office | No |
| 3×    | 🏖 Exempt (holiday/PTO) | No |
| 4×    | Unmarked | No |

### Managing periods

Click **Manage** (top right) to open the period drawer. Click any period card on the main view to jump straight to editing it.

Each period has:
- A name (free text — e.g. "May 27", "Q2 review", whatever)
- Start and end dates (overlap freely with other periods)
- A days-required target
- A color (used on the period card border, progress bar, and on the calendar dots)

### Backups

The **Save File** section in the drawer lets you:
- **Export** — download a `.json` of your current attendance and periods, named with today's date.
- **Import** — load a save file, with the option to either *replace* everything or *merge* (only adds days you don't already have marked, and adds periods whose IDs aren't already present).

Recommended: export a backup before clearing edits, switching browsers, or making big changes.

### Reset controls

At the bottom of the drawer:
- **Clear all Days** — removes ✓ and ✗ marks only. Keeps 🏖 exempt days and your periods.
- **Clear all Edits** — wipes attendance and periods entirely. Confirms twice.

## Data model

Everything is stored in two `localStorage` keys under the `ot26_` prefix.

`ot26_ranges`:

```json
[
  {
    "id": "8b73ti9",
    "name": "May 27",
    "start": "2026-02-16",
    "end": "2026-05-15",
    "color": "#b060f0",
    "req": 20
  }
]
```

`ot26_attendance`:

```json
{
  "2026-03-05": "check",
  "2026-03-10": "check",
  "2026-11-27": "exempt"
}
```

Valid attendance values: `"check"`, `"x"`, `"exempt"`. Absence of a key means unmarked.

An exported save file wraps both in:

```json
{
  "version": 1,
  "exportedAt": "2026-05-08T13:46:46.923Z",
  "ranges": [ ... ],
  "attendance": { ... }
}
```

## Customizing the defaults

Open `office-tracker.html` in any text editor and find the `DEFAULT_RANGES` and `DEFAULT_ATTENDANCE` constants near the top of the `<script>` block. These are the starting state for any browser that hasn't used the tracker before.

The current year is hard-coded as `YEAR = 2026` on the same block — change it to reuse the tracker for a different year.

## Technical notes

- Pure HTML/CSS/JS — no frameworks, no dependencies, no build.
- Uses Google Fonts (`Syne`, `DM Mono`) via CDN. If you need fully offline, swap them out for system fonts in the `<link>` tag.
- All state lives in `localStorage`. Clearing site data in your browser will reset the tracker (export first!).
- Designed for evergreen browsers. Tested on recent Chrome, Firefox, Safari.

## Why?

I built this for a hybrid work policy with rolling 12-week periods that overlap and stagger — every two months a new period starts, ending three months later. Spreadsheets got unwieldy. Apps wanted accounts. This does exactly one thing well.

## License

MIT. Do whatever you want with it.
