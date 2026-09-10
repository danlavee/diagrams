---
name: diagrams
description: Create or edit a diagram as a single SVG that carries its meaning and constraints with the drawing. Use when a task needs a vector diagram whose content and relationships live in one file.
---

# Diagrams

Deliver one SVG. It is the picture and the model. Declare `xmlns:sdl="https://diagrams.local/sdl"` on the root.

Work three phases in order, each writing into that file before the next starts. A later edit re-enters at the phase that owns the changed fact, walks every relationship that names it, and updates dependents — including paint.

## 1. Storyboard

Root `<metadata>` → `<sdl:diagram>`. Communicative facts only. No entities, no geometry.

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

Still under `<sdl:diagram>`. Still no paint. This is the ledger.

- **groups** — clusters or regions the storyboard called for (`<sdl:group id="…">`)
- **entities** — named things (`<sdl:entity id="…" kind="…" label="…">`) with the attributes relationships will bind
- **relationships** — semantic facts that must keep holding (`<sdl:rel kind="…" …>`): containment, flow, sequence, peers, sameness, alignment

A relationship names participants and the fact. Prefer predicates the next phase can discharge by copying and offsets; otherwise write the intent on the group.

Paint is not a second source of truth. Numbers that placement will need are filled onto these entities in phase 3.

## 3. Paint

Ordinary SVG. One `<g id="…">` per entity; geometry inside. Discharge every relationship into positions and sizes, write those values back onto the entities, then look at the rendered picture. Where a relationship promised equality, alignment, order, or grouping, the marks match it exactly.

## Change

Edit the ledger, not a lonely shape. Find every relationship that names the changed entity or attribute, update dependents, rewrite paint.

## File

`diagram.svg`. One file.
