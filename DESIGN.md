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

- **Type**: **Anton** for headlines — bold, condensed, heavy weight matching Moment/Armada/Line's actual headline treatment (chosen over Bebas Neue, which read too thin/light at weight, and Archivo Black, which isn't condensed and reads more streetwear-wordmark than ski-race). **Inter** for body/UI text (clean, highly legible, pairs well against Anton's heaviness). **Space Mono** for meta/technical text — specs, tickers, labels — per Deorum/Line's ticker-bar pattern.
- **Photography**: full-bleed real action/athlete photography as the primary visual driver, not illustration or stock imagery. TMC has genuine assets to lean on — team athletes (Yuki Tsubota, Simon D'artois, Grete Eliassen), the 30th-anniversary story, the founder's own history. Prefer authentic/grainy over overly polished where it fits the culture.
- **Color**: no existing brand palette to preserve (confirmed with client). Base palette is black/white/grayscale — consistent with nearly every reference site — plus **Alpenglow (`#FF5B3D`)** as the single accent color, reserved for CTAs/highlights, not used decoratively. Chosen over Avalanche Orange (too close to safety-gear orange), Glacier Blue (too close to what most competitor ski brands already use), and Neon Lime (too skate/core-coded for the ski-first launch, though worth reconsidering later for the skate department once Phase 3 happens).
- **Buttons**: lean toward Faction/Line/Armada's thin-outlined rectangular buttons over heavy filled or fully rounded pills — feels more "technical gear" than "consumer retail."
- **Product cards**: clean, low-chrome, white/light-gray background, a small spec or category badge (à la SunGod's pill tags or Deorum's expand icon) rather than heavy borders/shadows.
- **Department split-hero** (Armada's pattern): reserve this for Phase 3's seasonal sub-store nav — a homepage hero split between the currently-predominant department(s), each with its own photo/CTA, switchable by the owner per season.

## Figma

Design work is happening in Figma: https://www.figma.com/design/6fG9hOnYM5mb5rfmOQVbT0 ("TMC Freeriderz — Homepage Design"). Treat that file as the source of truth for specifics (exact spacing, component layout) once sections start getting built there — this doc stays the "why."

## Open questions

- How grainy/textured vs. clean the photography treatment should be (Line/Volcom's halftone grain vs. Moment/Faction's clean polish) — a middle ground is likely right given TMC's mix of premium ski gear and scrappy skate/music culture. Revisit once we have real photography (own shots or the Faction/Armada asset libraries) to test against.
