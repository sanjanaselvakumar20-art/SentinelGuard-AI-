# SentinelGuard AI: Contextual & Dual-Key Defense Agent
**CRIMEATHON'26 Case File CR-26-047 | Harbor & Finch Freight Pvt. Ltd.**

## Overview
SentinelGuard AI is an intelligent middleware defense agent designed to neutralize unmonitored third-party API activity and protect vulnerable vendor payment records (`E19`) in LedgerOne without disrupting legitimate overnight operations (`E15`).

## Key Features
- **Watchdog Layer:** Real-time behavioral sensing that flags bulk data exports or after-hours anomalies.
- **Gatekeeper Layer:** Two-person authorization rule enforcement requiring verified `approval_ref` tokens signed off by Finance Manager Madhavi Sundar before executing sensitive vendor record changes.

## How to Run the Demo / Simulation
1. Clone the repository: `git clone https://github.com/your-username/SentinelGuard-AI.git`
2. Install dependencies: `pip install -r requirements.txt`
3. Run the simulation: `python run_simulation.py`

# SentinelGuard-AI-
Active middleware and contextual dual-key defense agent for third-party unauthorized API activity



[Third-Party API Call] 
         │
         ▼
┌────────────────────────────────────────────────────────┐
│ LAYER 1: WATCHDOG (Contextual & Behavioral Sensing)    │
│ • Evaluates operating windows (IST/UTC alignment)      │
│ • Checks payload record volumes vs. baseline norms     │
│ • Action: Places anomalies in Sandbox Hold + alerts    │
│   IT Security Admin (Aditi Kapoor)                     │
└────────────────────────────────────────────────────────┘
         │
         ▼
┌────────────────────────────────────────────────────────┐
│ LAYER 2: GATEKEEPER (Two-Person Rule Enforcement)      │
│ • Inspects E19 vendor bank routing & account edits     │
│ • Validates cryptographic `approval_ref` signed by     │
│   Finance Manager (Madhavi Sundar)                     │
│ • Action: Hard-blocks missing/invalid approval tokens  │
└────────────────────────────────────────────────────────┘
         │
         ▼
[LedgerOne Database Execution / Audit Proof Log]


SentinelGuard-AI/
├── README.md                  # Project overview, architecture, and setup guide
├── requirements.txt           # Python dependencies
├── src/
│   ├── sentinel_guard.py      # Core Watchdog & Gatekeeper middleware engine
│   ├── log_correlator.py      # UTC/IST timestamp normalizer across E01, E15, E18, E19
│   └── run_simulation.py      # CLI & interactive replay simulator for demo & testing
├── docs/
│   ├── SentinelGuard_Pitch.pdf        # 10-Slide Concept & Architecture Deck
│   └── One_Page_Project_Overview.pdf  # Final Project Summary Slide
└── proof-pack/
    ├── validation_metrics.json        # Accuracy, precision, and false-alarm benchmarks
    └── short_report.md                # Timeline reconstruction, assumptions & ruled-out hypotheses



