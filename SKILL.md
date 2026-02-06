---
name: agentic-workspace-setup
description: Set up an AI-agent workspace with the three-layer architecture (commands → context → agents). Use when starting a new project that needs orchestrated AI workflows, creating personal assistants, automating multi-step tasks, or when the user mentions setting up agents, MCP servers, or agentic workflows.
---

# Agentic Workspace Setup

## Overview

Set up workspaces with a three-layer architecture that enables orchestrated AI workflows:

```
User Input → Command → Context Injection → Agent Execution → Output
```

This skill guides users through a discovery process, then implements the workspace.

## The Process

This skill has three phases:

1. **Discovery Phase** - Understand requirements through dialogue
2. **Design Phase** - Present architecture for approval
3. **Implementation Phase** - Create the workspace structure

---

## Phase 1: Discovery

Guide the user through understanding their workspace needs. Follow brainstorming principles:

-   **One question at a time** - Don't overwhelm with multiple questions
-   **Multiple choice preferred** - Easier to answer than open-ended
-   **Research actively** - Look up available skills, MCP servers, and patterns that could help

### Discovery Flow

```
1. Platform Selection (if not specified)
2. Domain & Purpose
3. Core Workflows (3-5 main tasks)
4. Knowledge Requirements
5. Tool/MCP Needs
6. Existing Resources to Leverage
```

### Question 1: Platform Selection

**If user hasn't specified platforms, ask:**

> Which agent platform(s) will you use for this workspace?
>
> -   [ ] **Cursor** - IDE with built-in agent support
> -   [ ] **Claude Code** - CLI-based coding agent
> -   [ ] **OpenCode** - Open-source terminal agent
> -   [ ] **Other** - Please specify
>
> (Select all that apply - the workspace can support multiple platforms)

**Platform differences:**

| Platform    | Config Location | Command Format            | Agent Format                      | Agent Model                |
| ----------- | --------------- | ------------------------- | --------------------------------- | -------------------------- |
| Cursor      | `.cursor/`      | `.cursor/commands/*.md`   | `.cursor/agents/*.md` (subagents) | Subagents only (see below) |
| Claude Code | `.claude/`      | `.claude/commands/*.md`   | CLAUDE.md                         | Primary + subagents        |
| OpenCode    | `.opencode/`    | `.opencode/commands/*.md` | `.opencode/agents/*.md`           | Primary + subagents        |

**⚠️ Cursor Platform Limitation:**

Cursor's main agent cannot be customized or replaced. Custom modes were removed from Cursor and replaced by slash commands. For Cursor workspaces:

-   **Rules replace primary agent config** - Use `.cursor/rules/*.mdc` with `alwaysApply: true` for persistent behavioral context
-   **Agents are subagents only** - Files in `.cursor/agents/` are specialists the main agent delegates to, not replacements
-   **Commands orchestrate** - Commands load context via `@` references and can suggest delegation to subagents

### Question 2: Domain & Purpose

> What domain will this workspace serve?
>
> Examples: content creation, research, customer support, data analysis, personal productivity, software development, etc.
>
> In one sentence, what's the primary purpose?

### Question 3: Core Workflows

> What are the 3-5 main tasks you'll perform in this workspace?
>
> For each, briefly describe:
>
> -   What triggers it (command name or user request)
> -   What output it produces
>
> Example:
>
> -   `/blog-post "topic"` → produces a formatted blog post
> -   `/research "query"` → produces a research summary with sources

### Question 4: Knowledge Requirements

> What domain-specific knowledge does the agent need that it wouldn't already know?
>
> Consider:
>
> -   **Voice/tone guidelines** - How should outputs sound?
> -   **Patterns/templates** - Specific structures to follow?
> -   **Rules/constraints** - What must always/never happen?
> -   **Examples** - Reference materials to learn from?

### Question 5: Tool/MCP Needs

**Before asking, research available MCP servers:**

```
Research available MCP servers at:
- https://github.com/modelcontextprotocol/servers
- https://mcp.so/servers
- User's existing MCP configurations
```

> Based on your workflows, here are MCP servers that could help:
>
> [Present researched options relevant to their domain]
>
> Which external capabilities do you need?
>
> -   [ ] Web search (brave-search, tavily)
> -   [ ] File system access
> -   [ ] Database connections
> -   [ ] API integrations
> -   [ ] Other: \_\_\_

