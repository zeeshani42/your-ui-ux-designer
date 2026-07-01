<div align="center">
<img width="1456" height="819" alt="Cover" src="https://github.com/user-attachments/assets/0caf6ecf-8808-4ce6-bbf3-1b7fa6e95a66" /> 
</div>

<br/>

# UI/UX Designer — a design skill for Claude

A universal UI/UX design skill for Claude. Generate production-grade dashboards, landing pages, and mobile apps with real states, responsive navigation, and a consistent design system. across HTML, Figma, Claude Code, or any design tool.

Most design tooling for AI targets raw HTML/CSS or graphics. This is a true **UI/UX skill**: it thinks in screens, navigation, interaction, and design systems not just markup.

---

## What makes it different

- **11 design styles** — Minimal, Material 3, Bento, Glassmorphism, Liquid Glass, Spatial, Aurora, Neo-Brutalism, and more — genuinely distinct, not recolored variants
- **Enterprise navigation** — the Gmail-style dual nav (fixed icon rail + collapsible secondary panel) that reflows correctly to a mobile top bar + bottom bar
- **Bring your own design system** — share tokens, a link, or an image; it adopts them and derives what's missing
- **Real output, not descriptions** — every screen ships Default / Loading / Empty / Error states, focus rings, four responsive breakpoints, and a `prefers-reduced-motion` fallback
- **Built-in validation** — checks that charts actually paint, controls actually work, and contrast actually passes, before delivering

---

<img width="1400" height="357" alt="1 — KPI Row" src="https://github.com/user-attachments/assets/3c0f4f83-f7b5-4ff0-abf6-d170237bdc01" />

<img width="1600" height="869" alt="2 — Score by Output Format" src="https://github.com/user-attachments/assets/049285a8-07ba-4c18-9511-10f7aec8c617" />

<img width="1600" height="924" alt="3 — Criterion Scores" src="https://github.com/user-attachments/assets/86ad7055-56e8-4a00-ae27-fc29a87f484b" />


## Benchmark results

Tested across **30 cases** — Aviation, Transport, and HRM — scored on a 10-criterion rubric.

| Output format | Cases | Sonnet 4.6 | Opus 4.8 |
|---|---|---|---|
| Claude Chat | 30 | 91.1 / 100 | — |
| HTML | 6 | 86.7 / 100 | 93.0 / 100 |
| Figma | 6 | 75.2 / 100 | 88.0 / 100 |
| Spec / Annotation | 6 | 89.7 / 100 | — |
| Components | 6 | 91.2 / 100 | — |
| UI Elements | 6 | 90.8 / 100 | — |
| **Overall** | **30** | **86.7 / 100** | |

**Route HTML and Figma outputs to Opus 4.8** — it resolves the responsiveness gap (breakpoints and reflow go from 75 to 88–93). Spec and components already score 89–91 on Sonnet, no lift needed.

### Criterion scores (post-fix, Opus 4.8)

| Criterion | Score |
|---|---|
| Screen type logic | 9.6 / 10 |
| Style fidelity | 9.5 / 10 |
| Contrast — 3 rules | 9.2 / 10 |
| 8pt grid | 9.1 / 10 |
| Enterprise grade | 8.6 / 10 |
| State completeness | 8.4 / 10 |
| Interaction layer | 8.0 / 10 |
| Responsiveness — breakpoints | 9.0 / 10 |
| Responsiveness — behavior | 9.0 / 10 |

---

## Compatible with

<table>
  <tr>
    <td align="center" width="20%">
        <img width="40" height="40" alt="image" src="https://github.com/user-attachments/assets/45baf16f-9fa5-4675-850c-19ddf55d80a1" /><br/>
      <strong>Claude Chat</strong><br/>
      <sub>Tested · 91.1</sub>
    </td>
    <td align="center" width="20%">
        <img width="40" height="40" alt="image" src="https://github.com/user-attachments/assets/c0c43f6b-37c6-45f1-bc2c-1133b01bb1c4" /><br/>
      <strong>Claude Code</strong><br/>
      <sub>Supported</sub>
    </td>
    <td align="center" width="20%">
        <img width="40" height="40" alt="image 1" src="https://github.com/user-attachments/assets/b24d6bb9-409a-47dc-b363-cd16f520da26" /><br/>
      <strong>Claude Cowork</strong><br/>
      <sub>Supported</sub>
    </td>
    <td align="center" width="20%">
        <img width="40" height="40" alt="figma icon" src="https://github.com/user-attachments/assets/73b8a7ea-c3ce-457e-88b5-524ea6e94ba5" /><br/>
      <strong>Figma</strong><br/>
      <sub>Tested · 88.0</sub>
    </td>
    <td align="center" width="20%">
        <img width="40" height="40" alt="html5" src="https://github.com/user-attachments/assets/9994e866-b452-4f8d-9e6c-c6070c3cd165" /><br/>
      <strong>HTML</strong><br/>
      <sub>Tested · 93.0</sub>
    </td>
  </tr>
</table>

---

## Install

1. Download `ui-ux-designer.skill` from this repo (see the file list above, or the [Releases](../../releases) page)
2. In Claude: **Settings → Capabilities → Skills → Upload skill**
3. Select the `.skill` file. Done — it installs automatically

The skill triggers on any UI/UX request. You can also invoke it explicitly with `/ui-ux-designer`.

---

## Try it

Paste any of these into Claude after installing:

```
Build a landing page for a B2B fintech product that does automated invoice reconciliation. Output as HTML.
```

```
Design a mobile app screen for a field-service technician — a job list with status, and a job detail view. Output as HTML.
```

The skill will ask a few quick questions (style, dark mode, etc.), then build.

---

## How it's built

A lean core file plus conditional reference files (styles, patterns, mobile, Figma) that load only when relevant — so the skill stays fast and never drops rules under load.

```
ui-ux-designer/
├── SKILL.md          core spine
└── references/
    ├── styles.md     11 style definitions
    ├── patterns.md   navigation, tables, dropdowns
    ├── mobile.md     touch / gesture / mobile spec
    └── figma.md      Figma auto-layout & variants
```

---

## Feedback & contributing

Found a case where it gets something wrong, or have an idea? Open an [issue](../../issues) — real examples (a prompt + a screenshot) are the most useful. Improvements are folded back into the skill.

---

## License

MIT — free to use, modify, and share. Please keep the attribution.

Built by **Zeeshan ur Rehman**, Principal UX Designer.

[LinkedIn](https://linkedin.com/in/zeeshanirehman) · [YouTube](https://youtube.com/@zeeshanirehman)
