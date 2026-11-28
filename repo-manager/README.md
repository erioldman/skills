# repo-manager

An agent skill that owns the full lifecycle of a personal repo:
assess → init → changelog → privacy pass → commit → tag → push → maintain.

## What it does

- **Assess first** — inventory hand-written vs tool-generated files, scan for secrets,
  report the assessment before touching anything.
- **Document** — every repo gets a [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)
  `CHANGELOG.md` and a README. Both are standing documentation: every state-changing
  update syncs them in the same cycle. New repos start from `## [Unreleased]`; the
  first push renames it to the release version.
- **Redact** — two privacy levels:
  - whole tool-generated files (lockfiles, caches, exports) → `.gitignore`,
  - machine-specific values inside shareable files → a git clean filter: the working
    tree keeps real values, the repo stores placeholders (`/path/to/<dir>/`).
- **Release** — releases happen at push, not at commit: the push versions
  `## [Unreleased]`, tags it with an annotated `vX.Y.Z` tag matching the changelog
  section, and pushes. No push goes out without a version tag.
- **Respect the chain** — every request maps to one step of the
  doc → stage → commit → push chain and runs everything up to and including it;
  stated limits ("no further than stage", "no push") are hard stops.

Scope is general: configs, code, skills, notes. Monorepos are supported with one
changelog per project and `<project>-vX.Y.Z` tags.

## Install

Symlink into your agent's skills directory (for example `~/.claude/skills/`,
`~/.commandcode/skills/`, or its equivalent):

```bash
ln -s ~/projects/skills/repo-manager <skills-dir>/repo-manager
```

## Triggers

"back up <dir>", "version-control", "git-init", "redact machine-specific values",
"check <dir> and doc the changes", "handle it fully" — or any lifecycle request on
a managed repo: document, stage, commit, tag, push.

## Requirements

`git` and `gh`, authenticated (`gh auth status`).
