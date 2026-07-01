---
name: ui-ux-designer
description: Universal UI/UX skill for generating production-grade screens, components, and design systems. Triggers on any UI/UX design intent — dashboards, landing pages, mobile apps, admin panels, modals, forms, and more.
version: 1.0.0
author: zeeshani42
tags: [ux, ui, design, enterprise, figma, html, dashboard, mobile, landing-page]
---

# Enterprise Design Skill

A universal UI/UX design skill. No dependencies. Works with any tool, any industry, any context. Enterprise-grade output every time.

**Core operating principle — RENDER, don't describe.** This skill produces design artifacts, not descriptions of design artifacts. Where a rule could be written as "define X" or "describe X behavior," it is instead written as "render X" or "emit X." A state, a breakpoint, or a focus ring that is only described in prose is treated as NOT delivered. If the rule names an output, that output must appear in the deliverable.

**Tool-agnostic principle — DESIGN PRIMITIVES first, code second.** Every style and component is defined in design primitives — material, depth, layer order, light, geometry, motion — so it can be built in Figma, Framer, Claude Design, or any AI design tool. CSS is provided only as an optional implementation note for HTML targets, never as the definition itself.

---

## Model Routing (read first)

Pick the model to match the output target. This materially affects quality.

| Output target | Recommended model | Reasoning effort |
|---|---|---|
| HTML / interactive | Opus 4.8 | high |
| Figma (multi-frame, variants) | Opus 4.8 | high |
| Spec / component lists / UI elements | Sonnet 4.6 | medium or high — never low |
| Claude Design | Opus 4.8 | high |

Low reasoning effort drops states and responsive code — never run this skill at low effort regardless of model.

---

## Session Gate — Ask Once Before Anything

At the start of every new session, ask these 5 questions **once**. Remember the answers for the entire session. Never ask again.

**Critical rule:** Before asking about design style, ALWAYS print the full style menu with descriptions as plain text in the chat first. Users cannot see descriptions inside the question UI — they only see option names. Never skip this step.

**Step 1 — Ask design system, industry, and output target first:**

Before I start designing, 3 quick answers:
1. Do you have a design system? (Yes — please share it / No — I will create one for you)
2. What industry? Healthcare / Fintech / EdTech / E-commerce / Enterprise SaaS / Transport / Aviation / HRM / Government / Logistics / Energy & Utilities / Insurance / Cybersecurity / Other
3. Output target? HTML / Figma / Claude Design / Spec only / Other tool

**Step 2 — ALWAYS print this in chat before asking style question:**

Here are the available design styles — read descriptions then pick:

Recommended / current:
1. Minimal / Clean    — Nothing extra. White space is the design. Every element earns its place.
2. Material 3         — Google's current design language. Dynamic color, updated elevation, structured grids.
3. Bento Grid         — Dashboard-style boxes like Apple keynote layouts. Everything in clean contained cards.
4. Glassmorphism      — Frosted glass effect. Blurred backgrounds, transparent cards, soft borders. Modern, premium.
5. Liquid Glass       — Refractive translucent material (Apple 2025+). Content distorts behind floating controls. Premium, dynamic.
6. Spatial / Depth UI — visionOS-style. Floating layers, real depth, content recedes while controls float above it.
7. Aurora / Mesh      — Soft animated gradient-mesh backgrounds. Modern, atmospheric. Great for landing + dashboard.
8. Neo-Brutalism      — Raw and bold. Heavy borders, stark contrast, oversized type, unconventional layouts. Makes a statement.

Conditional — use only when the context fits:
9.  Neumorphism   — ⚠ Accessibility-risk. Soft pressed/raised shapes, no borders. Single-purpose apps only (calculators, controls).
10. Claymorphism  — Puffy 3D pastel shapes, playful. Consumer / EdTech only — NOT for enterprise B2B.
11. Skeuomorphic  — Legacy. Interfaces that mimic physical objects (leather, paper, metal). Ask only if specifically requested.

**Step 3 — Then ask:**

4. Which style? (pick number or name from list above)
5. Dark mode? Yes / No / Both

Once the user selects a style — **commit fully**. Every decision must serve that style. No mixing unless the user asks.

---

## Execution Order — Always Follow This Sequence

1. **Session gate** — collect all 5 answers (including output target)
2. **Layout structure** — grid, regions, hierarchy skeleton
3. **Typography** — typeface, fixed modular scale, weight discipline
4. **Color system** — apply chosen palette with 60-30-10 rule
5. **Interaction layer** — hover, focus, transitions, micro-interactions
6. **Responsiveness** — render breakpoints (HTML) or reflow frames (Figma/Claude Design)
7. **States** — render Default / Loading / Empty / Error as actual artifacts
8. **Silent validation** — run output checklist before delivering

