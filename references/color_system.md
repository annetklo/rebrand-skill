# Color system: the kleur-spoor of Fase 3

How to build a full color system around one core color. Runs as one of the three parallel tracks in Fase 3 (beeldmerk, woordmerk, kleur), after the concept gate. Inputs: the creative brief (Fase 0), the chosen territory (Fase 1), the chosen concept (Fase 2), and the core color. Output: the palette gate page (spec at the bottom) that the client approves before Fase 4.

Brand-agnostic: the recipe works for any client core color. Mission Relearn coral is the worked example throughout.

## Step 0: pin the anchor hex, do not trust this file

Before anything else, confirm the exact core color with the user. Brand documents drift: MR's coral appears as `#F36E59` in older documents and as `#ED7059` in a later design-system revision; the live design-system CSS turned out to be the single source of truth. A ramp built on the wrong anchor is worthless, so ask which hex is canonical, or read it from the client's live CSS, or from optional project knowledge (bijv. een clients- of brand-bestand als je dat hebt). The worked example below uses `#F36E59` with ink `#231F20`; regenerate all derived values if the anchor differs.

Never generate the anchor from a formula. The brand color IS one step of the ramp (usually 500); everything else is built outward from it.

## Step 1: build the tint/shade ramp (5 to 7 steps)

Work in OKLCH, not HSL. In HSL a 5% lightness step looks huge for yellow and invisible for blue; in OKLCH equal L steps look equal across hues. CSS supports `oklch()` natively since 2023, so the ramp can ship as OKLCH with hex fallbacks.

Recipe:

1. Convert the anchor to OKLCH. Coral `#F36E59` = L 0.695, C 0.168, H 30.9. (Note: OKLCH hue, not HSL hue. Coral is hue 8 in HSL but 31 in OKLCH; never mix the two scales.)
2. Anchor at step 500. Sweep L outward: tints at roughly 0.965, 0.92, 0.80; shades at roughly 0.55, 0.45, 0.36. That gives 7 steps (50, 100, 300, 500, 700, 800, 900), enough for both light and dark mode from one ramp. 5 steps (drop 50 and 800) is the minimum for a small client brand.
3. Use relative chroma: at each L, compute the maximum chroma that stays inside sRGB gamut and take a fraction of it (tints 55 to 75%, shades 55 to 70%). Fixed absolute chroma clips out of gamut at the light end and turns to mud at the dark end.
4. Drift the hue deliberately: tints a few degrees toward orange (H+8 at the lightest step), shades toward red (H-6 at the darkest). Warm hues look richer with this drift than with a straight ramp; a fixed hue makes shades of coral look like dried blood.
5. Round-trip check: converting your step-500 OKLCH back to hex must reproduce the anchor exactly.

Worked example, all contrast values computed (script in step 4):

| Step | Hex | On white | On ink #231F20 | Role |
|---|---|---|---|---|
| coral-50 | `#FAF1EF` | 1.11 | 14.67 | tinted surface, callout fill |
| coral-100 | `#F7DED6` | 1.28 | 12.71 | chip/pill background |
| coral-300 | `#F0AA98` | 1.93 | 8.47 | dark-mode accent (see step 5) |
| coral-500 | `#F36E59` | 2.92 | 5.58 | THE brand color, anchor |
| coral-700 | `#BC4337` | 5.25 | 3.10 | text-safe coral on white |
| coral-800 | `#8C352F` | 7.88 | 2.07 | AAA text on white |
| coral-900 | `#612A27` | 11.24 | 1.45 | deep accent, borders on tints |

The single most important row: **coral-500 on white is 2.92:1. That fails 4.5:1 for normal text and even fails 3:1 for large text and UI components.** Nearly every saturated warm brand color fails at step 500 because green dominates the luminance weights (0.7152). The system must therefore name a "text-safe" step explicitly: here coral-700. Body links, coral text on white, and input borders use 700, never 500. The logo itself is exempt (WCAG exempts logotypes), UI text in the brand color is not.

Same trap on CTAs: white text on coral-500 is also 2.92:1, so the classic white-on-coral button fails AA. Two fixes that keep the look: ink text on coral-500 (5.58:1, passes) or white text on coral-700 (5.25:1, passes).

### OKLCH helper (optional, for generating ramps in a script)

Bjorn Ottosson's reference matrices, Python 3.9, stdlib only:

