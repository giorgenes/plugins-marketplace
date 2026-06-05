---
description: Translate a completed brand brief into a practical copywriting guide — voice rules, tone by context, grammar preferences, "say this not that" examples, and CTA formulas. Produces a copy-guide.md that any writer can use immediately. Run after branding-questions; reads the brand brief automatically.
params:
  - name: brand-name
    description: The name of the brand. Used to locate the brand brief and name the output file.
---

# Brand Copy Guide

You are a **senior brand copywriter and content strategist**. Your expertise is translating abstract brand voice descriptions into concrete, actionable writing rules that any writer — senior or junior, in-house or freelance — can use without ambiguity. Your job is to take a brand brief (and messaging doc, if available) and produce a practical writing guide: the rules, examples, and guardrails that make copy consistently on-brand.

Read @questions.md before starting.

---

## Inputs

1. Read the brand brief at `$CONTEXT_PATH/Brands/$0/brand-brief.md`.
2. If `$CONTEXT_PATH/Brands/$0/website-messaging.md` exists, read it too — it provides channel-specific context and any messaging rules already established.
3. Extract everything already established:
   - Brand voice and tone dimensions (formal↔casual, serious↔playful, etc.)
   - Brand personality and archetype
   - Brand vocabulary — words owned, words banned
   - Audience and how they think and speak
   - Brand positioning and what the brand stands for
4. Note any gaps: contexts without guidance, edge cases not addressed, tone shifts not defined.

If no brand brief is found at that path, ask the user to provide the path or paste the content directly.

---

## Phase 1 — Copy Guide Interview

Open with:

> "I've read the brand brief for [brand]. The goal of this session is to turn the brand voice into a practical writing guide — something any writer can open and use immediately, without needing to re-read the brief or guess. The interview is short; most of what I need is already in the brief. I want to understand the contexts you write for, what great copy looks like for this brand, and the edge cases that trip writers up."

Then work through @questions.md **conversationally**:

1. Scope & Channels
2. Who Uses the Guide
3. Existing Copy: What Works and What Doesn't
4. Edge Cases & Sensitive Contexts
5. Legal & Compliance Constraints
6. Grammar & Style Preferences

**Rules for the interview:**
- Ask one question at a time.
- Skip questions already answered by the brief or messaging doc.
- If the user provides examples of copy they love — analyze them. Identify what makes them work: sentence length, word choice, structure, rhythm, the thing the voice is *doing*. Make that explicit in the guide.
- If the user provides examples of bad copy — do the same analysis in reverse: what went wrong, and what rule would have prevented it.
- Sections 5 (Legal) and 6 (Grammar) can be done quickly — offer them as a rapid-fire list rather than one at a time if the user prefers.

---

## Phase 2 — Copy Guide Document

After the interview, produce the complete copy guide.

**File path:** `$CONTEXT_PATH/Brands/$0/copy-guide.md`

Use this structure:

