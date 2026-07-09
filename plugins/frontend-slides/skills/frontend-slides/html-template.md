# HTML Presentation Template

Reference architecture for generated decks. Every presentation is a fixed 16:9 stage: slides authored at 1920×1080, the whole stage scaled to the window. Styling is Tailwind utilities; raw CSS only in the three sanctioned blocks below.

## Base HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Presentation Title</title>

    <!-- Fonts: Fontshare or Google Fonts — never system fonts -->
    <link rel="stylesheet" href="https://api.fontshare.com/v2/css?f[]=...">

    <!-- Tailwind (CDN JIT — no build step) -->
    <script src="https://cdn.tailwindcss.com"></script>

    <!-- === DESIGN TOKENS ===
         The whole look is changed here: colors + fonts map to CSS variables
         so themes can be swapped (and regions inverted) at runtime. -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary:   'var(--bg-primary)',    // slide surface
                        secondary: 'var(--bg-secondary)',  // panel surface
                        ink:       'var(--text-primary)',  // primary text
                        muted:     'var(--text-secondary)',// secondary text
                        accent:    'var(--accent)',        // the one hot color
                    },
                    fontFamily: {
                        display: 'var(--font-display)',
                        body:    'var(--font-body)',
                    },
                    transitionTimingFunction: {
                        'out-expo': 'cubic-bezier(0.16, 1, 0.3, 1)',
                    },
                },
            },
        };
    </script>

    <style>
        /* === 1. TOKEN DEFINITIONS (values only — utilities reference these) === */
        :root {
            --bg-primary: #0a0f1c;
            --bg-secondary: #111827;
            --text-primary: #ffffff;
            --text-secondary: #9ca3af;
            --accent: #00ffcc;
            --font-display: 'Clash Display', sans-serif;
            --font-body: 'Satoshi', sans-serif;
        }

        /* === 2. STAGE MECHANICS === */
        /* --- PASTE viewport-base.css CONTENTS HERE, VERBATIM --- */

        /* === 3. CHOREOGRAPHY (state-scoped animation — can't be utilities) === */
        .reveal {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1),
                        transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .slide.visible .reveal { opacity: 1; transform: translateY(0); }
        .reveal:nth-child(1) { transition-delay: 0.1s; }
        .reveal:nth-child(2) { transition-delay: 0.2s; }
        .reveal:nth-child(3) { transition-delay: 0.3s; }
        .reveal:nth-child(4) { transition-delay: 0.4s; }
    </style>
</head>
<body>
    <div class="deck-viewport">
        <main class="deck-stage" id="deckStage">
            <!-- Slide 1: Title — layout: opening/offset-marquee -->
            <section class="slide active bg-primary text-ink">
                <h1 class="reveal absolute left-[96px] bottom-[380px] font-display text-[112px] font-bold leading-[0.95]">Presentation Title</h1>
                <p class="reveal absolute left-[96px] bottom-[300px] font-body text-[34px] text-muted">Subtitle or author</p>
            </section>

            <!-- Slide 2: ... -->
            <section class="slide bg-primary text-ink">
                <div class="absolute inset-[96px] flex flex-col gap-[32px]">
                    <h2 class="reveal font-display text-[64px] font-bold">Slide Title</h2>
                    <p class="reveal font-body text-[28px] text-muted">Content...</p>
                </div>
            </section>
        </main>
    </div>

    <script>
        /* === SLIDE PRESENTATION CONTROLLER === */
        class SlidePresentation {
            constructor() {
                this.slides = document.querySelectorAll('.slide');
                this.currentSlide = 0;
                this.stage = document.getElementById('deckStage');
                this.setupStageScale();
                this.setupKeyboardNav();
                this.setupTouchNav();
                this.showSlide(0);
            }

            setupStageScale() {
                const scale = () => {
                    const factor = Math.min(window.innerWidth / 1920, window.innerHeight / 1080);
                    const x = (window.innerWidth - 1920 * factor) / 2;
                    const y = (window.innerHeight - 1080 * factor) / 2;
                    this.stage.style.transform = `translate(${x}px, ${y}px) scale(${factor})`;
                };
                scale();
                window.addEventListener('resize', scale);
            }

            setupKeyboardNav() { /* Arrow keys, Space, Page Up/Down */ }
            setupTouchNav() { /* Touch/swipe support */ }

            showSlide(index) {
                this.currentSlide = Math.max(0, Math.min(index, this.slides.length - 1));
                this.slides.forEach((slide, i) => {
                    slide.classList.toggle('active', i === this.currentSlide);
                    slide.classList.toggle('visible', i === this.currentSlide);
                });
            }
        }

        new SlidePresentation();
    </script>
