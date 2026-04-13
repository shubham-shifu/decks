# Deck Design System

> Extracted from the Sana Goals deck. Use this as the canonical reference when generating any new HTML slide deck.

---

## 1. Fonts

| Role | Family | Google Fonts Import |
|------|--------|-------------------|
| Primary (all text) | `'DM Sans', sans-serif` | `DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400` |
| Monospace (labels, tags, data) | `'DM Mono', monospace` | `DM+Mono:wght@300;400` |

```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=DM+Mono:wght@300;400&display=swap" rel="stylesheet">
```

### Typography Scale

| Element | Size | Weight | Line-height | Letter-spacing | Notes |
|---------|------|--------|-------------|----------------|-------|
| `h1` | 2.6rem | 300 (light) | 1.15 | -0.03em | Use `<strong>` for 600 weight emphasis |
| `h2` | 1.6rem | 300 (light) | 1.25 | -0.02em | Use `<strong>` for 600 weight emphasis |
| `h3` (card) | 1rem | 500 | 1.3 | — | |
| `.subtitle` | 1rem | 300 | 1.55 | — | max-width: 36em |
| Card body `p` | 0.88rem | 300 | 1.5 | — | |
| `.slide-num` | 0.75rem | 300 | — | 0.15em | DM Mono, uppercase |
| `.card-label` | 0.68rem | 400 | — | 0.12em | DM Mono, uppercase |
| Tags/pills | 0.56–0.58rem | 400 | — | 0.05em | DM Mono, uppercase |
| Wireframe text | 0.74–0.8rem | 300–400 | — | — | |
| Base `html` | 18px | — | — | — | Root font size |

---

## 2. Color Palette

### CSS Custom Properties (copy directly into `:root`)

```css
:root {
  /* Base */
  --bg: #FAFAF8;
  --fg: #1A1A18;
  --muted: #636360;
  --card: #FFFFFF;
  --border: #E8E8E4;
  --soft: #F2F2EE;

  /* Accent: Teal */
  --teal: #0F8A6B;
  --teal-bg: #E6F5F0;

  /* Accent: Coral */
  --coral: #D85A30;
  --coral-bg: #FDF0EB;

  /* Accent: Amber */
  --amber: #B8750F;
  --amber-bg: #FDF5E8;

  /* Accent: Purple */
  --purple: #6B5CE7;
  --purple-bg: #F0EEFE;

  /* Accent: Blue */
  --blue: #2356D8;
  --blue-bg: #EEF2FD;

  /* Accent: Red */
  --red: #C42B2B;
  --red-bg: #FDE9E9;

  /* Slide dimensions */
  --slide-w: 1080px;
}
```

### Color Usage Guide

| Purpose | Color | Hex |
|---------|-------|-----|
| Page background | warm off-white | `#FAFAF8` |
| Primary text | near-black | `#1A1A18` |
| Secondary/muted text | warm gray | `#636360` |
| Cards | white | `#FFFFFF` |
| Borders | light warm gray | `#E8E8E4` |
| Soft backgrounds (callouts, hover) | pale warm gray | `#F2F2EE` |
| Wireframe borders/dividers | | `#DEDED8` |
| Inactive dots/dim values | | `#C4C3BC` |
| Dot hover | | `#7A7972` |
| Mac window buttons | red `#FF5F57`, yellow `#FEBC2E`, green `#28C840` | |

### Accent Color Pairings (foreground + background)

Each accent has a strong foreground and a tinted light background:

| Name | Foreground | Background | Typical Use |
|------|-----------|------------|-------------|
| Teal | `#0F8A6B` | `#E6F5F0` | Success, current state, positive |
| Coral | `#D85A30` | `#FDF0EB` | Yearly markers, warm highlights |
| Amber | `#B8750F` | `#FDF5E8` | Warnings, gaps, alternatives |
| Purple | `#6B5CE7` | `#F0EEFE` | Decisions needed, past items |
| Blue | `#2356D8` | `#EEF2FD` | Proposals, active/current, primary actions |
| Red | `#C42B2B` | `#FDE9E9` | Errors, blocks, mismatches |

