# Self-Contained 2D Genetic Algorithm

Write a **single standalone HTML file** (with CSS and JS embedded) that implements a visually impressive 2D genetic algorithm simulation of evolving walking creatures on HTML5 Canvas. Do not use any external libraries or frameworks.

#### 1. Visual Style and Atmosphere (Cinematic Look)
* **Theme:** Dark neon style (Dark UI: background color `#0d1117`, grid lines, glowing elements).
* **Creatures:** Systems of connected line segments (muscles) and point masses (nodes). The leader of the current generation should be highlighted in vibrant neon green/gold with a glow effect; the rest should be semi-transparent white/blue.
* **Environment:** Flat ground with distance markers (10m, 20m, 50m, 100m...) and a couple of small hills/obstacles.
* **Camera:** Smoothly tracks the most successful creature (autocamera along the X-axis).

#### 2. Physics and Creature Genetics
* **Physics:** Simple particle physics (mass, gravity, ground friction, spring/muscle elasticity).
* **Structure:** Each creature is generated with a random structure (4–6 nodes connected by muscles).
* **Genome:** Muscle length pulses along a sine wave. Genes determine the phase, frequency, and amplitude of contraction for each muscle.
* **Evolutionary Algorithm:**
  * Population: 20 creatures simulated simultaneously.
  * Generation duration: 12 seconds (or transition early if all creatures stop moving).
  * **Fitness:** Maximum distance traveled to the right (X coordinate).
  * Selection: Top 20% leaders pass their genes to the next generation with slight random mutations.

#### 3. Interface (HUD) and Interactivity
* **On-screen Dashboard over Canvas (Glassmorphism / Minimalist):**
  * Generation number (Generation #)
  * Record distance (Best Distance)
  * Countdown timer for the current generation
  * Micro progress chart showing distance records over generations (Canvas / SVG in the corner).
* **Viewer Controls:**
  * Time acceleration slider (`1x`, `2x`, `5x`, `10x`) — to fast-forward evolution on video.
  * Buttons: `Reset`, `Generate New Creatures`, `Next Generation`.

#### 4. Technical Requirements
* The code must be completely self-contained within a single `.html` file.
* Optimized for 60 FPS on HTML5 Canvas.
* Must work immediately upon opening the file in any modern browser without build tools or web servers.