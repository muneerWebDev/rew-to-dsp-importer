# User Guide

A walkthrough of the app, end to end.

## 1. Launch

Double-click `REW-to-DSP-Importer.exe`. It starts without an administrator prompt. If your DSP software itself runs as administrator, click **Restart as administrator** at the bottom of the window (see Troubleshooting).

## 2. Configure your DSP

The **DSP profile** card has five controls. The line under them spells out the exact key sequence your settings produce.

### Preset

Pick a built-in preset that matches your DSP, or load one of your saved custom presets.

| Preset                                     | Action key | Field order        |
|-------------------------------------------|-----------|--------------------|
| Alpine (Enter • Freq → Q → Gain)          | Enter     | Freq → Q → Gain    |
| Nakamichi (Tab • Freq → Q → Gain)         | Tab       | Freq → Q → Gain    |
| miniDSP (Tab • Freq → Gain → Q)           | Tab       | Freq → Gain → Q    |
| Helix DSP (Tab • Freq → Gain → Q)         | Tab       | Freq → Gain → Q    |
| Generic (Enter • Freq → Gain → Q)         | Enter     | Freq → Gain → Q    |
| Generic (Tab • Freq → Gain → Q)           | Tab       | Freq → Gain → Q    |

### Advance key

The key the DSP uses to advance from one field to the next. Click **Change** → a dialog pops up — press any key. Letters, F1–F12, Space, arrows and punctuation are accepted. Keys that can't be sent to other apps (the Windows key, media keys) are refused with a message. Press Esc to cancel without changing; Esc itself can't be the advance key because it stops typing.

### Field order

The order your DSP's per-band fields appear in. All 6 permutations of Freq / Gain / Q are available — this is the most common difference between DSP UIs.

### Entry pattern

- **Per filter**: types all three fields of filter 1, then filter 2, and so on. Most DSPs work this way.
- **Per column**: types every value of the first field, then every value of the second, then the third. Use it when the advance key moves down a column.

### Typing speed

**Normal** suits most software. Choose **Slow** if your DSP drops or scrambles characters, **Fast** if it keeps up. The choice is remembered.

### Saving a custom preset

Click **Save as…** next to the preset list, name it, and it's saved to `%APPDATA%\REWtoDSPImporter\presets.json`. It'll appear in the dropdown below a `Your presets` divider on every future launch.

Built-in preset names are protected — you can't overwrite them.

### Deleting a custom preset

Pick the preset from the dropdown, click **Delete**. Built-in presets can't be deleted; the button is disabled when one is selected.

## 3. Export filters from REW

In Room EQ Wizard:

1. Open the **EQ** window.
2. Click the **Save** dropdown → **Save filter settings as text file**.
3. Save as a `.txt` file somewhere you'll find it.

The app understands these filter types:

- **PK** (peaking / bell) — typed into PEQ slots
- **LS, HS, LSC, HSC** (shelves) — typed into PEQ slots. Only Freq, Gain and Q are typed, so switch those bands to a shelf type in your DSP yourself. The preview flags them.
- **LP, HP** (low/high pass) — recognized but skipped (these usually map to crossover settings)
- **NO, AP** (notch / all-pass) — recognized but skipped

Filter slots marked OFF or `None` are silently ignored.

## 4. Import into your DSP

1. Open your DSP software, navigate to the PEQ section.
2. In **REW → DSP Importer**, click **Choose REW file…**.
3. Pick the REW `.txt` file you exported.
4. Review the **preview table** — every parsed filter is shown with its type, frequency, gain, Q, and whether it'll be typed or skipped.
5. Set the run options under the table if you need them (see below), then click **Start typing N filters**.
6. The app minimizes and a small panel appears at the top of the screen, counting down 8 seconds. Click into your DSP's **first field** (the panel names it).
7. Wait. The panel shows which filter is being typed and a progress bar.
8. The panel shows **Done** when finished. Click **Close** to bring the app back.

### Run options

- **Start at filter**: skip the filters before this number. Click into that filter's first field in the DSP instead of the first one. After a stopped run, choosing the same file again preselects the filter it stopped at (Per filter pattern only).
- **Begin typing**: *After a countdown* gives you 8 seconds. *When I press F8* waits as long as you like: click into the DSP, then press F8. The choice is remembered.
- **Test run**: types into a test pad inside the app instead of your DSP, showing each value and the advance key, e.g. `24.00 [Enter] 2.00 [Enter] -12.00 [Enter]`. Use it to check the order, key and speed. Keep the pad focused; clicking elsewhere stops it.

If the file contains filter lines the app can't read, the preview says how many and shows them. They are not typed.

## Zapco HB II

The Zapco HB II software can't be typed into, because it has no frequency field. Use **Write Zapco preset file…** instead. See the [Zapco guide](ZAPCO_GUIDE.md).

## 5. Aborting

You can stop the countdown or the typing at any time:

- **Press Esc** — the typing loop polls Windows' physical keyboard state, so this works even though your DSP window has focus, not ours.
- **Click Stop** on the panel.
- **Move the mouse to a screen corner** — pyautogui's built-in failsafe. Same effect.

Heads-up: pressing Esc may also be received by your DSP, which can cancel the field you were just editing. If that matters, prefer the mouse-corner failsafe.

## Troubleshooting

**"Can't type into that window".**
Your DSP software runs as administrator, and Windows refuses keystrokes from a normal app to an elevated one. Close the panel, click **Restart as administrator** at the bottom of the main window, accept the prompt, and run the import again.

**"No Filters" — but the file has filters in it.**
The file isn't in REW's "Generic" filter format. In REW: **EQ → Equaliser** dropdown → choose **Generic**, then re-export.

**Typed values landed in the wrong fields.**
The Field Order doesn't match your DSP. Try a different order — there are only 6 permutations.

**A few filters appeared in the preview but none typed.**
Check that they're not all LP/HP/NO/AP. Those are recognized but skipped because most DSPs treat them as crossover settings, not PEQ.

**App typed half the values, then stopped.**
You likely tapped Esc or grazed the mouse against a screen corner. Both abort by design, and the panel says where it stopped.

**Characters are missing or scrambled in the DSP.**
The DSP can't keep up. Set **Typing speed** to Slow.

## File locations

| What                | Where                                                   |
|---------------------|--------------------------------------------------------|
| Custom presets, typing speed | `%APPDATA%\REWtoDSPImporter\presets.json`              |
| The exe             | wherever you placed `REW-to-DSP-Importer.exe`          |

To reset all custom presets, delete `presets.json`.
