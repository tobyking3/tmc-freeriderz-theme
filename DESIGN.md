# TMC Freeriderz — Design Direction

Visual/design brief, built from inspiration sites the client shared. See `BUSINESS.md` for the brand/business context this should express, and `BUILD_PLAN.md` for build sequencing.

> Living document — update as design decisions actually get made (once we're in Figma, treat that as the source of truth for specifics like exact hex values/type choices, and keep this page as the "why").

## Inspiration reviewed

| Site | Category | Standout pattern |
|---|---|---|
| [momentskis.com](https://www.momentskis.com/) | Ski brand (Reno, NV) | Full-bleed action hero, bold condensed uppercase type, dark cinematic "Factory" storytelling section, rounded pill buttons |
| [sungod.co](https://www.sungod.co/) | Performance eyewear | Split dual-photo hero, warm/cool color contrast, clean category cards with small pill tags |
| [factionskis.com](https://factionskis.com/en-gb) | Ski brand (Alps) | Minimalist black/white, sharp-edged outline buttons, "Ski Finder" quiz CTA, clean product grid with spec badges |
| [deorumski.com](https://www.deorumski.com/en-gb) | Ski poles/hardware (Vancouver) | Technical/boutique feel, monospace uppercase type, engineering-led copy, POV action video |
| [armadasnow.com](https://www.armadasnow.com/en-gb) | Ski/snowboard brand | **Split-screen department hero** (Ski / Snowboard, each own photo + CTA) — direct template for our seasonal sub-store concept. Neon lime-green accent on video UI. |
| [lineskis.com](https://lineskis.com/en-gb) | Ski brand (core/park) | Fisheye lens hero with blue vignette, zine-ish ticker copy ("SKI NERDS WELCOME!"), halftone/grainy photo treatment on category tiles |
| [volcom.co.uk](https://www.volcom.co.uk/) | Skate/streetwear | Grunge/spray-paint headline lettering, yellow/orange accent, clean product grid with wishlist hearts and sale-price treatment |

## Synthesized direction

Sit closer to **Moment / Armada / Line** (core mountain-culture, real athlete photography, bold condensed type) than **SunGod / Deorum** (clean performance-sport / boutique-technical) — TMC's identity (ski + skate + music/vinyl + street culture, 30 years of real Whistler history) calls for grittier, more authentic treatment than a polished performance-sport brand.

- **Type**: bold, heavy, condensed uppercase sans-serif for headlines (matches Moment/Armada/Line). A secondary monospace/technical face for meta text (specs, tickers, labels) — see Deorum/Line's ticker bar.
- **Photography**: full-bleed real action/athlete photography as the primary visual driver, not illustration or stock imagery. TMC has genuine assets to lean on — team athletes (Yuki Tsubota, Simon D'artois, Grete Eliassen), the 30th-anniversary story, the founder's own history. Prefer authentic/grainy over overly polished where it fits the culture.
- **Color**: no existing brand palette to preserve (confirmed with client). Recommend mostly black/white/grayscale — consistent with nearly every reference site — plus **one** deliberate accent color reserved for CTAs/highlights, not used decoratively. Exact color TBD in Figma; consider something that reads "mountain/snow" without clashing with the existing black logo (Armada's lime and Line's electric blue are useful reference points for how sparingly to use it).
- **Buttons**: lean toward Faction/Line/Armada's thin-outlined rectangular buttons over heavy filled or fully rounded pills — feels more "technical gear" than "consumer retail."
- **Product cards**: clean, low-chrome, white/light-gray background, a small spec or category badge (à la SunGod's pill tags or Deorum's expand icon) rather than heavy borders/shadows.
- **Department split-hero** (Armada's pattern): reserve this for Phase 3's seasonal sub-store nav — a homepage hero split between the currently-predominant department(s), each with its own photo/CTA, switchable by the owner per season.

## Open questions for Figma work

- Exact accent color (needs a swatch decision — TBD when we're in Figma with real assets to test against)
- Specific typeface choices (condensed display + mono/technical pairing — need to pick actual fonts, considering Shopify font-picker availability)
- How grainy/textured vs. clean the photography treatment should be (Line/Volcom's halftone grain vs. Moment/Faction's clean polish) — a middle ground is likely right given TMC's mix of premium ski gear and scrappy skate/music culture
