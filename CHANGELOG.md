# Changelog

Versions follow `MAJOR.MINOR.PATCH`. Each release on GitHub is tagged `vMAJOR.MINOR.PATCH` and ships
`Corruption_3-PC-vMAJOR.MINOR.PATCH-win64.zip` with its SHA-256. The version is also shown at the bottom of the
F1 panel and in the executable's file properties.

## v0.1.3 - 2026-10-27 - image effects, enhanced metal and ubershader

### Image effects (F1 > Effects)
- Built-in Aurora image effects, all live: ambient occlusion, bloom/glow, CAS sharpening, FXAA and colour grading
  (brightness, contrast, saturation, gamma, temperature, vignette).
- **Ambient occlusion (SSAO) is on by default.** Soft contact shading in corners and where objects meet (walls, the
  ship, the floor plates, the suit). It is applied to the 3D world before the visor, HUD and messages are drawn, so
  those are never darkened, and it pauses in menus, the map and videos. It needs MSAA off (Video > Antialiasing = 1x).
  - Stable picture: no flicker, no bands on floors, no seam across the screen, no shadows of characters on walls in
    cutscenes, and it stays on during charged shots.
  - "SSAO glow protection" keeps it off surfaces the game marks as glowing (Samus' visor glass, lights, energy), so
    her face behind the visor is not darkened.
  - Sliders for radius, intensity, softness, quality, bias, power, fade distance, edge sharpness and glow protection;
    "Reset SSAO" restores the tuned defaults (intensity 0.60, power 0.74).
- Bloom/glow can take its glow only from the 3D scene ("Glow only from the 3D scene", on), not from the visor HUD.
- FXAA no longer leaves black dots along horizontal edges.
- Bundled ReShade 6.8.0 with a curated MIT/BSD effect set, loaded only when "Load ReShade at startup" is ticked
  (Home = menu, End = toggle effects). ReShade effects apply only to 3D scenes: they pause in menus, the map, videos
  and while a port panel (F1, F5, ...) is open.

### Enhanced metal (F1 > Video, needs per-pixel lighting)
- **New, on by default.** A modern metal material on the game's metallic surfaces (Samus' suit and arm cannon,
  soldiers' armour, machinery): sharper reflections that follow the curvature, coloured highlights from the scene's
  own lights, edge sheen and a reflection of the surroundings. Glowing parts (visor glass, energy) are left alone.
- Sliders: metal strength (0.30), roughness (0.25), metallic (0.62), edge sheen (0.50) and surface detail (1.00,
  fine relief taken from the textures); "Reset metal" restores them. The first time it is used it compiles new
  shaders (possible short stutters until the cache fills).

### Performance and stability
- **New: F1 > Performance > "Ubershader while shaders compile"**, on by default. While a material's shader
  is still being compiled, the draw uses a generic shader that reads the material from memory instead of waiting, so
  nothing is skipped and nothing stalls. Compiled shaders and the shader cache always have priority; the ubershader
  only covers the gap. In a test with one material in eight left uncompiled, the worst frame dropped from 218 ms to
  75 ms and the average went from 58.4 to 59.7 FPS. It costs some GPU time during those frames, adds about 100 MB to
  the shader cache and about 2 s to the start-up shader pass. Not used while frame interpolation is on.
- Fixed a full freeze when the game was started from a PowerShell or CMD window and that window was then clicked (its
  title turns into "Select ..."): Windows pauses any program writing to such a console, and the game's log mirror was
  on the game thread's path. Log destinations now have their own threads and bounded queues, so a stuck console, disk
  or antivirus can only lose log lines, never stop the game.
- "Purge shader cache" button in F1 > Performance: deletes this profile's compiled shader databases at the next start,
  for troubleshooting. Saves, settings and bindings are not touched.
- The executable's file properties now report the real version (they were stuck at 0.1.0).
- Every release is scanned with VirusTotal and the public report is linked in its notes.

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
- Shader cache hygiene: the first launch after an update deletes the cached shaders the new version no longer uses,
  entries unused for 7 days are dropped, the cache is capped at 400 MiB (`WII_COMPILED_AURORA_DAWN_CACHE_MB`) and
  the file is compacted when it holds a lot of free space.

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
