# Agentic Workspace Setup

A skill for setting up AI-agent workspaces with a three-layer architecture.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## What It Does

Guides you through creating structured workspaces where AI agents can:

-   Execute commands that load domain-specific context
-   Apply patterns, voice guidelines, and quality standards consistently
-   Produce outputs that match your requirements

## The Three-Layer Architecture

```
User Input → Command → Context Injection → Agent Execution → Output
```

| Layer        | Purpose                           | Examples                                       |
| ------------ | --------------------------------- | ---------------------------------------------- |
| **Commands** | Entry points that load context    | `/blog-post`, `/research`, `/respond`          |
| **Context**  | Domain knowledge and patterns     | Voice guidelines, templates, quality standards |
| **Agents**   | Execute tasks with loaded context | Orchestrator, specialists, reviewers           |

## Supported Platforms

| Platform    | Config Location                            | Agent Model               |
| ----------- | ------------------------------------------ | ------------------------- |
| Cursor      | `.cursor/commands/`, `.cursor/rules/`      | Subagents only (see note) |
| Claude Code | `.claude/commands/`, `CLAUDE.md`           | Primary + subagents       |
| OpenCode    | `.opencode/commands/`, `.opencode/agents/` | Primary + subagents       |

> **Cursor Note:** Cursor's main agent cannot be customized. Use `.cursor/rules/` with `alwaysApply: true` for behavioral config, and `.cursor/agents/` for delegated subagent specialists only.

## Usage

Invoke this skill when:

-   Starting a new project that needs AI workflows
-   Creating a personal assistant workspace
-   Automating multi-step tasks with consistent outputs
-   Setting up MCP servers for agent tooling

The skill will guide you through:

1. **Discovery** - Understanding your requirements
2. **Design** - Presenting architecture for approval
3. **Implementation** - Creating the workspace structure

## Files

| File           | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| `SKILL.md`     | Main skill instructions                                      |
| `templates.md` | Copy-ready templates for agents, commands, and context files |

## Example Output

**Cursor (Rules-First):**

```
my-workspace/
├── .cursor/
│   ├── rules/
│   │   └── behavior.mdc          # alwaysApply: true - acts as agent config
│   ├── commands/
│   │   └── create-post.md
│   └── agents/
│       └── content-reviewer.md   # Subagent specialist
├── context/
│   ├── core/
│   │   └── quality-standards.md
│   └── content/
│       ├── voice-guidelines.md
│       └── templates.md
└── output/
```

**OpenCode / Claude Code:**

```
my-workspace/
├── .opencode/                    # or .claude/
│   ├── commands/
│   │   └── create-post.md
│   └── agents/
│       └── content-writer.md     # Primary agent
├── context/
│   └── ...
└── output/
```

## Learn More

See [SKILL.md](SKILL.md) for the complete skill instructions and [templates.md](templates.md) for ready-to-use templates.

## Inspiration

This skill was inspired by this video on Youtube:**[
5 Steps to to Revolutionize Your Workflow with OpenCode](https://www.youtube.com/watch?v=0pL5kHbXk2M)** and the corresponding [repo](https://github.com/darrenhinde/personal-agent-systems).

## License

MIT License - see [LICENSE](LICENSE) for details.