### Question 6: Existing Resources

**Research user's existing skills and patterns:**

```
Check for existing resources:
- ~/.cursor/skills/ - Global skills
- .cursor/skills/ - Project skills
- Existing context files in project
- CLAUDE.md or similar configuration
```

> I found these existing resources that might be relevant:
>
> [List discovered skills, agents, or patterns]
>
> Should we:
>
> -   [ ] Integrate with existing skills (which ones?)
> -   [ ] Create everything fresh
> -   [ ] Mix: use some existing, create new for gaps

---

## Phase 2: Design Presentation

Once discovery is complete, present the design in sections (200-300 words each). Check after each section.

### Section 1: Architecture Overview

Present:

-   Folder structure for selected platform(s)
-   How the three layers will work together
-   High-level workflow diagram

Ask: "Does this architecture look right?"

### Section 2: Context Files

Present:

-   List of context files to create
-   Purpose of each file
-   Key content for each

Ask: "Are these the right context files? Any missing?"

### Section 3: Agents

**For Claude Code / OpenCode:**

Present:

-   Primary agent role and responsibilities
-   Subagent breakdown (if applicable)
-   How agents interact

**For Cursor (subagent-only model):**

Present:

-   How rules will configure the main agent's behavior (pseudo-agent config)
-   Subagent specialists to create (delegated tasks)
-   When the main agent should delegate to each subagent

Ask: "Does this agent structure make sense?"

### Section 4: Commands

Present:

-   Command names and triggers
-   Which context each loads
-   Expected outputs

Ask: "Are these the right commands?"

### Section 5: MCP Configuration

Present:

-   Selected MCP servers
-   Configuration for each platform
-   How agents will use them

Ask: "Ready to implement?"

---

## Phase 3: Implementation

Once design is validated, create the workspace.

### Implementation Checklist

**For Claude Code / OpenCode:**

```
Workspace Setup:
- [ ] Create folder structure
- [ ] Write context files
- [ ] Create agents (primary + subagents)
- [ ] Write commands
- [ ] Configure MCP servers
- [ ] Verify one workflow end-to-end
```

**For Cursor:**

```
Workspace Setup:
- [ ] Create folder structure
- [ ] Write context files
- [ ] Create rules (behavior.mdc with alwaysApply: true)
- [ ] Create subagents (specialists for delegation)
- [ ] Write commands (with @ references and delegation hints)
- [ ] Configure MCP servers
- [ ] Verify one workflow end-to-end
```

### Verification

Test one complete workflow before finishing:

-   [ ] Command triggers and loads context correctly
-   [ ] Agent demonstrates domain knowledge from context files
-   [ ] Output follows expected format
-   [ ] Files save to correct location (if applicable)

### Platform-Specific Structures

**Cursor (Rules-First Architecture):**

```
project/
├── .cursor/
│   ├── rules/                    # Primary behavioral config
│   │   ├── behavior.mdc          # alwaysApply: true - acts as agent config
│   │   └── domain/
│   │       └── patterns.mdc      # Intelligent apply based on context
│   ├── commands/
│   │   └── workflows/
│   ├── agents/                   # Subagents (delegated specialists)
│   │   └── specialists/
│   └── skills/                   # Optional: skill files for reference
├── context/
│   ├── core/
│   └── domain/
└── output/
```

> **Why rules-first?** Since Cursor's main agent cannot be customized, rules with `alwaysApply: true` serve as the primary way to inject persistent behavioral context (voice, constraints, patterns).

**OpenCode:**

```
project/
├── .opencode/
│   ├── commands/
│   ├── agents/
│   └── context/
│       ├── core/
│       └── domain/
├── opencode.json
└── output/
```

**Claude Code:**

```
project/
├── .claude/
│   └── commands/        # Custom slash commands
├── CLAUDE.md            # Main agent configuration
├── context/
│   └── domain/
└── output/
```

**Multi-Platform (Cursor + OpenCode):**

```
project/
├── .cursor/
│   ├── commands/
│   └── agents/
├── .opencode/
│   ├── commands/
│   └── agents/
├── context/             # Shared context
│   ├── core/
│   └── domain/
├── opencode.json
└── output/
```

---

## Reference: Cursor-Specific Guidance

