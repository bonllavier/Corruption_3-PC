# Troubleshooting and bug reports

## How to report a problem

1. **In game, press F12.** A small status line appears in F1 > Diagnostics while the report is written (one or two seconds).
   The port creates `UserData/Reports/report_<date>.zip` and opens the folder in Explorer with the zip selected.
2. Open a new issue: [Bug report](../../../issues/new/choose). Drag the zip into the text box.
3. Say **where you were**: planet, room or objective name, and what you were doing (fighting, using a lever, opening the map...).
   With the area name the developer can go there directly and reproduce it. A short description of what you saw is enough;
   the screenshot in the zip shows the rest.

What the zip contains, and nothing else:

| File | Content |
| --- | --- |
| `screenshot.png` | The frame on screen when you pressed F12 |
| `console.log` | The port's log for that session (loading, shaders, warnings) |
| `crash_*.txt` | Only if the game crashed earlier in that session: registers and stack |
| `Config.toml` | Your settings and key bindings |
| `system.txt` | Windows build, CPU, RAM, GPU, display, port version |
| `HOW_TO_REPORT.txt` | These instructions |

No save games, no game data, no personal files. Open the files before sending if you want to check.

### If the game closes with an error dialog

The dialog names the folder of that run, `UserData/Logs/base_<number>_pid<number>`. Zip that whole folder and attach it
to the issue (it holds `console.log`, `crash_*.txt` and a memory snapshot that lets the crash be analysed offline).
Logs older than four days are deleted automatically.

### Performance problems (stutter, low FPS)

Press **F9** for the performance panel and include a screenshot of it in the report, plus the area. Performance issues
are reproduced from the area name alone, so no further files are needed. Note that the first visit to an area compiles
new shaders: a short hitch there is expected.

## Common issues

**"No Metroid Prime 3: Corruption disc image was found"**
Copy your dump into the `game` folder next to the executable, or set `iso_path` under `[paths]` in `UserData/Config.toml`.
Supported: `.iso`, `.rvz`, `.wbfs`, `.gcz`, `.wia`, `.ciso`.

**"The disc image is not Metroid Prime 3: Corruption (USA)"**
Only the USA disc, game ID `RM3E01`, revision 0, is supported. PAL and Japanese discs, and the *Metroid Prime Trilogy*
disc, have different code and will not work.

**"Unsupported Processor"**
The port is built for x86-64-v3 (AVX2). Intel Core 4th generation (Haswell, 2013) or newer, AMD Excavator (2015) or newer.

**Black screen or crash at startup on the graphics side**
Try `graphics_api = "vulkan"` (or `"d3d12"`) in F1 > Video, and update your GPU drivers. Attach the run's log folder.

**Keys do nothing**
The game window must have focus. Check F1 > Controls that *Keyboard and mouse mode* is on (it needs a restart when changed).

**Low-battery warning from the game**
F1 > Controls > *Wii Remote battery always full* (on by default) answers the game's battery query with a full battery.

**Dark rooms or missing geometry for a moment**
Shaders for that material are still compiling. It resolves by itself within a second or two; the shared shader cache
grows with every release.

## Where things are

Everything lives next to the executable (portable layout):

| Folder | Content |
| --- | --- |
| `game/` | Your disc image (read only) |
| `UserData/Config.toml` | Settings and key bindings |
| `UserData/NAND/` | Save files (Wii NAND layout) |
| `UserData/Logs/` | One folder per run with the console log and crash files |
| `UserData/Reports/` | F12 bug reports |
| `UserData/Cache/` | Shader and pipeline caches; safe to delete |
| `UserData/texture_replacements/` | Custom textures (Dolphin naming) and the generated keyboard icons |
