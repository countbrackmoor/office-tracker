# Changelog — Office Tracker

2026 hybrid office attendance tracker. Single-file HTML, `localStorage`-backed.

---

## 2026-06-21 — Changelog established

### Added
- This CHANGELOG.md, reconstructed from past work sessions
- Project rule: future changes to this module must be logged here in the same session they're made

---

## ~2026-05-29 — Initial build (single multi-step session)

The whole tool was built and refined in one session. Captured below as a series of feature additions in the order they happened.

### Added (core)
- Weekday-only calendar grid for all of 2026, grouped by month
- Per-day click-to-toggle marking (✓ / ✗)
- Staggered date range cards with progress bars

### Added (drawer)
- Slide-in **Manage** drawer (originally "Manage Periods", later renamed)
- Add / edit / delete periods with color picker, date inputs, requirement count

### Added (data I/O)
- Export to JSON save file
- Import with merge vs. replace modes

### Added (day states)
- Four-state day cycle: unmarked → ✓ → ✗ → 🏖 exempt → unmarked
- Exempt state does not count toward requirements

### Added (calendar visuals)
- Multi-dot indicators per day showing all overlapping periods that include it

### Changed
- Max 4 period cards per row with responsive breakpoints
- "Manage Periods" → "Manage" (header button and drawer title)

### Added (defaults baked in)
- 8 real named periods (May 27 through Jan 6 2027) replacing placeholder periods
- Pre-populated exempt days (holidays, observed days off)
- Constants live in `DEFAULT_RANGES` and `DEFAULT_ATTENDANCE` near top of script

### Added (reset section)
- **Clear all Days** — removes ✓ and ✗ marks only; keeps 🏖 exempt and periods; single confirm
- **Clear all Edits** — full wipe of attendance and periods; double confirm; suggests exporting backup
- Both skip the prompt if there's nothing to clear; small post-action feedback message

### Added (docs)
- `README.md` covering usage, data model schema (`ot26_ranges`, `ot26_attendance` `localStorage` keys), customization, technical notes

### Tech notes
- `YEAR = 2026` hard-coded near top of script
- Save file wraps both keys with `version: 1` and `exportedAt` ISO timestamp
- Google Fonts: Syne, DM Mono
