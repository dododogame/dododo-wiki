---
layout: wiki-page
lang: en-US
title: Versions
---

## Versioning

The versioning of Dododo is slightly different from the popular [Semantic Versioning](https://semver.org/).

The format of the version number is

```text
<generation>.<major>.<minor>.<patch>[-<prerelease>]
```

| Component | Description |
|---|---|
| `generation` | The generation. Different generations are actually different games, and they are updated independently. |
| `major` | The major version. Incrementing in the major version causes backward incompatibility in beatmaps. |
| `minor` | The minor version. Incrementing in the minor version brings new features. |
| `patch` | The patch version. Incrementing in the patch version fixes bugs. |
| `prerelease` | The prerelease number. The version without a prerelease number is newer and more stable than that with one. |

Specially, if the major version is 0, this generation is under fast development and is considered unstable.

If a version contains prerelease number, it is a prerelease version.
Prerelease versions do not have pre-built desktop apps.
The game on web with internet is always the latest version even if it is a prerelease version.

## Change log

The date format is YYYY-MM-DD.
{% assign prefix="https://github.com/dododogame/dododo/releases/tag/v" %}

### [1.0.1.0-1]({{ prefix }}1.0.1.0-1)

- **Date**: 2022-08-21

### [1.0.1.0-2]({{ prefix }}1.0.1.0-2)

- **Date**: 2022-08-25
- Changes:
  - Changed a translation in zh-TW.
  - Changed the built launcher script for Windows (from a bat script to a vbs script).
  - Fixed a bug about updating the excess number.
  - Fixed a bug about counting measures.
  - Fixed a bug about missing left-half ties and right-half ties.

### [1.0.1.0-3]({{ prefix }}1.0.1.0-3)

- **Date**: 2022-09-05
- Changes:
  - Tried again to enable uploading files in mobile Safari.