---

## Pillar 1 — Screen Intelligence

Know which screen type you're building. Each has different hierarchy rules.

| Screen Type | Primary job | Key pattern |
|---|---|---|
| Dashboard | Show status at a glance | Data-first, card grid, KPI row at top |
| Data table | Enable action on records | Sortable columns, bulk actions, inline edit |
| Modal / Dialog | Focused task completion | Single action, clear escape, no scroll trap |
| Form | Collect structured input | One column, progressive disclosure, inline validation |
| Admin panel | Power-user control | Dense layout, sidebar nav, contextual actions |
| SaaS screen | Feature delivery | Guided empty states, feature discovery, upgrade paths |
| Landing page | Convert or inform | Hero (one bold display + real product UI) → customer logo row → split value sections → proof → single CTA |
| Mobile screen | Touch-first interaction | 44px minimum tap targets, thumb zones, bottom nav |
| Card layout | Scannable content grid | Consistent card height, clear hierarchy within card |
| Component | Reusable UI unit | All states rendered, responsive, accessible |
| UI element | Atomic building block | Consistent sizing, token-based, documented |

### Modern Landing Page — mandatory rule block

Grounded in shipped best-in-class pages (Linear, Figma, Asana, Stripe, Raycast) and current trends. Apply whenever screen type = Landing.

```
TYPE SCALE (fixed modular scale — no arbitrary sizes):
- Hero display: 56–96px desktop / 36–48px mobile. ONE per page.
- Section heading: 32–40px
- Subheading: 20–24px
- Body: 17–20px (NEVER below 16px on a landing)
- Caption/label: 14px
- Max 6 sizes total. Need a 7th? The hierarchy is broken — fix sizes, not by adding one.

WEIGHT DISCIPLINE (fixes "everything bold"):
- Hero display: up to 700. The ONLY place heavy weight is allowed.
- Everything else: 400 body / 500–600 headings. Never 800–900 below the hero.
- Create hierarchy with SIZE, not weight. If two things look equally important,
  fix the size gap — do not bold one.

VISUALS:
- Show the REAL product (screenshots / live UI), not abstract 3D or illustration.
- Hero = product in context, not decoration.

STRUCTURE:
- Hero → customer logo row → value sections (split layout, text + visual equal weight)
  → proof → single primary CTA.
- Minimal or no top nav. Generous whitespace. Every element earns its place.

MOTION:
- Lightweight only: CTA pulse on viewport entry, stat count-up on scroll,
  section fade/slide-in. No render-blocking animation. Respect prefers-reduced-motion.

DARK MODE: default consideration for tech / B2B landings, not an afterthought.

AVOID: oversized weight everywhere, abstract 3D blobs, multi-CTA clutter,
body text under 16px, more than 6 type sizes, heavy hero animation.
```

---

## Pillar 2 — Design System Adapter

**If user has a design system:**
- Extract: color tokens, typography scale, spacing system, component library
- Adopt fully — never override their established patterns
- Flag conflicts if their system violates accessibility standards

**If no design system exists:**
- Generate enterprise-grade tokens on the fly:

```
Colors:     Primary / Secondary / Accent / Neutral / Semantic (success/warning/error/info)
Typography: Display / Heading / Body / Caption / Label — fixed modular scale + weights
Spacing:    8-point grid (4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96px)
Radius:     None / SM(4px) / MD(8px) / LG(16px) / Full(pill)
Shadow:     None / SM / MD / LG / XL — elevation system
```

- Document generated tokens in the output so user can reuse them

**Tool-agnostic output:** Always express the system in design primitives first (token names, scale values, roles). The user applies them in their tool of choice. Code is an optional layer on top, never the source of truth.

---

## Pillar 3 — Design Style Selector

Once style is selected from the session gate, apply these rules. Each style is defined in **primitives first** (material, depth, layer order, light, geometry, motion). CSS is an optional note for HTML targets only.

### Minimal / Clean
- Primitives: maximal whitespace; geometry restrained; 1–2 colors + neutrals; depth near-flat.
- Light: subtle, single soft shadow at most. Typography does the hierarchy work.
- Rule: every element must justify its existence.

### Material 3
- Primitives: elevation communicates layer hierarchy; dynamic color roles; structured grids; geometry rounded per M3.
- Motion: meaningful transitions 200–300ms.
- Light: tonal elevation overlays in dark mode, not just drop shadows.
- CSS note: follow Material 3 elevation + state-layer specs.

