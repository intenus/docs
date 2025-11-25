---
icon: message-minus
---

# Examples

### Example 1: Simple Swap

**Your Intent**: "I want to swap 1,000 SUI for USDC with minimum slippage"

**What Happens**:

1. Intent Agent creates a standardized swap intent
2. Solvers propose routes:
   * Solver A: Direct swap on Cetus (output: 2,480 USDC)
   * Solver B: Split route via Turbos + Aftermath (output: 2,495 USDC)
   * Solver C: P2P matching + DEX (output: 2,492 USDC)
3. AI ranks solutions considering output, reliability, and gas costs
4. Best solution (Solver B) is executed
5. You receive 2,495 USDC (15 USDC better than direct swap!)

***

### Example 2: Limit Order

**Your Intent**: "Buy 10,000 USDC worth of SUI when price reaches $2.30"

**What Happens**:

1. Limit order intent is created and encrypted
2. Solvers monitor market conditions
3. When SUI hits $2.30, solvers compete to fill your order
4. Best execution is triggered automatically
5. You receive approximately 4,348 SUI at your target price

***

### Example 3: Complex Strategy

**Your Intent**: "Swap 5,000 SUI for USDC and lend it at the best rate for 30 days"

**What Happens**:

1. Intent Agent breaks this into two linked operations
2. Swap solvers find optimal SUI→USDC conversion
3. Lending solvers identify highest-yield lending protocol
4. Both operations execute atomically in a single transaction
5. Your USDC is automatically deposited in the optimal lending pool
