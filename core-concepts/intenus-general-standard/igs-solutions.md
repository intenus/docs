# IGS Solutions

## Solution Schema Reference

**IGS Solutions** define the standardized format for solver execution proposals, enabling deterministic validation and ranking.

## Complete Solution Structure

```json
{
  "igs_version": "1.0.0",
  "solution_id": "sol_abc123",
  "intent_id": "int_xyz789",
  "solver_address": "0x...",
  "timestamp": 1699123456000,

  "execution_plan": {
    "steps": [
      {
        "protocol": "Cetus",
        "protocol_address": "0x...",
        "action": "swap",
        "params": {
          "pool_id": "0x...",
          "amount_in": "600000000",
          "min_amount_out": "1480000"
        }
      },
      {
        "protocol": "Turbos",
        "protocol_address": "0x...",
        "action": "swap",
        "params": {
          "pool_id": "0x...",
          "amount_in": "400000000",
          "min_amount_out": "985000"
        }
      }
    ],
    "total_gas_estimate": "500000"
  },

  "expected_outcomes": {
    "output_amount": "2495000",
    "execution_time_ms": 5000,
    "slippage_bps": 30,
    "success_probability": 0.98
  },

  "solver_commitment": {
    "signature": "0x...",
    "stake_locked": "10000000000",
    "guarantee_output": "2465000",
    "penalty_amount": "500000000"
  }
}
```

## Key Components

### Execution Plan

Step-by-step instructions for on-chain execution:
- **Protocol**: Which DeFi protocol to use
- **Action**: Specific operation (swap, lend, etc.)
- **Params**: Operation-specific parameters

### Expected Outcomes

Quantifiable performance metrics:
- **Output Amount**: Expected user receipt
- **Execution Time**: Completion estimate
- **Slippage**: Price impact prediction
- **Success Probability**: Likelihood of completion

### Solver Commitment

Economic guarantees binding the solver:
- **Signature**: Cryptographic proof
- **Stake Locked**: Collateral at risk
- **Guarantee Output**: Minimum promised amount
- **Penalty Amount**: Slashing if underperforms

## Validation Requirements

All solutions must:
- ✅ Reference a valid intent_id
- ✅ Come from registered solver
- ✅ Include valid execution plan
- ✅ Provide realistic outcome estimates
- ✅ Include cryptographic signature

## Learn More

- [IGS Core](igs-core.md) - Primitive types
- [Solutions Concept](../solutions.md) - High-level overview
- [Pre-ranking Engine](../pre-ranking-engine.md) - Validation process
