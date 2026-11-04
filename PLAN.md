# kaiwa-coach — Project Plan

## Goal
A Japanese speaking-practice web app, built for Vincent's Japanese lessons.
Flow: speak into the mic → Whisper transcribes → the app shows what it heard →
an LLM kindly corrects the Japanese and explains why (nicely!).

## Architecture
- Frontend: a single page (HTML/JS) served by the backend. Mic via MediaRecorder.
- Backend: Python FastAPI, runs on the MacBook Air at http://localhost:8000
  - POST /transcribe — audio → faster-whisper (small, multilingual), local, free
  - POST /correct — text → LLM with a "kind teacher" prompt
  - GET /health
- LLM provider is a switch in `.env`: claude / gemini / ollama. No keys in the repo, ever.

## How we work
- One GitHub issue per task below. One branch per issue (`issue-N-short-name`).
- Every change goes through a pull request: review → green checks → merge.
- `main` is protected: PR required, no force pushes, no deletions.
- Tests: pytest. Every backend PR includes or updates tests.

## Task breakdown
1. Scaffolding — layout, README, .gitignore, requirements, PLAN.md (this file)
2. Mic recording UI — record/stop/playback, Japanese labels
3. Backend skeleton — FastAPI app, /health, static file serving
4. /transcribe — faster-whisper integration, audio format handling
5. /correct — LLM client abstraction (claude/gemini/ollama via env)
6. Kind-correction prompt — beginner-friendly Japanese explanations
7. Frontend wiring — record → transcribe → correct → display
8. Pytest suite — endpoint tests (synthetic audio), prompt unit tests
9. Docs + demo guide — Japanese README, lesson demo script

## Running it (MacBook Air)
1. `pip install -r requirements.txt`
2. First run downloads the Whisper model automatically (~1 GB, one time)
3. `uvicorn backend.main:app`
4. Open http://localhost:8000

## Open decisions
- Correction provider for v1: Gemini free tier (no credit card) vs Claude API (~1¢/correction) vs local Ollama
