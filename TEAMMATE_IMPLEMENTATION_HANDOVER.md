# Cyber SOS: Developer & Teammate Implementation Handover
**Batch 10 | Societal Project 1BSOP308 | Department of CSE, BMSIT&M**  
**Document Target:** Teammate / Development Lead (Handover Specification)

---

## 📌 Quick Summary for the Teammate

Hey! You have received this repository along with:
1. `Cyber_Safety_Societal_Project_Concepts.pdf` (The original VTU concepts pitch).
2. `Societal Project_synopsis BATCH-10(1).docx` (Our officially submitted synopsis).
3. `Cyber_SOS_Updated_Project_Plan_Batch10.pdf` (The freshly generated, updated 5-page master plan PDF).
4. `cyber_sos_interactive_prototype.html` (A working single-file HTML preview of the UI/charts).

This document contains **everything you need to implement and ship the project on Vercel without guessing anything.**

---

## 🎯 What The Project Is About (The Updated Vision)

We are **NOT** making a boring Google Form or standard multiple-choice quiz. If we just make a quiz, the college evaluators will say *"Where is the software engineering?"*

Instead, we are building a **Trojan-Style Cyber Incident Simulator & Silent Behavioral Observer**:
1. **The Cover / Bait:** We send a link to college WhatsApp groups: *"BMSIT Societal Project Survey: Student Digital Habits"*.
2. **The Hijack:** The student enters their Name/USN and clicks *"Begin Survey"*. Instantly, the screen glitches and launches a photorealistic **Virtual Desktop OS** (or mobile OS).
3. **The Silent Observation:** Real-time crisis alerts fire (Device login from Frankfurt, WhatsApp panic about leaked marks, and a ₹0 AutoPay mandate). The system **silently records** what the student clicks and how fast they react without telling them it's a test!
4. **The Intervention (< 90% Score):** If they make panic mistakes or trigger traps, the OS enters lockdown and streams an educational video/masterclass.
5. **The Objective Post-Mortem & Calibration:** Instead of repeating the same test (which causes memorization), we quiz them objectively on what they got **wrong** AND what they got **right** (with a 1–5 star confidence slider) to separate lucky guesses from genuine competence.

---

## 🎨 Visual & Immersion Standards (Look & Feel)

Our visual benchmarks are 3 top-tier Vercel sites:
* **The Mentalist (`the-mentalist-2026-round-1.vercel.app`):** Dark noir vignette, monospace `'Courier New'` labels, CRT scanline overlay, confidential stamps, ambient tension drone audio.
* **Access Denied (`accessdenied-round2-lovely.vercel.app`):** Hyper-realistic institutional software look (authentic BMSIT logo, verified badges, dispatch logs).
* **Kaustubh Dua (`kaustubhdua.vercel.app`):** Tactile HUD ergonomics, Web Audio sound effects (critical alert chimes, keyboard clicks), achievement toast popups, zero-bloat performance.

---

## 🛠️ Recommended Tech Stack & File Structure

```
cyber-sos/
├── package.json
├── vite.config.js
├── tailwind.config.js
├── vercel.json
├── index.html
└── src/
    ├── main.jsx
    ├── App.jsx
    ├── audio/
    │   └── soundEngine.js          # Web Audio API (procedural sounds, zero asset loading)
    ├── components/
    │   ├── Facade/
    │   │   └── SurveyBait.jsx      # Legitimate-looking BMSIT Student Survey
    │   ├── VirtualMachine/
    │   │   ├── DesktopOS.jsx       # Virtual OS desktop, taskbar, dock, clock
    │   │   ├── WindowFrame.jsx     # Draggable / closable OS window container
    │   │   ├── NotificationCenter.jsx # System toast popups
    │   │   └── Apps/
    │   │       ├── SecurityApp.jsx # Active sessions list & "Terminate Remote Session" button
    │   │       ├── ChatApp.jsx     # Simulated WhatsApp Web conversation
    │   │       └── BankingApp.jsx  # UPI / Mandate dispute center
    │   ├── Telemetry/
    │   │   └── TelemetryTracker.js # Silent logger (timestamps, clicks, panic index)
    │   ├── Intervention/
    │   │   └── VideoPlayer.jsx     # Educational video container
    │   ├── PostMortem/
    │   │   └── ObjectiveReview.jsx # Post-test with confidence calibration sliders
    │   └── Analytics/
    │       └── ResearchDashboard.jsx # Comparative charts + one-click CSV export
    └── data/
        ├── scenariosData.js
        └── postMortemQuestions.js
```