```python
import math

def _lin(c8):
    c = c8 / 255.0
    return c / 12.92 if c <= 0.04045 else ((c + 0.055) / 1.055) ** 2.4

def _srgb(c):
    c = max(0.0, min(1.0, c))
    return round((12.92 * c if c <= 0.0031308 else 1.055 * c ** (1 / 2.4) - 0.055) * 255)

def oklch_to_hex(L, C, H):
    a, b = C * math.cos(math.radians(H)), C * math.sin(math.radians(H))
    l_, m_, s_ = L + 0.3963377774*a + 0.2158037573*b, L - 0.1055613458*a - 0.0638541728*b, L - 0.0894841775*a - 1.2914855480*b
    l, m, s = l_**3, m_**3, s_**3
    r = +4.0767416621*l - 3.3077115913*m + 0.2309699292*s
    g = -1.2684380046*l + 2.6097574011*m - 0.3413193965*s
    bb = -0.0041960863*l - 0.7034186147*m + 1.7076147010*s
    return "#%02X%02X%02X" % (_srgb(r), _srgb(g), _srgb(bb))

def hex_to_oklch(hex_color):
    h = hex_color.lstrip("#")
    r, g, b = (_lin(int(h[i:i+2], 16)) for i in (0, 2, 4))
    l = (0.4122214708*r + 0.5363325363*g + 0.0514459929*b) ** (1/3)
    m = (0.2119034982*r + 0.6806995451*g + 0.1073969566*b) ** (1/3)
    s = (0.0883024619*r + 0.2817188376*g + 0.6299787005*b) ** (1/3)
    L = 0.2104542553*l + 0.7936177850*m - 0.0040720468*s
    a = 1.9779984951*l - 2.4285922050*m + 0.4505937099*s
    bb = 0.0259040371*l + 0.7827717662*m - 0.8086757660*s
    return L, math.hypot(a, bb), math.degrees(math.atan2(bb, a)) % 360
```

Find max in-gamut chroma at a given L and H by bisection on C (40 iterations, check all three linear channels stay in 0..1).

## Step 2: neutrals with a hue cast

Pure 0-saturation grays look dead next to a saturated brand color. Tint every neutral toward the brand hue with OKLCH chroma 0.005 to 0.02 (roughly 2 to 6% saturation): warm cast reads approachable and human (fits education and consultancy, fits MR), cool cast reads technical (dev tools, finance). Pick ONE temperature and keep it identical across every surface: page background, card, sidebar, border, tooltip. OneSignal's "11 shades of gray" case built its entire UI plus dark mode from one such tinted base.

Recipe: copy the brand hue (H 31 for coral), sweep L from 0.985 down to 0.25, chroma 0.006 to 0.012. Worked example:

| Step | Hex | On white | Role |
|---|---|---|---|
| neutral-50 | `#FEF9F8` | 1.04 | page background |
| neutral-100 | `#F5EEED` | 1.15 | alternating section, card on 50 |
| neutral-300 | `#D4CBCA` | 1.59 | borders, dividers |
| neutral-500 | `#8D8482` | 3.65 | disabled text, placeholders ONLY |
| neutral-700 | `#534B49` | 8.50 | muted/secondary text |
| neutral-900 | `#26201F` | 16.05 | near-ink, headings |

