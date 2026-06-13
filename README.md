# Agent Skills

A repository containing custom agent skills and instructions designed to extend AI agent capabilities for specialized coding tasks, workflows, and projects.

## Available Skills

| Skill Name | Description |
| :--- | :--- |
| [node.js-scaffolding](./node.js-scaffolding) | Guidelines and rules for scaffolding Node.js applications with proper structure, authentication, and error handling. |
| [codebase-narrator](./codebase-narrator) | Generates developer inner-monologue walkthroughs of codebases, narrating the thought process, decisions, and trade-offs with line-by-line annotations for beginners. |

---

## How to Use These Skills

To load any of these skills into your Antigravity AI coding assistant:

1. Locate your global or project skills directory (typically `<appDataDir>/config/skills/`).
2. Copy the desired skill folder (e.g., `node.js-scaffolding/`) into that directory.
3. The agent will automatically recognize the skill, read its `SKILL.md` rules, and follow them whenever performing related tasks.

### Structure of a Skill

Each skill is structured as a directory containing a required markdown file with frontmatter:

```
my-custom-skill/
├── SKILL.md                 # Main instructions & rules
├── scripts/                 # (Optional) Helper scripts and automation utilities
├── examples/                # (Optional) Code samples & templates
└── references/              # (Optional) Documentation references
```
