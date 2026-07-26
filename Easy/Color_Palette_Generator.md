# Color Palette Generator

Create a single **index.html** file that generates random color palettes. The goal is a simple, visually pleasing tool that demonstrates working with colors, events, and the Clipboard API.

### Core Requirements

* **Palette Display**:
    * Show **5 color swatches** side by side, each filling an equal share of the screen width.
    * Each swatch displays its **HEX code** (e.g. `#3FA7D6`) centered on the color. Pick black or white text automatically based on the background brightness so the code is always readable.
* **Generation**:
    * A **"Generate" button** (and the **Spacebar** as a shortcut) replaces all unlocked colors with new random ones.
* **Locking**:
    * Each swatch has a **lock icon** (🔓 / 🔒). Clicking it toggles the lock; locked colors survive regeneration so the user can build a palette gradually.
* **Copy to Clipboard**:
    * Clicking a swatch's HEX code copies it to the clipboard and shows a brief **"Copied!"** confirmation (e.g. a small toast or a temporary label change).
* **Polish**:
    * Add a short CSS transition when colors change so the swap feels smooth rather than jarring.

### Technical Constraints
* Everything must be contained in a **single HTML file** (HTML, CSS, and JavaScript).
* Use standard **Vanilla JavaScript** (no external libraries or complex frameworks).
* The code should be easy to read and well-commented.
