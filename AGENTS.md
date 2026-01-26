# AGENTS.md

This file provides guidance to AI coding agents (Claude Code, OpenCode, Cursor, etc.) when working with code in this repository.

## Repository Overview

A collection of AI toolkits that extend agent capabilities, including:

- **Skills** - Packaged instructions and scripts that can be distributed and installed
- **Commands** - Command templates and prompt definitions for agent execution

## Skills

Skills are packaged, distributable units that extend AI agent capabilities. They follow the [Agent Skills](https://agentskills.io/) format and can be installed via `npx skills add <owner/repo>`.

### Directory Structure

```
skills/
  {skill-name}/           # kebab-case directory name
    SKILL.md              # Required: skill definition with frontmatter
    scripts/              # Optional: executable scripts
      {script-name}.sh    # Bash scripts (preferred)
    references/           # Optional: supporting documentation
      {doc-name}.md       # Reference materials
```

### Naming Conventions

- **Skill directory**: `kebab-case` (e.g., `vercel-deploy`, `log-monitor`)
- **SKILL.md**: Always uppercase, always this exact filename
- **Scripts**: `kebab-case.sh` (e.g., `deploy.sh`, `fetch-logs.sh`)
- **Zip file**: Must match directory name exactly: `{skill-name}.zip`

### SKILL.md Format

```markdown
---
name: {skill-name}
description: {One sentence describing when to use this skill. Include trigger phrases like "Deploy my app", "Check logs", etc.}
---

# {Skill Title}

{Brief description of what the skill does.}

## How It Works

{Numbered list explaining the skill's workflow}

## Usage

bash ~/.agents/skills/{skill-name}/scripts/{script}.sh [args]
```

**Arguments:**
- `arg1` - Description (defaults to X)

**Examples:**
{Show 2-3 common usage patterns}

### Output

{Show example output users will see}

### Present Results to User

{Template for how Claude should format results when presenting to users}

### Troubleshooting

{Common issues and solutions, especially network/permissions errors}

```
### Best Practices for Context Efficiency

Skills are loaded on-demand — only the skill name and description are loaded at startup. The full `SKILL.md` loads into context only when the agent decides the skill is relevant. To minimize context usage:

- **Keep SKILL.md under 500 lines** — put detailed reference material in separate files
- **Write specific descriptions** — helps the agent know exactly when to activate the skill
- **Use progressive disclosure** — reference supporting files that get read only when needed
- **Prefer scripts over inline code** — script execution doesn't consume context (only output does)
- **File references work one level deep** — link directly from SKILL.md to supporting files

### Script Requirements

- Use `#!/bin/bash` shebang
- Use `set -e` for fail-fast behavior
- Write status messages to stderr: `echo "Message" >&2`
- Write machine-readable output (JSON) to stdout
- Include a cleanup trap for temp files
- Reference the script path as `~/.agents/skills/{skill-name}/scripts/{script}.sh`
```

Add the skill to project knowledge or paste SKILL.md contents into the conversation.

## Commands

Commands are executable prompt templates that guide AI agents to perform specific tasks. Unlike skills (which are distributed units), commands are standalone Markdown files that define task instructions.

### Directory Structure

```
commands/
  {command-name}.md      # Command definition with YAML frontmatter
  references/           # Optional: supporting documentation
    {doc-name}.md       # Reference materials
```

### Command Format

```markdown
---
description: {Brief description of when to use this command}
model: {model-identifier (optional)}
---

{Command instructions and workflow steps}
```

### Frontmatter Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `description` | string | Yes | One-line description for agent to understand when to use this command |
| `model` | string | No | Specific model to use for this command |

### Best Practices

- **Triggers matter**: Include specific phrases users might say in the description (e.g., "Commit my changes", "Check logs")
- **Be specific**: Clear instructions produce better results
- **Action-oriented**: Focus on what the agent should do, not abstract concepts
- **Examples matter**: Include example inputs/outputs where applicable

### Example

```markdown
---
description: Create conventional commit with Chinese description
model: zhipuai-coding-plan/glm-4.7
---

You are an experienced software engineer responsible for creating Git commit messages...

## Workflow
1. Inspect changes
2. Stage files
3. Write commit message
4. Execute commit
```

## Usage Summary

| Type | When to Use | Key Characteristic |
|------|-------------|-------------------|
| **Skills** | Reusable capabilities that should be distributed across projects | Installable via `npx skills add <owner/repo>`, include scripts |
| **Commands** | One-off or project-specific task instructions | Simple markdown files, not distributed |
