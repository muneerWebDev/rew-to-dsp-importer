# REW → DSP Importer

A free Windows app that **types your REW (Room EQ Wizard) filters into your DSP
software for you**, so you don't have to copy every frequency, gain and Q by hand.

It works with DSP software that has no REW import of its own: Alpine,
Nakamichi, and anything else where you type a value and press Tab or Enter to
move to the next field. For the Zapco HB II, which has no frequency field to
type into, it writes the filters into a Zapco preset file instead.

**[Download the latest version](https://github.com/muneerWebDev/rew-to-dsp-importer/releases/latest)**
(one `.exe`, nothing to install)

---

## How it works

1. Export your filters from REW as a text file.
2. Open the app, pick your DSP preset and choose the REW file.
3. Check the preview, click **Start typing**, then click the first Frequency
   field in your DSP software.
4. The app types every filter for you.

## Features

- **Built-in presets** for Alpine, Nakamichi, miniDSP, Helix DSP and generic
  Enter/Tab layouts
- **Custom presets**: capture any key as the advance key, pick the field order
  your DSP uses, and save it
- **Preview before anything is typed**: every filter is shown with its type,
  frequency, gain and Q, and unsupported types are marked as skipped
- **Test run**: types into a test pad inside the app first, so you can check the
  order and key without touching your DSP
- **Stop anytime**: press **Esc**, click **Stop**, or move the mouse to a screen
  corner
- **Resume**: start at any filter, and a stopped run remembers where it broke off
- **Typing speed**: Slow, Normal or Fast, for DSP software that drops fast input
- **Zapco HB II**: writes the filters into a preset file you import in the
  Zapco program ([guide](docs/ZAPCO_GUIDE.md),
  [printable PDF](docs/Zapco-HB-II-Guide.pdf))
- **No administrator prompt** unless your DSP software itself runs as
  administrator

## Download and run

1. Download `REW-to-DSP-Importer.exe` from the
   [latest release](https://github.com/muneerWebDev/rew-to-dsp-importer/releases/latest).
2. Double-click it.

**Windows may show a "Windows protected your PC" message.** This appears
because the app is not code signed. Click **More info**, then **Run anyway**.
Each release lists the file's SHA-256 checksum if you want to verify your
download.

Requires Windows 10 or 11.

## Using it

1. **Export from REW**: in the **EQ** window, save the filter settings as a
   text file (Generic equaliser format).
2. **Pick a preset** that matches your DSP. If there isn't one, set your own:
   - **Advance key**: the key your DSP uses to move to the next field.
   - **Field order**: the order of the fields in your DSP, for example
     Freq → Gain → Q.
   - **Entry pattern**: *Per filter* (all three fields of filter 1, then
     filter 2) or *Per column* (every Freq, then every Q, then every Gain).
3. Click **Choose REW file…** and pick your `.txt`.
4. Review the preview, then click **Start typing**. Try **Test run** first if
   it's your first time.
5. The app minimizes and counts down 8 seconds (or waits for **F8**). Click the
   first field in your DSP. The app types each filter and shows progress.

Want to try it without your own measurements? Use the
[sample REW file](docs/sample-rew-filters.txt) with **Test run**.

The full walkthrough, including troubleshooting, is in the
[user guide](docs/USER_GUIDE.md).

## Supported filter types

| REW type | Meaning | What the app does |
|----------|---------|-------------------|
| `PK` | Peaking / bell | Typed (Freq, Gain, Q) |
| `LS` / `HS` / `LSC` / `HSC` | Shelf | Typed (Freq, Gain, Q). Set the band to shelf in your DSP yourself |
| `LP` / `HP` | Low / high pass | Shown in the preview, not typed |
| `NO` | Notch | Shown in the preview, not typed |
| `AP` | All-pass | Shown in the preview, not typed |

## Your DSP isn't listed?

If your DSP software lets you type values and move between fields with a key,
a custom preset will usually work. If it doesn't, or you'd like a built-in
preset or a file export for your DSP,
[open an issue](https://github.com/muneerWebDev/rew-to-dsp-importer/issues)
and say which DSP and software version you use.

## Good to know

- The app sends keystrokes to whichever window is focused, so keep your DSP
  software in front while it types.
- Turn the volume down before applying new filters.
- Alpine, Nakamichi, miniDSP, Helix and Zapco are trademarks of their owners.
  This app is an independent tool and is not affiliated with or endorsed by
  them, or by Room EQ Wizard.

## License

Free to use, for personal and commercial work. See [LICENSE.txt](LICENSE.txt).

Made by Muneer · [muneer.me](https://muneer.me)
