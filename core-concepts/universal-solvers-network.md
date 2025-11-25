---
icon: circle-nodes
---

# Universal Solvers Network

## What Makes It "Universal"?

The **Universal Solvers Network (USN)** is Intenus's decentralized marketplace where solvers compete to execute any type of DeFi operation—not just swaps, but lending, bridging, limit orders, and complex multi-step strategies.

**Traditional Systems**: Each protocol has its own solver network (CoW for swaps, 1inch for aggregation, etc.)

**Intenus USN**: One unified network handles ALL DeFi operations through standardized intent representations.

## Core Architecture

The USN operates on three foundational principles:

### 1. Open Participation

Anyone can become a solver by:

* Staking minimum collateral (economic security)
* Registering on-chain identity (accountability)
* Building expertise in specific operation types

### 2. Standardized Communication

All interactions use the **Intenus General Standard (IGS)**:

* Solvers read intents in consistent format
* Solutions follow predictable schemas
* AI ranking works across all intent types

### 3. Competitive Economics

Market dynamics ensure optimal performance:

* Multiple solvers compete for each intent
* Best solutions win execution rights
* Fees reward superior performance

## How Solvers Join the Network

{% stepper %}
{% step %}
#### Registration

Solver submits on-chain registration with:

* Minimum stake requirement (e.g., 10,000 SUI)
* Identity verification
* Supported intent types
{% endstep %}

{% step %}
#### Reputation Building

New solvers start with neutral reputation:

* First 10 successful executions build initial score
* Consistent performance increases visibility
* Stake multipliers provide competitive edge
{% endstep %}

{% step %}
#### Specialization

Solvers can focus on specific strategies:

* DEX aggregation specialists
* P2P matching experts
* Lending optimization algorithms
* Cross-chain bridge specialists
{% endstep %}
{% endstepper %}

## Solver Economics

### Fee Structure

When a solver's solution wins:

**90%** goes to the winning solver **10%** goes to protocol treasury

### Reputation Multipliers

Higher reputation = higher visibility in rankings:

| Reputation Tier      | Stake Multiplier | Visibility Boost |
| -------------------- | ---------------- | ---------------- |
| Novice (0-50)        | 1.0x             | Base             |
| Established (51-200) | 1.2x             | +20%             |
| Elite (201-500)      | 1.5x             | +50%             |
| Master (500+)        | 2.0x             | +100%            |

### Economic Incentives

**Why Solvers Participate**:

* **Profit**: Earn fees from successful executions
* **Volume**: Access to consistent intent flow
* **Efficiency**: Standardized intents reduce integration costs
* **Reputation**: Build portable performance history

## Solver Strategies

Different solvers employ diverse approaches:

### DEX Aggregation

Traditional AMM routing optimization:

```
Route: SUI → [60% Cetus, 40% Turbos] → USDC
Advantage: Deep liquidity access
Best for: Large trades, common pairs
```

### Peer-to-Peer Matching

Finding counterparties with opposite intents:

```
Alice wants: SUI → USDC
Bob wants: USDC → SUI
Solution: Direct settlement (zero slippage!)
Best for: High-volume pairs, matching intents
```

### Hybrid Execution

Combining multiple approaches:

```
1. Match 30% via P2P
2. Route 50% via primary DEX
3. Fill remaining 20% via secondary DEX
Best for: Complex intents, optimal pricing
```

### AI-Driven Optimization

Machine learning models that:

* Predict optimal execution timing
* Dynamically adjust routing based on market conditions
* Learn from historical performance patterns

## Quality Assurance

### Performance Monitoring

Every solution is tracked:

* **Promised vs. Actual**: Output amount accuracy
* **Gas Efficiency**: Actual vs. estimated costs
* **Execution Speed**: Time to completion
* **Success Rate**: Completion reliability

### Slashing Mechanisms

Solvers face penalties for:

| Violation           | Penalty          | Recovery                 |
| ------------------- | ---------------- | ------------------------ |
| Failed execution    | -5% stake        | 30 days good performance |
| Incorrect estimates | -2% stake        | 10 successful executions |
| MEV extraction      | -20% stake       | Review by governance     |
| Repeated failures   | Disqualification | Reapplication required   |

### Appeals Process

Solvers can contest penalties:

* 24-hour challenge window
* TEE attestation provides evidence
* Governance resolves disputes
* Wrongful penalties are reversed with compensation

## Network Benefits

### For Users

✅ **Best Execution**: Competition ensures optimal outcomes ✅ **Coverage**: Support for all DeFi operations ✅ **Innovation**: Continuous solver strategy improvements ✅ **Reliability**: Economic stakes align incentives

### For Solvers

✅ **Open Market**: Permissionless participation ✅ **Fair Competition**: Verifiable, unbiased ranking ✅ **Portable Reputation**: Performance history follows solver ✅ **Diverse Revenue**: Multiple intent types = more opportunities

### For The Ecosystem

✅ **Composability**: New protocols automatically integrated ✅ **Efficiency**: Reduced liquidity fragmentation ✅ **Security**: Distributed trust model ✅ **Innovation**: Open experimentation with strategies

## Solver Infrastructure

### Required Components

To operate as a solver, you need:

**On-Chain**:

* Registered solver address
* Staked collateral
* Solution submission capabilities

**Off-Chain**:

* Intent monitoring service
* Market data feeds (prices, liquidity)
* Strategy computation engine
* Simulation environment

**Integration**:

* Protocol adapters (Cetus, Turbos, etc.)
* IGS schema validator
* Seal encryption/decryption
* Walrus storage access

## Becoming a Solver

Ready to join the network?

1. **Review Technical Specs**: [Integration Guide](../technical-documentation/integration-guide.md)
2. **Understand IGS**: [Intenus General Standard](intenus-general-standard/)
3. **Check Requirements**: Minimum stake, infrastructure needs
4. **Join Community**: Connect with other solvers
5. **Start Testing**: Testnet environment available

## Learn More

* [Solution Specifications](solutions.md)
* [AI-Powered Ranking](ranking-engine.md)
* [Technical Integration](../technical-documentation/solver-network.md)
