# Positioning Audit: Master Prompt

> Paste this entire file into Claude Code from a folder containing a `.env` (your API keys, optional for this playbook) and a `CLAUDE.md` (business brief). If `CLAUDE.md` is absent or has placeholders, Claude interviews you conversationally and fills it in for you. Either way Claude runs the audit end-to-end, produces a single consolidated report in markdown and Word formats, and saves supporting data alongside.
>
> Built by Nishant Kapoor at EntireCommerce AI. Version 1, April 2026.

---

You are executing the Positioning Audit playbook for the brand in the current working directory. Follow these steps in order. Do not skip steps. Do not invent data. Honour the voice conventions in Step 7.

---

## Step 1. Load or populate the business brief

Look for `CLAUDE.md` in the current working directory.

**If `CLAUDE.md` exists and the positioning-relevant fields are populated** (no `{placeholder}` text, the six minimum fields filled), read it and proceed to Step 2.

**If `CLAUDE.md` is missing, has placeholders, or lacks required fields**, run the business-brief interview before proceeding. Do not skip. Do not guess.

### The business-brief interview

Ask the user the following questions conversationally, one batch at a time. After each batch, write the answers into `CLAUDE.md` in the current working directory (create the file if missing) and confirm with the user before moving to the next batch.

**Batch 1: Brand overview.** Brand name. Primary URL. Ecommerce platform (Shopify, WooCommerce, custom). Geographic focus. Stage (pre-launch, first year, established, mature).

**Batch 2: Product and ICP.** Product category in one sentence. ICP in the founder's own words, in 1-2 lines (write it in the voice the founder uses at dinner; skip the website voice for this field).

**Batch 3: Current positioning.** Current positioning statement verbatim, or "None yet". Three to five competitors with URLs (load-bearing for Section 4). Twelve-month revenue goal.

