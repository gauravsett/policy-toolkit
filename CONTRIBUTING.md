# Contributing

We welcome contributions from policy researchers, analysts, and anyone using AI tools for policy work. You don't need to be a developer to contribute.

## What to contribute

### Tools

Anything installable or copyable that makes an AI coding agent more useful for policy work:

- **Skills** — Reusable capabilities invoked as slash commands (e.g., `/literature-review`, `/draft-memo`)
- **Starter configs** — CLAUDE.md or AGENTS.md files tailored for policy research projects
- **Agent definitions** — Specialized subagent configurations for policy tasks
- **Hooks** — Automated checks or enforcement (e.g., citation verification)

### Workflows

Multi-step processes that show how to combine tools (or just use an AI agent effectively) for end-to-end policy research tasks. For example: how to go from a research question to a published policy brief.

## How to contribute a tool

1. Create a folder in `tools/` with a short, descriptive name (e.g., `tools/literature-review/`)

2. Add a **README.md** with these sections:

   ```markdown
   # Tool Name

   Brief description of what this tool does.

   ## Installation

   How to install or copy this into your project.

   ## Usage

   How to use it, with examples.

   ## Frameworks

   Which frameworks this works with (Claude Code, Codex, etc.)
   and any that it has been tested with.
   ```

3. If your tool is a **skill**, include a **SKILL.md** following the [Agent Skills](https://agentskills.io) format:

   ```markdown
   ---
   name: your-skill-name
   description: A clear description of what this skill does and when to invoke it.
   ---

   # Your Skill Name

   Instructions that the AI agent follows when this skill is invoked.
   ```

4. Include any supporting files the tool needs (scripts, reference documents, templates).

5. Open a pull request.

## How to contribute a workflow

1. Create a folder in `workflows/` with a short, descriptive name (e.g., `workflows/research-to-memo/`)

2. Add a **README.md** with these sections:

   ```markdown
   # Workflow Name

   Brief description of what this workflow accomplishes.

   ## Prerequisites

   Any tools, skills, or setup needed before starting.

   ## Steps

   Step-by-step walkthrough of the process.
   ```

3. Include any supporting files (prompt templates, example outputs, scripts).

4. Open a pull request.

## Quality standards

- Every contribution must have a **README.md** explaining what it does and how to use it.
- Test your tool or workflow with at least one framework before submitting.
- Do not include API keys, secrets, or personal data.
- Keep skill instructions focused — one capability per skill works better than trying to do everything.

## Updating the catalog

When you add a new tool or workflow, also add a row to the corresponding table in [README.md](README.md) so others can discover it.
