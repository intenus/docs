---
icon: thought-bubble
---

# Intents

## What is an Intent?

An **intent** is a declaration of what you want to achieve, not how to achieve it.

**Traditional Approach (How)**: "Execute a swap of 1,000 SUI for USDC on Cetus DEX using the SUI/USDC pool at 0.3% fee tier".\
**Intent Approach (What)**: "I want to convert 1,000 SUI into USDC".

The "how" is left to competing solvers who find the optimal execution path.

## Benefits of Intent-Based Trading

**1. Simplicity**

You don't need to:

* Know which DEX has the best price
* Understand liquidity pool mechanics
* Calculate optimal routing paths
* Manually compare gas costs

**2. Better Execution**

Solvers compete to give you the best deal, considering factors you might miss:

* Hidden liquidity sources
* Gas cost optimization
* MEV protection strategies
* Multi-protocol routing

**3. Future-Proof**

As new protocols launch, solvers automatically incorporate them into their strategies without requiring you to learn new interfaces.

## Intent Parameters

When creating an intent, you can specify:

**Required Parameters**:

* What asset you're starting with (input)
* What asset you want to receive (output)
* The amount you're trading

**Optional Constraints**:

* Maximum slippage tolerance
* Deadline for execution
* Minimum output amount
* Maximum gas price
* Preferred protocols or exclusions

**Privacy Settings**:

* Who can view your intent
* How long it remains visible
* Whether to reveal intent size
