# claude-watch

A Claude companion app for Apple Watch. Drive Claude from your wrist:

- **Get notified** when an agent needs you (a permission prompt, a question, or a finished task).
- **Listen** to the last state / session summary read aloud.
- **Speak** a directive back to Claude, transcribed from your voice.

Audio capture, playback, and speech-to-text use native Apple Watch APIs. This app
decides *when* and *what* to speak, listen for, and send.

> **Status:** Design phase. This repository currently contains the architecture
> and build plan only — see **[PLAN.md](./PLAN.md)**. No application code yet.

## At a glance

| Capability | How it works |
| --- | --- |
| Notify | A repo-committed `Notification`/`Stop` hook POSTs to a small relay → APNs push to the watch |
| Read state | The relay stores the last assistant message; the watch fetches it and reads it with `AVSpeechSynthesizer` |
| Voice in | The watch transcribes speech on-device and queues a directive on the relay; a `Stop` hook injects it back into the session |

The first milestone targets **Claude Code on the web** as the transport (no
machine to keep running), and the design generalizes to **local Claude Code
hooks** later. See [PLAN.md](./PLAN.md) for the full rationale, data flows, and
roadmap.
