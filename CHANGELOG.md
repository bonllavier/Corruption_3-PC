# Changelog

Versions follow `MAJOR.MINOR.PATCH`. Each release on GitHub is tagged `vMAJOR.MINOR.PATCH` and ships
`Corruption_3-PC-vMAJOR.MINOR.PATCH-win64.zip` with its SHA-256. The version is also shown at the bottom of the
F1 panel and in the executable's file properties.

## v0.1.0 - 2026-10-25 - first public test build

- Native Windows build of Metroid Prime 3: Corruption (USA, RM3E01) running from the player's own disc image
  (`.iso`, `.rvz`, `.wbfs`, `.gcz`, `.wia`, `.ciso`). The first start asks for the file with a dialog and remembers the
  path; no extraction step. Updates: unzip over the old folder, `UserData` (saves, settings) is never in the zip.
- Keyboard and mouse mode on by default: virtual Wii Remote + Nunchuk with remappable keys, mouse look in first
  person, gesture keys (push/pull, twist, lasso, spring jump), key caps in the game's own button prompts following the
  Windows display language.
- Options panel (F1) in English: internal resolution, borderless/exclusive fullscreen, MSAA, anisotropic filtering,
  per-pixel lighting, console copy filter, frame interpolation, audio modes, performance threads.
- In-game bug reports (F12 or F1 > Diagnostics): screenshot, session log, settings and system summary zipped under
  `UserData/Reports`, folder opened automatically.
- Crash dialog names the run's log folder to attach to a report.
- F1 > Info tab: version, build date, author, paths, and a check against GitHub Releases for newer builds (on-screen
  notice; `Check for updates.ps1` in the folder does the same). Report zips carry the version in their name.
- Full Wii Remote battery reported to the game (no low-battery warning with the virtual remote).
- Fixed the "WiiConnect24 cannot be used ... Error Code: 109042" dialog on the Game Select screen (the WiiConnect24
  scheduler probe now succeeds; the game never connects to anything).
- Shared shader cache seeded with every pipeline seen so far (first-run stutter reduced).
- Known: experimental Super-xBR texture upscaling can produce magenta polygons; off by default. Only the USA disc.
