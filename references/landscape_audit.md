# Phase 1: Landscape audit (touchpoints + competitor map)

Method file for Phase 1 of /rebrand. Runs only after the Phase 0 gate (creative brief approved). Output is one HTML gate page, opened as a local review surface, that feeds the visual territories (see `references/brand_strategy.md`). The Phase 1 gate itself (territory choice) happens after territories are built; this file produces the evidence those territories stand on.

Ground rules for this phase:

- Zero image-generation cost. Everything here is screenshots, `curl` downloads, and researcher subagents. No image-generation model (Gemini or otherwise) is invoked in Phase 1.
- All output lands in the single engagement directory from SKILL.md (Output locations), one per engagement: `<engagement-map>/{yymmdd}-rebrand-{merk}/` in your workspace (e.g. `<engagement-map>/260831-rebrand-mr/`), with its shared `assets/` subfolder for screenshots and downloaded logo files. Phase 1 does not open a new directory; it writes into the directory Phase 0 created, so the gate pages of all phases can reference each other and the brief relatively. Never write into the live brand-style folder of the existing identity; the current brand assets stay untouched until Phase 5 migration.
- Read the creative brief first. The audit answers "where is visual room, given THIS positioning", not "what does the market look like in general". Every analysis step below references brief attributes by name.

---

## Step 1: Touchpoint audit (where the brand actually lives)

Before looking outward, inventory the brand as it exists today. This wall is the "before" evidence and becomes the migration checklist in Phase 5.

Build the touchpoint list from the brief. As a worked example, the Mission Relearn set:

| Touchpoint | Source | Capture method |
|---|---|---|
| missionrelearn.com | live site | headless Chrome, viewport 1280x800: hero + one content section |
| Quotes / proposals | newest issued quote or proposal PDF in the document archive | `pdftoppm -png -f 1 -l 1` on page 1 |
| Decks | most recent deck export (PDF) | `pdftoppm` cover + one content slide |
| LinkedIn | profile header + 2 recent posts with visuals | screenshot via an authenticated browser session (e.g. a browser-automation MCP) |
| Newsletter | latest newsletter edition | screenshot of header + first scroll |
| Dashboard | live dashboard URL (if the brand has a product surface) | headless Chrome viewport screenshot |
| Academy | academy landing/lesson page | headless Chrome viewport screenshot |

Capture rules:

- Same viewport width for every web capture (1280px) so the wall compares like with like.
- Viewport screenshots, never full-page `captureBeyondViewport`: scroll-reveal sections render empty in full-page captures and produce false findings.
- Batch-render gotchas for headless Chrome: one render per fresh profile (`--user-data-dir` on a fresh temp dir), Chrome often does not exit so kill by process group, and delete a stale output file BEFORE re-rendering (a poll-until-stable otherwise sees the old bytes as "stable" and you kill Chrome before it wrote).
- Save as `assets/touchpoint_<name>.png`.

Per touchpoint, write exactly one line labeled **What jars:**. It must be observable in the screenshot and name the artifact. Good: "What jars: the rocket sits here in a different coral (#F26E5A) than on the site (#ED7059)." Bad: "What jars: it feels dated." If nothing genuinely jars, write "Consistent, no friction." and move on; do not invent friction to seem thorough.

Also record per touchpoint: which logo variant is in use, which accent-color hex, which fonts actually render (decks and docx often fall back from the brand heading font). Inconsistencies found here are findings, not embarrassments; they go on the gate page.

---

## Step 2: The corpus (three rings)

Collect the competitor set before scanning anything. Uniform corpus first, analysis second; scanning brands one by one as you think of them guarantees a biased map.

