# Literature Review Workflow

An end-to-end process for building a literature review collection using AI-assisted search, from an empty collection to a comprehensive set of papers ready for synthesis.

## Tools used

- [lit-review-initiate](../../tools/lit-review-initiate/) — Initiate: generates queries from a spec and retrieves an initial set of candidates
- [lit-review-iterate](../../tools/lit-review-iterate/) — Iterate: mines an existing collection for citation leads and gaps, then retrieves new candidates

## Prerequisites

- Both tools installed in your agent's skills directory
- A literature review specification (see below)
- Optional: Semantic Scholar API key in `.env` for higher rate limits

## Steps

### 1. Write a literature review spec

Define your review's scope before invoking any tools. Your spec should include:

- **Research question**: The guiding question the literature should answer
- **Topics**: What to include, prioritize, and exclude (match by substantive focus, not mere mention)
- **Sources**: What source types to include, prioritize, and exclude (e.g., peer-reviewed journals, government reports, think tank publications)
- **Dates**: Publication year ranges to include, prioritize, and exclude
- **Language**: What languages to include and exclude

Save this as a file in your project (e.g., `lit-review-spec.md`) so both tools can reference it.

### 2. Initiate — build an initial collection

Invoke `/lit-review-initiate` with your spec. The agent will:

1. Generate 10–20 diverse search queries from your spec
2. Run them against Semantic Scholar and web search
3. Deduplicate, filter, and rank results into three tiers
4. Present candidates for your review

**Your role**: Review the output, select papers to keep, and download/save them. Note any topics that seem underrepresented — this informs the next step.

### 3. Iterate — expand the collection

Once you have an initial set of papers, invoke `/lit-review-iterate` with your spec and collection. The agent will:

1. Analyze citations across your papers to find frequently referenced works you're missing
2. Cluster your collection by topic and framework to identify gaps
3. Generate new queries targeting those gaps
4. Retrieve, filter, rank, and present new candidates

**Your role**: Review the output, select papers to add, and update your collection.

### 4. Repeat until sufficient

Run `/lit-review-iterate` again with the updated collection. Each round should surface diminishing returns as gaps are filled. Stop when:

- New rounds mostly surface papers you've already seen or rejected
- The cluster analysis shows even coverage across the topics in your spec
- You're confident a reviewer wouldn't identify a major gap

Typically 2–4 iteration rounds are sufficient, depending on the breadth of your research question.

### 5. Organize and synthesize

Once your collection is complete, you have a well-documented set of papers with provenance notes explaining why each was included. Use these notes to:

- Group papers by the clusters identified during iteration
- Identify the key debates and schools of thought
- Draft your literature review's structure around the thematic clusters

## Tips

- **Keep your spec updated**: If early rounds reveal that your scope is too broad or too narrow, revise the spec before the next iteration round.
- **Save iteration notes**: The cluster analysis and gap identification from each round are valuable context. Keep them alongside your collection so subsequent rounds can build on them.
- **Trust the tiers**: The "Optional" tier exists so you can quickly skim and move on. Don't feel obligated to read everything.
- **Quality over quantity**: A focused collection of 30–50 well-chosen papers is usually more useful than an exhaustive list of 200.
