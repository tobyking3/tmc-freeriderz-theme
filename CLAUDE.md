# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> This is a living document — as sections/blocks get built out, conventions solidify, or the design system takes shape, update this file rather than letting it drift out of date. The "Current status" section at the bottom in particular should be kept current.

See `BUILD_PLAN.md` for the section-by-section build checklist, `BUSINESS.md` for what TMC Freeriderz actually is as a business (history, positioning, reputation, brand voice), and `DESIGN.md` for the visual direction distilled from client-supplied inspiration sites — read all three before making design or copy decisions.

## Project

A Shopify theme for the client store **TMC Freeriderz** (`tmcfreeriderz-com.myshopify.com`), built **from scratch** on Shopify's minimal **Skeleton theme** (`github.com/Shopify/skeleton-theme`) rather than a full-featured starting point like Horizon — this was a deliberate choice so the project isn't fighting an existing framework's own component system/design tokens, and is free to use whatever frontend libraries fit.

- Sibling folder `../horizon-inspiration` is a clone of Shopify's Horizon theme, kept purely as a design/pattern reference (its own `CLAUDE.md` documents Horizon's architecture) — it is not part of this project and shares no code with it.
- Remote: `git@github.com:tobyking3/tmc-freeriderz-theme.git` (private). CI (`.github/workflows/ci.yml`) runs Theme Check on every push.

## Commands

- `shopify theme dev --store tmcfreeriderz-com.myshopify.com` — local dev server: builds, watches, and hot-reloads Liquid/CSS/JS against a development theme on the store.
- `npm run css:watch` — Tailwind CLI in watch mode, compiling `src/tailwind.css` → `assets/tailwind.css`. Run this **alongside** `shopify theme dev` (separate terminal) whenever editing markup that uses Tailwind classes — the dev server doesn't compile Tailwind itself, it just syncs whatever `assets/tailwind.css` currently contains.
- `npm run css:build` — one-off minified Tailwind build (use before committing/pushing, so the committed `assets/tailwind.css` reflects the latest classes used).
- `shopify theme check` — lints the theme (Liquid/schema correctness, best practices, unused-snippet warnings, etc.). Run before pushing.
- `shopify theme push` / `shopify theme pull` — push/pull theme files to/from the store.

`npm install` is required once (installs `tailwindcss` + `@tailwindcss/cli` as dev dependencies — `node_modules` is gitignored). There's no other build tooling — Liquid, and all vendored JS in `assets/`, ship as-is with no bundling.

## Architecture

### Layout grid (`assets/critical.css`)

Every section wrapper gets `.shopify-section`, which establishes a 3-column CSS grid (`--content-grid: var(--content-margin) var(--content-width) var(--content-margin)`) constraining content to `var(--page-width)` with `var(--page-margin)` gutters. A section's direct children default to the center column (`grid-column: 2`); give a child the `full-width` class to span the full viewport instead (used for hero/background-image sections — see `sections/custom-section.liquid`). This is the theme's core layout primitive — new sections should lean on it rather than re-inventing page-width/gutter logic.

### Design tokens

Currently minimal and Skeleton-default, defined in `config/settings_schema.json` and turned into CSS custom properties by `snippets/css-variables.liquid` (rendered once, early in `layout/theme.liquid`): `--font-primary--family/style/weight`, `--page-width`, `--page-margin`, `--color-background`, `--color-foreground`, `--style-border-radius-inputs`. This is intentionally sparse — there's no elaborate palette/typography system yet (contrast Horizon's much larger token set, documented in `../horizon-inspiration/CLAUDE.md`, for what a fuller system looks like if this one needs to grow that way). Expect to expand `config/settings_schema.json` + `css-variables.liquid` together as TMC Freeriderz's actual brand/design system gets defined.

### Sections, blocks, snippets

Same underlying Shopify theme-block platform conventions as any modern theme:

- Sections/blocks need a `{% schema %}`; blocks and non-trivial snippets should have a `{% doc %}` header (see `blocks/group.liquid`, `snippets/image.liquid` for the pattern — `@param`/`@example` tags).
- Section/block `name`/`label` strings use `t:` references into `locales/en.default.schema.json`.
- `block.shopify_attributes` must be output on a block's root element for the theme editor's drag-and-drop to work.
- A section/block can accept any theme block generically via `"blocks": [{ "type": "@theme" }]` (see `blocks/group.liquid`, `sections/custom-section.liquid`) instead of enumerating specific types.
- Per-component CSS lives in a `{% stylesheet %}` tag in the same file — parameterize per-instance values via inline `style="--x: {{ value }}"` custom properties rather than generating whole rules in Liquid.

