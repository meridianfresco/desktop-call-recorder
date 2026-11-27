# Release Notes - Desktop Call Recorder

---

## v2.0.29 - 2026-11-27

- Fixed: the new-call dot on the tray icon looked like a blocky square at the bottom right. It is now drawn at 16 times the size and scaled down, so it is a smooth red circle with a thin light ring at 16, 24 and 32 px (`icon-tray-notify.png`, `icon-tray-notify@1.5x.png`, `icon-tray-notify@2x.png`).
- Fixed: after an install or upgrade, the desktop and Start Menu shortcuts and the taskbar button could keep showing the previous version's icon, because Windows keeps icons cached. The installer now tells Windows to refresh its icon cache when it finishes.
- Changed: the installer no longer contains build-machine file paths. The recorder and transcriber programs are compiled with the build folder's path replaced, and the compiled copy of a file-watching module that only the build tools use (with its build logs) is left out of the package. The installer is about 1.6 MB smaller.

---

## v2.0.28 - 2026-11-27

- Changed: the app icon is Google's current Voice logo (the 2026 version: a green-to-blue handset with the sound-wave quarter), replacing the older two-tone green one. The icon set was regenerated from Google's own renditions at each size where Google publishes one (16, 24, 32, 48, 64 and 128 px) and resampled from the 1024 px original for the rest: `icon-1024.png` and `build/icon.png` (now square, 1024 x 1024), `icon-64.png`, and `icon.ico` (16, 24, 32, 40, 48, 64, 128 and 256 px; the installer, shortcuts and window use it). The tray icons have 1.5x and 2x versions (`icon-tray@1.5x.png`, `icon-tray@2x.png` and the matching `icon-tray-notify` files with the new-call dot), so the tray icon is sharp at 125% to 200% display scaling.
- Fixed: selected text in the dark and matrix themes is themed. It was the browser's default white on blue; it is now the accent color with the page color as text, and the matrix text glow is not drawn on it.
- Fixed: the Voice logo at the top left of the dark and matrix themes had a filled box on hover. Voice gives that logo no hover, and the v2.0.26 rule that fills hovered top-bar controls included it. The logo is now left out; the main menu, audio, help, settings, apps and account controls keep their hover and pressed fills.

---

## v2.0.27 - 2026-11-27

- Fixed: calls were logged with "Connecting…" as the caller name. While a call is being set up, Voice shows that text where the caller's name goes, and the call observer accepted it as the name; the main process then only replaced a name that was exactly "Unknown", so the real name never replaced it. Call-setup text ("Connecting…", "Calling…", "Ringing…") and call-control labels ("Hang up call", "Mute call", "Hold call", ...) are no longer taken as a name; the observer reports the caller's name as soon as Voice shows it, even after the call has connected; and a name read from Voice's own name element replaces one picked up by the last-resort text scan. Calls already stored with such a name (nine rows, all calls to the same number) are repaired at startup: they get the name another call to the same number resolved to, or "Unknown" when there is none; the database is backed up at startup before the repair.

---

## v2.0.26 - 2026-11-27

- Fixed: the top bar in the dark and matrix themes, compared against Voice's own look. A hovered or pressed header icon (main menu, audio, help, settings, apps) now gets a visible fill (Voice draws a grey circle; the theme had cleared it), and the "Receiving calls" pill has a fill at rest that differs from its hover and pressed fills (Voice draws it white on the grey bar). Hover on a Settings-page navigation item is lighter than the selected one; the two used the same fill, so hovering looked like selecting.
- Fixed: filled and tonal buttons (the dialog "Add", the in-call Hold, Keypad, Mute and Message buttons) use a fill that keeps their text readable in both themes: in the dark theme they were a strong blue with blue text on top. The in-call Hang up button is red again in both themes; the filled-button rule from v2.0.25 had turned it blue. Select-option lists have their own shade, slightly lighter than the dialog under them.
- Checked and unchanged: the Settings page controls (toggle, radios, outlined buttons, fields) in matrix, and the whole dark theme on screen (main page, row hover and open row, dialogs, message menu, in-call controls). A scan of the Messages, Calls, Voicemail and Settings pages found one border Voice draws transparent that the theme shows: the search pill's, which is deliberate. Not checked: the voicemail player, which needs a voicemail to be opened (that marks it read).

---

## v2.0.25 - 2026-11-27

