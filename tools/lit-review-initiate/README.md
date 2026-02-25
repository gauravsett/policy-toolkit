# Literature Review: Initiate

A skill that runs the first pass of a literature review when no papers exist yet. Given a literature review specification, it generates search queries, retrieves candidate papers from academic and web sources, filters and ranks them, and presents results in three tiers for human selection.

## Installation

Copy the `lit-review-initiate` folder into your agent's skills directory:

- **Claude Code**: `~/.claude/skills/lit-review-initiate/` (personal) or `.claude/skills/lit-review-initiate/` (project)

Then invoke with `/lit-review-initiate`.

## Usage

1. Write a literature review spec defining your research question, topic inclusion/exclusion criteria, source types, date ranges, and language preferences.
2. Invoke the skill and provide the spec (inline or as a file path).
3. The agent will generate search queries, retrieve papers via Semantic Scholar and web search, filter and rank results, and present them for your review.
4. Review the three-tier output (Highly Recommended / Recommended / Optional) and select papers to keep.

### Optional: Semantic Scholar API key

The skill uses the Semantic Scholar API, which works without authentication at lower rate limits (100 requests/5 minutes). For higher throughput, add your API key to `.env`:

```
SEMANTIC_SCHOLAR_API_KEY=your-key-here
```

## Frameworks

- **Claude Code**: Tested. Requires WebSearch and Bash tool access.
- **Codex**: Should work with equivalent tool access. Not yet tested.
