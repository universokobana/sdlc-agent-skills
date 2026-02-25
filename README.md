*[Leia em Português](README.pt-BR.md)*

> **Note:** This repository is based on the [Agent Skills standard](http://agentskills.io) for Claude. It contains SDLC (Software Development Lifecycle) skills for automating development workflows.

# Skills

Skills are folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. Skills teach Claude how to complete specific tasks in a repeatable way.

For more information, check out:
- [What are skills?](https://support.claude.com/en/articles/12512176-what-are-skills)
- [Using skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude)
- [How to create custom skills](https://support.claude.com/en/articles/12512198-creating-custom-skills)
- [Equipping agents for the real world with Agent Skills](https://anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

# About This Repository

This repository contains SDLC skills for automating software development workflows with Claude — including PR reviews, CI fixes, and code quality automation.

## Available Skills

| Skill | Description |
|-------|-------------|
| [fix-github-pr](./skills/fix-github-pr) | Fix GitHub PR review comments, Copilot suggestions, and CI test failures |

## Disclaimer

**These skills are provided for demonstration and educational purposes only.** Always test skills thoroughly in your own environment before relying on them for critical tasks.

# Repository Structure

- [./skills](./skills): SDLC automation skills
- [./spec](./spec): The Agent Skills specification
- [./template](./template): Skill template

# Try in Claude Code, Claude.ai, and the API

## Claude Code

You can register this repository as a Claude Code Plugin marketplace by running the following command in Claude Code:
```
/plugin marketplace add universokobana/sdlc-agent-skills
```

Then, to install the skills:
1. Select `Browse and install plugins`
2. Select `sdlc-agent-skills`
3. Select `sdlc-agent-skills`
4. Select `Install now`

Alternatively, directly install via:
```
/plugin install sdlc-agent-skills@sdlc-agent-skills
```

After installing the plugin, you can use the skill by just mentioning it. For example:
- "Fix PR #42"
- "Fix the review comments on my PR"
- "Fix CI failures on this PR"

## Claude.ai

To use any skill from this repository or upload custom skills, follow the instructions in [Using skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude#h_a4222fa77b).

## Claude API

You can use pre-built skills, and upload custom skills, via the Claude API. See the [Skills API Quickstart](https://docs.claude.com/en/api/skills-guide#creating-a-skill) for more.

# Creating a Basic Skill

Skills are simple to create - just a folder with a `SKILL.md` file containing YAML frontmatter and instructions. You can use the **template** in this repository as a starting point:

> **Important:** When creating or removing skills, you must update the following files:
> - `.claude-plugin/marketplace.json` - Register/unregister the skill in the `plugins[0].skills` array
> - `README.md` and `README.pt-BR.md` - Update the "Available Skills" table
> - `CLAUDE.md` - Update the repository structure and available skills sections

```markdown
---
name: my-skill-name
description: A clear description of what this skill does and when to use it
---

# My Skill Name

[Add your instructions here that Claude will follow when this skill is active]

## Examples
- Example usage 1
- Example usage 2

## Guidelines
- Guideline 1
- Guideline 2
```

The frontmatter requires only two fields:
- `name` - A unique identifier for your skill (lowercase, hyphens for spaces)
- `description` - A complete description of what the skill does and when to use it

The markdown content below contains the instructions, examples, and guidelines that Claude will follow. For more details, see [How to create custom skills](https://support.claude.com/en/articles/12512198-creating-custom-skills).
