# LLM Speedometer: Local LLM Performance Benchmarking Tool

**LLM Speedometer** is a lightweight, high-performance desktop application designed for developers, AI enthusiasts, and researchers to benchmark and analyze the speed and efficiency of locally running Large Language Models (LLMs). Built with a modern, resource-efficient stack using **Tauri** and **Vue.js**, the application interfaces directly with any local inference engine that supports the OpenAI-compatible API protocol (such as *Ollama, vLLM, llama.cpp, LM Studio, or SGLang*).

The tool acts as a dedicated testing playground that extracts, calculates, and visualizes real-time performance metrics directly from the API's JSON responses, without needing heavy server-side monitoring infrastructure.

---

## 🚀 Key Features

### 1. Real-Time API Performance Metrics

The application tracks and visualizes critical performance indicators (KPIs) pulled directly from the stream chunks and final JSON response payloads:

* **TTFT (Time to First Token):** Measures the exact latency of the *prefill phase*—how long it takes the local GPU/CPU to process the prompt and start generating text.
* **TPOT (Time Per Output Token):** Tracks the average time taken to generate each subsequent token during the *decoding phase*.
* **Tokens Per Second (TPS / Generation Throughput):** Displays the raw generation speed, calculated dynamically during streaming or extracted from custom engine usage extensions.
* **Token Count Auditing:** Displays precise breakdowns of `prompt_tokens`, `completion_tokens`, and `total_tokens`.

### 2. Stream-Based Analytical Charting

* **Live Speed Graphs:** Real-time visual rendering of token generation speed as the response streams in, highlighting spikes or "stuttering" in performance.
* **Engine Comparison Profiles:** Save benchmarking runs to compare how different backends (e.g., Ollama vs. vLLM) or quantization levels (e.g., Q4_K_M vs. Q8_0) handle identical prompts.

### 3. Engine-Agnostic OpenAI API Integration

* Fully customizable API Endpoint URL and API Key inputs to seamlessly switch between different local servers.
* Automatic parsing of proprietary backend metadata extensions (such as Ollama's `eval_duration` and `prompt_eval_count` properties).

---

## 🛠️ Architecture & Tech Stack

By pairing Tauri with Vue.js, the application guarantees an exceptionally low memory footprint on the host system, ensuring that the benchmarking tool itself does not steal valuable VRAM or CPU cycles from the local LLM being tested.

* **Frontend:** Vue.js (Composition API) + Vite — Powers a highly responsive, reactive, and clean user interface.
* **Desktop Runtime:** Tauri (Rust) — Provides a secure, native desktop window wrapper using the system's webview, resulting in a tiny application bundle size (typically under 10MB) and near-zero idle RAM usage.
* **Data Visualization:** Chart.js / ECharts — Handles high-frequency updates for real-time streaming metrics without UI lag.

---

## 📊 Use Cases

* **Hardware Optimization:** Test how changing GPU layers (`ngl`), context windows, or batch sizes affects your actual generation speed.
* **Quantization Benchmarking:** Visually evaluate the exact speed trade-offs when stepping down a model from 16-bit to 4-bit quantization.
* **Prompt Engineering Impact:** Measure how adding massive system prompts or long chat histories degrades the Time to First Token (TTFT).

---