- Fixed: states of menus, lists, buttons and the in-call controls in the dark and matrix themes, compared against Voice's own look: (1) menu items (the thread "More options" menu) show a fill only while hovered, and keyboard-focused; the first item was highlighted as soon as a menu opened, and every icon and label sat on a black square over the hover fill; (2) the check mark of the selected option in a dropdown (and in checkboxes) was dark blue on dark green and now uses the accent color; (3) dialpad keys have no fill at rest, as in Voice, and get a visible fill on hover and a stronger one while pressed; (4) buttons and "Send new message" get a visible hover and pressed fill (Voice's own is a state layer at 8% and 12%, invisible on black); contact rows keep Voice's no-hover; (5) the in-call Hang up button is Voice's red again, with a light icon, instead of the same dark pill as Keypad and Mute. Checked live in the matrix theme against the unthemed app, including two short test calls to a fake 1-800 number.
- Fixed: dialogs and pop-up menus in the dark and matrix themes, compared against Voice's own look (the People and Add-contact dialogs, the message "Options" menu with Copy text / Delete / Select, the dropdown lists): (1) they are raised surfaces again, filled with the theme's secondary color instead of the page color, so a dialog or menu has an edge instead of being black on black; (2) the filled "Add" button is filled with the theme's primary color, with a lighter fill on hover and while pressed, and a dimmed fill and text while disabled; (3) an empty required field shows Voice's error red (lightened to read on a dark surface) on the outline, label and asterisk; (4) the contact avatar in the People dialog has its blue circle back (the pop-up fill had covered it); (5) the line above the dialog buttons and the hairlines at the sides of the floating-label gap are gone: Voice draws those borders transparent and the theme had recolored them, which made them visible; (6) the labels of buttons in dialogs take the theme's text color from the stylesheet instead of being forced to the accent color, which is unreadable on a filled button in the dark theme.

---

## v2.0.24 - 2026-11-27

- Fixed: hover, selected and pressed states on conversation rows in the dark and matrix themes. Voice fills the circle over an avatar with translucent dark grey while you hover it and with a solid dark color once the row is selected, with a light check mark; the theme cleared both fills, which left a bare check on the avatar (hover) or on the row (selected). The circle now has those fills in theme colors. The pressed layer of a row (dark grey at 8-10%, invisible on black) and the click ripple (also cleared) are now drawn in the theme's colors. Checked live in the matrix theme against Voice's own look: hovering an avatar, selecting a conversation and holding the mouse down on a row.

---

## v2.0.23 - 2026-11-27

- Fixed: v2.0.22 gave every conversation row a fill; rows are plain again. A row now has a fill only while hovered (a medium green, in matrix) or open/selected (a stronger one), as Google does with its grey hover and tinted open row. The open-row color from v2.0.22 never showed because Voice paints that layer behind the list's own background; the fill is now on the row itself. Checked live in the matrix theme against the unthemed app for hovering a conversation, an avatar, a contact, a message bubble, the side navigation and the thread-header buttons.

---

## v2.0.22 - 2026-11-27

- Fixed: conversation rows in the dark and matrix themes. In Google each row is a card with a grey hover layer and a tinted open row; the theme cleared the card fill, gave every row the same near-black highlight (1.08:1 from the background) at all times, and Google's own hover layer is dark grey at 8%, which cannot be seen on black. A row now has the theme's secondary color as its card fill, a lighter mix of the border color while hovered, and the border color while open or selected. Hover on side-navigation items, list items and contacts uses the border color. Colors only; nothing else on the rows changes.

---

## v2.0.21 - 2026-11-27

- Changed: the dark and matrix themes now only recolor Google Voice; Google's layout is left as Google draws it. Checked by comparing every element of the themed app against the unthemed app: no element changes size or position any more. Removed from the themes: the 1px border on the top bar (it pushed the whole page down 1px), the custom 8px scrollbar (the list columns were 7px wider than Google's; the scrollbar now only takes theme colors), the 4px bar on the selected navigation item, the forced `display`, `visibility`, `opacity` and `pointer-events` rules, added shadows, borders, outlines and rounded corners (search bar, availability panel, dialer field, popups, bubbles, dialogs), the backdrop blur, the uppercase and letter spacing on matrix headings, and the global shadow removal in the dark theme. The matrix text glow is kept. Placeholders, the switch handle and the slider track keep their dimmed look through a semi-transparent color instead of `opacity`.
- Fixed: the hover/selection check mark on a conversation's avatar drew a black square over the avatar circle; the icon now has no fill of its own. The title of the availability panel ("Availability") showed as black text with a green glow for the first moments after the panel opened (its text color was Material's black until a timer re-colored it); the panel and dialog containers now set the theme text color directly. The selected navigation item and selected rows, which lost their 4px bar, now use the border color as fill so the selected state stays visible. The remaining `background` shorthands (switch, row highlight, page reveal) are `background-color`, so they no longer reset images.

