# File Listing Application

A desktop application for creating lists of files and folders.

This must be a real desktop application: it should run as a native Tauri window on the user's computer and work with the local file system through OS-level capabilities. Do not build a website, landing page, or browser-only SPA without a desktop wrapper.

Use the following stack:

- Tauri 2.0
- Vue.js 3
- TypeScript
- Rust for Tauri backend commands

Do not only describe the solution. Implement a working desktop application in the current repository.

## Application Goal

The desktop application should help users create structured lists of local files: photos, videos, audio files, PDF documents, or any files from a selected folder.

The user selects a folder or adds files through drag and drop. The application scans the selected files and folders, shows the result in a table, allows searching, filtering, editing selected fields, calculating hashes separately, and exporting the result to CSV.

## What To Build

### 1. Create the Project

If the project has not been initialized yet, create a desktop application with Tauri 2.0, Vue 3, and TypeScript.

Configure:

- Vue 3 frontend;
- TypeScript;
- Tauri 2.x;
- Rust commands for file system operations;
- basic project structure;
- README with run instructions.

### 2. Implement File and Folder Selection

Add the following to the interface:

- a button for selecting a folder through a system dialog;
- drag and drop support for files and folders;
- an `Include subfolders` toggle;
- visible state: idle, scanning, completed, error.

Scanning must run through the Tauri backend, not through a frontend mock.

### 3. Implement Scanning

For each discovered entry, collect the following basic metadata during the initial scan:

- file name;
- date modified;
- date created, if available;
- kind / extension;
- size;
- path;
- comments;
- tags;
- title.

Rules:

- do not calculate md5 or sha256 automatically during the initial scan;
- access errors for individual files or folders must not crash the application;
- the UI must not freeze when scanning large folders;
- results must be returned to the frontend as structured data.

### 4. Implement Hash Calculation by Button

Add a separate `Calculate hashes` button.

Behavior:

- hashes are calculated only after an explicit user action;
- md5 and sha256 are calculated only for files;
- folders keep empty hash values;
- if the user selected rows in the table, calculate hashes only for the selected files;
- if nothing is selected, calculate hashes for the current filtered list;
- show status or progress while hashes are being calculated;
- show read errors for individual files in the status area and do not interrupt the whole process.

### 5. Implement Filters

Add filtering by type:

- all files;
- images;
- videos;
- audio;
- PDF;
- custom extension.

For `custom extension`, add an input field. Example values: `.txt`, `.zip`, `.docx`.

Add search by:

- file name;
- path.

### 6. Implement the Preview Table

Show scan results in a table.

The table must support:

- sorting at least by name, size, and modification date;
- row selection for later hash calculation;
- hiding and showing columns;
- displaying the number of found records;
- an empty state when no files are selected;
- an empty state when filters return no results;
- editing user-editable text fields.

Editable fields:

- file name;
- comments;
- tags;
- title.

### 7. Implement Column Selection

The interface must include a panel or dropdown for selecting columns.

Required columns:

- File name
- Date modified
- Date created
- Kind
- Size
- Path
- Comments
- Tags
- Title

The `md5` and `sha256` columns must also be available, but their values are filled only after pressing `Calculate hashes`.

Optional columns can be added as prepared interface fields. Real extraction of these metadata fields is not required if it needs separate platform-specific integration:

- Version
- Pages
- Authors / Artist
- Album
- Track No
- Genre
- Year
- Duration
- Audio BitRate
- Audio Sample Rate
- Audio Channels
- Dimensions
- Pixel Width
- Pixel Height
- Camera Make
- Camera Model Name
- Date Taken
- ISO
- FNumber
- Focal Length
- Latitude
- Longitude
- Maps URL

In the README, explicitly state which metadata fields are actually extracted and which are only prepared interface fields.

### 8. Implement CSV Export

Add export to CSV.

Requirements:

- the user selects the save path through a system dialog;
- only selected or visible columns are exported;
- export respects the current filters;
- export respects user edits in the table;
- export includes md5 and sha256 only for files where the user has already calculated hashes;
- CSV must correctly escape commas, quotes, and line breaks;
- file encoding must be UTF-8.

Export must be implemented through Tauri/Rust or through a correct frontend plus Tauri file save dialog flow. Do not add a fake button that does not actually save a file.

## Interface

Make the first screen the actual working application. Do not create a landing page or marketing screen.

Minimum interface structure:

- top toolbar with folder selection, drag and drop area, subfolders toggle, calculate hashes button, and export button;
- filters panel: file type, custom extension, search;
- preview table;
- column selection panel;
- status area: file count, errors, progress, or current scanning/hash calculation stage.

The design should be calm, utilitarian, and suitable for regular work with many files.

## Technical Constraints

Follow these rules:

- use Tauri 2.x;
- use Vue 3;
- use TypeScript on the frontend;
- use Rust for file system operations, hash calculation by button, and file saving;
- the application must run as a Tauri desktop application, not only as a dev page in the browser;
- folder selection and CSV saving must use system desktop dialogs;
- do not block the UI during scanning;
- handle access errors without crashing the application;
- do not perform unrelated refactoring;
- do not add a server backend unless it is needed for Tauri;
- do not replace the application with a static mockup;
- do not leave critical functionality as pseudocode.

## Nice To Have

If the basic requirements are complete, implement one or more improvements:

- scan progress;
- cancel current scan;
- cancel hash calculation;
- persist user column settings;
- table virtualization for large lists;
- EXIF metadata for images;
- duration and basic parameters for audio/video;
- export to `.xlsx`;
- thumbnails for images.

## Result Verification

After implementation:

1. Install dependencies if required.
2. Run typecheck, lint, or build if such commands exist in the project.
3. Verify that the application starts.
4. Fix any errors found.
5. In the final response, briefly state:
   - which files were changed;
   - what was implemented;
   - which checks were run;
   - what limitations remain.

## Minimum Acceptable Result

The solution is sufficient if the user can:

1. select a folder;
2. scan files with an optional recursive subfolder traversal;
3. see the result in a table;
4. search and filter files;
5. select visible columns;
6. edit selected fields before export;
7. calculate md5 and sha256 by button;
8. export the result to CSV.
