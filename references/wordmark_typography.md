# Wordmark and typography: the phase 3 wordmark track

This reference drives the wordmark track of Phase 3 (Design exploration). It runs parallel to the symbol track (the logo-generator skill, github.com/op7418/logo-generator-skill, if installed; otherwise generate SVG variants directly) and feeds the same gate. The input is the creative brief (phase 0) and the chosen concept (phase 2); the output is a set of **designed wordmark treatments** on a gate page (a local HTML review surface): real fonts, license-checked, and a mandatory exploration of custom letterform interventions (section 8), never just typed candidates.

Ground rules for this track:

1. **Real fonts only at the gate.** Never approximate a candidate with a lookalike or a fallback stack in the final gate page. Download the actual files (see 1.3) or drop the candidate.
2. **License check before falling in love** (section 2). No candidate reaches the gate page without a verified license line.
3. **Never overwrite existing brand assets.** Everything lands in the new version folder inside the engagement folder in your workspace, e.g. `<engagement-folder>/v2-<date>/fonts/`. The client's current brand font files (in the worked example: the Cal Sans and Open Sans files in the Mission Relearn brand-assets folder) stay untouched.
4. All page labels and questions shown to the client are in the client's language (the worked example ran in Dutch); work notes are in English.

---

## 0. Guiding principle: a wordmark is a designed object, not a typeset line

A typed line with a color accent never passes a gate on its own. In a study of 9,563 brand wordmarks (Made Good Designs, brand typography study), roughly 98% use bespoke or modified lettering rather than an unmodified downloadable font. What looks like a typed face at Pentagram, Landor, or Chermayeff & Geismar & Haviv is almost always a one-off drawing: letterforms re-weighted, re-spaced, cut, joined, or redrawn, then trademarked as artwork. "Type the name in a good font" is the exception at that level, not the norm.

Consequences for this track:

- Font selection (section 1) is the **starting material**, not the deliverable. The deliverable is drawn artwork derived from that material.
- The position that needs defending at the gate is "unmodified type", not the intervention. Plain type is only defensible with an explicit Mastercard-style argument: the symbol is so strong that it carries the identity alone, and the wordmark's job is quiet fit (Pentagram set Mastercard in FF Mark unmodified, and that works only because the interlocking circles are world-famous). Write that argument out or do the surgery.
- Every gate page therefore carries the exploration protocol of section 8: rendered custom treatments, presented as designed objects, at equal fidelity.

---

## 1. Selecting candidates

Pick 3-4 candidates maximum, derived from the phase 2 concept note (its form-language line names the genre: geometric, humanist, grotesque, serif, or a hybrid). Do not shortlist from a generic "beautiful fonts" list; every candidate must be arguable from the concept in one sentence. Remember the guiding principle: a candidate is a block of marble, and these criteria test whether the marble is worth carving.

Every test below runs on the **actual name string** in its candidate name rendering (see section 3), not on a pangram. For Mission Relearn that string has two built-in traps:

- `relearn` ends in **rn**, the canonical misread pair: badly spaced it reads "releam". This alone disqualifies fonts where r's arm reaches toward the next letter.
- `mission` carries **ss** plus an **i-s-s-i** run: a strong repeating beat that exposes uneven rhythm instantly.

### 1.1 The eight criteria, each with its test

1. **Distinctiveness of the set string.** A wordmark carries the whole identity, so the raw typesetting must already be recognizable. Test: render "mission relearn" at ~200px in the candidate and in three neighbors from the same genre (for a geometric candidate: Futura, Poppins, Montserrat). If the candidate is not identifiable in a blind line-up, it needs a stronger custom intervention (section 7) or it is out.
2. **Small-size survival.** Test: render a strip at exactly 14px and one at 16px (the favicon-adjacent floor), plus a 25mm-wide print check via a quick PDF. Hairline contrast, tight joins, and elaborate detail die here. The practical floor named in apparel practice is a 3-4 inch chest print; anything that fails 14px on screen fails that too.
3. **Aperture.** Open apertures (a, c, e, s stay open) resist closing up small; closed-aperture geometrics (Futura-likes, including Cal Sans) look striking large but degrade below roughly 16px, a c reads as an o. Test: at 14px, can you still tell c from o and e from a filled loop in the actual string ("mission" has an s-pair, "relearn" has e-a)?
4. **Rhythm on the name's own pairs.** Test: cover the string so only three letters show, slide the window along the word (the triplet check), and judge whether the beat of i-s-s-i-o-n and e-l-e-a-r-n stays even. Uneven counters or a rogue wide glyph show up immediately.
5. **x-height balance.** Taller x-height helps small sizes; very tall reads "UI font", not "brand voice". Test: measure x-height against cap height (draw two guides on the 200px render). Roughly 0.68-0.75 suits a mark that must be both hero and favicon; display faces deliberately go lower for elegance, accept that only if the mark rarely lives small.
6. **Cut and weight range.** The mark must live at 180px and at 14px; one display cut rarely does both. Test: check whether the family ships a text cut or optical-size axis alongside the display cut, or a weight range wide enough to bump one weight up for small use. A single-weight display face (Cal Sans ships Regular only in the brand folder) is a real constraint: note it on the gate page.
7. **Voice fit against the concept.** Test: place the render next to the one-sentence concept from phase 2 and next to the slider results from phase 0 round 2 (playful vs authoritative, warm vs technical). Name the mismatch explicitly if there is one ("candidate 3 is more technical than the brief asks for") instead of letting a pretty render pass.
8. **Pairing with the body font.** The wordmark will sit above Open Sans paragraphs (or its successor) on every page. Test: one mock card with the wordmark at 32px over a real Open Sans paragraph. The pairing needs clear contrast (different skeleton or clearly different weight); a near-miss pairing (two similar humanist sans faces) looks like an error.