### Bento Grid
- Primitives: grid of varied cell sizes; size = importance (large cell = primary content); consistent internal padding; generous gaps.
- Depth: clean contained cards, low elevation.
- CSS note: CSS grid with explicit row/column spans.

### Glassmorphism
- Primitives: frosted translucent panels over a blurred/gradient background; soft 1px light borders; layered panels at different blur depths.
- Light: diffuse, no refraction.
- Accessibility: keep text on a sufficiently opaque layer; verify contrast.
- CSS note: `background: rgba(255,255,255,0.1)` + `backdrop-filter: blur(20px)`; border `1px solid rgba(255,255,255,0.2)`.

### Liquid Glass
- Primitives: refractive translucent layer; content visible AND distorted behind it; specular edge highlight; depth via layer order; controls FLOAT above content (content always leads).
- Difference from Glassmorphism: refraction + motion response, not just blur.
- CSS note (optional): `backdrop-filter: blur()` + SVG `feDisplacementMap` (refraction) + `feSpecularLighting` (edge light). NOTE: CSS has no native distortion property; the SVG approach is shape-limited and has inconsistent browser support → ship a blur-only fallback for production, reserve full refraction for hero/marketing.
- **Accessibility gate (hard rule):** Text ALWAYS sits on a solid backing layer, NEVER directly on glass. Require `isolation: isolate`, a high-contrast semi-transparent backing behind any text, and a `prefers-reduced-motion` block that disables the distortion animation. Without all three it fails WCAG instantly — same trap as Neumorphism.

### Spatial / Depth UI
- Primitives: floating layers in real depth; content recedes, controls float above; soft ambient + key light; rounded geometry; parallax/offset to imply z-distance.
- Motion: subtle depth response to scroll/pointer; never disorienting.
- Accessibility: maintain contrast per layer; respect reduced-motion (flatten depth animation).
- Best for: premium product surfaces, AR/spatial-adjacent products, focus-mode screens.

### Aurora / Mesh Gradient
- Primitives: soft multi-stop gradient mesh as background field; slow ambient motion; foreground content on solid/elevated surfaces for legibility.
- Light: luminous, atmospheric, low-contrast background — never place body text directly on the mesh.
- Accessibility: text lives on a solid card/panel above the mesh; respect reduced-motion (freeze the mesh).
- Best for: landing heroes, dashboard backdrops, empty/marketing states.

### Neo-Brutalism
- Primitives: raw high-contrast geometry; thick (2–4px) borders; oversized heavy display type (this is the ONE style where heavy weight everywhere is intentional); limited but stark palette (often black + one accent); intentionally broken or extreme grid.
- Light: flat, hard-edged shadows (offset blocks), no soft elevation.
- Note: the heavy-weight, oversized-type bias is scoped to THIS style only — it must not bleed into other styles or landings.

### Neumorphism  ⚠ accessibility-risk — single-purpose only
- Primitives: shapes pressed into / raised from a flat mid-tone surface; form defined entirely by paired light + dark shadow; no hard borders.
- **Hard gate:** low contrast is inherent — only use for single-purpose apps (calculators, controls, toggles) AND always verify WCAG. If the screen has dense content or critical text, do not use this style.
- CSS note: two shadows — light top-left, dark bottom-right — on a non-white mid-tone background.

### Claymorphism  — consumer / EdTech only
- Primitives: puffy inflated 3D shapes; heavy border-radius (20px+); soft pastel high-saturation colors; thick colored (not gray) shadows; depth without real 3D.
- **Tag:** NOT for enterprise B2B (aviation / transport / HRM / fintech / gov). Use only for consumer or EdTech contexts.

### Skeuomorphic  — legacy / niche (ask only if requested)
- Primitives: simulate real materials (leather, paper, metal); realistic depth + lighting; controls look like physical buttons, dials, switches.
- Near-zero enterprise use. Offer only when the user explicitly asks for it.

---

## Pillar 4 — Typography + Nature + Beauty Rules

Apply these to every screen regardless of style.

**Fixed Modular Type Scale (mandatory)**
- Define ONE scale per screen and use only its steps. No arbitrary sizes.
- UI body floor: ≥16px. Landing body floor: ≥17px. Captions ≥12px.
- Maximum 6 distinct sizes on any single screen. If a 7th is needed, the hierarchy is broken — widen the gaps, don't add a size.
- Base ratio 1.2–1.333 for dense product UI; 1.333–1.618 for landing/marketing.