</body>
</html>
```

## Tailwind Rules for Decks

- All layout, spacing, typography, color, border, and effect styling goes in utility classes on the markup.
- Stage geometry uses arbitrary pixel values at the 1920×1080 design size: `left-[96px]`, `text-[168px]`, `w-[560px]`, `tracking-[0.18em]`.
- Token-based colors/fonts come from `tailwind.config` names (`bg-primary`, `text-accent`, `font-display`) — never hardcode a hex twice.
- Keep one semantic hook class per animated/JS-targeted element (`reveal`, `slide`); it carries zero visual styling.
- Never compose class names in JS (`bg-${color}` is invisible to the CDN JIT); toggle complete literal class strings.
- No spaces in arbitrary values — underscores instead: `shadow-[0_8px_32px_rgba(0,0,0,0.3)]`, `bg-[linear-gradient(135deg,#1a1a1a,#2d2d2d)]`.
- Invert a region by re-declaring the CSS variables on it: `class="[--bg-primary:#fff] [--text-primary:#111] bg-primary text-ink"`.
- Keyframes and `.slide.active`-triggered animations stay in the choreography `<style>` block; static transitions may use utilities (`transition`, `duration-500`, `ease-out-expo`).

## Required JavaScript Features

Every presentation includes:

1. **SlidePresentation class** — keyboard nav (arrows, Space, PgUp/PgDn), touch/swipe, mouse wheel, optional progress/page count outside the stage.
2. **Stage scaling** — all slides at 1920×1080 inside `.deck-stage`; one transform scales the whole stage; letterbox, never reflow.
3. **Optional enhancements** (match the style): custom cursor, canvas particles, parallax, 3D tilt, magnetic buttons, counter animations.
4. **Inline editing** (default post-draft) — see below.

## Inline Editing Implementation

Include by default; never ask pre-draft. Skip only if the user wants a locked/export-only file.

**Do NOT use the CSS `~` sibling-hover trick** — `pointer-events: none` on the toggle breaks the hover chain (button vanishes before it can be clicked). Use JS hover with a 400ms grace timeout.

HTML (visual styling in utilities; `show`/`active` toggled by JS):

```html
<div class="edit-hotzone fixed top-0 left-0 w-[80px] h-[80px] z-[10000] cursor-pointer"></div>
<button id="editToggle" title="Edit mode (E)"
        class="edit-toggle fixed top-[16px] left-[16px] z-[10001] opacity-0 pointer-events-none transition-opacity duration-300">✏️</button>
```

Choreography block (state classes only):

```css
.edit-toggle.show,
.edit-toggle.active { opacity: 1; pointer-events: auto; }
```

JS (four interaction paths):

```javascript
const hotzone = document.querySelector('.edit-hotzone');
const editToggle = document.getElementById('editToggle');
let hideTimeout = null;
const scheduleHide = () => {
    hideTimeout = setTimeout(() => {
        if (!editor.isActive) editToggle.classList.remove('show');
    }, 400);
};

editToggle.addEventListener('click', () => editor.toggleEditMode());          // 1. click toggle
hotzone.addEventListener('mouseenter', () => { clearTimeout(hideTimeout); editToggle.classList.add('show'); });
hotzone.addEventListener('mouseleave', scheduleHide);                          // 2. hover with grace period
editToggle.addEventListener('mouseenter', () => clearTimeout(hideTimeout));
editToggle.addEventListener('mouseleave', scheduleHide);
hotzone.addEventListener('click', () => editor.toggleEditMode());              // 3. hotzone click
document.addEventListener('keydown', (e) => {                                 // 4. E key (not while editing)
    if ((e.key === 'e' || e.key === 'E') && !e.target.getAttribute('contenteditable')) {
        editor.toggleEditMode();
    }
});
```

Editor features: contenteditable text on click, auto-save to localStorage, export/save-file function.

## Image Pipeline (Skip If No Images)

Requires `pip install Pillow`. Process before generating HTML; save with `_processed` suffix, never overwrite originals.

```python
from PIL import Image, ImageDraw

def crop_circle(input_path, output_path):          # logos on rounded/clean styles
    img = Image.open(input_path).convert('RGBA')
    w, h = img.size
    size = min(w, h)
    left, top = (w - size) // 2, (h - size) // 2
    img = img.crop((left, top, left + size, top + size))
    mask = Image.new('L', (size, size), 0)
    ImageDraw.Draw(mask).ellipse([0, 0, size, size], fill=255)
    img.putalpha(mask)
    img.save(output_path, 'PNG')

def resize_max(input_path, output_path, max_dim=1200):  # images > 1MB
    img = Image.open(input_path)
    img.thumbnail((max_dim, max_dim), Image.LANCZOS)
    img.save(output_path, quality=85)
```

| Situation | Operation |
| --- | --- |
| Square logo on rounded aesthetic | `crop_circle()` |
| Image > 1MB | `resize_max(max_dim=1200)` |
| Wrong aspect ratio | Manual `img.crop()` |

### Image Placement

Use direct relative paths (not base64) — presentations are viewed locally. Style with utilities:

```html
<img src="assets/logo_round.png" alt="Logo"
     class="max-w-full max-h-[200px] object-contain rounded-lg">
<img src="assets/screenshot.png" alt="Screenshot"
     class="max-w-full max-h-[400px] object-contain rounded-xl border border-white/10 shadow-[0_8px_32px_rgba(0,0,0,0.3)]">
```

- Adapt border/shadow colors to the style's accent token (`border-accent/20`).
- Never repeat an image across slides (except logos on title + closing).
- Patterns: logo centered on title; screenshots in two-column layouts; full-bleed backgrounds with overlay text (sparingly).

## Code Quality

- Comment every major section: `<!-- === SECTION NAME === -->` in HTML, `/* === ... === */` in the style/script blocks.
- Semantic HTML (`<section>`, `<nav>`, `<main>`); full keyboard navigation; ARIA labels where needed.
- `prefers-reduced-motion` support ships in viewport-base.css — keep it.

## File Structure

```
presentation.html    # Self-contained: Tailwind CDN + config, all JS inline
assets/              # Images only, if any
```

Multiple presentations in one project: `[name].html` + `[name]-assets/`.
