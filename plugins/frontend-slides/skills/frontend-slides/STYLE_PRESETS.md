# Style Presets Reference

Curated visual styles for Frontend Slides — real design references, no generic "AI slop." **Abstract shapes only — no illustrations.**

Each preset ships its tokens as a `tailwind.config` `theme.extend.colors` object; use them as utilities (`bg-primary`, `text-accent`). Gradients and patterns are applied as arbitrary-value utilities. Mandatory stage mechanics: [viewport-base.css](viewport-base.css), pasted verbatim into every deck.

---

## Dark Themes

### 1. Bold Signal

**Vibe:** Confident, bold, modern, high-impact
**Layout:** Colored card on dark gradient; number top-left, navigation top-right, title bottom-left.
**Typography:** Display `Archivo Black` (900) · Body `Space Grotesk` (400/500)

```js
colors: { primary: '#1a1a1a', card: '#FF5722', ink: '#ffffff', 'on-card': '#1a1a1a' }
```

Background: `bg-[linear-gradient(135deg,#1a1a1a_0%,#2d2d2d_50%,#1a1a1a_100%)]`

**Signature:** bold colored focal card (orange/coral); large section numbers (01, 02); breadcrumbs with `opacity-40`/`opacity-100` states; strict grid alignment.

---

### 2. Electric Studio

**Vibe:** Bold, clean, professional, high contrast
**Layout:** Split panel — white top, blue bottom; brand marks in corners.
**Typography:** Display `Manrope` (800) · Body `Manrope` (400/500)

```js
colors: { dark: '#0a0a0a', paper: '#ffffff', accent: '#4361ee', ink: '#0a0a0a', light: '#ffffff' }
```

**Signature:** two-panel vertical split; accent bar on panel edge; quote typography as hero; minimal confident spacing.

---

### 3. Creative Voltage

**Vibe:** Bold, creative, energetic, retro-modern
**Layout:** Split panels — electric blue left, dark right; script accents.
**Typography:** Display `Syne` (700/800) · Mono `Space Mono` (400/700)

```js
colors: { primary: '#0066ff', dark: '#1a1a2e', accent: '#d4ff00', light: '#ffffff' }
```

**Signature:** electric blue + neon yellow contrast; halftone textures; neon badges/callouts; script type for flair.

---

### 4. Dark Botanical

**Vibe:** Elegant, sophisticated, artistic, premium
**Layout:** Centered content on dark; abstract soft shapes in a corner.
**Typography:** Display `Cormorant` (400/600, serif) · Body `IBM Plex Sans` (300/400)

```js
colors: { primary: '#0f0f0f', ink: '#e8e4df', muted: '#9a9590',
          warm: '#d4a574', pink: '#e8b4b8', gold: '#c9b896' }
```

**Signature:** blurred overlapping gradient circles (`blur-3xl`); warm accents (pink/gold/terracotta); thin vertical accent lines (`w-px`); italic signature type; **abstract CSS shapes only**.

---

## Light Themes

### 5. Notebook Tabs

**Vibe:** Editorial, organized, elegant, tactile
**Layout:** Cream paper card on dark background; colorful tabs on the right edge.
**Typography:** Display `Bodoni Moda` (400/700) · Body `DM Sans` (400/500)

```js
colors: { outer: '#2d2d2d', page: '#f8f6f1', ink: '#1a1a1a',
          'tab-mint': '#98d4bb', 'tab-lavender': '#c7b8ea', 'tab-pink': '#f4b8c5',
          'tab-sky': '#a8d8ea', 'tab-cream': '#ffe6a7' }
```

**Signature:** paper card with soft shadow; vertical-text section tabs on the right edge; binder-hole decorations on the left.

---

### 6. Pastel Geometry

**Vibe:** Friendly, organized, modern, approachable
**Layout:** White card on pastel background; vertical pills on the right edge.
**Typography:** Display + Body `Plus Jakarta Sans` (400/500/700/800)

```js
colors: { primary: '#c8d9e6', card: '#faf9f7', 'pill-pink': '#f0b4d4', 'pill-mint': '#a8d4c4',
          'pill-sage': '#5a7c6a', 'pill-lavender': '#9b8dc4', 'pill-violet': '#7c6aad' }
```

**Signature:** rounded card + soft shadow; right-edge vertical pills at constant width with varying heights (short → medium → tall → medium → short); corner action icon.

---

