# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm start        # Dev server: Eleventy with live reload + PostCSS watch (use this throughout the course)
npm run build    # Production build: clean dist, compile Eleventy + CSS with NODE_ENV=production
npm run css      # Compile CSS via PostCSS only (no Eleventy)
npm run clean    # Remove and recreate dist/
npm run patterns:create  # CLI generator for new pattern/component stubs
```

No test runner is configured — this is a CSS learning project.

## Architecture Overview

This is a static site built with [Eleventy](https://www.11ty.dev/) using the [CUBE CSS methodology](https://cube.fyi/) and a design token system that feeds both Tailwind CSS and CSS Custom Properties.

### CSS Layer Order (CUBE CSS)

PostCSS assembles `src/css/global.css` by importing these layers in order:

1. **Global** (`src/css/global/`) — reset, fonts, base element styles, CSS custom property declarations
2. **Compositions** (`src/css/compositions/`) — layout primitives (flow, cluster, grid, sidebar, switcher, wrapper, repel)
3. **Utilities** (`src/css/utilities/`) — single-purpose helpers
4. **Blocks** (`src/css/blocks/`) — component-scoped styles; these are intentionally empty stubs to be filled in during the course

### Design Token Pipeline

```
src/design-tokens/*.json
  → src/css-utils/tokens-to-tailwind.js  → tailwind.config.js (Tailwind utilities)
  → (Eleventy data)                       → CSS Custom Properties via src/css/global/variables.css
```

Tokens cover: colors, fonts, spacing, text sizes/weights/leading, viewports. `clamp-generator.js` produces fluid `clamp()` values for responsive scaling.

### Pattern Library

`src/pattern-library/patterns/` contains 16 UI patterns (button, card, hero, masthead, nav, etc.). Each pattern folder can have multiple variants. The `patterns:create` script scaffolds new patterns. Patterns are rendered via the `pattern.njk` macro and surfaced in the Eleventy-built pattern library at `/pattern-library/`.

### Templating

Eleventy uses Nunjucks (`.njk`) templates in `src/_includes/layouts/` and `src/_includes/macros/`. Data for the pattern library sidebar and tokens is provided via `src/_data/design/`.

### Output

All built files go to `dist/`. The `dist/` directory is wiped on each `npm run clean` / `npm run build`.