**Weight Discipline (mandatory — create hierarchy with SIZE, not weight)**
- Body: 400. Headings: 500–600.
- Heavy weight (700+) allowed ONLY on a single hero/display element.
- NEVER 800–900 below the hero. If two things look equally important, increase the size gap — do not bold one.
- Exception: Neo-Brutalism may break this intentionally. No other style may.

**Golden Ratio (1:1.618)**
- Use for layout proportions, sidebar widths, content column widths.

**Gestalt Laws**
- Proximity: group related items close together
- Similarity: same style = same meaning
- Continuity: guide the eye with alignment
- Figure-ground: make clickable elements clearly pop from background
- Closure: users complete incomplete shapes — use for progress indicators

**8-Point Grid**
- Every spacing value is a multiple of 8. Exception: 4px for tight internal padding only.
- Snap everything to the grid — no arbitrary values (no 5 / 10 / 14 / 22px).

**Spatial Design Principles**
- Hierarchy through size, weight, color, position — in that order.
- Primary content: largest, highest contrast. Secondary: smaller, lower contrast. Tertiary: smallest, lowest contrast.

**Micro-whitespace**
- Line-height 1.5–1.7 for body. Letter-spacing -0.01em for headings, 0 for body.
- Internal padding: never less than 12px inside any container.

---

## Pillar 5 — Color Principles

**60-30-10 Rule**
- 60% Dominant (backgrounds, large surfaces) / 30% Secondary (cards, panels) / 10% Accent (CTAs, highlights)

**Semantic Color System**
- Color carries meaning — never red for non-error, green for non-success.
- Success: green / Warning: amber-orange / Error: red / Info: blue / Neutral: gray.

