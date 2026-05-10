# Evidensi — Landing Page Documentation

**Figma file key:** `Xa8ciHpM5cgesS4mNenvFW`  
**Canvas node:** `4059:10603` (Gradual build - node page)  
**Last updated:** 2026-05-10  
**Stack:** Semantic HTML5 · Plain CSS · No JavaScript · Vercel static deploy

---

## 1. File Structure

```
evidensi/
├── index.html              — semantic HTML, all 8 page sections
├── styles.css              — all layout, typography, colour (no framework)
├── vercel.json             — { "outputDirectory": "." }
├── qa-report.md            — per-revision pixel-match log (revs 1–6)
├── Documentation.md        — this file
└── assets/
    ├── arrow-blue.svg          — 3×6px chevron, stroke #06678A (SIGN UP btn)
    ├── arrow-white.svg         — 4×7px chevron, stroke #FFFFFF (hero CTA btn)
    ├── arrow-apply.svg         — 3×6px chevron, stroke #055E74 (Framework Apply btn)
    ├── arrow-teal-4x7.svg      — 4×7px chevron, stroke #055E74 (BFB GET EARLY ACCESS btn)
    ├── arrow-white-3x6.svg     — 3×6px chevron, stroke #FFFFFF (Governance Apply btn)
    ├── burger-menu.svg         — 22×17px hamburger icon
    ├── hero-bg.png             — scattered dots background (rendered at 30% opacity)
    ├── bfb-public-bg.png       — blob watermark, "For the public" card
    ├── bfb-professionals-bg.png — blob watermark, "For professionals" card
    ├── hiw-does-bg.png         — checkmark circle watermark, "What it does" card
    └── hiw-doesnot-bg.png      — X circle watermark, "What it does NOT do" card
```

---

## 2. Design System

### 2.1 Typography

| Token | Font | Size | Weight | Line-height | Usage |
|---|---|---|---|---|---|
| Logo | Tilt Warp | 26px | 400 | 1.262 | "evidensi" logotype |
| Slogan | Tinos | 8px | 400 | 1.15 | "EVIDENCE STRENGTH INSIGHTS" |
| H1 | Tinos | 34px | 400 | 1.235 | Hero heading |
| H2 (teal modules) | Tinos | 31–32px | 400 | 1.25–1.387 | Module headings on coloured bg |
| H2 (white/grey modules) | Tinos | 32px | 400 | 1.25 | BFB, HIW, Governance headings |
| Card title | Tinos | 26px | 400 / **700** | 1.15 | BFB and HIW card titles; bold via characterStyleOverride |
| Module label | ABeeZee | 12px | 400 | 2.5 | Section eyebrow labels (7px letter-spacing) |
| Subtitle | Tinos | 15px | 400 | 1.15 | Hero "*STARTING WITH NUTRITION…" |
| Body | Inter | 16px | 400 | 1.625 | Body copy throughout |
| CTA copy line 1 | Inter | 16px | **700** | 1.625 | "Methodology expert?" (Framework + Governance) |
| CTA copy line 2 | Inter | 16px | 400 | 1.875 | Sub-copy below "Methodology expert?" |
| Grey teaser | Inter | 16px | 400 | 1.875 | Methodology Expert teaser section |
| Button label | Inter | 14px | 600 | 1.714 | All CTA/apply buttons |
| Footer links | Inter | 16px | 400 | 1.5 | Sign up / Contact / Privacy |
| Footer note/copy | Inter | 14px | 400 | 1.21 | Disclaimer + copyright |
| SIGN UP / BFB btn | Inter | 12–14px | 600 | 1.21–1.714 | Header SIGN UP (12px), BFB button (14px) |

All fonts loaded via Google Fonts (`ABeeZee`, `Tilt Warp`, `Tinos`, `Inter`).

### 2.2 Colour Palette

| Name | Hex | Usage |
|---|---|---|
| Teal primary | `#06678A` | Buttons backgrounds, teal text accents |
| Teal dark | `#055E74` | BFB/Framework apply button text, HIW card title |
| Teal mid | `#056B8B` | Governance CTA text |
| Teal gradient start | `#028191` | Framework module gradient |
| Teal gradient end | `#085A86` | Framework module gradient |
| HIW gradient start | `#0499B1` | How It Works module gradient |
| HIW gradient end | `#68C7C7` | How It Works module gradient |
| Pill magenta | `#B30377` | "currently in development" pill |
| Off-white | `#F3F3F0` | Methodology Expert teaser + BFB module bg |
| Dark body | `#1E2939` | Hero description text, grey teaser text |
| Black | `#000000` | Main body text, H2, labels |
| Footer dark | `#323232` + gradient | Footer dark background |
| Footer gradient | `rgba(102,102,102,0)` → `rgba(29,29,29,1)` at 152° | Overlay on footer |

### 2.3 Spacing System

All spacing directly from Figma layout tokens. Key values:

