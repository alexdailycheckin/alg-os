# Data Ingestion - Phases 2 and 3

How the intake handles file uploads (Phase 2) and online research (Phase 3). Both run BEFORE interactive intake (Phase 4) so the sparring layer has a populated state to interrogate.

The sparring rules in `/00-intake/sparring-rules.md` apply to inferred content from these phases. Origin does not matter.

## Phase 2 - File ingestion

### Accepted formats

| Format | Handling |
|---|---|
| `.pdf` | Parse text. For scanned PDFs, OCR if available, otherwise flag the file as image-only and ask the operator to summarise verbally. |
| `.docx` | Parse text and structure (headings, lists, tables). |
| `.pptx` | Parse slide titles and body text. Note speaker notes if present. |
| `.md`, `.txt` | Read as-is. |
| `.csv` | Read columns and first 50 rows. If the file is a structured list (customer lists, deal lists), parse fields. If the file is a raw export with hundreds of columns, flag for cleanup before ingestion. |
| `.xlsx` | Same as `.csv` for simple sheets. Flag complex multi-sheet workbooks for cleanup. |
| Image files | Ask the operator to describe the content. Do not attempt OCR on screenshots of slides. |

Anything else: tell the operator the format is not supported. Suggest converting to PDF or pasting the content directly into chat.

### What to extract per file type

**Brand and positioning docs.** Mission, one-liner, positioning statement, banned words, voice rules.

**Sales decks.** ICP description, persona slides, pricing slides, case studies, competitive slides.

**Customer lists.** Vertical mix, revenue band distribution, geography mix.

**Existing strategy or GTM docs.** Stated motion, channels, current artefacts, current positioning.

**Brand guidelines.** Voice, banned words, English variant, tone rules.

**Transcripts.** Real customer language, real objections, real triggers. High-signal source for ICP and persona work.

### Reflection pattern

After parsing all uploads, reflect back to the operator in a structured summary:

> "From the files you uploaded I have inferred:
> - ICP: [summary]
> - Personas: [summary]
> - Positioning: [summary]
> - Services: [summary]
> - Voice / banned words: [summary]
>
> Tell me what is wrong before we move on."

Do not write to `/workspace/foundation/` yet. Working memory only. The operator confirms or corrects, then we proceed.

### Sparring still applies

If the file says "we target mid-market companies," that fails the ICP bar even though it is in a brand doc. Flag it during reflection:

> "Your brand doc describes the ICP as 'mid-market companies.' That is a TAM, not an ICP. We will refine in Phase 4. For now I am noting it as a known weakness."

## Phase 3 - Online research

### Sources to scrape by default

| Source | What to extract |
|---|---|
| Operator's website | Stated positioning, services, ICP language, case studies, team page, pricing page if public. |
| Operator's LinkedIn company page | Headline, company description, employee count, recent posts (last 30 days). |
| Operator's recent press / news | Mentions in industry press, awards, funding announcements, customer wins. |
| Public reviews (G2, Trustpilot, Glassdoor for service companies) | Customer language, recurring themes, named pain points. |
| Competitor sites (named in interactive intake or inferred) | Their stated positioning, services, ICP. Used in Section E sparring. |

### Sources to scrape on request

If the operator points at specific URLs (industry reports, partner sites, niche forums), fetch and parse those too.

### Tools

Use `web_fetch` for known URLs. Use `web_search` for queries the operator suggests (e.g., "what does our category currently look like").

### Reflection pattern

After research completes, reflect back:

> "From your website, LinkedIn, and [other sources] I have inferred:
> - Positioning as stated publicly: [summary]
> - Most recent customer wins: [summary]
> - Public review themes: [summary]
> - Discrepancies vs your file uploads: [list any]
>
> Tell me what is inaccurate or out of date before we move on."

### Discrepancies

If file uploads and online research disagree (sales deck says one ICP, website says another), surface the discrepancy explicitly. Do not silently pick a winner. The operator decides which is current. Note the resolution.

## Phase 2 to 3 to 4 transition

When uploads and research are reflected and confirmed, working memory should hold a tentative version of every foundation file. Tentative meaning: enough signal to guess, not enough to write.

Phase 4 (interactive) starts by reading the working memory and asking targeted questions to:

1. Fill gaps where Phases 2 and 3 produced nothing.
2. Pressure-test inferred content where the answer looks weak.
3. Resolve contradictions surfaced in reflection.

The operator does not re-answer questions Phases 2 and 3 already covered. They confirm, correct, and fill gaps. This is what makes intake feel respectful of their time even when it takes its time on the bar.

## What if the operator has nothing

If the operator uploads no files and points at no URLs, skip Phases 2 and 3. Tell them:

> "No uploads, no public sources. Phase 4 (interactive) will carry the full load. This will take longer but the framework still works."

Do not pressure them to find files for the sake of process. The bar is what matters, not the workflow shape.
