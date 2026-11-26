# skills

Custom Agent Skills. Each directory is one skill: a `SKILL.md` with frontmatter
(`name`, `description`) that any agent supporting the skills format can discover
and load.

| Skill | What it does |
|-------|--------------|
| [repo-manager](./repo-manager/) | Owns the full lifecycle of a personal repo — assess, changelog, README, privacy pass, commit, tag, push, maintain — for any directory: configs, code, skills, notes. |
| [teach-me](./teach-me/) | Turns recent work or a named topic into an interactive, one-lesson-at-a-time course grounded in real diffs and evidence. |

## Install

Skills are discovered from your agent's skills directory (for example
`~/.claude/skills/`, `~/.commandcode/skills/`, or its equivalent). Keep the source
of truth in this repo and symlink each skill in:

```bash
ln -s ~/projects/skills/repo-manager <skills-dir>/repo-manager
ln -s ~/projects/skills/teach-me <skills-dir>/teach-me
```

## Versioning

Each skill keeps its own `CHANGELOG.md` in
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format and is tagged in this
monorepo as `<skill>-vX.Y.Z`.
