# Anumati Core: Prototype

Interactive prototype for **Anumati**, a zero-trust consent layer that sits between a personal AI agent and the payment, eSign and identity APIs it acts through.
Submitted with the Flipkart APM '29 2-pager by Bhagavath M S.

> This is a visual prototype with simulated data. Nothing connects to real UPI, Aadhaar or bank systems.

## How to run

1. Unzip the folder.
2. Open `index.html` in Chrome, Edge or Firefox.
3. Stay online. React, Tailwind and the icons load from public CDNs.

No install or build step is needed. The prototype is plain HTML, CSS and JS.

## What to try (about 3 minutes)

Click the scenarios in the left pane, in this order:

| # | Scenario | What to watch for |
|---|---|---|
| 1 | **Blinkit reorder · ₹350** | Auto-passes as T1. A single-use token is minted and the action is logged in the ledger. |
| 2 | **Mumbai flight · ₹2,200** | T2. Appears in the batched digest. Approve it with one tap. |
| 3 | **HSR lease eSign · ₹1,35,000** | T3 hard block. With **Commit-first** on, you set your max rent *before* seeing the agent's pick. The consent card flags the **sponsored listing** and shows cheaper flats the agent ranked lower. Try **Select unsponsored option #2**. |
| 4 | **BBD EV scooter · ₹1,20,000** | T3. The UPI AutoPay is held. Try **Pay ₹2,499 refundable token only**. |
| 5 | **₹400 gift card at 3:15 AM** | The rules alone give T1, but the scorer escalates it to **T3**: the instruction came from a promotional email (prompt injection). |

Also try:
- **Approve in under 3 seconds** on any T3 card. You get a "which payee?" check instead of a reflex approval.
- **1-click revoke** on any executed T1/T2 row in the audit ledger.
- **Custom payload** (Form or JSON tab): build your own tool call and see the predicted tier before you send it.
- **Leave a T3 card alone for 2 minutes**: it expires as declined. The system fails closed.

## How decisions are made

**Tier = reversibility × personal impact**, where impact is a share of Priya's monthly discretionary budget (₹1,00,000, via Account Aggregator).

| Tier | Rule | Handling |
|---|---|---|
| T1 Routine | Reversible, under 2% of budget, known payee | Auto-execute and log |
| T2 Notable | Reversible, 2–15%, or a new payee | 1-tap batched digest |
| T3 Critical | Irreversible, over 15%, or a protected category (legal, investment, identity, physical access, career messages) | Blocked until informed FIDO2 consent |

Three principles from the 2-pager, visible in the prototype:
- **Credential custody.** The agent holds no payment or eSign keys. Every action needs a single-use token scoped to payee, amount and expiry.
- **Rules decide, ML only escalates.** The anomaly scorer can raise a tier, never lower it.
- **Independent explanation.** Anumati writes the consent card from the verified payload, not the agent.

## Files

| File | Purpose |
|---|---|
| `index.html` | The prototype. Open this one. |
| `anumati-core.html` | Same app without the page wrapper. Not needed to run the prototype. |
