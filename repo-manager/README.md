# repo-manager

An agent skill that owns the full lifecycle of a personal repo:
assess → init → changelog → privacy pass → commit → tag → push → maintain.

## What it does

- **Assess first** — inventory hand-written vs tool-generated files, scan for secrets,
  report the assessment before touching anything.
- **Document** — every repo gets a [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)
  `CHANGELOG.md`; a README only when asked.
- **Redact** — two privacy levels:
  - whole tool-generated files (lockfiles, caches, exports) → `.gitignore`,
  - machine-specific values inside shareable files → a git clean filter: the working
    tree keeps real values, the repo stores placeholders (`/path/to/<dir>/`).
- **Release** — annotated `vX.Y.Z` tags matching changelog sections; no push goes out
  without a version tag.
- **Respect boundaries** — "no further than stage" is a hard stop.

Scope is general: configs, code, skills, notes. Monorepos are supported with one
changelog per project and `<project>-vX.Y.Z` tags.

## Install

Symlink into your agent's skills directory (for example `~/.claude/skills/`,
`~/.commandcode/skills/`, or its equivalent):

```bash
ln -s ~/projects/skills/repo-manager <skills-dir>/repo-manager
```

## Triggers

"back up <dir>", "check <dir> and doc the changes", "handle it fully",
"tag and push", "create the repo and push", "no further than stage".

## Requirements

`git` and `gh`, authenticated (`gh auth status`).
