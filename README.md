# AeroJudge Figures Package

Figure SVGs and audio for judge devices. The app still supplies production
packages while setup/update consumers are being migrated to separate repositories.

The [release workflow](.github/workflows/release.yml) creates `figures.zip`
with `figures/` at the archive root and publishes it on a `v*` tag push.
Use `vYYYY.RELEASE`, for example `v2026.2` for the second release of the 2026
season. Preserve released tags and assets.

The season comes from the package version: `2027.1` means season 2027.
Do not duplicate it in a separate `season` field or `season.cfg`. When package
consumption is implemented, derive the app's season setting from the installed
package version and convert it to the required format (for example, `27`).

## Package repository expectations

Keep packaging in the release workflow using standard ZIP commands,
`package.json` metadata and a simple `SHA256SUMS` file, with concise checks
and instructions. A separate packaging program requires a demonstrated need
and an approved approach. Versions identify releases; no separate changelog
is maintained. The application repository keeps its own changelog.

This workflow currently publishes only the ZIP. Metadata and checksum support
remain to be added in a separate change. Future setup/update scripts will consume
the published package; they will not build it.
