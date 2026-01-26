# AI Toolkits

A collection of skills for AI agents. Skills are packaged instructions and scripts that extend agent capabilities.

Skills follow the [Agent Skills](https://agentskills.io/) format.

## Available Skills

### commit-work

Create high-quality git commits with logical scoping and clear messages. Follows Conventional Commits format.

**Use when:**
- "Commit my changes"
- "Craft a commit message"
- "Stage changes"
- "Split work into multiple commits"

**Features:**
- Reviews working tree before staging
- Splits commits by logical boundaries (feature/refactor, backend/frontend, tests/prod)
- Supports patch staging for mixed changes
- Enforces Conventional Commits format
- Sanity checks for secrets, debug logging, and formatting churn

**Workflow:**
1. Inspect working tree (`git status`, `git diff`)
2. Decide commit boundaries (split when needed)
3. Stage with patch mode (`git add -p`)
4. Review staged changes (`git diff --cached`)
5. Write commit message following Conventional Commits
6. Run verification (tests, lint, build)
7. Repeat for remaining changes

**Commit message format:**
```
<type>(<scope>): <summary>

<What changed.>
<Why it changed.>
```

## Installation

```bash
npx add-skill catch6/ai-toolkits
```

## Usage

Skills are automatically available once installed. The agent will use them when relevant tasks are detected.

**Examples:**
```
Commit my changes
```
```
Help me split these changes into logical commits
```
```
Write a commit message for these changes
```

## Skill Structure

Each skill contains:
- `SKILL.md` - Instructions for the agent
- `scripts/` - Helper scripts for automation (optional)
- `references/` - Supporting documentation (optional)

## License

MIT
