# Persian Voice Phone Directory (MVP)

A voice-driven Persian phone directory: say a person's name or job title, and it transcribes your speech, looks up the contact, and speaks the phone number back - using open-source, self-hostable models (no third-party speech API).

Built as a proof of concept for private company.

## How it works

1. **Record** — captures audio from the browser mic in Colab (or a local mic via `sounddevice`).
2. **Transcribe** — [faster-whisper](https://github.com/SYSTRAN/faster-whisper) (`large-v3`) converts Persian speech to text.
3. **Match** — the request is normalized and fuzzy-matched against `contacts.csv` (`Name`, `Role`, `Number`) using [RapidFuzz](https://github.com/rapidfuzz/RapidFuzz). If it's ambiguous, the assistant asks a follow-up question instead of guessing.
4. **Speak** — [Piper](https://github.com/rhasspy/piper) (`fa_IR-ganji_adabi-medium`) synthesizes the spoken reply, fully offline.

## Features

- Fully self-hosted ASR + TTS — no paid speech APIs
- Lookup by name **or** job title
- Ambiguity handling via clarifying follow-up questions
- Supports multiple phone types per contact (mobile / office / home)
- Numbers are spoken as Persian digit words
- Auto-selects GPU or CPU
- Optional Gradio web demo for testing without the notebook

## Tech stack

faster-whisper (Whisper large-v3) · RapidFuzz · Piper TTS (fa_IR-ganji_adabi-medium) · pandas · Gradio
