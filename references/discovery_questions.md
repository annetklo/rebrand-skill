# Discovery question bank (Phase 0)

The question protocol for `/rebrand` Phase 0. The output of this phase is a creative brief that every later phase obeys. Never show form (sketches, fonts, colors) before the brief is approved at the gate.

## Method

- **Pose questions in the client's language.** The bank below is written in English; translate questions and options on the fly when the client works in another language (the worked example, the Mission Relearn run, was conducted in Dutch).
- **Four rounds, every question through AskUserQuestion.** Each round's core call carries the 4 core questions of that round (the tool maximum), each with 2 to 4 concrete options. The user can always answer free-form via "Other". Round 2 takes three AskUserQuestion calls: the core call (2.1 to 2.4), a second call with sliders S1 to S4, and a third call with sliders S5 to S7 plus question 2.5 as its fourth question (4 questions, within the tool maximum). Question 2.6 opens the next turn's call or joins a supplementary call. Nothing is ever delivered as a list in chat.
- **Options are calibrated, questions are canonical.** The question text below is posed verbatim (in the client's language). The suggested options are written for the Mission Relearn run (the worked example throughout this skill); when running for any client engagement, rewrite the options from the client's context, keep the question unchanged.
- **Question budget: 20 to 28 total.** 16 core questions plus selected follow-ups from the supplementary pool. The budget is this skill's own: four rounds of 4 core questions keeps a discovery session under an hour, and the supplementary pool exists so no single round ever exceeds the AskUserQuestion maximum of 4. Pick supplementary questions that the core answers left open, do not ask the whole bank.
- **Follow-up rule.** When an answer consists only of category-generic adjectives ("modern", "clean", "professional", "fresh") or contradicts an earlier answer, ask ONE targeted follow-up in chat before the next round. Use scenario framing, not "can you elaborate": e.g. "Name one brand that does this well for you, and what exactly you see there." Scenario questions beat adjective lists (standing intake practice).
- **Record verbatim.** Every answer goes literally into a working log in the engagement folder in your workspace, e.g. `"<engagement-folder>/discovery_log.md"`, with quotes marked as quotes. The brief later cites these; interpretation and quote must stay distinguishable.
- **Synthesize only after round 4.** No proposals, no "so what you're really saying is...", no sketches between rounds. Sequencing follows the HolaBrief rule: audience and problem first, personality in the middle, concrete design preferences last. If the user opens with "I want a sleeker logo", park it: "Good, that comes in round 3. First the why."

---

## Round 1: Ambition & scope

The most important round. The evolution-versus-revolution answer sets the risk budget for the whole project.

### Core (one AskUserQuestion call)

**1.1 What is the real reason you want to work on this brand right now? What happened or changed?**
Why: The trigger question. Separates a genuine strategic problem from brand fatigue; every scope decision downstream hangs on this answer.
Options:
- "The brand no longer fits what we do now or where we are headed"
- "A new audience or market the current brand does not speak to"
- "I have simply grown tired of it, it feels dated"
- "External trigger: pivot, new proposition, partnership, legal"

**1.2 How much of the current brand should a returning client still recognize afterwards?**
Why: Evolution versus revolution as a slider, not a binary (Helms Workshop / dansalva). A refresh keeps strategy and name, touches only the visual layer (phase 3 to 5) and carries far lower equity risk; a rebrand puts story and possibly name on the table and adds strategy, architecture, and possibly naming (phase 0 to 5), roughly doubling to tripling the session count of this very skill.
Options:
- "Refresh: same mark and name, everything tighter and more consistent"
- "Evolution: the mark may change, but the DNA stays instantly recognizable"
- "Revolution: everything is on the table, including the mark"
- "Not sure yet, let the exploration decide"

**1.3 Which of your names or brands should a client see first, and which may disappear behind another?**
Why: Brand architecture (Aaker's Brand Relationship Spectrum: branded house, sub-brands, endorsed, house of brands). Architecture is a capital-allocation decision; best practice is the fewest brands that meet the business goals. MR run: this is the question whether Mission Relearn, a sister product, or the Academy leads.
Options:
- "One brand, everything under it (branded house)"
- "Main brand with sub-brands that may have a face of their own"
- "Separate brands that do not need each other (house of brands)"
- "I don't know, this is exactly the question I want answered"

**1.4 What absolutely must not be lost? Which element would an existing client miss if it were gone?**
Why: The equity-preservation list. Becomes a hard constraint for phase 2 and 3; anything named here survives every concept. MR run: existing clients and an education consortium know the rocket, this is where that surfaces.
Options:
- "The name"
- "The color"
- "The mark or symbol"
- "Nothing is sacred"

### Supplementary (ask in chat when relevant)

**1.5 What is wrong with your current brand identity? Be specific: what grates, and where do you see it?**
Why: HolaBrief's defect question. Turns vague dissatisfaction into a fixable list; "it feels old" is not actionable, "the logo disappears on a projector screen" is.

**1.6 Sort your current brand elements into three buckets: what stays, what changes, what deserves exploration?**
Why: Column Five's three-bucket sort. The result is literally the scope statement of the brief and pre-answers half of round 3 and 4.

**1.7 Are you solving a strategic problem here, or are you mostly tired of your own brand? Honest answer.**
Why: The honesty gate from the refresh-versus-rebrand literature. Fatigue alone argues for a refresh; only a strategy gap justifies revolution money and risk.

**1.8 Where is this brand three years from now? What will you be doing then that you are not doing today?**
Why: Design for the destination, not the current state. A mark chosen for today's offering is outdated at launch.

**1.9 Who has a say in the final result, and who only needs to be kept informed?**
Why: Stakeholder map. Rebrands fail on internal perception gaps (Substance151, Phase3); for a solo founder the "stakeholders" are founder plus 2 or 3 clients plus the public evidence (site, LinkedIn, proposals).

**1.10 Is there a deadline or event attached (launch, event, campaign, new site)?**
Why: Sets pace and decides whether phases can spread over multiple sessions or must compress.

**1.11 Where does the brand live physically versus digitally, and is there budget for more than digital assets (print, signage, merchandise)?**
Why: Scopes the phase 4 mockup set and phase 5 deliverables before anyone falls in love with a letterpress-only idea.

---

## Round 2: Positioning & personality

### Core (first AskUserQuestion call)

**2.1 Who does this brand need to convince? Describe the one or two people (role, situation) the brand exists for first and foremost.**
Why: The ideal-customer question, first in every studied questionnaire. Everything visual is later judged through this person's eyes, not the founder's.
Options (MR run):
- "Decision-makers in government and the public sector"
- "Education and EdTech organizations"
- "Founders and professionals who want to learn to use AI"
- "A mix, with one primary group (I'll name it under Other)"

**2.2 Who is this brand explicitly NOT for?**
Why: In standing intake practice this single question surfaces more positioning than any standard target-audience question. The not-list is a harder constraint than the wish-list.
Options:
- "Private individuals and consumers"
- "Organizations that buy on price alone"
- "Tech people who can already do it themselves"
- "Exclude no one, really (note: that is a finding in itself)"

**2.3 What should someone feel in the first three seconds with this brand, and what should they never feel?**
Why: Desired customer feeling plus its negative twin, the "one thing you never want a customer to feel" (standing intake practice). The never-feeling is the emotional guardrail that survives every design round.
Options:
- "Trust: this is in good hands / never: risk"
- "Energy: something new is happening here / never: dullness"
- "Calm: finally someone who makes it understandable / never: overwhelm"
- "Ambition: this lifts us higher / never: preachiness"

**2.4 Complete this sentence: we are the only ___ that ___.**
Why: Neumeier's onliness test (Zag), the sharpest single positioning question found. His rule: if it cannot be filled in briefly, positioning work precedes design work. A failed answer here is a scope signal, not a detail.
Options:
- "I can fill it in right away (I'll type it under Other)"
- "I have a rough version, help me sharpen it"
- "I can't do it, and I want to solve that first"

### Personality sliders (two AskUserQuestion calls: S1 to S4 in the second call; S5 to S7 plus question 2.5 in the third)

Semantic differentials (Miro / Learning Loop / nineblaess mechanic). No midpoint option on purpose: the tool forces a lean, "exactly in the middle" goes via Other and is itself worth a follow-up. Ask each as one question:

**"Where should the brand sit: [left] versus [right]?"**

| # | Left | Right |
|---|---|---|
| S1 | Playful | Authoritative |
| S2 | Warm | Technical |
| S3 | Pioneering | Trustworthy |
| S4 | Accessible | Exclusive |
| S5 | Outspoken | Understated |
| S6 | Minimalist | Richly detailed |
| S7 | Unconventional | Mainstream |

Options per slider (fill in the pair):
- "Strongly [left]"
- "Leaning [left]"
- "Leaning [right]"
- "Strongly [right]"

Why (whole block): 5 to 8 sliders is the practical band; more waters the personality down, fewer makes it monotone (nineblaess). The positions become guardrails for every later tone and visual decision.

**2.5 On which of these sliders does your current brand sit somewhere other than where you just placed it?**
Why: The today-versus-desired gap on the same slider IS the design brief (workshop practice upgrade). A slider with no gap needs no design change. Delivery: the fourth question of the third AskUserQuestion call, after S5 to S7.
Options:
- "On most sliders: the brand now sits far from where it needs to be"
- "On two or three sliders (I'll type which ones under Other)"
- "On exactly one slider (I'll type which one under Other)"
- "Nowhere: current and desired coincide"

**2.6 And where does your most important competitor sit on these sliders?**
Why: Differentiation check. If the desired position coincides with the main competitor's position, the positioning is a me-too and phase 1 must find open space. Delivery: via AskUserQuestion in the call that opens the next turn, or bundled into a supplementary call; never as loose chat.
Options:
- "Largely in the same places as my desired position (note: me-too signal)"
- "The same on some sliders, clearly different on others (I'll type which under Other)"
- "Somewhere else almost everywhere"
- "No idea where the competitor sits (phase 1 will find out)"

### Supplementary

**2.7 If your brand walked into a room as a person, how would the people present describe that person in the first thirty seconds?**
Why: The scene question, standing intake practice. Personality via a concrete scenario beats any adjective list and produces quotable brief language.

**2.8 Name a brand outside your own sector that you admire, and name exactly what draws you to it.**
Why: The "outside your industry" clause prevents copycat answers, the "exactly what" clause forces transferable qualities instead of "just beautiful".

**2.9 Which brands or visual styles put you off, and why?**
Why: The negative twin (ManyRequests pairs every preference with an avoid-question). Anti-references are the cheapest way to kill wrong directions before they get drawn.

**2.10 Who are your three closest competitors, and what is your essential difference with each?**
Why: Feeds the phase 1 landscape scan and names candidate axes for the 2x2 map ("where does everyone sit, where is the open space").

**2.11 Tell the origin story in five sentences. Which element from it deserves a place in the brand?**
Why: HolaBrief's origin-story question. Origin details often carry the one idea phase 2 needs; the founder rarely sees which detail is the valuable one.

**2.12 Which five words describe this company, and which five words must never be associated with it?**
Why: The classic five-words plus its negative twin. Becomes the vocabulary guardrail in the brief's do's and don'ts.

---

## Round 3: The mark

### Core (one AskUserQuestion call)

**3.1 What does your current mark mean to you, and does that story still hold?**
Why: Decides whether phase 2 keeps the metaphor, shifts its accent, or replaces it. MR run: "What does the rocket mean to you, is 'launch' still the story now that clients launched long ago?"
Options:
- "The story still holds, the form is the problem"
- "The story half holds, the accent needs to shift"
- "The story no longer holds"
- "There never really was a story"

**3.2 What kind of mark fits how you use the brand?**
Why: Narrows the form engine's search space in phase 3 (pattern families: geometric, dot matrix, line systems, mixed; via the logo-generator skill, github.com/op7418/logo-generator-skill, if installed, else generate SVG variants directly) before any variant is drawn.
Options:
- "Abstract geometric mark"
- "Monogram or lettermark"
- "Stay figurative: a recognizable object"
- "No separate mark, wordmark only"

**3.3 Does the mark need to work apart from the name: favicon at 16 pixels, avatar, stamp, app icon?**
Why: The hardest technical constraint in the project. A solo-mark requirement kills detailed and figurative candidates early; better to know before phase 3 than in the phase 4 stress test.
Options:
- "Yes, the mark must work solo everywhere"
- "Mostly together with the name, solo is a bonus"
- "No, the wordmark is the brand"
- "I don't know, let the stress test decide"

**3.4 Which of the shown exploration directions strikes a chord with you, and what exactly does it strike?**
Why: Converts a gut response into a named direction; the "what exactly" clause blocks choosing on prettiness alone. Only ask when an exploration page exists; build the options from that page's actual direction titles (max 4, rest via Other). MR run: the 8 directions on the exploration page in the engagement folder (`<engagement-folder>/`).
Options: generate per run from the exploration page, plus:
- "No direction strikes anything (also an answer)"

### Supplementary

**3.5 Where does your eye go in your current logo, and is that the right element?**
Why: Locates where the equity actually sits inside the mark. Often it is a detail (a curve, a counter, an angle), not the whole figure; that detail is what evolution must carry over.

**3.6 Should the mark explain something (what you do) or evoke something (how it feels)?**
Why: Literal versus evocative splits the phase 2 territories cleanly and prevents the "could we add a little book next to the lightbulb" school of feedback later.

**3.7 Name two logos by others that you find technically impressive (not pretty, but well made), and why.**
Why: Reveals craft preferences (negative space, grid construction, custom letterforms) that steer phase 3 execution quality.

**3.8 Does the mark need to move: loading animation, video intro, animated avatar? Or is it always static?**
Why: A motion requirement changes geometry choices (a mark that rotates, draws itself, or loops needs rotational or path logic from day one).

**3.9 Black-and-white test: when the mark sits in one color on a photocopy, what must still hold up?**
Why: Forces shape-first thinking; color is not allowed to rescue a weak silhouette. This becomes a pass/fail criterion in the phase 4 degradation test.

**3.10 Are there shapes or symbols you want to avoid: sector clichés, wrong associations, cultural baggage?**
Why: The exclusion list for the form engine. Cross-check against the category tropes the phase 1 landscape scan finds ("what repeats across the category", Column Five).

**3.11 Which earlier designs or explorations (including rejected ones) did strike something, and what exactly?**
Why: Taste recovery. When a client rejects round after round ("not quite", "ugly"), the fix is upstream, not more variants: the earlier artifacts the client names, including rounds from killed concepts, point straight back to the working direction. Record kills as lineage kills but keep the artifacts; a client favorite can resurrect a "dead" family under a new reading.

---

## Round 4: Wordmark & system

### Core (one AskUserQuestion call)

**4.1 How should the name be written: capitals, lowercase, one word, or with an accent on part of the name?**
Why: Casing and internal accent are the wordmark's biggest identity levers and must be decided before any font is shortlisted. MR run: "Mission Relearn: two words, lowercase, 'Re' accent?"
Options:
- "All lowercase"
- "Initial capitals"
- "One word, joined"
- "Part of the name gets a visual accent"

**4.2 What font feel fits the brand?**
Why: Narrows the phase 3 font shortlist to one family direction before the license check, so nobody falls in love with an unaffordable candidate.
Options:
- "Geometric and constructed: tight, technical"
- "Humanist and warm: open, human"
- "Classic with a modern cut"
- "Neutral font plus one unconventional custom intervention in a letter"

**4.3 Is your core color sacred, and what may the palette gain?**
Why: Fixes or frees the anchor of the entire color system (phase 3 builds neutrals, support tints, dark-mode behavior and WCAG checks around this answer). MR run: "Is coral #F36E59 sacred?"
Options:
- "Sacred: exactly this value stays"
- "The color family stays, the exact shade may shift"
- "Color is completely open"
- "I don't know: show me options in phase 3"

**4.4 What are the five places where the brand lives most often? Rank them by importance.**
Why: The channels-and-deliverables question that closes every studied intake. The top 5 defines the phase 4 mockup set verbatim and weights every trade-off (screen versus print, 16 pixels versus billboard).
Options (MR run, pick the most important, the rest via Other):
- "Website and LinkedIn"
- "Quotes and proposals (PDF and Word)"
- "Slide decks and workshops"
- "Email and newsletter"

### Supplementary

**4.5 Which colors absolutely must NOT be in the palette?**
Why: The negative twin of 4.3 (ManyRequests). Also catches competitor-owned colors that the phase 1 landscape scan identifies.

**4.6 Does the brand need to work in two languages and registers: Dutch and English, formal government document and casual founder post?**
Why: Bilingual range and register spread affect tone-of-voice rules and sometimes lockups (long/short name variants). MR runs Dutch for clients and English for product.

**4.7 Dark on light, light on dark, or both as full citizens? Where does dark mode really live for you?**
Why: Dark-mode behavior is a phase 3 design input with its own WCAG contrast checks, not a phase 5 afterthought.

**4.8 How much system do you want: one logo with rules, or a full visual language (patterns, iconography, photography style, motion)?**
Why: Scopes phase 4 and 5. A solo founder often only needs the core kit; overscoping here is where 3-session projects become 10-session projects.

**4.9 Who will work with this brand day to day, and in which tools: Word, Canva, Figma, code?**
Why: Guidelines must match the real toolchain; determines which asset formats phase 5 exports (an SVG-only delivery fails a Word-based practice).

**4.10 May a font license cost money, and up to how much?**
Why: The license budget, asked before shortlisting (plan risk: a wordmark font can require a purchase; Google-Fonts-only is a genuine constraint for HTML and template work).

---

## Synthesis: from log to creative brief

Do this only after all four rounds are complete and logged.

1. **Re-read the verbatim log in one pass.** Mark literal quotes that deserve to appear in the brief as quotes. The founder's own phrasing ("finally someone who makes it understandable") is brief gold; do not paraphrase it away.
2. **Every claim in the brief traces to an answer.** No claim without a source line from the log. If you find yourself writing something nobody said, it belongs under "Open questions", not in the body.
3. **Slider gaps become design instructions.** For each slider where current position and desired position differ (question 2.5), write one sentence: "The brand must move from [current] to [desired]; for form/color/language that means: ...". Sliders without a gap get one line: "keep as is".
4. **Contradictions are findings, not noise.** List every unresolved contradiction explicitly under "Open questions & risks". Never smooth them over in the prose; a brief that reads consistent but hides a conflict will explode at the phase 3 gate.
5. **Write the brief as an HTML gate page plus an `.md` sibling** in the engagement folder, open the gate page as a local review surface (the HTML in the browser), and hold at the gate: phase 1 does not start until the brief is explicitly approved. Log the scope decision (evolution versus revolution, plus what is sacred) in your decision log.

### Creative brief: section list

1. **Trigger & scope decision**: the trigger (1.1), the recognition slider verdict (1.2), the three-bucket sort (1.6)
2. **Brand architecture**: which name leads, which follows (1.3)
3. **Audience & non-audience**: 2.1 and 2.2, as two lists
4. **Positioning**: the onliness statement (2.4), competitors and the essential difference (2.10), candidate 2x2 axes for phase 1
5. **Personality**: the 7 slider positions (desired, current, competitor) plus the gap sentences; the five words and the five forbidden words (2.12)
6. **Feeling target**: the 3-second feeling and the never-feeling (2.3)
7. **Equity: what stays**: the never-lose list (1.4), the element where the eye lands (3.5)
8. **Mark constraints**: metaphor verdict (3.1), mark type (3.2), solo requirement (3.3), exclusion shapes (3.10), motion (3.8)
9. **Wordmark & color constraints**: casing and accent (4.1), font feel (4.2), license budget (4.10), color sacred or free (4.3), forbidden colors (4.5), dark-mode requirement (4.7)
10. **Application top 5 & system scope**: 4.4 ranked, 4.8 scope, 4.9 toolchain
11. **Do's & don'ts**: one page distilling all negative twins and guardrails into checkable rules
12. **Open questions & risks**: unresolved contradictions, failed onliness, anything parked

Appendix: the verbatim discovery log.

## Red flags: stop and re-ask

Any of these means: do not synthesize, go back with a targeted re-ask.

1. **Contradiction across rounds.** Example: "revolution" chosen in 1.2 while 1.4 declares mark, name and color all sacred; or sliders say "trustworthy and understated" while every admired brand in 2.8 is wild and loud. Name the contradiction out loud and let the user pick which answer stands.
2. **Everything is important.** Every element lands in the "stays" bucket, all five applications are "equally important", every slider is "strongly both, really". A constraint set without slack cannot be designed against. Force ranking: "If you may keep only one, which one?"
3. **The onliness test fails and stays failed.** After one follow-up there is still no "we are the only ___ that ___". Per Neumeier: positioning work precedes design work. Pause the skill, recommend a positioning session first (for internal runs: `/office-hours`), and say so explicitly instead of designing on quicksand.
4. **Taste instead of strategy.** Rationales are all "I just like this" with no link back to the audience (2.1) or the feeling target (2.3). Re-ask through the audience's eyes: "What does [the decision-maker from 2.1] see in this, for three seconds?"
5. **Fatigue paired with revolution.** 1.1 says "I have grown tired of it" while 1.2 says "revolution". Intervention size exceeds problem size. Re-ask 1.2 with the cost framing: a refresh protects existing equity and runs only phase 3 to 5, while a rebrand adds phase 0 to 2 and roughly doubles to triples the session count of this skill; what does the bigger knife buy that the smaller one does not?