---

## 3. Layout System

### Slide Structure

```
body (100vh, overflow hidden)
  .deck (full viewport, relative)
    .slide (absolute, full size, centered flex)
      .slide-inner (max-width: 1080px or 90vw, max-height: 90vh, padding: 2.5rem 0)
```

- Only one `.slide.active` is visible at a time
- Inactive slides: `opacity: 0`, `pointer-events: none`, `transform: translateY(16px)`
- Active slides: `opacity: 1`, `pointer-events: auto`, `transform: translateY(0)`
- Transition: `opacity 0.45s ease, transform 0.45s ease`

### Grid Layouts

| Class | Columns | Gap | Use Case |
|-------|---------|-----|----------|
| `.cards.cards-2` | `1fr 1fr` | 1rem | Two equal cards |
| `.cards.cards-3` | `1fr 1fr 1fr` | 1rem | Three equal cards |
| `.two-col` | `1fr 1fr` | 2rem | Content + wireframe side-by-side |

---

## 4. Components

### Card (`.card`)

```css
background: var(--card);       /* #FFFFFF */
border: 1px solid var(--border); /* #E8E8E4 */
border-radius: 12px;
padding: 1.3rem 1.4rem;
```

**Accent variant** (`.card-accent`): adds a 3px colored left border + extra left padding (1.2rem). Apply color class: `.teal`, `.amber`, `.coral`, `.purple`, `.blue`.

**Top-accent variant** (inline style): `border-top: 2.5px solid var(--color)` for feature/option cards.

### Card Label (`.card-label`)

```css
font-family: 'DM Mono', monospace;
font-size: 0.68rem;
letter-spacing: 0.12em;
text-transform: uppercase;
margin-bottom: 0.55rem;
font-weight: 400;
color: [matching accent color via inline style];
```

### Callout (`.callout`)

```css
padding: 0.8rem 1rem;
background: var(--soft);       /* #F2F2EE */
border-radius: 10px;
margin-top: 1rem;
/* Text: 0.88rem, muted, weight 300. Strong: weight 500, fg color */
```

### Row List (`.row-list` > `.row-item`)

```css
/* Container */
display: flex; flex-direction: column; gap: 0.7rem; margin-top: 1.4rem;

/* Item */
display: flex; align-items: baseline; gap: 1rem;
padding: 0.85rem 1.1rem;
background: var(--card);
border: 1px solid var(--border);
border-radius: 10px;

/* Label inside */ .ri-label: DM Mono, 0.7rem, uppercase, letter-spacing 0.1em, muted, width 8rem
/* Text inside */  .ri-text: 0.92rem, weight 400, fg color, line-height 1.4
```

### Slide Number (`.slide-num`)

```css
font-family: 'DM Mono', monospace;
font-size: 0.75rem;
letter-spacing: 0.15em;
text-transform: uppercase;
color: var(--muted);
margin-bottom: 1.4rem;
font-weight: 300;
```

Format: `"01 — Slide title"` or `"Sana · Goals · subtitle"`

### Navigation Bar (`.nav`)

```css
position: fixed; bottom: 1.5rem; left: 50%; transform: translateX(-50%);
display: flex; align-items: center; gap: 1rem;
background: var(--card);
border: 1px solid var(--border);
border-radius: 40px;
padding: 0.5rem 0.8rem;
box-shadow: 0 4px 20px rgba(0,0,0,0.06);
z-index: 100;
```

**Nav buttons**: 36x36px circle, transparent bg, hover `var(--soft)`, disabled at `opacity: 0.2`

**Nav dots**: 10x10px circles, `#C4C3BC` default, hover `#7A7972`, active: `var(--fg)` + `width: 24px` + `border-radius: 10px` (pill shape)

---

## 5. Wireframe Components (for UI mockups within slides)

### Wireframe Container (`.wf`)

```css
background: #F5F4F0;
border: 1px solid #DEDED8;
border-radius: 12px;
overflow: hidden;
font-size: 0.8rem;
box-shadow: 0 2px 12px rgba(0,0,0,0.05);
```