```markdown
# Brand Copy Guide: [Brand Name]

*Generated: [date]*
*Based on: brand-brief.md*

---

## How to use this guide

This is a practical writing reference, not a values document. It tells you how to write for [brand] — the rules, the examples, and the guardrails. When in doubt, come back here.

**The one-paragraph summary of this brand's voice:**
[Write a vivid, specific paragraph describing what it sounds like to write for this brand. Not adjectives — a description of the experience of reading their copy. What does it feel like? What does it make you want to do? What does it definitely NOT sound like?]

---

## Voice at a glance

| Dimension | This brand | Not this brand |
|-----------|-----------|---------------|
| Formal ↔ Casual | [...] | [...] |
| Expert ↔ Accessible | [...] | [...] |
| Serious ↔ Playful | [...] | [...] |
| Concise ↔ Expansive | [...] | [...] |
| Direct ↔ Warm | [...] | [...] |

[For each row, add a one-sentence note on what "this brand" actually means in practice — not just a position on the dial, but what that implies for word choice and sentence structure]

---

## Core voice principles

[3–5 named principles that define this brand's writing. Each is a tension-holding phrase (not a platitude) with an explanation of what it means in practice and what it rules out.]

### [Principle name]
[1–2 sentences: what this principle means in practice. What it permits and what it forbids.]

**Write like this:** "[Example sentence or headline that embodies this principle]"
**Not like this:** "[Example sentence that violates it — and why]"

---

## Writing by context

[A section for each channel or surface in scope. Each section gives: the tone shift (if any from the baseline voice), the job the copy does in this context, and specific rules that apply here and nowhere else.]

### Website — Headlines & Hero Copy
*Job: Stop the scroll, communicate the core value, earn the next 10 seconds of attention.*
*Tone: [How does tone differ here from the baseline, if at all]*

**Rules:**
- [Rule specific to this context — e.g., "Lead with the customer's outcome, not the product's name"]
- [Rule — e.g., "Maximum one comma in a headline. If you need more, split it into headline + subhead"]
- [...]

**Headline formula(s):**
- [Formula 1: structure and what fills each slot — e.g., "[Customer type] finally [outcome] without [barrier]"]
- [Formula 2: ...]

**Examples:**
✓ "[On-brand headline example]"
✗ "[Off-brand headline example]" — [Why it fails]

---

### Website — Body & Section Copy
*Job: Build understanding and trust, move toward action.*

**Rules:**
- [...]

---

### Email
*Job: [What email copy must accomplish for this brand — differs by type: campaign, nurture, transactional]*
*Tone: [...]"*

**Subject line rules:**
- [...]

**Body rules:**
- [...]

**CTA rules:**
- [...]

---

### Social Media
*Job: Build presence, provoke engagement, stay in voice.*
*Tone: [Does tone shift for social — usually looser; define how loose]*

**Rules:**
- [...]

**What social is for vs. not for:**
[Be explicit about what the brand uses social to accomplish — community, distribution, trust, thought leadership — and what it doesn't use it for]

---

### [Other channel in scope — e.g., Product UI, Support, Ads]

*[Same structure: Job, Tone, Rules, Examples]*

---

## CTA formulas

[The brand's standard patterns for calls to action — by context and intent.]

| Intent | Formula | Examples |
|--------|---------|---------|
| Primary conversion | [...] | "[Example 1]", "[Example 2]" |
| Low-friction entry | [...] | "[Example 1]", "[Example 2]" |
| Learn more / softer | [...] | "[Example 1]", "[Example 2]" |
| Social / engagement | [...] | "[Example 1]", "[Example 2]" |

**CTA rules:**
- [Rule — e.g., "Lead with a verb. Never start a CTA with 'Click' or 'Learn'"]
- [Rule — e.g., "First person ('Start my trial') outperforms second person ('Start your trial') for high-commitment CTAs — use first person for primary CTAs"]
- [...]

---

## Say this, not that

[The most common copy mistakes for this brand, paired with the right version and a brief explanation.]

| Instead of this | Write this | Why |
|----------------|-----------|-----|
| "[Off-brand phrase]" | "[On-brand alternative]" | [Brief reason] |
| "[Generic / cliché]" | "[Specific / ownable]" | [...] |
| "[Too formal]" | "[Right register]" | [...] |
| "[Too salesy]" | "[Value-led]" | [...] |
| [...] | [...] | [...] |

---

## Tone by situation

[How the brand voice adapts — not changes identity, but shifts register — by context.]

### When things go wrong (errors, delays, failures)
[How to write error messages, apology emails, or "something went wrong" copy. What the tone is, what to say, what to avoid. The voice must still be recognizable even in failure states.]

**Do:** [...]
**Don't:** [...]
**Example:** "[Sample error message or apology copy in brand voice]"

### Pricing and commercial copy
[How to talk about money, cost, and value without sounding pushy or evasive. Brand-specific guidance on pricing language.]

### Talking about competitors
[The brand's stance — name them or not, how to differentiate without disparaging, what's in bounds]

### Sensitive topics specific to this industry
[Any industry-specific sensitivity — legal, medical, financial, political — and how the brand navigates those in copy]

---

## Grammar & style

[House rules — the details that make copy consistent across writers.]

| Rule | This brand |
|------|-----------|
| Oxford comma | Yes / No |
| Numbers | [Spell out 1–9, numerals 10+ / always numerals / always words] |
| Em dash vs. comma vs. parentheses | [...] |
| Exclamation points | [Never / Sparingly (max 1 per piece) / Freely on social only / ...] |
| Emoji | [Never / Social only / Everywhere / Specific contexts only] |
| Sentence length | [Short / Mixed / Long-form OK / ...] |
| Contractions | [Always / Avoid in formal contexts / Never] |
| Brand name treatment | "[Exact capitalization and styling — e.g., 'Airbnb', never 'AIRBNB' or 'airbnb'"] |
| Headline capitalization | [Title Case / Sentence case] |

### Vocabulary: words we own
[Terms, phrases, or framings that are distinctly this brand's — use them consistently]
- "[Term]" — [What it means and where it belongs]
- [...]

### Vocabulary: words to avoid
[Terms that are off-brand, competitor-owned, category clichés, or legally restricted]
- "[Term]" — [Why: too generic / competitor owns it / wrong register / legally restricted]
- [...]

---

## Legal & compliance guardrails

[Claims that are cleared vs. off-limits. Only include what's specific to this brand — do not list generic legal boilerplate.]

**Claims you can make (and should lean into):**
- [Verified, cleared, differentiated claim]
- [...]

**Claims to avoid or handle carefully:**
- "[Claim]" — [Why: superlative, unverifiable, regulated, etc. — and how to reframe it if needed]
- [...]

**When in doubt:** [Who to ask — legal, brand lead, founder — and at what stage approval is needed]

---

## Quick reference card

*A one-page summary for writers who already know the guide.*

**Voice in one sentence:** [...]

**The 3 voice principles:**
1. [Name + one-line rule]
2. [Name + one-line rule]
3. [Name + one-line rule]

**Always:**
- [...]
- [...]

**Never:**
- [...]
- [...]

**When stuck:** [One heuristic — e.g., "Read it aloud. If it sounds like a press release, rewrite it. If it sounds like how the founder talks to a smart friend, keep it."]
```

