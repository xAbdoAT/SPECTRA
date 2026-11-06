# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in SPECTRA, please report it responsibly.

**Please do NOT disclose security vulnerabilities in public issue trackers.**

### What to Include

- Detailed description of the vulnerability and its potential impact
- Clear, reproducible steps or a proof of concept
- Suggested remediation or patch (if available)
- Affected component (`index.html`, `api/`, or `HF/`)

### Response Timeline

- **Initial Acknowledgement:** Within 48 hours
- **Assessment & Triage:** Within 7 business days
- **Remediation & Patch Release:** Within 30 days for confirmed critical vulnerabilities

## Scope

### In Scope
- The primary standalone web application (`index.html`), including:
  - Content Security Policy (CSP) enforcement
  - Markdown sanitizer and XSS prevention
  - Safe credential management in `localStorage`
  - Local transport boundaries (`localhost`, `127.0.0.1`, `[::1]`)
- The optional API proxy server (`api/`), including:
  - Authentication and token handling
  - Tier-based rate limiting
  - CORS header restrictions and request sanitization
- Hugging Face Space configuration (`HF/`)

### Out of Scope
- Upstream third-party model providers (OpenRouter, Venice, Hugging Face, Ollama, LM Studio)
- Denial of service attacks against community-hosted demonstration instances
- Attacks requiring physical access to an unlocked client device or browser profile
- Social engineering attacks

## Supported Versions

| Version | Status | Notes |
|---------|--------|-------|
| 1.0.x (Current) | Supported | Active development on `main` branch |
| Legacy (Godmode pre-fork) | End of Life | Not supported |

## Security Architecture & Design Principles

- **Zero-Telemetry by Design:** SPECTRA does not run silent analytics beacons, tracking pixels, or background data collection. Provider credentials and conversation histories never leave your device unless explicitly dispatched to the model provider you specify.
- **Strict Content Security Policy:** `index.html` enforces a strict CSP limiting connections strictly to authorized providers (`openrouter.ai`, `api.venice.ai`, loopback local models) and verified runtime assets.
- **Constant-Time Verification:** The API server enforces constant-time string comparisons for Bearer tokens to mitigate timing attacks.
- **Loopback Enforcement:** Local model requests are confined to loopback addresses (`localhost`, `127.0.0.1`, `[::1]`) to prevent arbitrary internal network probing.