### Wireframe Title Bar (`.wf-bar`)

```css
background: #ECEAE5;
border-bottom: 1px solid #DEDED8;
padding: 0.5rem 0.9rem;
display: flex; align-items: center; gap: 0.5rem;
```

Contains Mac traffic light dots (9x9px circles: `#FF5F57`, `#FEBC2E`, `#28C840`) and a caption in DM Mono 0.6rem.

### Wireframe Input (`.wf-input`)

```css
background: var(--card);
border: 1px solid #DEDED8;
border-radius: 7px;
padding: 0.42rem 0.65rem;
font-size: 0.78rem;
```

States:
- `.filled`: `border-color: #B0C8F8; background: #FAFCFF`
- `.empty`: `color: #B0AFA8` (placeholder style)
- `.disabled`: `background: var(--soft); color: var(--muted)`

### Tags (`.wf-tag`)

```css
font-family: 'DM Mono', monospace;
font-size: 0.56rem;
letter-spacing: 0.05em;
text-transform: uppercase;
padding: 2px 6px;
border-radius: 4px;
```

| Class | Background | Color |
|-------|-----------|-------|
| `.tag-past` | `#EDE8FE` | `#6B5CE7` |
| `.tag-now` | `var(--blue-bg)` | `var(--blue)` |
| `.tag-soon` | `var(--soft)` | `var(--muted)` + 1px border |

### Counter (`.wf-counter`)

```css
display: flex; justify-content: space-between; align-items: center;
padding: 0.45rem 0.65rem; border-radius: 7px;
font-size: 0.75rem; font-weight: 500;
```

| Class | Background | Color |
|-------|-----------|-------|
| `.counter-ok` | `var(--teal-bg)` | `var(--teal)` |
| `.counter-warn` | `var(--amber-bg)` | `var(--amber)` |
| `.counter-err` | `var(--red-bg)` + 1px `#F0C0C0` border | `var(--red)` |

### Flag (`.wf-flag`)

```css
padding: 0.45rem 0.65rem; border-radius: 7px;
font-size: 0.75rem; line-height: 1.4;
display: flex; gap: 0.4rem; align-items: flex-start;
```

| Class | Background | Color |
|-------|-----------|-------|
| `.flag-err` | `var(--red-bg)` | `var(--red)` |
| `.flag-ok` | `var(--teal-bg)` | `var(--teal)` |
| `.flag-info` | `var(--blue-bg)` | `var(--blue)` |
| `.flag-warn` | `var(--amber-bg)` | `var(--amber)` |

### Buttons (`.wf-btn`)

```css
display: inline-block;
padding: 0.28rem 0.65rem;
border-radius: 5px;
font-size: 0.7rem;
font-weight: 500;
border: 1px solid;
```

| Class | Background | Color | Border |
|-------|-----------|-------|--------|
| `.btn-ghost` | `var(--soft)` | `var(--muted)` | `var(--border)` |
| `.btn-blue` | `var(--blue-bg)` | `var(--blue)` | `#C0D0F8` |
| `.btn-primary` | `var(--blue)` | `white` | `var(--blue)` |

### Pills (`.pill`)

```css
font-family: 'DM Mono', monospace;
font-size: 0.58rem;
padding: 2px 7px;
border-radius: 4px;
letter-spacing: 0.05em;
font-weight: 400;
white-space: nowrap;
```

| Class | Background | Color |
|-------|-----------|-------|
| `.pill-block` | `var(--red-bg)` | `var(--red)` |
| `.pill-auto` | `var(--teal-bg)` | `var(--teal)` |
| `.pill-warn` | `var(--amber-bg)` | `var(--amber)` |
| `.pill-info` | `var(--blue-bg)` | `var(--blue)` |

### Progress Bar (`.pbar`)

```css
height: 4px; background: #DEDED8; border-radius: 2px; overflow: hidden;
/* Fill: .pfill height 100%, border-radius 2px */
/* Colors: .pfill-teal, .pfill-amber, .pfill-blue */
```

### Tree View (goal hierarchy display)

