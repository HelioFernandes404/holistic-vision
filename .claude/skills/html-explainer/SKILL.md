---
name: html-explainer
description: Produce a self-contained HTML file instead of markdown for any output that benefits from visual structure. Use this skill whenever the user asks for documentation, a report, a writeup, a plan, an explanation, a code review summary, a diagram, a status update, a slide deck, or any content that would otherwise become a wall of markdown text. Even when the user doesn't say "HTML", if the output has structure, comparisons, timelines, code with annotations, or multiple sections, an HTML file will serve them far better. Use the repository's example HTML files as the visual and structural reference.
---

# html-explainer

When producing output that has meaningful structure -- comparisons, phases, timelines, code explanations, reports, plans -- a self-contained HTML file is almost always better than markdown. Markdown gets skimmed; HTML gets read.

Your job is to:
1. Identify which structural pattern fits the request
2. Build a complete self-contained HTML using the closest example file as reference
3. Write the file to disk and tell the user where it is

---

## Choosing the right pattern

Match the request to a structural pattern. Read the closest example HTML file before writing the new page. The examples are the source of truth for visual style, spacing, typography, color palette, and interaction treatment.

| Request type | Pattern |
|---|---|
| Compare approaches, options, or designs | **Side-by-side** |
| PR, diff, or code change explanation | **Annotated document** |
| Codebase walkthrough, module relationships | **Module map / diagram** |
| How a feature or concept works | **Feature explainer** (sticky nav, collapsible steps, TL;DR) |
| Implementation or project plan | **Phased plan** (milestones, phases, risk table) |
| Weekly/sprint status | **Status report** (chart, shipped/slipped/next) |
| Incident or post-mortem | **Incident timeline** |
| Slide presentation | **Slide deck** (scroll-snap, arrow-key nav) |
| Design tokens, component states | **Design system / component sheet** |
| Interactive prototype, animation tuning | **Prototype / sandbox** |
| Process flow, deploy pipeline | **Flowchart** (SVG, clickable nodes) |
| Drag/organize/prioritize items | **Triage editor** (with export button) |
| Toggle flags or config | **Flag/config editor** |
| Prompt or template tuning | **Prompt tuner** |

When the request doesn't match cleanly, default to the **Feature explainer** pattern -- it handles most documentation well.

**Example file locations** (relative to this skill's install dir):
| Category | Path |
|---|---|
| Exploration / planning | `examples/01-exploration/` |
| Code review | `examples/02-code-review/` |
| Design | `examples/03-design/` |
| Prototyping | `examples/04-prototyping/` |
| Diagrams | `examples/05-diagrams/` |
| Decks | `examples/06-decks/` |
| Research | `examples/07-research/` |
| Reports | `examples/08-reports/` |
| Editors | `examples/09-editors/` |

---

## HTML construction rules

### Always self-contained
- No external CSS or JS CDN links. Everything inline in `<style>` and `<script>`.
- Fonts: use system stacks. Don't load Google Fonts.
- SVG icons: inline. No icon library imports.

### Structure
Every page needs:
- `<!doctype html>` + `<html lang="en">`
- `<meta charset="utf-8">` and viewport meta
- A descriptive `<title>` derived from the actual content
- Inline CSS based on the selected example
- A clean reset appropriate to that example

### Visual style
- Preserve the native look of the selected example: palette, typography, border weight, radius, spacing, and layout density.
- Adapt class names and content as needed, but do not convert the page to another global design system.
- Keep responsive behavior from the example when it applies.
- Use new styles only when the content requires them.

---

## Patterns with interactive JS

For patterns that need interactivity (slide decks, editors, triage boards):

**Slide deck** -- keyboard nav:
```js
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight' || e.key === 'ArrowDown') nextSlide();
  if (e.key === 'ArrowLeft'  || e.key === 'ArrowUp')   prevSlide();
});
```
Use `scroll-snap-type: y mandatory` on `body`, `scroll-snap-align: start` on each `.slide`.

**Editors with export** -- always end with a button that serializes the current state to text the user can paste or commit. The export closes the loop between the HTML artifact and the next step in the user's workflow.

**Collapsible sections** — for explainers with many steps:
```html
<details>
  <summary>Step 3 -- Request hits rate-limit middleware</summary>
  <div class="detail-body">…</div>
</details>
```
Style `summary` with `cursor: pointer`, `padding: 0.5rem 0`, and a marker indicating expand/collapse state.

---

## What to do when the skill triggers

1. Read the user's request carefully — identify the content type and the information they want communicated.
2. Choose the pattern from the table above.
3. Read the closest matching example file from `examples/<category>/<file>.html` and use it as the visual and structural starting point.
4. Write the complete HTML to a file named descriptively (e.g., `feature-auth-explainer.html`, `week-23-status.html`, `refactor-plan.html`). Save it in the project root or wherever makes sense for the context.
5. Open it in the browser if possible: `xdg-open <filename>.html`
6. Tell the user the filename and what pattern you used.

---

## Quality check before delivering

- [ ] Opens in a browser with no external requests
- [ ] Visual style follows the selected example instead of a separate global theme
- [ ] Title is specific to the actual content, not generic
- [ ] Content is real — populated from the user's actual request, not placeholder Lorem Ipsum
- [ ] Interactive elements (if any) have visible focus styles
- [ ] The page would be useful to someone who has never seen the source markdown
