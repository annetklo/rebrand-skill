---
name: rebrand
description: >
  Run a full studio-grade rebranding engagement, from discovery questions through strategy,
  concept, design exploration, stress-testing, and delivery of guidelines and assets. Modeled
  on how Pentagram, Koto, and Wolff Olins structure identity work: strategy before form, a
  signed brief before any design, a small number of defensible directions shown in context,
  and explicit client gates between phases. Uses the logo-generator skill
  (github.com/op7418/logo-generator-skill) as the form engine in the design phase when
  installed, with direct SVG generation as the fallback. Default brand is Mission Relearn,
  the worked example, but the process serves any client rebrand equally. Use when the user
  says "rebrand", "rebranding", "brand refresh", "huisstijl vernieuwen", "nieuw logo traject",
  "brand identity traject", "merkvernieuwing", or asks to rethink a brand's identity rather
  than just generate a logo.
---

# Rebrand

A six-phase rebranding process with explicit decision gates. A form engine (the
`logo-generator` skill, github.com/op7418/logo-generator-skill, if installed; direct SVG
generation otherwise) produces good marks from a loose description; this skill wraps that
engine in everything a studio does before and after the mark: questioning, research,
strategy, one carrying idea, application stress-tests, and a guidelines handoff.

## Philosophy

Four principles govern every run. They are not preferences; they are the process.

1. **Strategy before form.** No visual work starts before the creative brief is approved at
   Gate 0. Pentagram writes a Positioning Brief and has it signed before a single mark is
   sketched; Koto's rule is that the strategy must be "clear and creatively usable" before
   identity work begins. If the user asks to "just see some logos", explain that the brief
   takes one session and makes every later phase cheaper, then offer Phase 0 as the starting
   point. Only skip on an explicit, informed override.
2. **One carrying idea per concept.** Every concept must be expressible in a single sentence
   ("the mark is the orbit you step back into"). If a concept needs a paragraph to
   explain, it is decoration, not an idea. The sentence steers the mark, the wordmark, the
   color, and the language.
3. **Fitness, not taste.** Sagi Haviv: "choosing an effective logo is not about what one
   likes or dislikes: it's about what works." Every direction presented at a gate carries a
   one-paragraph argument tracing it back to the brief. Never present a bare mark: Haviv's
   Armani Exchange lesson is that the identical mark was rejected on paper and approved as
   magazine ads and storefronts. Always show marks in context.
4. **Gates where the user chooses.** Nothing is declared "done" without an explicit user
   decision at a gate review page. This skill sets its own hard bounds, in the spirit of
   how studios contract scope: maximum two revision rounds on the brief, maximum three
   refinement rounds on design. Bounded rounds are what keep a rebrand from becoming an
   endless loop.

## The six phases

Each phase ends in a gate: an HTML page in the engagement folder in your workspace
(convention: `<engagement-map>/{yymmdd}-{slug}/`), opened as a local review surface
(the HTML
in the browser, with feedback collected in chat), and then an explicit decision from
the user, asked via AskUserQuestion in the client's language. Record every gate decision
in the
engagement's decision log (a decision-documentation skill or a plain decisions file both
work). A full run takes 3 to 5 sessions; phases can also run standalone (see
"Running a partial engagement" at the end).

### Phase 0 · Discovery: the question protocol · Gate: brief approved

**Read first**: `references/discovery_questions.md` (the question bank, ~40 questions in 4
rounds, with slider pairs and anti-reference questions).

**Purpose.** This is the phase the logo-generator skips entirely. It replaces a 2-hour
Pentagram kickoff workshop plus stakeholder interviews with four structured question rounds.
The answers become the creative brief that steers everything after.

**Steps.**
1. Run the four question rounds from the question bank, every question via AskUserQuestion
   with a maximum of 4 questions per call; the question bank's method section governs how
   many calls each round takes and the total budget of 20 to 28 questions. The rounds, in
   order: (1) ambition & scope, including the single most
   important question of the whole engagement: evolution or revolution; (2) positioning,
   including personality sliders and admired brands plus anti-references with the why;
   (3) the mark: what the current mark means, whether the story still holds, whether the
   sign must work standalone at favicon/avatar size; (4) wordmark & system: name
   rendering, font feel, color sanctity, top-5 applications where the brand actually lives.
2. Between rounds, reflect back what you heard in two or three sentences before asking the
   next round. This is an interview, not a form.
