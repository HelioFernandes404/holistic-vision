# holistic-html

A Claude Code skill that generates self-contained `.html` files instead of markdown — for documentation, reports, plans, code reviews, explainers, status updates, slide decks, and more.

## Install

```bash
npx holistic-html
```

Copies the skill and all 20 example files to `~/.claude/skills/holistic-html/`. Available in every Claude Code project after that.

## What it does

When you ask Claude for something that would normally produce a wall of markdown — an explanation, a plan, a report, a comparison — this skill produces a single browser-ready `.html` file instead.

The output uses the **GitHub Dark Minimalist** design system: dark background (`#0d1117`), JetBrains Mono body, GitHub-style tokens, no external dependencies.

## Examples

20 reference files organized by use case:

| Category | Examples |
|---|---|
| `examples/01-exploration/` | Code approaches, visual design directions, implementation plan |
| `examples/02-code-review/` | Annotated PR, module map, PR writeup |
| `examples/03-design/` | Living design system, component variants |
| `examples/04-prototyping/` | Animation sandbox, clickable flow |
| `examples/05-diagrams/` | SVG figure sheet, annotated flowchart |
| `examples/06-decks/` | Arrow-key slide deck |
| `examples/07-research/` | Feature explainer, concept explainer |
| `examples/08-reports/` | Weekly status, incident timeline |
| `examples/09-editors/` | Triage board, feature flag editor, prompt tuner |

Open `index.html` in a browser to browse them all.

## Skill structure

```
~/.claude/skills/holistic-html/
├── SKILL.md
├── references/
│   ├── design-tokens.md
│   └── pattern-catalog.md
└── examples/
    └── 01-exploration/ … 09-editors/
```

## License

MIT
