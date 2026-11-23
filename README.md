# Cyber SOS: Immediate Digital Incident Response Guide

> **1BSOP308 Societal Project · Batch 10**  
> **Department of Computer Science & Engineering**  
> **BMS Institute of Technology and Management (BMSIT&M), Bengaluru**  
> **Project Guide:** Prof. Ester Prescilla E  

---

## Team Members
* **Aditya Singh**
* **Tripti Khatri**
* **Ananya Nath**
* **Mukund Sharma**

---

## Project Overview

**Cyber SOS** is an interactive digital safety and incident triage benchmark designed to evaluate, educate, and calibrate student decision-making against modern deceptive digital threats. 

Instead of traditional, abstract multiple-choice security questions, Cyber SOS places candidates inside **hyper-realistic interactive interfaces** (such as smartphone Google Pay mandate requests, Microsoft 365 Outlook webmail, Google OAuth consent prompts, and Chrome extension permission dialogues). Candidates must interact with the screens as they would on their own devices, declare their confidence level, and justify their actions.

---

## Key Capabilities

1. **Hyper-Realistic Interactive Threat Scenarios:**
   * **Google Pay AutoPay Mandate:** A flagship smartphone viewport simulating a disguised monthly ₹15,000 AutoPay e-mandate disguised as a ₹0.00 validation fee.
   * **Official vs. Spoofed College Communications:** Microsoft 365 Outlook interface testing detection of double extensions (`.xlsx.lnk`, `.pdf.exe`) and spoofed institutional sender domains (`bmsit-careerportal.ac.in` vs official `bmsit.in`).
   * **Minimal vs. High-Privilege OAuth:** Google SSO consent dialogues assessing awareness of OAuth scope permissions.
   * **High-Privilege Chrome Extensions:** Simulated Chrome Web Store dialogues requesting all-website data modifications.

2. **Certainty-Based Marking (CBM) & Lucky Guess Filter:**
   * Evaluates the compound tuple: $(Action, Technical\_Reason, Confidence\_Tier)$.
   * Eliminates lucky guessing: clicking the safe action without the correct technical rationale awards **0 points**.
   * Confident mistakes on deceptive traps carry scaled penalties to eliminate overconfidence.

3. **Deterministic Diagnostic Feedback Engine:**
   * Generates domain-by-domain behavioral trajectory reports comparing pre-intervention baseline reflexes against post-intervention transfer skills.
   * Provides actionable **Rules of Thumb** for each digital threat vector.

4. **Atlassian Design System (ADS) & Tron Vector Aesthetics:**
   * Professional enterprise typography stack (`Inter`), 4px lozenges, and Atlassian Blue action controls (`#0c66e4`).
   * Custom neon-luminescent Tron vector emoji suite (`.tron-glyph`) with zero external font or image dependencies.

---

## Repository Structure

```
├── index.html                                    # Production Single-Page Web Application
├── cyber_sos_interactive_prototype.html          # Early Stage Interactive Prototype
├── electric_field_particles_demo.html            # Physics Particle Background Engine
├── vercel.json                                   # Production Edge Headers & Security Configuration
├── Cyber_SOS_Updated_Project_Plan_Batch10.pdf    # Detailed Societal Project Execution Plan
├── Cyber_Safety_Societal_Project_Concepts.pdf   # Research & Threat Concept Schematics
├── Societal Project_synopsis BATCH-10(1).docx   # Departmental Synopsis Document
├── TEAMMATE_IMPLEMENTATION_HANDOVER.md           # Engineering & Architecture Handover Notes
└── README.md                                     # Project Documentation & Overview
```

---

## Quick Start / Running Locally

No build tools or package managers required. Simply open `index.html` in any modern web browser or serve via a local static server:

```bash
# Python local server
python -m http.server 8000

# Access via browser
open http://localhost:8000
```
