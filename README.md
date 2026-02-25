# Policy Toolkit

Reusable tools and workflows for AI-assisted policy research using agentic development frameworks (Claude Code, OpenAI Codex, and others).

## What is this?

A community repository where policy researchers share and discover:

- **Tools** — Installable artifacts that extend your AI coding agent: skills, starter configurations (CLAUDE.md, AGENTS.md), agent definitions, hooks, and more.
- **Workflows** — Multi-step processes that show how to combine tools for end-to-end policy research tasks.

Tools follow the [Agent Skills](https://agentskills.io) open standard where applicable, so they work across Claude Code, OpenAI Codex, Gemini CLI, Cursor, and other compatible frameworks.

## Quick start

### Using a tool

1. Browse the [tools catalog](#tools) below
2. Open the tool's folder and read its README for installation instructions
3. Most skills can be installed by copying the folder to your agent's skills directory:
   - **Claude Code**: `~/.claude/skills/` (personal) or `.claude/skills/` (project)
   - **Codex**: Follow the skill's installation instructions

### Using a workflow

1. Browse the [workflows catalog](#workflows) below
2. Open the workflow's folder and follow the step-by-step README

## Tools

| Tool | Description | Frameworks |
|------|-------------|------------|
| [lit-review-initiate](tools/lit-review-initiate/) | Initiates a literature review — generates queries, retrieves papers, filters and ranks results for human review | Claude Code |
| [lit-review-iterate](tools/lit-review-iterate/) | Iteratively expands an existing literature collection via citation analysis, cluster gap detection, and targeted retrieval | Claude Code |

## Workflows

| Workflow | Description |
|----------|-------------|
| [literature-review](workflows/literature-review/) | End-to-end process for building a literature review collection, from initiation through iterative expansion |

## Contributing

We welcome contributions from policy researchers, analysts, and anyone using AI tools for policy work. See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add your own tools or workflows.

## License

[MIT](LICENSE)
