# Contributing to SPECTRA

Contributions to SPECTRA are welcome under the AGPL-3.0 license.

## Repository Architecture

SPECTRA is designed to be lightweight, modular, and privacy-preserving.

- **Primary Application (`index.html`):** Standalone, zero-dependency client application. Contains the complete UI, multi-model cognition engine, AutoTune heuristics, Parseltongue obfuscation, and markdown renderer. Runs in any modern browser without a build step.
- **API Proxy (`api/`):** Optional TypeScript / Express server (`api/server.ts`) exposing OpenAI-compatible endpoints (`/v1/chat/completions`) and multi-model racing for server-to-server or programmatic integration.
- **Hugging Face Space (`HF/`):** Self-contained deployment bundle configured for running SPECTRA on Hugging Face Spaces.
- **Documentation (`docs/`):** Architecture documentation, research specifications (`PAPER.md`), API reference (`API.md`), local model guides (`LOCAL_MODELS.md`), and security policies (`SECURITY.md`).

## Local Development

### 1. Client Application (`index.html`)

No compilation or package installation is required to work on the main client application.

```bash
# Clone the repository
git clone https://github.com/xAbdoAT/G0DM0D3.git
cd G0DM0D3

# Serve with any static HTTP server (or open index.html directly in a browser)
python -m http.server 8080
# or
npx serve .
```

Open `http://localhost:8080` in your browser. All changes to `index.html` are immediately testable upon refreshing the browser.

### 2. API Proxy (`api/`)

If you are developing or testing the optional backend proxy:

```bash
# Install dependencies
npm install

# Start the API proxy with auto-reload
npm run api
```

The API server will listen on `http://localhost:7860`.

## Guidelines

- **Privacy & Security First:** Never introduce external tracking, third-party analytics, or silent telemetry beacons. User API keys and conversation history must remain restricted to local browser storage (`localStorage`) or local memory.
- **Maintain Documentation Integrity:** If you modify API endpoints, state management, or UI capabilities, update the corresponding documentation files in `docs/`.
- **Focused Pull Requests:** Keep pull requests concise and scoped to a single fix or feature. Include clear reproduction steps or test verification in the PR description.
- **No Credentials:** Never commit API keys, personal tokens, or production environment files.

## Reporting Issues

Open a GitHub issue with:
- Clear description of the unexpected behavior
- Steps to reproduce
- Expected outcome versus observed outcome
- Environment details (browser, operating system, and model provider if applicable)

## License

By contributing, you agree that your code will be licensed under the GNU Affero General Public License v3.0 (AGPL-3.0).
