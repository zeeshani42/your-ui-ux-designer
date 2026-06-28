# Figma Output — Auto-Layout, Reflow & Variants

Load this when the session-gate output target is **Figma**. Covers building correct multi-frame, variant-driven, dark-mode-ready Figma via the MCP plugin. All rules are primitives-first; Figma API specifics noted where they bite.

## Contents
1. The 3-frame reflow rule
2. Auto-layout discipline
3. Fixed-size elements inside auto-layout
4. Component states as variants
5. Color / type / spacing as styles & variables
6. Dark mode
7. MCP plugin behaviours (known traps)
8. Figma validation checklist

---

## 1. The 3-frame reflow rule
Deliver three reflowed frames, not one frame resized:
- **390px** — mobile (single column, bottom nav, full-screen modals, kebab row actions).
- **768px** — tablet (2-col, drawer nav, condensed tables).
- **1440px** — desktop (full grid, rail + secondary panel, full tables).
Each frame is a genuine reflow — layout, nav pattern, and table treatment change per breakpoint, mirroring the HTML breakpoint intent (1280/1024/768/480).

## 2. Auto-layout discipline
- Build with auto-layout, not absolute positioning — frames must reflow, not break, when resized.
- Set spacing to 8-pt values (gap + padding) so the grid holds.
- Use `layoutGrow` / `layoutSizingHorizontal`/`Vertical` deliberately: `FILL` for flexible regions, `HUG` for content-sized, `FIXED` for set dimensions.
- Nest auto-layouts for rows-within-columns; don't fake structure with manual spacing.

## 3. Fixed-size elements inside auto-layout (known trap)
A fixed-size icon button (e.g. a 32×32 modal close ×) appended to an auto-layout parent **defaults to HUG and can grow/shrink wrong**. Explicitly set `layoutSizingHorizontal = FIXED` AND `layoutSizingVertical = FIXED` on both axes for icon buttons, avatars, and any element that must keep its size.
- Mobile modal body: set scrollable / `min-height` so content growth scrolls instead of clipping.

## 4. Component states as variants
- States are **component variants**, not duplicated static frames. Create a component set with a `State` property: Default / Hover / Focus / Loading / Empty / Error / Disabled (as applicable).
- `combineAsVariants` produces a true `ComponentSet` only when component names follow the `PropertyName=Value` pattern (e.g. `State=Hover`). Name them correctly before combining.
- Document each state's tokens + behaviour in the component description.

## 5. Color / type / spacing as styles & variables
- Define color as Figma **variables** (supports light/dark modes natively) or styles — never raw hex scattered on layers.
- Type scale as text styles (the fixed modular scale, ≤6 sizes, weight discipline).
- Spacing as number variables on the 8-pt grid where the plugin allows.
- Tokenize gradient/skeleton stops as variables so they don't drift across frames.

## 6. Dark mode
- Use variable **modes** (Light / Dark) so one component set serves both — don't build parallel dark copies.
- Apply Pillar 11 contrast pairing rules per mode. In dark mode, **don't separate panels with a 1px hairline** — use a lighter surface step (elevation), since a thin border vanishes on dark surfaces.
- Verify brand-button label color and any decorative-vs-body glyph contrast in BOTH modes.

## 7. MCP plugin behaviours (known traps)
- `planKey` must be in `team::{numeric-id}` format — obtain the numeric id via `Figma:whoami` (don't guess).
- Fixed-size buttons appended to auto-layout parents: set `layoutSizingHorizontal/Vertical = FIXED` explicitly (see §3).
- `combineAsVariants` needs `PropertyName=Value` component names to create a real `ComponentSet` (see §4).
- WCAG contrast can be computed in-plugin via sRGB linearization without leaving MCP context — but per this skill, **prefer the 3 pairing rules**; reserve in-plugin computation for an optional verification pass, not as the primary method.

## 8. Figma validation checklist
- 3 reflowed frames (390 / 768 / 1440), each a genuine reflow.
- Auto-layout throughout; no absolute positioning for structural layout.
- Icon/fixed elements set `FIXED` on both axes; modal bodies scrollable.
- States built as a `State` variant set (not static copies), names follow `Property=Value`.
- Color/type/spacing as variables/styles; dark mode via variable modes.
- Dark separators use elevation, not hairlines; brand-button + glyph contrast verified both modes.
- Default / Loading / Empty / Error all present as variants.