---

## 🔊 1. Procedural Web Audio Engine (`soundEngine.js`)

Do **not** use heavy `.mp3` files that fail to load or get blocked by CORS. Use the browser's native **Web Audio API**:

```javascript
// src/audio/soundEngine.js
class SoundEngine {
  constructor() {
    this.ctx = null;
    this.droneOsc = null;
    this.droneGain = null;
  }

  init() {
    if (!this.ctx) {
      this.ctx = new (window.AudioContext || window.webkitAudioContext)();
    }
    if (this.ctx.state === 'suspended') {
      this.ctx.resume();
    }
  }

  // High-urgency alert chime (Windows/macOS style)
  playAlert() {
    this.init();
    const osc = this.ctx.createOscillator();
    const gain = this.ctx.createGain();
    osc.type = 'sine';
    osc.frequency.setValueAtTime(880, this.ctx.currentTime); // A5
    osc.frequency.exponentialRampToValueAtTime(440, this.ctx.currentTime + 0.35); // Drop to A4
    gain.gain.setValueAtTime(0.2, this.ctx.currentTime);
    gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + 0.35);
    osc.connect(gain);
    gain.connect(this.ctx.destination);
    osc.start();
    osc.stop(this.ctx.currentTime + 0.35);
  }

  // Subtle typewriter / keypress click
  playClick() {
    this.init();
    const osc = this.ctx.createOscillator();
    const gain = this.ctx.createGain();
    osc.type = 'triangle';
    osc.frequency.setValueAtTime(120, this.ctx.currentTime);
    gain.gain.setValueAtTime(0.08, this.ctx.currentTime);
    gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + 0.05);
    osc.connect(gain);
    gain.connect(this.ctx.destination);
    osc.start();
    osc.stop(this.ctx.currentTime + 0.05);
  }

  // Low ambient tension drone (60Hz) during crisis
  startTensionDrone() {
    this.init();
    if (this.droneOsc) return;
    this.droneOsc = this.ctx.createOscillator();
    this.droneGain = this.ctx.createGain();
    this.droneOsc.type = 'sawtooth';
    this.droneOsc.frequency.setValueAtTime(58, this.ctx.currentTime);
    this.droneGain.gain.setValueAtTime(0.015, this.ctx.currentTime);
    this.droneOsc.connect(this.droneGain);
    this.droneGain.connect(this.ctx.destination);
    this.droneOsc.start();
  }

  stopTensionDrone() {
    if (this.droneOsc) {
      this.droneGain.gain.exponentialRampToValueAtTime(0.0001, this.ctx.currentTime + 0.5);
      setTimeout(() => {
        if (this.droneOsc) {
          this.droneOsc.stop();
          this.droneOsc.disconnect();
          this.droneOsc = null;
        }
      }, 500);
    }
  }
}

export const sounds = new SoundEngine();
```

---

## 🎬 2. The 3 Crisis Scenarios (Timeline & Trigger Logic)

### Trigger Timeline
* **$T = 0s$**: Student clicks *"Begin Survey"* on `SurveyBait.jsx`. Audio initializes. Screen undergoes a 0.5s CRT glitch into `DesktopOS.jsx`.
* **$T = 4s$**: **Crisis 1 Fires** (Frankfurt Device Login Alert).
* **$T = 14s$**: **Crisis 2 Fires** (WhatsApp Web Peer Panic Message).
* **$T = 26s$**: **Crisis 3 Fires** (UPI Mandate Prompt).

### Scenario Details
1. **Scenario 1: Frankfurt Device Login**
   * *Notification Toast:* `"Security Alert: Windows 11 device logged into your Google Account from Frankfurt, Germany (IP: 185.220.101.5). [Verify Identity]"`
   * *The Trap:* Clicking `[Verify Identity]` opens an in-browser modal asking for student OTP/password.
   * *The Safe Action:* Opening the OS taskbar `Security Center` app $\rightarrow$ clicking `[Terminate Remote Session]`.
   * *Scoring:* Trap clicked = $-40$ pts; Remote Session Terminated = $+35$ pts.

