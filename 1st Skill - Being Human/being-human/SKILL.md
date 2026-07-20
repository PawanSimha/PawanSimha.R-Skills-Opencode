---
name: beinghuman
description: Write and rewrite text to sound naturally human by eliminating detectable AI writing patterns. Activates whenever generating, editing, rewriting, or polishing any text including emails, reports, README files, documentation, blog posts, articles, proposals, social media posts, comments, and prompts. Also activates when the user says "make this sound human" or "rewrite this to not sound like AI".
context: fork
---

# beinghuman — Anti-AI Writing Detection Skill

This skill systematically detects and removes patterns that make text identifiable as AI-generated. It does **not** dumb text down — it removes the statistical artifacts of language model output while preserving meaning, accuracy, and appropriate formality.

## Core Principles

1. **Preserve meaning.** Never change facts, numbers, quotes, code, or citations.
2. **Never invent.** Do not add facts, sources, or analysis not present in the original.
3. **Never reduce accuracy.** Domain terminology stays. Technical precision stays.
4. **Do not casualize.** Natural human writing is not the same as informal writing. Academic and professional tones are valid.

---

## Phase 1: Detection Scan

Before writing or rewriting, scan the **source text** (or the planned output) for every pattern below. Patterns are classified by priority based on how strongly the Wikipedia page "Signs of AI writing" presents them as indicators.

**Priority levels:**

| Level | Meaning | Action |
|-------|---------|--------|
| **CRITICAL** | Near-definitive indicator (direct LLM artifacts, strongest tells per the page) | Always fix when present |
| **HIGH** | Strong statistical signal (dedicated section with cited studies and real examples) | Fix in almost all cases |
| **MEDIUM** | Moderate signal (brief subsection, qualified language, also found in human writing) | Fix unless in tension with domain needs |
| **LOW** | Weak signal (single paragraph, model-specific, or not a diagnostic pattern) | Skip if fixing would harm readability, accuracy, or tone |

**Processing order:** Apply CRITICAL → HIGH → MEDIUM → LOW. If higher-priority fixes reduce the need for lower-priority ones (e.g., stripping significance overlay also removes -ing clauses), do not re-apply lower-priority rules to the same text. If a LOW priority rule would reduce technical accuracy, domain-appropriate formality, or natural readability, skip it entirely.

### Vocabulary — Remove These Clusters

Scan for co-occurring "AI vocabulary" words. These are statistically overrepresented in LLM output and co-occur: where one appears, others are likely nearby.

| Priority | Category | AI Words to Remove | Why |
|----------|----------|-------------------|-----|
| **HIGH** | **Legacy puffery** | *stands as, serves as, is a testament, is a reminder, marks a pivotal moment, underscores the importance, highlights the significance, reflects broader trends, setting the stage for, marks a shift, indelible mark, deeply rooted* | LLMs inflate mundane facts into grand significance |
| **HIGH** | **Generic significance** | *vital role, crucial role, pivotal role, key role, significant moment, key turning point, evolving landscape, broader context* | Applied universally, even to trivial subjects |
| **CRITICAL** | **AI vocabulary** | *delve, tapestry, multifaceted, nuanced, realm, landscape, foster, leveraging, robust, testament, pivotal, intricate, underscores, fostering, enhancing, comprehensive, vibrant, rich* | Statistically proven overuse post-2022 — "one of the strongest tells" |
| **HIGH** | **Marketing puffery** | *boasts a, nestled in, in the heart of, groundbreaking, world-renowned, diverse array, featuring, commitment to, natural beauty* | LLMs cannot maintain neutral tone |
| **HIGH** | **Notability boilerplate** | *independent coverage, local/regional/national media outlets, profiled in, maintains an active social media presence, written by a leading expert* | LLMs echo Wikipedia guidelines verbatim |

### Sentence Structure — Break These Templates

| Priority | Pattern | AI Signature | Fix |
|----------|---------|-------------|-----|
| **HIGH** | **Tailing -ing clause** | ", creating a lively community within its borders", "reflecting its continued relevance", "highlighting its importance" | Remove the -ing clause entirely or merge into the main sentence |
| **MEDIUM** | **Negative parallelism** | "Not only X, but Y", "It is not just X, it's Y", "X rather than Y" | Use a direct statement unless genuine contrast exists |
| **LOW** | **Rule of three** | Three parallel items when two or one would suffice | Reduce to the actual number needed |
| **LOW** | **Elegant variation** | Avoiding word repetition by swapping in synonyms | Repeat key terms; clarity trumps variety |
| **MEDIUM** | **Challenges template** | "Despite its [positive words], [subject] faces challenges including..." | Remove this framing; state facts directly |

### Content Patterns — Remove These Moves

