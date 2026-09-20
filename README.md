# Chicken Trail Designer

Single-file browser tool for laying out a chicken run built from Anleolife-style
cube extensions, and for checking whether the parts on hand can actually build it.

Open `index.html` in a browser — no build step, no server, no network.

## Model

A design is a set of unit cubes on a 24 x 24 grid, up to 4 levels high.
Panels are counted per cube face:

- a face shared with a neighbouring cube uses **no panel** — that is the passage the birds walk through
- an exterior side face uses a **side panel**
- an open top uses a **roof panel** (rule: *Roof every open top*)
- ground-level bottoms are bare soil unless *Floor panels at ground level* is on
- a boundary between stacked levels uses a **floor panel** unless that rule is off
- **corner connectors** = unique lattice vertices, **frame bars** = unique lattice edges

Any single face can be overridden in the *Selected cube* card:
`auto -> wall -> open -> door`.

## Cards

- **Parts on hand** — your inventory. Untracked parts are tallied but never limit a build.
  Set the cube edge to match your panels (a 1 m panel is 39.4 in).
- **Bill of materials** — need vs. have vs. spare for the current design.
- **This design** — footprint, volume, longest trail, dead ends, junctions, reachability
  from the cube marked as the coop door.
- **What your parts can build** — the largest tunnel / two-wide run / block / loop /
  two-story run your tracked parts allow, and which part runs out first.

## Controls

Click to place or select, `Erase` to remove, `Coop door` to mark the entrance cube.
Right- or middle-drag pans, wheel zooms. Keys: `1-4` level, `q`/`e` rotate,
`b`/`x`/`d` tools, `z` undo.

Design and inventory autosave in the browser; JSON export/import and PNG export
are in the *Save / load* card.
