---
title: "Semantic Versioning"
tags:
  - Computer Engineering
  - Software Development Life Cycle
  - Semantic Versioning
---

# Semantic Versioning

Semantic Versioning aims to mitigated dependency hell.

Given a version number `MAJOR.MINOR.PATCH`, increment the:

1. `MAJOR` version when you make incompatible API changes.
2. `MINOR` version when you add functionality in a backwards compatible manner.
3. `PATCH` version when you make backwards bug fixes.

Additional labels for pre-release and build metadata are available as extensions to the `MAJOR.MINOR.PATCH` format.

## Semantic Versioning Compatibility

- `Patch` version Z (x.y.Z | x > 0) **MUST** be incremented if only backwards compatible bug fixes are introduced. A bug fix is defined as an internal change that fixes incorrect behaviors.

- `Minor` version Y (x.Y.z | x > 0) **MUST** be incremented if new, backwards compatible functionality is introduced to the public API. It **MUST** be incremented if any public API functionality is marked as depcrecated. It **MAY** be incremented if substantial new functionality or improvements are introduced within the private code. It **MAY** include patch level changes.

- `Major` version X (X.y.z | X > 0) **MUST** be incremented if any backwards incompatible changes are introduced to the public API. It **MAY** also include minor and patch level changes.

And many others...

## Regex

- Named groups
`^(?P<major>0|[1-9]\d*)\.(?P<minor>0|[1-9]\d*)\.(?P<patch>0|[1-9]\d*)(?:-(?P<prerelease>(?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*)(?:\.(?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*))*))?(?:\+(?P<buildmetadata>[0-9a-zA-Z-]+(?:\.[0-9a-zA-Z-]+)*))?$
`

- Numbered capture groups
`^(0|[1-9]\d*)\.(0|[1-9]\d*)\.(0|[1-9]\d*)(?:-((?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*)(?:\.(?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*))*))?(?:\+([0-9a-zA-Z-]+(?:\.[0-9a-zA-Z-]+)*))?$
`

**References**:
- [SemVer](https://semver.org/)
