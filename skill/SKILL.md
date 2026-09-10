---
name: diagrams
description: Create or edit a diagram as a single SVG that carries its meaning and constraints with the drawing. Use when a task needs a vector diagram whose content and relationships live in one file.
---

# Diagrams

Deliver one SVG. It is the picture and the model. Declare `xmlns:sdl="https://diagrams.local/sdl"` on the root.

Work three phases in order, each writing into that file before the next starts. A later edit re-enters at the phase that owns the changed fact, walks every relationship that names it, and updates dependents — including paint.

A fact about one node lives on that node. A fact about more than one node lives on the lowest parent that contains all of them.

## 1. Storyboard

Root `<metadata>` → `<sdl:diagram>`. Communicative facts only. No nodes, no geometry.

Write every tag that has something to say; skip the rest.

| Tag | Holds |
| --- | --- |
| `sdl:narrative` | identity and subject of the diagram |
| `sdl:message` | what a cold reader must take away |
| `sdl:storyboard` | the beats the eye should take in, in order |
| `sdl:type` | what kind of picture this is, when that is part of the request |
| `sdl:audience` | who it is for, when that changes what must be shown |
| `sdl:interactivity` | what can be pointed at, revealed, or followed, when the picture is not static |
| `sdl:look` | character of the figure — weight, density, tone |

## 2. Composition

Still no paint. Open the nodes the storyboard requires: `<g id="…" sdl:kind="…">`. Node-local facts are attributes of that element. Nested `<g>` is containment.

A relationship is `<sdl:rel>` on the lowest parent that contains all of its participants. It names the participants and the fact. Prefer predicates the next phase can discharge by copying and offsets; otherwise write the intent on that parent.

## 3. Paint

Marks inside those groups. Discharge every `<sdl:rel>` into positions and sizes on the nodes it names; marks use those values. Then look at the rendered picture. Where a relationship promised equality, alignment, order, or grouping, the marks match it exactly.

## Change

Edit the node a fact is about, or the parent that holds the relationship, not a lonely mark. Find every `<sdl:rel>` that names the changed node, update dependents, rewrite paint.

## File

`diagram.svg`. One file.