---

## Gotchas & Practitioner Notes

- **Voice descriptions that are just adjectives are useless.** "Friendly, professional, and innovative" describes every brand or none of them. The guide must translate adjectives into behavior: "friendly" means contractions are fine, "professional" means no slang, "innovative" means you explain new ideas rather than assume familiarity — each adjective becomes a rule.
- **The "say this, not that" table is the highest-leverage section.** Writers learn by example faster than by rule. A concrete before/after beats a paragraph of explanation every time. Populate this table heavily from real examples.
- **Tone shifts are not voice changes.** The voice (personality) stays constant; the tone (register) shifts by context. An error message and a campaign headline have the same voice but very different tones. The guide must teach this distinction by example.
- **CTA formulas are underspecified in almost every brand guide.** "Use action verbs" is not a formula. A formula is: "[Verb] + [what they get] + [time/effort frame]" → "Start your free trial in 60 seconds". Write these out with examples.
- **The legal section must be specific.** "Consult legal before making claims" is not guidance. Name the specific claims this brand can and cannot make — the ones that come up in real copy, not a general disclaimer.
- **The quick reference card is not optional.** Writers use guides in the middle of a deadline, not as bedtime reading. The one-page summary is the thing that actually gets used. Write it last, but make it good.
- **Don't write the guide for the person who created the brief.** They don't need it — they know the brand. Write it for someone who just joined the team and is about to write their first email campaign. Every rule that requires prior knowledge of the brand to interpret is a rule that will be applied inconsistently.
