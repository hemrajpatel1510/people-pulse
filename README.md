# PeoplePulse — Standalone Interactive Demo Video Player & Live Simulator

**Event**: Tech Zephyr 4.0 | IIT Bhubaneswar — Agentic AI Hackathon  
**Target Duration**: 300.0 Seconds (5:00 Minutes)  
**Integrity Mode**: Standalone / 100% Zero External Cloud Dependencies  

---

## 1. Overview

The **PeoplePulse Interactive Presentation Player and Simulator** is a high-fidelity, client-side web application that delivers the complete 5-minute hackathon pitch and live demonstration. Rather than using a static, compressed MP4 video, it renders an authentic DOM simulation of PeoplePulse's Admin Dashboard and sliding PulseAgent Copilot drawer.

The player is driven by an authoritative master clock synchronizing studio-quality voiceover narration, word-for-word real-time karaoke subtitles, and animated ODAEA (Observe, Decide, Act, Evaluate, Adapt) event streaming.

---

## 2. The 6 Official Hackathon Stages

The 300-second timeline strictly maps to the 6 official hackathon evaluation stages:

| Stage | Time Window | Duration | Color | Key Focus & Visual Representation |
| :--- | :--- | :--- | :--- | :--- |
| **Stage 1: Goal Context** | `0:00 – 0:45` (0s - 45s) | 45s | Blue (`#3B82F6`) | PeoplePulse Admin Dashboard, real-time KPI metrics, 84.2% participation, burnout crisis (76%). |
| **Stage 2: Decision Framework** | `0:45 – 1:30` (45s - 90s) | 45s | Purple (`#8B5CF6`) | PulseAgent drawer slides open; 6-stage lifecycle breadcrumbs & Gemini 2.0 Flash ReAct loop. |
| **Stage 3: Action Execution** | `1:30 – 2:14` (90s - 134s) | 44s | Slate (`#64748B`) | Live Postgres query via `get_organization_metrics` with server-injected `organization_id`. |
| **Stage 4: Dynamic Evaluation** | `2:14 – 2:40` (134s - 160s) | 26s | Amber (`#F59E0B`) | Live observation (68% org, 42% Support burnout); agent mathematically calculates interventions. |
| **Stage 5: Failure Adaptation** | `2:40 – 3:45` (160s - 225s) | 65s | Orange (`#F97316`) | **Primary Differentiator**: External webhook times out with HTTP 503; agent intercepts error and reroutes to internal emergency queue. |
| **Stage 6: Outcome & Governance** | `3:45 – 5:00` (225s - 300s) | 75s | Emerald (`#10B981`) | Resolution complete, HITL confirmation modal, immutable sanitized audit trail, 23 passing tests (511ms), and n ≥ 3 differential privacy closing. |

---

## 3. How to Run Locally

### Option A: Direct Local Browser Open (Zero Server)
You can directly open `index.html` in Microsoft Edge, Google Chrome, or Firefox:
```bash
# Windows
start demo_video_player/index.html
```
The player automatically detects `file:///` mode and initializes with zero local CORS blocking.

### Option B: Python Lightweight HTTP Server
```bash
python -m http.server 8080 --directory demo_video_player
# Open http://localhost:8080 in your browser
```

### Option C: Node npx serve
```bash
npx serve demo_video_player
```

---

## 4. Key Interactive Capabilities

1. **Dual-Mode Authoritative Clock**: Seamlessly synchronizes audio master time with a high-resolution `requestAnimationFrame` 60fps loop and soft exponential drift compensation.
2. **Interactive Live-Pause Sandbox**: Pausing at any point (via Spacebar or Pause button) unlocks the DOM:
   - Switch drawer tabs: **ReAct Copilot**, **Audit Trail**, and **Tools Registry**.
   - Expand `▸ Inspect Technical Schema & Payload` on any action or adaptation card to examine raw JSON arguments.
   - Interact with the **Human-in-the-Loop** confirmation dialog (`[Approve Action]` / `[Deny Action]`).
   - Resuming cleanly restores playback and subtitle synchronization without state corruption.
3. **Speed Multipliers with Pitch Preservation**: Toggle between `1.0x`, `1.25x`, and `1.5x` playback speeds. The audio preserves natural vocal frequency via `preservesPitch`.
4. **Keyboard Shortcuts**:
   - `Space`: Play / Pause
   - `←` / `→`: Seek backward / forward 5 seconds
   - `Shift` + `←` / `→`: Seek backward / forward 15 seconds
   - `1` – `6`: Direct jump to Stages 1 through 6
   - `M`: Toggle Mute / Unmute
   - `C`: Toggle Closed Captions
   - `S`: Cycle Playback Speed (1x → 1.25x → 1.5x)
   - `R`: Restart presentation from 0:00

---

## 5. Audio Narration & Subtitle Generation Scripts

To re-generate the audio narration assets:

- **Microsoft Neural Speech (Primary MP3)**:
  ```bash
  python demo_video_player/scripts/generate_audio_edgetts.py
  ```
  Generates `assets/audio/narration_full.mp3` (300.0s) and `assets/subtitles/subtitles.json` / `subtitles.vtt`.

- **Windows SAPI Offline Speech (Fallback WAV)**:
  ```powershell
  powershell -ExecutionPolicy Bypass -File demo_video_player/scripts/generate_audio_sapi.ps1
  ```
  Generates `assets/audio/narration_sapi.wav` (300.0s).

---

## 6. Automated Verification Harness

To verify timeline continuity, audio assets, subtitle synchronization, live-pause sandbox, and zero console errors:
```bash
node demo_video_player/scripts/verify_player.mjs
```
The test connects to headless Microsoft Edge using native Node 24 WebSockets (CDP) and emits structured pass/fail diagnostics.
