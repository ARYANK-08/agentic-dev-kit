# agentic-dev-kit

Markdown skills for Claude Code that improve each stage of the SDLC: how we code, architect, review, test, launch.

Each skill is a folder under `skills/` with a `SKILL.md`.

## Install a skill

Per project (shared with the team via git):

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
| [explain](skills/explain/SKILL.md) | Clear explanations: simplified English, diagrams, HTML pages, videos |

## Add a skill

1. Create `skills/<name>/SKILL.md` with `name` and `description` frontmatter.
2. Add a row to the table above.