### 1.2 Lowercase versus caps interacts with these tests

Lowercase gives a more even word-shape (fewer cap-height spikes) and kerns more smoothly, but strengthens the rn trap. Title Case breaks "Mission Relearn" into two clear units and survives in running text. Run criteria 1-4 on each name rendering still in play, not only on the default.

### 1.3 Getting the real font

- **Local first:** check the client's brand-assets folder in your workspace (in the worked example: CalSans-Regular.ttf and the Open Sans set in the Mission Relearn brand fonts folder). Also check `ls ~/Library/Fonts /Library/Fonts | grep -i "<name>"`.
- **Google Fonts:** fetch the css2 stylesheet and pull the file URLs from it: `curl -s -A "Mozilla/5.0" "https://fonts.googleapis.com/css2?family=Family+Name:wght@400;700"` returns woff2 URLs (an old User-Agent string returns ttf). Download into the version folder's `fonts/` subfolder. For surgery you need the **ttf** specifically (opentype.js reads TTF/OTF/WOFF, not woff2): download it from fonts.google.com or the google/fonts GitHub repo.
- **Commercial candidates:** use the foundry's official trial font if one exists. Trial policies differ per foundry and change over time; verify on the foundry's own site during the license fetch (2.1), never assume. If no trial exists and no purchase decision is made, the candidate does not reach the gate: no lookalike stand-ins.
- **Embedding in the gate page:** base64-encode the woff2 (`base64 -i font.woff2`) into a `@font-face` data URI so the gate page renders the real font offline. Set the fallback stack to something deliberately wrong-looking (`font-family:'Candidate3', cursive`) so a failed load is visible instead of silently masked, and verify with `document.fonts.check("32px 'Candidate3'")` or a glance before showing the client the page. Custom treatments (section 8) are frozen SVG paths and need no font at all.

---

## 2. License check, before falling in love

Run this per candidate **before** it goes on the gate page, and record the result in `licenties.md` inside the version folder. A wordmark decision without a license line is not a decision.

### 2.1 What to verify

1. **License type:** OFL (Google Fonts and most open repos) or a commercial EULA.
2. **Does it cover logo use explicitly?** Many commercial desktop EULAs restrict or surcharge logotype/branding use; "desktop license" alone is not enough. Search the EULA for "logo", "trademark", "branding". If unclear, mail the foundry before the gate, not after.
3. **What exactly is licensed:** desktop (design work), web (self-hosted or pageview-tiered), app/embedding, and broadcasting are separate line items at most foundries.
4. **Modification rights:** may you convert to outlines, may you modify the font file itself? Outline conversion rights are load-bearing for this track: the entire surgery pipeline (section 9) starts from outlines.
5. **Source everything live:** fetch the foundry's current EULA and pricing page per candidate (WebFetch or a researcher subagent) and cite that URL plus fetch date in the `licenties.md` line. Verify any trial-font availability in the same fetch. The gate page and `licenties.md` never cite section 2.3 of this file as a source.

### 2.2 OFL in practice (SIL Open Font License)

- Commercial use including logos: allowed, no royalty, no attribution requirement, no seat limits. Embedding, modifying, and converting to outlines: allowed. Outlining an OFL face (Bricolage Grotesque, Cal Sans) into a logo and operating on the paths is permitted.
- Constraints: you cannot sell the font files by themselves, a modified font file must be renamed (Reserved Font Name rule), and you cannot trademark the typeface itself.
- The catch for branding: the font stays available to everyone, so **zero exclusivity**. Distinctiveness must come from spacing and letterform surgery (sections 6-8). The customized mark, converted to outlines, is your own artwork and is trademarkable as a mark even though the source font is OFL. This is exactly why the 98% norm exists: surgery is what turns a shared font into an ownable mark.

### 2.3 Cost expectations (calibration only, never quote on a gate page)

These orders of magnitude exist only so a commercial candidate is not shortlisted naively. Every number that reaches the client comes from the live fetch in 2.1 point 5, cited with the foundry's URL and the fetch date in `licenties.md`, never from this list.

