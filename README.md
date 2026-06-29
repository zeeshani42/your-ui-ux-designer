<img width="1456" height="819" alt="Cover" src="https://github.com/user-attachments/assets/b403b70b-21c1-4221-99b6-1011c8530202" /> # UI/UX Designer — a design skill for Claude

A universal UI/UX **design** skill for Claude. Generate production-grade dashboards, landing pages, and mobile screens — with real states, responsive breakpoints, accessibility, and a consistent design system — across HTML, Figma, Claude Design, or any design tool.

Most design tooling for AI targets raw HTML/CSS or graphics. This is a true **UI/UX** skill: it thinks in screens, navigation, interaction, and design systems — not just markup.


---

## What it does

- **Three build archetypes** — Web system (dashboard / admin / SaaS), Landing page, and Mobile app. Each locks the right viewport, navigation, and presentation automatically.
- **Enterprise navigation** — the Gmail-style dual nav (fixed icon rail + collapsible secondary panel) that reflows correctly to a mobile top bar + bottom bar.
- **11 design styles** — Minimal, Material 3, Bento, Glassmorphism, Liquid Glass, Spatial, Aurora, Neo-Brutalism, and more — genuinely distinct, not recolors.
- **Bring your own design system** — share tokens, a link, or an image; it adopts them and derives what's missing.
- **Real output, not descriptions** — every screen ships Default / Loading / Empty / Error states, focus rings, four responsive breakpoints, and a `prefers-reduced-motion` fallback.
- **Built-in validation** — checks that charts actually paint, controls actually work, and contrast actually passes, before delivering.

---

## Install

1. Download **`ui-ux-designer.skill`** from this repo (see the file list above, or the [Releases](../../releases) page).
2. In Claude: **Settings → Capabilities → Skills → Upload skill**.
3. Select the `.skill` file. Done — it installs automatically.

> The skill triggers on any UI/UX request. You can also invoke it explicitly with `/ui-ux-designer`.

---

## Try it

Paste any of these into Claude after installing:

```
Build a dashboard for a logistics shipment-tracking platform. Output as HTML.
```

```
Build a landing page for a B2B fintech product that does automated invoice reconciliation. Output as HTML.
```

```
Design a mobile app screen for a field-service technician — a job list with status, and a job detail view. Output as HTML, light and dark.
```

The skill will ask a few quick questions (style, dark mode, etc.), then build.

---

## How it's built

A lean core file plus conditional reference files (styles, patterns, mobile, Figma) that load only when relevant — so the skill stays fast and never drops rules under load.

```
ui-ux-designer/
├── SKILL.md            core spine
└── references/
    ├── styles.md       11 style definitions
    ├── patterns.md     navigation, tables, dropdowns
    ├── mobile.md       touch / gesture / mobile spec
    └── figma.md        Figma auto-layout & variants
```

---

## Feedback & contributing

Found a case where it gets something wrong, or have an idea? Open an [Issue](../../issues) — real examples (a prompt + a screenshot) are the most useful. Improvements are folded back into the skill.

---

## License

MIT — free to use, modify, and share. Please keep the attribution.

---

Built by **Zeeshan ur Rehman**, Principal UX Designer.

[LinkedIn](https://www.linkedin.com/in/zeeshan-ur-rehman-59a00630) · [YouTube](https://www.youtube.com/@ZeeShani42)
