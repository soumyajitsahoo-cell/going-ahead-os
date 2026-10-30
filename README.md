# AetherOS

A self-contained web desktop environment implemented in a single `index.html` file. It runs entirely in the browser with no build step, compiler, or external backend.

## Overview

The entire operating system interface, window manager, state layer, and application suite live inside `index.html`. It simulates a desktop interface with optical glass styling, draggable and resizable windows, procedural audio, and persistent local storage.

## Getting Started

No installation or build process is required.

### Run Directly
Open `index.html` directly in any modern desktop browser (Chrome, Edge, Firefox, Safari):
- Double-click `index.html`, or
- Right-click `index.html` and choose "Open with" -> preferred browser.

### Run via Local HTTP Server (Optional)
Using Python:
```bash
python -m http.server 8000
```
Then navigate to `http://localhost:8000`.

Using Node.js:
```bash
npx serve .
```

## Structure of index.html

The file is organized into three primary sections:

1. **HTML & Head Declarations**
   - Viewport and document metadata.
   - Google Fonts (`Instrument Serif`, `Inter`, `JetBrains Mono`).
   - Tailwind CSS via CDN (`cdn.tailwindcss.com/3.4.17`).
   - Inline SVG filter definitions for real-time optical glass refraction (`feDisplacementMap`).

2. **CSS Design Tokens & Glass Styles**
   - CSS custom properties defining blur, saturation, specular highlights, and refraction levels.
   - Light and dark theme palettes.
   - Window physics, dock styling, and layout definitions.

3. **Core JavaScript Engines & UI Logic**
   - **OpticalRefractionEngine**: Generates squircle normal maps on an offscreen canvas to drive SVG displacement filters.
   - **WallpaperEngine**: Renders procedural gradient orbs on an HTML5 canvas with mouse parallax.
   - **SoundEngine**: Procedural UI sound effects and ambient sound synthesis using the Web Audio API.
   - **OSState & VFS**: In-memory state and virtual file system persisted to browser `localStorage` under `aetheros_optical_state_v2`.
   - **Window Manager**: Handles dragging, resizing, minimizing, maximizing, focus stacking (z-index), and dock magnification.

## Built-in Applications

The OS includes nine integrated client-side applications:

- **Files**: Virtual file explorer with support for creating, opening, and deleting virtual files.
- **Notes**: Text editor connected to the virtual file system.
- **Terminal**: Simulated shell supporting commands like `help`, `ls`, `cat`, `touch`, `clear`, and `neofetch`.
- **Prism Paint**: Canvas-based drawing tool with brush and color controls.
- **Pulse Music**: Ambient synthesizer and audio sequencer using the Web Audio API.
- **Tasks Flow**: Kanban task manager and productivity timer.
- **Activity**: System telemetry monitor tracking mock CPU, memory usage, and open window instances.
- **Calculator**: Arithmetic expression evaluator supporting mouse and keyboard input.
- **Settings**: System preferences for themes, wallpaper selection, blur radius, and refraction intensity.

## Tech Stack

- **Markup & Layout**: HTML5, Tailwind CSS
- **Visual Effects**: CSS Backdrop Filter, Canvas 2D, SVG Filters
- **Audio**: Web Audio API (procedural synthesis)
- **State**: Vanilla JavaScript (ES6+), Web Storage API (`localStorage`)
- **External Resources**: Tailwind CSS CDN, Google Fonts (falls back to system fonts offline)
