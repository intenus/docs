---
description: What is Prerank Engine?
icon: filter
---

# Prerank Engine

The **Prerank Engine** is the first validation layer in the Intenus intent-based trading pipeline. It acts as an intelligent filter that validates solver-submitted solutions against user-defined constraints before forwarding them to expensive AI ranking services.

{% hint style="success" %}
The Prerank Engine runs inside a verifiable enclave (Trusted Execution Environment – TEE), ensuring that all pre-ranking operations are transparent, secure, and fully attestable within a trusted environment. It serves as one of the two _**orchestrartor**_ of the [universal-solvers-network.md](universal-solvers-network.md "mention")
{% endhint %}

### **The Challenge It Solves**

* High computational costs (AI ranking is expensive)
* Exposure to invalid solutions that could fail or lose user funds

### **How Prerank Engine Helps?**

1. Monitors Sui blockchain for `IntentSubmitted` and `SolutionSubmitted` events
2. Fetches encrypted intent/solution data from Walrus decentralized storage
3. Performs instant constraint-based validation (deadline, slippage, gas limits, routing rules)
4. Filters out invalid solutions before they reach AI ranking
5. Provide features vector for ranking calculations.

## Why Pre-ranking?

Without pre-filtering:

* &#x20;Low-quality solutions waste ranking resources
* Invalid solutions delay processing
* Malicious submissions can spam the system
* Every solution costs gas/compute to evaluate

With pre-ranking:

* Only valid solutions reach full ranking
* Faster processing for quality solvers
* Economic spam prevention
* Efficient resource utilization

## Architecture

{% code title="Pre-Ranking Engine Architeture" %}
```
┌─────────────────────────────────────────────────────────────────┐
│                        Sui Blockchain                           │
│  IntentSubmitted Events │ SolutionSubmitted Events              │
└────────────┬────────────┴──────────────────┬───────────────────┘
             │                                │
             ▼                                ▼
    ┌────────────────┐              ┌────────────────┐
    │  Sui Service   │              │  Sui Service   │
    │  (Event Poll)  │              │  (Event Poll)  │
    └────────┬───────┘              └────────┬───────┘
             │ Emit                           │ Emit
             │ intent.submitted               │ solution.submitted
             ▼                                ▼
    ┌──────────────────────────────────────────────────┐
    │         Processing Service (Orchestrator)        │
    │  - Manages solution windows                      │
    │  - Coordinates instant preranking workflow       │
    └──────┬────────────────────────────────┬──────────┘
           │                                 │
           ▼                                 ▼
  ┌─────────────────┐             ┌──────────────────────┐
  │ Walrus Service  │             │  PreRanking Service  │
  │ - Fetch Intent  │             │  - Validate Now      │
  │ - Fetch Solution│             │  - Dry Run           │
  │ - Decrypt Data  │             │  - Extract Features  │
  └────────┬────────┘             └──────────┬───────────┘
           │                                  │
           ▼                                  ▼
  ┌──────────────────────────────────────────────────────┐
  │              Redis Storage Service                    │
  │  - Store intents/solutions (1h TTL)                  │
  │  - Event cursor (crash recovery)                     │
  │  - Ranking queue (AI service input)                  │
  └──────────────────────────────────────────────────────┘
                           │
                           ▼ Window closes
                  ┌──────────────────┐
                  │  AI Ranking API  │
                  │  (External)      │
                  └──────────────────┘
```
{% endcode %}

## Validation Pipeline

The engine validates solutions against **IGS (Intenus General Standard)** constraints defined by users:

| Constraint Type   | What It Protects            | Real-World Example                             |
| ----------------- | --------------------------- | ---------------------------------------------- |
| **Deadline**      | Time-bound execution        | "Must execute within 5 minutes of submission"  |
| **Max Slippage**  | Price deviation tolerance   | "Price can move maximum 2% (200 basis points)" |
| **Min Outputs**   | Guaranteed receive amounts  | "Must receive at least 950 USDC (not less)"    |
| **Max Inputs**    | Spending ceiling protection | "Don't spend more than 100 SUI"                |
| **Gas Budget**    | Transaction cost limits     | "Gas fees cannot exceed $2 worth of SUI"       |
| **Routing Rules** | Protocol safety controls    | "Only use Cetus DEX, block risky protocols"    |
| **Limit Price**   | Price boundary enforcement  | "Only execute if SUI ≥ $3.00"                  |

## **Validation Strategy**

* **Fast-fail approach:** Check cheap constraints first (deadline, routing) before expensive ones (dry-run simulation)
* **Two-phase validation:** Pre-flight checks → Blockchain simulation → Output verification

### Optional Quality Signals

Additional factors that improve ranking odds:

✨ **High Solver Reputation**: Previous performance > 8.0/10 ✨ **Competitive Output**: > 5% better than benchmark ✨ **Low Gas Cost**: < median gas for similar intents ✨ **Fast Execution**: Expected time < intent deadline ✨ **Novel Strategy**: Unused approach in last 100 similar intents

## Spam Prevention

### Economic Barriers

**Submission Requirements**:

* Minimum stake: 1,000+ SUI
* Per-submission gas fee: 0.001+ SUI
* Reputation at risk: Poor solutions hurt future chances

**Effect**: Makes spam economically unprofitable

### Rate Limiting

**Per-Solver Limits**:

* Maximum 5 solutions per intent
* Maximum 100 solutions per hour
* Cooldown after rejected solutions

**Effect**: Prevents solution flooding

### Quality Penalties

**Repeated Rejections**:

* 3 rejected solutions in a row: 1-hour cooldown
* 10 rejected solutions in 24h: Reputation penalty
* 50 rejected solutions in 7 days: Temporary suspension

**Effect**: Incentivizes quality over quantity

Different intent types have specialized checks:

## Learn More

* [Full Ranking Engine](ranking-engine.md)
* [Solution Specifications](solutions.md)
* [Solver Network](universal-solvers-network.md)

