# 3D Arcade Racing — AI Coding Agent Challenge

## Your role

You are an autonomous software developer working inside an existing **Vite + TypeScript + Three.js** project.

Your task is to turn the starter project into a **complete, playable, visually polished 3D arcade racing game** that runs in a desktop web browser.

**Implement the game directly in this repository.** Do not merely describe an approach or provide code snippets. Inspect the existing project, make the necessary changes, run the project, verify your implementation, and fix problems you find.

Do not ask the user for clarification. Make sensible implementation and design decisions independently.

## The game

Create a single-player, third-person **3D arcade racing game** featuring a controllable car, a closed race track, obstacles, checkpoints, a lap timer, and a clear race-completion state.

The game should feel like a small but finished arcade game rather than a static Three.js demo. Prioritize a reliable gameplay loop, responsive controls, and a coherent visual presentation.

## Required features

### 1. Playable 3D world

- Build one **continuous, closed-loop race track** with a clearly visible driving surface, turns, start/finish line, and recognizable surroundings.
- Make the track large enough for meaningful driving and multiple turns. A tiny circular arena does not satisfy the intended gameplay.
- Create a clearly recognizable **3D car** using geometry and materials. The car must visibly face its direction of travel.
- Add environmental detail to make the level look intentional and complete (for example: terrain, barriers, signs, scenery, lighting, decorative objects, or a sky/background).
- Provide a clear sense of depth through camera placement, lighting, materials, and spatial composition.
- Create **at least three obstacles or hazards** that affect driving when the car encounters them.
- Keep the gameplay area navigable. Track boundaries, barriers, or meaningful off-track penalties must prevent the player from trivially bypassing the racing course.

### 2. Driving and camera

- **W / Up Arrow:** accelerate.
- **S / Down Arrow:** brake and, when nearly stopped, reverse.
- **A / Left Arrow:** steer left.
- **D / Right Arrow:** steer right.
- **R:** restart the race.
- The car must accelerate, decelerate, turn, and move in response to controls with an **arcade-style driving feel**. Steering must affect the car's heading and movement, not just its appearance.
- Include basic handling behavior such as acceleration, drag/friction, speed limiting, and speed-dependent steering. It does **not** need to be a realistic vehicle simulator.
- Handle collisions with track boundaries and obstacles. The car must not simply pass through solid objects without consequence.
- Use a **third-person chase camera** that follows the car and keeps the course ahead reasonably visible. Smooth camera movement is encouraged.
- Use delta time or an equivalent approach so movement and gameplay are not unintentionally dependent on frame rate.

### 3. Race rules and progression

- The race consists of **three laps** around the closed track.
- Provide a visible **start/finish line** and **at least four checkpoints distributed around the course**, including or in addition to the start/finish line.
- Count a lap only after the player passes the checkpoints in the correct order and crosses the finish line in the intended direction. Driving back and forth across the finish line must **not** award extra laps.
- Show real-time lap progress and an elapsed race timer.
- When the player completes lap 3, stop race progression and display a clear **Race Complete** state, including the final elapsed time.
- Restarting the race must reset the car, timer, checkpoints, lap counter, and completion state consistently.
- The game should be completable through normal driving without requiring console commands or manual code edits.

### 4. Interface and feedback

Add an in-game HUD showing:

- Game title.
- Current lap, displayed as `Lap 1 / 3`, etc.
- Elapsed race time.
- Current speed (an approximate arcade-style value is acceptable; keep the unit consistent).
- Concise driving instructions.
- A visible **Restart** button in addition to the `R` key.

The interface must:

- Be readable over the 3D scene.
- Provide clear feedback for meaningful events, such as collisions, checkpoint progress, and race completion.
- Remain usable at a typical desktop viewport (for example, 1280 × 720).
- Avoid broken or overlapping HUD elements at a narrow viewport (for example, 390 × 844). Touch driving controls are **not** required.

### 5. Visual presentation

Make your own creative decisions about the game's aesthetic. Possible styles include low-poly, futuristic neon, cartoon, desert rally, sci-fi, or another coherent art direction.

The following are **not prescribed**: track layout, car design, colors, environment, lighting style, and decorative effects. Choose these yourself.

The final result should have a recognizable visual identity, not merely default Three.js primitives on an empty background. However, **working gameplay takes priority over decorative complexity**.

## Technical constraints

- Use the existing **Three.js + TypeScript + Vite** setup. Do not replace Three.js with Babylon.js, Unity, Unreal, or another rendering engine.
- Work from the current starter repository and keep the application runnable using its existing scripts.
- Generate all game visuals **procedurally in code** using geometry, materials, lighting, and other capabilities available in the project.
- **Do not download, import, or hotlink external 3D models, textures, images, audio files, fonts, or other assets.** Do not use CDNs or remote runtime services.
- Avoid adding runtime dependencies. If you believe an additional dependency is indispensable, explain why in the final report; favor implementing the feature with existing tools.
- Keep game logic reasonably organized and maintainable. You are free to choose the file structure.
- Handle window resizing without breaking the renderer or camera.
- Avoid obvious memory leaks, unnecessary object allocations on every frame, and runaway rendering or physics loops.
- The application must not produce uncaught JavaScript errors during normal gameplay.
- `npm run build` must complete successfully.
- No backend, login, database, multiplayer support, or external APIs are required.

## Autonomous workflow

1. Inspect the starter project and understand its available scripts and dependencies.
2. Plan a practical implementation that covers **all required gameplay features**.
3. Implement the game directly in the repository.
4. Run the appropriate build and available tests. If browser testing is available, actually interact with the game, not just inspect source code.
5. Fix issues you discover within the available execution time.
6. Finish with a short factual report containing:
   - What was implemented.
   - Commands/tests you actually ran and their outcomes.
   - Any known missing requirements, bugs, or limitations.

**Do not claim that features work unless you have verified them.** Do not stop after the first implementation if there is still time to test and improve it.

## Definition of done

A successful result is one in which a user can open the game in a browser, drive a recognizable 3D car around a closed course, encounter meaningful obstacles, pass checkpoints in order, complete three valid laps, see the final time, and restart the entire race — all without changing code or using developer tools.

The implementation should also build successfully, have readable HUD elements, and present a deliberate, visually cohesive arcade-game aesthetic.

## Important

This is a **single autonomous attempt**. You will receive no follow-up prompts, design corrections, or human debugging assistance. Use your own judgment and deliver the best complete, verifiable game you can.
