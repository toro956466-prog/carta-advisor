# Carta Advisory — Design system skill

> Instructions for using this design system on new Carta Advisory surfaces. Read `README.md` first for brand context and voice; this file tells you *how* to build.

---

## The five rules

Everything in this system descends from five non‑negotiables. When in doubt, re‑read this list before adding anything.

1. **Black, white, one green.** Every chromatic decision resolves to `#0a0a0a`, `#ffffff`, `#00c16a`, and the warm gray scale. If a design seems to need a second hue, it needs a second consideration instead.
2. **Two fonts: Syne (display ≥ 20px) and Manrope (everything else).** No exceptions. Syne never below 20px; Syne never for body copy.
3. **One green word per headline, one pulse dot per viewport.** Green is a signal, not a paint.
4. **Radii are binary.** `24px` on cards, `100px` on pills, `14px` on inputs. Do not introduce 4/6/8/12px rounded corners.
5. **No AI‑slop tropes.** No gradient‑stuffed hero backgrounds, no emoji, no rainbow charts, no rocket/moon copy, no "Learn more" CTAs, no stock photography. Ever.

If a proposed design violates one of these, the system is telling you to stop and redesign — not to override the rule.

---

## Getting started on a new surface

1. **Import the tokens first.** Every HTML file begins with:
   ```html
   <link rel="stylesheet" href="colors_and_type.css">
   ```
   This file is the single source of truth. Never hard‑code hex values, font sizes, or radii — always reach for a `var(--…)` token. If a value you need isn't in the token file, add it to the token file rather than inlining.

2. **Decide light or dark.** This system is dark‑primary. Default to `background: var(--black)` unless you have a specific reason (marketing mid‑sections, pricing, checkout). Light surfaces use `background: var(--white)` with the gray scale for hierarchy. **Never mix dark and light on the same fold** — transitions happen at section boundaries, never inside a card.

3. **Pick your type utilities, don't hand‑roll them.** Use `.t-display-1`, `.t-display-2`, `.t-lede`, `.t-body`, `.t-meta`, `.t-eyebrow`, `.t-label-caps`, `.t-wordmark`, and `.t-accent`. If you're writing `font-family: Syne…` by hand, you've gone off‑road.

4. **Reach for existing preview cards as references.** The `preview/` folder contains the definitive built examples. `preview/04-buttons.html` is the button spec. `preview/06-cards-lists.html` is the card spec. Open them side‑by‑side with your new surface.

5. **Never invent a new variant.** If you need a "secondary green," a "warning color," a "light card on dark," the answer is almost always: no. Re‑read the five rules. Ship with what's there.

---

## Composing a page

### Layout skeleton (marketing, long‑form)

```
nav (68px, dark, sticky, backdrop-blur)
hero (100px block padding, 50/50 grid, portrait right)
trust bar (light wash strip, 28px pad)
section light or dark (100px block padding)
testimonial (dark, 120px block padding, centered)
pricing (light, two‑plan grid)
footer (dark, 64px top pad)
```

Rhythm: dark → light → dark → dark → light → dark is the house cadence. **Alternate, don't gradient.** Transitions are abrupt; hard edges are the brand.

### Layout skeleton (reader app, dashboards)

```
sidebar 260px (fixed, #070707, nav + market widget + user)
topbar 68px (sticky, rgba(10,10,10,.96) + backdrop blur)
content area (1080px max, 48px/80px padding)
optional right rail 280px (sticky widgets)
```

Chrome is always `#070707` (one step darker than the canvas `#0a0a0a`). This creates the subtle elevation the reader app relies on without shadows.

### The 1200px page max
All marketing content sits inside `max-width: var(--page-max)` (1200px) with `padding: 0 var(--page-pad)` (80px). The reader app breaks this to 1080px for reading column comfort. Never exceed 1200px for any text‑primary surface.

### Section heads
Every H2 on marketing is preceded by a green eyebrow:
```html
<span class="eb">→ Today's dispatch</span>
<h2>What Tyler is watching before the open.</h2>
<p>Every morning at 7:15 ET. One thesis, one risk, one position change.</p>
```
The arrow glyph before the eyebrow text is part of the eyebrow; it's not a separate icon.

---

## Type — doing it right

### The pairing
- **Syne 800**: hero headlines, section H2s, prices, the wordmark, pull quotes.
- **Syne 700**: secondary display, card titles ≥ 24px, stat numerals ≥ 20px.
- **Manrope 700**: bold body, eyebrows, CTA labels, strong numerals in tables.
- **Manrope 600**: semi‑bold body, nav CTA, pill labels, author names.
- **Manrope 500**: nav links, default button labels, meta text.
- **Manrope 400**: body copy, lede, long‑form paragraphs.

