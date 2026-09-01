# Fase 4: Applications & stress-test

Loaded by SKILL.md when Fase 4 starts. Input: the frozen Fase 3 set (beeldmerk SVG, woordmerk SVG or font lockup, palette with dark-mode variants) plus the creative brief. Output: a stress-test report, derived usage rules (clear space, minimum sizes), the fixed mockup set, a misuse gallery, and a per-drager go/no-go that gates Fase 5.

Order of work is fixed. Degradation tests run FIRST, because they are cheap and they kill weak marks before any mockup polishing. A mark that fails the 1-bit or 16px test goes back to Fase 3 iteration; do not paper over a form problem with mockup styling.

1. Degradation battery on the frozen mark
2. Derive clear space and minimum sizes from the results
3. Build and render the fixed mockup set
4. Generate the misuse gallery
5. Assemble the review page and run the per-drager gate

## File locations (never overwrite v1)

All Fase 4 output goes into the new version folder, never into the existing brand-asset tree:

- Mockup HTML sources + screenshots: a new version folder next to the client's existing brand assets, e.g. `<merk-assets>/v2-<yymmdd>/stress-test/` (subfolders `mockups/`, `degradation/`, `misuse/`)
- Review page: the engagement folder in your workspace, e.g. `<engagement-map>/<yymmdd>-rebrand-stresstest/`, opened as a local review surface (de HTML in de browser), like every other gate
- The existing brand-asset folders (PNG exports and siblings) stay untouched until Fase 5 migration, and even then per-drager and additive

Keep the HTML sources in the version folder, not in a temp/scratch directory: temp files age out (macOS cleans them after roughly 3 days) and every mockup must stay re-renderable when the mark gets a late tweak.

Photorealistic showcase images via Gemini (`generate_showcase.py` from the logo-generator skill, github.com/op7418/logo-generator-skill, if installed) cost money per image. They are OFF by default in Fase 4. The HTML mockups below are the deliverable; offer Gemini showcases once, in one line, and only run them when the client explicitly says yes.

## Step 1: Degradation battery

Run all five tests on the frozen lockup and on the icon-only mark. Every verdict lands in the review page with the rendered evidence next to it. A fail on test 1 or 3 is a Fase 3 return; a fail on 2, 4 or 5 can sometimes be fixed inside Fase 4 (variant choice, palette tweak) and must then be re-tested.

| # | Test | How to produce it | Pass criteria |
|---|------|-------------------|---------------|
| 1 | 1-bit (zwart-wit) | Re-render the SVG twice with all fills and strokes forced to `#000` on white, and to `#FFF` on black. This is a re-render, never a threshold filter over a colored PNG: thresholding invents arbitrary shapes where colors have similar luma. | Every element still distinguishable; no shape depends on color or gradient to separate from its neighbor; counters and gaps stay open. This version is what ends up on facturen, stempels, embossing and office printers, so a fail here is a form fail. |
| 2 | Grayscale | Pillow: `Image.open(p).convert("L")` on the full-color render. Reference point: coral `#F36E59` converts to luma 147/255, roughly 58% gray; ink `#231F20` sits near 13%. | Adjacent color pairs must separate by at least 50 luma points on the 0-255 scale (roughly 20%). Coral sits at luma 147; anything between roughly 97 and 197 merges with it in grayscale print, and that pairing is then forbidden in the guidelines, or the palette changes. |
| 3 | 16px favicon | True 16x16 render via the logo-generator skill's `svg_to_png.py` (github.com/op7418/logo-generator-skill) if installed, else any SVG rasterizer (cairosvg, resvg), plus the tab-strip mockup below. Judge at 100% zoom; a 4x nearest-neighbor blowup may sit NEXT to it for inspection, but the verdict comes from true size. | Silhouette recognizable, strokes at least 2px at the 16px render (equals 64px on a 512px source). If the full mark fails this, that is normal and not a Fase 3 return: the correct fix is a dedicated simplified favicon mark (icon fragment or monogram), sourced at 512x512 with ~10% inner padding. |
| 4 | Beamer / low contrast | Simulate a mid-range projector in a lit room: desaturate to 60% and lift the black point to ~18%. Pillow: `ImageEnhance.Color(img).enhance(0.6)` then `img.point(lambda v: int(46 + v * 0.72))` per channel. Apply to the deck-cover mockup, not just the bare mark. | Mark and wordmark still read against the slide background at roughly 3:1 contrast after the wash. WCAG 1.4.11 formally exempts logos, but 3:1 is the internal floor here, and the clickable site-header logo must genuinely hit 3:1 against adjacent colors. |
| 5 | Print at 15mm | Render the lockup at 15mm width at 300dpi = 177px, and the icon alone at 6mm = 71px. Print one A4 proof if a printer is at hand; otherwise judge the 300dpi crops at 100%. | Wordmark counters (e, a, o) stay open, icon details stay separated, nothing fills in. The smallest width that still passes becomes the documented minimum in Step 2, rounded UP to a clean number. |

