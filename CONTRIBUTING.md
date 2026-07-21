# Contributing to Frontend Slides

Thanks for wanting to help! This project grows one template and one layout preset at a time, and both are **markdown-only contributions** — you don't need to write JavaScript to make a real difference.

## The two most valuable contributions

### 1. A new bold template

Templates live in `bold-template-pack/templates/<slug>/` and consist of two files:

- `preview.md` — a small style card: palette, fonts, mood/tone metadata, and a "visual snapshot" paragraph. This is what the agent reads when shortlisting styles.
- `design.md` — the full design system: colors, type stack, composition rules, decoration language, and per-layout guidance.

The easiest way to start is to copy an existing template (e.g. `templates/coral/`) and study its structure. Then:

1. Pick a distinctive aesthetic that isn't already covered (check `selection-index.json` for the current range of moods).
2. Write `design.md` first, then distill `preview.md` from it.
3. Add your template's entry to `bold-template-pack/selection-index.json`.
4. Generate at least one test deck with the skill using your template, and include a screenshot in your PR so reviewers can see it in action.

**Quality bar:** templates should feel like a designed system, not a color swap — a committed palette, a deliberate type pairing, and a recognizable compositional signature.

### 2. A new layout preset

Layout presets live in `layout-presets/<category>/` and are style-agnostic structural blueprints: they fix where everything sits on the 1920×1080 stage while colors/fonts stay swappable.

1. Check the existing categories (opening, section, list, stats, quote, comparison, timeline, …) for gaps.
2. Copy the structure of an existing preset in the closest category.
3. Describe the composition precisely: regions, sizes, alignment, and how content scales with more/fewer items.
4. Test it with at least two different visual styles to prove it's genuinely style-agnostic.

## Other welcome contributions

- **Bug fixes** to the scripts (`extract-pptx.py`, `deploy.sh`, `export-pdf.sh`)
- **Docs improvements** — clearer install steps, agent-specific setup notes
- **Example decks** for the demo gallery (`docs/demos/`)

## Ground rules

- One template or preset per PR, please — it keeps review fast.
- Match the tone and structure of existing files; the agent parses these, so consistency matters.
- Templates adapted from elsewhere must be properly credited and license-compatible (this repo is MIT).
- By contributing you agree your contribution is licensed under the MIT license.

## Questions?

Open an issue — questions are welcome, and "is this template idea worth building?" is a perfectly good issue.
