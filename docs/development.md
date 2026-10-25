# Development notes

## How releases are made

Releases are versioned `vMAJOR.MINOR.PATCH`. The version lives in one place in the build tree
(`prime_port_version.h`) and flows into the executable's file properties, the F1 panel footer, the zip name,
the git tag and the GitHub Release. Each release ships:

- `MetroidPrime3PCPort-vX.Y.Z-win64.zip`: executable, runtime DLLs, bundled Wii bootstrap/DSP data, shader seed,
  `Config.default.toml` (copied to `UserData/Config.toml` on first run; the zip never contains `UserData`, so players
  update by unzipping over the old folder), this documentation.
- `MetroidPrime3PCPort-vX.Y.Z-win64.zip.sha256`: checksum to verify the download.

The maintainer runs one script that packages the zip, commits this repository, tags it, pushes, creates the
GitHub Release with the matching `CHANGELOG.md` section and uploads both files. A tag pushed by hand gets a draft
release from the `Release` workflow so the zip can be attached from the web UI.

## Why the executable is not built by GitHub Actions

The port is a static recompilation: the game's PowerPC code is translated to C once, from the maintainer's own
disc, and that translated code is compiled and linked together with the host runtime. The translated code and the
disc-derived inputs it needs (the game's executable and its 74 relocatable modules) are derivative of Nintendo's
copyrighted binary and are **not** uploaded anywhere. A GitHub runner therefore has nothing to build from.

What is published is the player-facing release and this documentation. The host runtime is a modified build of
WiiCompiled, licensed under the GPL v3; see `LICENSE` and `THIRD-PARTY-NOTICES.md`.

## Repository layout

```
README.md                 Player documentation (requirements, setup, controls, reporting)
CHANGELOG.md              One section per released version
LICENSE                   GNU GPL v3
THIRD-PARTY-NOTICES.md    Components and their licenses
docs/controls.md          Full key table, gestures, mouse look, latency, real Wii Remote
docs/troubleshooting.md   Bug reports (F12), crash folders, common errors, where files live
docs/development.md       This file
docs/media/               Banner and logo
.github/ISSUE_TEMPLATE/   Bug report and performance report forms
.github/workflows/        Documentation checks and draft releases for tags
```

Player data (`UserData/`, `game/`), build outputs and disc images are ignored by `.gitignore` and refused by the
workflow if they are ever tracked.
