<div align="center">

---

### 🎯 **[Want us to run this for you? Book a call →](https://entirecommerce.ai/audit)**

---

</div>

# Positioning Audit Playbook

## A standalone brand positioning audit you can run on your own brand in 20 to 30 minutes inside Claude Code. Pulls apart founder vision, ICP language, and competitor whitespace. Hands back three positioning options with full messaging systems. Delivered as a Word doc plus the markdown source. Built by Nishant Kapoor at EntireCommerce AI.

---

<div align="center">

### ⚡ Fastest way to use this playbook

**Paste this document's URL into Claude Code and say:**

> *"Read this and take me through it step by step."*

**Claude will interview you for the business context, walk you through any missing API setup, and run the full positioning audit end-to-end. You don't need to read the rest of this document.**

</div>

---

## Who This Playbook Is For

This playbook is for three people.

**The founder-led DTC brand owner post-product-market-fit.** You have traffic. You have revenue. You also have the nagging feeling your messaging is blurry. You can describe your product in five different ways depending on who you are talking to, and you suspect none of the five is sharp enough. You want a positioning diagnostic that tells you what the ICP actually asks for, where the competition is crowding, and which positioning territory you could own with a clear conscience.

**The fractional CMO inheriting a brand with stale messaging.** You picked up a new engagement and the positioning on the site is two years old, written by a designer who is no longer involved, and possibly never grounded in real audience research in the first place. You need to rebuild the frame, and you need a diagnostic output you can share with the founder in week one that justifies the direction you are about to take.

**The in-house growth lead prepping for a rebrand.** The brand has agreed to a rebrand. A design agency is about to quote six figures for the job. Before the brief lands, you want a positioning audit that names the category frame, the primary promise, and the messaging system the agency should work from. Without that, the agency picks the positioning, which is backwards.

If you have been piecing together positioning drafts by staring at competitor homepages, running customer interviews you never transcribe, and revising the about page on instinct, this playbook compresses all of it into one consolidated output in a single Claude Code session.

---

## What The Positioning Audit Actually Is

**The short version.** Three inputs, eight sections, three positioning options, one recommendation. Claude Code runs the diagnostic end-to-end: captures the founder's vision in their own words, audits every positioning claim the brand currently makes across the homepage, product pages, ads, and email, mines the ICP's actual language from Reddit, X, Quora, YouTube, and niche forums, scans the 3 to 5 competitors you name for their explicit positioning claims, and synthesises the three datasets into a clear intersection map. Overlap, whitespace, misalignment. Three positioning options (Safe, Bold, Bet-the-brand) follow from the intersection. Each option has a full messaging system: category frame, positioning statement, headline and subhead, five primary promises, three objection-handling lines, tone of voice brief, three example ad headlines, and an example social bio. One recommendation with reasoning.

**Best for.** Premium DTC brands. AOV $500+ or 2x category median. Founder-led. 5,000+ sessions per month, or pre-launch with a clear ICP and 3 to 5 named competitors. US, UK, or English-speaking European markets. Works outside that ICP, is tuned for it.

**How it's different.** Three things most positioning audits skip.

First, the **three-way intersection**. A typical brand audit looks at founder vision OR customer research OR competitor analysis. This playbook forces the three datasets into one map on purpose, and the positioning call comes from where the three intersect. The overlap region (founder and ICP use the same language, and current site also uses it) is the strongest ground. The whitespace (ICP asks for something no competitor delivers) is the opportunity. The misalignment (founder vision drifts from ICP language) is the drag. Most audits stop at one axis. This one runs all three.

Second, the **three-option output**. The audit hands you Safe, Bold, and Bet-the-brand options. A safe option iterates on the current positioning. A bold option leans into the strongest whitespace. A bet-the-brand option reshapes the brand around a category-creating claim. Each option carries a different risk-reward profile, and the founder picks based on conviction and 12-month revenue goal. This beats a single-recommendation deliverable because positioning is a commitment, and commitments stick when the decision-maker picks from options.

Third, the **founder-voice friendly** method. Section 1 captures the founder's vocabulary verbatim. Phrases the founder reaches for when describing the brand to a sceptic become positioning raw material in Section 6. The audit never overrides the founder's voice with a marketing-school template. Where founder language matches ICP language (Section 5.1), the playbook doubles down. Where founder language drifts from ICP language (Section 5.4), the playbook names the drift explicitly and lets the founder choose whether to swap the phrase or build a campaign that teaches the audience the founder's frame.