| Priority | Pattern | AI Move | Replace With |
|----------|---------|---------|-------------|
| **HIGH** | **Significance overlay** | Attaching importance to trivial data (population, etymology, station specs) | Just the fact. No editorializing. |
| **HIGH** | **Broader context inflation** | Linking everything to a "broader movement", "wider debate", or "evolving landscape" | Nothing, unless genuinely and specifically sourced |
| **MEDIUM** | **Challenges + Future Prospects** | Cookie-cutter sections with formulaic optimism | If the section exists, rewrite without the template framing |
| **HIGH** | **Weasel attribution** | "Some scholars argue", "Many believe", "Experts suggest", "It is widely thought" | Either name a specific source or remove |
| **MEDIUM** | **Source count inflation** | Presenting 1–2 sources as representing "multiple" or "many" | Attribute accurately: name the actual sources |
| **HIGH** | **Notability hammering** | Listing media outlets by name in body text with type labels | Inline citation, no notability commentary in prose |

### Formatting — Normalize These

| Priority | Quirk | Fix |
|----------|-------|-----|
| **LOW** | **Title case in headings** | → Sentence case (unless proper noun) |
| **LOW** | **Overuse of boldface** | Bold only the article title in the lead |
| **LOW** | **Inline-header vertical lists** | → Prose or proper section headings |
| **LOW** | **Em dashes** (overuse) | → Commas, parentheses, or separate sentences |
| **LOW** | **Curly quotation marks** | → Straight quotes |
| **LOW** | **Emoji as formatting** | → Remove from non-casual text |
| **LOW** | **Horizontal rules before headings** | → Remove |
| **LOW** | **Tables for simple data** | → Prose unless table is genuinely needed |
| **LOW** | **Skipped heading levels** | → Proper nesting |
| **HIGH** | **Markdown in wikitext context** | → Native wikitext |
| **LOW** | **utm_source= parameters** | → Clean URLs |
| **CRITICAL** | **Placeholder text** {like this} | → Remove or fill |

---

## Phase 2: Rewrite

Apply rewrite rules in priority order. Rules sourced from HIGH-evidence patterns (Rules 3, 5) should be applied before MEDIUM-evidence rules (Rules 1, 2, 4). LOW-priority rules (Rules 6, 7) are protective — apply them last, and only if they don't reduce quality.

### Rule 1: Remove the Introduction

If the first sentence is any of these, delete it:
- "In today's rapidly evolving [topic] landscape..."
- "When it comes to [topic]..."
- "It is important to note that..."
- "Let's dive into..."
- "In this article/guide/post we will explore..."
- "Welcome to this [document type] about..."

### Rule 2: Remove the Conclusion

If the last paragraph is any of these, delete it:
- "In conclusion, ..." / "To summarize, ..."
- "Ultimately, [topic] serves as a reminder that..."
- "As we have seen, ..."
- "The [subject] stands as a testament to..."
- Generic calls to action ("Don't forget to...")

### Rule 3: Strip Significance Language

For every sentence, check: would this sentence still be true and complete if I removed the significance overlay?

Example:
- **Before:** "The population reached 56,998 in 2008, creating a lively community within its borders and further enhancing its significance as a dynamic hub of activity and culture."
- **After:** "The population was 56,998 in 2008."

### Rule 4: Simplify Verb Phrases

Replace verbose constructions with simpler ones:

| AI Verb Phrase | Human Alternative |
|----------------|-------------------|
| stands as / serves as | is |
| represents a | is a |
| contributes to | [omit or use specific verb] |
| plays a role in | [omit or specific] |
| sets the stage for | precedes / leads to (if true) |
| serves to | [omit] |
| is designed to | [omit or specific] |

### Rule 5: Eliminate Weasel Words

Remove: *arguably, purportedly, supposedly, reportedly, allegedly, some might say, it could be argued, it is believed, many consider, broadly regarded, widely seen as* — unless directly sourced.

### Rule 6: Break the Rhythm

Read the output aloud (silently). If three consecutive sentences have the same structure, rewrite at least one. Vary:
- Sentence length (short / long / medium)
- Sentence opening (subject / phrase / transition / question)
- Sentence type (simple / compound / complex)

### Rule 7: Keep Domain Terminology

Never replace:
- Medical terms with lay equivalents when writing for medical audiences
- Legal terms of art  
- Scientific nomenclature
- Technical jargon relevant to the field
- Mathematical notation

The goal is natural human writing at the appropriate register, not simplification.

---

## Phase 3: Internal Review Checklist

Before returning any rewritten text, silently verify every item. When conflicts arise (e.g., a LOW-priority fix would harm technical accuracy), skip the lower-priority rule. Fidelity to meaning and domain correctness always overrides pattern removal.

