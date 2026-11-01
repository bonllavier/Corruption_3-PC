# Changelog

Versions follow `MAJOR.MINOR.PATCH`. Each release on GitHub is tagged `vMAJOR.MINOR.PATCH` and ships
`Corruption_3-PC-vMAJOR.MINOR.PATCH-win64.zip` with its SHA-256. The version is also shown at the bottom of the
F1 panel and in the executable's file properties.

## v0.1.6 - 2026-11-01 - World lighting, wall reflections, gamepad, FOV, achievements and smoother fights

### First launch: shaders compile in the background
- The first launch of a new install compiles the game's shaders in the background. Measured on a 4-core i7-4790:
  **about 17 minutes, with memory use temporarily reaching about 9 GB** (of 16 GB installed).
- That memory stays in use until you close the game, so restart it once the compilation has finished. Later launches
  reuse the compiled shaders and get ready in **about 7 seconds**.
- With less than 16 GB of RAM, keep the Windows page file enabled for that first run.
- Updating from an earlier version only recompiles the shaders that changed.

### World lighting (F1 > Effects, experimental, each option on its own)
- **New: environment material and borrowed lights.** Walls and floors with baked light react to the view and get
  highlights from the room's character lights.
- **New: floor reflections (SSR)** on smooth floors, on by default at strength 0.70. They only reflect what is on
  screen.
- **New: wall reflections** on very smooth walls such as polished panels, in their own section so you can turn them off
  without affecting anything else. On by default at strength 0.80. They only reflect what is on screen, and Samus
  herself is never reflected. Performance cost: low to medium.
- **New:** material in rooms with live lights, smooth lightmaps, soft highlights, soft character shadows and
  reflections that respect occlusion. All of these are on by default.
- **New, off by default:** light shafts (medium GPU cost), area-coloured reflections and linear light blending.
- **Fixed: duplicated glow.** Thin lights and the gunship's engine flames showed separate copies of their glow at high
  resolutions. Option *"Fix glow ghost copies"*, on by default.

### Materials
- New F1 > Materials tab, with materials for Samus out of the suit, the gunship and Gandrayda's frost.

### Controls and options
- **New: gamepad support** through SDL3.
- **New: first-person field of view option.** It cannot be used while RetroAchievements is on.
- **New: RetroAchievements** (casual mode), in the F2 window.
- **New: photo mode.** F3 freezes the game; the right arrow advances one frame.
- **New: two start-up screens** in place of the Wii Remote strap screen, showing what this PC version adds.

### Performance and fixes
- Fewer frame drops in effect-heavy moments such as the PED suit's Phazon and the fight with Rundas. Ambient occlusion
  and reflections now run once per game frame, and fewer shaders compile at once during play.
- **SSAO quality now defaults to 8 samples** (it was 12), which costs less GPU time.
- Fixed: the SSAO quality setting went back to its default after being changed.
- Fixed: choosing to exit to the title screen could leave a black screen.
- New option *"Expand draws on the decoder thread"* (F1 > Performance), **off by default**. Turning it on breaks the
  lava surface in Bryyo (seams between its patches when ripples appear), so leave it off.
- More shaders are compiled ahead of time for new installs.
- Removed the F9 performance panel and other developer diagnostics from the public build. F12 bug reports, the FPS
  counter and the F6 motion panel stay.

### About the VirusTotal result
1 of the 70 engines that analysed the executable flags it: Trapmine, with the label `malicious.moderate.ml.score`. The
other 69, including Kaspersky, Bitdefender, Malwarebytes, Microsoft and ESET, report nothing. I consider it a false
positive, although a scan alone cannot prove that:

- It is a machine-learning score, not a malware signature: the label names no malware family and no behaviour.
- Trapmine has flagged this port before: versions before v0.1.5 got this same label and v0.1.5 got `suspicious.low`, so
  the score went back up in this release. In [this r/antivirus thread](https://www.reddit.com/r/antivirus/comments/15zfn7x/maliciousmoderatemlscore/)
  about the same label, a game developer reports that Trapmine flags their two games as well. That is a personal
  experience, not an official verdict.
- The executable is about 157 MB, unsigned, new to VirusTotal and mostly machine-translated code, which may be what the model
  distrusts. This is my best guess, not a confirmed cause.

You never need to turn off your antivirus for this project. The reasons, what the port does and how to check the download
yourself are in the README, under [Antivirus warnings](https://github.com/bonllavier/Corruption_3-PC#antivirus-warnings).

### Updating
Unzipping over an existing folder keeps your `UserData/Config.toml`, so any option you have already saved keeps your
value. If you installed v0.1.5, your SSAO quality stays at 12 samples until you change it in F1 > Effects.

## v0.1.5 - 2026-10-28 - Samus' face and skin, enhanced materials, F11 screenshots

This version also contains everything from 0.1.4, which was withdrawn.

### Screenshots
- **New: F11 takes a screenshot** of the game picture as you see it, with the image effects applied and without the
  port's menus or notices. It is saved as JPEG (quality 92) in `UserData/Screenshots`, named
  `Corruption3PC_v<version>_<build>_<date>_<time>.jpg`; `<build>` is a short identifier of the executable, so
  pictures from different builds of the same version can be told apart. A short notice confirms where it was saved.

### Ambient occlusion (SSAO)
- **Samus' face behind the visor no longer gets ambient occlusion**, while the helmet and suit around it keep theirs.
  The port recognises the face by its textures and builds a per-pixel mask of where it stays visible each frame, so
  the helmet frame and anything in front of the face are still shaded. No new game shaders, no shader recompilation.
- What is seen through the visor glass (the inner rim of the helmet) no longer gets ambient occlusion either.
- The same applies to **Samus out of the suit** (face, skin, eyes, hair, eyelashes and the Zero Suit) in cutscenes.
- New option F1 > Effects > *"No SSAO on Samus' face"* (on by default) to compare.

### Enhanced metal
- **Skin no longer looks metallic.** The game gives skin the same reflection setup as metal, so the enhanced metal
  material also made faces and hands shine like metal. Samus' skin and eyes, Commander Dane's skin and Gandrayda's eye
  are now excluded; suits, armour and machinery keep the effect.

### Enhanced materials (F1 > Video, needs per-pixel lighting)
- **New, on by default.** Surfaces the port identifies by their textures get a modern material matched to what they
  are, even when the game gives them no reflection: relief taken from the original textures (plates and seams catch
  the light), sharp highlights from the scene's own lights and a reflection of the surroundings. Only the original
  textures are used; nothing is upscaled or replaced.
- **Starships:** the Federation fleet and the G.F.S. Olympus hulls in the opening space scene (brushed metal) and
  Samus' gunship paint (glossy paint, less metallic). Cockpit glass, holographic panels and light strips are left as
  they were.
- **Bounty hunters:** Ghor's exoskeleton as brushed machine metal, Rundas' armour as polished crystal and Gandrayda's
  skin with a soft sheen instead of the suit metal.
- The first time each of these surfaces appears its shader variant is compiled; during that moment it is drawn with
  the normal lighting. The shader cache keeps it for the next sessions.
- *"Enhanced materials"* can be switched off at any time to compare.

### Security and antivirus
- The public executable no longer contains the developer profiling tools (the F8 stack profiler and the per-thread
  CPU list of F9), which inspected the game's own threads in a way antivirus heuristics dislike. It ships without
  debug information (smaller file) and with a standard Windows application manifest (runs as the current user, never
  asks for administrator rights). Bug reports (F12) are unchanged.
- **About the VirusTotal result.** The zip is reported clean by every engine. The executable is clean for all engines
  except one, Trapmine, which marks it `suspicious.low.ml.score` (previous versions got `malicious.moderate.ml.score`).
  That is not a signature of any known malware: it is a machine-learning score computed from the general shape of the
  file. This executable is unusual for that kind of model: about 156 MB of automatically generated code (the game's
  translated program), no digital signature, a new file nobody has seen before, and a few standard Windows calls that
  come with the Rust library used to read the disc image. These changes lowered the score by one level; removing it
  completely needs the file to be digitally signed or reviewed by the vendor as a false positive. The executable never
  asks for administrator rights, does not install anything and only writes to its own data folder (settings, saves, caches, logs, screenshots).

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
