# Chicken Trail Designer

Single-file browser tool for laying out a chicken run built from Anleolife-style
cube extensions, and for checking whether the parts on hand can actually build it.

Open `index.html` in a browser — no build step, no server, no network. Rendering is raw
WebGL (no libraries): drag to orbit, right-drag to pan, wheel to zoom, click a cube face to
add the next cube against it.

## Model

A design is a set of unit cubes on a 24 x 24 grid, up to 4 levels high.
Panels are counted per cube face:

- a face shared with a neighbouring cube uses **no panel** — that is the passage the birds walk through
- an exterior side face uses a **side panel**
- an open top uses a **roof panel** (rule: *Roof every open top*)
- ground-level bottoms are bare soil unless *Floor panels at ground level* is on
- a boundary between stacked levels uses a **floor panel** unless that rule is off
### Connectors

Connectors sit on **edges**, not corners, and the type is forced by the geometry: for every
lattice edge the tool counts the panels reaching it and the angle between them.

| Panels on the edge | Connector |
|---|---|
| 2, coplanar | straight joiner (default letter **E**) |
| 2, at 90 deg, enclosing a cube | outside 90 deg (**D**) |
| 2, at 90 deg, enclosing empty space | inside 90 deg (**F**) |
| 3 | T joint |
| 4 | cross joint |
| 1 | free edge - nothing to join to |

So a plain box needs 8 outside corners and 4 free bottom edges; adding a floor makes all 12
outside corners; an L-shaped trail produces exactly one inside corner at the re-entrant turn;
a courtyard loop produces four. Stacking levels with a floor between them produces T joints
around the floor's perimeter.

Only the **vertical** edges are tracked as parts, since those are the side connectors that run
short. Roof and floor joiners are counted and reported under *This design*, but never limit a
build. The letters are editable - type the codes off your own parts bags into the boxes in
*Parts on hand*, and they follow through to the bill of materials and the legend.
Two multipliers sit under the parts list: **connectors per joined edge** (if a single edge
takes more than one piece) and **screws per connector**, which drives the fastener total.

Any single face can be overridden in the *Selected cube* card: shift-click a cube (or use the
Select tool) and click a face to cycle `auto -> wall -> open -> door`. That is how a gate gets
into a wall. Faces shared with a neighbouring cube stay open passages whatever they are set to,
so a door has to go on an exterior face. Door panels draw as a solid sheet with three view
slots, mesh panels as see-through wire. The compass in the corner of the view gives the
bearings the face names use.

## Cards

- **Parts on hand** — your inventory. Untracked parts are tallied but never limit a build.
  Set the cube edge to match your panels (a 1 m panel is 39.4 in).
- **Bill of materials** — need vs. have vs. spare for the current design.
- **This design** — footprint, volume, longest trail, dead ends, junctions, reachability
  from the cube marked as the coop door.
- **What your parts can build** — the largest tunnel / two-wide run / block / loop /
  two-story run your tracked parts allow, and which part runs out first.

## Controls

Click a cube face to add the next cube against it, or click the ground to start one.
`Erase` removes, `Select` (or shift-click) opens the face inspector, `Coop door` marks the
entrance. Drag orbits, right-drag pans, wheel zooms.
Keys: `1-4` ground level, `q`/`e` orbit, `f` frame all, `b`/`x`/`s`/`d` tools,
`c` connector colours, `h` roof on/off, `z` undo.

Design and inventory autosave in the browser; JSON export/import and PNG export
are in the *Save / load* card.