Only two blocks (`group`, `text`) and a handful of demo sections exist so far — this is the Skeleton default set, not yet TMC-specific.

### Styling: Tailwind + `{% stylesheet %}` coexist

Two valid approaches, use whichever fits:

- **Tailwind utility classes directly in markup** — the default for layout, spacing, one-off styling. Source is `src/tailwind.css` (`@import 'tailwindcss'` + `@source` globs pointing at `sections/blocks/snippets/templates/layout`); compiled output is `assets/tailwind.css`, linked in `layout/theme.liquid`. Extend the theme (colors, fonts, etc.) via the `@theme { ... }` block already stubbed in `src/tailwind.css`.
- **`{% stylesheet %}` + CSS custom properties** — for settings-driven values that need to come from a section/block's schema (a merchant-configurable color, spacing, etc.), where a Tailwind class can't express a dynamic value. Skeleton's own sections (`hello-world`, `header`, `footer`, `custom-section`) use this pattern; keep using it for that specific case.

`assets/tailwind.css` is committed (not gitignored) — Shopify serves theme assets as-is, there's no build step at deploy time, so the compiled CSS must be up to date in the repo before pushing/committing.

### JavaScript: no bundler, import map + vendored libraries

`snippets/scripts.liquid` declares an `importmap` and is rendered in `layout/theme.liquid`. All JS dependencies are vendored as pinned, self-hosted single-file ES modules in `assets/` (no CDN at runtime, no `node_modules` shipped to the browser):

| Import specifier | File | Notes |
|---|---|---|
| `@vendor/motion` | `assets/motion.js` | Named exports: `animate`, `animateMini`, `createScopedAnimate`, `delay`, `inView`, `scroll`, `scrollInfo`. Depends on `motion-dom`/`motion-utils` (also in the import map — don't remove those entries even if nothing imports them directly). |
| `@vendor/embla-carousel` | `assets/embla-carousel.js` | Default export: `import EmblaCarousel from '@vendor/embla-carousel'`. |
| `@vendor/alpinejs` | `assets/alpinejs.js` | Default export, already booted globally in `scripts.liquid` (`window.Alpine = Alpine; Alpine.start()`) — don't call `Alpine.start()` again elsewhere. Use `x-data` etc. directly in markup. |
| `@vendor/fuse` | `assets/fuse.js` | Default export: `import Fuse from '@vendor/fuse'`. |

**Adding a new vendored library**: fetch its pinned single-file ESM bundle (e.g. `https://cdn.jsdelivr.net/npm/<pkg>@<version>/+esm`), save it flat in `assets/` (Shopify's `assets/` directory does **not** support subfolders), add an entry to the import map in `snippets/scripts.liquid`. If the bundle itself imports another package via a bare/absolute specifier (check with `grep -oE 'from"[^"]+"' assets/<file>.js`), that package needs vendoring and mapping too — this is exactly how `motion-dom`/`motion-utils` ended up as separate entries alongside `@vendor/motion`.

### Icons — two coexisting patterns

- **Skeleton's originals**: `assets/icon-account.svg`, `assets/icon-cart.svg`, inlined via `{{ 'icon-account.svg' | inline_asset_content }}` (see `sections/header.liquid`).
- **Lucide set** (added for this project): 16 icons as individual snippets (`snippets/icon-<name>.liquid`), rendered through a dispatcher — `{% render 'icon', name: 'shopping-cart', class: 'size-5' %}` (see `snippets/icon.liquid` for the full list and instructions on adding more). Source: `lucide-static@1.47.0`. Note Lucide has no brand/social icons (Instagram, Facebook, etc. — dropped for trademark reasons); source those separately if needed.

Prefer the Lucide/dispatcher pattern for new work; the two Skeleton icons can be migrated over if/when `header.liquid` gets rebuilt.

## Current status

- Homepage (`templates/index.json`) still renders Skeleton's placeholder `hello-world` section — no real design work has started yet.
- `header`, `footer`, `product`, `cart`, `collection`, etc. are all Skeleton's bare-bones defaults, unstyled beyond structural necessity.
- Tailwind/Motion/Embla/Alpine/Fuse/Lucide are wired and verified working (headless-browser smoke test confirmed `window.Alpine` boots via the import map, Tailwind CSS loads, no console errors from any vendored library) — but nothing in the actual theme uses them yet.
