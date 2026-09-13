---
name: diagrams
description: Create or edit a diagram as a single SVG that carries its meaning and constraints with the drawing. Use when a task needs a vector diagram whose content and relationships live in one file.
---

# Diagrams

Deliver one SVG. It is the picture and the model. Declare `xmlns:sdl="https://diagrams.local/sdl"` on the root.

Work three phases in order, each writing into that file before the next starts. A later edit re-enters at the phase that owns the changed fact, walks every relationship that names it, and updates dependents — including paint.

A fact about one node lives on that node. A fact about more than one node lives on the lowest parent that contains all of them. Picture facts live only on the marks. SDL holds kind, relationships, and the brief.

When placing nodes, or when paint would add an extra joint, an occupancy fight, or a meeting the relationships do not settle, read `references/composition.md` before finishing composition.

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

Still no paint. Open the nodes the storyboard requires: `<g id="…" sdl:kind="…">`. Node-local meaning the renderer does not own is an attribute of that element. Nested `<g>` is containment.

A relationship is `<sdl:rel>` on the lowest parent that contains all of its participants. It is a semantic fact that must keep holding. It names the participants and the fact. Prefer predicates the next phase can discharge by copying and offsets; otherwise write the intent on that parent. Copy, offset, and gap stay on that relationship.

Follow `references/composition.md`.

## 3. Paint

Marks inside those groups. Discharge every `<sdl:rel>` onto those marks. Position, size, path, ink, and visible words live only on the marks. Then look at the rendered picture per `references/composition.md`.

## Change

Edit the home of the fact: the mark that draws a picture fact, `sdl:*` on the node for meaning, or the parent that holds the relationship. Find every `<sdl:rel>` that names the changed node, update dependents, and write new geometry only on the marks.

## File

`diagram.svg`. One file.
