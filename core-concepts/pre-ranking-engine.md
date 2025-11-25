---
icon: filter
---

# Pre-ranking Engine

## The First Line of Defense

The **Pre-ranking Engine** is a validation layer that filters and validates solver solutions before they reach the AI-powered ranking engine. It ensures only high-quality, compliant solutions consume computational resources for full evaluation.

## Why Pre-ranking?

Without pre-filtering:

* ❌ Low-quality solutions waste ranking resources
* ❌ Invalid solutions delay processing
* ❌ Malicious submissions can spam the system
* ❌ Every solution costs gas/compute to evaluate

With pre-ranking:

* ✅ Only valid solutions reach full ranking
* ✅ Faster processing for quality solvers
* ✅ Economic spam prevention
* ✅ Efficient resource utilization

## Validation Pipeline

{% stepper %}
{% step %}
#### 1. Schema Validation

First check: Does the solution follow IGS standards?

**Validated Fields**:

* Solution ID format
* Intent ID reference
* Solver address format
* Execution plan structure
* Expected outcomes format
* Cryptographic signatures

**Result**: Malformed solutions rejected immediately
{% endstep %}

{% step %}
#### 2. Authorization Check

Second check: Is the solver authorized?

**Requirements**:

* Solver must be registered on-chain
* Minimum stake requirement met
* Not currently suspended
* Has decryption access to the intent

**Result**: Unauthorized submissions rejected
{% endstep %}

{% step %}
#### 3. Economic Feasibility

Third check: Is the solution economically sensible?

**Validation**:

```
if (gas_cost > expected_output_value):
    reject("Unprofitable for user")

if (output_amount < intent.min_output):
    reject("Doesn't meet minimum requirements")

if (slippage > intent.max_slippage):
    reject("Exceeds slippage tolerance")
```

**Result**: Economically invalid solutions filtered out
{% endstep %}

{% step %}
#### 4. Simulation Check

Fourth check: Can the solution actually execute?

**Process**:

* Simulate execution on current chain state
* Verify all protocol calls succeed
* Confirm expected outcomes achievable
* Check for execution errors

**Result**: Non-executable solutions rejected
{% endstep %}

{% step %}
#### 5. Freshness Validation

Fifth check: Is market data recent?

**Requirements**:

* Price data must be < 30 seconds old
* Liquidity snapshots must be current
* Gas estimates must reflect current network

**Result**: Stale solutions rejected
{% endstep %}
{% endstepper %}

## Filtering Criteria

### Must-Pass Validations

Solutions must satisfy ALL criteria:

| Validation            | Criteria                 | Rejection Rate |
| --------------------- | ------------------------ | -------------- |
| Schema Compliance     | Valid IGS format         | \~5%           |
| Authorization         | Registered + staked      | \~2%           |
| Economic Viability    | Profitable + constraints | \~15%          |
| Execution Feasibility | Simulation succeeds      | \~10%          |
| Data Freshness        | < 30s old                | \~3%           |

**Typical Survival Rate**: 65-70% of submitted solutions pass pre-ranking.

### Optional Quality Signals

Additional factors that improve ranking odds:

✨ **High Solver Reputation**: Previous performance > 8.0/10 ✨ **Competitive Output**: > 5% better than benchmark ✨ **Low Gas Cost**: < median gas for similar intents ✨ **Fast Execution**: Expected time < intent deadline ✨ **Novel Strategy**: Unused approach in last 100 similar intents

## Performance Optimization

### Quick Rejections

Pre-ranking processes validations in order of cost:

1. **Schema check** (cheapest): Invalid format rejected in < 10ms
2. **Auth check** (cheap): Database lookup, rejects in < 50ms
3. **Economic check** (moderate): Basic math, rejects in < 100ms
4. **Simulation** (expensive): Full execution test, takes 500-2000ms
5. **AI Ranking** (most expensive): Only for passed solutions

**Result**: 95% of invalid solutions caught before expensive operations.

### Batching Strategy

Pre-ranking processes solutions in parallel:

```
Time Window: 30-60 seconds

Parallel Processing:
├── Batch 1: Solutions 1-10 (validated simultaneously)
├── Batch 2: Solutions 11-20
└── Batch N: Final solutions

Passed solutions → AI Ranking Engine
```

## Spam Prevention

### Economic Barriers

**Submission Requirements**:

* Minimum stake: 10,000 SUI
* Per-submission gas fee: 0.001 SUI
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

## Intent-Specific Validation

Different intent types have specialized checks:

### For Swap Intents

```typescript
validate_swap(solution) {
  // Output must exceed minimum
  if (solution.output < intent.min_output)
    return reject();

  // Slippage within bounds
  if (calculate_slippage() > intent.max_slippage)
    return reject();

  // Route must exist
  if (!can_execute_route(solution.path))
    return reject();

  return pass();
}
```

### For Limit Orders

```typescript
validate_limit_order(solution) {
  // Price must meet target
  if (solution.execution_price != intent.target_price)
    return reject();

  // Monitoring mechanism must be reliable
  if (solution.monitor_strategy.reliability < 0.95)
    return reject();

  return pass();
}
```

### For Lending Intents

```typescript
validate_lending(solution) {
  // APY must meet minimum
  if (solution.apy < intent.min_apy)
    return reject();

  // Protocol must be whitelisted
  if (!is_approved_protocol(solution.protocol))
    return reject();

  // Liquidity must be sufficient
  if (protocol.available_liquidity < intent.amount)
    return reject();

  return pass();
}
```

## Metrics and Monitoring

### Pre-ranking Performance

Key metrics tracked:

**Throughput**:

* Solutions processed per second
* Average validation time
* Bottleneck identification

**Quality**:

* Rejection rate by validation stage
* False positive rate (rejected but should pass)
* False negative rate (passed but should reject)

**Efficiency**:

* Compute cost per solution
* Resource utilization
* Cost savings vs. no pre-ranking

### Continuous Improvement

**Data Collection**:

* Every validation decision logged
* Simulation results archived
* Rejection reasons catalogued

**Optimization**:

* Identify common rejection patterns
* Improve validation logic
* Add new sanity checks
* Remove redundant validations

## Integration with Ranking Engine

### Handoff Process

Pre-ranking passes filtered solutions with metadata:

```json
{
  "passed_solutions": [
    {
      "solution_id": "sol_abc123",
      "validation_score": 9.2,
      "checks_passed": [
        "schema", "auth", "economic",
        "simulation", "freshness"
      ],
      "quality_signals": {
        "high_reputation": true,
        "competitive_output": true,
        "low_gas": false
      },
      "simulation_results": {
        "estimated_output": "2495 USDC",
        "estimated_gas": "0.02 SUI",
        "success_probability": 0.98
      }
    }
  ]
}
```

### Priority Ordering

Solutions passed to ranking engine are pre-sorted by:

1. Validation score (more quality signals = higher)
2. Solver reputation
3. Economic competitiveness

**Benefit**: AI ranking can use fast-path for obviously superior solutions.

## Security Considerations

### Protection Against Attacks

**Simulation Attacks**:

* Solutions designed to pass simulation but fail execution
* **Mitigation**: Solver reputation + slashing for failures

**Resource Exhaustion**:

* Malicious solutions that consume excessive resources
* **Mitigation**: Timeouts, resource limits, rate limiting

**Data Freshness Attacks**:

* Using outdated data to game rankings
* **Mitigation**: Strict timestamp validation, on-chain verification

## Learn More

* [Full Ranking Engine](ranking-engine.md)
* [Solution Specifications](solutions.md)
* [Solver Network](universal-solvers-network.md)
