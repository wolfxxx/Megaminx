# Megaminx (Three.js, Piece-Based MVP)

An interactive browser-based Megaminx simulator built with Three.js.

This project renders a 12-face dodecahedron puzzle, lets you select faces by clicking, and supports clockwise/counterclockwise turns with animation, scramble, and reset.

## Features

- 3D Megaminx rendering using Three.js (`WebGLRenderer`)
- Click-to-select faces
- Face turns:
  - `E` = clockwise
  - `Q` = counterclockwise
- Scramble:
  - `S` key or button (`40` random turns)
- Reset to solved state
- Orbit camera controls (drag/orbit/zoom)
- Solved-state indicator
- Startup move self-check:
  - Validates `CW` + `CCW` inverse behavior
  - Validates `5x CW` identity on each face
  - Reports pass/fail in UI

## Tech Stack

- HTML + CSS + JavaScript (single-file app)
- [Three.js](https://threejs.org/) via ES module import map
- OrbitControls from Three.js examples

## How It Works (High Level)

The simulator:

1. Builds a dodecahedron core.
2. Extracts face groups and adjacency/topology from geometry.
3. Tracks puzzle state with piece permutation/orientation arrays:
   - Edges: permutation + orientation
   - Corners: permutation + orientation
4. Draws sticker meshes per face slot:
   - 1 center pentagon
   - 5 between-corner triangles (edge stickers)
   - 5 corner diamonds (corner stickers)
5. On each move:
   - Animates affected stickers around the selected face axis
   - Applies permutation/orientation updates to state
   - Recomputes slot colors from current state

## Controls

- Mouse:
  - Click sticker to select a face
  - Drag to orbit camera
  - Scroll to zoom
- Keyboard:
  - `E`: Rotate selected face CW
  - `Q`: Rotate selected face CCW
  - `S`: Scramble
- UI Buttons:
  - Rotate CW
  - Rotate CCW
  - Scramble
  - Reset

## Selected Face Info

The UI shows:

- Selected face number (`#1`..`#12`)
- Center color name in bold and in that color

## Running Locally

Because this app imports ES modules from a CDN, run it through a local web server (not `file://`).

Example options:

```bash
# Python
python -m http.server 8080
```

Then open:

`http://localhost:8080/`

## File Layout

- `index.html` - complete application (UI, rendering, puzzle logic)
- `README.md` - project documentation

## Notes

- This is a practical piece-based MVP with working move/state flow and UI.
- It is structured so future upgrades are straightforward (move notation parser, proper scramble notation display, timers, solve helpers, etc.).

## License

No license file is included yet. Add one if you want to define reuse terms.
