---
title: "Keep a Changelog"
tags:
  - Software Development Life Cycle
  - Changelog
---

# Changelog

## What is a changelog?

A changelog is a file which contains a curated, chronologically ordered list of notable changes for each version of a project.

## Why keep a changelog?

To make it easier for users and contributors to see what notable changes have been made between each release (or version) of the project.

## Who needs a changelog?

People do. Whether consumers or developers, the end users of software are human beings who care about what's in the software. When the software changes people want to know why and how.

## How do I make a good changelog?

### Guiding Principles

* Changelogs are for humans not machines
* There should be an entry for every single version
* The same types of changes should be grouped
* Versions and sections should be linkable
* The latest version comes first
* The release date of each version is displayed
* Mention whether you follow Semantic Versioning

### Types of changes

* __Added__ for new features
* __Changed__ for changes in existing functionality
* __Deprecated__ for soon-to-be removed features
* __Removed__ for now removed features
* __Fixed__ for any bug fixes
* __Security__ in case of vulnerabilities

## How can I reduce the effort required to maintain a changelog?

Keep an `Unreleased` section at the top to track upcoming changes.

This serves two purposes:
- People can see what changes they might expect in upcoming releases.
- At release time, you can move the `Unreleaed` section changes into a new release version section.

## Can changelogs be bad?

- Don't use commit log diffs as changelog.
- Don't ignore deprecations
- Use date format in ISO standard, `2020-01-20`.

## Example of changelog

```Markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

_No unreleased changes_

## [0.0.1] - 2014-05-31

### Added

- abc

### Changed

- abc

### Removed

- abc
[unreleased]: <link to github next tag>
[0.0.1]: <link to github tag 0.0.1>
```

**Resources**:
- [Keep a changelog](https://keepachangelog.com/en/1.0.0/)