3. Ask Wolff Olins' two butterfly questions somewhere in rounds 1 or 2, verbatim:
   "What makes you truly special?" and "What does the world need from you?" The
   overlap of the two answers is the raw material for the brand idea.
4. Frame the evolution/revolution question with its real criterion: revolution is justified
   only by structural change (merger, pivot, new market, name change, broken reputation);
   an equity-rich brand should evolve, because strategic refreshes compound brand equity
   instead of resetting it. The forcing question: "are we solving a real strategic problem,
   or reacting to brand boredom?"
5. Build the creative brief from `assets/brief_template.html`. Include an explicit equity
   inventory: what we keep, what we cut, what may move freely. Record answers
   verbatim (see Operating rules).
6. If real customers or stakeholders are reachable (a client engagement usually has them),
   propose 3 to 5 short interviews before finalizing the brief. DesignStudio's Airbnb
   immersion put four designers in 13 cities; the solo translation is firsthand evidence,
   not hours: talk to real users, use the product, read the actual touchpoints.

**Deliverables.** Creative brief (HTML in the engagement folder + `.md` sibling), the
scope decision (evolution or revolution), a decision log entry.

**Gate.** Open the brief on the review surface, collect feedback, revise (maximum two
revision rounds, this skill's hard bound), then ask: "Is this brief approved as the
foundation for everything that follows?" Options: "Approved, on to research" / "One more
revision round" / "Stop here, the brief is the deliverable". No visual work until this
gate passes.

### Phase 1 · Research & audit · Gate: territory choice

**Read first**: `references/landscape_audit.md` (how to run the sector scan, the 2x2 map,
the whitespace analysis).

**Purpose.** Pentagram's Discovery phase pairs the workshop with a brand audit and
competitive research before any strategy is written. Here that is a touchpoint audit plus a
visual landscape scan, ending in 2 or 3 visual territories to choose from.

**Steps.**
1. **Touchpoint audit**: inventory where the brand actually lives. For Mission Relearn:
   missionrelearn.com, quotes and proposals, decks, LinkedIn, newsletter, dashboard,
   Academy. Screenshot each, note what jars against the brief. For a client: ask for their
   top-5 touchpoints (already captured in Phase 0 round 4) and audit those.
2. **Landscape scan**: launch researcher subagents (web research) on the sector's visual
   language per `references/landscape_audit.md`. For MR: AI-literacy, EdTech NL,
   consultancies, government suppliers. Output: a 2x2 map of "where everyone stands, where
   the space is", with named competitors placed on the axes.
3. **Visual territories**: build 2 or 3 moodboard directions, each a coherent world of
   typography, color, and form language with a name ("warm science", "clear
   institute", "the spark" are the shape of it, derive real ones from the brief). This is the
   Koto/DesignStudio territory model: each territory must be arguable from the brief, not
   just aesthetically distinct.

**Deliverables.** Audit page with screenshots and findings, the 2x2 competitive map, 2 or 3
territories on one gate page (HTML in the browser).

**Gate.** Open the territories page on the review surface, collect feedback, then
AskUserQuestion: "Which territory
becomes the basis for the concepts?" with one option per territory plus "Combine elements
(explain via Other)". Log the choice.

### Phase 2 · Concept: one carrying idea · Gate: concept choice

**Read first**: `references/brand_strategy.md` (the territory method, attribute-to-form
translation tables, the one-idea principle with examples).

**Purpose.** Turn the chosen territory into 2 or 3 concepts, each with one carrying idea in
one sentence. This is where taste is replaced by argument.

**Steps.**
1. Per concept, write a concept note containing: the idea in one sentence; why it fits the
   brief (quote the brief's own words back); how it plays through the mark, the wordmark, and
   language; rough sketches (SVG or described); and the kill-criteria: the observable
   conditions under which this concept has failed. Kill-criteria keep the phase-3 iteration
   honest, because "I don't like it" is not a kill-criterion but "the sign is
   illegible at 16px" is.
2. Make the concepts span the evolution-revolution spectrum decided in Phase 0. Pentagram
   deliberately spreads its logo options across "how the client may best utilize its
   existing brand equity" and lets the gate decide; do the same, even inside a chosen
   scope, so the user sees the range before committing.
3. Present concepts with early in-context hints (a favicon, a deck cover thumbnail), never
   as bare abstractions.

**Deliverables.** 2 or 3 concept notes with sketches on one gate page.

**Gate.** Open the page, collect feedback, then: "Which concept carries the rebrand?"
Options per concept
plus "Hybrid (motivate via Other)". A hybrid choice requires the user to name which idea
carries and which elements borrow; a hybrid without one carrying idea violates principle 2
and should be pushed back on once, explicitly, before being accepted. Log the decision.

### Phase 3 · Design exploration (the logo-generator runs here) · Gate: direction choice

**Read first**: `references/wordmark_typography.md` and `references/color_system.md`. The
mark track additionally uses the logo-generator's own
`references/design_patterns.md` when that skill is installed.

**Purpose.** Three parallel tracks, all steered by the brief and the chosen concept:
mark, wordmark, color. This skill's own rule for the gate: present 4 to 6 defensible
variants, always in context, over at most three refinement rounds. The form engine
produces 6 to 8; the brief filters them down before presenting.

**Steps.**
1. **Mark track, via the form engine.** If the `logo-generator` skill
   (github.com/op7418/logo-generator-skill) is installed, invoke it (Skill tool, name
   `logo-generator`) and never modify it, it tracks an upstream repo; without it, generate
   the SVG variants directly from the same steering block. Skip
   its own Phase 1 information gathering entirely: its questions ("name, industry, concept,
   style") are already answered at brief depth. Feed it a design instruction composed of:
   the one-sentence carrying idea, the brief's personality sliders, the do's/don'ts and
   equity inventory, the chosen territory's form language, and the constraint set (must
   work at 16px favicon, single color, on navy and on paper white). Ask it for 6 to 8
   variants inside the chosen concept, not 6 random directions. Its SVG patterns, showcase
   template, and PNG export scripts do the form work; the brief does the steering.
2. **Wordmark track.** A full track, not an afterthought, and never a typed line: a
   wordmark is a designed object (see the leading principle and the mandatory exploration
   protocol in `references/wordmark_typography.md`: minimum 6 custom treatments across at
   least 3 surgery families at equal fidelity, plain type only as the argued control).
   Font candidates render in the real font (install or download the actual files, never
   approximate with a lookalike). Run the license check BEFORE presenting a candidate, so
   nobody falls in love with a font that costs a fortune or forbids logo use.
3. **Color track.** Build the palette around the core color per
   `references/color_system.md`: neutrals, supporting tints, dark-mode behavior, and WCAG
   contrast checks with the actual computed ratios shown on the page.
4. Present all three tracks on one exploration page, reusing the design language of
   earlier gate pages in the engagement folder so the series reads as one, with every mark
   shown in at least one real context per Haviv's rule. Open every design gate page with a
   system-context mock: a fragment of the client's real design language (page header,
   kicker, card) with the candidate in place, before any grid of tiles. The deciding
   question for a mark is not "does it look good on a tile" but "does the brand suddenly
   belong"; that reframing came verbatim from a client and unlocked a stalled engagement.
5. Iterate through at most two annotation rounds on the review surface, then freeze. If
   the user wants a third round, that is this skill's hard maximum; after three, the answer
   to further tweaking is "then the concept is not good enough, back to phase 2", said
   out loud. When rounds stall on taste rather than fitness, do not spend the remaining
   rounds on more variants: switch to the taste-recovery protocol and calibration rounds
   (see "Taste recovery and taste gates").
6. This gate is the natural moment for a second pair of human eyes (designer or peer);
   offer to prepare a shareable version of the exploration page for that review.

**Deliverables.** Concept-driven exploration page; a chosen mark, wordmark, and
palette.

**Gate.** "Which combination of mark, wordmark, and palette goes through to the system?"
Freeze the choice, log it.

### Phase 4 · System & stress test · Gate: go/no-go per carrier

**Read first**: `references/applications_stresstest.md` (the fixed mockup set, degradation
tests, the go/no-go checklist per carrier).

**Purpose.** Turn the frozen choice into a system and prove it survives reality. Pentagram
shows every option across website pages, social, banners, stationery, and swag; the
stress-test is that practice made into a checklist.

**Steps.**
1. Define lockup rules, clear space, minimum sizes, and misuse examples (the "never do
   this" gallery every guidelines PDF carries).
2. Build the fixed mockup set from the reference file on real carriers: favicon 16px,
   LinkedIn avatar and banner, deck cover, quote header, site header,
   email signature, sticker.
3. Run degradation tests: black-and-white photocopy, small on a projector, dark/light
   behavior.
4. Anything that fails a degradation test goes back into a bounded fix loop within the
   frozen direction; it does not reopen the phase-3 gate.

**Deliverables.** Mockup page per application, the definitive lockup set, presented on a
gate page for annotation.

**Gate.** The per-carrier go/no-go gate from `references/applications_stresstest.md` Step 5
closes this phase: every carrier gets its own recorded go or no-go (batched at most 4
questions per AskUserQuestion call). Phase 5 may only migrate a carrier that has its own
recorded go.

### Phase 5 · Delivery & migration · Gate: go-live per carrier

**Read first**: `references/applications_stresstest.md` (go/no-go checklist) and
`assets/guidelines_template.html`.

**Purpose.** Pentagram's final phase hands over guidelines, electronic logo art, templates,
and a launch timing plan. Same here, plus the brain-knowledge updates that make the new
identity the default for every future session.

**Steps.**
1. **Asset export**: SVG plus PNG in all standard sizes plus favicon/ICO, written to a NEW
   dated version folder under the brand-assets directory (convention: `v{N}-{yymmdd}/`).
   Never overwrite or delete the current version folder; the old identity must stay
   restorable (see Operating rules).
2. **Guidelines**: build the brand-guidelines page from `assets/guidelines_template.html`
   (logo usage, typography, color with tokens, applications, misuse). Then, on user
   approval only, update your optional project knowledge (e.g. a brand file,
   brand-reference page, or design-assets skill, if you have one) so the new identity
   becomes the working default.
3. **Migration plan**: an ordered replacement list (site, LinkedIn, templates, decks,
   quotes) with a go/no-go per carrier. Include a launch-timing note: which carriers
   switch together, which can trail.

**Deliverables.** Version folder with assets, guidelines page, updated brain knowledge,
migration checklist.

**Gate.** Execute migration per carrier against the recorded go-list from the Phase 4 gate;
do not re-ask the 9 questions. Re-ask only a carrier whose status changed since that gate
(a failed degradation fix, a scope change, new information). Nothing deploys, posts, or
ships to a client without a recorded go. Log the final acceptance.

## Taste recovery and taste gates

Concept rigor (kill-criteria, one-paragraph arguments) belongs at concept gates. Design
gates also run on taste, and taste can stall: when the client rejects rounds repeatedly
("not yet", "ugly"), the fix is upstream, not more variants. In a real run, four failed
design rounds were recovered in a single round with this protocol.

- **Three taste-directive questions** (via AskUserQuestion), asked the moment a
  second consecutive round is rejected:
  1. "What put you off in the last round?" Options: "damage" / "too much explanation" /
     "too harsh" / "just not beautiful".
  2. "Which earlier artifacts did strike a chord?" Name concrete candidates as options,
     including rounds from BEFORE the current concept. In the run, the client named the
     very first exploration ("the planet with the cutout") and a recolored wordmark,
     which killed the active concept lineage entirely.
  3. "Should the mark carry the story, or may it simply fit?" Options: "simply fit" /
     "visible story" / "in between".
- **Lineage kills, not variant kills.** A gate answer like "start over, go back to
  before you proposed X" kills a whole concept LINEAGE (the concept and all its
  descendants), not one variant. Record the kill at that level.
- **Kills keep artifacts.** Never delete killed work; the client's favorites can resurrect
  "dead" work under a new reading. In the run, the winning mark came from the same
  negative-space family as an earlier killed concept.
- **Light rationales when the client asks for taste.** Full concept notes at a taste
  gate are concept theater with a cost: when the question on the table is "beautiful", give
  each candidate a one-line rationale instead. Meaning may legitimately land on
  "in between", a light reference, if the client explicitly chooses that.
- **Calibration rounds.** Per surviving lane, offer 3 calibrations of ONE variable each
  (e.g. hole size, ring angle, phase depth). Clients choose confidently between
  calibrations where they stall on concepts; in the run, two calibration rounds went from
  three surviving lanes to one chosen mark. Calibration rounds count toward the phase-3
  round bound.

## Phase 3 integration: the logo-generator as form engine

When installed, the `logo-generator` skill (github.com/op7418/logo-generator-skill) is
CALLED, never edited (it tracks github upstream); without it, generate the SVG variants
directly under the same contract. The integration contract:

- **Input**: instead of its loose "name, industry, concept, style" intake, hand it a
  steering block distilled from the approved brief and the chosen concept: the carrying
  idea sentence, personality slider positions, equity inventory (what must survive), form
  language of the chosen territory, hard constraints (16px legibility, single-color
  version, works on the brand's dark and light surfaces).
- **Scope**: 6 to 8 variants WITHIN the chosen concept. If its output drifts outside the
  concept, cut those variants before presenting; the brief is the filter, per principle 3.
- **Output routing**: its SVG variants and showcase HTML land in the current
  engagement folder (`<engagement-map>/{yymmdd}-{slug}/`), and final exports go through
  the Phase 5 version folder, never into the skill's own directory or the existing
  brand-style assets.
- **Gemini showcases**: its `generate_showcase.py` calls the Gemini image API, which is
  billed per image. Run it only when the user explicitly asks for showcase or presentation
  imagery, and say beforehand that it costs money. Never run `--all-styles` speculatively.

## Operating rules

- **Questions**: all interactive questions go through AskUserQuestion, maximum 4 questions
  per call, 2 to 4 options each, in the client's language, and the user can always answer
  free-form via Other. Never dump the question bank as a wall of text. One round of
  questions per turn, with a short reflection between rounds.
- **Verbatim answers**: record the user's answers verbatim in the brief (quoted, marked as
  such), then interpret next to the quote. The user's own words are evidence; your
  paraphrase is analysis. When the two diverge later, the quote wins.
- **One decision-owner**: Pentagram routes all feedback through a single internal point
  person to keep rounds bounded. For MR that is its founder; for a client engagement, ask in
  Phase 0 round 1 who owns the decisions, and accept gate choices only from that person's
  consolidated feedback.
- **Bounded rounds**: two revision rounds on the brief, three refinement rounds on design,
  as hard limits announced up front. Going past a limit requires reopening the previous
  gate, not another tweak.
- **Never overwrite brand assets**: every export lands in a new dated version folder under
  the brand style directory (`v{N}-{yymmdd}/`). Existing folders, PNGs, and templates are
  read-only for this skill. The same applies to client brand assets.
- **Decisions are logged**: every gate outcome goes into the engagement's decision log
  (a decision-documentation skill or a plain decisions file), with alternatives considered
  and the argument for the choice. This is what prevents relitigating a settled gate three
  sessions later.
- **Language**: Run all client-facing output in the client's language: gate questions,
  discovery questions, brief and guidelines text. The question bank and templates are
  written in English; translate them on the fly when the client works in another language
  (the worked example ran in Dutch).
- **Gemini image generation only on explicit request** (see integration contract above).
- **No em-dashes** in any output, prose or HTML; use a comma or colon.

## Output locations

- **Working pages** (briefs, audits, territories, concepts, explorations, mockups,
  guidelines drafts): the engagement folder in your workspace
  (`<engagement-map>/{yymmdd}-{slug}/`), opened on the local review surface (the HTML in
  the browser).
  **One directory for the whole engagement**, e.g. `<engagement-map>/260831-rebrand-mr/`,
  named on day one and reused across sessions; this section is authoritative, so where a
  reference file names its own folder pattern, this run folder wins. Per-phase separation
  comes from filename prefixes (`{YYMMDD}_{phase}_...`), never from separate directories:
  that is what lets a later session find every gate page in one place.
- **Brief**: generated from `assets/brief_template.html`, with an `.md` sibling (same stem)
  as the LLM-portable copy per the take-it-with-you rule.
- **Guidelines**: generated from `assets/guidelines_template.html`.
- **Final assets**: the new dated version folder under the brand-assets directory
  (`v{N}-{yymmdd}/`); for a client, their own brand folder in the agreed project tree.
- **Client deliverables** follow the document-output rules (the client's language, PDF for
  external sharing).

## Running a partial engagement

Phase 0 + 1 alone is a valid, sellable engagement: a signed creative brief plus an audit and
landscape map is exactly what Pentagram's Phase 1 delivers as a standalone confirmed
milestone, and it is often what a client needs to decide whether a full rebrand is worth
it. Other valid cuts: Phase 0 through 2 (strategy and concept, design later or elsewhere),
or Phase 3 through 5 on top of an existing brief (verify the brief meets the Phase 0 bar
first: carrying idea, equity inventory, evolution/revolution decision; if not, run a
compressed Phase 0 to fill the gaps). Every partial run still ends at its phase gate with a
logged decision, so a later session can pick up exactly where it stopped.