2. **Scenario 2: WhatsApp Peer Panic**
   * *WhatsApp Window Pings:* Message from "Rahul (CSE Batchmate)": `"Bro someone leaked our 6th sem internal marks! Download and check: Marks_Sheet_Batch10.xlsx.lnk"`
   * *The Trap:* Clicking download on an untrusted executable `.lnk` or macro file.
   * *The Safe Action:* Clicking `"Report as Compromised"` or ignoring the attachment.
   * *Scoring:* Downloaded file = $-35$ pts; Ignored/Flagged = $+35$ pts.

3. **Scenario 3: UPI AutoPay Mandate**
   * *Modal:* `"College Hackathon Prize: Authorize ₹0.00 / ₹1.00 mandate to receive ₹3,000 disbursement (Max recurring limit: ₹15,000)."`
   * *The Trap:* Entering UPI PIN assuming ₹0 has no risk.
   * *The Safe Action:* Clicking `"Reject Mandate"`.
   * *Scoring:* Approved = $-45$ pts; Rejected = $+30$ pts.

---

## 📊 3. Silent Behavioral Telemetry Engine (`TelemetryTracker.js`)

State object to maintain in your root or context:

```javascript
const initialTelemetry = {
  student: { name: '', usn: '', semester: '', branch: '' },
  startTime: null,
  actions: [],
  metrics: {
    firstActionLatencyMs: 0,
    panicClickCount: 0,
    trap1Triggered: false,
    trap2Triggered: false,
    trap3Triggered: false,
    safeActionsTaken: 0,
    finalScore: 100 // Deductions applied dynamically
  }
};
```

### The 90% Threshold Branching
* If `finalScore < 90`:
  * Transition to `VideoPlayer.jsx`.
  * Stream the short 3-minute video explaining:
    1. How AutoPay mandates work.
    2. Why you never click links inside security alert popups.
    3. How attackers weaponize academic panic.
* If `finalScore >= 90`:
  * Skip video directly to `ObjectiveReview.jsx`.

---

## 📝 4. Objective Post-Mortem & Confidence Calibration

Instead of re-running the same simulation, present a clean question interface:

### Structure of Questions:
1. **Adaptive Question on Failed Trap (e.g. Frankfurt Login):**
   * *"In the simulation, you clicked 'Verify Identity' on the Frankfurt alert popup. What specific risk did that create?"*
   * Options:
     * A) It opened a credential harvesting site that captures your 2FA token. (Correct)
     * B) It automatically formatted your hard drive.
     * C) It disconnected your Wi-Fi router.
2. **Adaptive Question on Correctly Handled Scenario (e.g. WhatsApp Marks):**
   * *"You chose NOT to download the Excel sheet sent on WhatsApp. What was your reasoning?"*
   * Options:
     * A) The `.xlsx.lnk` extension indicates an obfuscated Windows shortcut executable designed to run malicious PowerShell scripts. (Correct)
     * B) I didn't care about my internal marks.
3. **The Confidence Slider (1 to 5 Stars):**
   * Below each question: *"Rate your confidence in this answer (1 = Pure Guess, 5 = Absolutely Certain)"*.

---

## 📈 5. Final Analytics Dashboard & One-Click CSV Export

At the end, render a polished analytics screen with:
* **Pre-Score vs Post-Score comparison chart** (using `Chart.js` or clean SVG bars).
* **Confidence vs Competence Matrix**:
  * *High Confidence + Correct* = **True Mastery** 🛡️
  * *Low Confidence + Correct* = **Lucky Guess** 🎲
  * *High Confidence + Wrong* = **Critical Blindspot (Dunning-Kruger)** ⚠️
  * *Low Confidence + Wrong* = **Teachable Gap** 📚
* **Download Research CSV Button**: Generates a `.csv` file with student USN, timestamps, pre-score, post-score, and failure flags ready to paste into the final VTU report!

---

## 🚀 6. Vercel Deployment Checklist

1. Create a GitHub repo for your code.
2. Connect to [Vercel](https://vercel.com) and deploy the `main` branch.
3. Add a simple custom domain or clean Vercel subdomain: e.g. `bmsit-cyber-sos-2026.vercel.app`.
4. Test on both Desktop (Chrome/Edge) and Mobile (Safari/Chrome).

**All set! You have the plan PDF, the prototype HTML, and this exact instruction set. Happy coding!**
