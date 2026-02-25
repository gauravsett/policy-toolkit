# Literature Review: Iterate

A skill that iteratively expands an existing literature review collection. It mines your current papers for citation patterns and thematic clusters, identifies gaps, generates targeted search queries, and presents new candidates for human review.

Use this after you have an initial collection (e.g., from [lit-review-initiate](../lit-review-initiate/)).

## Installation

Copy the `lit-review-iterate` folder into your agent's skills directory:

- **Claude Code**: `~/.claude/skills/lit-review-iterate/` (personal) or `.claude/skills/lit-review-iterate/` (project)

Then invoke with `/lit-review-iterate`.

## Usage

1. Have an existing paper collection and your literature review spec ready.
2. Invoke the skill, providing the spec and pointing the agent to your collected papers.
3. The agent will:
   - Analyze citations across your collection to find frequently referenced works you don't have yet
   - Cluster your papers by topic/framework to identify gaps
   - Generate new search queries targeting those gaps
   - Retrieve, filter, rank, and present candidates
4. Review the three-tier output and select papers to add.
5. Repeat until your collection has sufficient breadth and depth.

### Optional: Semantic Scholar API key

The skill uses the Semantic Scholar API, which works without authentication at lower rate limits (100 requests/5 minutes). For higher throughput, add your API key to `.env`:

```
SEMANTIC_SCHOLAR_API_KEY=your-key-here
```

## Frameworks

- **Claude Code**: Tested. Requires WebSearch and Bash tool access.
- **Codex**: Should work with equivalent tool access. Not yet tested.
