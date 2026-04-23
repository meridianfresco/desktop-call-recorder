# Release Notes - Desktop Call Recorder

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
