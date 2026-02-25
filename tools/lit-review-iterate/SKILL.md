---
name: lit-review-iterate
description: Iterates on an existing literature review collection through citation analysis and cluster analysis, then generates new queries, retrieves candidates, and presents them for human review. Use iteratively after an initial collection exists.
---

# Literature Review: Iterate

## Overview

This skill iteratively expands a literature review collection by mining the existing papers for leads. It analyzes citations and clusters to surface gaps and generate new retrieval directions, then runs the standard filter/rank/present cycle. Repeat until the collection is sufficient in breadth and depth.

## Expected Input

- **Required**:
  - A literature review specification
  - An existing collection of papers (from prompt)
- **Optional**: Notes from prior augmentation rounds (what was already searched, what clusters were identified)

## Expected Output

- **Deliverable**: A ranked list of new candidate papers for human review
- **Format**: Three-tier list with rough provenance notes (see Output Format below)

---

## Step 1: Citation Analysis

Read the papers in the existing collection and identify works that are cited prominently across multiple papers.

**Process:**
- Scan reference sections across all papers in the collection
- Count how many papers in the collection cite each external work
- Flag works cited by 3+ papers as likely foundational
- Note the context in which each work is cited (what argument it supports)

**Output:** A ranked list of frequently cited external works not yet in the collection, with citation counts and context notes.

---

## Step 2: Cluster Analysis

Group the existing collection by intellectual tradition, topic, or methodology to identify the shape of the literature and surface gaps.

**Clustering approach:**
- Identify natural groupings by topic focus, theoretical framework, or empirical domain
- Label each cluster descriptively (e.g., "institutional design — comparative approaches", "regulatory impact — quantitative methods")
- Note which clusters are well-represented and which are thin

**For each cluster, generate leads by asking:**
- What are the foundational texts in this cluster? (likely already surfaced in citation analysis)
- Where are more works like these found? (specific journals, venues, authors, research centers)
- What are the divergent or dissenting views within this cluster?
- What are the opposing frameworks or alternative schools of thought?
- What empirical domains or case studies are underrepresented?
- What are the empirical tests of the theories in this cluster?
- What cross-disciplinary imports affect this literature?
- What structural sections would a top-tier journal reviewer expect that are missing? (e.g., measurement debates, method critiques, international comparisons)

**Also ask across the full collection:**
- What alternative frameworks or paradigms would a hostile reviewer say the collection ignores entirely?
- Of all gaps identified, which missing literature would most weaken the argument if a reviewer noticed it? (Prioritize these in Step 3.)

**Output:** A set of retrieval leads per cluster, plus a short prioritized gap list for Step 3.

---

## Step 3: Query Generation

Convert the leads from Steps 1–2 into a new set of search queries.

**Query design principles:**

1. **Prioritize gaps**: Focus queries on gaps identified in the cluster analysis over topics already well-covered.
2. **Mine existing results for terms**: Use titles, abstracts, and keywords from collected papers to discover terminology not in prior queries.
3. **Target specific leads**: Generate queries for specific authors, venues, or sub-topics surfaced in citation/cluster analysis.
4. **Seek dissent**: Include queries aimed at dissenting, critical, or underrepresented perspectives.
5. **Adapt to the platform**: Use simple, concept-focused queries for Semantic Scholar; use broader phrasing for WebSearch.
6. **Avoid redundancy**: Do not re-run queries likely to surface papers already in the collection.
7. **Target 10–20 new queries** per augmentation round.

---

## Step 4: Retrieval

Execute each query using the WebSearch tool and the Semantic Scholar API. For each result, collect: title, authors, year, venue, abstract, URL/DOI, and citation count.

**Web search** — use the WebSearch tool directly (not via Bash/curl). Use it to find government reports, think tank publications, and other non-academic sources. Use WebFetch to retrieve content from specific URLs when needed.

**Semantic Scholar API** — use the Bash tool with curl. If available, set the API key in `.env` as `SEMANTIC_SCHOLAR_API_KEY` for higher rate limits; the API also works without a key at lower rate limits (100 requests/5 minutes).
- Search: `GET https://api.semanticscholar.org/graph/v1/paper/search?query=<query>&fields=title,authors,year,venue,abstract,citationCount,externalIds,openAccessPdf&limit=50`
  - Header (if key available): `x-api-key: $SEMANTIC_SCHOLAR_API_KEY`
- Paper details: `GET https://api.semanticscholar.org/graph/v1/paper/<paperId>?fields=title,authors,year,abstract,citationCount,references,citations`
  - Header (if key available): `x-api-key: $SEMANTIC_SCHOLAR_API_KEY`
- Optional filters (use only when appropriate, not by default): `year=2015-` (range), `minCitationCount=10`, `fieldsOfStudy=Political Science`, `publicationTypes=JournalArticle,Review`
- For citation analysis: use the `references` and `citations` fields on paper details to do forward/backward citation expansion.

Deduplicate against the existing collection and against each other.

---

## Step 5: Filter and Rank

Apply the same filter and rank logic as in `lit-review-initiate`:

**Filter** out results that:
- Are already in the collection
- Are in excluded source types or languages
- Fall outside included date ranges (unless seminal)
- Focus primarily on excluded topics
- Are clearly not substantively relevant to the research question

**Rank** remaining results into three tiers:
- **Highly Recommended**: Strong relevance, hits priority criteria, high quality, fills an identified gap
- **Recommended**: Solid fit without hitting priority criteria
- **Optional**: Plausible but uncertain fit

For each result, write a rough note explaining provenance: which query, which cluster gap, which citation lead, or which foundational work it relates to.

---

## Step 6: Human Review Presentation

Present results in three sections:

**Section 1 — Highly Recommended**: Strong fit, fills a clear gap.
**Section 2 — Recommended**: Solid fit, worth reviewing.
**Section 3 — Optional**: Lower confidence, human can skim or skip.

Each entry: title, authors, year, venue, link, and rough note. Human selects papers to download and add to the collection.

---

## Output Format

```
## Highly Recommended

1. **Title** — Author(s) (Year). *Venue*.
   Link: [URL or DOI link]
   Note: [provenance, e.g., "cited by 5 papers in collection; cluster gap: comparative regulatory frameworks"]

2. ...

## Recommended

1. **Title** — Author(s) (Year). *Venue*.
   Link: [URL or DOI link]
   Note: [rough note]

2. ...

## Optional

1. **Title** — Author(s) (Year). *Venue*.
   Link: [URL or DOI link]
   Note: [rough note]

2. ...
```