**Ring 1, direct competitors (target 8-12).** Brands a prospect would shortlist next to this one. Worked example, Mission Relearn: NL agencies and solo consultants selling AI-literacy training, AI-literacy workshops, and AI-adoption guidance to government, education, and enterprise. Candidate sources, in this order:
1. The creative brief (Phase 0 names who the brand must convince and against whom).
2. Optional project knowledge (e.g. a clients file if you have one): competitors that surfaced in real deals.
3. Web search: for the MR example "AI geletterdheid training", "AI training bureau overheid", "AI literacy consultancy Nederland" (query strings in the market's own language), plus vendors visible in the ecosystems the brand operates in (e.g. an education consortium or national education program the client takes part in).

**Ring 2, sector neighbours (target 5-8).** Not direct rivals, but brands the buyer sees in the same week. For the MR example: NL EdTech products, learning platforms, generalist consultancies with an AI practice, government program identities (national education programs), training agencies outside AI.

**Ring 3, aspirational and anti-reference (target 3-5).** Taken from Discovery round 2 (admired brands and anti-references). Include at least one anti-reference on purpose: it calibrates the far end of the map.

Total corpus: 16-25 brands. Below 16, clusters are anecdotes; above 25, the wall stops being readable.

Confirm the corpus with the client before spending research time. One AskUserQuestion call, one question:

> Question: "This is the scan list: [n] direct competitors, [n] sector neighbours, [n] reference brands. Is this list right?"
> Options: "List is right, start the scan" / "Brands are missing (I'll name them)" / "Take brands off"

---

## Step 3: Running the scan

### Researcher subagents

Launch one researcher subagent per 4-6 brands, in parallel. Subagents research and describe; they do not capture pixels. The main session does all downloading and screenshotting afterward, so every visual lands at the same scale and quality.

Prompt template per subagent (fill the bracketed parts):

```
You are doing a visual brand audit for a rebranding project. For each of these
brands: [brand list with URLs if known].

Find and return, per brand, exactly these fields:
1. homepage_url and, if findable, a direct URL to the logo file (SVG/PNG).
2. logo_mark: one line describing the geometry (e.g. "abstract node-and-line
   network in a circle", "lowercase geometric sans wordmark, no mark").
3. core_color: the dominant brand hue as a band (primary blue / blue-purple
   gradient / green / orange-coral / red / black-grey / multicolor). Do not
   guess hex codes from memory; the main session samples those from the
   downloaded asset.
4. form_family: geometric / organic / typographic-only / figurative.
5. headline_type: geometric sans / humanist sans / grotesque / serif /
   display / script. Plus: is body type the same family or a contrast?
6. imagery_style: photo / illustration / 3D / abstract gradient / none.
7. tone_words: 3 words the brand itself uses on its homepage, verbatim
   (e.g. "growth", "learning", "connect", "empower").
8. cliche_flags: which of these appear anywhere in the identity: brain,
   neural nodes/synapses, circuit traces, hexagon, robot, owl, graduation
   cap, open book, pencil, lightbulb, swoosh, radial gradient circle with
   central opening, generic upward arrow, handshake, puzzle pieces,
   tree-of-knowledge.
Return a markdown table, one row per brand, plus source URLs. If a field is
not observable, write "unknown" instead of guessing. Do not print any
credentials or config files.
```

### Main-session capture

After the subagents return:

1. `curl -sL` each logo asset into `assets/logo_<brand>.png|svg`. Sample the dominant color to a real hex with python (Pillow) from the downloaded file; this replaces the subagent's hue-band guess where possible.
2. Screenshot each homepage at 1280x800 into `assets/scan_<brand>.png` (same Chrome recipe and gotchas as Step 1).
3. Build the brandscape wall: every logo in an identical tile (160px box, same padding, neutral background) on the gate page. Uniform scale is not cosmetic: clustering only becomes visible when marks sit side by side at equal size. A wall of mixed-size screenshots hides exactly the sameness you are looking for.

Record per brand, final schema (this feeds the map): name, ring (1/2/3), core color hex, hue band, form family, headline type class, imagery style, tone words, cliche flags.

---

## Step 4: Analysis

### 4a. Count, do not eyeball

Redesigns drift toward category norms because designers keep seeing the same references. The counter-move is literal counting. Tally the corpus per element:

- Hue bands: how many brands per band. Benchmark for calibration: 39% of Fortune 500 logos are primary blue, and blue dominates consulting because it codes trust. Expect the direct ring to skew blue or blue-purple.
- Form family and mark geometry.
- Headline type class.

If 70% or more of the corpus shares the same hue band, mark geometry, AND type class, name that cluster explicitly in one phrase on the gate page (e.g. "blue, geometric sans, abstract node mark") and render it as one dense blob on the map. Optional supporting stat: Wynter has published survey research on category sameness among B2B/SaaS marketing leaders. Before citing any figure from it on the gate page, have one of the Phase 1 researcher subagents verify the study first: year, surveyed population, the exact percentages, and the source URL. If verified, cite the figures with the URL in a footnote on the gate page; if the study cannot be pinned to a source, leave it out entirely. The sameness argument does not depend on it: the corpus's own 70% tally and the blanding literature carry it. The formula behind the blob has a name, "blanding" (Brunfaut/Greenwood, 2018): invented name, clean geometric sans, generous whitespace, no ornament. It was the 2015-2024 default and the backlash (characterful serifs, flat color, expressive type) is the current emergent code.

### 4b. Semiotic layer: residual / dominant / emergent

Classify every recurring convention in the corpus as one of three codes:

- **Residual**: fading conventions. In education: crests, traditional serif wordmarks, open-book icons.
- **Dominant**: the category's current markers. In AI: node networks, gradients, blue-purple, radial-symmetric gradient circles with a central opening (the pattern OpenAI, Claude, and peers all share; VelvetShark documented it).
- **Emergent**: early signals converging on tomorrow's norm. Post-2024: characterful serifs, flat color, visible "human fingerprint" typography.

Sector priors to verify against the actual corpus (verify, never copy blindly):

- **AI consultancy/startups.** Dominant: node-and-line marks, brains, circuits, hexagons, electric blue and deep purple gradients, geometric sans wordmarks. Escape routes seen working in the wild: anchor to a concrete non-AI object (DeepSeek's whale, Midjourney's sailboat), sharp angles instead of radial symmetry, flat color instead of gradient, creative negative space (FedEx arrow is the canonical reference).
- **EdTech.** Dominant: owls, graduation caps, open books, pencils, lightbulbs; bright primary blue/yellow/green; rounded friendly sans. The successful outliers skipped the literal symbol set: Duolingo made the owl a personality instead of a wisdom cliche, Khan Academy chose a leaf (growth) over anything school-shaped.
- **NL education/training.** Institutional layer (ministries, national programs, foundations): fresh accessible palettes, connection/community symbolism, gradients "for energy and dynamism". Commercial training agencies: warm-but-corporate blue or orange, person photos, rounded sans, tone words "groei", "leren", "verbinden" (grow, learn, connect). Residual: crests and serifs at traditional universities. Worked-example implication for Mission Relearn: coral sits off the dominant hue band of this market, which makes it an existing differentiator to protect, not a candidate for replacement. The audit must confirm this against the corpus: count how many scanned brands use a warm red-orange.

Decision rule (Keller): the new identity keeps 1-2 dominant codes for category credibility (points of parity) and deliberately breaks the rest (points of difference). For every recurring sign, ask three questions and note the answers: what meaning does it generate, is that the meaning the brief needs, and what does the gap cost?

### 4c. Cliche kill-list

The blacklist below goes on the gate page verbatim and is copied forward into the Phase 2 concept notes and the Phase 3 design brief for the form-engine run (the logo-generator skill, github.com/op7418/logo-generator-skill, if installed; else direct SVG generation). Any concept or variant containing one of these gets flagged automatically; it may only survive with a written justification tied to a named brief attribute (Duolingo-style subversion counts, lazy use does not).

> **Forbidden without explicit justification:** brain, neural nodes/synapses, circuit traces, hexagon, robot, owl, graduation cap, open book, pencil, lightbulb, swoosh, radial gradient circle with a central opening, generic upward growth arrow, handshake, puzzle pieces, tree of knowledge.

Add corpus-specific entries: any element that 3+ brands in ring 1 already use joins the list, even if it is not on the generic list.

### 4d. Choosing the 2x2 axes

The map is visual, not strategic. Business-positioning axes (price, segment, service model) belong in the Phase 0 brief; this map plots what a buyer can SEE. Four rules:

1. **Visual and observable.** Both poles must be judgeable from a homepage screenshot plus logo alone. The test: could two people independently place a brand on the axis within one step of each other, using only the captures? "Innovative ↔ traditional" fails this test (it is an opinion); "geometric ↔ organic" passes.
2. **Orthogonal.** If the plotted corpus forms a rough diagonal, the axes correlate and you are measuring one thing twice ("premium ↔ budget" x "high-end ↔ basic" is the classic double). Reject the pair and pick again. Do this rejection visibly: the gate page notes which pair was tried and dropped.
3. **Contrasting poles, plain labels.** Each pole is a real opposite, phrased so the client and an outside reader read it the same way.
4. **Separating power.** Prefer the pair that both spreads the corpus AND connects to a brief attribute. A map where all 20 brands land in one quadrant is a finding (name the blob), but a second map with a better-separating pair should accompany it.

Default pairs for this sector, in order of preference:

- "warm ↔ cool" (palette) x "geometric ↔ organic" (form language)
- "playful ↔ formal" (tone) x "abstract ↔ literal" (mark)

Plot the full corpus with ring-coded markers: ring 1 filled dot, ring 2 outlined dot, ring 3 star. Plot the brand's CURRENT identity as its own marker in its own accent color (coral, in the MR worked example). The distance between the brand-now marker and the white space is the size of the design job; say that number of quadrants out loud on the gate page.

### 4e. Reading the map: naming the white space

Read spacing and clusters, not just positions. A crowded zone is sameness risk; an empty quadrant is a candidate, nothing more. A white-space claim is only valid when it passes all three tests:

1. **Empty**: genuinely empty in the scanned corpus (point at the map).
2. **Wanted**: desirable to the target buyer named in the brief (point at the brief attribute it serves).
3. **Credible**: ownable and credible for this brand with its history and assets (point at an existing asset or proof).

Empty because nobody wants it is a trap, not an opportunity. If no quadrant passes all three, say so on the gate page and propose the least-crowded credible position instead; a forced white-space claim poisons Phase 2.

### 4f. Fame x Uniqueness check on existing assets

Before any territory work, score the brand's current distinctive assets on Romaniuk's two dimensions (Ehrenberg-Bass, Building Distinctive Brand Assets): **Fame** (how strongly the audience links the asset to the brand) and **Uniqueness** (whether they link it ONLY to this brand). Without survey budget, the solo-founder proxy:

- Uniqueness: does any brand in the corpus use this element? (Count it.)
- Fame: does the existing audience already meet this element everywhere? (In the MR worked example: coral appears in all output, site, quotes, decks, LinkedIn. That is seed fame.)

Score at minimum the brand's accent color, its mark, its wordmark treatment, and its heading typeface as brand voice (for MR: the coral, the rocket mark, the wordmark, Cal Sans). Standing rule: never abandon an asset with existing fame for novelty. High-fame assets are constraints on the territories, and that is a feature; it is what makes "evolution" cheaper than "revolution".

---

## Step 5: Deliverable: the landscape gate page

One HTML page in the engagement directory: `<engagement-map>/{yymmdd}-rebrand-{merk}/{YYMMDD}_Landscape-audit.html`. Design language matches the engagement's earlier gate pages; in the MR worked example the tokens are `--coral: #F36E59`, `--ink: #231F20`, `--paper: #FAF8F6`, `--line: #E8E2DD`, Cal Sans headings, Open Sans body. For a client run, use the client's current tokens or a neutral studio style. Images referenced relatively from `assets/`.

Sections, in this order:

1. **Touchpoint wall.** All touchpoint screenshots at equal width, each with its "What jars:" line and the logo-variant/accent-hex/font findings.
2. **Brandscape wall.** Every corpus logo in an identical 160px tile, grouped by ring, brand name + hue band as caption.
3. **Cluster summary.** The tallies (hue band, form family, type class) as small bar counts, the named cluster phrase if the 70% threshold is hit, and the residual/dominant/emergent table with the Keller keep/break decision per code.
4. **2x2 map.** Inline SVG, pole labels, ring-coded markers, brand-now marker in the brand's accent color, the rejected axis pair named in a footnote.
5. **Cliche blacklist.** The forbidden list plus corpus-specific additions, flagged as "carries forward to phase 2 and 3".
6. **White-space statement.** Exactly one sentence, this template: "The white space for [brand] is [visual position in axis terms], because [target audience from the brief] looks for [feeling/meaning] there and none of the [n] scanned brands occupies it." Below it, the three validity tests as pass/fail rows with one line of evidence each, and the Fame x Uniqueness scores of the current assets.
7. **Next step.** One line: "This map feeds the 2-3 territories (phase 1 gate). Choose below."

Open the gate page as a local review surface (the HTML in the browser):

```
open "<engagement-map>/{yymmdd}-rebrand-{merk}/{YYMMDD}_Landscape-audit.html"
```

Then one AskUserQuestion call (this is a review checkpoint, not the Phase 1 gate; the gate follows the territories):

> Question: "Does this map match your picture of the market?"
> Options: "Yes, build the territories on this white space" / "The axes are off, try another pair" / "Brands are missing, scan more"

Free-form corrections come in via Other; fold them in and re-render the same page (new findings appended, nothing overwritten elsewhere).

---

## Quality bar (check before opening the gate page)

- Corpus size at least 16, with all three rings represented.
- Every brand has all recorded fields filled or explicitly "unknown"; no guessed hex codes.
- Every touchpoint has a screenshot AND a "What jars:" line (or "Consistent, no friction.").
- At least one axis pair was tested and rejected for correlation, and the rejection is noted on the page.
- The white-space statement passes all three validity tests, or the page says explicitly that it does not and proposes the fallback.
- The accent-color fame/uniqueness count against the corpus is on the page.
- No em-dash characters anywhere in the page or this phase's output.
