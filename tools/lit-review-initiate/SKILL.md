---
name: lit-review-initiate
description: Initiates a literature review — generates search queries from a spec, retrieves papers, filters and ranks results, and presents them for human review. Use when starting a literature review with no existing paper collection.
---

# Literature Review: Initiate

## Overview

This skill runs the first pass of a literature review when no papers exist yet. It takes a literature review spec as input, generates search queries, retrieves candidate papers, filters and ranks them against the spec criteria, and presents results in three tiers for human selection.

## Expected Input

- **Required**: A literature review specification with the following fields:
  - **Research question**: The guiding question the literature should answer
  - **Topics**: Include / Prioritize / Exclude by topic (match by substantive focus, not mere mention)
  - **Sources**: Include / Prioritize / Exclude by source type
  - **Dates**: Include / Prioritize / Exclude by publication year
  - **Language**: Include / Exclude by language
- **Format**: The spec can be provided inline or as a reference to a file

## Expected Output

- **Deliverable**: A ranked list of candidate papers for human review
- **Format**: Three-tier list (see Output Format below)

---

## Step 1: Query Generation

Read the spec carefully. Generate a diverse set of search queries that together cover the breadth of the included topics and the research question.

**Query design principles:**

1. **Decompose first**: Break the research question into 2–4 concept blocks (e.g., actor, mechanism, domain). Generate synonym-rich term sets per block — including abbreviations, spelling variants, and related terms.
2. **Adapt to the platform**: Semantic Scholar uses semantic ranking, not Boolean matching — use simple, concept-focused queries (2–5 key terms) rather than exhaustive Boolean strings. Save broader synonym exploration for WebSearch queries.
3. **Vary systematically**: Generate queries that cross concept blocks in different combinations. Include queries at different specificity levels (broad concept vs. narrow sub-topic).
4. **Cover the breadth**: Span different framings and synonyms of each included topic. Include sub-topics implied by the spec even if not explicitly named.
5. **Avoid excluded topics**: Do not generate queries that would primarily surface excluded topics.
6. **Err toward sensitivity**: Retrieving too many candidates is preferable to missing relevant papers. Precision rates of 1–5% are normal in systematic reviews.
7. **Target 10–20 queries** for a typical spec.

---

## Step 2: Retrieval

Execute each query using the WebSearch tool and the Semantic Scholar API. For each result, collect: title, authors, year, venue, abstract, URL/DOI, and citation count.

**Web search** — use the WebSearch tool directly (not via Bash/curl). Use it to find government reports, think tank publications, and other non-academic sources. Use WebFetch to retrieve content from specific URLs when needed.

**Semantic Scholar API** — use the Bash tool with curl. If available, set the API key in `.env` as `SEMANTIC_SCHOLAR_API_KEY` for higher rate limits; the API also works without a key at lower rate limits (100 requests/5 minutes).
- Search: `GET https://api.semanticscholar.org/graph/v1/paper/search?query=<query>&fields=title,authors,year,venue,abstract,citationCount,externalIds,openAccessPdf&limit=50`
  - Header (if key available): `x-api-key: $SEMANTIC_SCHOLAR_API_KEY`
- Paper details: `GET https://api.semanticscholar.org/graph/v1/paper/<paperId>?fields=title,authors,year,abstract,citationCount,references,citations`
  - Header (if key available): `x-api-key: $SEMANTIC_SCHOLAR_API_KEY`
- Optional filters (use only when appropriate, not by default): `year=2015-` (range), `minCitationCount=10`, `fieldsOfStudy=Political Science`, `publicationTypes=JournalArticle,Review`

Deduplicate across queries. Aim to collect at least 5–10x more candidates than the final list will contain.

---

## Step 3: Filter and Rank

**Filter** out results that:
- Are in excluded source types or languages
- Fall outside included date ranges (unless seminal)
- Focus primarily on excluded topics (even if included topics appear)
- Are clearly not substantively relevant to the research question

**Rank** remaining results into three tiers:
- **Highly Recommended**: Strong match on relevance to the research question, hits prioritization criteria (source type, recency, topic focus), and appears high quality
- **Recommended**: Solid relevance and quality, meets include criteria without hitting priority criteria
- **Optional**: Plausible relevance but lower confidence — tangential focus, older, lower venue quality, or unclear fit

For each result, write a brief rough note explaining what led to it (e.g., which query surfaced it, which included topic it addresses).

---

## Step 4: Human Review Presentation

Present results in three sections:

**Section 1 — Highly Recommended**: Strong fit, read these first.
**Section 2 — Recommended**: Solid fit, worth reviewing.
**Section 3 — Optional**: Lower confidence, human can skim or skip.

Each entry: title, authors, year, venue, link, and rough note. Human selects papers to download and add to the collection.

---

## Output Format

```
## Highly Recommended

1. **Title** — Author(s) (Year). *Venue*.
   Link: [URL or DOI link]
   Note: [what led to this result, e.g., "query: climate adaptation governance; directly addresses institutional design for resilience"]

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
