# agentic-dev-kit

Markdown skills for Claude Code that improve each stage of the SDLC: how we code, architect, review, test, launch.

Each skill is a folder under `skills/` with a `SKILL.md`.

## Install a skill

One line, no clone (project, shared via git):

```bash
mkdir -p .claude/skills/explain && curl -fsSL https://raw.githubusercontent.com/ARYANK-08/agentic-dev-kit/main/skills/explain/SKILL.md -o .claude/skills/explain/SKILL.md
```

For all your projects, use `~/.claude/skills/explain` instead of `.claude/skills/explain`. For another skill, swap `explain` for its name.

Or copy from a clone:

Per project:

```bash
mkdir -p .claude/skills
cp -r path/to/agentic-dev-kit/skills/<name> .claude/skills/
```

For all your projects:

```bash
cp -r path/to/agentic-dev-kit/skills/<name> ~/.claude/skills/
```

Restart Claude Code. The skill loads when your request matches its `description`.

## Skills

| Skill | Use it for |
| ----- | ---------- |
| [explain](skills/explain/SKILL.md) | Clear explanations: simplified English, explain-like-I'm-13, diagrams, HTML pages, videos |

## Add a skill

1. Create `skills/<name>/SKILL.md` with `name` and `description` frontmatter.
2. Add a row to the table above.