**Batch 4: Positioning raw material.** The key objection the brand hears most often. What the founder wishes the ICP would say about the brand (the phrases the founder would want to see in a five-star review written in the founder's exact language).

**Batch 5: Optional context.** Price range or AOV. Catalog size. Distinctive or patented elements. Secondary audience if material. Where the ICP hangs out online (useful for Section 3 mining).

### Minimum required to proceed to Step 2

1. Brand name
2. Primary URL
3. Product category (one sentence)
4. ICP in founder's own words (1-2 lines)
5. Three to five competitor URLs
6. Twelve-month revenue goal

Optional fields can be marked "unknown" in `CLAUDE.md`. Claude flags any gaps in the final report.

Do not invent any value. Ask the user.

---

## Step 2. Inventory tool access

Read the `.env` file (if present) in the current working directory. Print a credential inventory:

```
External tools (all that the positioning audit uses)
- Serper: configured / not configured
- WebFetch: always available
- Public audience research (Reddit, X, Quora, YouTube, forums): always available
- Meta Ad Library: always available (with JS-render fallback chain if needed)
- Claude / ChatGPT / Perplexity (LLM positioning probes): always available
```

The positioning audit runs entirely on External tools. No client logins required. If Serper is missing, Section 4 SERP snippet capture runs without it and notes the limitation.

After printing, if Serper is missing, ask:

> "Serper is not configured. Want me to look up the current sign-up steps, so we can add a Serper SERP snippet layer to Section 4? Answer `yes`, `no`, or `skip`."

If `yes`, use WebSearch and WebFetch to pull the current sign-up flow for Serper (pricing, free tier, where the API key lives, the `.env` variable name `SERPER_API_KEY`). Produce step-by-step instructions the user can follow in about 5 minutes.

If `no` or `skip`, proceed without Serper. Note the absence in Section 4 of the final report.

Never hardcode sign-up URLs or pricing from memory. Pull fresh from the web every time.

---

## Step 3. Detect the path and confirm the mode

**Path A** if the brand has a live site with at least three public surfaces (homepage, one product page, one About/story page). WebFetch the primary URL to verify.

**Path B** if pre-launch or fewer than three public surfaces exist.

State the detected path and ask the user to confirm. Then ask which mode applies:

| Mode | When it applies | Duration |
|---|---|---|
| Full | Path A, default | 30 minutes |
| Quick | Time-boxed, Path A or B | 15 minutes |
| Competitor-deep | Single-competitor teardown with response positioning | 45 minutes |
| Pre-launch | Path B, skips Section 2 | 25 minutes |

Record path and mode in the report header.

---

## Step 4. Draft the eight sections

Produce all eight sections of the report in drafting mode. Do not write to disk yet.

### Section 1. Founder vision capture

Interview-driven. Capture seven fields:

1. Twelve-month revenue goal (from CLAUDE.md if already there)
2. Target customer in founder's own words (pull from CLAUDE.md ICP field, expand if thin)
3. Positioning hypothesis (why does this brand win? what do you do that nobody else does?)
4. Product origin story (what was the triggering pain or insight?)
5. Known constraints (capital, team, time, supply chain, regulatory)
6. Biggest-lever belief (if you could only move one thing to unlock growth, what would it be?)
7. What the founder wishes the ICP would say (from CLAUDE.md, expand with verbatim phrases if the founder is present)

Transcribe verbatim where the founder's phrasing is distinctive. Capture emotional register, metaphors, and the phrases the founder reaches for when describing the brand to a sceptic. Those phrases become positioning material in Section 6.

Save founder quotes to `data/positioning-audit/{YYYY-MM-DD}/founder-vision.md`.

### Section 2. Current-state messaging audit (Path A only)

On Path B, compress to one paragraph: "Pre-launch, no current-state surfaces to audit" and proceed to Section 3.

On Path A, catalogue every explicit positioning claim across these surfaces:

| Surface | What to capture |
|---|---|
| Homepage | H1, subhead, hero subcopy, primary CTA, above-the-fold claims |
| Highest-revenue product page | H1, subhead, first three body paragraphs, objection-handling copy |
| About page | Founder-voice claims, origin-story copy, team positioning |
| Paid-ad primary text | 5-10 active ads via Meta Ad Library. Verbatim primary text |
| Social bio | Instagram, X, LinkedIn company page taglines |
| Email welcome | If public on a thank-you page post-signup, or previously captured |

For each surface, produce a two-column table (Surface, Claim). One row per claim. Verbatim.

Categorise each claim: Feature (what it is), Benefit (what it does for the buyer), Identity (who the buyer becomes), Category (what kind of thing this is), Social proof (numbers, press, reviews).

Count frequency by category. Flag imbalances (a brand over-indexed on Feature claims and under-indexed on Identity claims has a positioning gap).

Pull the 10 to 15 most-used phrases across all surfaces. Those are the brand's current lexicon.

Save full capture to `data/positioning-audit/{YYYY-MM-DD}/current-state-capture.md`.

### Section 3. Audience insights

Run the canonical audience master prompt. Located at:
`/Users/nishantkapoor/Library/CloudStorage/Dropbox/Claude-Projects/EntireCommerce/playbooks/audience-insights-master-prompt.md`

Read the file. Feed it the three required inputs from Section 1 and the CLAUDE.md brief:

1. Target audience (one line, founder's own words)
2. Their #1 struggle (one line)
3. What the brand sells and how it helps (one line)

Deliverable per the master prompt: a one-page brief with nine sub-headings (Avatar, Core tension, What they tried and why it broke, Market gap, Recurring language, Three headlines, Top three objections and responses, Positioning angle, Belief shift). Plus a 15-quote verbatim appendix.

Save the 15-quote appendix to `data/positioning-audit/{YYYY-MM-DD}/audience-voc-mining.md`.

Do not rewrite the master prompt inline. Reference it by path. Edits to the master propagate to every audit that references it.

### Section 4. Competitor positioning scan

For each of the 3 to 5 competitor URLs, produce seven sub-sections:

**4.1 Homepage hero.** H1, subhead, hero subcopy. Verbatim via WebFetch.

**4.2 Elevator pitch.** The one-sentence self-description the brand uses on its homepage or About page.

**4.3 Primary promise.** The core benefit the brand leads with. One of: faster, cheaper, easier, more premium, more effective, more ethical, more specialised.

**4.4 Secondary claims.** Three to five supporting claims from the homepage. Verbatim.

**4.5 Tone of voice.** Three adjectives. Source: homepage and About page copy.

**4.6 Visual identity flavour.** One sentence. Minimal, dense, photography-heavy, illustration-forward, retro, high-contrast.

**4.7 Ad-library angles.** 30-day Meta Ad Library snapshot. Top 3 angles in rotation. One sentence each.

**WebFetch tool note.** Meta Ad Library is JS-rendered and WebFetch often returns empty. Fallback chain: Playwright headless-browser script if available, third-party Meta Ad Library indexes (adscan.ai), manual browser screenshots. If none available, note "Meta Ad Library: unable to verify for {competitor}; manual screenshot pass required" and file as an appendix gap.

After the per-competitor teardowns, produce a cross-competitor positioning map. 2x2 grid on the two dominant axes the category plays on. Pick axes that force competitors to sort into distinct quadrants. Examples:

- Jewellery: Craft-heritage vs Modern-everyday (y-axis) x Price-accessible vs Luxury-exclusive (x-axis).
- Short-game training: Data-driven vs Feel-based (y-axis) x Solo-practice vs Coach-led (x-axis).
- Luxury resale: Transparency-first vs Opacity-traditional (y-axis) x Breadth-of-stock vs Curated-rarity (x-axis).

If three competitors land in the same quadrant, flag as commodity territory. If one or two quadrants sit empty, flag as potential whitespace.

Produce one paragraph of "what every competitor claims" (commodity territory). One paragraph of "what no competitor claims" (potential whitespace).

Save the per-competitor capture to `data/positioning-audit/{YYYY-MM-DD}/competitor-positioning-scan.md`.

### Section 5. Overlap, whitespace, misalignment synthesis

The intersection section. Load-bearing. Compares Section 1, Section 3, and Section 4.

**5.1 Overlap: founder vision matches ICP language.** Phrases the founder uses (Section 1) that also appear in the Recurring Language block of Section 3. For each overlap phrase, state: "Founder says X. ICP says X. Current site says [Y / also X / not at all]." If the current site says neither, that is the fastest positioning win available.

**5.2 Commodity territory: current claims overlap with all competitors.** Claims from Section 2 (current-state) that also appear in Section 4 (competitor claims). Flag every claim in the brand's top-10 phrases that also appears in at least two competitors' top claims. These claims carry zero positioning weight and should be rewritten or replaced.

**5.3 Whitespace: ICP asks for X that no competitor delivers.** Recurring Language phrases from Section 3 that do not appear in any competitor's homepage, ad copy, or positioning claims from Section 4. Rank whitespace opportunities by: frequency in the 15-quote appendix, alignment with Section 1 founder vision, commercial viability for the 12-month revenue goal.

**5.4 Misalignment: founder vision drifts from ICP language.** Phrases the founder uses in Section 1 that the ICP in Section 3 does not use. For each drift, offer two options to the founder: swap the founder's phrase for the ICP phrase, or build a campaign that teaches the ICP the founder's phrase.

Produce a consolidated intersection map at the end: Overlap in the centre, Commodity territory in the bottom-left quadrant, Whitespace in the top-right quadrant, Misalignment as a red-flag list. This map appears at the top of the executive summary.

### Section 6. Three positioning options

Produce three positioning options. Each option has an eight-element messaging system. Each option represents a different risk-reward profile.

**Option A. Safe.** Iterates on current positioning. Sharpens the headline. Cleans up commodity claims from 5.2. Doubles down on overlap region from 5.1. Low risk, low ceiling. Fit: brands compounding current performance without a rebrand.

**Option B. Bold.** Leans into the strongest whitespace opportunity from 5.3. Category frame shifts. Primary promise shifts. Medium risk, medium-high ceiling. Fit: brands that need meaningful re-acceleration.

**Option C. Bet-the-brand.** Reshapes the brand around a category-creating claim. Category frame is new. Primary promise is something no competitor makes. High risk, high ceiling. Fit: brands with founder appetite for category education, or brands facing existential positioning problems.

For each option, produce all eight elements:

1. **Category frame.** One sentence. What category does the brand belong to?
2. **Positioning statement.** "For [ICP] who [struggle], [brand] is the [category] that [primary promise], because [reason to believe]." Internal-facing.
3. **Headline + subhead.** ≤12 words headline, ≤20 words subhead. Uses phrases from Section 3 Recurring Language.
4. **Five primary promises.** Five core benefit claims, one sentence each. Each traceable to an ICP quote or founder-vision phrase.
5. **Three objection-handling lines.** The three most-heard objections paired with one-sentence responses.
6. **Tone of voice brief.** Three adjectives, three words the brand uses, three words the brand avoids.
7. **Three example ad headlines.** Concrete Meta or Google headlines in the option's voice.
8. **Example social bio.** 150-character Instagram / X / LinkedIn bio in the option's voice.

No option produced from thin air. Every element traces to Section 1, Section 3, or Section 5 evidence.

### Section 7. Recommendation with reasoning

Pick one of the three options. Defend the pick.

Structure:

- **The recommendation.** Option A, B, or C. One sentence.
- **Why this one.** Three bullets. Each bullet links back to specific evidence from Sections 3, 4, or 5. Cite quote counts, competitor claim counts, founder phrases.
- **Risks of each option.** One paragraph per option.
  - Safe: ceiling too low for the 12-month goal.
  - Bold: 3 to 6 months of traffic turbulence while the brand teaches the new frame.
  - Bet-the-brand: 12 months of founder evangelism before paid acquisition becomes reliable.
- **Proof the founder needs before committing.** A concrete test. Example: "Two-week Meta Ads test with the recommended option's headline against the current-state headline. Pass criterion: recommended CTR within 70% of control or better."

### Section 8. Messaging rollout plan

Sequence of touchpoints to update. Default order:

1. Homepage hero first (highest leverage, one-week build, 48-hour measurement window).
2. Meta and Google ads second (30% of budget to new variants for two weeks, compare CTR, CPA, ROAS).
3. Social bios and primary pinned posts (cheap, immediate, compounding).
4. Email welcome series (subject lines and H1s in emails 1 through 3 of the flow).
5. Product pages last (most expensive surface, highest conversion sensitivity).

Tests to run before full rollout:

- Two-week ad test vs control. Pass: CTR within 70% of control or better.
- Two-week homepage A/B test if a CRO tool is available. Pass: PDP add-to-cart rate holds or improves.
- Two-day qualitative comprehension check with 5 ICP prospects. Pass: at least 3 of 5 correctly describe the intended ICP when shown only the headline.

KPI table:

- Leading indicators (first 14 days): homepage bounce, ad CTR, email open rate on welcome, time on homepage.
- Mid indicators (30-60 days): add-to-cart rate, welcome-flow revenue per send, branded-search volume.
- Lagging indicators (90 days): revenue growth rate, CAC, organic traffic on branded queries.

---

## Step 5. Synthesis pass (mandatory before writing to disk)

Do not write yet. Assemble the complete draft of all eight sections as a single document in your working context. Read it end-to-end in one pass. Ask:

- What cross-cutting tension surfaces in three or more sections that no section captures on its own?
- What is the single positioning move that would collapse the most ambiguity in the brand?
- Is any ICE-ranked action solving only one surface? Consider demoting in favour of moves that touch multiple surfaces.

Produce 3 to 5 cross-cutting tension bullets. Each bullet states the tension in one sentence and names the sections it spans in brackets.

Revise:

- **Executive Summary** (3-4 sentences) to lead with the positioning call the intersection reveals.
- **The three positioning options** to cross-reference synthesis tensions where relevant.
- **ICE action list** to promote multi-leverage moves.
- Write the bullets into the **Cross-cutting tensions** block.
- Generate the **Key findings** block (5-7 one-sentence bullets, one per section).
- Generate the **Three positioning options skim layer** (one sentence per option, front of report).
- Draft the **Conclusion** (2-3 short paragraphs: what to do this week, paid-engagement path, book-a-call CTA at https://entirecommerce.ai/audit).

---

## Step 6. Produce the ICE action list

Every candidate positioning move becomes a candidate initiative. Examples:

- Rewrite homepage H1 and subhead to the recommended option
- Run two-week ad test: recommended option primary text vs current-state
- Update Instagram bio and pinned posts
- Rebuild email welcome flow with the recommended primary promise
- Brief the designer on the tone-of-voice adjectives
- Test the recommended headline with five ICP prospects (qualitative comprehension check)
- Update product-page H1s for top-3 revenue SKUs
- Commission About page rewrite with three verbatim founder quotes

Score each on Impact x Confidence x Effort (inverse). Rank descending. Group:

- **This week**: top 5 items. Homepage test usually leads.
- **Next 30 days**: next 10 items.
- **Backlog**: everything else.

No P0/P1/P2 labels. Bucket names only.

---

## Step 7. Voice enforcement gate (mandatory before writing to disk)

Positioning writing invites every banned pattern. Run the gate carefully.

Grep the full draft for each banned pattern and rewrite every match:

| Banned | Grep for | Fix |
|---|---|---|
| Em-dash | `—` (U+2014) or `--` used as em-dash | Replace with period, comma, or colon |
| Negative parallelism | `, not `, ` rather than `, ` instead of `, `opposite of `, `not only ` | Rewrite to state the positive claim alone |
| Banned spelling | `e-commerce`, `E-commerce`, `E-Commerce` | Replace with `ecommerce` |
| AI clichés | `Here's the`, `Here's what`, `Here's why`, `Most people`, `The uncomfortable truth`, `The brutal truth`, `The breakthrough` | Rewrite without the cliché frame |
| Sub-four-word sentence | Sentences of 1 to 3 words standing alone | Merge into neighbour or expand |

Safe / Bold / Bet-the-brand option framing invites "X, not Y" contrasts. Resist every temptation. State what each option IS. The specifics (different category frame, different primary promise, different ceiling) do the differentiation work.

`not` is permitted only when the negation is genuinely load-bearing and cannot be rewritten.

Shipping with more than zero matches is a spec violation.

---

## Step 8. Write outputs

Report structure (fixed order):

```
# Positioning Audit: {Brand Name} ({YYYY-MM-DD})

Path: {A / B}
Mode: {Full / Quick / Competitor-deep / Pre-launch}

## Executive summary
(3-4 sentences leading with the positioning call)

## The intersection map
(Founder Vision | ICP Language | Competitor Whitespace, with overlap, whitespace, misalignment regions called out)

## Key findings
(5-7 one-line bullets across sections)

## The three positioning options (skim layer)
(One sentence per option: Safe, Bold, Bet-the-brand)

## 1. Founder vision capture
## 2. Current-state messaging audit (Path A only)
## 3. Audience insights
## 4. Competitor positioning scan
## 5. Overlap, whitespace, misalignment synthesis
## 6. Three positioning options (detailed)
## 7. Recommendation with reasoning
## 8. Messaging rollout plan

## Cross-cutting tensions
(3-5 synthesis bullets from Step 5)

## ICE action list
(Ranked initiatives grouped into This week / Next 30 days / Backlog)

## Conclusion
(2-3 short paragraphs)
```

Write the file to:

```
{cwd}/docs/positioning-audit/{YYYY-MM-DD}/positioning-audit-report.md
```

Then convert to Word doc:

```bash
pandoc {cwd}/docs/positioning-audit/{YYYY-MM-DD}/positioning-audit-report.md \
  -o {cwd}/docs/positioning-audit/{YYYY-MM-DD}/positioning-audit-report.docx \
  --toc --number-sections
```

If pandoc is missing, tell the user: `brew install pandoc` (Mac) or equivalent. Do not skip the Word doc silently.

Save supporting data to:

```
{cwd}/data/positioning-audit/{YYYY-MM-DD}/
  audience-voc-mining.md      (15-quote verbatim appendix)
  competitor-positioning-scan.md   (per-competitor capture)
  current-state-capture.md    (Path A only, surface-by-surface claim capture)
  founder-vision.md           (verbatim founder quotes from Section 1)
```

**Exactly one consolidated report file at the primary output path.** Do not produce per-section files. If sub-agents returned per-section drafts, merge them into the single file before writing.

---

## Step 9. Merge into actions.md

If the current working directory has an `actions.md`, merge the five items from the ICE "This week" bucket into the Next Actions section. Respect existing priority caps (P0 max 5, P1 max 10, P2 max 15). If a tier is over cap, rescore by ICE and demote the weakest before adding.

---

## Step 10. Commit (optional)

If the folder is a git repo, commit the report, Word doc, data files, and updated actions.md. Commit message format:

```
Positioning audit: {Brand Name} ({YYYY-MM-DD}): {recommended option in 6 words}
```

---

## Voice conventions (strict, applied throughout)

- No em-dashes. Use period, comma, or colon.
- No negative parallelisms. State the positive.
- Four-word sentence floor.
- Spelling: "ecommerce" one word.
- No AI clichés.
- Every finding traces to real data. No fabricated numbers. No invented sources.
- ICP language discipline: use the buyer's exact phrases in Sections 5, 6, 7, 8. Founder phrases appear only where traceable to the Section 1 capture.

---

## Acceptance criteria

- End-to-end from this one prompt. No manual copy-paste between steps.
- Correct path detection (A or B) and mode selection with user confirmation.
- Single consolidated report at the output path. Cross-cutting tensions, Key findings, Three-option skim layer, and Conclusion populated by the synthesis pass.
- Three full positioning options with eight-element messaging systems each.
- One named recommendation with reasoning.
- Word doc produced alongside the markdown via pandoc.
- No invented data. Audience insights traceable to 15 verbatim quotes.
- Voice enforcement gate run before write. Zero banned-pattern matches in final output.

---

## What to do with the output

The top 5 items in the ICE "This week" bucket go to work this week. The recommended option in Section 7 is the positioning call the founder commits to. Run the proof test in Section 7. If it passes, roll out per Section 8. If it fails, return to Section 6 and tune.

Want this run for you on a live engagement with a weekly review cadence, a daily dashboard, and the thirty-plus downstream playbooks across every GTM function? Book a call at https://entirecommerce.ai/audit.