Deliverable consequence, non-negotiable: the final asset set ships at minimum as full color + mono black + mono white (reversed). The dark-mode variant decision (mono white, or an adjusted-color version) is made here, on the evidence of tests 1 and 4.

## Step 2: Derive clear space and minimum size

These rules are DERIVED from the chosen mark and the test results, never invented as arbitrary values.

**Clear space.** Define the exclusion zone as a ratio to an element inside the mark itself, so it scales with every reproduction. Two standard methods; pick the one that fits the mark type:

- Wordmark-led lockup: the unit is the cap height of one letter in the wordmark (University at Buffalo and Memphis use this). X-height gives a tighter zone, cap height a roomier one; for a consultancy mark that must survive government documents, take cap height.
- Icon-led mark: the unit is a fraction of the icon, standard is half the icon height (Spotify's published rule: exclusion zone = half the height of the icon).

Draw the rule as a diagram for the guidelines: the lockup with the unit element repeated on all four sides. Phrase it as an absolute minimum ("geef het meer ruimte waar het kan"). Nothing enters the zone: no text, no second logo, no page edge, no graphic element.

**Minimum size.** Document in TWO systems, mm for print and px for digital, because the failure modes differ (ink spread vs pixel grid). Start from convention, then let the tests decide:

- Convention: full lockup ~20mm wide in print (range 15-25mm) and 70-120px digital; icon-only ~6mm print, 21-24px digital (Spotify publishes 70px/20mm for the logo, 21px/6mm for the icon). Practical digital floor: never below 24px height for a lockup on the web.
- The documented value = the smallest size that passed test 5 (print) and test 3 (digital), rounded up. Convention is the starting hypothesis, the render is the judge.
- The below-minimum rule always flips to "gebruik dan het losse beeldmerk", never to "verklein de volledige lockup toch maar".

**Favicon and round-crop safe zone.** The favicon/avatar mark lives on a 512x512 source with ~10% inner padding, and everything essential inside a central circle of 80% of the canvas (the Android maskable spec is 409px on 512px), because LinkedIn, WhatsApp and Android all crop to a circle or squircle.

Record all derived values in a small table; Fase 5 copies it verbatim into the guidelines page and into your optional project knowledge (bijv. een brand-bestand als je dat hebt).

## Step 3: The fixed mockup set

The table below is the example touchpoint set from the MR run. Derive the client's own set from the Fase 0 brief: their most-used real touchpoints, always including favicon and avatar (every brand meets a browser tab and a round crop). Keep the same table structure per touchpoint: canvas, what it must show, drager-specific requirements.

Nine mockups, each a self-contained HTML file with the mark inlined as SVG (or the exact-size PNG for the favicon cells), fonts via Google Fonts, no other external assets. Platform mockups (tab strip, LinkedIn) are schematic: gray UI shapes that suggest the context, never a pixel-clone with the platform's own logos. Number the files so the render loop and the review page stay in order.

| File | Canvas (px) | What it must show | Drager-specific requirements |
|------|-------------|-------------------|------------------------------|
| `01_favicon_tabstrip.html` | 1200x220 | A light AND a dark browser tab strip, each with the favicon at true 16px and 32px next to competitor-neutral gray tabs | Judge at 100%. The 16px cell uses the real 16px PNG from test 3, not a downscaled CSS image. Both strip shades must pass. |
| `02_linkedin_avatar.html` | 900x500 | The 400x400 avatar shown in a round crop at 400px AND at 48px (feed size), on white and on the app's dark gray | Nothing essential outside the central 80% circle. The 48px render is the real verdict: that is how most people see it. |
| `03_linkedin_banner.html` | 1584x396 | Profile banner with the mark placed in the right two-thirds, vertically centered | The avatar circle overlaps the bottom-left of a profile banner and mobile crops the sides: keep the mark out of the left ~400px and away from the outer 10% edges. If the run covers the bedrijfspagina too, add a 1128x191 company-cover variant. |
| `04_deck_cover.html` | 1920x1080 | Title slide in the deck-template style: mark + title + one line | Runs through the beamer wash (test 4) as a second render. Both the normal and the washed version go on the review page. |
| `05_offerte_header.html` | 1240x360 | Top strip of an A4 offerte at 150dpi (1240px = 210mm), with the logo at its real print size | At 20mm the logo is ~118px on this canvas. Header must also work in the mono-black version (office printers). Use a real offerte title block in the brand's own fonts (MR: Cal Sans/Open Sans). |
| `06_site_header.html` | 1440x160 | Sticky site header, light and dark mode stacked, logo at 32-40px height with nav links | The logo is a clickable UI element here: 3:1 contrast against adjacent colors is a hard requirement, no WCAG logo exemption. |
| `07_email_signature.html` | 700x300 | Signature block at 600px mail width: name, rol, logo at ~120px display width | Text in the house mail typography (MR: Open Sans 11px). Note in the mockup caption: mail clients (Gmail, Outlook) do not render SVG, so the shipped asset is a PNG at 2x (240px file, 120px display). |
| `08_sticker_stempel.html` | 1000x520 | Left: round stamp, 40mm at 300dpi = 472px, mono black on white. Right: die-cut sticker, mono white on coral | Stamp side uses ONLY the 1-bit version from test 1. Minimum line width for rubber stamps is 0.3mm = 3.5px at 300dpi; any thinner line in the mark fails this drager. |
| `09_social_post.html` | 1080x1080 | Social template: one headline + one product/visual crop + the mark in a fixed corner | The MR run's standing rule for social images: one kopregel plus crop, no subkop, minimal text. The mark's corner position and size become template constants for the brand's social-template tooling in Fase 5. |

Dark/light coverage is built into the set: 01 and 06 show both modes side by side, 02 shows the dark app background, 04 gets the beamer variant. Every mockup that shows a dark context uses the dark-mode variant decided in Step 1, not an auto-inverted file.

### Render recipe (headless Chrome, known gotchas apply)

One render = one fresh Chrome process with its own profile, killed by process group, and delete stale output first. Proven failure modes from real runs: a bash for-loop hangs on render 1 because Chrome never exits; re-rendering onto an existing file makes the stability poll accept the OLD bytes; `p.terminate()` leaves helper processes that pile up until every render silently produces an empty PNG; macOS has no `timeout` command; and window widths under ~500px only clip the screenshot instead of narrowing the layout.

```python
import subprocess, os, signal, tempfile, time, shutil

CHROME = "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"

def render(html_path, png_path, width, height):
    if os.path.exists(png_path):
        os.remove(png_path)  # otherwise the poll sees the old bytes as "stable"
    profile = tempfile.mkdtemp(prefix="chrome-prof-")
    p = subprocess.Popen([
        CHROME, "--headless", "--disable-gpu",
        f"--user-data-dir={profile}",
        f"--window-size={max(width, 500)},{height}",
        f"--screenshot={png_path}",
        f"file://{html_path}",
    ], start_new_session=True)
    last = -1
    for _ in range(60):
        time.sleep(0.5)
        size = os.path.getsize(png_path) if os.path.exists(png_path) else -1
        if size > 0 and size == last:
            break
        last = size
    os.killpg(os.getpgid(p.pid), signal.SIGKILL)  # kills Chrome's helpers too
    shutil.rmtree(profile, ignore_errors=True)
```

For a mockup narrower than 500px (none in the standard set, but iterations happen): force `body{width:...px}` in the HTML and render at >=500 wide. If a render fails with no visible reason: `pgrep -f "Google Chrome" | wc -l` and `pkill -9 -f chrome-prof-` before retrying. Exact-size PNGs of the bare mark (16px, 32px, 71px, 177px) come from an SVG rasterizer (the logo-generator skill's `svg_to_png.py` if installed, else cairosvg or resvg directly), not from Chrome.

## Step 4: Misuse gallery

Generate the eight standard misuse examples with the ACTUAL chosen mark, each as a small thumbnail with a coral cross overlay and a Dutch caption. Showing the real mark done wrong teaches faster than any rule text; this gallery goes verbatim into the Fase 5 guidelines.

Build as one HTML grid (`misuse/misuse_gallery.html`), render once. The wrong versions are produced deliberately and precisely:

| # | Misuse render | Caption (verbatim in the guidelines) |
|---|---------------|--------------------------------------|
| 1 | Non-proportional scale, 130% horizontal | "Niet uitrekken of samendrukken" |
| 2 | Mark recolored to an off-brand color (pick a plausible offender, e.g. a corporate blue) | "Geen eigen kleuren kiezen: alleen de vastgelegde varianten" |
| 3 | 2px contrasting outline added around all shapes | "Geen outline toevoegen" |
| 4 | Drop shadow (8px blur, 40% black) | "Geen schaduw, gloed of filter" |
| 5 | Mark on a busy photo without a rustvlak (use a cluttered stock-style CSS collage) | "Niet op drukke achtergronden zonder rustvlak" |
| 6 | Rotated 12 degrees | "Niet roteren of kantelen" |
| 7 | 40% opacity as watermark over text | "Niet halftransparant als watermerk gebruiken" |
| 8 | Old rocket mark and new mark side by side in one lockup, or the new mark in the old styling | "Oud en nieuw merk nooit mengen: de migratie per drager is atomair" |

Two structural misuses are covered elsewhere and need no thumbnail: crowding (the clear-space diagram from Step 2 handles it) and typeface substitution (the woordmerk section of the guidelines handles it). Do not pad the gallery beyond what the guidelines will actually show.

## Step 5: Review page and the per-drager gate

Before assembling the page, copy every PNG it will show (the degradation renders, the nine mockup screenshots, the misuse gallery render) from the version folder into an `assets/` subfolder of the review directory: `<engagement-map>/<yymmdd>-rebrand-stresstest/assets/`. A local review server typically serves the HTML from its own directory and only resolves images that sit inside it, referenced with relative paths (`assets/<name>.png`); absolute or root paths show up as broken images, at exactly the moment the client must judge renders. The version folder under `<merk-assets>/v2-<yymmdd>/stress-test/` stays the canonical source; the review copies are duplicates only, never the files Fase 5 migrates from.

Then assemble one gate page in `<engagement-map>/<yymmdd>-rebrand-stresstest/` and open it as a local review surface (de HTML in de browser). Page order mirrors the work order:

1. Degradation results, each test with its render and an explicit verdict (geslaagd / gezakt / gezakt met fix)
2. Derived rules: the clear-space diagram, the minimum-size table (mm + px), the below-minimum rule
3. The nine mockups, grouped per drager, dark and light variants side by side
4. The misuse gallery

Then run the gate through AskUserQuestion, maximum 4 questions per call, so the nine dragers take three calls. One question per drager, phrased in Dutch, for example:

- Header: "Favicon", question: "Favicon (16px, beide tab-strips): go voor migratie in fase 5?", options: "Go" / "Go, met kleine aanpassing (zeg welke)" / "No-go, terug naar fase 3"
- Same pattern for: LinkedIn-avatar, LinkedIn-banner, deck-cover, offerte-header, site-header, e-mailhandtekening, sticker/stempel, social-template

The hard rule: **each drager gets its own explicit go.** A blanket "ziet er goed uit" is not a go; ask the per-drager questions anyway and record every answer. Fase 5 may only migrate a drager that has its own recorded go, and a no-go on one drager never blocks migration of the others. Log the answers as one entry in the project's decision log (in the MR run: a `plans/decisions/` folder maintained by a decision-documentation skill), with the review page linked as evidence.

### Go/no-go criteria per drager (what "go" must mean)

Use this as the checklist when presenting each question; a drager with an open blocking item cannot be offered as "Go". The rows follow the example touchpoint set (MR-run); when the client's set differs, derive one blocking-criteria row per drager the same way, from the degradation results and the drager-specific requirements.

| Drager | Blocking criteria |
|--------|-------------------|
| Favicon | Reads at true 16px; passes on light AND dark tab strip; essential form inside the 80% circle safe zone; dedicated simplified mark exists if the full mark failed test 3 |
| LinkedIn-avatar | Survives the round crop; reads at 48px feed size; works on the dark app background |
| LinkedIn-banner | Mark clear of the avatar overlap (left ~400px) and outer 10% edges; readable in the washed beamer-style render of a phone screen in daylight is not required, mobile crop is |
| Deck-cover | Passes the beamer wash (test 4) at 3:1; consistent with the slide-deck template |
| Offerte-header | Mono-black version acceptable (office printers); logo at or above the documented print minimum on A4 |
| Site-header | 3:1 contrast as clickable element in BOTH modes; fits at 32-40px height without a special variant |
| E-mailhandtekening | PNG fallback produced at 2x; legible next to Open Sans 11px text |
| Sticker/stempel | 1-bit version passed test 1; no line under 0.3mm at 40mm stamp size; single color, zero gradients |
| Social-template | Fixed corner position defined; template respects the one-kopregel-plus-crop rule; values ready to hand to the brand's social-template tooling in Fase 5 |

When all questions are answered, summarize: which dragers have go, which have go-met-aanpassing (list the aanpassingen as Fase 4 punch list, re-render, re-ask only those), which are no-go. Only then does SKILL.md hand over to Fase 5, carrying the derived rules table, the final lockup set, and the per-drager go-list.
