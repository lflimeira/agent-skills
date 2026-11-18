# Agent Skills

A collection of AI agent skills focused on software engineering work.

The skills follow the open [Agent Skills](https://agentskills.io) standard (`SKILL.md`), so they work with Claude, OpenAI Codex, GitHub Copilot, Gemini CLI, Cursor and other tools that support it.

## Skills

| Skill | What it does |
|-------|--------------|
| [design-doc-writer](skills/design-doc-writer/SKILL.md) | Writes short, to-the-point Design Docs for features and technical proposals, plus an optional linked Implementation Doc with code and technical details. Gathers context (repos, microservices, docs, specs) first, asks for goals and non-goals, and reviews existing docs. |

## Installation

Clone the repository:

```bash
git clone https://github.com/lflimeira/agent-skills.git
```

Then copy the skill folder (e.g. `skills/design-doc-writer`) to the skills directory of your tool:

| Tool | Personal (all projects) | Project (shared with the team) |
|------|-------------------------|--------------------------------|
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| OpenAI Codex CLI | `~/.agents/skills/` | `.agents/skills/` |
| GitHub Copilot (VS Code / CLI) | `~/.agents/skills/` | `.agents/skills/` or `.github/skills/` |
| Gemini CLI | `~/.agents/skills/` | `.agents/skills/` or `.gemini/skills/` |
| Cursor | `~/.cursor/skills/` | `.agents/skills/` or `.cursor/skills/` |

Example (Claude Code):

```bash
mkdir -p ~/.claude/skills
cp -r agent-skills/skills/design-doc-writer ~/.claude/skills/
```

Paths can change between tool versions, so check your tool's documentation if a skill isn't detected.

### Claude app (claude.ai / desktop)

Zip the skill folder and upload it in the app's skills settings:

```bash
cd agent-skills/skills
zip -r design-doc-writer.zip design-doc-writer
```

## Usage

Just ask your agent for a design doc, for example:

> Help me write a design doc to add a caching layer to the orders service.

The skill asks for context, confirms its understanding, writes the Design Doc and, if you want, the Implementation Doc linked to it.

## Structure

```
skills/
└── <skill-name>/
    └── SKILL.md
```

## Contributing

Feedback, issues and pull requests are welcome.

## License

[MIT](LICENSE)
