# Markdown Editor - Tauri 2 Desktop App

Create a cross-platform desktop application using **Tauri 2** — a modern, distraction-free Markdown editor with a side-by-side live preview and native system integration.

## Core Features

### Editor & Preview
- **Split-screen layout**: A side-by-side view with a text editor on the left and a rendered preview on the right.
- **Synchronized scrolling**: Scrolling the editor should automatically scroll the preview to the corresponding position.
- **Live Rendering**: The preview should update in real-time as the user types (use `marked.js` for parsing).

### Layout Modes
- **Split View**: Default side-by-side mode.
- **Preview Only**: A toggle to completely hide the editor panel for a clean reading experience.
- **Focus Mode**: A toggle to hide the preview for maximum writing focus.

### Native File System Integration
- **Open File**: Use Tauri's dialog API to open `.md` files from the local disk.
- **Save / Save As**: Implement native "Save" and "Save As" functionality using Tauri's `@tauri-apps/plugin-fs` and `@tauri-apps/plugin-dialog`.
- **Title Bar Integration**: Display the current filename in the window title bar, with an asterisk (*) indicating unsaved changes.

### Toolbar
- A minimal toolbar at the top with buttons for formatting: `B` (Bold), `I` (Italic), `H` (Heading), `List`, `Link`, `Code`.
- Keyboard shortcuts: `Cmd/Ctrl + S` (Save), `Cmd/Ctrl + O` (Open), `Cmd/Ctrl + N` (New).

### Design Requirements
- **Premium Desktop Look**: Use a native-feeling design with glassmorphism or a clean sidebar.
- **Color Themes**: Support Light and Dark modes, preferably syncing with the OS theme by default.
- **Customizable Typography**: Allow users to choose between a few curated fonts for the editor and preview.

## Technical Constraints
- **Framework**: Tauri 2 (Latest stable).
- **Frontend**: Vite with **Vue.js 3** (Composition API). In component files, the 'Template' block should come first, followed by 'Script' and 'Styles'.
- **State Management**: Pinia.
- **Styling**: Vanilla CSS.
- **Libraries**:
    - `marked.js` for Markdown parsing.
    - `prism.js` for code syntax highlighting.
    - Tauri Plugins: `@tauri-apps/plugin-fs`, `@tauri-apps/plugin-dialog`, `@tauri-apps/plugin-shell`.
- **Packaging**: Ensure the app can be built for macOS, Windows, and Linux.

## Project Structure
- Standard Tauri 2 project structure.
- Frontend logic should handle the editor state and communication with the Rust backend (if needed for advanced features) via Tauri's IPC.
