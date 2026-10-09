# Changelog

## 2.3 — Test run, resume, F8 start, no forced admin

### Added
- **Test run**: types the filters into a built-in test pad instead of your DSP, with the advance key spelled out (`24.00 [Enter] 2.00 [Enter] …`), so the order, key and speed can be checked safely. It stops by itself if the pad loses focus.
- **Start at filter N** in the preview. After a run is stopped, choosing the same file again preselects the filter it stopped at (Per filter pattern only).
- **Begin typing "When I press F8"** as an alternative to the 8 second countdown: click into the DSP in your own time, then press F8. The key is swallowed, so the DSP doesn't see it. The choice is remembered.
- **Unreadable filter lines are reported** in the preview instead of being dropped silently.

### Changed
- **The app no longer forces the administrator prompt.** It starts normally. Before typing it checks the target window: if that runs as administrator, the run is blocked with an explanation instead of typing into nothing, and **Restart as administrator** in the footer relaunches the app elevated.
- The preview's `#` column now numbers only the filters that get typed, matching "Start at filter" and the progress text.
- Save / Delete preset moved next to the preset list, so the window (now with the Zapco card) still fits small screens.

## 2.2 — Zapco HB II

### Added
- **Zapco HB II support, by preset file.** The Zapco HB II DSP Configurator has no frequency field (a band's frequency is set by dragging its dot on the graph), so its EQ can't be typed into. The new **Write Zapco preset file…** button writes the REW filters into a copy of a preset saved from the Zapco program, which is then imported there with LOAD/SAVE → Open → Import.
- Pick one or more outputs to receive the filters. Only their EQ is replaced; crossovers, delays, levels and the other outputs are copied as they are, and the original file is never overwritten.
- Values outside Zapco's limits (gain +6 to -15 dB, Q 0.5 to 15, 20 Hz to 20 kHz, 31 bands) are limited and flagged in the review table. Shelf filters are skipped.
- `docs/ZAPCO_GUIDE.md`, a step by step guide for installers.

## 2.1 — Reliable abort, live progress, new look

### Fixed
- **Esc now always stops typing.** A background watcher checks the key every 10 ms; before, a quick tap between keystrokes could be missed.
- **Typing ran at half the intended speed** because PyAutoGUI's own 0.1 s pause stacked on top of the app's delay.
- **The window froze ("Not Responding")** during the countdown and typing. Both now run on a worker thread.
- **Keys PyAutoGUI can't press** (some punctuation, media keys, the Windows key) were accepted as the advance key and then silently did nothing. Punctuation now works; unsendable keys are rejected in the capture dialog.
- **A hand-edited `presets.json` could crash the app** on an unknown grouping or a non-object file. Invalid entries are now dropped.
- **The window didn't fit on small screens** (fixed 620×920). It now sizes to its content, about 560×630.

### Added
- **Run overlay**: an always-on-top panel shows the countdown, then "Typing filter 3 of 9" with a progress bar, then the result. It has a Stop button, and the main window minimizes out of the way during a run.
- **Typing speed** setting (Slow / Normal / Fast), remembered between launches. Slow is close to the pace of 2.0.
- **Shelf warning** in the preview: shelf filters are flagged because the band type has to be switched in the DSP by hand.
- A plain-language line under the settings that spells out the exact key sequence.
- App icon, dark title bar, and crisp rendering on scaled (high-DPI) displays.

### Changed
- New dark theme with a single amber accent; emoji icons removed.
- "Action key" is now labelled "Advance key"; "Group fields by" is now "Entry pattern" (Per filter / Per column).

## 2.0 — Entry pattern

- "Group fields by" option: type filter by filter, or all of one parameter at a time.

## 1.1.0 — Custom presets & UX overhaul

### Added
- Customisable presets: capture *any* key as the action key, pick any of the 6 Freq/Gain/Q permutations, save with a name. Stored in `%APPDATA%\REWtoDSPImporter\presets.json`.
- **Esc key** as a global abort hotkey (in addition to mouse-to-corner).
- Filter-type expansion: parses PK, LS/HS/LSC/HSC, LP/HP, NO/AP; preview marks non-typeable rows as skipped.
- Filter preview table before typing — shows what will be sent and what's skipped.
- Refined visual design: Segoe UI typography, card-style layout, vibrant accent colors, hover feedback, larger primary CTA, status footer.

### Changed
- Built `.exe` is now `dist/REWtoDSPImporter.exe` (was `rew_to_alpine_final_gui.exe`).
- Footer link: `muneer.dev` → `muneer.me`.

## 1.0.0 — Initial release

- Tkinter GUI for selecting Enter or Tab as the action key.
- Parses REW PK filter lines and types Freq → Q → Gain into the focused DSP.
- 8-second countdown after the user clicks into the first DSP field.
- PyAutoGUI failsafe (mouse to screen corner) for aborting.
- Packaged as a single Windows `.exe` via PyInstaller.
