<p align="center">
  <img src="docs/media/banner.png" alt="Metroid Prime 3 PC Port" width="100%">
</p>

# Metroid Prime 3 PC Port

A native Windows port of **Metroid Prime 3: Corruption** (Wii, USA), created by **bonllavier**.
The game's code runs recompiled on your PC: no emulator, no virtual machine. You play with keyboard and mouse
(or a real Wii Remote over Bluetooth), at your monitor's resolution, with per-pixel lighting, anisotropic
filtering and MSAA on top of the original look.

> **Status: experimental alpha.** The game boots, loads saves, and the opening of the campaign (G.F.S. Olympus,
> Norion) is playable at 60 FPS. Later areas have not been tested end to end. Expect bugs and please report them,
> that is what this release is for.

**No game data is included.** You need your own dump of the disc. See [Legal](#legal).

---

## Requirements

| | Minimum |
| --- | --- |
| OS | Windows 10 or 11, 64-bit |
| CPU | x86-64-v3 (Intel Haswell / 4th gen or newer, AMD Excavator / Zen or newer) |
| GPU | Direct3D 12 or Vulkan capable, up to date drivers |
| RAM | 8 GB |
| Game | Your own dump of *Metroid Prime 3: Corruption* (USA), game ID `RM3E01`, as `.iso`, `.rvz`, `.wbfs`, `.gcz`, `.wia` or `.ciso` |

## Getting started

1. Download the latest `MetroidPrime3PCPort-vX.Y.Z-win64.zip` from the [Releases](../../releases) page and unzip it anywhere.
2. Copy your disc image into the **`game`** folder (the first image found there is used).
3. Run **`MetroidPrime3PCPort.exe`**. The first start compiles shaders for a few seconds.
4. Pick your save slot with the mouse and click. **F1** opens the options at any time.

Everything the port writes (settings, saves, logs, caches, bug reports) stays inside its own `UserData` folder. The disc image is only ever read.

## Controls

The port drives a virtual Wii Remote and Nunchuk. Every key can be remapped in **F1 > Controls**; the game's own button prompts show your keys instead of Wii buttons.

| Keyboard / mouse | Wii |
| --- | --- |
| Mouse | Aim. In first person the camera follows the mouse (mouse look) |
| Left click / Enter | A |
| Right click / Space | B |
| W A S D | Nunchuk stick |
| Shift | Z (lock on) |
| Ctrl | C (Morph Ball) |
| Arrow keys | D-pad |
| Esc | + (pause / menu) |
| `-` | - (visor select) |
| 1, 2, H | 1, 2, HOME |
| E / Q (hold, release) | Push the remote forward / pull it back (levers, ship controls) |
| Z / X | Twist the remote left / right |
| R / F | Flick the Nunchuk: grapple lasso throw / pull |
| T | Flick the remote up (Morph Ball spring jump) |
| G (hold), U/J, N/M, I/K | Shake both, tilt remote, twist Nunchuk, tilt Nunchuk |

Full table and gesture notes: [docs/controls.md](docs/controls.md).

### Hotkeys

| Key | Action |
| --- | --- |
| F1 | Port options: video, controls, audio, performance, diagnostics |
| F10 | Renderer bar (resolution, display mode, Wii Remote pairing, audio) |
| F12 | **Create a bug report** (screenshot + log + settings, zipped) |
| F9 | Performance panel |
| F6 | Virtual Wii Remote motion panel |
| Esc (menu closed) | Exit prompt |

## Reporting bugs and helping with testing

Press **F12** when something looks wrong. The port writes `UserData/Reports/report_<date>.zip` with a screenshot, the
console log of that session, your settings and a system summary, then opens the folder for you. Attach that zip to a
new [issue](../../issues/new/choose) and tell us **where in the game you were** (planet, room, what you were doing).
The area is the key detail: with it the problem can be reproduced directly.

If the game closes with an error dialog, the dialog names the `UserData/Logs/...` folder of that run. Zip that folder and attach it.
Nothing personal is collected: you can open every file in the zip before sending it. See [docs/troubleshooting.md](docs/troubleshooting.md).

## Options worth knowing (F1)

- **Video**: internal resolution (monitor native by default), MSAA 2x/4x/8x, anisotropic filtering, per-pixel lighting, console copy filter (the Wii's vertical blur, off by default), frame interpolation to 120/180 Hz (off by default).
- **Controls**: key bindings, mouse look sensitivity and smoothing, keyboard icons in game prompts, hide cursor, always-full Wii Remote battery.
- **Audio**: volume, stereo / Pro Logic II / mono, high-quality resampler.
- **Performance**: GPU thread, disc reads on their own thread, texture decoding on several cores, shader waiting policy. The game logic always runs at 60 Hz, like the console.

## Known issues

- First launch and the first visit to a new area compile shaders; a short stutter is normal until the cache fills.
- Experimental texture upscaling (Super-xBR) can paint some polygons magenta; it is off by default.
- Bluetooth Wii Remote support exists but has had far less testing than keyboard and mouse.
- Only the USA disc (RM3E01, revision 0) is supported.

## Legal

This project contains **no game code, assets or data**. The port runs from the player's own disc image, which is only read.
*Metroid* and *Metroid Prime* are trademarks of Nintendo. This is a fan project with no affiliation to Nintendo or Retro Studios.

The port is built on [WiiCompiled](https://github.com/WiiCompiled) and its Aurora renderer and is licensed under the
[GNU GPL v3](LICENSE). Third-party components and their licenses are listed in [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

## Credits

- **bonllavier**: port creator, Metroid Prime 3 runtime hooks, keyboard/mouse mode, PC options.
- WiiCompiled authors: static recompilation runtime and Aurora (GX on WebGPU/Dawn).
- nod (disc image reader), Dawn, SDL3, Dear ImGui, Super-xBR by Hyllian, and everyone in THIRD-PARTY-NOTICES.md.
