# Agentic Workspace Setup

A skill for setting up AI-agent workspaces with a three-layer architecture.

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

| Platform    | Config Location                            |
| ----------- | ------------------------------------------ |
| Cursor      | `.cursor/commands/`, `.cursor/agents/`     |
| Claude Code | `.claude/commands/`, `CLAUDE.md`           |
| OpenCode    | `.opencode/commands/`, `.opencode/agents/` |

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

```
my-workspace/
├── .cursor/
│   ├── commands/
│   │   └── create-post.md
│   └── agents/
│       └── content-writer.md
├── context/
│   ├── core/
│   │   └── quality-standards.md
│   └── content/
│       ├── voice-guidelines.md
│       └── templates.md
└── output/
```

## Learn More

See [SKILL.md](SKILL.md) for the complete skill instructions and [templates.md](templates.md) for ready-to-use templates.
