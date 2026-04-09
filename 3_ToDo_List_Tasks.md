**Task 1 — Basic HTML page**
Create an HTML page with a title "Task Manager", a heading, and an unordered list of 5 hardcoded tasks (e.g. "Buy groceries", "Walk the dog", etc.). Style it with basic inline or embedded CSS — background color, font, centered layout.

---

**Task 2 — Add interactivity**
On the same HTML page, add a text input and an "Add Task" button. When the button is clicked, the typed text should be added as a new item to the task list using JavaScript. Clear the input after adding.

---

**Task 3 — Mark tasks as done**
Add the ability to click on any task in the list to toggle it as "completed" — strike through the text and change its color to gray. Clicking it again should toggle it back to active.

---

**Task 4 — Delete button**
Add a "✕" button next to each task in the list. When clicked, the task should be removed from the DOM. Make sure the button also appears for newly added tasks, not just the hardcoded ones.

---

**Task 5 — Task counter**
Add a counter at the top of the page that shows the total number of tasks: `Total: Z`. It should update automatically whenever a task is added or deleted.

---

**Task 6 — Active & Completed split**
Expand the counter to show all three values: `Active: X | Completed: Y | Total: Z`. The Active and Completed numbers should also update when a task is toggled (clicked to mark as done or undone).

---

**Task 7 — Save to localStorage**
Make the task list persistent using `localStorage`. When the page is refreshed, all tasks (including their completed/active state) should be restored. Add a "Clear All" button that wipes both the list and the stored data.
