---
icon: medal
---

# Ranking Engine

## The Brain of Intenus

The **Ranking Engine** is Intenus's AI-powered system that evaluates competing solver solutions and selects the optimal one for execution. Unlike simple price comparisons, it performs sophisticated multi-dimensional analysis within a secure Trusted Execution Environment (TEE).

## Why AI-Powered Ranking?

**Traditional Systems** use simple, deterministic metrics:
- Highest output amount
- Lowest gas cost
- First-come-first-served

**Intenus Ranking Engine** considers complex, nuanced factors:
- Historical solver reliability
- Risk-adjusted returns
- Market condition analysis
- User preference patterns
- Execution probability

## How It Works

{% stepper %}
{% step %}
### 1. Intent Classification

When solutions arrive, AI models first classify the intent:

```
Input: "Swap 1,000 SUI for USDC, minimize slippage"

Classification:
- Type: swap.exact_input
- Complexity: simple
- Risk tolerance: low
- Priority: execution quality over speed
```

This classification determines which ranking strategy to apply.
{% endstep %}

{% step %}
### 2. Solution Scoring

Each solution is evaluated across multiple dimensions:

**Economic Factors** (40% weight):
- Output amount vs. benchmark
- Gas efficiency
- MEV capture for user

**Reliability Factors** (30% weight):
- Solver reputation score
- Historical accuracy
- Success rate for similar intents

**Execution Factors** (20% weight):
- Expected completion time
- Slippage probability
- Failure risk

**Strategic Factors** (10% weight):
- Novel approaches
- Market adaptation
- Innovation bonus
{% endstep %}

{% step %}
### 3. Secure Computation

All ranking happens inside Nautilus TEE:
- Solutions remain confidential
- Computation is verifiable
- Results are cryptographically attested
- No human can bias the outcome
{% endstep %}

{% step %}
### 4. Winner Selection

The highest-scoring solution wins:
- Ranking proof generated
- Winning solver notified
- Solution executed on-chain
- Results archived for learning
{% endstep %}
{% endstepper %}

## Ranking Strategies

Different intent types use specialized strategies:

### For Spot Swaps

**Focus**: Output maximization + reliability

```
Score = (0.4 × output_amount) +
        (0.3 × solver_reputation) +
        (0.2 × execution_speed) +
        (0.1 × innovation)
```

### For Limit Orders

**Focus**: Execution certainty + price accuracy

```
Score = (0.5 × price_accuracy) +
        (0.3 × execution_probability) +
        (0.2 × gas_efficiency)
```

### For Complex Strategies

**Focus**: Successful completion + cost efficiency

```
Score = (0.4 × total_value) +
        (0.3 × completion_risk) +
        (0.2 × solver_reputation) +
        (0.1 × gas_optimization)
```

## Multi-Factor Analysis

### Economic Efficiency

**Output Surplus**:
```
surplus = (actual_output - minimum_expected) / minimum_expected
```

Higher surplus = better deal for users

**Gas Optimization**:
```
efficiency = expected_value / total_gas_cost
```

Balances value against execution cost

### Solver Reputation

Reputation score aggregates:
- **Accuracy**: Promised vs. delivered outcomes
- **Reliability**: Success rate over last 100 intents
- **Consistency**: Performance variance
- **Longevity**: Time active in network

**Reputation Formula**:
```
reputation = (accuracy × 0.4) +
             (reliability × 0.3) +
             (consistency × 0.2) +
             (longevity × 0.1)
```

### Risk Assessment

AI models evaluate:
- Market volatility impact
- Liquidity depth risks
- Smart contract dependencies
- Execution complexity

High-risk solutions require higher expected value to win.

### Speed Metrics

**Expected Execution Time**:
- Current network congestion
- Transaction complexity
- Historical solver speed
- Protocol response times

**Confirmation Probability**:
- Gas price adequacy
- Transaction ordering likelihood
- Network conditions