---

## v2.0.20 - 2026-11-27

- Fixed: text fields in the dark and matrix themes (the add-contact dialog, for example). The text caret was Material's blue (`#0b57d0`), and red while Material flags a required field as invalid; it is now the accent color. A focused outlined field (`mat-focused`) had a 2px outline in the same near-black green as unfocused fields, so focus was thicker but not visible; its outline is now the accent color.

---

## v2.0.19 - 2026-11-27

- Fixed: the audio settings panel (headset button) looked mis-styled in the dark and matrix themes. (1) The square dialog host (`mat-mdc-dialog-container`) took the popup rule's border and shadow, drawing a second, square outline around the rounded panel; the host now has none, so only the rounded surface is outlined. (2) The shadow-piercer script treated each select's trigger as a surface and gave it a bright border and a glow on top of Voice's own outlined box, which showed as lines above and below the selected device name inside a second box; the trigger is no longer treated as a surface. (3) The select text was forced to bold weight; it keeps Voice's own weight.

---

## v2.0.18 - 2026-11-27

- Fixed: the dialer's "Enter a name or number" field ran under the call button in the dark and matrix themes. The theme's generic input rule forced `padding: 8px` and a 1px border on Voice's borderless input, growing it from its 232px column to 249px. The forced padding is removed from that rule, so inputs keep Voice's own sizing. Voice draws this field as a filled row (`.input-row`) around a borderless input; the input keeps its native borderless look and the row now has the theme fill and a ring (an inset shadow, which takes no space) that turns to the accent color while the field has focus.
- Fixed: placeholder text was nearly invisible (`#444746` in the dialer, `#757575` in the search bar on a black background). Placeholders now use the theme foreground at 60% opacity.

---

## v2.0.17 - 2026-11-27

- Fixed: the Voice search bar looked like two boxes with a seam after the search icon in the dark and matrix themes. The form had a rounded 1px border and the input inside it a second 1px border with a different radius, and the placeholder was Google's stock grey. The form is now one pill (the `--theme-selection` fill that `mappings.scss` intended, a 1px border, and an accent border while it has focus); the input and the buttons inside are transparent and borderless; the placeholder uses the theme foreground.

---

## v2.0.16 - 2026-11-27

- Fixed: headings such as "AVAILABILITY", "SUGGESTIONS" and the Settings section titles looked blurred in the matrix theme. They had a constant full-strength 8px green text-shadow, which on 11px uppercase text smears the letters. The glow is now 3px at 45% opacity: the neon halo stays, the letters are crisp.

---

## v2.0.15 - 2026-11-27

- Fixed: the availability menu under the "Receiving calls" chip had no background of its own (only its title and button were filled), so the page showed through it and its border was barely visible. It now has the theme background, a 1px accent border, rounded corners and a shadow.
- Fixed: keyboard focus rings in the dark and matrix themes. The theme reset set `outline-color` to `--theme-selection`, almost the background color, so Voice's own inset rings on thread, call and voicemail rows were invisible; every focus ring now uses the accent color. Contact rows and the contact list used the browser's default ring, drawn outside the box and cut off by the scroll container on the left; they get an inset ring.
- Checked: no hard-cut text (text clipped without an ellipsis) on Calls, Messages, Voicemail, Archive, Spam or Settings.

---

## v2.0.14 - 2026-11-27

- Fixed: the "Receiving calls" availability chip looked clipped in the dark and matrix themes: the hover and focus background showed only at the two ends of the pill because every child of the top bar had a solid black fill. The top bar is a Google-bar `header`, which the popup rule (`[ng-non-bindable][class*="gb_"]`) also matched; its children now keep the color rules but have a transparent fill, so the chip, the headset, help and settings buttons show a complete hover and focus background. The same rule had drawn a bordered box around the apps grid and avatar; that border is gone. Keyboard focus on top-bar buttons shows a theme-colored ring, drawn inside the button because the wrapper around the availability chip clips at its edge, instead of the browser's white one. The white focus ring around the availability panel (the dialog container takes focus when it opens) is gone.
- Fixed: opening the availability menu (or a dialog Voice marks as having no overlay) dimmed and blurred the whole page. Only Voice's dark backdrops (`cdk-overlay-dark-backdrop`, `dark-overlay-backdrop`) get the dim and blur now; the invisible click-away backdrops stay invisible.