```css
.tree-row { display: flex; align-items: center; gap: 0.55rem; padding: 0.42rem 0.5rem; border-radius: 6px; font-size: 0.79rem; }
.tree-row:hover { background: #EEECEA; }
.tree-row.year { font-weight: 500; font-size: 0.84rem; }
.tree-row.quarter { padding-left: 1.5rem; }
.tree-row.month { padding-left: 3rem; font-size: 0.74rem; color: var(--muted); }
```

Tree dots: `.dot-y` coral 7px, `.dot-q` blue 7px, `.dot-m` teal 5px

Tree values: DM Mono 0.66rem, `.good` teal, `.warn` amber, `.dim` `#C4C3BC`

Badges: DM Mono 0.56rem, padding 2px 7px, border-radius 4px
- `.badge-auto`: amber-bg/amber
- `.badge-you`: teal-bg/teal
- `.badge-soon`: soft/muted + border
- `.badge-lock`: soft/muted + border

### Edge Case Table (`.ec-table`)

```css
width: 100%; border-collapse: collapse;
th: DM Mono, 0.62rem, uppercase, letter-spacing 0.1em, muted, padding 0.5rem 0.8rem, border-bottom
td: 0.82rem, padding 0.6rem 0.8rem, border-bottom, line-height 1.4
td:first-child: weight 400, fg color, width 35%
td:last-child: muted, weight 300
```

### Carry Forward Options (`.carry-opt`)

```css
border: 1px solid var(--border); border-radius: 9px;
padding: 0.8rem 1rem; background: var(--card);
display: flex; gap: 0.8rem; align-items: flex-start;
/* Selected: border-color var(--blue), background var(--blue-bg) */
/* h4: 0.84rem weight 500, p: 0.78rem muted weight 300 line-height 1.45 */
```

---

## 6. Animations

### Fade-Up (`.fade-up`)

Applied to direct children of `.slide-inner`. Only animates when parent slide has `.active`.

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(8px); }
  to   { opacity: 1; transform: translateY(0); }
}

.slide.active .fade-up {
  animation: fadeUp 0.45s ease both;
}

/* Staggered delays for sequential reveal */
.slide.active .fade-up:nth-child(2) { animation-delay: 0.07s; }
.slide.active .fade-up:nth-child(3) { animation-delay: 0.13s; }
.slide.active .fade-up:nth-child(4) { animation-delay: 0.19s; }
.slide.active .fade-up:nth-child(5) { animation-delay: 0.25s; }
.slide.active .fade-up:nth-child(6) { animation-delay: 0.31s; }
```

### Slide Transition

```css
.slide {
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.45s ease, transform 0.45s ease;
  transform: translateY(16px);
}
.slide.active {
  opacity: 1;
  pointer-events: auto;
  transform: translateY(0);
}
```

### Button/Dot Transitions

- Nav buttons: `transition: background 0.15s`
- Nav dots: `transition: all 0.2s`

---

## 7. Slide Content Patterns

### Title Slide (Slide 0)
- Slide number line (brand + context): `"Sana · Goals · a proposal for [Name]"`
- `h1` with `<strong>` for emphasis on key phrase
- `.subtitle` paragraph
- 3-column accent cards summarizing the deck: Current State (teal), The Gap (amber), The Proposal (blue)

### Content Slide (Slides 1-8)
- Slide number: `"01 — Descriptive title"`
- `h2` with `<strong>` emphasis
- `.subtitle` for context
- Body: cards grid, two-col layout with wireframes, row-list, tables, or option cards
- Optional `.callout` at bottom for key takeaway

### Summary/Close Slide (Slide 9)
- Slide number: `"09 — Summary"`
- `h1` (not h2) for closing emphasis
- `.subtitle`
- 2-column cards: Today (teal) vs Plan (blue)
- `.callout` with next step CTA

---

## 8. Slide JavaScript (Navigation)

```javascript
const slides = document.querySelectorAll('.slide');
const dotsEl = document.getElementById('dots');
let cur = 0;

// Generate dots
slides.forEach((_, i) => {
  const d = document.createElement('button');
  d.className = 'nav-dot' + (i === 0 ? ' active' : '');
  d.onclick = () => goTo(i);
  dotsEl.appendChild(d);
});

