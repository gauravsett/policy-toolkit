# Policy Toolkit

This is a community repository of reusable tools and workflows for AI-assisted policy research.

## Repository structure

- `tools/` — Installable artifacts (skills, AGENTS.md starters, agent configs). Each tool is a self-contained folder with a README.
- `workflows/` — Multi-step processes that combine tools for end-to-end policy research tasks.
- `CONTRIBUTING.md` — How to add new tools or workflows.

## Conventions

- Each tool or workflow lives in its own folder with a README explaining what it does, how to install/use it, and which frameworks it supports.
- Skills follow the Agent Skills open standard (SKILL.md with YAML frontmatter).
- Tools should note framework compatibility (Claude Code, Codex, etc.) in their README.

## When working in this repo

- If someone asks to add a new tool, create a folder in `tools/` with at minimum a README.md.
- If the tool is a skill, include a SKILL.md following the Agent Skills format.
- If someone asks to add a workflow, create a folder in `workflows/` with a README.md.
- Refer to CONTRIBUTING.md for the expected structure.
- If you modify this file (AGENTS.md), make the equivalent update to CLAUDE.md so they stay in sync.
