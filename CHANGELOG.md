# Changelog

Versions follow `MAJOR.MINOR.PATCH`. Each release on GitHub is tagged `vMAJOR.MINOR.PATCH` and ships
`Corruption_3-PC-vMAJOR.MINOR.PATCH-win64.zip` with its SHA-256. The version is also shown at the bottom of the
F1 panel and in the executable's file properties.

## v0.1.2 - 2026-10-25 - scanner fix and mouse look toggle

- Fixed the scan visor no longer scanning anything after a long session (outlines still visible) until the game was
  restarted: the renderer ran out of slots for the small screen readbacks the scanner uses and now recycles them.
- Fixed a crash "invalid tex offset 6" in late-game effects.
- Mouse look on/off key (L by default, remappable in F1 > Controls) with a small HUD-style panel at the top of the
  screen while aiming in first person, in English or Spanish following Windows. Its size and position can be adjusted
  in F1 > Controls.
- Update check fixed: it reported "HTTP 404" because GitHub's "latest release" address leaves out pre-releases
  (every 0.x build); it now reads the public release list (no account or token involved). v0.1.1 and older still show
  the 404, so players on those versions have to download this one by hand once.
- Bug reports (F12) now also include your Metroid Prime 3 save (`save/save.bin`, `save/banner.bin`) so the reported
  spot can be loaded directly.

## v0.1.1 - 2026-10-25 - video memory fix

- Fixed a crash after long sessions ("Aurora reported a fatal renderer error ... ID3D12Device::CreateHeap ...
  Copy Conv Texture"): the renderer kept every EFB copy texture for every destination the game ever wrote until the
  game rewrote that memory, so video memory filled up after about 40 minutes of play. Copy textures now live under a
  512 MiB budget (`WII_COMPILED_AURORA_COPY_BUDGET_MB` to change it); the destinations idle for longest are released
  first and nothing used in the last five seconds is touched.
- Mouse look now stops while Samus uses her arm on in-world controls (keypads, levers) and inside the gunship, and
  resumes afterwards; it follows the game's own command table and control hints.
- More Wii button textures replaced by key caps (HUD "Press A" prompts, options pictures, control stick diagonals).

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
