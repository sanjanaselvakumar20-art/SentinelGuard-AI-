


# SentinelGuard AI: Contextual and Dual-Key Defense Agent

Crimeathon'26 · Case CR-26-047 · Harbor & Finch · Selected approach: Defense

## Overview

Harbor & Finch lets external software (LedgerOne, HelpDeskr and BlueVault) connect through API keys. These keys skip employee SSO login, and some hold broader permissions and weaker restrictions than the business needs. With weak monitoring and uncertain permission reviews, a stolen or over-permissioned key could export large amounts of customer data or change vendor payment details without anyone noticing.

SentinelGuard AI is a guard that sits in front of LedgerOne. It checks every external API call for context and requires a second approval for sensitive vendor changes, before any harm is done.

## Problem statement

Unmonitored third-party API access to LedgerOne, HelpDeskr and BlueVault, without employee SSO, puts customer data and vendor payment records at risk of unauthorized access, bulk export and tampering.

The case evidence points to this problem: API activity and export volumes (E01, E18), registered integrations and scopes (E04), private-link traffic (E15) and vendor-record changes (E19).

## Solution

SentinelGuard combines two defense ideas in one lightweight middleware.

**1. Dual-Key and Contextual Anomaly Gateway (the Watchdog).**
Standard API monitoring looks only at IP addresses or rate limits. The Watchdog also checks the context of each call: whether the key is registered, whether the action is within its approved scope, and whether the time and volume fit its normal sync window. If an integration tries a large export or a vendor-record change at an unusual time, SentinelGuard places a temporary sandbox hold and sends a one-click alert to the IT Security Administrator (Aditi Kapoor), instead of only logging it.

**2. Vendor Payment Two-Person Rule Interceptor (the Gatekeeper).**
Any automated request that changes a vendor's bank routing number or account name must carry an `approval_ref`. That reference must match an active, single-use approval signed off by the Finance Manager (Madhavi Sundar) for that vendor. A request without a valid approval is blocked immediately.

Daily-life analogy: a bank vault that needs both a physical key (the API key) and a manager's live sign-off when a high-value action happens.

**Pipeline:** API request → Watchdog → Gatekeeper → LedgerOne (safe execution or hold).

## Key features

- Approved-integration register with least-privilege scopes
- Context checks on time, volume and sync windows
- Sandbox hold for suspicious large exports and reads
- One-time `approval_ref` approvals bound to a single vendor
- Instant block for vendor bank or name edits without valid approval
- Hard block and dual-manager alert for after-hours bulk vendor edits
- One-click release or reject for held requests
- Full audit log with the reason for every decision
- Replay of your own logs (pasted as JSON)

## How it overcomes the problem

| Weakness in the case | How SentinelGuard responds |
|---|---|
| Keys bypass employee SSO | Checks the behavior of each call, not only the key |
| Keys with excess permissions | Blocks any action outside the key's registered scope |
| Silent bulk exports | Holds them in a sandbox and alerts IT Security |
| Vendor payment tampering | Requires a second, Finance-signed approval for each bank change |
| IP rules fail on trusted tunnels | Judges time, volume and scope, so a trusted source cannot hide odd behavior |
| Routine overnight syncs look like exports | Allows them only inside each key's approved window, avoiding false alarms |

## Benefits

- Stops damage before it happens, instead of reporting it afterwards
- Protects customer data and vendor payments at the point of access
- Keeps people in control: IT Security and Finance decide with one click
- Lightweight: sits in front of existing systems without replacing them
- Auditable: every decision has a recorded reason, which supports renewals and compliance

## Technology

- Python and FastAPI proxy for the middleware (planned design)
- Pandas and Scikit-Learn for baseline timing and volume models (planned design)
- Signed `approval_ref` token store linked to Finance
- Webhook dispatcher for one-click alerts

## Working prototype

The runnable demo is a single HTML page that simulates the guard in the browser. It uses only requests that you type, paste or generate with its preset scenarios, and it connects to no real system.

- Open `sentinelguard-demo.html` in any modern browser, or use the published demo link.
- Try the preset scenarios: normal overnight sync, after-hours export, bank edit without approval, bank edit with approval, night bulk vendor edit and unknown key.
- Issue an `approval_ref` in the Finance panel, then use it in a vendor edit.
- Release or reject held requests in the IT Security panel.
- Paste your own logs into the replay box to test them.

## Current status and limits

- The demo uses rule-based checks. The behavioral-model component is part of the planned design.
- Demo thresholds (1,000+ records as bulk, 08:00–19:00 operating hours, a 01:00–03:00 sync window for TallyBridge Connect) are defaults and should be tuned to real evidence.
- Early replay results (100% of unverified E19 bank edits blocked, 0% false alarms on TallyBridge syncs, under 45 ms inspection) are preliminary, not final proof.
- Known risks: unsynced BlueVault clocks can obscure traces, approvals can pause urgent changes if managers are offline, and slow low-volume reads may look like normal queries.

## Next steps

1. Live stress test against unseen attack datasets (Tier 3).
2. Extend the guard to HelpDeskr and BlueVault exports and file keys.
3. Goal: zero unauthorized payouts, with auditable trust for customer renewals and compliance.

## Overall view

SentinelGuard AI turns a trusted-but-unwatched access path into a checked one. It adds context to every API call and a second signature to every vendor bank change, so a stolen or over-permissioned key can no longer quietly drain data or divert payments.




        