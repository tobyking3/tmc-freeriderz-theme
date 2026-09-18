# TMC Freeriderz — Build Plan

Living checklist for building the theme, section by section. Check items off as they're done; add/reorder sections as scope becomes clearer. See `CLAUDE.md` for the technical architecture this is built on.

## Phase 0 — Foundation

Blocks visual work on every section below, so goes first.

- [ ] Brand tokens (colors, fonts, spacing scale) — `src/tailwind.css` `@theme` block + `config/settings_schema.json` / `snippets/css-variables.liquid`
- [ ] Header (logo, nav, cart icon, mobile menu)
- [ ] Footer (links, social, newsletter signup)
- [ ] Base primitives (button snippet, typography styles)

## Phase 1 — Homepage, top to bottom

- [ ] Announcement bar (optional thin promo strip above header)
- [ ] Hero (main banner, Motion entrance animation, primary CTA)
- [ ] Value props (shipping/warranty/etc. — Lucide icons + short copy)
- [ ] Featured collection (product grid, Embla carousel on mobile)
- [ ] Category tiles ("shop by category")
- [ ] Brand story (image + copy, Motion scroll/fade)
- [ ] Best sellers / new arrivals (Embla carousel, reuse product-card component)
- [ ] Social proof (reviews or UGC gallery — note: needs a separate icon source for social/brand icons, Lucide doesn't have them)
- [ ] Newsletter signup (Alpine for inline validation/success state)

## Phase 2 — Cross-cutting (after homepage has real content)

- [ ] Predictive search (Fuse.js) in the header
- [ ] Scroll/page-transition polish with Motion across sections
- [ ] Responsive + accessibility pass
- [ ] `shopify theme check` clean
- [ ] Lighthouse / performance check

## Phase 3 — Seasonal "sub-store" architecture (later, not blocking Phase 1)

TMC's business is seasonal: **skiing (freestyle in particular) is the core year-round identity and main revenue driver**; skate/music/lifestyle categories carry the store through the summer off-season. Design direction (from the client): present the store as if it were split into separate department "sub-stores" (Ski / Skate / Music / Lifestyle) via top-level nav and department-specific landing pages — without actually creating multiple Shopify stores. The owner should be able to switch which department is the homepage's predominant face depending on season (e.g. a theme setting like "active department" / "season mode"), without restructuring the catalog or nav.

- [ ] Design the department nav/landing concept (Ski / Skate / Music / Lifestyle)
- [ ] Add a merchant-facing theme setting to control which department is "predominant" (drives homepage hero/featured content)
- [ ] Build out the non-ski department landing pages using that pattern

Explicitly deferred until the ski experience (Phases 0–2) is solid — don't start this until asked.

## Data-informed content (from Shopify sales analytics, trailing 365 days)

Confirmed via `run-analytics-query` (includes in-store POS sales, unified with online orders):

- **Armada ZERO Whitewalker 116** is the #1 ski by both revenue ($13.8k net) and order count (15) — over 2.5x the next-best ski. Strong candidate for hero/featured-product treatment.
- **Faction Prodigy** (Prodigy 2 + 3 combined, $9.3k net) is Faction's top-performing line, narrowly ahead of their Studio series.
- Non-ski volume worth keeping visible on the homepage: the in-house **TMC Beanie** and **Sunglasses** each had 170+ orders (high-volume, low-ticket) — supports keeping some lifestyle/accessory presence even while ski leads.
- Re-run this query periodically as the season progresses — best-sellers will shift, and this should inform which products get featured-collection/hero treatment.

## Notes

- Phase 0's brand tokens are blocked on brand direction (logo, palette, type) from the client.
- Ski (specifically freestyle/freeride) is the primary focus for all initial section work — see Phase 3 for how the other departments fit in later.
- **Brand asset libraries**: as a trusted retailer, the client has permission to use Faction's and Armada's official brand asset libraries (campaign photography, product shots, video) — access pending (client needs to obtain it). Once available, prefer this official imagery over anything we'd otherwise source/shoot for ski-related sections.
