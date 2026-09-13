# Persian Voice Phone Directory (MVP)

A Persian voice phone directory. Say a name or job title, hear the number back. Fully self-hosted, open-source ASR/TTS.(no third-party speech API).

Built as a proof of concept for private company.

## How it works

1. **Record** — captures audio from the browser mic in Colab (or a local mic via `sounddevice`).
2. **Transcribe** — [faster-whisper](https://github.com/SYSTRAN/faster-whisper) (`large-v3`) converts Persian speech to text.
3. **Match** — the request is normalized and fuzzy-matched against `contacts.csv` (`Name`, `Role`, `Number`) using [RapidFuzz](https://github.com/rapidfuzz/RapidFuzz). If it's ambiguous, the assistant asks a follow-up question instead of guessing.
4. **Speak** — [Piper](https://github.com/rhasspy/piper) (`fa_IR-ganji_adabi-medium`) synthesizes the spoken reply, fully offline.

## Challenges solved

- **Name vs. role disambiguation** — determines whether a caller meant a person's name or their job title, and combines fuzzy scores accordingly instead of just taking the top match.
- **ambiguity handling** — asks a clarifying follow-up instead of guessing when multiple contacts plausibly match.
- **Fully offline speech loop** — no cloud ASR/TTS calls, making it usable in privacy-sensitive or air-gapped settings.
- **No LLM in the matching loop** — contact resolution is pure heuristic/fuzzy-scoring logic, not a model call, so lookups are fast and deterministic.

## Tech stack

faster-whisper (Whisper large-v3) · RapidFuzz · Piper TTS (fa_IR-ganji_adabi-medium) · pandas · Gradio
