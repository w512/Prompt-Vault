# Feeder - Technical Specification

## Project: RSS Aggregator App (Full-stack Nim)

### 1. General Project Description

The goal of the project is to create a lightweight web service for aggregating RSS feeds. The service should poll a specified list of RSS sources in the background, save new articles to a database, and provide the user with a minimalist web interface for reading headlines and navigating to the original sources.

**Key Feature:** The entire project (parser, backend, and frontend) must be implemented exclusively in the **Nim** programming language.

---

### 2. Architecture and Technology Stack

The project is divided into three main components:

1. **Crawler/Parser (Background Worker):** A service for periodically downloading and parsing XML/RSS.
2. **Backend API & Web Server:** A service for serving HTML pages and interacting with the database.
3. **Frontend:** A web interface (2 pages) generated on the server or client side using Nim.

**Recommended Stack:**

* **Programming Language:** Nim (version 2.0+)
* **Web Framework:** `Jester`, `Mummy`, or `HappyX` (at the developer's choice, priority is simplicity and performance).
* **HTML Templater / Frontend:** The interface is implemented strictly according to the Server-Side Rendering (SSR) model using the built-in Nim macro `htmlgen`. Client-side SPA frameworks are not used. Interaction with the server (adding/removing feeds) must be performed via standard HTML forms (POST requests) followed by a server redirect. For styling, use `Pico.css` (or a similar classless framework) via CDN to ensure responsiveness without writing a large amount of custom CSS.
* **Database:** SQLite (via the built-in `db_sqlite` module), as the project does not expect massive loads at the start and requires ease of deployment.
* **RSS/XML Parsing:** `std/xmltree`, `std/parsexml`, or the `parsexml` library.

---

### 3. Database Schema (SQLite)

At least two tables need to be designed:

#### Table `feeds` (RSS Sources)

* `id`: INTEGER PRIMARY KEY AUTOINCREMENT
* `title`: TEXT (Feed title, filled in automatically during the first parse)
* `url`: TEXT UNIQUE NOT NULL (Link to the RSS feed)
* `error_count`: INTEGER DEFAULT 0 (To handle dead links)
* `is_active`: BOOLEAN DEFAULT 1 (To handle active/inactive state)
* `created_at`: TIMESTAMP DEFAULT CURRENT_TIMESTAMP

**Database Requirements:**
* **WAL Mode:** When initializing the connection to SQLite, it is mandatory to execute `PRAGMA journal_mode=WAL;`. This is critical to prevent `database is locked` errors during simultaneous read operations by the web server and write operations by the background crawler.
* **Timezones:** All timestamps (`TIMESTAMP`) must be saved strictly in UTC.

#### Table `articles` (Articles)

* `id`: INTEGER PRIMARY KEY AUTOINCREMENT
* `feed_id`: INTEGER (Foreign key to `feeds.id`)
* `title`: TEXT NOT NULL (Article title)
* `link`: TEXT UNIQUE NOT NULL (Direct link to the original article)
* `description`: TEXT (Brief description/preview, if present in the RSS)
* `published_at`: TIMESTAMP (Publication date from RSS)
* `fetched_at`: TIMESTAMP DEFAULT CURRENT_TIMESTAMP (Date saved in the DB)

---

### 4. Functional Requirements

#### 4.1. Background Module (Crawler)

* **Frequency:** Run parsing every $N$ minutes (configured via a configuration file, default is 15 minutes). Use Nim's asynchronous features (`asyncdispatch`, `httpclient`).
* **Workflow:**
  1. Retrieve a list of all URLs from the `feeds` table where `is_active = true`.
  2. Asynchronously perform an HTTP GET request to each URL.
  3. Parse the XML structure (support for RSS 2.0 and Atom).
  4. For each item (`item` / `entry`), check if the `link` exists in the `articles` table (duplicate protection).
  5. If the article is not in the database, write it.
  6. **Timeouts:** Crawler HTTP GET requests must have a strict timeout (e.g., 10 seconds).
  7. **Handling Unreachable Feeds:** If a parsing error occurs or the URL is unreachable, increment `error_count`. If there are more than 5 consecutive errors, set `is_active = false` and stop polling this feed (until it is reset via the interface).
  8. **Data Retention:** After each update cycle, the worker should delete old articles (e.g., older than 30 days from `fetched_at`) to control the database file size.

#### 4.2. Web Interface (Frontend and Backend)

The application consists of exactly two pages (endpoints):

##### Page 1: Article List (Homepage `/`)

* **Interface Elements:**
  * Logo / Service Name.
  * "Manage Sources" button/link (navigates to Page 2).
  * Article feed: chronological list (newest first).
  * Display for each article: Title, RSS source name, Publication date, Brief description (1-2 sentences).
* **Behavior:** Clicking an article title opens the original link in a **new tab** (`target="_blank"`).
* **Pagination:** Output 50 articles per page (with "Next" / "Previous" buttons or infinite scroll).

##### Page 2: Manage Sources (`/feeds`)

* **Interface Elements:**
  * Form to add a new RSS channel: text input field for URL and an "Add" button.
  * List of current subscriptions (URL and Name).
  * Next to each source in the list: a "Delete" button (cascadingly deletes the source and all its articles from the DB).
  * "Back to Articles" button.
* **Validation:** When adding, verify that the string is a valid URL. Ideally, perform a quick check on-the-fly (to verify if the RSS is reachable).
* **Security (XSS Protection):** All string data retrieved from the RSS (titles, descriptions) must undergo mandatory HTML escaping before insertion into the HTML template via `htmlgen`.

---

### 5. Non-Functional Requirements

* **Configuration:** Application settings (server port, DB file path, crawler update interval) must be specified via a simple `.env` file or `config.ini`.
* **Logging:** Use the standard `std/logging` module. It is mandatory to log parsing errors (e.g., if an RSS feed is unavailable or returns invalid XML) so that the background process does not crash.
* **Build System:** The project must be built with a single command using `nimble build` (configure `package.nimble` accordingly).
* **Deployment:** The build output should be a single binary file (including compiled HTML templates if using SSR) + the database file. Provide a Dockerfile for containerization (using Alpine or Debian as the base image).

---

### 6. Acceptance Criteria

1. The background parser runs in a separate thread/task and does not block the processing of HTTP requests by the web server.
2. When a new valid RSS URL is added on the `/feeds` page, its articles appear on the main page within the next update cycle (or immediately upon addition).
3. Duplicate articles are not created in the database during repeated parsing runs.
4. The interface renders correctly on both desktop monitors and mobile phone screens.
5. There are no memory leaks during long-term operation of the service (verified using Nim's `arc` / `orc` memory management).
6. Basic unit tests are written (using the `std/unittest` module), covering XML parsing logic (extracting fields for RSS 2.0 and Atom), parsing different date formats, and the article deduplication algorithm.
