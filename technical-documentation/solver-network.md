---
icon: diagram-project
---

# Solver Network

## What are Solvers?

**Solvers** are independent entities (algorithms, trading firms, or individuals) that compete to execute your intents optimally. Think of them as specialized trading experts who:

* Monitor available intents
* Construct execution strategies
* Compete to provide the best outcomes
* Earn fees for successful executions

## How Solvers Compete

{% stepper %}
{% step %}
#### **Registration**

Solvers must:

* Stake minimum capital (aligned incentives)
* Register their identity on-chain
* Build reputation over time
{% endstep %}

{% step %}
#### **Intent Discovery**

Qualified solvers can:

* Access encrypted intent data
* Decrypt based on their credentials
* View intent details during auction windows
{% endstep %}

{% step %}
#### **Solution Construction**

Each solver independently:

* Analyzes current market conditions
* Searches liquidity across all protocols
* Constructs optimal routing strategies
* Simulates expected outcomes
{% endstep %}

{% step %}
#### **Submission**

Solvers submit their proposed solutions including:

* Exact execution path
* Expected output amounts
* Gas cost estimates
* Performance commitments
{% endstep %}
{% endstepper %}

## Solver Strategies

Different solvers may employ various approaches:

**DEX Aggregation**

Traditional route optimization across automated market makers (AMMs).

**Peer-to-Peer Matching**

Finding counterparties with opposite intents for direct settlement (like CoW Protocol).

**Hybrid Approaches**

Combining on-chain liquidity with off-chain matching.

**AI-Driven Strategies**

Machine learning models that predict optimal execution timing and routing.

## Quality Assurance

The protocol ensures solver quality through:

**Reputation Scoring**:

* Historical accuracy tracking
* Consistent performance rewards
* Public reputation scores

**Economic Penalties**:

* Stake slashing for malicious behavior
* Reputation loss for poor execution
* Automatic disqualification for repeated violations

**Performance Incentives**:

* Higher rankings for reliable solvers
* Increased fee share for top performers
* Visibility multipliers based on stake and reputation
