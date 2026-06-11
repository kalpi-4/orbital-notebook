# 🪐 Orbital Notebook

A single-file, zero-dependency N-body gravitational simulator with a built-in notebook — runs entirely in your browser, no server required.

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)
![No dependencies](https://img.shields.io/badge/dependencies-none-brightgreen.svg)
![Single file](https://img.shields.io/badge/size-single%20HTML%20file-orange.svg)

---

## What it does

Orbital Notebook lets you place bodies in space, give them mass and velocity, and watch them interact under Newtonian gravity. Kepler's laws, gravitational slingshots, orbital resonances, and tidal locking all emerge naturally from the physics — nothing is hardcoded.

Alongside the simulator sits a lightweight notebook where you can annotate your experiments with text, Markdown, and embedded orbit previews.

---

## Features

### Simulator
- **N-body physics** — full pairwise Newtonian gravity between any number of bodies
- **Leapfrog (Störmer-Verlet) integration** — energy-conserving symplectic integrator; not Euler
- **Adaptive timestep** — automatically shrinks during close approaches and slingshots
- **Collision merging** — bodies merge on contact, conserving momentum and mass; physical radii derived from realistic densities (rocky, gas giant, stellar)
- **Orbital resonance detection** — watches for simple integer period ratios (1:2, 2:3, etc.) and displays them live
- **Energy monitor** — tracks ΔE% so you can verify integration accuracy
- **Time warp** — 0.1× to 10,000× real-time via a continuous slider

### Camera & Navigation
- **Scroll to zoom** anchored to the cursor position
- **Right-click or middle-click drag** to pan in any mode
- **Follow mode** — click any body to lock the camera on it
- **Fit all** — auto-zooms to show every body
- **`+` / `−`** keyboard zoom · **`Home`** resets camera

### Tools
- **Place mode** (`P`) — click canvas to place a body; set mass, velocity direction and magnitude via a directional wheel or numeric inputs; live arrow preview on canvas
- **Pan mode** (`V`) — drag to move the view
- **Measure mode** (`M`) — click to measure distances between any two points; auto-formats in km, AU, or ly
- **Grid overlay** (`G`) — dynamic grid that rescales at any zoom level, with axis labels
- **Trails** (`T`) — color-coded orbital paths with gradient fade
- **Center of mass** crosshair toggle

### Presets
| Preset | Description |
|---|---|
| Solar System | Sun + 8 planets with real masses and orbital velocities |
| Earth–Moon | Correct tangential velocity, camera sized to the orbit |
| Binary Stars | Two equal stars in mutual circular orbit |
| Figure-8 | Chenciner–Montgomery three-body choreography |
| Blank | Empty canvas |

### Notebook
- **Text**, **Markdown**, and **Orbit** cell types
- Add, delete, duplicate, reorder (drag-and-drop) cells
- Markdown cells render headings, bold, italic, inline code
- Orbit cells show a live miniature preview of the current simulation
- Resizable panel; collapsible for full-screen simulation

### Export / Import
- Save your full session (notebook content + simulation state + camera) as JSON
- Reload any saved session instantly

---

## Getting started

Download `orbital_notebook.html` and open it in any modern browser. That's it.

```
git clone https://github.com/yourusername/orbital-notebook.git
cd orbital-notebook
open orbital_notebook.html   # macOS
# or just drag the file into your browser
```

No build step. No npm install. No server.

---

## Keyboard shortcuts

| Key | Action |
|---|---|
| `Space` | Play / Pause |
| `P` | Place mode |
| `V` | Pan mode |
| `M` | Measure mode |
| `G` | Toggle grid |
| `T` | Toggle trails |
| `F` | Fit all bodies |
| `+` / `−` | Zoom in / out |
| `Home` | Reset camera to origin |
| `Escape` | Close popover / cancel placement |

---

## Physics notes

The simulator uses a **velocity Verlet (leapfrog)** integrator. For a two-body system with stable initial conditions, total energy should remain constant to within a fraction of a percent over thousands of orbits — the ΔE% readout in the status bar lets you watch this live.

**Kepler's laws emerge from the integrator** — elliptical orbits, equal-areas-in-equal-times, and the T²∝a³ period-radius relationship all appear without being explicitly programmed.

**Gravitational slingshots** occur naturally when a low-mass body passes close to a massive one: the adaptive timestep shrinks to maintain accuracy through the close approach, and the body exits with a different velocity than it entered, exactly as in real mission planning.

**Collision detection** uses physical radii computed from body mass and a realistic bulk density (5,500 kg/m³ for rocky bodies, 1,400 kg/m³ for gas giants, 1,409 kg/m³ for stars). The visual size of a body on screen is independent and logarithmically scaled for legibility at all zoom levels.

---

## Browser compatibility

Works in any browser with Canvas 2D and ES2020 support — Chrome, Firefox, Safari, and Edge all work fine. No WebGL required.

---

## Contributing

Issues and pull requests are welcome. Some things that would be interesting to explore:

- Web Worker offload for the physics loop (decouples sim rate from frame rate)
- Barnes-Hut tree for large body counts (currently O(n²))
- Runge-Kutta 4 integrator option for comparison
- 3D mode via WebGL
- Real asteroid / exoplanet data import (CSV)

---

## License

MIT — do whatever you like with it.