### Headline composition
House pattern: `[White Syne] [green italic accent word] [white Syne]`.
- Exactly **one** green word per headline. Never two. Never a whole phrase.
- Green accent word takes `font-style: italic` — that's Syne italic doing the lifting.
- Tracking is `-0.03em` on `.t-display-1`, `-0.02em` on `.t-display-2`.

### Body
- 15px / 1.6 for interface body.
- 17px / 1.75 for long‑form (dispatches, deep‑dives) in the reader app.
- 18px / 1.75 for the hero lede, capped at `max-width: 440px`.
- Line‑lengths: 55–75ch for reading surfaces, `max-width: 560px` for section‑head descriptions.

### Numerals
Any column of numbers or a price/P&L gets:
```css
font-variant-numeric: tabular-nums;
```
Tickers stay `UPPERCASE` Syne. Prices stay tabular Manrope **unless** they're hero‑grade (Syne 800, `--fs-price: 56px`). Deltas use the **true minus** (`−`, U+2212), never a hyphen.

---

## Color — doing it right

### The green
`--green: #00c16a` is the *only* chromatic token. Its variants exist only for state:
- `--green-hover: #00e07a` — CTA hover only
- `--green-dim: #00a358` — pressed state, focus ring
- `--green-glow: rgba(0,193,106,.25)` — hero halo only
- `--green-mist: rgba(0,193,106,.06)` — atmospheric wash only

**Where green goes:**
- Primary CTA fill, primary CTA text (on dark)
- Section eyebrows (all caps labels)
- One accent word per hero headline (`.t-accent`)
- The `✓` in feature lists
- Pulse dot (max once per viewport)
- The halo glow behind the portrait
- Position P&L when positive
- Alert dots in the reader rail

**Where green does not go:**
- Body text backgrounds, container fills, or any text block fill
- Icons (use `currentColor`)
- Charts with more than one series (monochrome only)
- Nav links (these are `--on-dark-50`)
- Disabled states (use `--on-dark-30`)

### Negative deltas
For `−` deltas (e.g. `−0.82%`), use a muted rose `#ff8a8a` — **this is the one exception** to the three‑color rule, and it only appears in numeric deltas inside data surfaces (reader app, tables). Never use it elsewhere. Never name a token for it; inline it where needed with a comment.

### Gray scale on light
`--gray-50` page alt, `--gray-100` subtle rule, `--gray-200` input border, `--gray-400` eyebrow, `--gray-600` body muted, `--gray-800` near‑ink. Six steps. Don't invent in‑between values.

### Dark surface layering
On `--black` use the `--on-dark-*` scale:
- 92% white — primary body text on dark
- 85% white — list body
- 60% white — secondary text, footnote
- 50% white — nav links, quiet meta
- 30% white — disabled text
- 12% white — ghost borders
- 08% white — card borders, dividers
- 05% white — raised‑card fill on black

Cards on black are `--card-dark: #111` with `1px solid var(--on-dark-08)` border. No shadows on dark.

---

## Components — the canonical forms

### Buttons
- **Primary**: `--green` fill, `--black` text, `.r-pill` radius (100px), `10px 20px` pad (sm) / `16px 28px` pad (lg). Hover: `--green-hover` + `translateY(-1px)` (sm) / `(-2px)` (lg).
- **Outline (on dark)**: transparent, `1px solid var(--on-dark-12)`, white text. Hover: border `--on-dark-30`.
- **Outline (on light)**: transparent, `1px solid var(--gray-200)`, `--black` text. Hover: border `--black`.
- **Ghost**: no border, `--on-dark-85` color, hover `--white`. Nav only.
- **Never**: shadowed buttons, rounded‑square (4px) buttons, gradient buttons, icon‑only primary buttons.

CTA copy is always imperative: `Read today's dispatch →`, `Start 14‑day trial →`. Never `Learn more`, `Get started`, or `Click here`. The arrow `→` is part of the CTA.

### Inputs
- `14px` radius, `1px solid var(--gray-200)` on light / `1px solid var(--on-dark-12)` on dark.
- `12px 14px` padding, Manrope 500, 15px.
- Focus ring: `0 0 0 3px var(--green-mist)` + border `--green-dim`.
- Labels sit above, `.t-label-caps` style.

