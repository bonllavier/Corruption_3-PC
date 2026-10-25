# Changelog

Versions follow `MAJOR.MINOR.PATCH`. Each release on GitHub is tagged `vMAJOR.MINOR.PATCH` and ships
`MetroidPrime3PCPort-vMAJOR.MINOR.PATCH-win64.zip` with its SHA-256. The version is also shown at the bottom of the
F1 panel and in the executable's file properties.

## v0.1.0 - 2026-10-25 - first public test build

- Native Windows build of Metroid Prime 3: Corruption (USA, RM3E01) running from the player's own disc image
  (`.iso`, `.rvz`, `.wbfs`, `.gcz`, `.wia`, `.ciso`) placed in the `game` folder. No extraction step.
- Keyboard and mouse mode on by default: virtual Wii Remote + Nunchuk with remappable keys, mouse look in first
  person, gesture keys (push/pull, twist, lasso, spring jump), key caps in the game's own button prompts following the
  Windows display language.
- Options panel (F1) in English: internal resolution, borderless/exclusive fullscreen, MSAA, anisotropic filtering,
  per-pixel lighting, console copy filter, frame interpolation, audio modes, performance threads.
- In-game bug reports (F12 or F1 > Diagnostics): screenshot, session log, settings and system summary zipped under
  `UserData/Reports`, folder opened automatically.
- Crash dialog names the run's log folder to attach to a report.
- Full Wii Remote battery reported to the game (no low-battery warning with the virtual remote).
- Shared shader cache seeded with every pipeline seen so far (first-run stutter reduced).
- Known: experimental Super-xBR texture upscaling can produce magenta polygons; off by default. Only the USA disc.
