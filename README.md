# Desktop Call Recorder — Google Voice AI

Add AI-powered call recording, transcription, and summarization to Google Voice — running entirely on your machine, with no subscriptions, no cloud AI, and no data leaving your device.

Built for solopreneurs, independent operators, and small-business professionals who already use Google Voice and want the call intelligence that dedicated business phone platforms charge $15–30/user/month to provide.

---

## What Google Voice Is Missing — And What This Fixes

Google Voice is a capable, free calling platform. But it has no native call recording on consumer plans, no AI transcription, no call summaries, and no desktop app. If you've looked at switching to a dedicated business phone service just to get those features, this application gives you the same capabilities without leaving Google Voice or paying a monthly per-seat fee.

| Capability | Google Voice (native) | Desktop Call Recorder |
|---|---|---|
| AI call transcription | ✗ | ✓ On-device, automatic |
| AI call summaries | ✗ | ✓ Structured, after every call |
| Automatic call recording | ✗ (paid plans only) | ✓ Both sides, MP3 |
| Desktop app | ✗ | ✓ Windows native |
| Speaker-separated transcript | ✗ | ✓ Your side / caller's side |
| Local storage, no cloud required | — | ✓ SQLite, fully offline |

---

## Features

- **Google Voice AI Transcription** — every call is automatically transcribed on-device using NVIDIA's Parakeet TDT V3 model via Sherpa-ONNX, split by speaker lane so you can read a conversation rather than listen to a recording
- **AI Call Summaries** — after transcription, Microsoft's Phi-3.5 Mini Instruct generates a structured summary covering stakeholders, key insights, needs, objections, and next steps
- **Automatic Call Recording** — captures both sides of every Google Voice call using a custom Rust audio engine (WASAPI), encoded to MP3 via FFmpeg
- **Call History** — paginated log with filtering, sorting, inline audio playback, and a built-in file browser
- **Cloud Backup (Optional)** — sync call records, transcripts, summaries, and audio to any Cloudflare R2-compatible bucket
- **Desktop App** — native Windows application wrapping Google Voice with full theme support, system tray integration, and startup launch

All AI processing runs locally. No audio, transcript, or summary is ever sent to an external server.

---

## System Requirements

**Operating System**
- Windows 10 x64 or later (Windows 11 recommended)

**CPU**
- x64 processor with AVX2 support — Intel Core 4th gen (Haswell, 2014) or newer, AMD Ryzen (Zen, 2017) or newer
- Older CPUs without AVX2 are not supported

**RAM**
- 12 GB minimum — 16 GB or more recommended
- 8 GB machines can run the app but may struggle with calls longer than ~10 minutes

**GPU — Optional, but significantly faster AI summaries**
- The app auto-detects your hardware and downloads the right engine at setup — no manual configuration

| GPU | Backend | Summary speed |
|---|---|---|
| NVIDIA GTX 10 series or newer | CUDA 12 | Fastest (~30 sec) |
| AMD Radeon RX 5000 series or newer | Vulkan | Fast (~1–2 min) |
| Intel Arc A/B series | Vulkan | Fast (~1–2 min) |
| Intel Iris Xe / UHD / integrated | CPU | Standard |
| No GPU | CPU | Standard (~5–10 min) |

> NVIDIA users need driver version 528 or newer (released 2023). Most systems already meet this.

**Disk**
- 4–5 GB free space for the AI model and inference engine (downloaded automatically on first launch)

**Other**
- A Google Voice account (free personal or Google Workspace)

---

## Installation

1. Download the latest `.zip` from [Releases](https://github.com/meridianfresco/desktop-call-recorder/releases), extract it, and run the `Setup .exe` inside
2. Windows may show a SmartScreen prompt since the app is unsigned — click **More info → Run anyway**
3. Launch the app and sign in to your Google Voice account
4. On first launch, the app downloads the AI models (~3 GB) automatically

---

## Privacy

- All transcription and summarization runs on your local hardware — no audio or text is sent anywhere
- Call recordings are stored in your local AppData directory
- No telemetry, no analytics, no account required beyond Google Voice itself
- Cloud sync is entirely opt-in and requires your own storage credentials

---

## License

Released under a **non-commercial license**. Free to use, copy, modify, and distribute for personal and professional use — may not be sold or redistributed for direct commercial gain.

See [LICENSE](LICENSE) for full terms and third-party component attributions.

*Not affiliated with, endorsed by, or sponsored by Google LLC. Google Voice is a service of Google LLC.*

---

## Credits

**Product direction, QA, and release management** — [Meridian Fresco](https://github.com/meridianfresco)

**Coding assistance** — Claude Code (Anthropic) and Google Gemini

**Foundational architecture** — Based on the original [Google Voice Desktop App](https://github.com/jerrod-lankford/google-voice-desktop-app) by Jerrod Lankford

**Core technologies:**

| Component | License | Author |
|---|---|---|
| [Electron](https://github.com/electron/electron) | MIT | OpenJS Foundation |
| [llama.cpp](https://github.com/ggerganov/llama.cpp) | MIT | Georgi Gerganov |
| [Phi-3.5 Mini Instruct](https://huggingface.co/microsoft/Phi-3.5-mini-instruct) | MIT | Microsoft |
| [Parakeet TDT 0.6B V3](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3) | Apache 2.0 | NVIDIA |
| [Sherpa-ONNX](https://github.com/k2-fsa/sherpa-onnx) | Apache 2.0 | k2-fsa |
| [FFmpeg](https://ffmpeg.org) | GPL v2.1+ | FFmpeg team |
| [sql.js](https://github.com/sql-js/sql.js) | MIT | sql.js contributors |
| [Material Web (@material/web)](https://github.com/material-components/material-web) | Apache 2.0 | Google |

---

© 2026 Desktop Call Recorder — Meridian Fresco
