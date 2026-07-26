# Pixel Art Editor

Create a single **index.html** file implementing a small pixel art editor. The goal is a functional drawing tool that demonstrates canvas rendering, tool state machines, a flood-fill algorithm, and file export.

### Core Requirements

* **Canvas**:
    * A drawing grid rendered on a `<canvas>`, with selectable sizes: **16×16, 32×32, 64×64** (switching sizes asks for confirmation and clears the drawing).
    * Show a subtle grid overlay; a checkbox toggles it on/off. Transparent pixels render as a light checkerboard pattern.
    * Drawing works by clicking **and by dragging** with the mouse button held down.
* **Tools** (selectable via a toolbar with a visible active state):
    * **Pencil** — paints the current color.
    * **Eraser** — makes pixels transparent.
    * **Fill (bucket)** — flood-fills the contiguous same-colored area (implement the algorithm yourself, e.g. BFS; it must not stack-overflow on 64×64).
    * **Eyedropper** — picks the color of the clicked pixel and makes it the current color.
* **Color Handling**:
    * A native **color picker** plus a palette of ~16 preset color swatches.
    * A strip of the **8 most recently used colors** that updates as the user draws.
* **Undo / Redo**:
    * At least 20 steps of history, wired to buttons and to **Ctrl/Cmd+Z / Ctrl/Cmd+Shift+Z**. One drag stroke counts as a single undo step.
* **Export & Persistence**:
    * **"Download PNG"** exports the artwork at a sensible scale (e.g. each pixel becomes a 10×10 block) with transparency preserved.
    * The current drawing auto-saves to `localStorage` and is restored on reload.
    * A **"Clear"** button wipes the canvas after confirmation.

### Technical Constraints
* Everything must be contained in a **single HTML file** (HTML, CSS, and JavaScript).
* Use standard **Vanilla JavaScript** and the raw Canvas API — no external libraries.
* Rendering must stay crisp: no anti-aliasing artifacts on pixel edges at any grid size.
* The code should be easy to read and well-commented.
