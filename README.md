# X-Border: Cross-Border FX Payment Routing Engine

A high-performance, multi-hop financial routing engine built on the **XRP Ledger (XRPL)** using **Next.js 16**, **TypeScript**, and **Tailwind v4**.

---

## 🛑 The Problem: Cross-Border Payments are Broken
Moving money internationally across different currencies (Foreign Exchange / FX) is traditionally slow, expensive, and opaque.

If a business or user wants to send **USD** from the United States to a recipient who needs **EUR** in Europe, the transaction must navigate the legacy SWIFT banking network:
*   **High Intermediary Fees:** Multiple correspondent banks sit in the middle, each skimming a fee off the top.
*   **Settle Latency:** Clearing and settlement take between **3 to 5 business days**.
*   **Counterparty Risk:** Transactions can fail or get stuck mid-route, leaving capital in limbo with zero real-time visibility.

---

## 💡 Our Solution: Instantly Settled Digital Asset Routing
**X-Border** replaces legacy banking chains with the **XRP Ledger (XRPL)** infrastructure. By treating native **XRP** as a universal neutral bridge asset, value can cross borders and change currencies natively in **under 3 seconds** for fractions of a penny.

Instead of hunting for rare, direct liquidity pools (e.g., USD directly to EUR), the system models the blockchain's order books and **Automated Market Makers (AMMs)** as a financial network graph to automatically route payments through optimized multi-hop hops:

\[\text{Source Asset (USD)} \longrightarrow \text{Bridge Asset (XRP)} \longrightarrow \text{Destination Asset (EUR)}\]

---

## 🎯 What This Project Accomplishes
This platform functions as **"Google Maps for Money."** It solves core blockchain fintech engineering challenges across three layers:

### 1. Real-Time Pathfinding (Algorithmic Routing)
The backend service actively listens to the live XRPL Testnet via stateful WebSockets. When a payment request is initiated, our custom routing engine scans the ledger’s distributed exchange topology. It calculates the absolute **cheapest execution path**, factoring in:
*   **Slippage & Price Impact:** Modeling AMM Constant Product curves (\(x \times y = k\)) to prevent massive value loss on large transfers.
*   **Transfer Fees:** Factoring in operational gateway fees charged by individual currency issuers.

### 2. Atomic Settlement (All-or-Nothing Execution)
Using XRPL's native `Payment` transaction primitives with strict execution path attributes, the engine wraps the entire multi-hop swap into a **single, atomic transaction package**. The transaction either completely succeeds or gracefully reverts—guaranteeing that funds are never locked or lost halfway through a route.

### 3. High-Fidelity Fintech Visualization
The user interface leverages **Magic UI** and **Aceternity UI** to render complex on-chain financial operations into intuitive, production-grade dashboards:
*   **Dynamic Flow Lines:** Users visually monitor their money changing states and crossing liquidity nodes in real time.
*   **Deterministic State States:** Built using **React Query** (TanStack Query) to manage state cache expiration perfectly synchronized with the 3–5 second ledger close times, avoiding rate-limiting on blockchain infrastructure.

---

## 🛠️ Core Infrastructure Architecture

*   **Core Domain:** Decoupled Architecture / Factory Patterns (Allows replacing XRPL with EVM/Solana adapters seamlessly without rewriting business logic).
*   **State Layer:** `Zustand` for local cryptographic key memory retention + `@tanstack/react-query` for high-throughput node synchronization.
*   **Style Engine:** Tailwind v4 (utilizing pure CSS `@theme` variables for lightning-fast hardware accelerated graphics rendering).
