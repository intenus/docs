---
icon: lock
---

# Privacy Protection

## Why Privacy Matters in DeFi

Public blockchains are transparent by design, but this creates problems for traders:

* **Front-Running**: Bots spot pending transactions and exploit them
* **Sandwich Attacks**: Attackers place trades before and after yours
* **Strategy Leakage**: Your trading patterns become publicly analyzable
* **Competitive Disadvantage**: Large trades reveal your position to the market

## Intenus Privacy Architecture

### **Layer 1: Intent Encryption (Seal)**

When you submit an intent:

1. Content is encrypted using Seal's programmable access control
2. Only qualified solvers with proper credentials can decrypt
3. Access is time-bounded and automatically revoked
4. Encryption keys are managed by smart contracts

**What's Protected**:

* Trade size and direction
* Slippage constraints
* Timing preferences
* Any custom parameters

**What's Visible**:

* Intent exists (but not details)
* General category (swap, lend, etc.)
* Execution status

### **Layer 2: Solver Access Control**

Strict policies govern who can view your intent:

**Qualification Requirements**:

* Minimum stake amount
* Positive reputation score
* Registration verification
* Policy compliance

**Access Windows**:

* Limited time to view intents
* Automatic expiration after deadline
* No pre-auction access

### **Layer 3: Solution Privacy**

During the competition phase:

* Solver solutions remain encrypted
* Other solvers can't see competing strategies
* AI ranking happens in isolated TEE environment
* Only winning solution is eventually revealed

### **Layer 4: Execution Privacy**

Even during execution:

* Transaction origin is obfuscated
* Intent batching prevents correlation
* On-chain traces minimize information leakage

## User Privacy Controls

You have granular control over privacy settings:

**Basic Privacy** (Default):

* Encrypted intent content
* Standard solver access rules
* Public execution results

**Enhanced Privacy**:

* Restricted solver whitelist
* Delayed public reporting
* Minimal metadata exposure

**Maximum Privacy**:

* Private solver selection
* No public execution history
* Premium privacy features

## Privacy vs. Efficiency Trade-offs

Higher privacy can impact execution:

* **Fewer Solvers**: Limited access may reduce competition
* **Discovery Time**: Privacy measures may add slight delays
* **Fee Premium**: Enhanced privacy features may cost more

Intenus provides transparent controls so you can balance privacy and optimization based on your specific needs.



