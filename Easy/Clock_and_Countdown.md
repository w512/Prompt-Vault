# Clock, Stopwatch & Countdown

Create a single **index.html** file that combines a live digital clock, a stopwatch, and a countdown timer. The goal is a clean, easy-to-use time utility that demonstrates interval management, date formatting, UI state, and browser storage.

### Core Requirements

* **Digital Clock**:
    * Display the current time in `HH:MM:SS` format and update it every second using JavaScript's `setInterval`.
    * Show the current date below the clock in a readable long format, such as `Tuesday, May 5, 2026`.
    * Add a button that toggles between **24-hour** and **12-hour** time with an AM/PM indicator.
* **Stopwatch**:
    * Display elapsed time as `MM:SS:MS`.
    * Provide **Start**, **Stop**, **Reset**, and **Lap** buttons.
    * Start must continue from the current elapsed time, Stop must pause without resetting, and Reset must return the stopwatch to zero and clear its current timing state.
    * Prevent multiple timers from being started when Start is clicked repeatedly.
* **Lap Times**:
    * The Lap button records the current stopwatch value without stopping it.
    * Show recorded laps in a numbered list, for example `Lap 1: 00:12:45`.
    * Keep the lap list after a page refresh using `localStorage`.
* **Countdown Timer**:
    * Include a number input for a duration in seconds and a **Start Countdown** button.
    * Accept only positive whole numbers and show the remaining time as it counts down to zero.
    * Disable the start button while a countdown is running so overlapping countdowns cannot be created.
    * When the countdown reaches zero, display a visible **"Time is up!"** message and temporarily change the page background to red for a few seconds. A browser alert may also be used, but it must not replace the visible message.
* **Preferences**:
    * Save the selected 12-hour or 24-hour clock format to `localStorage`.
    * Restore the saved clock format and stopwatch lap list when the page is reopened.

### Design Requirements

* Use a dark theme with a large, highly readable clock display.
* Clearly separate the clock, stopwatch, and countdown into labeled sections.
* Give controls visible hover, focus, and disabled states.
* Keep the layout usable on both desktop and mobile screens.

### Technical Constraints

* Everything must be contained in a **single HTML file** (HTML, CSS, and JavaScript).
* Use standard **Vanilla JavaScript** with no external libraries or frameworks.
* Manage intervals carefully: clear timers when they stop or finish and never leave duplicate intervals running.
* The file must work by opening it directly in a modern browser without a server.
* The code should be easy to read and well-commented.
