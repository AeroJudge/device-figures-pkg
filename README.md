# AeroJudge Figures Package

Figure SVGs and audio for judge devices. Device setup and updates install this
package from its latest release.

The [release workflow](.github/workflows/release.yml) checks that the pushed
tag matches the version in `package.json`, creates `figures.zip` with
`figures/` at the archive root and `figures/package.json` inside it, and
publishes `figures.zip`, `package.json` and `SHA256SUMS`. Use `vYYYY.RELEASE`,
for example `v2026.3` for the third release of the 2026 season. Preserve released
tags and assets.

The season comes from the package version: `2027.1` means season 2027.
Do not duplicate it in a separate `season` field or `season.cfg`. In a future
season-handling change, derive the app's season setting from the installed
package version and convert it to the required format (for example, `27`).

## Package repository expectations

Keep packaging in the release workflow using standard ZIP commands,
`package.json` metadata and a simple `SHA256SUMS` file, with concise checks
and instructions. A separate packaging program requires a demonstrated need
and an approved approach. Versions identify releases; no separate changelog
is maintained. The application repository keeps its own changelog.

To release: work in a branch, set `version` in `package.json`, merge, then push
the matching tag. On the device the installed package is identified by
`/var/opt/judge/figures/package.json`. Setup/update scripts consume the published
package; they do not build it.
