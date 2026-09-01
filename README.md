# /rebrand

A studio-grade rebranding process skill for Claude Code.

Most logo skills generate marks. This one runs an engagement: discovery questions before any design, a signed creative brief, a small number of defensible directions shown in the client's real context, explicit client gates between phases, real letterform surgery on font outlines, and adversarial self-checks before anything reaches the client. Modeled on how Pentagram, Koto, and Wolff Olins structure identity work: strategy before form, one carrying idea per concept, fitness over taste, bounded revision rounds.

The skill is Dutch-first: everything the client sees (questions, briefs, gate pages, guidelines) is in Dutch. The process instructions are in English, so the method ports to any language by translating the client-facing strings.

## The six phases

| Fase | Name | What happens | Gate (client decides) |
|---|---|---|---|
| 0 | Discovery | Four structured question rounds (~20-28 questions), the evolutie/revolutie decision, equity inventory, creative brief | "Is deze brief akkoord als fundament?" |
| 1 | Research & audit | Touchpoint audit, competitive landscape scan, 2x2 map, 2-3 visual territories | "Welk territory wordt de basis?" |
| 2 | Concept | 2-3 concepts, each with one carrying idea in one sentence, plus explicit kill-criteria | "Welk concept draagt de rebrand?" |
| 3 | Design exploration | Three parallel tracks: beeldmerk (icon geometry), woordmerk (letterform surgery on real font outlines), kleur (palette with computed WCAG ratios) | "Welke combinatie gaat door?" |
| 4 | System & stress-test | Lockup rules, fixed mockup set on real carriers, degradation tests (16px favicon, black-and-white copy, dark/light) | Go/no-go per carrier |
| 5 | Delivery & migration | Versioned asset export, brand guidelines, ordered migration plan | Livegang per carrier |

Each phase ends in a gate page the client reviews and annotates. Open the gate page as a local review surface (simply the HTML in the browser); the client's decision is asked explicitly, in Dutch, and logged. Nothing is "done" without a recorded decision. Partial engagements are valid: Fase 0+1 alone (brief plus audit) is a sellable milestone.

## What makes it different

- **A taste-recovery protocol.** When a client rejects rounds repeatedly ("nog niet", "lelijk"), the fix is upstream, not more variants. The skill switches to three taste-directive questions: what repelled, which earlier artifacts did land (named concretely, including rounds from before the current concept), and whether the mark must carry the story or may simply fit. In the worked engagement this recovered the direction in one round after four failed design rounds. A gate answer like "begin opnieuw, terug voordat je X voorstelde" kills a whole concept lineage, not one variant; killed work is archived, not deleted, because the client's favorites can resurrect it under a new reading.
- **Judging in system context.** The deciding question for a mark is not "is it beautiful on a tile" but "hoort het merk er ineens bij": every gate page opens with a mock fragment of the client's real design language (page header, kicker, card) with the candidate in place.
- **Kill-criteria per concept.** "Ik vind het niet mooi" is not a kill-criterion; "het teken is onleesbaar op 16px" is. Every concept ships with the observable conditions under which it has failed, which keeps iteration honest.
- **Calibration rounds.** Once a lane survives, the skill offers three calibrations of one variable each (hole size, ring angle, phase depth). Clients choose confidently between calibrations where they stall on concepts.
- **A responsive ladder.** Accessories in a mark follow a ratio ladder (roughly 1 : 0.42 : 0.18 of the base disc) and an explicit rule for what drops at which size, so the family degrades by design instead of by accident.
- **Real letterform surgery.** The wordmark track works on actual font outlines (opentype.js paths, boolean operations, per-contour offsets), not on typed lines with a font applied, with a workbench of proven geometry recipes and known SVG/boolean pitfalls.
- **Craft grounded in named sources.** The design references cite published research (Pieters/Wedel/Batra 2010, Henderson and Cote 1998, van Grinsven and Das 2016) and practitioner writing (Frere-Jones, Karow, Tracy), not vibes.

## Install

Clone this repository into your Claude Code skills directory:

```
git clone https://github.com/annetklo/rebrand-skill .claude/skills/rebrand
```

or, once published to a skills registry:

```
npx skills add rebrand
```

Then say "rebrand", "brand refresh", or "huisstijl vernieuwen" in a Claude Code session.

## Requirements

- **Claude Code** (the skill is a process; Claude runs it).
- **Node.js** with `opentype.js`, `paper-jsdom`, and `paperjs-offset` for the wordmark workbench (letterform surgery, boolean operations, outline offsets).
- **Headless Chrome** for rendering gate pages and mockups to PNG.
- Optional: the **logo-generator skill** by op7418 (github.com/op7418/logo-generator-skill) as the form engine in Fase 3; if it is not installed, the skill generates SVG variants directly from the geometry recipes in its references.
- Optional: **pen.dev** as a presentation surface for exploration pages.

> **Tip (pen.dev):** a `.pen` file is plain JSON, but it must be built on the app's own template base: the correct `version` (2.17 as of September 2026), a `fileToken`, and `themes`/`variables` as dicts. A wrong version opens as a silently empty canvas. Copy `version`, `themes`, and `variables` from a known-good file and generate a fresh token.

## Worked example

The skill uses **Mission Relearn** (an AI-literacy consultancy in the Netherlands) as its worked example throughout: the discovery answers, the territory names, the geometry of the exploration lanes, and the taste-recovery round all come from a real engagement run in late 2026. That is deliberate. A process skill with a real brand threaded through it is easier to follow than one full of placeholders; substitute your own brand's brief and the same machinery applies.

## Honest limitations

- **The process needs a human client at the gates.** The skill structures decisions; it does not make them. Without a person answering the gate questions, you get a logo generator with extra steps.
- **Human tests cannot be automated.** The doodle test (can someone sketch the mark from memory), hallway recognition, and stakeholder interviews require actual people.
- **AI is not a substitute for a type designer on the final master.** The wordmark workbench gets you to a defensible, tested direction with real outline surgery, but a mark that will carry a company for a decade deserves a professional's pass on spacing, optical corrections, and production masters.

## Credits and sources

The craft references in this skill cite, among others:

- Pieters, Wedel and Batra (2010), on visual complexity and attention
- Henderson and Cote (1998), "Guidelines for Selecting or Modifying Logos"
- van Grinsven and Das (2016), on logo change and consumer response
- Tobias Frere-Jones, on optical adjustment in type
- Peter Karow, on digital letterform technology
- Walter Tracy, *Letters of Credit*, on type evaluation
- Published case documentation from Pentagram, Koto, Wolff Olins, DesignStudio, and Sagi Haviv (Chermayeff & Geismar & Haviv)

These sources retain their own rights; citation here is reference, not reproduction.

## License

The process text in this skill is suggested for release under the **MIT License**. Cited sources, quoted practitioners, and any third-party skills or fonts you use with it retain their own licenses and rights.
