---
icon: lock
---

# Privacy & Security

## Multi-Layer Security

**Privacy Protection**

* **Encrypted Intents**: Your trading plans are hidden from front-runners
* **Time-Bounded Access**: Solvers can only view intents during active auction periods
* **Automatic Revocation**: Access permissions expire after execution

**Trusted Computation**

* **TEE Verification**: All AI ranking happens in hardware-secured environments
* **Attestation Proofs**: Cryptographic verification that computation was performed correctly
* **Reproducible Results**: Rankings can be independently verified

**Economic Security**

* **Solver Staking**: Solvers must stake capital to participate
* **Reputation System**: Historical performance tracking incentivizes honest behavior
* **Slashing Mechanisms**: Malicious solvers lose stake and reputation

***

## Risk Mitigation

**Front-Running Protection**

Traditional MEV attacks are prevented through:

* Intent encryption before submission
* Batch execution that prevents order manipulation
* Privacy-preserving solver access

**Slippage Control**

You maintain full control:

* Set maximum acceptable slippage
* Define price ranges for outputs
* Automatic transaction reversal if conditions aren't met

**Smart Contract Security**

* Modular architecture limits attack surface
* Formal verification of critical components
* Continuous security audits by leading firms

***

## Understanding Risks

While Intenus implements comprehensive security measures, users should understand:

**Smart Contract Risk**: As with all DeFi protocols, smart contract bugs could potentially lead to loss of funds.

**Market Risk**: Intenus optimizes execution but cannot eliminate inherent market volatility.

**Solver Risk**: While economic incentives and reputation systems discourage malicious behavior, the solver network operates in a competitive environment.

**Privacy Considerations**: While intent content is encrypted, some metadata (timing, participants) may be observable on-chain.
