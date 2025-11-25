---
description: IGS Schema
icon: brackets-curly
---

# Intenus General Standard

## Purpose

The **Intenus General Standard (IGS)** is a comprehensive schema that standardizes how intents, solutions, and execution data are represented across the entire protocol. Think of it as a universal language that all system components understand.

#### Why Standardization Matters

**Interoperability**: Different solvers, AI models, and smart contracts can seamlessly communicate

**Extensibility**: New intent types can be added without breaking existing functionality

**Verifiability**: Standardized formats enable deterministic verification of solutions

**Clarity**: Unambiguous representation prevents misinterpretation

## IGS Structure

The IGS framework consists of three layers:

### **1. Core Primitives**

Foundational data types used throughout the protocol:

```json
{
  "SuiAddress": "0x...",
  "TokenAmount": "1000000000",
  "Timestamp": 1699123456000,
  "Signature": "0x..."
}
```

**Purpose**: Eliminates ambiguity in basic data representation **Examples**: Addresses, amounts, time values, signatures

### **2. Intent Specification**

Structured representation of user trading goals:

```json
{
  "igs_version": "1.0.0",
  "intent_type": "swap.exact_input",
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
    "deadline_ms": 1699123456000
  },
  "privacy": {
    "encryption_required": true,
    "solver_access_window_ms": 300000
  }
}
```

**Key Features**:

* Flexible amount types (exact, range, percentage)
* Comprehensive constraint system
* Privacy policy integration
* Support for complex multi-asset operations

### **3. Solution Specification**

Standardized format for solver proposals:

```json
{
  "solution_id": "sol_abc123",
  "intent_id": "int_xyz789",
  "solver_address": "0x...",
  "execution_plan": {
    "steps": [
      {
        "protocol": "Cetus",
        "action": "swap",
        "params": {...}
      }
    ],
    "total_gas_estimate": "500000"
  },
  "expected_outcomes": {
    "output_amount": "995000",
    "execution_time_ms": 5000,
    "slippage_bps": 30
  },
  "solver_commitment": {
    "signature": "0x...",
    "stake_locked": "10000000000"
  }
}
```

### Supported Intent Types

#### **Swap Intents**

* **exact\_input**: Specify input amount, optimize output
* **exact\_output**: Specify output amount, minimize input
* **range\_swap**: Flexible amounts within ranges

#### **Limit Order Intents**

* **limit\_buy**: Execute purchase at target price
* **limit\_sell**: Execute sale at target price
* **stop\_loss**: Trigger sale below threshold
* **take\_profit**: Trigger sale above threshold

#### **Lending Intents**

* **lend**: Deposit assets for yield
* **borrow**: Take loans against collateral
* **repay**: Pay back borrowed assets
* **optimize\_yield**: Automatically rebalance

#### **Bridge Intents**

* **cross\_chain\_transfer**: Move assets between chains
* **liquidity\_bridge**: Optimized cross-chain liquidity

#### **Composite Intents**

* **multi\_step**: Sequential operations
* **conditional**: If-then logic
* **batch**: Multiple parallel operations

#### Version Management

IGS uses semantic versioning:

* **Major**: Breaking changes to schema structure
* **Minor**: Backward-compatible additions
* **Patch**: Bug fixes and clarifications

Current version: **1.0.0**
