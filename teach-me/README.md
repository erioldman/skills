# teach-me

An agent skill that turns recently completed work — code changes, bug
hunts, features, PRs — or a named development topic into an interactive,
one-lesson-at-a-time teaching session grounded in real diffs, files, and evidence.

## How it teaches

- Opens with a numbered lesson map (3–8 lessons, dependency-ordered) and the control
  signals — nothing deeper.
- Exactly one lesson per reply: grounding in the real artifact, line-by-line
  mechanics, the transferable principle, honest caveats, one-sentence takeaway.
- `next` advances, questions are welcome anytime, `back <n>` replays a lesson a
  different way.
- Corrections update the map; the course closes by teaching the shipping process and
  recapping every takeaway.

## Usage

```
/teach-me                    # teach this session's work
/teach-me git clean filters  # teach a named topic
```

## Install

Symlink into your agent's skills directory (for example `~/.claude/skills/`,
`~/.commandcode/skills/`, or its equivalent):

```bash
ln -s ~/projects/skills/teach-me <skills-dir>/teach-me
```
