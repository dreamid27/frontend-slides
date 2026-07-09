# Animation Patterns Reference

Match animations to the intended feeling. Static styling is Tailwind utilities; state-triggered animation (`.slide.visible …`) lives in the choreography `<style>` block.

## Effect-to-Feeling Guide

| Feeling | Animations | Visual cues |
| --- | --- | --- |
| **Dramatic / Cinematic** | Slow fades (1–1.5s), scale 0.9→1, parallax | Dark backgrounds, spotlights, full-bleed images |
| **Techy / Futuristic** | Neon glow (shadow utilities), glitch/scramble text, grid reveals | Canvas particles, grid patterns, mono accents, cyan/magenta |
| **Playful / Friendly** | Bouncy easing, floating/bobbing | Rounded corners, pastel/bright colors |
| **Professional / Corporate** | Subtle fast transitions (200–300ms) | Navy/slate/charcoal, precise spacing, data focus |
| **Calm / Minimal** | Very slow subtle motion, gentle fades | Whitespace, muted palette, serif type |
| **Editorial / Magazine** | Staggered text reveals, image-text interplay | Strong hierarchy, pull quotes, serif headlines + sans body |

## Entrance Animations (choreography block)

Hidden state + transition on the hook class; `.slide.visible` reveals. Variants differ only in the hidden transform:

```css
/* Fade + slide up (most versatile) */
.reveal        { opacity: 0; transform: translateY(30px);
                 transition: opacity 0.6s cubic-bezier(0.16,1,0.3,1),
                             transform 0.6s cubic-bezier(0.16,1,0.3,1); }
.reveal-scale  { opacity: 0; transform: scale(0.9);      transition: /* same */; }
.reveal-left   { opacity: 0; transform: translateX(-50px); transition: /* same */; }
.reveal-blur   { opacity: 0; filter: blur(10px);
                 transition: opacity 0.8s, filter 0.8s cubic-bezier(0.16,1,0.3,1); }

.slide.visible :is(.reveal, .reveal-scale, .reveal-left, .reveal-blur) {
    opacity: 1; transform: none; filter: none;
}
```

Stagger with utilities on each element: `class="reveal delay-100"`, `delay-200`, or arbitrary `[transition-delay:0.35s]`.

## Background Effects (Tailwind utilities)

```html
<!-- Gradient mesh — layered radial gradients for depth -->
<div class="absolute inset-0 bg-primary
            bg-[radial-gradient(ellipse_at_20%_80%,rgba(120,0,255,0.3)_0%,transparent_50%),radial-gradient(ellipse_at_80%_20%,rgba(0,255,200,0.2)_0%,transparent_50%)]"></div>

<!-- Grid pattern — subtle structural lines -->
<div class="absolute inset-0
            bg-[linear-gradient(rgba(255,255,255,0.03)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.03)_1px,transparent_1px)]
            bg-[size:50px_50px]"></div>

<!-- Noise texture — inline SVG grain as a data URI -->
<div class="absolute inset-0 opacity-20 bg-[url('data:image/svg+xml,...')]"></div>
```

Remember: no spaces inside arbitrary values — use underscores.

## Interactive Effects

```javascript
/* 3D tilt on hover — adds depth to cards/panels */
class TiltEffect {
    constructor(element) {
        this.element = element;
        this.element.style.transformStyle = 'preserve-3d';
        this.element.style.perspective = '1000px';
        this.element.addEventListener('mousemove', (e) => {
            const rect = this.element.getBoundingClientRect();
            const x = (e.clientX - rect.left) / rect.width - 0.5;
            const y = (e.clientY - rect.top) / rect.height - 0.5;
            this.element.style.transform = `rotateY(${x * 10}deg) rotateX(${-y * 10}deg)`;
        });
        this.element.addEventListener('mouseleave', () => {
            this.element.style.transform = 'rotateY(0) rotateX(0)';
        });
    }
}
```

## Troubleshooting

| Problem | Fix |
| --- | --- |
| Utility classes have no effect | Check the Tailwind CDN `<script>` loads; verify class names are literal strings, never built in JS |
| Arbitrary value ignored | Remove spaces (`bg-[size:50px_50px]`, not `50px 50px`); check bracket syntax |
| Fonts not loading | Check the Fontshare/Google Fonts URL; font names in `tailwind.config` must match exactly |
| Animations not triggering | Verify `.visible` is being toggled on the active slide; hook classes must match the choreography block |
| Mobile issues | Never add breakpoints inside slides — the stage scales as a whole; reduce particle counts on small devices |
| Performance issues | Animate only `transform`/`opacity`; use `will-change` sparingly; throttle scroll handlers |