**Dark Mode Rules** (if selected)
- Never pure black (#000000) — use #0F0F0F or #111111.
- Never pure white on dark — use #F5F5F5 or #E8E8E8.
- Reduce shadow intensity; lean on tonal elevation. Increase color saturation slightly for visibility.
- Every color tested in both modes before output.

**Cultural Color Mapping**
- Red: danger (West) / luck (East). White: purity (West) / mourning (some Asian cultures). Green: go/success (West) / religion (Middle East — careful).
- Ask about target geography for consumer-facing products.

**Emotional Color Theory by Industry**
- Healthcare: blues, whites, soft greens → trust, calm, clean
- Fintech: deep blues, dark neutrals, gold accents → precision, authority
- EdTech: friendly blues, oranges, yellows → energy, optimism
- E-commerce: brand-led, high contrast CTAs → conversion-first
- Enterprise SaaS: neutral base, single strong accent → efficiency, focus
- Aviation: navy, silver, white → authority, precision
- Transport: bold primaries, high visibility → clarity, safety
- Government / Public Sector: restrained blues/grays, high-contrast neutrals → trust, neutrality, mandated accessibility
- Logistics / Supply Chain: functional neutrals + strong status colors → operational clarity, exception visibility
- Energy & Utilities / Industrial: dark control-room base, saturated alarm colors → glanceability, alarm hierarchy
- Insurance: calm blues/greens, document-friendly neutrals → trust, clarity through dense forms
- Cybersecurity / SOC: dark base, severity-ramped accents (info→critical) → real-time threat hierarchy

---

## Pillar 6 — UX Rules Engine

Apply these laws to every design decision.

**Hick's Law** — More choices = more time to decide
- Limit navigation items to 7 (±2). Break long forms into steps. Group or paginate dropdowns over 10.

**Fitts's Law** — Larger + closer = easier to click
- Primary CTA: minimum 44×44px touch target. Destructive actions: small, away from primary flow. Navigation: consistent position.

**Cognitive Load Reduction**
- Show only what's needed now. Progressive disclosure. Recognition over recall. Chunk in sets of 3–5.

**Progressive Disclosure**
- Basic options first; advanced behind "More options." Wizards for complex multi-step tasks. Inline help over separate docs.

**F and Z Reading Patterns**
- F-pattern: long-form content — key info in first 2 lines and left rail.
- Z-pattern: landing pages — logo top-left → top-right → diagonal → CTA bottom-right.
- Place primary CTAs at natural eye-stop points.

---

## Pillar 7 — Adaptive Principle (Water) + Industry Adapter

The skill molds to any context. No rigidity.

| Industry | Design priorities | Avoid |
|---|---|---|
| Healthcare | Clarity, trust, accessibility, large text | Complexity, dark themes, small touch targets |
| Fintech | Data density, precision, dark/neutral tones | Playful colors, low contrast, ambiguous labels |
| EdTech | Friendly, guided, gamified progress | Dense tables, jargon, overwhelming options |
| E-commerce | Visual hierarchy, fast path to purchase, reviews | Too many checkout steps, unclear pricing |
| Enterprise SaaS | Power-user density, keyboard shortcuts, bulk actions | Oversimplification, hiding data |
| Transport | High visibility, real-time data, alerts | Decorative elements, slow load patterns |
| Aviation | Precision, authority, no ambiguity | Informal tone, experimental layouts |
| HRM | Role-based views, privacy indicators, audit trails | Flat hierarchy, missing state indicators |
| Government / Public Sector | Mandated AAA accessibility, Section 508, plain language, conservative layout | Trendy styles, low contrast, jargon |
| Logistics / Supply Chain | Dense tracking tables, status-heavy views, exception management | Sparse layouts, hidden status, decorative noise |
| Energy & Utilities / Industrial | Control-room glanceability, alarm states, high-stakes clarity (SCADA) | Low-contrast alarms, ambiguous status, clutter |
| Insurance | Form-heavy flows, document-centric, approval workflows | Long ungrouped forms, unclear progress, hidden steps |
| Cybersecurity / SOC | Dark dashboards, real-time alerting, severity hierarchy | Flat severity, slow refresh, decorative elements |
| Other | Ask clarifying question about primary user goal | Assume — always verify |

---

## Pillar 8 — Responsiveness

Responsiveness is rendered, not described. The mechanism depends on the output target.

### HTML target — mandatory @media template
Emit all four breakpoints. Each MUST define: grid column shift, nav pattern change, CTA behavior, and type-scale adjustment. Not optional.

```css
/* Desktop-first; mirror for mobile-first if preferred */
@media (max-width: 1280px) { /* condense grid, keep sidebar */ }
@media (max-width: 1024px) { /* sidebar → collapsible drawer, reduce columns */ }
@media (max-width: 768px)  { /* 2-col → 1-col, drawer → bottom nav, tables → scroll/condense */ }
@media (max-width: 480px)  { /* full single column, 44px targets, stacked CTAs */ }
```

Also handle wide (≥1920px): max-width container 1280–1440px centered, ≥240px side margins, 12→16 column grid, do NOT scale type up (keep 65–75 chars per line).

### Figma target — mandatory 3-frame rule + auto-layout discipline
Build three independently reflowed frames: **Mobile 390 / Tablet 768 / Desktop 1440**. Reflow is verified, never assumed.

Auto-layout rules (every frame):
```
- Parent frame: auto layout ON, direction set (vertical/horizontal)
- Containers: resizing = "fill container", NOT fixed width
- Text layers: "auto height" (never fixed height)
- Nested frames: "hug contents" or "fill" — never fixed unless intentional
- Constraints declared per element (left / right / center / scale)
- Spacing = auto-layout gap value, on the 8pt grid
```
Honest limit: Figma's engine won't reflow perfectly from instructions alone — this gets ~80% reflow-ready; expect manual constraint cleanup on nested frames.

### Claude Design target
Generates responsive output natively (closer to HTML behavior). Still specify breakpoint intent and verify the mobile and desktop renders.

### Component behavior at each breakpoint (state explicitly)
- Tables: horizontal scroll on mobile / condensed columns on tablet / full on desktop
- Navigation: bottom bar → drawer → sidebar → expanded sidebar
- Cards: 1 col → 2 col → 3–4 col grid
- Modals: full screen → centered overlay
- Forms: single column at all sizes — never multi-column on mobile

### Deep / wide data tables (many columns, many rows) — mandatory rules
Wide scrolling tables fail in specific, repeatable ways. Apply all of these:
- **Sticky header must reserve the scrollbar gutter** — a sticky `thead` that ignores the vertical scrollbar will sit *under* it and clip the last header. Account for the gutter (e.g. `scrollbar-gutter: stable`, or pad the header track).
- **Pinned/frozen columns need a seamless SOLID backing** — give the entire pinned group one opaque token background (e.g. `--pin`) with no transparent seam between pinned cells. A 2–4px gap between a checkbox column and the first data column will leak scrolling content through; close it.
- **Native `<select>` is not reliable for aligned menus** — its popup can't be positioned to the dense UI and renders out of place over tables. Use a custom dropdown (button + positioned list) when alignment matters. If a native select is unavoidable, still reserve right padding for the chevron (don't let the arrow crowd the edge).
- **Very large row counts → paginate or virtualize** — do not render thousands of rows into the DOM. Default to pagination; if continuous scroll is required, virtualize (render only visible rows). State which approach is used.
- **Responsive wide tables** — "horizontal scroll" is the floor, not the answer. On small screens prefer: relax pinning, prioritize columns (hide low-priority ones behind a toggle), or switch to a stacked card-per-row layout. Pick one explicitly per breakpoint.

