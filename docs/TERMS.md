# SPECTRA — Terms of Service

**Last updated:** 2026-11-07

---

## 1. Acceptance

By using SPECTRA — whether through the standalone web interface, the API proxy server, or a self-hosted instance — you agree to these terms. If you do not agree, do not use the software.

---

## 2. Nature of the Software

SPECTRA is an open-source research and cognition workbench for multi-model evaluation, parameter tuning (AutoTune), input perturbation analysis (Parseltongue), and output transformation (STM). It is provided **as-is** for experimentation, research, and educational use under the AGPL-3.0 license. It is maintained as an open-source community project.

---

## 3. Data Privacy and Collection Architecture

SPECTRA adheres to a **client-first, zero-telemetry** privacy model in the web application.

### Web Application (`index.html`)

- **Zero Telemetry:** The client web application does not run analytics beacons, tracking pixels, or background telemetry. No user queries, prompts, or metadata are collected or transmitted to third-party databases.
- **Local Credential & State Custody:** Your API keys (OpenRouter, Venice, or local model endpoints) and chat histories are stored strictly within your browser's `localStorage` on your own device.
- **Direct Provider Connection:** When an API request is initiated, your browser connects directly and exclusively to the model endpoint you configured. If using local models (Ollama, LM Studio), traffic remains strictly on your loopback interface (`localhost`, `127.0.0.1`, `::1`).

### Optional API Proxy Server (`api/`)

When deploying and using the optional Node/TypeScript API proxy server (`api/server.ts`), the following operational pipelines exist:

| Pipeline | Type | Default State | Description |
|---|---|---|---|
| **Operational Metadata** | System Metrics | Active on API server | Collects in-memory operational performance metrics (latency in ms, winning model, character count, error category). Does not record message text or system prompts. |
| **Research Dataset** | Per-request Opt-in | Disabled (Off) | Only active if a client programmatically sets `"contribute_to_dataset": true` in an API call. Used strictly for open research dataset compilation. |

#### What Operational Metadata Excludes
- Never records raw user prompts or conversational text
- Never records system instructions or reasoning traces
- Never captures user API keys or authentication credentials
- Never stores IP addresses in permanent records

---

## 4. Chat History and Credential Custody

All persistent conversational data within the web application lives strictly in your browser's local storage. SPECTRA maintains no remote user accounts and no server-side synchronization.

**Important Implications:**
- Clearing your browser cache or site data **permanently removes** your conversation history.
- Private/incognito windows discard conversation history as soon as the session window closes.
- Conversation data does not automatically sync between devices or different browsers.
- You can export and back up your chat data at any time via **Settings (⚙️) → Data → Export Data**.

---

## 5. User Responsibilities & Acceptable Use

By using SPECTRA, you agree:
- You are solely responsible for the inputs you provide and the outputs generated through model providers.
- You will comply with all applicable laws and regulations in your jurisdiction.
- You will abide by the acceptable use policies and terms of service of the underlying model providers you choose to access (e.g. [OpenRouter Terms of Service](https://openrouter.ai/terms), [Venice Terms](https://venice.ai/legal/tos)).
- You will not utilize the tool to generate unlawful content.

---

## 6. Enterprise Use & Licensing

- **Self-Hosting:** Self-hosting SPECTRA from source code under the AGPL-3.0 license is free for everyone, including enterprise organizations, provided that any derivative works and modifications are made available under AGPL-3.0.
- **Commercial Licensing:** Organizations with custom compliance, closed-source derivative, or proprietary distribution requirements may contact the maintainers regarding commercial dual-licensing arrangements.
- **Academic & Non-Profit Use:** Academic research, education, non-profit, and independent hobbyist use is entirely free.

---

## 7. Disclaimer of Warranties & Limitation of Liability

SPECTRA IS PROVIDED "AS-IS" WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NONINFRINGEMENT.

In no event shall the authors, maintainers, or contributors be liable for any claim, damages, or other liability arising from the use of, or inability to use, this software, including API consumption costs incurred with third-party providers.

---

## 8. Third-Party Services

SPECTRA allows you to interface with third-party model services. Your relationship with those services is subject to their respective policies:

| Service | Role | Terms |
|---|---|---|
| **OpenRouter** | Cloud AI model aggregator | [openrouter.ai/terms](https://openrouter.ai/terms) |
| **Venice AI** | Privacy-focused inference provider | [venice.ai/legal/tos](https://venice.ai/legal/tos) |
| **Hugging Face** | Host for optional API backend spaces | [huggingface.co/terms-of-service](https://huggingface.co/terms-of-service) |

SPECTRA is an independent open-source project and is not affiliated with, endorsed by, or sponsored by any of these providers.

---

## 9. Open Source Verification

SPECTRA is licensed under the **GNU Affero General Public License v3.0 (AGPL-3.0)**. The complete codebase is open and directly verifiable:
- Standalone Client Application: `index.html`
- Optional API Server: `api/server.ts`
- Operational Metadata Logic: `api/lib/metadata.ts`
- Dataset Opt-in Handler: `api/lib/dataset.ts`
