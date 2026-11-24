# AeroJudge Figures Package

Figure SVGs and audio for judge devices. Device setup and updates install this
package from its latest release.

The [release workflow](.github/workflows/release.yml) checks that the pushed
tag matches the version in `package.json`, creates `figures.zip` with
`figures/` at the archive root and `figures/package.json` inside it, and
publishes `figures.zip`, `package.json` and `SHA256SUMS`. Use `vYYYY.RELEASE`,
for example `v2026.3` for the third release of the 2026 season. Preserve released
tags and assets.

The season comes from the package version: `2027.0` means season 2027.
Do not duplicate it in a separate `season` field or `season.cfg`. The app
derives its two-digit season (for example, `27`) from the installed package
version.

## Figures and audio layout

This section explains the v2027.0 layout of shared figure images, sequence
recordings and common device audio. Default and event sequences use the same
internal folder structure, in preparation for additional language support.

### Folder structure

```text
figures/
    common-audio/
        en/
            085.mp3
            instructions-global.mp3
            roundcompleted.mp3
            ...
    default/
        SPK_27S/
            images/
                1B.svg
                1C.svg
                ...
            en/
                fig1.mp3
                call1.mp3
                ...
        FAIL/
            images/             # Fallback and failsafe images
            en/                 # English fallback recordings
        FS/
            images/             # Freestyle images
            en/                 # Freestyle recordings
    event/
        folder_info.md          # Maintains directory structure
        SPU_6JX/                # Example generated event sequence
            images/
            en/
```

`common-audio/<locale>/` contains fixed recordings shared across sequences:
score values, penalties, review flags, instructions and standard announcements.

Each sequence owns its language-independent images in `images/` and its
recordings in locale folders such as `en/`. Additional locales, for example
`es-MX/` or `en-AU/`, can be added as recordings become available. They do not
require duplicate images.
Locale folders describe available recordings, not a guarantee of complete
application translation support.

Event sequences are generated for an event, downloaded, consumed and discarded.
The event folder shown above is illustrative; the package only supplies
the download placeholder.

### Sequence names and files

Known sequence names use `{ClassCode}K_{Year}{Variant}`. For example, `SPK_27S`
identifies Sportsman Known, 2027, Standard.

The following class codes are used for known default sequences.

| Class code | Application class |
|---|---|
| BA | BASIC |
| SP | SPORTSMAN |
| IN | INTERMEDIATE |
| AD | ADVANCED |
| UN | UNLIMITED |

Variants are `S` for Standard and `A` for Alternate. Event sequence identifiers
must match the app's normalized `short_desc` from Score (trimmed and uppercase).
Keep identifiers independent of the display language.

- `images/1B.svg`, `images/2B.svg`, etc.: B-direction figure images.
- `images/1C.svg`, `images/2C.svg`, etc.: C-direction figure images.
- `<locale>/fig1.mp3`, etc.: figure numbers and names announcements.
- `<locale>/call1.mp3`, etc.: detailed figure caller audio.

Preserve figure numbering, direction suffixes and filenames across locales.

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