---

## v2.0.13 - 2026-11-27

- Fixed: the loading spinner still showed Voice's blue for the first few hundred milliseconds of every page load (File > Reload, startup), because the full theme is injected at dom-ready, after the spinner is already drawn. The preload now asks the main process, synchronously at document start, for a one-rule stylesheet that colors the page-load spinner and the circular spinners with the active theme's accent (`$active` of matrix.scss or dark.scss; empty for the default theme) and applies it with `webFrame.insertCSS` before any page script runs. Measured on a reload: both spinners are theme-colored from the first frame (about 40 ms).

---

## v2.0.12 - 2026-11-27

- Fixed: loading spinners were dark blue in the dark and matrix themes. The circular spinner (availability chip, thread-list loading, other in-page loading states) is drawn with a fixed `#0b57d0` and the page-load spinner with `#005cbb`; both arcs now use the theme's active color, and linear progress bars use the theme colors too. The page-load spinner still shows Voice's blue for the first fraction of a second of a page load, before the theme is injected.

---

## v2.0.11 - 2026-11-27

- Fixed: Material controls in the dark and matrix themes used Voice's fixed blue / grey / white instead of the theme palette. Settings slide toggles (track, handle, icon) and radio buttons (ring and selected dot), the hover and press state layer on dialpad keys, buttons and radios, and the voicemail seek slider (track, filled part, thumb) now use the theme colors. An off toggle has a dimmed handle so it reads differently from an on toggle. The selected radio dot was previously invisible.

---

## v2.0.10 - 2026-11-27

- Fixed: the search suggestions dropdown under the Voice search bar was unreadable in the dark and matrix themes: transparent background (the page showed through) and black text on black. It is a child of `<body>` with role `listbox` and a `gb_*` class, not an Angular overlay, so the overlay rules never applied to it. It now has the theme background, border and foreground color.

---

## v2.0.9 - 2026-11-27

- Fixed: the keyboard-focus ring around the voicemail seek slider thumb (and other Material controls) was Voice's blue (`#00639b`) in the dark and matrix themes. The ring (`.mat-focus-indicator::before`) now uses the theme's active color.

---

## v2.0.8 - 2026-11-27

- Fixed: calls placed or received while Focus Mode was on were not detected, so they were not logged or recorded. Focus Mode hid the dialer sidebar with `display: none`, and the call observer finds the hang-up control through `offsetParent`, which is `null` inside a hidden subtree. Focus Mode now moves the sidebar off-screen while no call is active (it keeps its layout box, so detection and the dial handlers work) and shows it again while a call is dialing, ringing or connected, so the call controls are reachable. Three calls with the old rule left no call-log row; a call with the new rule was logged normally.
- Fixed: Focus Mode is applied every time the Voice page loads. It used to be applied only at the moment the switch was toggled, so a restart or reload showed the sidebar again while the setting still read "on".
- Fixed: contact avatars in the dark and matrix themes keep Voice's own colors. The circle color (set inline by Voice), the white letter or person glyph and contact photos are no longer repainted by the theme reset, the icon rule, the matrix text glow or the shadow-piercer script. The thread-header avatar is no longer a solid theme-green disc (the selection-header indicator rule matched its inline background).
- Fixed: tooltips in the dark and matrix themes have a solid background. The shadow-piercer script set `background: transparent !important` on every element inside overlay panes, which beat the stylesheet's tooltip background; tooltip, menu, select, autocomplete and dialog surfaces now get the theme background instead.
- Fixed: the Settings, Cloud Backup, R2 Bucket Browser, About, Transcription, Summary and Logs windows open with the native background of the user's GUI surface color instead of white, so there is no white flash before the page applies its theme. The Focus Mode description in Settings mentions that the sidebar reappears during calls.

---

## v2.0.7 - 2026-11-27

