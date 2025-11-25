---
icon: brain-circuit
---

# AI-Powered Ranking

## Why AI?

Traditional solver selection uses simple metrics (lowest price, fastest execution). Intenus employs sophisticated AI to evaluate solutions across multiple dimensions simultaneously.

## The Ranking Process

{% stepper %}
{% step %}
#### Intent Classification

Machine learning models analyze your intent to determine:

* Trading urgency (immediate vs. patient execution)
* Size category (retail vs. institutional)
* Risk tolerance (based on slippage constraints)
* Complexity level (simple swap vs. multi-step strategy)

This classification determines which ranking strategy is optimal for your specific needs.
{% endstep %}

{% step %}
#### Multi-Factor Evaluation

Solutions are scored across multiple dimensions:

**Economic Efficiency**:

* Output surplus vs. market benchmark
* Gas cost optimization
* Price impact minimization

**Execution Quality**:

* Historical solver reliability
* Slippage control accuracy
* Transaction success rate

**Speed & Certainty**:

* Expected confirmation time
* Probability of successful execution
* Network congestion adaptation

**Strategic Value**:

* MEV protection effectiveness
* Privacy preservation quality
* Long-term price impact
{% endstep %}

{% step %}
#### Ranking Algorithm

A reinforcement learning model combines scores to produce final rankings. The model continuously learns from:

* Actual execution outcomes
* User satisfaction signals
* Market condition correlations
* Solver performance patterns
{% endstep %}

{% step %}
#### Verifiable Computation

All AI ranking occurs within **Nautilus Trusted Execution Environments (TEEs)**:

* **Attestation**: Cryptographic proof that ranking was performed correctly&#x20;
* **Reproducibility**: Anyone can verify the ranking given the same inputs&#x20;
* **Integrity**: No party can manipulate the ranking process&#x20;
* **Confidentiality**: Solution details remain private during evaluation

#### Continuous Improvement

The AI models improve over time through:

* **Historical Data**: Every execution creates training data stored on Walrus
* **Feedback Loops**: User satisfaction and outcome quality inform model updates
* **Market Adaptation**: Models adjust to changing DeFi landscape
* **Solver Innovation**: New strategies are automatically incorporated
{% endstep %}
{% endstepper %}
