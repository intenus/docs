# FAQ

## General Questions

<details>

<summary><strong>What makes Intenus different from DEX aggregators like 1inch?</strong></summary>

Traditional DEX aggregators find the best route across known DEXs at the moment you trade. Intenus creates a competitive marketplace where multiple solvers bid to execute your trade, often finding better opportunities through:

* Peer-to-peer matching (like CoW Protocol)
* MEV capture and redistribution
* Predictive routing based on market conditions
* Multi-protocol strategies beyond simple swaps

Additionally, our AI-powered ranking evaluates solutions across multiple dimensions (not just price), and all intents are encrypted to prevent front-running.

</details>

<details>

<summary><strong>Is Intenus only for advanced traders?</strong></summary>

Not at all! Intenus is designed to be simpler than traditional DeFi. You express what you want in plain language, and the protocol handles all complexity. Advanced traders can leverage sophisticated features, but beginners benefit from optimal execution without needing to understand the mechanics.

</details>

<details>

<summary><strong>What tokens and chains does Intenus support?</strong></summary>

Intenus currently operates on Sui blockchain and supports all SPL tokens. Cross-chain bridging support is in development and will enable trading across multiple blockchains.

</details>

<details>

<summary><strong>How long does it take to execute a trade?</strong></summary>

Most intents execute within 30 seconds to 2 minutes:

* Solver discovery: 10-30 seconds
* AI ranking: 5-15 seconds
* On-chain execution: 5-30 seconds

Time-sensitive intents can prioritize speed over marginal price improvements.

</details>

## Trading Questions

<details>

<summary><strong>What fees does Intenus charge?</strong></summary>

Fee structure:

* **Protocol Fee**: 0.1-0.3% of trade value (competitive with DEXs)
* **Solver Fee**: Varies by solution quality (typically 0.05-0.15%)
* **Gas Fees**: Standard Sui network fees (usually <$0.01)

Total fees are typically lower than manually trading across multiple protocols, and you get better execution.

</details>

<details>

<summary><strong>Can I cancel an intent after submitting?</strong></summary>

Yes, intents can be cancelled anytime before execution begins. Once the winning solution starts executing, cancellation is not possible (to prevent manipulation).

</details>

<details>

<summary><strong>What happens if no solver submits a solution?</strong></summary>

If no solutions are submitted within the intent deadline:

1. Intent automatically expires
2. No fees are charged
3. Your assets remain in your wallet
4. You can submit a new intent with adjusted parameters

</details>

<details>

<summary><strong>How do I know I'm getting the best price?</strong></summary>

Transparency features:

* View all submitted solutions before execution
* Compare against real-time DEX prices
* See historical execution quality
* Access detailed execution reports post-trade

</details>

<details>

<summary><strong>What if the solver's solution doesn't execute as promised?</strong></summary>

Multiple protections:

1. **Simulations**: All solutions are simulated before selection
2. **Commitments**: Solvers stake capital and sign commitments
3. **Verification**: Actual outcomes must match promises
4. **Slashing**: Poor performance results in reputation loss and stake slashing
5. **Compensation**: In case of solver misbehavior, you're protected by their staked capital

</details>

## Security Questions

<details>

<summary><strong>How secure is Intenus?</strong></summary>

Security is multi-layered:

* **Smart Contract Security**: Audited by leading security firms
* **TEE Security**: AI ranking in hardware-secured environments
* **Economic Security**: Solver staking and slashing mechanisms
* **Cryptographic Security**: Intent encryption via Seal protocol
* **Continuous Monitoring**: Real-time anomaly detection

</details>

<details>

<summary><strong>Can solvers see my trading intentions?</strong></summary>

No. Your intents are encrypted and only qualified solvers with proper credentials can decrypt them during limited auction windows. Intent details are never publicly visible.

</details>

<details>

<summary><strong>Is my wallet at risk?</strong></summary>

Your wallet security is maintained:

