---
icon: square-code
---

# Solutions

## What is a Solution?

A **solution** is a solver's proposed execution strategy for fulfilling your intent. While an intent describes _what_ you want, a solution specifies _how_ to achieve it.

**Example**:

* **Your Intent**: "Swap 1,000 SUI for USDC with minimal slippage"
* **Solver's Solution**: "Execute via 60% Cetus pool + 40% Turbos pool, expected output: 2,495 USDC, gas: 0.02 SUI"

## Anatomy of a Solution

Every solution submitted by a solver contains:

### 1. Execution Plan

The step-by-step path to execute your trade:

```json
{
  "steps": [
    {
      "protocol": "Cetus",
      "action": "swap",
      "input": "600 SUI",
      "expected_output": "1,497 USDC"
    },
    {
      "protocol": "Turbos",
      "action": "swap",
      "input": "400 SUI",
      "expected_output": "998 USDC"
    }
  ]
}
```

### 2. Expected Outcomes

Quantifiable promises about performance:

* **Output Amount**: How much you'll receive
* **Execution Time**: Expected completion time
* **Slippage**: Estimated price impact
* **Gas Cost**: Transaction fees
* **Success Probability**: Based on historical data

### 3. Solver Commitment

A cryptographic guarantee binding the solver to their proposal:

* **Signature**: Proves solution authenticity
* **Staked Amount**: Economic collateral at risk
* **Reputation Score**: Historical performance data

## How Solutions Are Evaluated

Solutions compete on multiple dimensions:

**Economic Efficiency** 📊

* Maximizes output or minimizes input
* Optimizes gas costs
* Captures MEV opportunities for users

**Execution Quality** ⚡

* Minimizes slippage
* Reduces failure risk
* Ensures timely completion

**Solver Reliability** 🛡️

* Historical accuracy
* Reputation score
* Stake amount

## Solution Lifecycle

{% stepper %}
{% step %}
#### Submission

Solvers propose solutions during a fixed auction window (typically 30-60 seconds)
{% endstep %}

{% step %}
#### Ranking

AI models evaluate solutions within a Trusted Execution Environment (TEE), scoring each against multi-dimensional criteria
{% endstep %}

{% step %}
#### Selection

The highest-ranked solution is chosen for execution
{% endstep %}

{% step %}
#### Execution

The winning solution executes on-chain via Sui's Programmable Transaction Blocks (PTBs)
{% endstep %}

{% step %}
#### Verification

Actual outcomes are compared against promised results. Solvers face penalties for underperformance
{% endstep %}
{% endstepper %}

## Why Multiple Solutions Matter

**Competition Drives Quality**

* Solvers constantly innovate to win more intents
* Users benefit from continuous optimization
* No single point of failure or monopoly

**Diverse Strategies**

* Different market conditions favor different approaches
* P2P matching vs. DEX routing vs. hybrid strategies
* Specialization emerges naturally

**Transparent Pricing**

* You always know what to expect
* Solutions can't hide costs in complex routing
* Cryptographic commitments enforce honesty

## Solution Validation

Before execution, solutions undergo rigorous checks:

✅ **Schema Compliance**: Must conform to IGS standards ✅ **Economic Feasibility**: Simulated execution must succeed ✅ **Constraint Satisfaction**: Must meet all intent requirements ✅ **Solver Authorization**: Must come from verified, staked solver ✅ **Freshness**: Market data must be recent

## Protection Mechanisms

**Against Bad Solutions**:

* Slashing penalties for failed executions
* Reputation decay for consistent underperformance
* Automatic disqualification after violations

**Against Malicious Solvers**:

* Encrypted submissions prevent copying
* TEE-based ranking eliminates bias
* Economic stakes ensure aligned incentives

## Learn More

* [How Solvers Compete](../technical/solver-network.md)
* [AI-Powered Ranking](ranking-engine.md)
* [Intent Specification](intents.md)
