# Design system pipeline map

An interactive map of how a design system stays the same in Figma and in code: what is defined where,
what is generated from it, and which automated checks catch drift. It also shows where AI agents fit in.

**View it:** https://dgwillia.github.io/DesignSystemMap/

## What it shows

- **Overview.** The whole system in six ideas. Point at an idea to highlight the parts it covers.
- **Hover any box** for a one-line explanation of its role. Click it for the detail: what it defines,
  who makes it, and which checks guard it.
- **Replay a change.** Eight step-by-step scenarios: a token changing in Figma or in code, a hand edit to
  a generated file, new and changed components, and an AI agent building a screen.

## The model in brief

- **Tokens: Figma leads.** Variables are exported to a snapshot in the repo, then built into code.
- **Components: code leads. Figma mirrors it.** A parity check compares the two, prop by prop.
- **Generated files are never edited by hand.** A check rebuilds them and fails if anything differs.
- **Agents follow written rules** (`AGENTS.md`, `DESIGN.md`, `GAPS.md`) and read real props through
  Storybook's MCP add-on. A person reviews and merges.

## Adapt it to your own system

Everything the map shows lives in [`map-data.js`](map-data.js). Edit that file; you shouldn't need to touch
`index.html`.

| In `map-data.js` | What it is |
|---|---|
| `NODES` | The boxes: label, role (source of truth, generated, copy, hand-written, mirror, uses it) and hover text |
| `CHECKS` | The checks along the bottom: what each compares, when it runs, when it fails |
| `EDGES` | The arrows, as SVG paths |
| `IDEAS` | The six ideas in the overview |
| `SCENARIOS` | The walkthroughs. Each step lists the boxes (`n`), arrows (`e`) and check results (`c`) to show |
| `WHERE` | The "What is defined where" table |

File and command names (`npm run parity`, `figma-snapshot.json`) are examples. Swap in your own.

## Run it locally

No build step. Open `index.html` in a browser, or serve the folder:

```sh
npx serve .
```
