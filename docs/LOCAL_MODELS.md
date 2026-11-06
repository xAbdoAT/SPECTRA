# Running SPECTRA with Local Models

SPECTRA can interface directly with any local inference server that provides OpenAI-compatible endpoints (`/v1/models` and `/v1/chat/completions`). To protect private internal networks, local requests are strictly restricted to loopback addresses (`localhost`, `127.0.0.1`, and `::1`).

---

## 1. Quick Start with Ollama

1. Install Ollama and pull your desired models:

   ```bash
   ollama pull qwen2.5:7b
   ollama pull llama3.1:8b
   ```

2. Start the Ollama server:

   ```bash
   ollama serve
   ```

3. In SPECTRA, click **Settings (⚙️) → API Keys → Local Models**.
4. Set the **Base URL** to `http://localhost:11434/v1`.
5. Click **Test & Discover Models**. SPECTRA will query `/v1/models` and populate available options.
6. Toggle **Local-only mode** if you wish to restrict all operations to local inference and prevent any outbound cloud calls to OpenRouter or Venice.

> **Note on CORS:** If you access SPECTRA from a hosted URL (e.g. GitHub Pages or a remote static host), your browser will require Ollama to allow Cross-Origin Resource Sharing (CORS). On Linux/macOS, launch Ollama with:
> ```bash
> OLLAMA_ORIGINS="*" ollama serve
> ```
> On Windows PowerShell:
> ```powershell
> $env:OLLAMA_ORIGINS="*" ; ollama serve
> ```
> If you prefer not to configure CORS on Ollama, serve SPECTRA locally as described below.

---

## 2. Quick Start with LM Studio

1. Open LM Studio and load your selected model into memory.
2. Navigate to the **Local Server** (Developer) tab and start the server on port `1234`.
3. In LM Studio's server settings, verify that **CORS** is enabled.
4. In SPECTRA Settings, enter `http://localhost:1234/v1` as the Base URL and click **Test & Discover Models**.

---

## 3. Quick Start with vLLM / llama.cpp / LocalAI

Any server exposing an OpenAI-compliant `/v1` endpoint is supported:

- **vLLM:** Start with `python -m vllm.entrypoints.openai.api_server --model <model_path> --port 8000`
- **llama.cpp:** Start `llama-server -m <path-to-gguf> --port 8080`
- Set the base URL in SPECTRA to the appropriate port (e.g., `http://localhost:8000/v1`).

---

## 4. Serving SPECTRA Locally

To run SPECTRA completely offline with maximum privacy:

```bash
# From the repository root:
python -m http.server 8080
```

Open `http://localhost:8080` in your web browser. In this setup:
- All assets are loaded from your own filesystem.
- No network requests are made to third-party CDNs.
- Local model endpoints communicate directly across your loopback interface.
- Conversation histories and API settings remain stored exclusively in your browser's local storage (`localStorage`).

---

## 5. Multi-Model Local Racing

SPECTRA supports racing multiple local models simultaneously:

1. In the **Local Model IDs** field in Settings, enter multiple model names separated by commas (for example: `qwen2.5:7b, llama3.1:8b, mistral:7b`).
2. The first listed model acts as the primary evaluator for classification, verification checks, and refinement.
3. When you submit a prompt, SPECTRA streams inference across all specified local models concurrently and presents their responses side-by-side or allows you to select the preferred generation.

---

## Troubleshooting

- **Failed to fetch / Connection refused:** Ensure your local server is actively running and listening on the expected port. Confirm CORS permissions are allowed on the local server.
- **No models found:** Verify that `GET <base-url>/models` returns an OpenAI-standard `{ "data": [{ "id": "..." }] }` payload.
- **High latency:** Racing multiple large models simultaneously requires sufficient GPU VRAM and CPU threads. If latency is high, configure a single lightweight model (e.g. 7B or 8B quantized) or lower **Max Tokens** in Settings.
