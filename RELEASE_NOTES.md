# Release Notes - Desktop Call Recorder

---

## v2.0.4 — 2026-04-23

- Added AMD GPU support: AMD Radeon RX 5000+ and Intel Arc GPUs now use the Vulkan inference build for hardware-accelerated summaries. GPU detection runs automatically at setup — NVIDIA gets CUDA, AMD/Arc gets Vulkan, everything else gets the optimized CPU build.
- Vulkan detection uses Windows WMI (no third-party tools required) with explicit exclusions for Intel integrated graphics (Iris Xe, UHD) which offer no meaningful benefit for this workload.
- Updated system requirements in README to reflect supported hardware matrix across all GPU and CPU paths.

---

## v2.0.3 — 2026-04-23

- Fixed: inference watchdog was too short for CPU-only machines (Intel/AMD, no NVIDIA GPU). GPU builds keep the 5-minute limit; CPU builds now get 15 minutes, which is enough headroom for calls up to ~40 minutes on a mid-range laptop CPU.

---

## v2.0.2 — 2026-04-23

- AI engine now auto-detects GPU at install time: NVIDIA CUDA GPUs get the CUDA 12 build (5–10x faster inference), all other hardware gets the optimized CPU (AVX2) build. No configuration needed.
- GPU layer offload (`-ngl 99`) is applied automatically when the CUDA build is active; CPU builds run without it.
- Added KV cache quantization (`q4_0`) — reduces KV cache memory by 4x on both GPU and CPU builds with no meaningful quality impact. A 60-minute call now uses ~1.7 GB for the cache instead of ~6.75 GB.

---

## v2.0.1 — 2026-04-23

- Fixed: AI summary silently fails on longer calls (10+ minutes) due to a hardcoded 4096-token context window that the transcript overflows. Context window now scales dynamically with prompt length so any call length is handled correctly.
- Fixed: When AI summary generation fails, no error was shown to the user — the button would just stop spinning with no explanation. Failures now surface as a toast message in the transcription view.

---

## v2.0.0 - 2026-04-19

### Initial Public Release

---

**Call Recording**
Records both sides of Google Voice calls using a custom Rust audio engine (WASAPI). Captures microphone and speaker as separate channels, encoded to MP3 via FFmpeg. Includes an optional recording announcement that plays a legal notice to both parties at the start of each call.

**AI Transcription**
Transcribes recordings on-device using NVIDIA's Parakeet TDT 0.6B V3 model via Sherpa-ONNX. Displays results in a split-lane dialogue view (your side / caller's side) with timestamps. Optional word-level refinement pass for improved accuracy on difficult audio. Runs fully locally - no audio leaves your machine.

**AI Summarization**
Generates a structured call summary after transcription using Microsoft's Phi-3.5 Mini Instruct via llama.cpp. Summary covers stakeholders, key insights, primary needs, objections, and next steps. Runs fully locally.

**AI Model Setup**
First-time setup downloads and installs AI models automatically with a progress UI showing per-asset status, download speed, and ETA. Individual assets can be retried on failure.

**Call History**
Paginated call log with filtering by direction (inbound/outbound) and phone number, sortable by name, size, or date. Displays caller name, number, duration, talk time, and status. Supports copy to clipboard, individual record deletion, and full purge.

**Audio Playback**
Built-in MP3 player docked to the call log. Includes seek bar, play/pause, rewind/forward 5 seconds, and volume control. Reveal recording in Explorer without leaving the app.

**Text Message Archival**
Archive Google Voice text conversations by contact. Threads are fingerprinted for change detection and can be synced to cloud storage alongside call records.

**Cloud Backup**
Optional sync to any Cloudflare R2-compatible storage bucket. Backs up call metadata, transcripts, summaries, and audio recordings. Configurable per-call or automatic after each session. Storage usage displayed with warnings at 70% and 90% of the free-tier limit.

**R2 Bucket Browser**
Full in-app file browser for your R2 bucket. Navigate folders, search recursively, sort by name/size/date, multi-select, bulk delete, and preview JSON, MP3, image, and video files inline. Generate presigned download URLs with selectable expiry (1 hour, 1 day, 7 days).

**Interface & Themes**
Material Design 3 UI with 7 accent colors and 7 surface variants including a full OLED black theme. Per-window zoom, focus mode to hide the dialer sidebar, and dark mode for the Google Voice web dialer.

**System Integration**
Launch on Windows startup, start minimized to system tray, and close to tray. Toast notifications with optional sound. Custom ringtones for incoming, outgoing, busy, and call-ended tones.

**Settings**
Granular controls for transcription, summarization, recording announcement, cloud sync, capture engine (WASAPI or Electron), and notification behavior. All preferences saved locally.

**Platform**
Windows 11 x64 only. Requires a Google Voice account and approximately 2-4 GB of disk space for AI models.

---

*Not affiliated with or endorsed by Google LLC.*
