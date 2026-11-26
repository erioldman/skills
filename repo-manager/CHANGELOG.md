# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.0.2] - 2026-11-26

### Changed

- Commit reports hyperlink the commit hash to the remote commit.

## [1.0.1] - 2026-11-26

### Changed

- Merged the identical "push" and "tag and push" boundary rows; no behavior change.
- Description triggers extended: version-control, git-init, and redacting
  machine-specific values now route to the skill.

## [1.0.0] - 2026-11-26

### Added

- Full repo lifecycle in one skill: assess → init → document → redact → commit →
  tag → push → maintain, for any personal repo (config, code, skills, notes).
- Two-level privacy model: `.gitignore` for tool-generated files, per-file redaction
  via a git clean filter — including the renormalize gotcha (`git add --renormalize`
  after filter changes) and the rule against reconfiguring filters from docs.
- Hard preferences: no `Co-authored-by` trailer, Keep a Changelog format,
  private-by-default remotes (public only on explicit request, then verified),
  always push with a version tag, hard stage boundaries.
- Monorepo support: per-project changelogs and `<project>-vX.Y.Z` tags.
- Boundary-phrase table mapping user phrasing to the exact stopping point.

### Changed

- Renamed from `dotfile-repo` to `repo-manager`; scope generalized from config
  directories to any personal repo. Machine-specific references replaced with
  generic conventions.
