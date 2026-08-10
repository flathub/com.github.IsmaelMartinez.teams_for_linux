# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

This is the Flathub packaging repo for teams-for-linux — nothing more. The application source lives in a
separate repository, `IsmaelMartinez/teams-for-linux`, and is consumed here as a prebuilt `.deb` release
asset. Only two files carry meaning: `com.github.IsmaelMartinez.teams_for_linux.yml` (the Flatpak manifest)
and `flathub.json` (Flathub publishing config). A bug in the app itself is not fixable here; only packaging
concerns are — `finish-args` permissions, `build-commands`, and the `teams-for-linux.sh` wrapper script
embedded in the manifest.

## Version pins are owned by the update bot

The `url`, `sha256`, and version fields are maintained by Flathub's external-data-checker via the
`x-checker-data` blocks, which open `update-master-*` PRs. Every version bump in this repo's history is
authored by `flathubbot`. Do not hand-edit those fields; make packaging changes only. If a manual bump is
explicitly requested, all three sources must move to the same tag together — the x86_64 `.deb`, the aarch64
`.deb`, and the version-pinned `metainfo.xml` URL — with both `sha256` values recomputed.

## Nothing can be built or verified locally

The development machine is macOS and has no `flatpak`, `flatpak-builder`, `flatpak-builder-lint`, or
`appstreamcli`. There is no way to build, lint, or run the package here. The first real check is the Flathub
buildbot on the pull request, and after that a community member tests the resulting build. Never describe a
manifest change as verified, tested, or working — describe it as proposed, and say what the buildbot and a
tester still need to confirm.

## Git workflow

Branch off `master`, push the branch to `origin` (the personal fork), and open the PR against `upstream`
(`flathub/com.github.IsmaelMartinez.teams_for_linux`) `master`. Never push to `upstream` master directly.

## Manifest conventions

YAML uses 2-space indentation with LF endings and a trailing newline, per `.editorconfig`. Every non-obvious
`finish-arg`, build command, or wrapper flag carries a comment above it explaining why it is there — see the
notes on the `--socket=x11` entry, `--system-talk-name=org.freedesktop.login1`, `XCURSOR_PATH`, and the
`--ozone-platform=x11` wrapper argument. Preserve this when adding or changing entries: a permission or flag
without a stated reason is impossible to audit later.