**Skip this playbook if** your brand has less than 3 months of trading and zero public surfaces (a dedicated pre-launch brand audit is the better fit), you are a B2B SaaS or a service business (the DTC benchmarks and audience-mining sources misalign), or the founder does not want to engage with the interview in Section 1 (the playbook leans hard on founder voice, and without it the output is thinner).

---

## Setup (15 Minutes)

### Prerequisites

Before you start, make sure you have:

- **Claude Code** installed. Download from [claude.com/claude-code](https://claude.com/claude-code). Verify with `claude --version`.
- **pandoc** installed for the Word-doc export. On macOS: `brew install pandoc`. On Windows: [pandoc.org/installing.html](https://pandoc.org/installing.html). Verify with `pandoc --version`.
- **A project folder** on your machine. One per brand you audit.

### Cost overview

The playbook itself is free. You pay for API credits consumed by tools the audit uses. Most are free or near-free on this particular playbook because the positioning audit is External-only.

| Tool | Subscription model | Typical per-run cost | Role |
|---|---|---|---|
| Serper | Free tier gives 2,500 credits | Under $0.50 | Optional. Competitor SERP snippet capture for Section 4. |
| Claude / ChatGPT / Perplexity | Your existing subscriptions | $0 | AEO positioning probes. "Who is the best X for Y?" style queries. |
| WebFetch (built into Claude Code) | Free | $0 | Current-state audit (Section 2) and competitor homepage scans (Section 4). |
| Reddit / X / Quora / YouTube public pages | Free | $0 | ICP language mining in Section 3. |
| Meta Ad Library | Free | $0 | Competitor ad angle capture in Section 4.7. |

**Typical total cost per full positioning audit run: $0 to $1.** The playbook can run end-to-end without any paid external tools. Serper is optional; it polishes the Section 4 SERP snippet capture.

Numbers above are approximate as of April 2026. Pricing changes. When you run the master prompt, Claude will print the credential inventory and offer to look up current sign-up steps for anything missing.

### Step 1: Create the project folder

```bash
mkdir my-brand-positioning && cd my-brand-positioning
```

Drop the three files from this bundle (CLAUDE.md, positioning-audit.md, README.md) into the folder.

### Step 2: Set up your .env (optional for this playbook)

The positioning audit runs mostly without API credentials. Serper helps with competitor SERP snippet capture. If you already have a `.env` in place for other EntireCommerce playbooks (GTM audit, SEO audit), this playbook reads from the same file with no extra setup.

Minimum recommended `.env` if you want Serper snippets:

```
SERPER_API_KEY=your_key
```

### Step 3: Populate CLAUDE.md (or let Claude interview you)

Two options:

**Option A (recommended, fastest):** Leave `CLAUDE.md` as-is. When you run the master prompt in Step 5, Claude interviews you conversationally for the positioning fields. Takes about 10 minutes.

**Option B (DIY):** Open `CLAUDE.md` and fill in every `{placeholder}` yourself before running the audit.

Either option produces the same end state: a populated `CLAUDE.md` that grounds every playbook you run from this folder.

**Gotcha I hit:** Three to five competitor URLs are load-bearing. Section 4 runs on them directly. If you leave the field blank, Claude auto-derives competitors from the SERPs, which usually works, your hand-picked list is always sharper.

### Step 4: Open Claude Code in the folder

```bash
claude
```

Claude Code loads `CLAUDE.md` automatically on session start.

---

## The Three Files in This Bundle

### File 1: CLAUDE.md (business-briefing template)

**Path:** `{your-project-folder}/CLAUDE.md`
**What it does:** Claude Code loads this on every session start. Grounds the positioning audit in your brand's specifics: brand name, URL, product category, ICP in founder's words, current positioning statement, competitors, 12-month revenue goal, key objection, what the founder wishes customers would say.
**How to use it:** Replace every `{placeholder}` with your specifics. Founder voice beats marketing copy.

### File 2: positioning-audit.md (the master prompt Claude runs)

**Path:** `{your-project-folder}/positioning-audit.md`
**What it does:** The prompt Claude executes end-to-end to produce the audit. Covers all eight sections plus the synthesis pass plus the voice-enforcement gate plus the pandoc Word-doc export.
**How to use it:** Paste its entire contents into Claude Code and hit enter. Leave the structure alone.

### File 3: README.md

**Path:** `{your-project-folder}/README.md`
**What it does:** You're reading it. Setup, run, and troubleshooting reference.

---

## Your First Run

Five steps. Twenty to thirty minutes.

1. **Open Claude Code in your project folder.** `cd my-brand-positioning && claude`
2. **Paste the full contents of `positioning-audit.md` into the terminal.** Hit enter.
3. **Claude prints a credential inventory.** Mostly informational for this playbook. Serper can add polish, everything else runs on WebFetch plus public LLM probes.
4. **Claude auto-detects the path (A or B) and asks you to confirm the mode** (Full, Quick, Competitor-deep, Pre-launch).
5. **Claude runs the audit.** Interviews you for founder vision, audits your current-state messaging, mines ICP language via WebSearch, scans 3 to 5 competitors, builds the intersection map, produces three positioning options with messaging systems, runs the synthesis pass, runs the voice gate, writes the report.

Output lands at:

```
{your-project-folder}/docs/positioning-audit/YYYY-MM-DD/positioning-audit-report.md
{your-project-folder}/docs/positioning-audit/YYYY-MM-DD/positioning-audit-report.docx
```

Plus supporting evidence (15-quote audience appendix, per-competitor capture, current-state capture, founder-vision quotes) in `{your-project-folder}/data/positioning-audit/YYYY-MM-DD/`.

---

## What You'll Get

Ten high-value deliverables in one consolidated report.

1. **Executive summary with the intersection map front-loaded.** A 3-4 sentence narrative leading with the recommended positioning move, plus a one-visual intersection map (founder vision, ICP language, competitor whitespace). Produced by a dedicated synthesis pass.
2. **Key findings and three-option skim layer at the top.** 5-7 skim-readable bullets and one sentence per positioning option (Safe, Bold, Bet-the-brand), front-loaded for 90-second reading.
3. **Founder vision capture.** Seven-field structured output: 12-month revenue goal, positioning hypothesis, product origin, constraints, biggest-lever belief, the phrases the founder uses when describing the brand, what the founder wishes customers would say. Verbatim founder quotes stored in the data folder.
4. **Current-state messaging audit (Path A only).** Table of 20 to 40 rows cataloguing every explicit positioning claim across homepage, product pages, ads, social bios, email welcome. Frequency chart by claim category (Feature, Benefit, Identity, Category, Social proof). List of the brand's 10 most-repeated phrases.
5. **Audience insights one-pager.** Avatar, core tension, 5-7 recurring phrases, 3 headline options, top 3 objections with responses, positioning angle, belief shift. Built from 15 verbatim customer quotes mined from Reddit, X, Quora, YouTube, and niche forums.
6. **Competitor positioning scan.** Per-competitor homepage hero capture, elevator pitch, primary promise, secondary claims, tone of voice, visual identity flavour, ad-library angles. Plus a 2x2 positioning map on the two dominant axes the category plays on.
7. **Overlap, whitespace, misalignment synthesis.** Four-part output naming the strongest ground (founder and ICP agree), the commodity territory (current claims overlap with all competitors), the whitespace (ICP asks for X that no competitor delivers), and the misalignment (founder vision drifts from ICP language).
8. **Three positioning options with full messaging systems.** Safe, Bold, Bet-the-brand. Each option has: category frame, one-sentence positioning statement, headline and subhead, five primary promises, three objection-handling lines, tone of voice brief, three example ad headlines, example social bio.
9. **Recommendation with reasoning.** One named option. Three evidence-backed bullets for why. Named risks per option. A concrete test the founder runs before full rollout.
10. **Messaging rollout plan and ICE action list.** Sequenced rollout (homepage first, ads second, social bios, email welcome, product pages last). Three tests with pass criteria. KPI table. ICE-scored action list grouped into This week, Next 30 days, Backlog.

**Format.** One consolidated Word doc plus the markdown source. Typically 3,500 to 6,000 words. Reading time around 20 minutes cover to cover, 90 seconds via the Key Findings block at the top.

---

## Modes

The audit auto-detects the path and asks you to confirm the mode.

| Mode | When it applies | What changes |
|---|---|---|
| Full | Path A, 30 minutes | All eight sections plus synthesis. Current-state audit in depth. Three full positioning options. Rollout plan. |
| Quick | Path A or B, 15 minutes | Section 1 (founder vision, compressed), Section 3 (audience, 5 quotes), Section 5 whitespace-only, one recommended positioning option. |
| Competitor-deep | Path A, 45 minutes | Full audit plus single-competitor teardown with response positioning. |
| Pre-launch | Path B, 25 minutes | Skip Section 2 (no current-state surfaces). Section 4 runs in full. Section 6 output is the primary deliverable. |

---

## Honest Caveats

**The three-option output depends on the audience data quality.** If the 15-quote audience mining surfaces thin data (fewer than 10 quotes, or quotes that cluster on surface pain points without deeper emotional charge), the three positioning options will be directionally correct but less sharply differentiated. Run the Quick mode with 5 quotes only if you are time-boxed; otherwise hold out for the full 15.

**Meta Ad Library WebFetch fails more often than it succeeds.** JS-rendered, returns empty on most runs. The spec has a fallback chain (Playwright, third-party ad library indexes, manual screenshots). Expect Section 4.7 to sometimes stub with "Meta Ad Library unavailable via WebFetch; manual screenshot pass required."

**Founder interview depth correlates with output sharpness.** A 20-minute interview produces a useful Section 1. A 5-minute interview produces a thin Section 1, and every downstream section that leans on founder voice (Section 5.1, Section 5.4, Section 6) thins in sympathy. Budget time for the interview.

**Voice rules are strictly enforced.** The Safe / Bold / Bet-the-brand frame invites "X not Y" contrasts. Claude runs a mechanical grep-pass before writing the report to disk. If a banned pattern slips through, flag and rerun the voice gate.

**The audit is a decision artefact.** A positioning audit names the direction. The rebrand (design system, copy rollout, ad rewrites, email flow updates) happens after. Budget 4 to 12 weeks of execution post-audit for a Bold option, 12 to 26 weeks for a Bet-the-brand option.

**Pre-launch (Path B) output is a hypothesis.** With no live site and no trading history, the three positioning options are informed bets. The recommendation still applies, and the founder tests the chosen option with a landing page and a small ad spend before building out the full brand.

---

## Quick-Start Checklist

Work top-to-bottom.

- [ ] Claude Code installed (`claude --version` works)
- [ ] pandoc installed (`pandoc --version` works)
- [ ] Project folder created for the brand you want to audit
- [ ] CLAUDE.md from this bundle copied into the project folder
- [ ] positioning-audit.md from this bundle copied into the project folder
- [ ] Serper API key added to `.env` (optional, improves Section 4 SERP snippets)
- [ ] CLAUDE.md populated with brand specifics (three to five competitor URLs is the load-bearing field)
- [ ] 20 to 30 minutes blocked for the founder interview (Section 1 depth correlates with output sharpness)
- [ ] First run executed and Word doc produced at `docs/positioning-audit/{date}/`
- [ ] Report reviewed, one positioning option selected
- [ ] Homepage test planned: new H1 and subhead ready for a two-week A/B
- [ ] Ad test planned: new primary text ready for a two-week split
- [ ] Re-run in 90 days once lagging indicators have had time to move
- [ ] Book a call if you would rather we run this for you: [entirecommerce.ai/audit](https://entirecommerce.ai/audit)

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| "pandoc not found" at Word-doc export | pandoc not installed | `brew install pandoc` (macOS) or [pandoc.org/installing.html](https://pandoc.org/installing.html) |
| Section 4 (competitors) returns sparse data | Competitor URLs missing from CLAUDE.md, Claude had to auto-derive | Fill in the three to five competitor URLs in CLAUDE.md and rerun |
| Section 3 (audience) surfaces fewer than 10 quotes | Niche category with sparse Reddit / Quora conversations | Expand source list: niche blog comment sections, YouTube comments on category review videos, industry podcast transcripts |
| Meta Ad Library scan fails | WebFetch against JS-rendered page returns empty | Use the fallback chain: third-party ad library index, manual screenshots. Note the limitation in the report |
| Report splits into per-section files | Sub-agent split issue | Rerun. The spec bans per-section files; a clean run consolidates |
| Voice gate flags em-dashes or "X, not Y" patterns | Style drift in sub-agent output (positioning work is a high-risk zone) | Paste the banned-patterns list back into Claude and ask it to scan-and-fix the full file |
| Three options feel directionally similar | Thin audience data or thin founder interview | Rerun with fuller inputs. The options differentiate on ICP language and founder voice, they need raw material to sharpen |
| Founder disagrees with the recommendation | Expected on Bet-the-brand recommendations | The three options exist so the founder can pick. Disagreement is a signal to revisit Section 1 capture and tune the recommendation. |

---

## Credit

Built by Nishant Kapoor at EntireCommerce AI.

- **LinkedIn**: [linkedin.com/in/nishantkapoor1](https://www.linkedin.com/in/nishantkapoor1)
- **Email**: nishant@entirecommerce.co
- **Book a call**: [entirecommerce.ai/audit](https://entirecommerce.ai/audit)
- **Full playbook library** (GTM audit, weekly review, SEO audit, CRO review, competitor creative audit, content strategy, and thirty-plus more): [entirecommerce.ai/playbooks](https://entirecommerce.ai/playbooks)

Use this playbook freely. Share it with other DTC founders. If you ship a case study running it on your brand, tag us. We will link to it from the site.
