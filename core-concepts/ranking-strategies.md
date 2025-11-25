---
description: >-
  Explore how the Ranking Engine is able to produce precise and accurate scoring
  results.
icon: chess-board
---

# Ranking Strategies

## Overview

The Intenus Protocol employs dynamic ranking strategies to evaluate and score solver solutions based on user intent characteristics and market conditions. Rather than using a one-size-fits-all approach, the AI-powered ranking engine selects from 11 distinct strategies, each optimized for specific trading scenarios and user priorities.

### How Ranking Strategies Work

Each ranking strategy is essentially a mathematical formula that combines nine core factors (f₁-f₉) with dynamically predicted weights (w₁-w₉). The AI classification engine first analyzes the user's intent to determine:

* **Intent Category**: swap, limit order, complex DeFi, arbitrage, or other
* **User Priority**: speed, cost, output maximization, or balanced approach
* **Complexity Level**: simple, moderate, or complex execution requirements
* **Risk Tolerance**: low, medium, or high risk acceptance

Based on this classification, the system selects an appropriate ranking strategy and uses machine learning models to predict optimal weights for the nine scoring factors.

## Ranking Strategy Formulas

### Strategy Overview & Formulas

<table><thead><tr><th width="212.69140625">Strategy</th><th width="282.95703125">Formula</th><th>Use Case</th></tr></thead><tbody><tr><td><strong>Surplus-First</strong></td><td><code>w₁×f₁ + w₃×(1/f₃) + w₈×f₈</code></td><td>Whale trades, large swaps</td></tr><tr><td><strong>Cost-Minimization</strong></td><td><code>w₄×(1/f₄) + w₂×f₂ + w₉×f₉</code></td><td>Gas-sensitive users, small trades</td></tr><tr><td><strong>Surplus-Maximization</strong></td><td><code>w₁×f₁ + w₂×f₂ + w₃×(1/f₃)</code></td><td>High-value swaps, arbitrage</td></tr><tr><td><strong>Speed-Priority</strong></td><td><code>w₇×(1/f₇) + w₉×f₉ + w₁×f₁</code></td><td>Day traders, MEV protection</td></tr><tr><td><strong>Execution-Guarantee</strong></td><td><code>w₉×f₉ + w₈×f₈ + w₄×(1/f₄)</code></td><td>Protocols, institutions</td></tr><tr><td><strong>Stability-First</strong></td><td><code>w₂×f₂ + w₅×(1/f₅) + w₁×f₁</code></td><td>Stablecoin swaps, large orders</td></tr><tr><td><strong>Reliability-Focus</strong></td><td><code>w₉×f₉ + w₅×(1/f₅) + w₈×f₈</code></td><td>Multi-hop swaps, exotic pairs</td></tr><tr><td><strong>Gas-Optimized</strong></td><td><code>w₃×(1/f₃) + w₄×(1/f₄) + w₉×f₉</code></td><td>L2 optimization, micro-transactions</td></tr><tr><td><strong>Speed-Profit</strong></td><td><code>w₁×f₁ + w₇×(1/f₇) + w₉×f₉</code></td><td>MEV bots, arbitrageurs</td></tr><tr><td><strong>Risk-Adjusted</strong></td><td><code>w₂×f₂ + w₈×f₈ + w₉×f₉</code></td><td>DeFi protocols, lending</td></tr><tr><td><strong>Balanced</strong></td><td><code>Σ(wᵢ × fᵢ)</code> where <code>Σwᵢ = 1</code></td><td>Default fallback strategy</td></tr></tbody></table>

### Scoring Factors (f₁-f₉)

| Factor                 | Symbol | Description                  | Type               |
| ---------------------- | ------ | ---------------------------- | ------------------ |
| **Surplus USD**        | `f₁`   | Absolute profit in USD       | Higher = Better    |
| **Surplus Percentage** | `f₂`   | Relative profit percentage   | Higher = Better    |
| **Gas Cost**           | `f₃`   | Gas fees in USD              | Lower = Better     |
| **Total Cost**         | `f₄`   | Protocol/swap fees total     | Lower = Better     |
| **Total Hops**         | `f₅`   | Number of routing hops       | Lower = Better     |
| **Protocols Count**    | `f₆`   | DEX protocols involved       | Varies by strategy |
| **Execution Time**     | `f₇`   | Expected execution time      | Lower = Better     |
| **Reputation Score**   | `f₈`   | Historical solver reputation | Higher = Better    |
| **Success Rate**       | `f₉`   | Solver success rate          | Higher = Better    |

### Weight Variables (w₁-w₉)

| Weight | Maps to Factor | Description                    |
| ------ | -------------- | ------------------------------ |
| `w₁`   | `f₁`           | Weight for surplus USD         |
| `w₂`   | `f₂`           | Weight for surplus percentage  |
| `w₃`   | `f₃`           | Weight for gas cost            |
| `w₄`   | `f₄`           | Weight for total cost          |
| `w₅`   | `f₅`           | Weight for routing hops        |
| `w₆`   | `f₆`           | Weight for protocols count     |
| `w₇`   | `f₇`           | Weight for execution time      |
| `w₈`   | `f₈`           | Weight for solver reputation   |
| `w₉`   | `f₉`           | Weight for solver success rate |

### General Formula Structure

All strategies follow the general pattern:

```
Score = Σ(wᵢ × fᵢ) where i ∈ {1,2,...,9}
```

For factors where "lower is better" (f₃, f₄, f₅, f₇), the formula uses:

```
wᵢ × (1/fᵢ) or wᵢ × (max_value - fᵢ)
```

### Dynamic Weight Prediction

Weights `wᵢ` are dynamically predicted by ML models based on:

* Intent classification and features
* Market context and conditions
* User behavior and preferences
* Solver pool characteristics

The AI ranking engine outputs the 9 weights that best match the user's intent and current market conditions.

### Example dataset on Walrus

{% file src="../.gitbook/assets/training_data.csv" %}
