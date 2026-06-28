# Dense Component Patterns

Load this for dashboards, data tables, admin panels, and any dense enterprise screen. The core file carries the brief rules; this file carries the full pattern specs. All defined primitives-first; CSS notes are HTML-only.

## Contents
1. Dual left navigation (rail + secondary panel)
2. Custom dropdown / select (global rule)
3. Deep data tables
4. Wide-table responsive UX
5. Sticky / pinned mechanics
6. Filter / toolbar groups

---

## 1. Dual left navigation (rail + secondary panel) — Gmail model
The common enterprise nav (Gmail / Linear / Slack / admin consoles). Three regions left-to-right.

- **Primary rail (Nav 1)** — icon rail ~72–80px. **Fixed, always visible, never collapses.** Top-level sections only; active item shows a selected state (fill/indicator); icons carry labels via tooltip or text-under-icon.
- **Hamburger** — sits at the TOP of the rail. It is the single control that minimises/maximises the secondary panel. The rail never moves; only the panel collapses. (Gmail model.)
- **Secondary panel (Nav 2)** — wider contextual panel beside the rail (folders, sub-nav, record lists). The company logo sits at the TOP of THIS panel — **never on the rail.** Content is driven by the rail selection; own header + scroll.
- **Content** — working area right of both.

Rules: the hamburger always controls the panel; rail icons stay fixed. Never merge the two into one collapsible sidebar — that loses the always-available top-level nav.

Responsive behaviour (web system) — the rail/panel must CONVERT, never just vanish:
- **≥1280px:** rail + panel + content all visible. Hamburger in the rail toggles the panel.
- **≤1280px:** condense; keep rail + panel.
- **≤1024px (critical):** the secondary panel becomes an **overlay drawer**. The hamburger must **branch its JS** to open/close the drawer (toggle `.open-drawer`), NOT run the desktop collapse-inline logic — otherwise the panel becomes permanently unreachable. Content area does NOT shift; a backdrop sits behind the drawer; Esc / backdrop-tap closes.
- **≤768px:** rail → bottom bar. A **top bar appears the instant the rail is hidden** (see below). Never leave a breakpoint where neither the rail nor the top bar exists — that dead zone is the DEF-01/02 bug.

**Mobile top bar (web system, ≤768px) — 4 slots, NOT grouped:**
1. Hamburger — far left.
2. Logo — beside the hamburger (left cluster).
3. Search icon — right-aligned.
4. Profile photo — far right.
Left cluster = hamburger + logo; right cluster = search + profile. The hamburger opens the secondary nav as an overlay drawer. **The hamburger is NEVER in the bottom bar and is NEVER `display:none` — it moves to this top bar.** On desktop the hamburger lives in the rail and the logo sits atop the secondary panel; on mobile both surface together in this top bar (because the panel becomes a drawer).

**Mobile bottom bar:** primary nav tabs, **max 5**. If more than 5 items, show 4 + a "More" tab that reveals the rest as a sheet. Bottom bar holds primary tabs only — no hamburger.

Hard rule: the hamburger ALWAYS controls the secondary nav; rail/bottom-bar primary icons stay fixed. Never merge the two navs into one collapsible sidebar.

## 2. Custom dropdown / select — GLOBAL rule
Native `<select>` cannot be themed, width-matched, anchored, or dark-mode-styled — it breaks alignment and theme **anywhere**, not just in tables. Use a custom listbox **everywhere**: forms, filters, toolbars, table cells, panels.

Custom listbox requirements (or it's a dead/inaccessible control — Pillar 11 operability fail):
- Trigger button: matches input height + theme; chevron with proper padding (never flush to the edge).
- Popup: anchored to the trigger, width-matched, themed for light/dark, elevated above content.
- **Keyboard: arrow-key roving, Home/End, type-ahead, Enter/Space select, Esc close, focus returns to trigger.** Open/select/Esc alone is NOT enough.
- ARIA: `role="listbox"` / `role="option"`, `aria-expanded`, `aria-activedescendant`, selected state.
- Paginate/virtualize lists >10 options (Hick's Law).
- **Escape the scroll clip.** When the trigger sits inside a scrolling / `overflow:auto` container (table wrapper, panel), an absolutely-positioned menu gets clipped at the container edge. The popup must render above the clip — anchored to the trigger in on-screen space, layered above content — so the full list is always visible. Never let a dropdown be clipped by its scroll parent.

## 3. Deep data tables
For high column count (20+) and high row count (100s–1000s).

- **Sortable headers** — must actually sort AND expose `aria-sort` (ascending/descending/none). A header that looks sortable but does nothing is an operability fail. Show the sort direction indicator.
- **Pinned/frozen columns** — first column(s) (id/name) and any action column. Pinned cells need a **seamless solid backing** matching the row (including hover/selected), so scrolled content doesn't show through.
- **Sticky header** — stays on vertical scroll; reserve a **scrollbar gutter** so the header aligns with the body (no 1-column drift).
- **Bulk actions** — header checkbox (select-all / indeterminate), per-row checkbox, a contextual bulk-action bar appearing on selection.
- **Inline edit** — editable cells are real controls: focusable, ARIA-labelled, visible focus ring, Enter to commit / Esc to cancel. Not static `<div>`s.
- **Pagination or virtualization** for large sets — never render 1000 live DOM rows unpaginated.
- **Interactive data cells are controls** — any cell that drills down or sorts is keyboard-focusable with role/label + focus ring.

## 4. Wide-table responsive UX
When columns exceed viewport width:
- Confine horizontal scroll to the **table wrapper only** — never the page (`overflow-x: auto` on the wrapper, not body).
- Keep pinned column(s) visible while the rest scrolls.
- ≤768px: condense to essential columns + "expand row" for detail, OR switch to a stacked card-per-record layout. Don't shrink text below the floor to force-fit.
- Sticky bars (bulk-action bar, pagination) stay full-bleed at the narrowest breakpoint.

## 5. Sticky / pinned mechanics
- Sticky elements need a defined stacking order (header above body, pinned column above scroll content, bulk bar above rows).
- Solid/elevated backing on every sticky/pinned surface — never let content bleed through a transparent sticky element.
- Test sticky + pinned together (a frozen first column under a sticky header is the classic corner-cell bug — that corner needs the highest stack + solid backing).

## 6. Filter / toolbar groups
- Segmented controls, filter chips, tab groups, view toggles: **never orphan the last item on wrap** (Pillar 11 wrap discipline). If the group doesn't fit one row, drop the whole group to its own row or a balanced grid. Validate at the **narrow** end of the container.
- Filter chips: removable (x), show active count, clear-all affordance.
- Toolbar: primary actions left/visible, overflow into a kebab; never let actions wrap into a ragged second row.
