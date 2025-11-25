# IGS Intents

## Intent Schema Reference

**IGS Intents** standardize how user trading goals are expressed, ensuring consistent interpretation across solvers, AI models, and smart contracts.

## Complete Intent Structure

```json
{
  "igs_version": "1.0.0",
  "intent_id": "int_xyz789",
  "intent_type": "swap.exact_input",
  "user_address": "0x...",
  "timestamp": 1699123456000,

  "operation": {
    "mode": "exact_input",
    "inputs": [{
      "asset_id": "0x2::sui::SUI",
      "amount": {"type": "exact", "value": "1000000000"}
    }],
    "outputs": [{
      "asset_id": "0x...::usdc::USDC",
      "amount": {"type": "range", "min": "950000", "max": "1000000"}
    }]
  },

  "constraints": {
    "max_slippage_bps": 50,
    "deadline_ms": 1699123456000,
    "max_gas_price": "1000",
    "allowed_protocols": ["Cetus", "Turbos"]
  },

  "privacy": {
    "encryption_required": true,
    "solver_access_window_ms": 300000,
    "min_solver_stake": "10000000000"
  },

  "signature": "0x..."
}
```

## Intent Types

### Swap Intents

**swap.exact_input**: Specify input, optimize output
**swap.exact_output**: Specify output, minimize input
**swap.range**: Flexible amounts within bounds

### Limit Order Intents

**limit.buy**: Execute buy at target price or better
**limit.sell**: Execute sell at target price or better
**limit.stop_loss**: Trigger sale below threshold
**limit.take_profit**: Trigger sale above threshold

### Lending Intents

**lend.deposit**: Lend assets for yield
**lend.borrow**: Borrow against collateral
**lend.repay**: Repay borrowed assets
**lend.optimize**: Automatically rebalance for best APY

### Bridge Intents

**bridge.transfer**: Move assets cross-chain
**bridge.optimized**: Optimize cost + speed

### Composite Intents

**composite.sequential**: Execute steps in order
**composite.conditional**: If-then logic
**composite.batch**: Parallel operations

## Learn More

- [IGS Core](igs-core.md) - Primitive types
- [Intents Concept](../intents.md) - High-level overview
