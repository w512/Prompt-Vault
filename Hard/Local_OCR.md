# Local LLM-powered OCR
A local, privacy-focused desktop application for converting PDFs and images to structured Markdown using large language models.

---

Write a complete, ready-to-run Python desktop application for local text recognition (OCR) from images and PDF files using Vision-Language models via a local Ollama server.

### Technical Stack:
- GUI: `customtkinter` (modern dark theme by default).
- PDF handling: `pymupdf` (the `fitz` library for fast rendering of pages into images).
- AI Interaction: Official `ollama` Python client, connected to a user-configurable Ollama server URL.
- Concurrency: standard `threading` and `queue` modules.

### Architecture & Code Requirements:
1. Thread Safety: PDF conversion, Ollama model-list retrieval, and Ollama query processing must run in background threads to keep the application GUI responsive. Workers must put plain events into a thread-safe queue and must never access Tk directly. The main thread must poll that queue using `.after()` and perform all GUI updates. Only one background operation may run at a time.
2. File Processing:
   - If an image file (png, jpg, jpeg, webp) is selected, pass it directly to Ollama.
   - If a PDF is selected, the application should create a temporary folder using `tempfile`, render each page to a PNG at the user-selected resolution (DPI), send them sequentially to the model, and then clean up by deleting the temporary folder and files in a `finally` block.
3. Result Saving: Save the final text as a Markdown file (.md) in the same directory as the input document, appended with the `_extracted.md` suffix.

### UI Requirements (The layout must be responsive):
- A 'Select File' button accompanied by a text label showing the selected file's name.
- Settings section:
  - Editable Ollama server URL field, defaulting to `http://localhost:11434`. It must also accept remote/local-network URLs.
  - A "Refresh Models" button that obtains available models from the configured server using `ollama.Client(host=url).list()` without freezing the GUI.
  - An editable Model Selection ComboBox populated from the server response. The user must also be able to type an arbitrary model tag manually. `gemma4:12b` and `qwen3.6:27b` are examples/suggestions only and must not be hard-coded as the only allowed values or assumed to exist. Models must never be pulled automatically.
  - Failure to fetch models must display a clear error but must not prevent manual model entry.
  - PDF DPI dropdown with options: "100", "150", "200", "300" (default is 150).
- A large, accented 'Start OCR' button. During processing, it must be disabled (`state='disabled'`) and show 'Processing, please wait...', returning to its active state upon completion or error.
- A progress bar (`CTkProgressBar`): should run in indeterminate animation mode (`.start()`) during processing and reset to 0 upon completion.
- A large log text box (`CTkTextbox`) using a monospace font. It should output progress steps in real time: '[Start]', '[1/3] Converting...', '[2/3] Sending page X to Ollama...', '[Success] File saved'. The text box must automatically autoscroll to the bottom as new lines are appended.
- Native `messagebox` popups upon completion (indicating success or displaying an error).

### System Prompt for the VLM inside the code:
When querying Ollama, create `ollama.Client(host=user_url)` and use its `chat` method with the selected or manually entered model. Send each page independently and pass the following system prompt verbatim:
`
Convert this image into Markdown text format. Your task is to perform high-accuracy Optical Character Recognition (OCR). Preserve the document's structure as accurately as possible: headers, lists, and tables. Do not add any greetings, explanations, or introductory/concluding remarks. Output only the raw recognized text.
`