## Verifiable Computation

### TEE Infrastructure

Ranking occurs in Nautilus Trusted Execution Environment:

**Security Properties**:
✅ **Isolation**: Code runs in secure enclave
✅ **Attestation**: Cryptographic proof of correct execution
✅ **Confidentiality**: Solution details remain private
✅ **Integrity**: Results cannot be tampered with

### Proof Generation

Each ranking produces:

```json
{
  "ranking_id": "rank_abc123",
  "tee_attestation": "0x...",
  "winner_solution": "sol_xyz789",
  "scores": {
    "sol_xyz789": 9.2,
    "sol_def456": 8.7,
    "sol_ghi789": 8.1
  },
  "timestamp": 1699123456000
}
```

Users and solvers can verify:
- Computation occurred in genuine TEE
- Ranking followed documented strategy
- Winner was correctly selected

## Continuous Learning

### Training Data Collection

Every execution generates training data:
- Intent specification
- Competing solutions
- Chosen winner
- Actual outcomes
- Market conditions

Data is stored on Walrus for:
- Model retraining
- Strategy improvement
- Performance auditing

### Reinforcement Learning

AI models learn from outcomes:

**Positive Reinforcement**:
- Winning solutions that performed as promised
- Unexpected solver excellence
- Novel successful strategies

**Negative Reinforcement**:
- Solutions that underperformed
- Failed executions
- Inaccurate estimates

### Model Updates

Updated models are:
- Tested on historical data
- Validated in testnet environment
- Gradually rolled out
- Monitored for performance

## Fairness Guarantees

### Preventing Bias

**No Favoritism**:
- All solvers evaluated by same criteria
- Reputation earned through performance
- Stakes level playing field

**Transparent Weights**:
- Ranking factors publicly documented
- Weights adjusted through governance
- Changes announced in advance

**Verifiable Results**:
- TEE attestations prove correctness
- Anyone can audit rankings
- Disputes resolved with cryptographic evidence

### Anti-Gaming Measures

**Sybil Resistance**:
- Stake requirements limit fake identities
- Reputation doesn't transfer between addresses
- Economic cost to create multiple solvers

**Collusion Detection**:
- Statistical analysis of submission patterns
- Correlated behavior flagged
- Coordinated solutions penalized

**Quality Standards**:
- Minimum performance thresholds
- Automatic disqualification for violations
- Regular performance reviews

## Performance Metrics

### User Outcomes

The engine's effectiveness is measured by:
- **Average Surplus**: How much better than direct execution
- **Execution Success Rate**: Percentage of completed intents
- **User Satisfaction**: Repeat usage patterns
- **Cost Savings**: Gas + price improvements

### Solver Distribution

Healthy competition indicators:
- No single solver wins >30% of intents
- New solvers can compete effectively
- Innovation is rewarded
- Multiple viable strategies exist

## Technical Architecture

### Components

**Intent Classifier**:
- ML model trained on historical intents
- Determines optimal ranking strategy
- Runs inside TEE

**Score Calculator**:
- Implements ranking formulas
- Aggregates multi-dimensional data
- Produces final scores

**Proof Generator**:
- Creates cryptographic attestation
- Packages ranking results
- Enables verification

**Data Archiver**:
- Stores results on Walrus
- Feeds continuous learning
- Enables auditing

## Future Enhancements

Planned improvements:

**Personalized Rankings**:
- Learn individual user preferences
- Adapt to trading patterns
- Optimize for specific goals

**Predictive Analysis**:
- Forecast market movements
- Optimize execution timing
- Anticipate liquidity changes

**Cross-Chain Intelligence**:
- Coordinate multi-chain strategies
- Optimize bridge selection
- Minimize total cost

## Learn More

- [Universal Solvers Network](universal-solvers-network.md)
- [Solution Specifications](solutions.md)
- [Technical Details](../technical-documentation/ai-powered-ranking.md)