Second classic trap: neutral-500 at 3.65:1 fails 4.5:1, so "muted text" must map to neutral-700, not the middle gray that looks right in a mockup. (MR's current muted `#6A7280` sits at 4.85:1 on white: passes, barely. Check the equivalent step of any new neutral ramp against 4.5 before assigning it the muted-text role.)

If the brand keeps a dark surface color (MR's ink `#231F20`, or navy `#181B2B`), treat it as the 950 end of the neutral ramp and verify it carries the same hue temperature. Ink converts to OKLCH L 0.244, C 0.006, H 1: warm, consistent with coral. A cool navy next to warm neutrals will look accidentally mismatched on the gate page; flag it rather than hide it.

## Step 3: supporting hues, two selection methods

Method A, wheel-derived (use when the brand needs hues that are provably distinct):

- Complementary: opposite in OKLCH hue space. For coral H 31 that is H 211, a teal-blue. Maximum contrast, energetic, suits a bold two-color identity. Rule: drop the complement's chroma below the primary's (60 to 80% of it), otherwise the two colors compete for the accent role.
- Split-complementary is the pragmatic default: the two hues flanking the complement (H 181 and H 241 for coral), contrast without the vibration of a direct complement.
- Analogous (warm red, orange, amber around coral): harmonious and calm but low differentiation; only works when the neutral ramp carries all functional contrast.

Method B, environment-derived (use when the brand already lives somewhere): pull candidate hues from the chosen Fase 1 territory moodboard and from colors the brand already owns de facto. MR example: navy `#181B2B` (dark surfaces in the current design system) and sky-blue `#DCEEF5` (info chips) are already supporting hues in production; a wheel exercise that ignores them proposes a palette the brand cannot migrate to. Extract, then normalize: rebuild each inherited hue as a proper ramp with the step-1 recipe so cross-hue steps are interchangeable at equal contrast (coral-700 and blue-700 must both pass 4.5:1 on white).

How many is too many: **one accent plus at most two supporting hue families plus the neutral ramp.** Frame the distribution as 60-30-10: tinted neutrals roughly 60% of any surface, supporting hue 30%, brand accent 10%. Color is the strongest recall handle a brand has (in Reboot's 2018 online recall study, 78% of participants remembered a brand's primary color versus 43% its name), and that handle only works when the 10% stays singular, so never introduce a second accent (MR's design system says this verbatim: "Don't introduce a second accent"). Status colors (success, warning, danger, info) are functional, not brand: build each as a small ramp (bg, border, text) with the same recipe, but they do not count toward the hue budget and never appear in brand expression.

## Step 4: accessibility check, computed, never eyeballed

WCAG 2.2 thresholds (unchanged from 2.1):

- 1.4.3 Contrast (Minimum), AA: normal text 4.5:1; large text 3:1. Large text = at least 18pt (24px) regular or 14pt (18.66px) bold.
- 1.4.6 Contrast (Enhanced), AAA: normal text 7:1; large text 4.5:1.
- 1.4.11 Non-text Contrast, AA: 3:1 for UI component boundaries and states (input borders, checkbox marks, focus indicators) and meaningful graphics, against adjacent colors. Disabled components and pure decoration are exempt.
- 2.4.13 Focus Appearance (AAA, new in 2.2): focus indicator at least a 2px perimeter, 3:1 against the unfocused state.
- Logos and wordmarks are exempt from text contrast; UI text set in the brand color is not.

Relative luminance, exact formula (per sRGB channel c in 0..1, so channel/255):

```
c_lin = c / 12.92                    if c <= 0.04045
c_lin = ((c + 0.055) / 1.055) ^ 2.4  otherwise
L = 0.2126 * R_lin + 0.7152 * G_lin + 0.0722 * B_lin
ratio = (L1 + 0.05) / (L2 + 0.05)    with L1 the lighter of the two
```

(The WCAG text prints the threshold as 0.03928; 0.04045 is the corrected sRGB constant and both give identical results at 8-bit.)

Ready-to-run checker, Python 3.9, no packages. Run it with `python3`, feed it every pair in the required-pairs list below, and paste the output into the gate page:

```python
#!/usr/bin/env python3
"""WCAG 2.2 contrast checker. Usage: python3 contrast.py '#F36E59' '#FFFFFF'"""
import sys

def _lin(c8):
    c = c8 / 255.0
    return c / 12.92 if c <= 0.04045 else ((c + 0.055) / 1.055) ** 2.4

def luminance(hex_color):
    h = hex_color.lstrip("#")
    r, g, b = (int(h[i:i+2], 16) for i in (0, 2, 4))
    return 0.2126 * _lin(r) + 0.7152 * _lin(g) + 0.0722 * _lin(b)

def contrast(hex1, hex2):
    l1, l2 = luminance(hex1), luminance(hex2)
    if l1 < l2:
        l1, l2 = l2, l1
    return (l1 + 0.05) / (l2 + 0.05)

def verdict(ratio):
    labels = []
    if ratio >= 7.0:
        labels.append("AAA normale tekst")
    if ratio >= 4.5:
        labels.append("AA normale tekst")
    if ratio >= 3.0:
        labels.append("AA grote tekst / UI")
    return ", ".join(labels) if labels else "FAALT alles"

if __name__ == "__main__":
    a, b = sys.argv[1], sys.argv[2]
    r = contrast(a, b)
    print("%s op %s: %.2f:1  [%s]" % (a, b, r, verdict(r)))
```

Required pairs (the gate page shows all of them with pass/fail per threshold):

1. Text-safe brand step on white and on the page background (target >= 4.5)
2. Brand-500 on white (expected to fail: document it, do not hide it)
3. Ink/foreground on white, on background, on brand-50 and brand-100 tints (>= 4.5)
4. Muted text step on white and on every light surface it will sit on (>= 4.5)
5. CTA combinations: button text on button fill, both light and dark mode (>= 4.5)
6. Border step against adjacent surfaces, focus ring against white (>= 3.0)
7. Dark mode: accent step on the dark surface and on the elevated surface (>= 4.5)
8. Each supporting hue's text step on white (>= 4.5)

## Step 5: dark mode, four rules

1. **Tonal swap, never reuse.** The light-mode accent step does not move to dark mode; a lighter and softer step from the same ramp takes over (the Material pattern: a tone-600 accent in light becomes tone-200/300 in dark). Coral example: coral-300 `#F0AA98` is the dark-mode accent at 8.47:1 on ink, comfortably AAA. Rule of thumb when no step fits: reduce saturation 15 to 25% and raise lightness until the measured ratio reaches 4.5:1 on the dark surface.
2. **No pure black.** The dark surface is a dark neutral carrying the same hue cast as the light-mode neutrals (Material uses #121212-class surfaces). MR's ink `#231F20` already qualifies (OKLCH L 0.244, warm hue 1). If a client brand has no dark color, derive one: neutral ramp hue, L 0.20 to 0.25.
3. **Elevation = lighter surface, not shadow.** Shadows are invisible on dark backgrounds. Define 2 or 3 elevated surfaces by raising L with the same hue: on ink, `#2E2829` (card) and `#3A3334` (modal/popover) work as elevation steps. Verify content still passes on the highest surface: coral-300 on `#2E2829` is 7.51:1, still AAA.
4. **Test the actual pair, then look at it.** Coral-500 on ink measures 5.58:1 and passes AA numerically, but a saturated warm mid-tone on near-black halates: it vibrates at text sizes and large filled areas. Use the measured-and-passing 500 only for small accents (icons, eyebrow text, focus rings) and set running text and buttons in the 300 step. The number is necessary, not sufficient: the dark-mode preview on the gate page exists precisely because this failure is visible but not computable.

## Deliverable: the palette gate page

One HTML gate page in the engagement folder in your workspace (`<engagement-map>/<datum>-rebrand-<naam>/`), in the same design language as the exploration gate page from the concept phase: branded for the brand under review (MR-branded for MR work, client-branded for client work). Open the gate page as a local review surface (de HTML in de browser). Never write into an existing brand-style folder; exports later land in a new version folder in Fase 5.

Sections, in order:

1. **Ramp-overzicht**: horizontal strips for the primary ramp, the neutral ramp, and each supporting ramp. Every swatch shows step number, hex, and OKLCH values. The anchor step gets a marker "merk-kleur, vast".
2. **Token-voorstel**: two tables. Tier 1 primitives (numeric names: `coral-500`, `neutral-100`), then Tier 2 semantic mapping (`text-primary`, `text-muted`, `surface-page`, `surface-card`, `border-default`, `action-primary`, `action-primary-hover`, `focus-ring`, plus the status ramps) with one column per mode: licht and donker. Components will reference only Tier 2, so a future rebrand swaps Tier 1 and remaps Tier 2 without touching any template: state this on the page, it is the payoff of the whole exercise.
3. **Contrast-tabel**: every required pair from step 4, script-computed ratio, and per threshold a chip: "voldoet AA", "voldoet AAA", or "faalt". Failing pairs stay visible with the fix next to them ("gebruik coral-700 voor tekst"). A gate page that only shows passing pairs is a sales page, not a review surface.
4. **Dark-mode-preview**: the same mini-UI twice, side by side (licht / donker): a card with heading, body text, muted caption, one primary button, one link, one input with focus ring, one status banner. Both rendered purely from Tier 2 tokens.
5. **In-context-strook**: the palette on the three most-used real applications from the Fase 0 brief (for MR typically: site-hero, offerte-pagina, LinkedIn-tegel).

Gate: after the client reviews (annotations on the review surface for iteration, max two rounds, then freeze), close with one AskUserQuestion call, for example:

- header: "Palet", question: "Welke kleursysteem-richting keur je goed voor fase 4?", options such as "Richting A zoals getoond", "Richting A met aanpassingen (zet ze in je antwoord)", "Nog een iteratieronde".

The approved palette (hexes, OKLCH values, both token tables, and the full contrast table) is written to the run folder as `palet-def.md` so Fase 4 (stress-test) and Fase 5 (guidelines, `brand.md` update) read from one file instead of from the gate page's HTML.
