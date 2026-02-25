# Claude Instructions for SDLC Agent Skills

This repository contains SDLC (Software Development Lifecycle) skills for automating development workflows with Claude.

## Repository Structure

```
sdlc-agent-skills/
├── skills/
│   └── fix-github-pr/         # Fix GitHub PR review comments and CI failures
├── spec/                      # Agent Skills specification
└── template/                  # Skill template
```

## Creating New Skills

**IMPORTANT**: When creating or removing skills, you MUST update the `.claude-plugin/marketplace.json` file to register/unregister the skill in the `plugins[0].skills` array.

## Available Skills

### fix-github-pr
- **Purpose**: Systematically fix GitHub PR review comments, Copilot suggestions, and CI test failures
- **Documentation**: `skills/fix-github-pr/SKILL.md`
- **Triggers**: "fix PR", "fix PR comments", "resolve review", "address Copilot feedback", "fix CI", "fix failing tests on PR"
