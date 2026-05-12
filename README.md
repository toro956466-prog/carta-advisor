# Carta Advisory — Design System

Carta Advisory is the premium market‑intelligence brand of **Tyler Ontiveros**, a portfolio‑manager‑turned‑educator. It is *not* Carta the cap‑table company; it is a subscription research product published at `cartaadvisor.io` aimed at retail traders, self‑directed investors, and finance creators. The brand sells **clarity in a loud market** — disciplined reads on equities, macro, and rates, delivered as a daily dispatch ("Active", $29/mo) and a premium desk ("Starter", $99/mo, with live alerts and model portfolios).

Everything in this system exists to make Tyler sound like the most composed person in the room. The voice is sober but never dry, confident without hype, and the visuals follow suit: a near‑black canvas, one emerald green accent, disciplined typography, and a total refusal of the gradient‑stuffed fintech cliché.

---

## PRODUCTS COVERED

This system dresses four surfaces, all of which ship from the `preview/` and `kits/` files:

| Surface | What it is |
|---|---|
| **Marketing site** (`cartaadvisor.io`) | Public pages — home, advisor bio, subscribe, thanks. Dark hero, light mid‑sections, dark footer. |
| **Dispatch emails** | The daily "Active" read and weekly deep‑dives. Rendered on `#0a0a0a` with the same type stack, slightly looser line-height. |
| **Reader web app** | Where subscribers read archived dispatches, manage alerts, and view model portfolios. Dark‑mode primary. |
| **Checkout / account** | Stripe‑driven subscribe flow + account management. Dark‑mode primary with card elevation. |

---

## CONTENT FUNDAMENTALS

> Write like a veteran PM briefing a room of smart non‑professionals. Short sentences. No jargon without a price tag attached. Never cheerlead.

### Voice
- **Composed.** Tyler has seen cycles. Copy reflects that — present‑tense, first‑person plural ("We watch the 10‑year, not the 10‑second"), zero exclamation points in product copy.
- **Specific before sweeping.** Lead with a number, a ticker, or a date. Claims earn generalities.
- **Dry humor, never cute.** A single wry aside per long read is allowed. Emojis are not.
- **Technical when warranted, translated always.** If we write "basis points," we write "(hundredths of a percent)" on first use.

### Tone by surface
| Surface | Tone |
|---|---|
| Hero / headline | Declarative, 6–9 words, one green accent word |
| Eyebrow / section label | 2–4 words, ALL CAPS, no period |
| Body lede under hero | 18–28 words, one sentence, ends on a concrete noun |
| Feature bullets | Start with a verb or a number. No closing period. |
| CTA | Imperative verb + noun ("Read today's dispatch", "Start the trial"). Never "Click here" or "Learn more" |
| Footnote / disclosure | Full sentences, period. This is where we sound like a lawyer, because we have to. |

### Numbers & tickers
- Tickers in `UPPERCASE` inline with prose, never wrapped in `$`: `AAPL`, `TLT`, `^VIX`.
- Percents use `%` glyph tight: `3.2%`, never `3.2 %` or `3.2pct`.
- Prices round to sensible precision — equity to 2dp, rates to 2dp, FX to 4dp.
- Basis‑point deltas prefer explicit sign: `+12 bps`, `−8 bps` (true minus, not hyphen).
- Use **tabular numerals** in tables and price stacks: `font-variant-numeric: tabular-nums`.

### Words we use
watch • read • dispatch • desk • signal • thesis • position • size • risk • context

### Words we don't
crush • moon • rocket • secret • guaranteed • easy • passive income • 10x • literally • game‑changer

### Copy guardrails
- **Never promise returns.** Every page that implies performance links to the `Important Disclosures` footer anchor.
- **No testimonial without a real name + publicly visible handle.**
- **Currency is USD** unless the dispatch is explicitly macro/FX.
- **Dates are `Apr 20, 2026`**, never `04/20/26`. The reader is often international.

---

## VISUAL FOUNDATIONS

### The three‑color rule
The palette is **black, white, one green** — and nothing else. Any chart, badge, or illustration must resolve to that set (plus the warm gray scale). If a design feels like it needs a second hue, it needs a second consideration instead.

- **Black `#0a0a0a`** is the primary brand surface. It is warm, not cool — 10/10/10 sits softer on OLED than pure `#000` and does not vibrate next to the green.
- **White `#ffffff`** is the light‑mode canvas, used for mid‑page "zoom out" sections on the marketing site and for card text on dark.
- **Green `#00c16a`** is the only chromatic color. Use it for: primary CTAs, the pulsing eyebrow dot, one accent word per hero headline, the `✓` in feature lists, and the radial glow behind the hero portrait. **Never** as a body‑text background or fill behind long copy.

