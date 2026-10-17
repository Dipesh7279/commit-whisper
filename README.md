# Commit Whisper

> Make every code change explainable.

Commit Whisper turns a git diff into four useful outputs:

- a conventional commit message;
- a human-readable release note;
- a review-risk signal; and
- a compact change map.

It is designed for developers who want a better commit without sending source code to a hosted service.

## Why this is Open Source AI

AI is the core workflow, not a decorative chatbot. The model receives a diff, identifies intent, writes a conventional commit, summarizes user impact, and highlights what a reviewer should verify.

The app supports local Ollama models, including `qwen2.5-coder:1.5b-base` and [llama3.2](https://ollama.com/library/llama3.2), both open-weight options that run locally through [Ollama](https://ollama.com). A built-in demo mode makes the experience immediately testable without an account, API key, download, or server.

Review the model's own terms before redistributing model weights or deploying it commercially.

## Run it

No build step is required:

1. Clone or download this repository.
2. Open `index.html` in a browser.
3. Paste a git diff or use the included example.
4. Choose **Demo mode** and click **Whisper this diff**.

For local inference:

```bash
ollama list
```

Start Ollama, open the page, choose an installed model such as **Ollama · Qwen 2.5 Coder 1.5B**, and run the analysis. The browser calls `http://localhost:11434`; the diff is not sent to a hosted API. If you have enough disk space, you can also install `llama3.2` with `ollama pull llama3.2`.

If local analysis fails, the app now displays Ollama's actual error response and a suggested recovery step. Confirm the selected model is listed by `ollama list`; if it is missing, install it with `ollama pull qwen2.5-coder:1.5b-base` or `ollama pull llama3.2`, matching the model selected in the app. If Ollama reports a memory or model-runner error, close memory-heavy apps and restart Ollama before trying again.

## Architecture

This is intentionally a small, dependency-free static application:

```text
git diff → browser UI → demo adapter OR Ollama HTTP API → structured JSON → result cards
```

- `index.html` contains the responsive UI, interaction logic, prompt, Ollama adapter, fallback mode, and accessibility behavior.
- Demo mode uses a deterministic example so judges can test the product instantly.
- Ollama mode requests structured JSON with `commit`, `release`, `review`, and `chips` fields.
- No backend, framework, telemetry, API key, or database is required.

## Two-minute demo script

1. Say: “Commit Whisper turns an opaque diff into the context a team actually needs.”
2. Point out the local-first and open-weight AI badges.
3. Keep the sample authentication diff and click **Whisper this diff** in Demo mode.
4. Show the conventional commit, release note, review signal, and security tags.
5. Switch to Ollama mode and explain that the same workflow can run on a local open-weight model.
6. Copy the commit message to finish.

## Known limitations

- The local model must be installed separately with Ollama.
- Browser security settings may block requests if Ollama is not configured to accept local browser origins.
- Demo mode is a presentation fallback, not a model inference result.

## License

The application code is released under the [MIT License](LICENSE).