- Fixed: call talk time was blank for many calls. The Voice call timer reads `00:00` at the moment of connect, and the old code only accepted a reading above zero and never looked again. Talk time now starts the clock at CONNECTED, refines it with the timer readings Voice shows during the call (sent every ~2 seconds), and at hang-up uses the timer when it agrees with the wall clock and the wall clock when it does not. `metadata.talkTimeSource` (`gv-timer`, `wall-clock`, `none`) and `metadata.talkTimerStrategy` record which was used. The logic lives in `src/utils/talkTime.js`.
- Added: the call-timer reader tries three strategies in order (`gv-test-id`, screen-reader text, text scan), logs which one matched, and logs a `[TalkTime]` warning when it had to fall back to the wall clock, so a future change to the Voice page shows up in the log instead of as blank talk times.
- Added: `tests/talkTime.test.mjs` (23 tests including a check that the timer parser copied into `preload.cjs` is identical to the module) and `npm test`.
- Changed: call audio is written through an asynchronous, ordered writer (`src/utils/pcmWriter.js`) instead of a synchronous append on the main process for every audio chunk (about 23 per second per stream). A 45-minute call previously spent roughly 12 seconds of main-process time in blocking disk writes, with single writes up to 70 ms.
- Fixed: the last audio chunk of each stream could be dropped at hang-up because the chunk listeners were removed before the renderer's final flush. They now stay attached until the renderer confirms it stopped and the writers have drained, and the WAV headers are written from the bytes actually on disk.
- Changed: the ffmpeg mix, the transcription worker and the summary model (`llama-cli`) run at below-normal priority so a long call's post-processing yields to the app windows and the Voice page.
- Changed: the silence scan used before transcription scales its time limit with the recording length (minimum 30 s) instead of a fixed 20 s.
- Added: guarded `click` route in the dev inspector (hang-up / end-call / new-call controls only, `confirm=1` required).
- Fixed: the dark / matrix theme injection (stylesheet, body attributes, the 400 ms icon-recolour interval) now runs only on `voice.google.com` and no longer touches Google sign-in or other pages. The check is an exact hostname match.
- Fixed: the unread-badge count skipped the closed drawer copy of the side nav only by `offsetParent`, so it could count each badge twice. It now ignores hidden nodes, sends the count only when it changed, and disconnects the previous observer when re-arming after back/forward navigation.
- Fixed: the dialer-ready probes (tel: auto-dial, splash and curtain handshakes) also look for the input inside `gv-make-call-panel`, so they no longer depend on the English placeholder text or generated ids.
- Fixed: dark / matrix select, autocomplete and other overlay panels were not clickable because the whole overlay pane was set to `pointer-events: none`; only the transparent wrapper is now click-through.
- Fixed: the dark sent-message bubble colours were overridden by the base theme (equal specificity, later rule wins); the dark rule now has higher specificity. The Clear-search icon and other hidden icons are no longer forced visible by the icon rule in the dark / matrix themes. The dark piercer panels use the theme background instead of pure black.
- Changed: `injectTheme` reuses the last SASS compile when the source is unchanged, creates its reveal style tag once per document, removes superseded stylesheets when two injections overlap, and catches rejected `executeJavaScript` / `insertCSS` calls. The Focus Mode toggle no longer inserts its rule twice, clears its key on removal and catches errors.
- Fixed: the REC indicator is re-inserted if Voice re-renders the call status, never adds a second style tag, and its label uses a darker red (5.09:1 on the Voice surface). The full audit record is in `docs/DIALER_CSS_AUDIT.md`.
- Changed: the call-quality survey blocker runs once per mutation batch and removes only the survey's own backdrop. `CallObserver` re-creates its in-call status observer when the status element changes and disconnects it when no call is active.

---

## v2.0.6 - 2026-11-26