### Gray scale
Six steps, warm, pulled from the marketing site. Resist adding intermediate values.

`#f9f9f9 → #f0f0f0 → #e2e2e2 → #999 → #555 → #222 → #0a0a0a`

On dark surfaces, text layers are rgba white at `.92 / .85 / .60 / .50 / .30 / .12 / .08 / .05` — see `--on-dark-*` tokens.

### Typography
Two families, used with discipline.

- **Syne** (`700`, `800`) — display only. Headlines, prices, wordmark. Always tight tracking (`-.02` to `-.03em`), always ≥ 20px. Never body.
- **Manrope** (`400`, `500`, `600`, `700`) — everything else. Body, nav, pills, labels, numerals, forms.

Body copy lives at 15px / 1.6. The hero lede is 18px / 1.75 (never wider than 440px). Headlines fluid‑scale via `clamp()` so the hero never shrinks below 44px or exceeds 72px. All caps labels get `+0.10–0.12em` tracking; display headlines get `-0.02 to -0.03em`.

### Space, radius, elevation
- **Radii** are binary: `24px` cards, `100px` pills, `14px` inputs. The system does not use 4/6/8px rounded rectangles.
- **Section rhythm** on marketing is `100px` block padding with `80px` horizontal gutters, capped at a `1200px` content max.
- **Elevation** exists only twice: the hero portrait gets a dual drop‑shadow (`0 20px 40px rgba(0,0,0,.4)` + `0 0 60px rgba(0,193,106,.15)`), and raised cards on dark sit on `#111` with a `1px rgba(255,255,255,.08)` border. No shadows on light surfaces.

### Motion
Motion is atmospheric, never interruptive. Two ambient loops — a `pulse` on the green eyebrow dot and a slow `float` on the hero image — plus a `glow` breathe on the halo. Interactive elements use `.2s` color transitions and a `−2px translate` on CTA hover. Use `cubic-bezier(.2,.7,.2,1)` as the house ease. **No page‑load reveal animations.**

### Layout primitives
- **Fixed 68px dark nav** with `rgba(10,10,10,.96)` + `backdrop-filter: blur(12px)`.
- **50/50 hero grid** on desktop (portrait right), collapses to stacked on narrow viewports.
- **Trust bar** strip between hero and content — light gray wash with bordered white pills.
- **Section eyebrow** — green `11px` caps label above every H2.
- **Card on dark** — `#111` fill, `24px` radius, `48px` padding, `rgba(255,255,255,.08)` border.

---

## ICONOGRAPHY

Carta Advisory **does not use a drawn icon set.** Instead, iconography in this system is three things:

1. **Typographic glyphs** — `→` for forward actions, `✓` for list affirmations, `−` (true minus) and `+` for deltas. All set in Manrope so they visually weld to adjacent text.
2. **The pulsing dot** — a `8px` green circle with a 2s opacity/scale pulse. It is the system's only "live" signifier and appears at most once per viewport (hero eyebrow, market‑open indicator, live‑alert badge).
3. **The halo** — a soft radial green glow behind the hero portrait and any hero‑grade product shot. It is not decoration; it is the brand's one visual flourish. Recipe: `radial-gradient(circle, rgba(0,193,106,0.25) 0%, rgba(0,193,106,0.08) 40%, transparent 70%)` on a 520px round, 20px blur, breathing at 4s.

If a future surface genuinely needs line icons (settings panels, table toolbars), use a **1.5px stroke, 24px frame, square caps, rounded joins, no fills**, all rendered in `currentColor`. The icon must read correctly at 20px without anti‑alias tricks. Do not introduce colored icons.

### Photography & imagery
The single portrait of Tyler is the brand's anchor image. Additional imagery, when needed, follows:
- **Subject shot on a near‑black backdrop**, lit from one side, clean silhouette.
- **Charts as imagery** — when an equities chart is the visual, it is monochrome green on black, with a single labelled pivot. No rainbow multi‑series charts in marketing surfaces.
- **No stock photography.** Never.

---

## FILES IN THIS SYSTEM

```
colors_and_type.css     # All design tokens. Import this first.
preview/                # Reviewable design-system cards (one per concern)
  01-colors.html
  02-type.html
  03-spacing-radii.html
  04-buttons.html
  05-forms.html
  06-cards-lists.html
  07-iconography.html
  08-brand.html
kits/                   # Full UI mockups assembled from the system
  marketing.html
  reader-app.html
assets/                 # Brand assets (logos, portrait)
SKILL.md                # Operating instructions for designers using this system
```
