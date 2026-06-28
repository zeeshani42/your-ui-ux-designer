# Mobile Interactions — Full Specification

Load this when designing a mobile screen, or when a target needs touch/gesture detail. The core file (Pillar 8 + 10) carries the must-always rules; this file carries the full touch spec. For B2B enterprise (aviation / transport / HRM), most exotic gestures rarely fire — prioritise touch targets, thumb zones, states, and the kebab pattern. Use the gesture sections only when the product genuinely needs them.

**Archetype scope (read first).** This file's *phone shell / device-frame* presentation applies to the **Mobile-app archetype ONLY** (see Build Archetype in core). A **web system or landing page never gets a phone frame** — at narrow width it reflows edge-to-edge in the real browser viewport, and its nav converts (rail → bottom bar) on true viewport width. The touch rules below (44px targets, kebab, drawer, focus traps) still apply to a web system's mobile breakpoint; the *framing* does not. Don't shrink a web system inside a fixed shell — that makes the breakpoint read "desktop" while it looks like a phone, so the rail won't convert.

## Contents
1. Touch targets & thumb zones
2. Core gestures
3. Navigation patterns (mobile)
4. Row actions & lists
5. Sheets, modals & overlays
6. Motion, haptics & feedback
7. Orientation & safe areas
8. Mobile validation checklist

---

## 1. Touch targets & thumb zones
- **Minimum target 44×44px** (iOS) / 48×48dp (Android). Applies to every tappable element, including icons and row affordances.
- Minimum 8px gap between adjacent targets — no accidental taps.
- **Thumb zones:** primary actions in the bottom third (easy reach); destructive/rare actions top or behind confirmation. Avoid critical controls in the top corners on tall phones.
- Bottom nav and primary CTA live in the natural thumb arc.

## 2. Core gestures
Use only what the product needs; never invent gestures the user can't discover.
- **Tap** — primary activation. Always provide a visible pressed state.
- **Long-press** — secondary/contextual menu. Must have a non-gesture fallback (a visible kebab) — never the ONLY way to reach an action.
- **Swipe** — horizontal on list rows for reveal-actions (e.g. archive/delete); horizontal on cards for carousels; vertical for scroll. Show a hint affordance the first time.
- **Drag-to-reorder** — explicit handle, lift elevation on grab, clear drop target. Provide a non-drag fallback for accessibility.
- **Pinch / rotate** — media/map only; never for navigation. Always reversible.
- **Pull-to-refresh** — list tops; show spinner + release threshold.
- Every gesture respects `prefers-reduced-motion` for its accompanying animation.

## 3. Navigation patterns (mobile)
- **Bottom tab bar** — 3–5 top-level destinations, 44px targets, label + icon. The mobile form of the primary rail.
- **Drawer / off-canvas** — secondary nav (the desktop secondary panel) slides in; dim + tap-out to close; trap focus while open.
- **Bottom sheet** — contextual actions and filters; drag handle; snap points; dismiss on swipe-down or tap-out.
- Back behaviour predictable; never trap the user. Sticky headers stay readable on scroll.

### Dual-nav on mobile (Gmail model)
This is the **web-system** archetype at ≤768px (not the mobile-app archetype). The rail CONVERTS — it never disappears.
- **Primary rail → bottom tab bar.** Max 5 tabs; if more, show 4 + a "More" button that reveals the rest as a sheet. Bottom bar holds primary tabs only.
- **A top bar appears the instant the rail is hidden** — never a breakpoint where neither rail nor top bar exists. Top-bar slots, NOT grouped: (1) hamburger far left, (2) logo beside it, (3) search icon right-aligned, (4) profile photo far right. Left cluster = hamburger + logo; right cluster = search + profile.
- **The hamburger lives in the top bar, never in the bottom bar, never `display:none`.** It opens the secondary nav as an overlay drawer OVER the page — slides in with a backdrop, above the content; does NOT push or reflow the page (Gmail behaviour). On desktop the hamburger is in the rail and the logo sits atop the secondary panel; on mobile both surface in this top bar because the panel becomes the drawer.
- The hamburger JS must branch on viewport: collapse-inline on desktop, open/close overlay drawer at ≤1024px and ≤768px.
- a11y: drawer is `role="dialog"`, `aria-modal="true"`, focus trap on open, focus returns to the hamburger on close, Esc + backdrop-tap + swipe to close.

## 4. Row actions & lists
- **≤480px: collapse multiple row actions into ONE overflow kebab (⋮, 44px).** Never stack labelled buttons vertically inside a row.
- Swipe-to-reveal may supplement the kebab but never replace it (discoverability + accessibility).
- Dense lists: 1 primary line + 1 supporting line; truncate with ellipsis, never wrap to 3+ lines in a list.

## 5. Sheets, modals & overlays
- Mobile modals go **full-screen** (centered dialogs are a desktop pattern).
- Modal body scrollable; header + primary action stay fixed/visible. Never trap content off-screen.
- Single clear primary action; clear escape (X + swipe-down + back). Focus moves in on open, returns to trigger on close.
- Bottom sheets for lightweight choices; full sheet for multi-step.
- **Overlays inside the mobile-app phone shell.** In the Mobile-app archetype the layout sits in a centered phone shell; a `position:fixed` overlay resolves to the viewport, not the shell — so it offsets beside the phone frame on wide screens. Scope the overlay to the shell: place it in the shell DOM and let the shell own the positioning context (`position:absolute; inset:0` within the shell), so full-screen sheets cover the shell, not the desktop. A real device is unaffected; this keeps desktop preview correct. (Web systems have no shell — their overlays cover the true viewport normally.)

## 6. Motion, haptics & feedback
- Feedback timing: 150–300ms UI reaction; 300–500ms transitions. Ease-out entering, ease-in leaving.
- **Pressed state on every tap** (color/scale/elevation) — touch has no hover, so the pressed state is the only feedback.
- Haptics (where supported): light tap on selection, success notification on completion, error pattern on failure. Never overuse.
- Loading: skeleton pulse, never a blank white screen. Success: brief check. Error: inline message + recovery path.
- All motion ships a `prefers-reduced-motion: reduce` alternative.

## 7. Orientation & safe areas
- Respect device safe-area insets (notch, home indicator, rounded corners) — content and sticky bars never sit under them.
- Portrait is primary for enterprise; support landscape for tables/media where it helps, but don't force it.
- Sticky bars full-bleed within the safe area; no page-level horizontal scroll (confine `overflow-x` to the scrollable region only).

## 8. Mobile validation checklist
- All targets ≥44px with ≥8px spacing · primary actions in thumb zone.
- Every tap has a visible pressed state · no hover-only affordances.
- Row actions collapse to a 44px kebab ≤480px.
- Modals full-screen with scrollable body + fixed primary action.
- Every gesture has a non-gesture fallback.
- Safe-area insets respected · no page-level horizontal scroll.
- Default / Loading / Empty / Error all rendered for the mobile layout.
- `prefers-reduced-motion` alternative present for every animation.