- Fixed: the app's browser-identity adjustments never ran on Google's sign-in pages (`accounts.google.com`). Those pages' Content Security Policy blocked the inline `<script>` the app injected, so the sign-in page saw a `Firefox/149` user agent alongside Chromium-only values (`navigator.userAgentData`, `window.chrome`). The adjustments are now applied by a session frame preload (`webFrame.executeJavaScript`) in every frame and login popup, with no script tag injected. On the sign-in page the browser properties now read consistently with the Firefox user agent (`userAgentData`, `window.chrome`, `vendor`, `productSub`, `appVersion`, `oscpu`, `deviceMemory`, `performance.memory`, `buildID`), and the CSP error no longer appears.
- Changed: re-enabled GPU hardware acceleration (removed `app.disableHardwareAcceleration()`) and removed legacy `--no-sandbox`, `--disable-site-isolation-trials`, `--disable-infobars`, and `IsolateOrigins,site-per-process,SitePerProcess` flags so Google Sign-In sees a real hardware GPU instead of `Microsoft Basic Render Driver` and failing WebGPU adapter probes. Kept `PublicKeyCredential` and `navigator.credentials` present to match Firefox while `passkey-block-preload.cjs` and the WebAuthn/FedCM flags suppress the Windows Security passkey prompt.
- Fixed: `PushMonitor` now detaches its DevTools-protocol debugger when the window navigates to a Google sign-in or sign-out page and re-arms when Voice loads again, with a single listener per arming. Previously the debugger stayed attached while sign-in pages loaded.
- Changed: the passkey-block preload no longer depends on Node's `fs` / `path` modules; its source is inlined in `passkey-block-preload.cjs`.
- Changed: the Notification hijack is applied through `webFrame` and skipped on `accounts.google.com`. `exporterAPI`, the call-notice / WebRTC instrumentation and call-quality survey suppression are limited to `voice.google.com`. All `Sec-CH-*` request headers and the `Critical-CH` response header are stripped, and login popups are created with the WebAuthn Blink features disabled.
- Changed: the main window's pre-paint background and the cover shown while Voice loads (File → Reload, the tray Reload item, blank-screen recovery) now follow the theme: Voice's light surface by default, black for the dark and matrix themes. A loading Voice page no longer appears over black on the default theme. The return to Voice after signing in loads Voice directly instead of going through the cover step. The cover now hides every element on the page, with transitions and animations switched off, so parts of Voice that set their own visibility (such as the "Call as" number block) no longer stay on screen while it reloads. The theme-switch curtain is now a dark gray instead of pure black.
- Known issue: Google can still show "Couldn't sign you in — This browser or app may not be secure" on some sign-in attempts, sometimes several times in a row before the password page appears. Trying again eventually works. This is not resolved in this release.

---

## v2.0.5 - 2026-11-26

- Added automatic database backups: each time the app starts, your call history (`call-log.db`) and text log (`text-log.db`) are copied to a `backups` folder next to them. The newest 5 distinct copies of each are kept, so a bad write or corrupted file can be rolled back by copying a backup over the original.
- Fixed: the early passkey/WebAuthn block was never registering (wrong option name in the Electron call, so it silently fell back to a later injection). It now registers for every frame of the Google session and runs in the page's own JavaScript context before Google's scripts. The previous later injection remains as a fallback.
- Fixed: after signing out of Google Voice and signing back in, you could end up on your Google Account page instead of Voice. The app now recognizes that landing page (and only that one) and returns to Voice automatically.
- Fixed: the splash screen could stay up until you clicked it. The app now always hands off to the main window within a few seconds, even if Windows doesn't report the window as ready.

---

## v2.0.4 - 2026-04-23

- Added AMD GPU support: AMD Radeon RX 5000+ and Intel Arc GPUs now use the Vulkan inference build for hardware-accelerated summaries. GPU detection runs automatically at setup - NVIDIA gets CUDA, AMD/Arc gets Vulkan, everything else gets the optimized CPU build.
- Vulkan detection uses Windows WMI (no third-party tools required) with explicit exclusions for Intel integrated graphics (Iris Xe, UHD) which offer no meaningful benefit for this workload.
- Updated system requirements in README to reflect supported hardware matrix across all GPU and CPU paths.

---

## v2.0.3 - 2026-04-23

- Fixed: inference watchdog was too short for CPU-only machines (Intel/AMD, no NVIDIA GPU). GPU builds keep the 5-minute limit; CPU builds now get 15 minutes, which is enough headroom for calls up to ~40 minutes on a mid-range laptop CPU.

---

## v2.0.2 - 2026-04-23

- AI engine now auto-detects GPU at install time: NVIDIA CUDA GPUs get the CUDA 12 build (5-10x faster inference), all other hardware gets the optimized CPU (AVX2) build. No configuration needed.
- GPU layer offload (-ngl 99) is applied automatically when the CUDA build is active; CPU builds run without it.
- Added KV cache quantization (q4_0) - reduces KV cache memory by 4x on both GPU and CPU builds with no meaningful quality impact. A 60-minute call now uses ~1.7 GB for the cache instead of ~6.75 GB.

---

## v2.0.1 - 2026-04-23

- Fixed: AI summary silently fails on longer calls (10+ minutes) due to a hardcoded 4096-token context window that the transcript overflows. Context window now scales dynamically with prompt length so any call length is handled correctly.
- Fixed: When AI summary generation fails, no error was shown to the user - the button would just stop spinning with no explanation. Failures now surface as a toast message in the transcription view.

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
Windows 10 x64 or later. Requires a Google Voice account and approximately 4-5 GB of disk space for AI models and engine.

---

*Not affiliated with or endorsed by Google LLC.*