- **Page container max-width: `1440px`** — pixel-confirmed from 3000px Figma artboard (Framework module renders at 360px at 0.25× = 1440px actual; MCP YAML reports `horizontal: fill` but does not expose the max-width constraint)
- Module padding (most sections): `30–40px top, 45px bottom, 20px sides`
- Inter-element gap within modules: `22–29px`
- Card inner padding: `25px 20px 30–40px`
- Card corner radius: `20px`
- Button corner radius: `3px`
- Page container box-shadow: `0px 4px 30px 0px rgba(0,0,0,0.05)`

---

## 3. Page Structure & HTML Hierarchy

```
.page-wrapper
└── .page-container
    ├── .thematic-grouping          — subtle white gradient bg
    │   ├── header.header
    │   └── section.hero-section    — hero bg image via ::before pseudo-element
    ├── section.frame-method-expert — off-white teaser strip
    ├── section.module-framework    — teal gradient module
    ├── section.module-builtforboth — off-white module
    ├── section.module-howitworks   — teal gradient module
    ├── section.module-governance   — white module
    └── footer.footer               — dark gradient footer
```

---

## 4. Module Implementation Notes

### Header
- Three-column flex row: burger icon (56px) · logo+slogan stack (146px) · SIGN UP button
- Logo sits in a `position: relative` wrapper; slogan is `position: absolute` bottom-anchored into the logo frame's bottom padding
- `@media (max-width: 359px)`: `gap` reduced from 10px → 5px to prevent header wrap at 320px