### 7. Split Pastel

**Vibe:** Playful, modern, friendly, creative
**Layout:** Two-color vertical split (peach left, lavender right).
**Typography:** Display + Body `Outfit` (400/500/700/800)

```js
colors: { peach: '#f5e6dc', lavender: '#e4dff0', ink: '#1a1a1a',
          'badge-mint': '#c8f0d8', 'badge-yellow': '#f0f0c8', 'badge-pink': '#f0d4e0' }
```

**Signature:** split background colors; playful badge pills with icons; grid-pattern overlay on the right panel; rounded CTA buttons.

---

### 8. Vintage Editorial

**Vibe:** Witty, confident, editorial, personality-driven
**Layout:** Centered content on cream; abstract geometric accent shapes.
**Typography:** Display `Fraunces` (700/900, serif) · Body `Work Sans` (400/500)

```js
colors: { cream: '#f5f3ee', ink: '#1a1a1a', muted: '#555555', warm: '#e8d4c0' }
```

**Signature:** geometric shapes (circle outline + line + dot); bold bordered CTA boxes; witty conversational copy; **geometric CSS shapes only**.

---

## Specialty Themes

### 9. Neon Cyber

**Vibe:** Futuristic, techy, confident
**Typography:** `Clash Display` + `Satoshi` (Fontshare)

```js
colors: { primary: '#0a0f1c', accent: '#00ffcc', magenta: '#ff00aa' }
```

**Signature:** canvas particles, neon glow (`shadow-[0_0_24px_rgba(0,255,204,0.4)]`), grid patterns.

---

### 10. Terminal Green

**Vibe:** Developer-focused, hacker aesthetic
**Typography:** `JetBrains Mono` only

```js
colors: { primary: '#0d1117', accent: '#39d353' }
```

**Signature:** scan lines, blinking cursor, code-syntax styling.

---

### 11. Swiss Modern

**Vibe:** Clean, precise, Bauhaus-inspired
**Typography:** `Archivo` (800) + `Nunito` (400)

```js
colors: { paper: '#ffffff', ink: '#000000', accent: '#ff3300' }
```

**Signature:** visible grid, asymmetric layouts, geometric shapes.

---

### 12. Paper & Ink

**Vibe:** Editorial, literary, thoughtful
**Typography:** `Cormorant Garamond` + `Source Serif 4`

```js
colors: { cream: '#faf9f7', ink: '#1a1a1a', accent: '#c41e3a' }
```

**Signature:** drop caps, pull quotes, elegant horizontal rules.

---

## Font Pairing Quick Reference

| Preset | Display font | Body font | Source |
| --- | --- | --- | --- |
| Bold Signal | Archivo Black | Space Grotesk | Google |
| Electric Studio | Manrope | Manrope | Google |
| Creative Voltage | Syne | Space Mono | Google |
| Dark Botanical | Cormorant | IBM Plex Sans | Google |
| Notebook Tabs | Bodoni Moda | DM Sans | Google |
| Pastel Geometry | Plus Jakarta Sans | Plus Jakarta Sans | Google |
| Split Pastel | Outfit | Outfit | Google |
| Vintage Editorial | Fraunces | Work Sans | Google |
| Neon Cyber | Clash Display | Satoshi | Fontshare |
| Terminal Green | JetBrains Mono | JetBrains Mono | JetBrains |

---

## DO NOT USE (Generic AI Patterns)

- **Fonts:** Inter, Roboto, Arial, or system fonts as display type.
- **Colors:** `#6366f1` generic indigo; purple gradients on white.
- **Layouts:** everything centered, generic hero sections, identical card grids.
- **Decorations:** realistic illustrations, gratuitous glassmorphism, purposeless drop shadows.

---

## Tailwind Gotchas

- **Negating CSS functions:** a leading `-` before a function is silently dropped — write `right-[calc(-1*clamp(28px,3.5vw,44px))]`, never `-clamp(...)`.
- **Spaces in arbitrary values break the class:** use underscores — `bg-[linear-gradient(135deg,#1a1a1a,#2d2d2d)]`, `shadow-[0_8px_32px_rgba(0,0,0,0.3)]`.
- **Dynamic class names are invisible to the CDN JIT:** never build `bg-${color}` in JS; toggle complete literal strings.
- **Config fonts must match the loaded font name exactly:** `fontFamily: { display: '"Clash Display", sans-serif' }`.