* You approve each transaction
* Funds never leave your custody until execution
* No unlimited token approvals required
* Smart contracts cannot access funds beyond approved intents

</details>

<details>

<summary><strong>How is front-running prevented?</strong></summary>

Multiple mechanisms:

* Intent encryption hides trade details
* Batch execution prevents order manipulation
* Time-bounded solver access
* MEV protection built into ranking algorithm
* Sealed-bid auction structure

</details>

## Solver Questions

<details>

<summary><strong>How much capital do I need to become a solver?</strong></summary>

Minimum requirements:

* **Stake**: 10,000 SUI (adjustable by governance)
* **Infrastructure**: Server for running solver logic
* **Liquidity Access**: Ability to execute across protocols

Higher stakes provide competitive advantages in rankings.

</details>

<details>

<summary><strong>How do solvers make money?</strong></summary>

Revenue streams:

* **Execution Fees**: 70% of protocol fees for winning solutions
* **Performance Bonuses**: Extra rewards for consistent quality
* **MEV Capture**: Keep value extracted through optimal routing
* **Reputation Value**: Higher visibility leads to more wins

</details>

<details>

<summary><strong>What happens if my solution fails to execute?</strong></summary>

Consequences depend on failure type:

* **Technical Failure** (network issues): Minimal reputation impact
* **Simulation Error**: Moderate reputation penalty
* **Malicious Behavior**: Severe slashing and potential ban
* **Repeated Failures**: Automatic disqualification

</details>

<details>

<summary><strong>Can I run multiple solver strategies?</strong></summary>

Yes! You can:

* Register multiple solver addresses
* Run different algorithms simultaneously
* Specialize in different intent types
* Compete with yourself to find best strategies

</details>

## Technical Questions

<details>

<summary><strong>What is IGS and why does it matter?</strong></summary>

IGS (Intenus General Standard) is a unified schema for representing intents and solutions. It matters because:

* Enables solver interoperability
* Allows protocol extensions without breaking changes
* Ensures verifiable execution
* Facilitates AI model training

</details>

<details>

<summary><strong>How does the AI ranking work?</strong></summary>

The process:

1. Intent classification determines optimal ranking strategy
2. Solutions evaluated across multiple dimensions
3. Reinforcement learning model combines scores
4. Ranking computed in TEE for verifiability
5. Continuous learning from execution outcomes

All ranking logic is auditable and reproducible.

</details>

<details>

<summary><strong>What is a Trusted Execution Environment (TEE)?</strong></summary>

A TEE is a secure area within a processor that:

* Isolates computation from external access
* Provides cryptographic attestation of correct execution
* Protects confidentiality of processed data
* Enables verifiable off-chain computation

Intenus uses Nautilus TEE infrastructure on Sui.

</details>

<details>

<summary><strong>Can I verify the AI ranking was done correctly?</strong></summary>

Yes! Every ranking includes:

* **Attestation Proof**: Cryptographic verification
* **Input Hash**: Verifiable reference to solutions
* **Reproducibility**: Same inputs = same output
* **Audit Trail**: Complete ranking history on Walrus

</details>

<details>

<summary><strong>What happens to my data?</strong></summary>

Data flow:

* **Encrypted Intents**: Stored on Walrus, encrypted via Seal
* **Solutions**: Temporarily stored, winning solution archived
* **Execution History**: Public record (anonymized)
* **Training Data**: Aggregated and anonymized for AI improvement

You control privacy settings for your intents.

</details>

## Economic Questions

<details>

<summary><strong>How are fees distributed?</strong></summary>

Fee breakdown:

* 70% to winning solver
* 20% to protocol treasury (development, security)
* 10% to TEE infrastructure providers

Users pay similar or lower total fees than traditional DeFi.

</details>

<details>

<summary><strong>What incentivizes solvers to compete fairly?</strong></summary>

Economic alignment:

* Stake at risk for misbehavior
* Reputation affects future earnings
* Long-term value of honest participation
* Slashing penalties for malicious acts
* Competitive marketplace dynamics

</details>