### Hero Section
- Hero background image rendered via `::before` pseudo-element at `opacity: 0.3` — this matches Figma's image fill intent without the image being a layout element
- CTA button is **inside** `.hero-section` (structural deviation from Figma hierarchy) so the hero `::before` background visually covers the button area
- H1, subtitle, description each have their own padding to control spacing (no `gap` on parent — matches Figma's "no gap" auto-layout)

### Methodology Expert Teaser
- Plain `background: #F3F3F0` strip; text is Inter (pixel-confirmed via 4× Figma render — MCP YAML incorrectly reports Tinos due to characterStyleOverride)
- `<strong>` on "Methodology expert?" → Inter 700; link text → Inter 400 regular

### Evidensi Framework Module
- Dual-stop linear gradient: `136deg, #028191 11%, #085A86 100%`
- CTA copy uses display:block `<span>` elements to produce different line-heights per line:
  - `.module-cta-q` → Inter 700, line-height 1.625
  - `.module-cta-sub` → Inter 400, line-height 1.875
- Apply button: white bg, teal text (`#055E74`), `arrow-apply.svg` icon

### Built For Both Module
- Cards constrained to `max-width: 600px` — MCP YAML reports `horizontal: fill` but pixel measurement of Figma renders confirms the cap (card x=212–811 at 1024px viewport = 600px wide)
- Card background images (`bfb-public-bg.png`, `bfb-professionals-bg.png`) via `background-image` on `.bfb-card-body`
- GET EARLY ACCESS button: white bg, teal text, `arrow-teal-4x7.svg` icon

### How It Works Module
- Dual-stop linear gradient: `136deg, #0499B1 11%, #68C7C7 100%`
- Card watermark background images (`hiw-does-bg.png`, `hiw-doesnot-bg.png`) — near-white on white, intentional subtle design
- Card title bold on "does"/"does NOT do" via `<strong>` → Tinos 700 (characterStyleOverride, pixel-confirmed)
- `.hiw-desc-wrap` uses `max-width: 600px` (not `align-self: stretch`) to prevent text stranding at left edge on wide viewports
- `.hiw-bottom-text` and `.hiw-bottom-link` → Inter (pixel-confirmed from 4× render; MCP YAML reports Tinos)

### Governance Module
- White background (`#FFFFFF`)
- H2 "How integrity is protected" → Tinos (serif, pixel-confirmed)
- Body paragraph + bullet list → Inter (pixel-confirmed)
- `.gov-body` constrained to `max-width: 600px` — centers content at wide viewports
- CTA copy uses same display:block span pattern as Framework module:
  - `.gov-cta-q` → Inter 700, line-height 1.625
  - `.gov-cta-sub` → Inter 400, line-height 1.875
  - Color: `#056B8B` (teal mid)
- Apply button: teal bg (`#06678A`), white text, `arrow-white-3x6.svg` icon

### Footer
- Multi-layer background: `linear-gradient(152deg, rgba(102,102,102,0) 0%, rgba(29,29,29,1) 100%), #323232`
- Three-row content: disclaimer · links row · copyright
- All footer text → Inter (pixel-confirmed from 4× Figma render; MCP YAML reports Tinos for links)
- Links row: `gap: 10px` on flex container; separator `|` rendered as plain `<span class="footer-sep">` without surrounding spaces (CSS gap handles spacing)

---

## 5. Critical Implementation Methodology

### 5.1 characterStyleOverride Limitation

The Figma MCP tool (`mcp__figma-personal__get_figma_data`) returns each TEXT node's **base** `textStyle` token only. Character-level overrides (`characterStyleOverrides` + `styleOverrideTable` in the Figma REST API) are silently omitted. This caused incorrect font-family/weight assignments in multiple sections.

**Detection method:** Download direct Figma node renders via `mcp__figma-personal__download_figma_images` at 4× scale and inspect letterforms. Serif presence/absence is unambiguous at ×8 zoom:
- Serifs on 'i', 't', 'f', bracket on 'r' → **Tinos**
- Clean terminals, single-story 'a'/'g' → **Inter**

**All confirmed overrides:**

| Section | MCP-reported | Pixel-confirmed |
|---|---|---|
| Methodology Expert teaser | Tinos 400 | Inter 400 (regular + bold) |
| Framework CTA "Methodology expert?" | Tinos 700 | Inter 700 |
| Framework CTA sub-copy | Tinos 700 | Inter 400 |
| HIW card title "does" / "does NOT do" | Tinos 400 | Tinos **700** |
| HIW bottom "Want updates as we build?" | Tinos 400 | Inter **700** |
| HIW bottom "Sign up Here" | Tinos 400 | Inter 400 + underline |
| HIW bottom all text | Tinos | Inter |
| Governance CTA "Methodology expert?" | Tinos | Inter 700 |
| Governance CTA sub-copy | Tinos | Inter 400 |
| Footer links + separator | Tinos | Inter |

### 5.2 MCP Layout Token Limitation

The MCP YAML also omits certain layout constraints (e.g., `max-width` on cards). Cards in BFB, HIW, and Governance modules all report `horizontal: fill` in YAML but have a 600px visual cap. Confirmed by measuring x-positions of card boundaries in Figma renders at 1024px and 1440px viewports.

---

## 6. Responsive Behaviour

All seven required viewports verified via Playwright + visual inspection:

| Viewport | Notes |
|---|---|
| 320px | H1 scales to 28px (media query); header gap tightened to 5px |
| 375px | Primary design reference |
| 390px | iPhone 14 size; subtitle fits 1 line |
| 600px | Mid-range; all cards at natural width |
| 1024px | Cards cap at 600px, centered |
| 1440px | Wide desktop; all modules centered in container |
| 2560px | Ultra-wide; cards at 600px, full-width modules |

**Wide-viewport centering pattern:** `width: 100%; max-width: 600px` on content blocks (`.gov-body`, `.hiw-desc-wrap`, `.module-body`, cards) with `align-items: center` on flex parent — centers content without requiring media queries.

---

## 7. Known Rendering Differences from Figma

These are irresolvable font rendering differences between Figma's renderer and Chrome/Webkit:

| Difference | Reason | Status |
|---|---|---|
| Subtitle wraps to 2 lines at 375px (Figma: 1 line) | Tinos renders wider in Chrome at 15px | Accepted |
| Section heights 2–8px taller in browser | Chrome adds slightly more leading | Accepted |
| BFB cards 0–88px shorter than Figma at wider viewports | Tinos renders narrower in Chrome → fewer line wraps in italic quote | Accepted |
| BFB/HIW H2 fits 1 line in Chrome at 1024px+ (Figma: 2 lines) | Tinos narrower at 32px in Chrome | Accepted |
| HIW height -22px at 320px | Chrome renders Inter/Tinos bullet text more compactly at 320px | Accepted |

---

## 8. Change Log

| Rev | Change |
|---|---|
| v1 | Initial implementation: header, hero, CTA, methodology teaser, framework module. Arrow icon sizes, button gaps, max-widths corrected from initial Figma token extraction |
| v2 | Hero section spacing refined (padding-only model, no gap); CTA inside hero for bg image coverage; CTA icon padding corrected |
| v3 | characterStyleOverride fixes for grey teaser (Tinos→Inter) and framework CTA (Tinos→Inter); line-heights pixel-calibrated to 1.625/1.875 |
| v4 | Built For Both module added; BFB card max-width 600px confirmed via pixel measurement |
| v5 | How It Works module added; HIW card max-width, watermark bgs, characterStyleOverrides (bold titles, underline link) |
| v6 | HIW fixes: desc-wrap wide-viewport centering (align-self:stretch removed, max-width:600px added); bottom text font Tinos→Inter; "Want updates" bold confirmed |
| v7 | Governance module + Footer added; CTA copy display:block span pattern; all arrow SVGs; dark footer gradient |
| v7.1 | Font fixes post pixel-inspection: Governance CTA Tinos→Inter + line-height restructure (1.625/1.875); footer links/separator Tinos→Inter |
| v7.2 | Add `max-width: 1440px` to `.page-container` — pixel-confirmed from Figma 3000px artboard (Framework module 360px at 0.25× = 1440px); MCP YAML does not expose this constraint |
