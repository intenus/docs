---
icon: key
---

# How It works?

Intenus operates through a sophisticated four-layer architecture designed to deliver optimal trade execution.

### The Journey of Your Trade

{% stepper %}
{% step %}
#### Intent Creation

When you express your trading goal, our **Intent Agent** transforms it into a standardized format called IGS (Intenus General Standard). This ensures your intent can be understood uniformly across the entire network.

**Example**: "Swap 1,000 SUI for at least 950 USDC within 5 minutes" becomes:

```
Intent Type: Swap (Exact Input)
Input: 1,000 SUI
Output: 950-1,000 USDC (range)
Max Slippage: 0.5%
Deadline: 5 minutes
```
{% endstep %}

{% step %}
#### Privacy Protection

Your intent is encrypted using **Seal's programmable access control**. This means:

* Only qualified solvers can see your trade
* Access is time-limited
* Your strategy remains private from potential front-runners
{% endstep %}

{% step %}
#### Solver Competition

Multiple independent **solvers** (specialized trading algorithms) compete to propose the best execution path for your trade. Each solver:

* Analyzes liquidity across all available protocols
* Constructs optimal routing strategies
* Submits their proposed solution with expected outcomes
{% endstep %}

{% step %}
#### AI-Powered Ranking

Here's where Intenus shines. Inside a **secure Trusted Execution Environment (TEE)**:

* AI models classify your intent type
* Solutions are evaluated across multiple dimensions:
  * **Profitability**: How much output you'll receive
  * **Reliability**: Historical performance of the solver
  * **Speed**: Expected execution time
  * **Risk**: Slippage and failure probability
* The best solution is selected through verifiable computation
{% endstep %}

{% step %}
#### Execution & Verification

The winning solution is executed on the Sui blockchain:

* Transaction is atomically executed using Programmable Transaction Blocks (PTBs)
* Results are verified against promised outcomes
* Execution data is archived on Walrus for transparency
* Poor-performing solvers face reputation penalties
{% endstep %}
{% endstepper %}

### Why This Approach is Superior

With Traditional DEX, you manually search for the best price across platforms. DEX Aggregators provide automated routing but limited to specific protocols. Intenus provides AI-powered competition across ALL protocols with verified, optimal execution
