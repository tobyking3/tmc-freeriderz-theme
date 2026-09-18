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

## Notes

- Phase 0's brand tokens are blocked on brand direction (logo, palette, type) from the client.