function goTo(n) {
  slides[cur].classList.remove('active');
  dotsEl.children[cur].classList.remove('active');
  cur = n;
  slides[cur].classList.add('active');
  dotsEl.children[cur].classList.add('active');
  document.getElementById('prev').disabled = cur === 0;
  document.getElementById('next').disabled = cur === slides.length - 1;
}

function go(dir) {
  if (cur + dir >= 0 && cur + dir < slides.length) goTo(cur + dir);
}

// Keyboard navigation
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight' || e.key === 'ArrowDown') go(1);
  if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') go(-1);
});
```

---

## 9. Design Principles (inferred)

1. **Warm neutrals** — background is warm off-white (#FAFAF8), not cold gray. Borders and muted tones follow the same warmth.
2. **Light weight typography** — headings default to weight 300 (light). Bold (600) is used sparingly via `<strong>` for emphasis within headings.
3. **Monospace for metadata** — all labels, tags, numbers, and status indicators use DM Mono. This creates a clear visual hierarchy separating data from prose.
4. **Color = meaning** — each accent color maps to a semantic role (teal=positive, amber=warning, blue=active/proposal, red=error, purple=decision). Background tints use the same hue at ~10% opacity.
5. **Minimal shadows** — only the nav bar and wireframes have shadows. Cards use borders, not elevation.
6. **Subtle animation** — fade-up with 8px translateY, staggered at 70ms intervals. Nothing bounces or overshoots.
7. **Single-file HTML** — everything (CSS, JS, content) lives in one self-contained HTML file. No external dependencies beyond Google Fonts.
8. **Always mobile responsive** — every deck MUST be mobile responsive. Use the breakpoints and rules below.

---

## 10. Mobile Responsiveness (REQUIRED)

Every deck must include these responsive styles. All grids collapse to single column on mobile. Typography scales down. Navigation remains usable on touch.

### Breakpoints

| Breakpoint | Target |
|-----------|--------|
| `max-width: 768px` | Tablets and small screens |
| `max-width: 480px` | Mobile phones |

### Responsive CSS (copy into every deck)

```css
/* ── RESPONSIVE ── */
@media(max-width:768px){
  html{font-size:16px}
  .slide-inner{padding:1.5rem 1rem}
  h1{font-size:1.8rem}
  h2{font-size:1.3rem}
  .cards-2,.cards-3{grid-template-columns:1fr}
  .two-col{grid-template-columns:1fr;gap:1.2rem}
  .flow{flex-direction:column;align-items:stretch}
  .flow-arrow{transform:rotate(90deg);text-align:center;padding:.2rem 0}
  .nav{padding:.4rem .6rem;gap:.6rem}
  .nav-dots{gap:5px}
  .nav-dot{width:8px;height:8px}
  .nav-dot.active{width:18px}
  .ec-table{font-size:.75rem}
  .ec-table th,.ec-table td{padding:.4rem .5rem}
  .do-dont{grid-template-columns:1fr}
  .row-item{flex-direction:column;gap:.3rem}
  .row-item .ri-label{width:auto}
  .q-card{flex-direction:column;gap:.4rem}
}
@media(max-width:480px){
  html{font-size:15px}
  h1{font-size:1.5rem}
  h2{font-size:1.15rem}
  .subtitle{font-size:.88rem}
  .card{padding:1rem 1.1rem}
  .slide-inner{padding:1.2rem .8rem}
  .nav button{width:32px;height:32px;font-size:.85rem}
}
```

### Rules

1. All multi-column grids (`.cards-2`, `.cards-3`, `.two-col`) collapse to `1fr` (single column) at 768px
2. Font sizes scale down: h1 from 2.6rem → 1.8rem → 1.5rem, h2 from 1.6rem → 1.3rem → 1.15rem
3. Row items (`.row-item`) stack vertically — label on top, text below
4. Flow diagrams go vertical with rotated arrows
5. Navigation stays fixed at bottom, dots shrink slightly
6. Touch targets remain at least 32px for accessibility