Since Cursor's main agent is locked, use this adapted approach:

### Rules as Pseudo-Agent Config

Create `.cursor/rules/behavior.mdc` with `alwaysApply: true`:

```markdown
---
description: "Core behavioral configuration for this workspace"
alwaysApply: true
---

## Role & Voice

You are a [Role] working on [Domain]. When responding:

-   Use [tone/voice guidelines]
-   Follow [communication patterns]

## Core Constraints

-   Always [required behavior]
-   Never [prohibited behavior]

## Output Standards

-   [Format requirements]
-   [Quality expectations]
```

### Subagent Structure for Cursor

Subagents in `.cursor/agents/` are specialists the main agent delegates to:

```markdown
---
name: security-reviewer
description: Reviews code for security vulnerabilities including injection, XSS, and hardcoded secrets
---

## Role

You are a security specialist who reviews code for vulnerabilities.

## Focus Areas

-   SQL/NoSQL injection
-   Cross-site scripting (XSS)
-   Hardcoded secrets and credentials
-   Authentication/authorization flaws

## Output

Provide a structured report with:

1. Severity (Critical/High/Medium/Low)
2. Location (file:line)
3. Description
4. Recommended fix
```

### Commands That Orchestrate Delegation

Commands can suggest when the main agent should delegate:

```markdown
---
name: security-audit
---

@context/security/standards.md

Perform a comprehensive security review of the codebase.

**Important:** Delegate the detailed code review to the security-reviewer subagent.

Report findings in a structured format with severity levels.
```

---

## Reference: Three-Layer Architecture

| Layer        | Purpose                                          | Location                      |
| ------------ | ------------------------------------------------ | ----------------------------- |
| **Commands** | Entry points that load context and invoke agents | Platform-specific             |
| **Context**  | Domain knowledge, patterns, rules, examples      | `context/` or platform folder |
| **Agents**   | Execute tasks with loaded context                | Platform-specific             |

**Key principle:** Commands are context loaders, not just shortcuts.

**Cursor adaptation:** The "Agents" layer becomes "Subagents + Rules" where rules handle main agent behavior and subagents handle delegated specialist tasks.

---

## Reference: Context File Structure

```markdown
# [Domain] - [Specific Area]

## Core Principles

-   Principle 1: Description
-   Principle 2: Description

## Patterns

### Pattern Name

-   When to use
-   How to apply
-   Example

## Quality Standards

-   [ ] Checklist item 1
-   [ ] Checklist item 2

## Examples

[Concrete examples with explanations]
```

**Best practices:**

-   50-150 lines per file
-   Specific patterns over general advice
-   Include concrete examples
-   Organize hierarchically

---

## Reference: Agent Structure

```markdown
---
name: agent-name
description: What this agent does and when to use it
model: inherit
---

## Role

You are a [Role Title] who [primary responsibility].

## Context Awareness

-   Apply [context-file-1] for [purpose]
-   Use [context-file-2] to ensure [quality]

## Process

1. **ANALYZE** the request
2. **VALIDATE** prerequisites
3. **EXECUTE** the task
4. **VERIFY** quality

## Output Standards

-   [Standard 1]
-   [Standard 2]
```

---

## Reference: Command Structure

```markdown
---
name: command-name
agent: target-agent
---

@context/core/standards.md
@context/domain/patterns.md

You are my [Role].

**Request:** $ARGUMENTS

[Instructions]

## Output Format

[Specification]
```

---

## Anti-Patterns

| Avoid                                       | Do Instead                                             |
| ------------------------------------------- | ------------------------------------------------------ |
| Generic context ("write well")              | Specific patterns ("use H2 for sections")              |
| Overloading context (5+ files)              | Limit to 2-4 focused files                             |
| Vague agent prompts                         | Clear role, process, output format                     |
| Commands without context                    | Always inject relevant domain knowledge                |
| Monolithic agents                           | Split into orchestrator + specialized subagents        |
| Skipping discovery                          | Always understand requirements first                   |
| **Cursor:** Expecting custom primary agents | Use `alwaysApply` rules for behavioral config          |
| **Cursor:** Putting behavior in agents/     | Agents are subagents only; use rules for main behavior |

---

## Additional Resources

For detailed templates and examples, see [templates.md](templates.md).