- Desktop: roughly $100-300 per family, single weights $20-60.
- Web: roughly $200-500 per year, or pageview-tiered.
- Separate logo/branding license where required: $500-2,000+.
- Unlimited/enterprise and exclusivity tiers run an order of magnitude higher and are per-foundry, per-negotiation: mail the foundry, do not estimate.
- Premium foundries often sell full families rather than single weights, which is why display faces feel expensive; whether a trial exists is per-foundry, verified during the 2.1 fetch. Budget the license as part of the rebrand decision at the phase 3 gate, not as a surprise in phase 5.

### 2.4 Cal Sans, the current heading font

Whenever Cal Sans is a candidate (continuity option), the gate page states facts about it, so produce those facts by verification at run time. Do not quote this file for anything the local font file cannot prove.

- **License, repo, and origin story: fetch, do not assert.** Locate the official Cal Sans repository with a fresh search (do not trust a remembered URL), then read its OFL text and README (WebFetch or a researcher subagent). The gate page's license line, any designer attribution, and any origin anecdote come from that fetch, cited with URL and date in `licenties.md`. If the README does not name a designer, the gate page names none.
- **Feature inventory: dump it from the local file.** Which character variants or stylistic sets actually exist comes from the file, not from memory: `python3 -c "from fontTools.ttLib import TTFont; f=TTFont('CalSans-Regular.ttf'); print(sorted({r.FeatureTag for r in f['GSUB'].table.FeatureList.FeatureRecord}))"` (fontTools install: see section 4.4; run against the copy in the brand folder, 1.3). Whatever cvXX/ssXX tags that prints are the cheap sources of variation worth testing before drawing anything custom; render each on the name string. If it prints none, say so on the gate page.
- **What the local file proves without any fetch:** one weight only (Regular, criterion 6), extremely tight default spacing tuned for display sizes (add positive letter-spacing small, 4.3), and closed geometric apertures that degrade below ~16px (criterion 3).
- Under OFL: free for logo use, but zero exclusivity: any startup can type its name in it. If Cal Sans stays, the wordmark's distinctiveness must come entirely from spacing plus letterform surgery.
- If the font **file** is ever modified (not just outlines), the OFL Reserved Font Name rule requires renaming it (e.g. "MR Display"), and the renamed file goes in the version folder.

---

## 3. Case and name rendering: the decision tree

Phase 0 round 4 already asked the client's instinct. Phase 3 renders the evidence: show the preferred form plus exactly one counter-proposal per candidate, in the real font, and settle it at the gate. Walk the tree in this order; each question changes what the next one means.

### Q1: One word or two?

| Option | For | Against |
|---|---|---|
| `mission relearn` (two words) | Readable; the name is also just plain language; the word space gives a natural resting point; "Relearn" stays recognizable as a word of its own | Longer overall shape, harder small (a favicon lockup then needs the symbol alone); two words demand a deliberate word-space decision (4.2) |
| `missionrelearn` (run together) | Digital-native, matches the domain missionrelearn.com; one compact shape | 15 characters without a resting point; the n-r transition mid-word creates a new stumbling point; reads as a URL, not a name |
| Stacked (two lines) | Nearly square lockup, strong for avatar and stamp | Not a primary form, only a secondary lockup; never choose it as the sole rendering |

A long two-word name is exactly the case where practice says: the mark needs a monogram or the symbol alone for small placements. That is fine, the symbol track covers it; do not force the full wordmark into a favicon.

### Q2: Case

| Option | For | Against |
|---|---|---|
| `mission relearn` (lowercase) | The dominant rebrand direction of the 2010s-2020s (amazon, intel, xerox, stripe, airbnb, mastercard, adidas went that way); reads approachable, human, digital-native; even word shape that kerns more smoothly | The rn trap in "relearn" gets stronger; less authority, and MR sells to government and education where authority counts; follows the trend instead of standing apart from it |
| `Mission Relearn` (Title Case) | Current form, no recognition loss; survives in running text (the name gets typed daily in emails and quotes); two capitals mark the two words | Two cap peaks break the word shape; kerns more restlessly around the M and R |
| `MISSION RELEARN` (all caps) | Authority, institutional; with generous tracking (4.3) a classic luxury/institution look | Clashes with "warm" from the brief if it points that way; longest form of all; caps-lock tone in a digital context |

Counter-trend note for the gate page: brands asserting authority, heritage, or scale keep caps (finance, law, luxury). Which side MR belongs on is a brief question (round 2 sliders), not a taste question.

### Q3: The Re accent

"Relearn" carries the idea: learning, again. An accent on "Re" makes the mark tell that story.

