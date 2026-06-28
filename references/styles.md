# Design Styles — Full Primitive Definitions

Load this when a style is selected at the session gate. Each style is defined **primitives-first** (material, depth, layer order, light, geometry, motion). CSS is an optional note for HTML targets only — never the definition itself. Once a style is chosen, commit fully; every decision serves it.

## Contents
1. Minimal / Clean
2. Material 3
3. Bento Grid
4. Glassmorphism
5. Liquid Glass
6. Spatial / Depth UI
7. Aurora / Mesh Gradient
8. Neo-Brutalism
9. Neumorphism (conditional)
10. Claymorphism (conditional)
11. Skeuomorphic (legacy)

---

## 1. Minimal / Clean
- Primitives: maximal whitespace; restrained geometry; 1–2 colors + neutrals; near-flat depth.
- Light: subtle, single soft shadow at most. Typography does the hierarchy work.
- Rule: every element must justify its existence.
- **Native form-control dark fix:** `accent-color` on native `checkbox` / `radio` / `range` does not reliably re-resolve a CSS variable when the theme attribute flips. If the brand color is a mid-saturation blue that would sink into dark surfaces, declare an explicit `[data-theme="dark"]` override using the lighter dark-palette interactive token (e.g. `--color-info` / `--border-focus`), or replace the native control with a themed custom component. Applies to any style using native form controls, not just Minimal.

## 2. Material 3
- Primitives: elevation communicates layer hierarchy; dynamic color roles; structured grids; rounded geometry per M3.
- Motion: meaningful transitions 200–300ms.
- Light: tonal elevation overlays in dark mode, not just drop shadows.
- CSS note: follow Material 3 elevation + state-layer specs.

## 3. Bento Grid
- Primitives: grid of varied cell sizes; size = importance (large cell = primary content); consistent internal padding; generous gaps.
- Depth: clean contained cards, low elevation.
- CSS note: CSS grid with explicit row/column spans.

## 4. Glassmorphism
- Primitives: frosted translucent panels over a blurred/gradient background; soft 1px light borders; layered panels at different blur depths.
- Light: diffuse, no refraction.
- Accessibility: keep text on a sufficiently opaque layer; verify with the 3 pairing rules.
- CSS note: `background: rgba(255,255,255,0.1)` + `backdrop-filter: blur(20px)`; border `1px solid rgba(255,255,255,0.2)`.

## 5. Liquid Glass
- Primitives: refractive translucent layer; content visible AND distorted behind it; specular edge highlight; depth via layer order; controls FLOAT above content (content always leads).
- Difference from Glassmorphism: refraction + motion response, not just blur.
- CSS note (optional): `backdrop-filter: blur()` + SVG `feDisplacementMap` (refraction) + `feSpecularLighting` (edge light). CSS has no native distortion property; the SVG approach is shape-limited with inconsistent browser support → ship a blur-only fallback for production, reserve full refraction for hero/marketing.
- **Accessibility gate (hard rule):** text ALWAYS sits on a solid backing layer, NEVER directly on glass. Promote this to a **named token/class — `text-backing`** — so it is structural, not remembered: a high-contrast semi-transparent backing behind any text. Also require `isolation: isolate` and a `prefers-reduced-motion` block that disables the distortion animation. Without all three it fails instantly — same trap as Neumorphism.
- **`text-backing` placement:** the backing goes on the text's CARD/container surface (raise the card's opacity so text reads) — NOT as an opaque box around each text node. A backing hugging each label renders as a dark rectangle (debug-artifact look). One backing per card surface, not per text element.

## 6. Spatial / Depth UI
- Primitives: floating layers in real depth; content recedes, controls float above; soft ambient + key light; rounded geometry; parallax/offset to imply z-distance.
- Motion: subtle depth response to scroll/pointer; never disorienting.
- Accessibility: maintain contrast per layer; respect reduced-motion (flatten depth animation).
- Best for: premium product surfaces, AR/spatial-adjacent products, focus-mode screens.

## 7. Aurora / Mesh Gradient
- Primitives: soft multi-stop gradient mesh as background field; slow ambient motion; foreground content on solid/elevated surfaces for legibility.
- Light: luminous, atmospheric, low-contrast background — never place body text directly on the mesh.
- Accessibility: text lives on a solid card/panel above the mesh (use the `text-backing` rule); respect reduced-motion (freeze the mesh).
- Best for: landing heroes, dashboard backdrops, empty/marketing states.

## 8. Neo-Brutalism
- Primitives: raw high-contrast geometry; thick (2–4px) borders; oversized heavy display type (the ONE style where heavy weight everywhere is intentional); limited but stark palette (often black + one accent); intentionally broken/extreme grid.
- Light: flat hard-edged shadows (offset blocks), no soft elevation.
- **Weight exemption:** this is the only style exempt from weight discipline. When you emit heavy weight, add a one-line CSS comment (e.g. `/* Neo-Brutalism: intentional heavy weight */`) so an auditor doesn't read 700–900 as a violation.
- Note: the heavy-weight, oversized-type bias is scoped to THIS style only — it must not bleed into other styles or landings.

## 9. Neumorphism ⚠ accessibility-risk — single-purpose only
- Primitives: shapes pressed into / raised from a flat mid-tone surface; form defined entirely by paired light + dark shadow; no hard borders.
- **Hard gate:** low contrast is inherent — only for single-purpose apps (calculators, controls, toggles) AND always verify against the pairing rules. Dense content or critical text → do not use this style.
- CSS note: two shadows — light top-left, dark bottom-right — on a non-white mid-tone background.

## 10. Claymorphism — consumer / EdTech only
- Primitives: puffy inflated 3D shapes; heavy border-radius (20px+); soft pastel high-saturation colors; thick colored (not gray) shadows; depth without real 3D.
- **Tag:** NOT for enterprise B2B (aviation / transport / HRM / fintech / gov). Consumer or EdTech contexts only.

## 11. Skeuomorphic — legacy / niche (ask only if requested)
- Primitives: simulate real materials (leather, paper, metal); realistic depth + lighting; controls look like physical buttons, dials, switches.
- Near-zero enterprise use. Offer only when explicitly asked.
