# Project Description: HantaSim

## 1. Brief Overview

**HantaSim** is an interactive 2D top-down simulation of hantavirus spread in a closed population, implemented in **Rust** and **Bevy 0.18**.

The project does not model the classic person-to-person transmission pattern. Instead, it demonstrates an environmental infection model:

> **Core simulation rule:** hantavirus is not transmitted directly between humans. Mice act as carriers, leave contaminated clouds in the environment, and humans become infected only when they enter those clouds.

The project is intended for educational and demonstration purposes and is not designed for medical or epidemiological forecasting.

---

## 2. Current Project State

The project is in a working state and provides a full interactive simulation with:

- world, population, mouse, and point-of-interest generation;
- movement models for humans and mice;
- environmental contamination through viral clouds;
- human infection through contaminated clouds;
- disease and immunity progression;
- statistics, charts, and R0 estimation;
- a UI panel for configuring simulation parameters;
- pause, time acceleration, and simulation restart;
- saving and loading the complete simulation state;
- persistent user settings between launches.

The main logic is already split into modules, the project uses Bevy's ECS approach, and the execution order of systems is explicitly defined through the `SimulationSet` chain.

---

## 3. Main Simulation Entities

### Humans

Humans are the susceptible population. Each human moves between points of interest and has a health state.

Health states:

| State | Description |
|---|---|
| `Susceptible` | healthy and vulnerable to infection |
| `Incubating` | infected but not yet symptomatic |
| `Symptomatic` | sick; movement speed is reduced |
| `Recovered` | recovered and immune |
| `Dead` | deceased; removed from the active population, leaving a death marker |

Humans **do not infect each other**. The only infection route is entering a contaminated cloud.

### Mice

Mice are virus carriers. They move through the world, do not get sick, and periodically create contaminated clouds.

Implemented mouse behavior includes:

- random/smooth trajectory movement;
- staying within world bounds;
- a timer for spawning contaminated clouds;
- an alternative mode with a static contamination circle around each mouse.

### Contamination Clouds

Contamination clouds are areas of viral concentration in the environment.

They have:

- infection radius;
- intensity;
- lifetime;
- diffusion, meaning gradual expansion;
- wind drift;
- concentration decay;
- infection tracking for R0 calculation.

### Points of Interest (POI)

Humans do not move chaotically. Instead, they move between points of interest:

- homes (`Home`);
- workplaces (`Work`);
- shops (`Shop`);
- cafes (`Cafe`);
- parks (`Park`).

Each human is assigned a home, while later destinations are selected using weighted probabilities. This creates local concentrations of people and makes environmental transmission easier to observe.

---

## 4. Key Features

### Interactive Simulation

The user can run, pause, and speed up the simulation. Speed presets are available from `10s/s` to `12h/s`.

### Configurable Population

Through the UI, the user can configure:

- world size;
- number of humans;
- number of mice;
- human and mouse movement speed;
- number of points of interest of different types;
- number of humans per home.

### Virus Settings

Available parameters include:

- incubation period;
- disease duration;
- mortality rate;
- immunity duration;
- contaminated cloud spawn interval;
- infection probability inside a cloud.

### Environment and Wind

The simulation accounts for:

- cloud lifetime;
- cloud radius;
- diffusion;
- wind direction and strength;
- random wind variability;
- showing or hiding clouds.

### Alternative Infection Model

There is a **Static circle around mouse** toggle.

- In the normal mode, mice leave temporary clouds that drift, expand, and decay.
- In the simplified mode, each mouse carries a permanent contamination circle around itself.

### Day/Night Cycle

The project includes virtual time and a day/night cycle. This affects human behavior: at night, people return home; during the day, they move between POIs.

### Statistics and Visualization

The following values are displayed in real time:

- number of healthy humans;
- number of humans in incubation;
- number of symptomatic humans;
- number of recovered humans;
- number of deaths;
- SIR history;
- R0 estimate.

The user can also click a human to select them and view detailed information.

### Saving and Loading

Two types of persistence are implemented:

1. **Automatic settings persistence** in `saves/hantasim_settings.ron`.
2. **Full world snapshot** to a JSON file through the `Save` / `Load` buttons.

A full save includes the state of humans, mice, clouds, POIs, statistics, and simulation time.

---

## 5. Controls

Main controls:

- `Space` — pause / resume;
- `1`–`8` — select simulation speed;
- `WASD` or arrow keys — move the camera;
- mouse wheel or `Q` / `E` — zoom;
- click a human — select a human;
- `Save` / `Load` buttons — save and load state.

---

## 6. Technologies

Technology stack:

- Rust;
- Bevy 0.18;

---

## 7. Main Project Focus Points

1. **No person-to-person transmission.** This is the core invariant of the model.
2. **Infection happens only through the environment.** Mice create clouds, and humans become infected through contact with them.
3. **The simulation is interactive.** Most parameters can be changed through the UI.
4. **The world is reproducible.** A random number generator seed is used.
5. **The architecture is modular.** Entities, systems, UI, statistics, and persistence are separated into dedicated modules.
6. **The project is intended for demonstration and learning.** It is a visual model, not a medical forecasting tool.
