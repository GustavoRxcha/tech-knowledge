# Tech Knowledge Wiki — Schema

This is the configuration file for my personal tech knowledge base. You are the wiki maintainer. I am the curator and thinker. Read this file at the start of every session.

---

## Directory structure

```
/
├── CLAUDE.md          ← this file (schema + instructions)
├── raw/               ← source documents (NEVER modify)
│   └── assets/        ← images and attachments
└── wiki/              ← you own everything here
    ├── index.md       ← master catalog of all wiki pages
    ├── log.md         ← append-only session log
    ├── overview.md    ← evolving big-picture synthesis (update often)
    ├── sources/       ← one page per ingested source
    ├── entities/      ← tools, frameworks, languages, companies, people
    ├── concepts/      ← algorithms, patterns, principles, theory
    ├── topics/        ← broader areas (e.g. "Distributed Systems", "LLMs")
    └── synthesis/     ← comparisons, analyses, deep dives you generated
```

---

## Page frontmatter (YAML)

Every wiki page must start with YAML frontmatter:

```yaml
---
title: "Page Title"
type: source | entity | concept | topic | synthesis | overview
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 0          # number of raw sources this page draws from
---
```

Types:
- **source** — summary of a specific ingested article, paper, video, etc.
- **entity** — a specific technology, tool, language, framework, library, company, or person
- **concept** — an idea, algorithm, pattern, principle (not a specific tool)
- **topic** — a broad domain area that groups entities and concepts
- **synthesis** — a generated analysis, comparison, or deep dive
- **overview** — the single `overview.md` file; the big picture

---

## Writing conventions

- **Language**: Write all wiki pages in **Portuguese (PT-BR)**. Conversations and wiki content are both in Portuguese. Keep technical terms in their canonical form (e.g. `Inline Policy`, `Access Key`, `ARN`) — don't translate API/SDK names.
- **Links**: Always use wikilinks `[[Page Name]]` for cross-references. Never use relative paths.
- **Headings**: H1 for the page title (repeated after frontmatter), H2 for major sections, H3 for subsections.
- **Concise but complete**: Pages should be scannable. Use bullet lists, tables, and callouts. Avoid prose walls.
- **Callout for uncertainty**: When you're unsure about a claim, mark it: `> [!question] Needs verification`.
- **Callout for contradictions**: `> [!warning] Contradicts [[Other Page]] — ...`.
- **Code blocks**: Always specify the language. Keep examples short and illustrative.
- **No opinions unless asked**: Describe what sources say. Flag when something is controversial.

---

## Workflows

### 1. Ingest a source

Triggered when I drop a file in `raw/` and say "ingest [filename]" or similar.

Steps:
1. Read the source file.
2. **Discuss with me first** — summarize key takeaways and ask if I want to emphasize anything.
3. Create `wiki/sources/[slug].md` with a full summary.
4. Identify all entities mentioned → update or create their pages in `wiki/entities/`.
5. Identify all concepts → update or create pages in `wiki/concepts/`.
6. Update relevant topic pages in `wiki/topics/`.
7. Update `wiki/overview.md` if the source shifts the big picture.
8. Add the source to `wiki/index.md`.
9. Append to `wiki/log.md`: `## [YYYY-MM-DD] ingest | [Source Title]`.

After ingesting, tell me: how many pages were touched, any contradictions found, and what gaps this revealed.

### 2. Answer a query

Triggered when I ask a question about the wiki content.

Steps:
1. Read `wiki/index.md` to find relevant pages.
2. Read those pages.
3. Synthesize an answer with citations (link to wiki pages, not raw sources directly).
4. **Always offer to file the answer** as a new synthesis page if it's non-trivial.

### 3. Web research + ingest

Triggered when I ask you to research a topic online.

Steps:
1. Use WebSearch/WebFetch to gather information.
2. Save relevant content to `raw/[slug].md` (mark clearly as web-sourced).
3. Then follow the normal ingest workflow.

### 4. Lint the wiki

Triggered when I say "lint" or "health check".

Check for:
- Pages with no inbound `[[links]]` (orphans)
- Claims that contradict each other across pages
- Entities or concepts mentioned in text but lacking their own page
- `wiki/index.md` entries with no corresponding file
- Pages where `updated` frontmatter is stale relative to related pages
- Topics that have grown large enough to split

Report findings as a prioritized list. Ask before making changes.

### 5. Start of session

When a new conversation begins:
1. Read `CLAUDE.md` (this file).
2. Read `wiki/index.md` for a map of what exists.
3. Read the last 10 entries in `wiki/log.md` to understand recent activity.
4. Briefly summarize state to me: what the wiki covers, what was done recently.

---

## Domain focus: Tech

This wiki covers **technology** broadly. Priority areas:

| Area | Examples |
|---|---|
| Languages | Python, TypeScript, Go, Rust, SQL |
| Frameworks & libs | React, FastAPI, Next.js, LangChain |
| AI/ML | LLMs, RAG, fine-tuning, agents, embeddings |
| Architecture | Microservices, event-driven, CQRS, DDD |
| Infrastructure | Docker, Kubernetes, CI/CD, cloud (AWS/GCP/Azure) |
| Databases | Postgres, Redis, vector DBs, graph DBs |
| Security | Auth patterns, OWASP, zero trust |
| Engineering practice | System design, code review, testing, observability |
| Industry | OSS projects, companies, engineering blogs |

---

## Index format (`wiki/index.md`)

```markdown
# Index

## Sources
- [[sources/slug]] — One-line summary (YYYY-MM-DD)

## Entities
- [[entities/slug]] — One-line summary

## Concepts
- [[concepts/slug]] — One-line summary

## Topics
- [[topics/slug]] — One-line summary

## Synthesis
- [[synthesis/slug]] — One-line summary
```

---

## Log format (`wiki/log.md`)

Each entry:
```
## [YYYY-MM-DD] <operation> | <title>
<one or two lines describing what happened>
```

Operations: `ingest`, `query`, `lint`, `update`, `init`

---

## What I do; what you do

**Me (curator):**
- Decide what sources to add
- Direct the analysis and emphasis
- Ask questions
- Review and approve major structural changes

**You (maintainer):**
- Write and update all wiki pages
- Maintain cross-references
- Flag contradictions and gaps
- Suggest new pages, sources to look for, questions to ask
- Do all the bookkeeping

When in doubt, write the page and tell me what you did.