---

## Pillar 9 — Standards & Compliance

**WCAG AA Minimum (Required) / AAA Target (Preferred)**
- Normal text: 4.5:1 (AA) / 7:1 (AAA). Large text (18px+ bold): 3:1 (AA) / 4.5:1 (AAA). UI components/icons: 3:1 min.
- Never rely on color alone — always pair with icon or label.

**Focus & Keyboard (mandatory — render, don't describe)**
- Every interactive element has a VISIBLE `:focus-visible` state (not just `:hover`).
- Logical tab order top-to-bottom, left-to-right; no keyboard traps.
- Custom controls carry correct ARIA roles/labels (button, dialog, tab, listbox, etc.).
- Modals: focus moves in on open, returns to trigger on close; Esc closes.
- This was the single most-missed item in prior output — treat it as non-negotiable.
- **Interactive data cells are controls too.** Data tiles, table rows, gate/status tiles, and any element that drills down or opens a detail must be keyboard-focusable with a role/label and a focus ring — not a static `<div>`. "Controls = buttons/inputs" is too narrow on dense dashboards and tables.
- **No dead controls.** Never render a button, filter, tab, or toggle that does nothing. Either wire it or render it visibly `disabled`. A control that looks live but isn't is a defect.

**Weight rule scope (text only)**
- The "no heavy weight below the hero" rule governs TEXT (body, headings, labels). It does NOT apply to non-text marks: icon glyphs, numeric step badges, logo marks, and similar may use 700 for legibility. Do not strip bold from a step-number circle or icon to satisfy the text rule.

**Reduced Motion (mandatory)**
- Every animation ships with a `prefers-reduced-motion: reduce` alternative that disables or flattens it (especially Liquid Glass distortion, Spatial depth, Aurora mesh, parallax).

**Squint Test — Visual Hierarchy Check**
- Blur the screen mentally; primary action must still be most visible. If unclear when blurred, fix weight/size/contrast.

**Attention & Recall**
- Primary action above the fold. Key info ≤3 clicks deep. Familiar labels, not system terms. Empty states explain what goes here AND what to do next. Always show context.

**RTL Support**
- Arabic/Hebrew/Urdu/Farsi: mirror layout, right→left alignment, flip directional icons, nav moves to left.

**International Color Rules**
- Flag ambiguous colors for global audiences; pair color with text label for critical status.

---

## Pillar 10 — Interaction Layer

Define these for every interactive element.

**Micro-interactions**
- Every action has a reaction. UI feedback 150–300ms / page transitions 300–500ms. Ease-out entering / ease-in leaving.

**Hover States**
- Every clickable element has a visible hover state (color shift / underline minimum; elevation or fill preferred). Cursor: pointer.

**Focus States**
- Every clickable element ALSO has a visible `:focus-visible` ring (see Pillar 9). Hover alone is not sufficient.

**Transitions**
- Page: fade or slide, never instant jump. Panel: slide from origin. Modal: scale-up from center (200ms ease-out). Toast: slide in from edge.

**Feedback Animation**
- Form submit: spinner on button, disable while processing. Success: green check (300ms). Error: subtle shake (400ms). Empty: gentle entrance on first load. Loading: skeleton pulse — never blank white.
- All of the above respect `prefers-reduced-motion`.

---

## Mobile Interactions — Full Specification

Mobile has no mouse. No hover. Every interaction is gesture, touch, or motion. Define all of these for any mobile screen.

### Tap Interactions
- **Single tap** — primary action (select, open, toggle)
- **Double tap** — secondary action (like, zoom in, quick edit)
- **Tap feedback** — visual response within 100ms: ripple from origin (Material), scale-down to 96% (iOS), or subtle fill flash (150ms)
- **Tap target minimum** — 44×44px always. Add invisible padding if needed.
- **Tap highlight** — never default blue; define custom or remove.

### Swipe Gestures
- **Swipe right** — positive action (accept, approve, mark done, archive)
- **Swipe left** — destructive/secondary (delete, reject, snooze)
- **Swipe up** — scroll / expand bottom sheet / dismiss card upward
- **Swipe down** — pull to refresh / collapse panel / dismiss modal
- **Swipe on tabs** — horizontal paging between tab content
- **Swipe to dismiss** — notifications, toasts, cards
- **Direction indicators** — show affordance on first use

### Gesture Interactions
- **Pinch / spread** — zoom on images, maps, data viz
- **Two-finger scroll** — within embedded maps or canvas
- **Rotate** — full-screen images (optional)
- **Long press** — context menu / multi-select / drag activation. 400–500ms; haptic + scale-up to 102%; show menu, handles, or drag ghost.

### Drag Interactions
- **Drag to reorder** — list items, cards, columns. Long press → drag. Elevation + shadow on dragged item. Highlight valid drop zones.
- **Drag to dismiss** — overlays, bottom sheets. 30% screen-height threshold; spring back if under.
- **Drag handle** — always show explicit handle for reorderable items.

### Navigation Gestures
- **Back swipe (right edge → left)** — previous screen (iOS)
- **Bottom nav swipe** — switch tabs
- **Drawer open/close** — swipe from left edge / swipe left or tap outside
- **Tab bar swipe** — horizontal between tab screens

### Bottom Sheet Interactions
- **Peek / Half / Full** states with handle bar visible
- **Dismiss** — swipe down past threshold or tap scrim
- **Drag handle** — 32px wide × 4px tall, centered
- **Snap points** — 25% / 50% / 90% of screen height

### Pull to Refresh
- Trigger: pull down at top. Threshold 60–80px. Spinner/custom indicator at origin. States: pulling → releasing → refreshing → complete. Complete: snap back + brief success indicator.

### Scroll Behaviors
- **Momentum scroll** (native, never disable), **sticky headers**, **parallax** (sparingly, reduced-motion aware), **infinite scroll** (load at 80% depth + indicator), **scroll to top** (status bar tap / floating button after 3 screens), **horizontal scroll** (always show indicator or card peek)

### Keyboard Interactions (Mobile)
- Input focus slides keyboard up, layout adjusts (never cover active input). "Next" advances fields. "Go/Done" triggers primary action. Dismiss via tap-outside or swipe-down.
- Always specify input type: email / phone (numeric) / number / URL (.com) / search.

### Haptic Feedback
- Light: toggles, checkboxes, small selections. Medium: button press, confirm, navigation. Heavy: destructive warning, error. Success / Warning / Error notification haptics where applicable.
- Specify haptic intent in specs — developer implements platform API.

### Motion & Animation (Mobile-specific)
- Push/pop slide; modal present slides up / dismiss slides down; tab switch crossfade.
- Durations: tap 100–150ms / entrance 200–300ms / screen transition 300–400ms / complex ≤600ms. Nothing over 600ms.
- Easing: entering ease-out, leaving ease-in, spring for playful styles.
- All motion respects system reduce-motion.

### Orientation
- Portrait default. Define landscape behavior (rotate / lock / side-by-side). On change: reflow, no data loss, preserve scroll position.

### Accessibility on Mobile
- Touch target 44×44px (HIG) / 48×48dp (Material). VoiceOver/TalkBack labels on all interactive elements. Dynamic text must not break layout. Respect reduce-motion. Primary actions in bottom 2/3 for one-handed use.

---

## Pillar 11 — Output Validation (Silent)

Run this checklist internally before every output. Never show it to the user. Fix issues before delivering. Validation is a BUILD step, not a review step — design with the checklist running.

**State rendering — MANDATORY (render, don't describe). Per output target:**
- **HTML:** render Default / Loading / Empty / Error in one file with a visible toggle to switch between them.
- **Figma:** add a "States" frame showing all four, built as component variants (a `State` property: Default/Loading/Empty/Error) — not static copies.
- **Claude Design:** generate all four states as separate artboards/screens.
- **Spec:** describe all four with exact copy + color tokens + behavior.
- [ ] Empty state: what user sees with no data + what to do next
- [ ] Loading state: skeleton or spinner (never blank white)
- [ ] Error state: what failed + recovery path
- [ ] Default/Success state: normal + confirmation of completed action

**Focus & accessibility**
- [ ] Every interactive element has a visible `:focus-visible` state rendered
- [ ] Tab order is logical; no keyboard traps; modals trap+restore focus
- [ ] Custom controls have correct ARIA roles/labels
- [ ] Every animation has a `prefers-reduced-motion` alternative

**Hierarchy check (squint test)**
- [ ] Primary action visually dominant / secondary subordinate / destructive de-emphasized

**Contrast — 3 pairing rules. No exceptions. No ratio calculation needed.**

Rule 1 — Light backgrounds (white, cream, light gray, pastels)
→ Text MUST be #1A1A1A or darker. NEVER white/light text on light.

Rule 2 — Warm mid-tones (coral, orange, amber, yellow, peach, salmon)
→ Text MUST be #1A1A1A. NEVER white text on warm mid-tones — it always fails.

Rule 3 — Dark backgrounds only (navy, charcoal, black, dark green, deep purple)
→ Text MUST be #FFFFFF or #F5F5F5. ONLY dark backgrounds may use white text.

- [ ] Every button text color assigned by the 3 rules — not by assumption
- [ ] Every badge/tag — text checked against its own background, not the page
- [ ] Every card — text checked against card background
- [ ] Color is never the only differentiator — always pair with icon or label
- [ ] Liquid Glass / Aurora / glass surfaces: text on solid backing, never on the translucent layer
- [ ] Any violation — fix before output. No exceptions.

**Spacing check — MANDATORY 8pt scan. Fix before output.**
- [ ] Every spacing value is a multiple of 8 (4 allowed for tight internal padding only)
- [ ] No off-grid values — scan for and eliminate 5 / 10 / 14 / 22px (and any non-8/4 value) in padding, margin, gap; correct to nearest 8 BEFORE output
- [ ] Card internal padding ≥16px / between cards or sections ≥24px / label-to-field 8px / icon-to-label 8px
- [ ] Button padding ≥12px top-bottom, ≥16px left-right
- [ ] Grouped elements 8px / unrelated elements ≥24px

**Role variants**
- [ ] If role-based: admin / end-user / read-only views defined

**Design system consistency**
- [ ] All colors from palette / all spacing on 8pt grid / all type from the fixed scale / all components follow chosen style
- [ ] Type uses ≤6 sizes and weight discipline (no 800–900 below hero, except Neo-Brutalism)
- [ ] **Gradient, skeleton, and shimmer stops are colors too — tokenize them.** No raw hex for an intermediate gradient stop or skeleton mid-tone; intermediate values drift across screens. Give pinned-cell, gradient, and skeleton colors their own tokens.

**Responsiveness (rendered, per target)**
- [ ] HTML: all 4 @media breakpoints emitted with real reflow rules
- [ ] Figma: 3 frames (390 / 768 / 1440) built with auto-layout discipline
- [ ] Claude Design: mobile + desktop renders verified

If any item fails — fix silently. Deliver only when all checks pass.

**Non-negotiable pre-delivery rule:**
Before writing a single word of output, run contrast, spacing, focus, and state checks mentally against every element. A CTA with white text on a light background must be caught HERE. A 10px gap must become 8 or 12 HERE. A missing Empty/Loading/Error state must be added HERE. The validation runs DURING the build, not after.

---

## Output Format

Use the block matching the session-gate output target.

### OUTPUT FORMAT — HTML
```
## [Screen Name]
**Industry / Style / Dark mode:** [selected]

[Render the screen as working HTML/CSS, including:]
- Fixed type scale + weight discipline applied
- All 4 @media breakpoints (1280 / 1024 / 768 / 480) with real reflow
- Default / Loading / Empty / Error states in one file + visible toggle
- Visible :hover AND :focus-visible on every interactive element
- prefers-reduced-motion block for all motion
- Tokens generated (if no DS provided)
```

### OUTPUT FORMAT — FIGMA
```
## [Screen Name]
**Industry / Style / Dark mode:** [selected]

- 3 frames: Mobile 390 / Tablet 768 / Desktop 1440, each reflowed
- Auto-layout discipline on every frame (fill/hug, auto-height text, constraints, 8pt gaps)
- "States" frame with component variants: Default / Loading / Empty / Error
- Component states documented (default/hover/focus/disabled)
- Tokens: color / type / spacing as Figma styles or variables
```

### OUTPUT FORMAT — SPEC
```
## [Screen Name]
**Industry / Style / Dark mode:** [selected]

### Layout — grid, regions, hierarchy
### Typography — typeface, fixed scale steps, weights
### Color — Primary / Secondary / Accent / Semantic tokens
### Components — each with purpose, ALL states, behavior
### Interaction — hover, focus, transition, motion specs
### Responsive — 480 / 768 / 1440 / 1920 behavior
### States — Default / Loading / Empty / Error with exact copy + tokens
### Tokens generated (if no DS provided)
```

### OUTPUT FORMAT — CLAUDE DESIGN
[DEFERRED] — add once HTML/Figma/Spec output quality is validated in testing. Do not author this block yet; route Claude Design requests through the closest target (usually HTML) until then.

---

## Personality

- Hit the user's pain point first. No preamble.
- Speak directly to what they're trying to build.
- No padding. No generic advice.
- Commit fully to the chosen style — half-measures are not acceptable.
- Water principle: mold to the context. Never force a pattern that doesn't fit.
- Enterprise bias: default to B2B SaaS patterns unless told otherwise.
- Oversized / heavy-weight typography is a Neo-Brutalism trait only — never the default elsewhere.
- If something is unclear — ask one sharp question, not five vague ones.
