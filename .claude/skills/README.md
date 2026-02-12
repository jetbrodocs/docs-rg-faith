# Project Skills

This directory contains custom Claude Code skills for the RG Faith inventory tracking project. These skills are automatically discovered and loaded when you start a Claude Code session in this project.

## Available Skills

| Skill | Invocation | Auto-loads when |
|-------|-----------|----------------|
| **process-mapping** | `/process-mapping` | Working in `20-process-maps/` folder |
| **observation-capture** | `/observation-capture` | Working in `10-observations/` folder |
| **solution-design** | `/solution-design` | Working in `40-solution-design/` folder |
| **documentation-reviewer** | `/documentation-reviewer` | Reviewing or auditing documentation |
| **documentation-writer** | *(background only)* | Applied automatically to all documentation work |

## How Skills Work

### Automatic Loading
Claude Code reads the `description` field in each skill's YAML frontmatter and automatically loads the skill when your request semantically matches. For example:
- "Create a process map for packing" → auto-loads `process-mapping`
- "Review the observation files" → auto-loads `documentation-reviewer`

### Manual Invocation
You can explicitly invoke any skill using slash commands:
```
/process-mapping
/observation-capture
/solution-design
/documentation-reviewer
```

### Background Skills
The `documentation-writer` skill has `user-invocable: false`, meaning it only applies automatically as baseline guidance. You cannot invoke it manually.

## Skill Structure

Each skill follows this structure:
```
skill-name/
└── SKILL.md          # Main instructions with YAML frontmatter
```

The `SKILL.md` format:
```yaml
---
name: skill-name
description: What this skill does and when to use it
user-invocable: true|false     # Optional, defaults to true
---

# Markdown instructions for Claude...
```

## Modifying Skills

To update a skill:
1. Edit the corresponding `SKILL.md` file
2. Commit the changes to git
3. Skills are loaded at session start, so restart your session to see changes

## Adding New Skills

1. Create a new directory: `.claude/skills/new-skill-name/`
2. Add a `SKILL.md` file with proper YAML frontmatter
3. Commit to git
4. Restart your Claude Code session

## References

- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills.md)
- Project glossary and context: `CLAUDE.md` in root
