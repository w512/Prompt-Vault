# Pomodoro Timer with Analytics

Create a single **index.html** file implementing a Pomodoro timer with customizable intervals and productivity analytics. The goal is a polished focus tool that demonstrates accurate timer state management, browser notifications, data persistence, and chart-based reporting.

### Core Requirements

* **Timer & Phases**:
    * Implement three phases: **Focus** (25 minutes by default), **Short Break** (5 minutes), and **Long Break** (15 minutes).
    * After each completed Focus session, switch to a Short Break; after every fourth completed Focus session, switch to a Long Break.
    * Provide **Start**, **Pause**, **Skip**, and **Reset** controls with clear enabled and disabled states.
    * Add an option to start the next phase automatically or wait for the user to start it manually.
    * Keep time accurately even when the browser tab is inactive by calculating the remaining time from timestamps rather than relying only on interval ticks.
* **Alerts & Notifications**:
    * Play an audio alert when a phase finishes.
    * Support browser desktop notifications after requesting permission through a user action.
    * The timer must remain functional when notifications are unavailable or permission is denied.
    * Update the browser tab title with the remaining time and current phase, for example `14:20 — Focus`.
* **Customization**:
    * Include a settings panel where users can change the Focus, Short Break, and Long Break durations using positive whole-minute values.
    * Allow users to set a daily goal for completed Focus sessions.
    * Apply a distinct visual theme to each phase, such as red for Focus, green for Short Break, and blue for Long Break.
* **Progress & Analytics**:
    * Display the remaining time prominently inside a circular progress indicator that updates throughout the current phase.
    * Track completed Focus sessions and breaks with their type, date, and completion time.
    * Show today's Focus-session progress against the daily goal.
    * Use **Chart.js** to display the number of completed Focus sessions per day for at least the last seven days.
    * Include a readable empty state before any sessions have been completed.
* **Persistence**:
    * Save timer settings, the daily goal, auto-start preference, and session history to `localStorage`.
    * Restore all saved data when the page is reopened.
    * Only naturally completed phases count in analytics; skipped or reset phases must not be recorded as completed sessions.

### Design Requirements

* Use a modern responsive layout with the timer as the primary visual element.
* Style the settings and analytics panels with a subtle glassmorphism effect.
* Add smooth transitions when phase colors and circular progress change.
* Clearly indicate the active phase and whether the timer is running or paused.
* Keep controls and charts usable on both desktop and mobile screens.

### Technical Constraints

* Everything must be contained in a **single HTML file** (HTML, CSS, and JavaScript).
* Use standard **Vanilla JavaScript** for timer logic, state management, rendering, and persistence.
* **Chart.js** may be loaded from a CDN; do not use any other frameworks or external JavaScript libraries.
* Prevent duplicate intervals and clean up active timers whenever a phase is paused, skipped, reset, or completed.
* The file must run correctly in a modern browser when opened directly without a server (an internet connection is required to load Chart.js from the CDN).
* The code should be easy to read and well-commented.