- [ ] Zero "AI vocabulary" words remain (delve, tapestry, pivotal, testament, etc.)
- [ ] Zero -ing tail clauses creating unsupported significance
- [ ] Zero notability boilerplate in body text
- [ ] Zero "Challenges" / "Future Prospects" template framing
- [ ] No more than one em dash per 3 paragraphs
- [ ] No title case in headings
- [ ] No boldface abuse
- [ ] No weasel words
- [ ] No placeholder text or knowledge-cutoff disclaimers
- [ ] No canned introductions or conclusions
- [ ] Each sentence has a different structure from its neighbors
- [ ] Key terms are repeated for clarity (not swapped for synonyms)
- [ ] Meaning is identical to source
- [ ] Technical accuracy is preserved
- [ ] No facts were added or changed
- [ ] Quotations, code, math, and citations are untouched
- [ ] Tone matches the original (unless user asked for tone change)
- [ ] Read naturally without being too informal

If any check fails, go back to Phase 2.

---

## Domain Exceptions

These fields have legitimate reasons for patterns that would otherwise be marked. Do not alter text in these contexts unless the pattern is gratuitous:

| Domain | Allowed Patterns | Still Remove |
|--------|-----------------|--------------|
| **Academic writing** | Formal register, abstract nouns, passive voice, significance framing (if source-backed) | Weasel words, puffery, AI vocabulary, repetitive structure |
| **Scientific writing** | Passive voice, nominalizations, complex terminology | AI vocabulary, empty significance overlaid on data |
| **Technical documentation** | Imperative tone, structured lists, bold for UI elements | Marketing language, unnecessary introductions, AI vocabulary |
| **Legal writing** | Archaic terms (whereof, herein), formal constructions, passive | Weasel words, canned templates, placeholder text |
| **Medical writing** | Clinical terminology, cautious hedging ("may indicate"), formal register | Puffery, AI vocabulary, unsupported significance |
| **Quotations** | Anything the quoted source says | Never alter quotations at all |
| **Code** | Any code | Never alter code |
| **Mathematical expressions** | Any math | Never alter math |
| **Citations** | Any citation format | Do not change citation content or formatting style |
| **Poetry / Creative writing** | Any stylistic choice | Only remove patterns that feel mechanical; preserve voice |

---

## Anti-Patterns (What NOT to Do)

| Trap | Why It Fails |
|------|-------------|
| Replacing big words with small words | Reduces precision; human experts use domain vocabulary |
| Making everything sound casual | Humans write formally in professional contexts |
| Adding personal anecdotes | Fictionalizes; violates the "never invent" rule |
| Over-correcting to extreme simplicity | Creates a different AI tell (LLMs optimized for grade-school reading level) |
| Removing all transitions | Creates choppy text; humans use transitions naturally |
| Adding contractions everywhere | "Don't", "can't", "won't" are fine, but not universal |
| Making text "witty" or "charming" | Feigned personality is another AI tell |
| Over-using sentence fragments | Stylistic fragments work in context; forced ones do not |

---

## Examples

### Example 1: Significance Overlay

**Before (AI):** "The Statistical Institute of Catalonia was officially established in 1989, marking a pivotal moment in the evolution of regional statistics in Spain. The founding of Idescat represented a significant shift toward regional statistical independence, enabling Catalonia to develop a statistical system tailored to its unique socio-economic context."

**After (Human):** "The Statistical Institute of Catalonia was established in 1989."

### Example 2: Puffery + -ing Clauses

**Before (AI):** "Nestled within the breathtaking region of Gonder in Ethiopia, Alamata Raya Kobo stands as a vibrant town with a rich cultural heritage, offering visitors a fascinating glimpse into the diverse tapestry of Ethiopia."

**After (Human):** "Alamata Raya Kobo is a town in the Amhara region of Ethiopia."

### Example 3: Tailing -ing Clause

**Before (AI):** "The station has broad gauge with 8 tracks and 6 platforms, serving as a major railway hub with historical significance and contributing to the socio-economic development of the region."

**After (Human):** "The station has broad gauge, 8 tracks, and 6 platforms."

### Example 4: Negative Parallelism

**Before (AI):** "The McAllen Texas Temple is not just a place of worship — it's a bridge across divides, embodying the spirit of unity that underlies its sacred purpose."

**After (Human):** "The McAllen Texas Temple was designed with Spanish colonial architectural elements."

### Example 5: Canned Introduction

**Before (AI):** "In today's rapidly evolving digital landscape, effective communication has become more important than ever. In this article, we will explore the key strategies that can help organizations navigate these changes and foster meaningful connections with their audiences."

**After (Human):** [Delete both sentences. Start with the first substantive point.]

### Example 6: Technical Documentation (Domain Exception)

**Before (AI):** "This REST API stands as a robust solution for managing user authentication, leveraging JWT tokens to ensure secure data transmission. It plays a pivotal role in modern application security."

**After (Human):** "This REST API manages user authentication using JWT tokens. It provides endpoint-based authentication for web and mobile applications."

(Note: "robust", "leveraging", "pivotal role" removed; technical description preserved; no casualization.)

### Example 7: Notability Hammering

**Before (AI):** "The subject has been profiled in multiple high-quality, independent, and widely-read outlets, including The Australian, SBS News, and 7News. These sources provide significant, substantial, secondary coverage, not trivial mentions."

**After (Human):** [Delete; just cite the sources inline.]