### Cards
- **On light**: `--white` fill, `1px solid var(--gray-200)`, `.r-card` (24px) radius, `48px` padding. No shadow.
- **On dark**: `--card-dark` (#111) fill, `1px solid var(--on-dark-08)` border, `.r-card` radius, `48px` padding. No shadow.
- **Raised callout**: same as on‑dark card but `1px solid var(--green)` for emphasis. Use once per page, max.

### The wordmark
Always the three parts together: dot + "Carta" (Syne 800) + "Advisory" (Syne 500, 55% opacity). The dot lives `10px` left of "Carta". Below 14px display, "Advisory" drops off and the mark becomes "• Carta". Never inside a button or pill.

### The pulsing dot
```html
<span class="pdot"></span>
```
```css
.pdot { width: 8px; height: 8px; background: var(--green);
  border-radius: 50%; animation: pulse 2s infinite; }
@keyframes pulse { 0%,100% { opacity:1; transform:scale(1) }
                   50% { opacity:.55; transform:scale(1.3) } }
```
**Once per viewport.** If the hero has one and the nav has one, kill the nav's.

---

## Data surfaces (reader app, dashboards)

Charts are **monochrome green on black**. One series. One labelled pivot (March pivot, 52w high, entry VWAP). Line weight `2px`, stroke `--green`, gradient fill from `.28` opacity to `0`. Reference lines are `rgba(255,255,255,.06)` dashed `2 4`. Never rainbow, never bar‑and‑line combos in marketing. Tables lean on `tabular-nums` + sparse horizontal rules (`--on-dark-08`) rather than zebra striping.

A position callout uses the `1px solid var(--green)` raised‑card treatment and three columns: label + stat copy / spacer / P&L stat. P&L number is Syne 800, 22px, `--green` for positive or `#ff8a8a` for negative.

---

## Motion

Four animations exist in this system. Do not add a fifth.

1. **`pulse`** — 2s ease on the green dot. Opacity `1 → .55 → 1`, scale `1 → 1.3 → 1`.
2. **`glow`** — 4s ease‑in‑out on the halo. Opacity `.85 → 1 → .85`, scale `1 → 1.05 → 1`.
3. **`float`** — 6s ease‑in‑out on the portrait. `translateY(0 → -10px → 0)`.
4. **Hover lift** — `.2s cubic-bezier(.2,.7,.2,1)` `translateY(-1px)` on sm CTAs, `-2px` on lg CTAs. Color transitions are also `.2s` on the same ease.

**No page‑load reveal animations.** No scroll‑triggered fades. No number count‑ups. No parallax. The brand's motion philosophy is *ambient*, not performative.

---

## Copy

Read the README's Voice & Tone section first. A quick checklist before you ship copy:

- [ ] Every CTA is `[verb] [noun] →` (not "Learn more", not "Get started")
- [ ] The hero headline is 6–9 words with exactly one green accent word
- [ ] The lede is one sentence, 18–28 words, ends on a concrete noun
- [ ] No emoji, no `!`, no "proprietary", "guaranteed", "crush", "10x"
- [ ] Tickers are `UPPERCASE`, never `$AAPL`
- [ ] Percents are tight: `3.2%`, not `3.2 %`
- [ ] Deltas use `+` and true `−` (U+2212), not hyphen
- [ ] Dates are `Apr 20, 2026`, never `04/20/26`
- [ ] Any performance claim links to the Important Disclosures footer anchor

---

## Extending the system

If you genuinely need a new component, ask these questions in order:

1. **Is it a rearrangement of existing pieces?** 90% of the time, yes — build it that way.
2. **Does it need a new color?** No, it doesn't. Reach for the gray scale or `--on-dark-*` before inventing.
3. **Does it need a new radius?** No. Use 24/100/14. A 16px "split the difference" is the slippery slope this system exists to prevent.
4. **Does it need a new font weight?** Check the scale. Syne has 700/800. Manrope has 400/500/600/700. If you want 900, you want Syne 800 at larger size.
5. **If you must add a token**, add it to `colors_and_type.css` with a comment explaining *why* it couldn't be expressed with existing tokens. Future designers should be able to trace the decision.

---

## Files in this system

```
colors_and_type.css     Tokens — import first, always.
README.md               Brand, voice, content fundamentals.
SKILL.md                This file — operating instructions.
preview/                Reviewable cards, one per concern.
  01-colors.html        Palette + on‑dark scale
  02-type.html          Syne + Manrope scale, pairings, hero spec
  03-spacing-radii.html 8pt scale, radii, shadows, grid, motion
  04-buttons.html       Primary/secondary/ghost/link, states, CTAs
  05-forms.html         Inputs, selects, checkbox, subscribe block
  06-cards-lists.html   Cards on light + dark, ticker rows, quotes
  07-iconography.html   Glyphs, pulse dot, halo, settings icons
  08-brand.html         Wordmark, clear space, photography, voice
kits/                   Full assembled surfaces.
  marketing.html        cartaadvisor.io landing page
  reader-app.html       Dispatch reader with position rail
```

When you build a new surface, place it in `kits/`, open the relevant `preview/` cards in a second tab, and work with both visible. That's the workflow.