| Option | For | Against |
|---|---|---|
| No accent | Calm, timeless, needs no explanation | The brand idea stays invisible in the wordmark; distinctiveness must then come entirely from the symbol |
| Color accent (coral "re"/"Re") | Cheap to implement on any medium; coral is already the brand accent | Disappears in one-color applications (black-and-white copy, stamp, embossing); color as the sole carrier of the idea is fragile; **color alone is not a design intervention and never passes the gate as the only treatment (section 0)** |
| Weight accent (bold "re" against a regular rest, or the reverse) | Survives one-color reproduction; subtler than color | Requires a family with a usable weight range (criterion 6); too small a difference reads as a typo |
| Glyph intervention (one letter in "Re" carries the symbol's motif) | The most ownable; couples wordmark and symbol in one gesture; this is section 6's DNA rule in practice | Requires real surgery (section 7) plus the gate tests of section 10; a half-hearted intervention reads as damage |

At the gate, ask via AskUserQuestion (max 4 questions, 2-4 options each), for example: "Which name rendering feels like Mission Relearn?" with the two or three rendered forms as options, and "Should 'Re' carry an accent?" with none / color / weight / glyph as options. The client can always answer free-form via Other.

---

## 4. Optical spacing in five steps

Metric kerning (the font's built-in pairs) is never enough for a logotype: every pair gets judged by eye so **perceived** space is equal, not measured space. Software "optical" kerning is only a starting point.

### 4.1 The five steps

1. **Set the baseline.** Render the string at 200-300px in an HTML workbench (one `<span>` per letter so each gap is individually adjustable via `letter-spacing` in em on the preceding span). Start from the font's metric kerning and the tracking rule of thumb for the chosen case (4.3). For Cal Sans: expect to **add** space, it ships display-tight.
2. **Triplet pass.** Cover all but three letters (two strips of paper on screen, or a CSS mask) and slide along the word. Equalize perceived space using the hierarchy: two straights widest (il, li in "mission"? none here, but ll-type pairs generally), straight-round intermediate, two rounds tightest (oo-type). Treat diagonals (none in this name) and open shapes (r, L, T) as danger pairs: the r in both words donates white space to the right, so r-e and r-n need tightening judged by area, not distance.
3. **Fix the name's traps.** "rn" at the end of relearn: open it slightly wider than the surrounding rhythm suggests, then squint; if it still threatens to read "releam" the candidate needs a glyph fix (section 7) or it is out. The word space in a two-word logotype is itself a design decision: usually tighter than the font's default space, around the width of the n's counter, so the mark reads as one unit without the words colliding.
4. **Error-revealing passes.** Flip the render upside down (kills reading, exposes spacing), blur it (squint test), and view it in negative: white-on-dark reads tighter, so ship the reversed version 0.5-1% looser if it closes up. These three checks are the difference between "looks fine" and proofed.
5. **Freeze and record.** Write the final per-pair values into the workbench HTML and commit that HTML plus the font file to the version folder as the un-outlined source. Then convert to outlines (section 9) for surgery and the deliverable SVG. Both siblings live side by side so the mark can always be re-derived.

**After surgery, kern again.** Any intervention from section 7 changes optical width: a bite out of a right sidebearing leaves a hole, a shear can cause collisions. Re-kern the operated letter's two gaps by optical volume, not by advance width, until the rhythm of white spaces looks even again (micro spacing guidance: logodesign.net on micro vs macro spacing).

### 4.2 Word space

Covered in step 3, repeated because it is always forgotten: never accept the font's default space glyph in a logotype. Tune it as its own pair.

### 4.3 Tracking rules of thumb

| Situation | Tracking |
|---|---|
| lowercase display (>= 48px) | tight: -1% to 0 (Cal Sans: more like 0 to +0.5%, it already ships extremely tight) |
| Title Case display | around 0 |
| ALL CAPS display | +5% to +12%, wider as the size gets smaller |
| Any case below ~20px | add tracking; display-tight spacing clogs up small |
| Reversed (light on dark) | +0.5% to +1% relative to the positive version |

### 4.4 fontTools as alternative outline route

The primary text-to-outline pipeline is section 9 (opentype.js plus paper.js, because surgery needs booleans). fontTools remains a valid freeze-only route when no surgery is planned: open the TTF with `TTFont` (`pip3 install --break-system-packages fonttools`), walk the string through `getBestCmap()`, draw each glyph via `fontTools.pens.svgPathPen.SVGPathPen` against `getGlyphSet()`, and place each path at the running x-advance plus your frozen per-pair adjustments. Two gotchas: font coordinates are y-up while SVG is y-down, so wrap glyph paths in `transform="matrix(s,0,0,-s,x,baseline)"` with `s = target-size / unitsPerEm` (unitsPerEm is typically 1000 or 2048, read it from the head table); and modern fonts keep kerning in GPOS rather than the legacy kern table, which is exactly why the frozen values come from your own workbench, not from the file.

---

## 5. The decision ladder: three routes to a wordmark

Documented studio practice sorts wordmark craft into three routes. Choose the route explicitly, on the gate page, with the reasoning written out. The recurring test behind the choice: **does the concept have to pass through the counters and strokes of the letters, or can it sit next to them?**

### Route A: existing typeface plus one surgical intervention

When an existing face already carries the right voice and the idea needs only a local intervention. Cheapest and fastest; the risk is genericness if the intervention is timid.

- **Citi** (Paula Scher, Pentagram, 1998-99): based on Interstate, but with a modified 't' so the red arc reads as an umbrella handle, and a rounder 'c' replacing Interstate's oblong one. The arc is the idea; the letterforms were altered to receive it (Fonts In Use, "Citibank Identity").
- **V&A** (Alan Fletcher, Pentagram, 1989): Bodoni with half the 'A' amputated; the ampersand's stroke reinstates the missing bar, fusing three characters into one unit. The closest existing precedent for "removal as identity": one letter deliberately loses material and a neighbor completes it (Creative Review, "V&A museum logo").
- **I Love NY** (Milton Glaser, 1977): American Typewriter, stock, but a heart glyph replaces the word "love" as a rebus. The typeface is untouched; the glyph substitution carries everything (MoMA collection; Creative Review).
- **Google** (in-house, 2015): even on top of the custom face Product Sans, the logotype deviates further: heavier strokes and the tilted 'e', kept as a deliberate signal of unconventionality (Google Design, "Evolving the Google Identity").

### Route B: fully custom lettering or a bespoke typeface

Forced when (i) the concept must live inside the letterforms themselves, (ii) the name is the primary visual asset with no strong symbol, or (iii) exclusivity and trademark defensibility matter. This is the norm among major brands (the ~98% in the Made Good Designs study).

- **FedEx** (Lindon Leader, Landor, 1994): neither Univers 67 nor Futura Bold could hold the hidden arrow "without torturing the letterforms", so Leader drew his own letters borrowing from both, engineering the negative-space arrow between E and x. When an idea must live inside the counters, you draw custom letters; you do not force a stock face (Logo Histories, Lindon Leader account).
- **Graphcore** (Pentagram, Hudson-Powell, 2017-18): wordmark drawn from the geometry of a bespoke typeface, Graphcore Quantized, with 65+ alternate glyphs at varying "resolutions". The concept (resolution, computation) is executed inside the letterforms (pentagram.com/work/graphcore; It's Nice That).
- **Airbnb Cereal** (Dalton Maag, 2018): the 'a' and 'b' were drawn so they can be written in one continuous stroke like the Belo symbol itself: mark-DNA deliberately migrated into letterforms (Karri Saarinen, "Working Type", Airbnb Design).
- **Saks Fifth Avenue** (Michael Bierut, Pentagram, 2007): the 1973 Tom Carnase cursive redrawn by type designer Joe Finocchiaro, then cut into a grid of 64 tiles that shuffle into near-infinite compositions. A destructive-looking cut as the system, with classical lettering underneath: the strongest precedent for a "cut" concept executed on finished letterforms (pentagram.com/work/saks-fifth-avenue).
- **Slack** (Pentagram, Bierut, 2019): custom wordmark lettering next to the rebuilt octothorpe, with Larsseit as the brand face; even a "simple" lowercase wordmark at this level is drawn, not typed (Design Week; Dezeen).

### Route C: standard face, selection and fit as the craft

The legitimate "typed" end of the spectrum. Valid only when a strong symbol carries the identity and the wordmark's job is quiet fit.

- **Mastercard** (Pentagram, Bierut/Hayman, 2016): set in FF Mark, lowercase, letterspaced, moved below the symbol. The craft is selection: FF Mark's circular geometry echoes the interlocking circles. This works because the symbol is world-famous (Fonts In Use, "Mastercard identity 2016"; Dezeen).

Route C is never the default for a brand without decades of symbol equity. Choosing it requires the written Mastercard argument from section 0 on the gate page, and it still requires bespoke spacing (section 4) and the fit-argument ("this face's geometry echoes the mark because...") to be demonstrated, not asserted.

---

## 6. The DNA rule: the mark's form language is letterform material

Before any surgery, interrogate the symbol as raw material: list its exact angles, radii, corner language, and cut shapes. Those measurements are the only legitimate source of wordmark interventions. A cut at an arbitrary angle is decoration; a cut at the mark's angle is identity.

The strongest documented wordmarks carry the **same single idea** as their mark, executed at two scales:

- Airbnb Cereal draws 'a' and 'b' with the Belo's one-stroke logic.
- Graphcore's wordmark shares the Quantized typeface's resolution geometry with the whole identity.
- Citi's letterforms were reshaped specifically to receive the arc that absorbed the Travelers umbrella.
- Saks cuts the finished lettering with the same grid that drives the whole system.

**This revises the naive "one break total" reading.** A concept note that reads "the intervention lives only in the symbol, the wordmark gets no second form intervention" mistakes coherence for excess. One idea expressed twice is not two breaks; it is one idea with two intensities: full strength in the mark (the whole bite), one precise echo in the wordmark (one cut, one terminal, one counter). That is the V&A and Google model of restraint: the intervention is singular and disciplined, not absent. A phase 2 concept note that bans the concept's form idea from the wordmark fails review and goes back to phase 2; none of the documented studio practices above support such a ban.

Operational rules:

1. **Sample, never approximate.** The wordmark intervention reuses the mark's exact geometry: same quarter-circle radius (scaled proportionally, e.g. cut radius as a fixed percentage of cap height), same corner rounding, same angle. One radius language across mark and wordmark is what makes it read as one idea instead of two tricks.
2. **DNA regression test.** Overlay the actual mark geometry (the real SVG path, scaled) on the operated letter; radius and angle must match exactly, not approximately. This overlay is a required exhibit on the gate page (section 10).
3. **One echo, not a rash.** The mark carries the idea at full intensity; the wordmark echoes it once, at one surgical site. Repeating the cut across many letters turns an idea into a texture (that is a different, deliberate choice: see stencil cuts and ink traps in section 7, which are systems, not echoes).

---

## 7. The surgery-families catalog

Nine documented families of letterform intervention. Each entry: what it is, when it serves an idea, the SVG execution route (on per-glyph outline paths, section 9), and a legibility guardrail. Pick **one family** as the wordmark's idea; two families in one wordmark reads as damage, not design.

1. **Terminal cut.** Slice a stroke ending at the brand angle. Serves an idea when the mark has a signature angle worth echoing. SVG: subtract a rectangle rotated to that angle across the terminal. Guardrail: the subtlest family, but run the 14px strip after every cut; a sliced terminal that sings at 180px can make an r read as a broken i at 14px.
2. **Angled shear.** Skew one glyph, or slice the whole word along one diagonal and shift the halves. Serves ideas of motion, disruption, perspective. SVG: apply `skewX` to the glyph group, then re-bake the transform into coordinates so it survives booleans. Guardrail: check for collisions with neighbors after the shear and re-kern.
3. **Counter replacement.** A closed letter's counter (o, e, a, R) becomes the brand mark's silhouette. Serves an idea when the mark is compact enough to read at counter scale (reference: Goodwill's lowercase g doubling as the smiling face). SVG: delete the counter subpath (mind `fill-rule`), insert the mark silhouette as the new counter, matched to the font's stroke weight rather than the bounding box. Guardrail: the letter must read as that letter first and the mark second; test by having someone read the 14px strip aloud.
4. **Glyph replacement.** Swap one letter for the symbol or another sign entirely (johnson banks' 2017 Mozilla identity replaced "ill" with "://" to set the name as "moz://a": the swap can span more than one glyph if it reads as one sign). Highest memorability, highest risk. SVG: delete the letter's path, insert the replacement scaled to the surrounding optical weight, re-kern both gaps as new pairs. Guardrail: one replacement maximum, ever; the word must survive the read-aloud test.
5. **Ligatures and joins.** Fuse two adjacent glyphs into one drawn form (the ss in "mission" is a natural candidate). Serves ideas of connection and continuity. SVG: nudge the glyphs until strokes overlap, `unite()` the paths, replace the junction segments with one curve matching the brand radius. Guardrail: never ligate rn in "relearn", a joined rn is literally an m; and any ligature must pass the upside-down and blur tests without turning into a blob.
6. **Notches and bites.** Subtract a concave shape from one strategic glyph. The direct DNA carrier for a removal concept like De Uitsnede: the mark's concave quarter-circle taken out of one letter of "Re". Reference for cuts-through-letters as a system: Pentagram's Cohere identity, a custom typeface where cell-shaped cuts disperse through the characters with a variable axis for cut depth (Creative Boom on Cohere). SVG: `subtract()` the mark's exact cut shape (section 6 rule 1) from the glyph. Guardrail: at weight 800 a cut narrower than ~15% of the stroke fills in optically at small sizes; make cuts wide and confident, and never cut the feature that distinguishes the letter from a neighbor (the e crossbar, the c-versus-o gap, the n-versus-h shoulder).
7. **Stencil cuts.** Break stems with uniform gaps, all at one angle and one width. Reads industrial, serves ideas of construction and modularity. SVG: subtract thin rectangles at the system angle. Guardrail: systematize completely or skip; irregular stencil gaps read as rendering errors.
8. **Ink traps as style.** Exaggerated wedges subtracted where strokes join; originally a print fix for small sizes, turned into a display aesthetic by Dinamo's Whyte Inktrap (with a variable axis from absent to pronounced). Serves ideas of precision and process-made-visible. SVG: subtract small wedges at every stem/curve junction, identical proportion everywhere. Guardrail: for a digital-first brand this is an aesthetic signal, not a functional one; use it as a full system or not at all.
9. **Baseline shift or rotation of one glyph.** Translate or rotate a single glyph a few percent (Google's tilted 'e' is the canonical restrained example). Serves ideas of play and unconventionality. SVG: transform the glyph group, re-bake, re-kern its neighbors. Guardrail: exactly one letter, a few percent at most; two moved letters read as broken typesetting.

Universal optical rules across all families:

- **Legibility floor:** keep roughly two thirds of a glyph's silhouette intact; a cut deeper than the stroke width breaks the letter skeleton.
- **Position:** a modified letter mid-word survives because the rest of the word carries it; the first letter is the riskiest surgical site. For "Mission Relearn" the R or e of "Re" is mid-logo and concept-flagged: a good site.
- **Blacklist**, documented as tired by working designers: the crossbar-less A, the swoosh under the name, the generic circle around the first letter, and arrow-hidden-in-letter FedEx copies. None of these reach a gate page.
- The bar remains Leader's FedEx standard: the team explored roughly 200 concepts, and most viewers never consciously see the arrow. Subtle beats clever.

---

## 8. Mandatory wordmark-exploration protocol

The wordmark track mirrors the symbol exploration: breadth first, then a gate. Typing candidates in fonts is phase 3 step zero, not the exploration.

1. **Minimum 6 distinct custom treatments**, drawn from **at least 3 different surgery families** (section 7), executed on the leading font candidate(s). Fewer than 6 rendered treatments means the exploration did not happen.
2. **Equal fidelity.** Every treatment is real frozen SVG (section 9 route A), rendered at the same sizes on the same grounds, on **one gate page**. No treatment is presented as a sketch next to finished neighbors; unequal fidelity rigs the gate.
3. **One-line rationale per treatment**, in the client's language, naming its surgery family and how it carries the concept idea, e.g. "Treatment 3 (bite): the symbol's quarter circle, at exactly the same radius, taken out of the shoulder of the R; the brand idea 'remove first' lives in the name as well."
4. **At least one treatment applies the DNA rule literally** (section 6): the mark's exact geometry sampled into a letterform.
5. **The plain-type control.** One unmodified typeset version may appear on the page as control and as the Route C position, carrying its written Mastercard argument (section 5). It competes on the same tests; it does not win by default.
6. Every treatment passes the section 10 gate tests **before** the page is shown; a treatment that fails them is replaced, not shown broken.

The gate decision then chooses among designed objects, which is the point: the client judges drawings, not a font menu.

---

## 9. SVG execution workflow (Google Fonts and local TTFs)

### 9.1 Route A, preferred: real outlines, real booleans

Live `<text>` renders differently per engine and font version, cannot be boolean-cut, and ships a font dependency into the logo file. A wordmark is frozen geometry, so freeze it first.

1. **Extract per-glyph paths with opentype.js** (npm, runs in Node): `opentype.parse(buffer)` on a local .ttf, then `font.getPaths(text, x, y, fontSize, {kerning: true})` gives one Path per glyph (each letter individually addressable, which is what surgery needs); `.toPathData(3)` exports SVG path data, `font.getAdvanceWidth()` gives spacing for re-kerning. opentype.js reads TTF, OTF and WOFF, not woff2: fetch the ttf (1.3). Bricolage Grotesque and other OFL faces may be outlined into a logo (2.2). Use **fontkit** instead when real shaping matters (its `font.layout(string)` applies OpenType features like ligatures before extraction).
2. **Booleans with paper.js headless** (`paper-jsdom`): import glyph path and cut shape, `glyphPath.subtract(cutShape)` for bites and cuts, `unite()` for joins, export `pathData`. opentype.js itself does not subtract. Python alternative: `svgpathtools` plus `pyclipper`.
3. **Inkscape CLI as fallback** when installed: `inkscape in.svg --export-text-to-path --export-plain-svg -o out.svg`, and `--actions="path-difference"` for booleans. On this machine the Node route is more reliable.
4. **Bake the result** to one filled path per glyph, no strokes; verify the fill-rule after booleans (a counter that disappears or fills solid is a fill-rule bug, not a design choice).
5. **Re-kern after surgery** (4.1, post-surgery rule), then freeze workbench HTML, font file, build script, and outlined SVG together in the version folder so the mark can always be re-derived.

### 9.2 Route B, exploration fallback: mask/clipPath overlays on live text

Render the webfont and overlay black cut shapes inside a `<mask>` or `<clipPath>` on the text. Fast to iterate, no libraries. Precision caveats: cut positions depend on the exact rendered font version and kerning of the viewing engine; if the webfont fails to load, cuts land on the wrong letters; no true joins or counter work is possible. Use only for on-screen exploration in a controlled render, never for the shipped asset or the gate page's frozen treatments. Never use overlay shapes in the background color as fake subtraction: it breaks on photos and gradients; a real `subtract()` keeps transparency.

### 9.3 Always verify by render at three sizes

Rasterize every frozen treatment at hero (~180px), heading (32px), and small (24px cap height, plus the 14-16px strip from criterion 2), via headless Chrome or resvg, and compare Chrome versus resvg output for parity. A treatment only exists once its three renders exist.

### 9.4 Workbench pitfalls (proven)

Pitfalls proven in a real engagement run; each cost debugging time once so it does not have to again.

- **Arc precision.** Rounding path coordinates to 1 decimal collapses the tiny start/end offset that makes a full-circle arc renderable; the arc degenerates and the hole silently vanishes. Guard: emit coordinates at 2 decimals and use a 0.05 offset between arc start and end.
- **Evenodd holes.** `fill-rule: evenodd` only punches a hole when the hole contour lies fully INSIDE the outer contour; a contour crossing the edge fills outside the shape as well. For an edge bite (crescent), compute the two circle-circle intersection points analytically and emit a two-arc path: the big arc of the disc, then back along the cutter arc.
- **paperjs-offset on raw font outlines.** paperjs-offset (npm, 2.2.1) throws "must contain at least one non-zero-length curve" on raw glyph paths. Guard: dedupe zero-length segments first (drop consecutive points closer than 0.01), do NOT call `resolveCrossings()`/`reorient()` on raw glyph compounds (it corrupts them), offset per contour and `unite()` the results.
- **NaN poisoning.** opentype.js `getKerningValue`/`advanceWidth` can return undefined for some pairs and for the space glyph; the NaN then enters path data as the literal string "NaN", whose letter "a" parses as an SVG arc command and crashes the parser far from the cause. Guard: wrap both in `isFinite` checks, and fail fast on `/NaN/` in any generated path data.
- **Weaving needs strand-like crossings.** Over-under weave logic produces collateral slivers wherever letterforms overlap in large patches. Guard: position the glyphs so only stem-like parts cross, build the gap as the RING of the over-shape (grown minus original) intersected with the (grown) crossing patch, and drop micro-specks (children with area below ~5) after the booleans.

---

## 10. Gate page deliverable spec and wordmark gate criteria

The wordmark gate is one HTML page, opened as a local review surface (the HTML in the browser), styled in the client's own design language, and reviewed alongside the symbol gate.

### 10.1 What the page shows, per treatment

1. **The real artwork.** Frozen SVG paths for custom treatments (9.1); embedded verified webfont only for the plain-type control (1.3).
2. **Three sizes.** Hero at ~180px, heading at 32px, and a small strip at 14px, all of the same frozen geometry. The small strip is the honesty check; no treatment gets presented on its hero render alone.
3. **Light, dark, and mono.** Each treatment on the light ground and the dark ground of the phase 3 palette (until that palette lands: ink #231F20 on paper, and paper on navy #181B2B), plus one pure 1-bit black-on-white render. The reversed version uses its looser tracking (4.3).
4. **Next to the symbol, plus the DNA overlay.** One lockup preview per treatment with the leading symbol direction, and for DNA-rule treatments the regression overlay from section 6 rule 2.
5. **License line.** One sentence per source font, in the client's language, from `licenties.md`.
6. **Name-rendering evidence.** The preferred form plus one counter-proposal (section 3), rendered, not described.
7. **Rationale and kill line.** The one-line family-plus-concept rationale (section 8 point 3) and one sentence naming what would disqualify the treatment (the kill-criteria habit from phase 2 continues here).

### 10.2 Gate criteria a treatment must pass before it is shown

1. **Squint/blur test:** Gaussian blur of ~2-3% of the render width; the word silhouette must still read and the intervention must read as intent, not dirt.
2. **24px render:** at 24px height the operated letter stays unambiguous; at the 14-16px strip the intervention may vanish gracefully but may never make a letter ambiguous.
3. **Mono 1-bit survival:** the treatment works in pure black on white, no color, no grayscale. An idea carried only by a color accent fails this by definition (section 0).
4. **Legibility floor:** roughly two thirds of the operated glyph's silhouette intact; the distinguishing feature versus neighbor letters untouched; at weight 800, cuts at least ~15% of the stroke width.
5. **Read-aloud test:** someone who has not seen the mark reads the small strip aloud without stalling on the operated letter.
6. **DNA overlay match** for DNA-rule treatments: the mark's real geometry overlays exactly.
7. **One sentence:** the treatment must be describable in one sentence, in the client's language, that names the idea it serves ("the bite out of the R is the same quarter circle as in the symbol: remove first, then learn again"). If the sentence needs a second clause of explanation, the treatment is too clever.

### 10.3 Closing the gate

Labels on the page, in the client's language (English base set): "Treatment 1: <family>", "Large", "Heading", "Small (14 px)", "On light", "On dark", "One color", "Next to the symbol", "DNA overlay", "License", "Rationale". After the client reviews the page, close the gate with one AskUserQuestion call (max 4 questions): treatment choice, name rendering, Re accent, and route confirmation (A/B/C from section 5). Record the outcome in the engagement's decision log and freeze the winner into the version folder: the outlined SVG, the workbench HTML, the build script, the font files, and `licenties.md`.

---

Sources for the cases and techniques in sections 0 and 5-9: Made Good Designs brand typography study (madegooddesigns.com/brand-typography-study/); Fonts In Use on Citibank and Mastercard; Creative Review on V&A and I Love NY; MoMA collection (I Love NY sketch); Google Design, "Evolving the Google Identity"; Logo Histories on FedEx (Lindon Leader); pentagram.com on Saks Fifth Avenue, Graphcore, Mastercard; It's Nice That on Graphcore; Karri Saarinen, "Working Type" (Airbnb Design); Design Week and Dezeen on Slack; Creative Boom on Pentagram's Cohere identity; Dinamo, Whyte Inktrap release; Wikipedia, "Ink trap"; opentype.js README (github.com/opentypejs/opentype.js); logodesign.net on micro vs macro spacing and on logo scalability.
