
# Intenus: Intent-Based DeFi Agent

| Key                                   | Value                                                                 |
|----------------------------------------|-----------------------------------------------------------------------|
| **AI Enclave Host**                    | <http://13.211.142.216:800dddd0/docs>                                      |
| **INTENUS_PACKAGE_ID**                 | `0x993c7635b44582e9c47c589c759239d3e1ce787811af5bfa0056aa253caa394a`   |
| **INTENUS_SOLVER_REGISTRY_ID**         | `0xf71c16414b66054dfe9ebca5f22f8076a8294715d5a3e4ae4b2b4e0cd5d7e64a`   |
| **INTENUS_SOLVER_REGISTRY_ADMIN_CAP**  | `0xaf69f4d0fa49c43bfa9bfe382467eacd33ead8e2bb36aeb6fcb8f1df36d60909`   |
| **INTENUS_SLASH_MANAGER_ID**           | `0x1d023609156241468439e933c094dba4982d35292b0dd21c66cf85cc8f53b283`   |
| **INTENUS_SLASH_MANAGER_ADMIN_CAP**    | `0xbe3b9146c100a38b106161c2d03e91432e8a608e1873ce1f894e576c63e70ea0`   |
| **INTENUS_TEE_VERIFIER_ID**            | `0xf0867b65374e34905b7737432e93d53722b08bc39cd621740b685a366272f857`   |
| **INTENUS_TEE_VERIFIER_ADMIN_CAP**     | `0x392ea4b56d73d59cb32e132fa7f610a7fb5f1e97d0983af6bfced645bea59e9f`   |
| **INTENUS_SEAL_ENCLAVE_CONFIG_ID**     | `0xe525e478d2448b4e895d744b31f9fa7cab599f6ce5c36b6b24dab2f9c54ad0fd`   |
| **INTENUS_TREASURY_ID**                | `0x1aa5d3878fac1e2b10bf471bd1cbef6868ca1d04643c24c3d3b358d762f34f53`   |
| **INTENUS_PACKAGE_UPGRADE_CAP**        | `0xa25adda6a6965df626313123b48c067a342c21127932b4c2f7ba83dcfb71c288`   |
| **INTENUS_PACKAGE_PUBLISHER**          | `0x01741371472c4a88b2a8670c72f4ad96285eb13ddfa51c1b8abe3a76dd128014`   |

| Resource      | Link                                      |
|---------------|-------------------------------------------|
| Pitch         | <https://pitch.intenus.xyz>                |
| Docs          | <https://docs.intenus.xyz>                 |
| Whitepaper    | <https://docs.intenus.xyz/resources/whitepaper>  |
| App           | <https://app.intenus.xyz>                  |

## Introduction

Intenus is a universal intent-based infrastructure empowered by AI agents that transform natural language into optimal on-chain execution. It unifies fragmented DeFi protocols into a single interface, allowing users to trade efficiently across the ecosystem simply by expressing their goals.

### Vision

Transform DeFi from a maze of protocols into a single, intelligent interface where users express intents and AI agents handle the complexity.

**Built on Sui** | Powered by **Walrus**, **Seal**, and **Nautilus**

---

## Problem Statement

Despite the rapid growth of Decentralized Finance (DeFi), the ecosystem remains inaccessible to the mass market and technically constrained by outdated architectural models.

### 1. Fragmented Liquidity & Interoperability Friction

DeFi liquidity is currently isolated across disparate protocols and blockchains.

- **Siloed Interactions:** Users are forced to manage multiple interfaces and understand unique operational logic for each protocol (e.g., separate platforms for Lending, Swapping, and Bridging).
- **Inefficient Composition:** Executing complex, multi-step strategies (e.g., "Swap A to B, then Bridge to C, then Deposit into D") requires manual, atomic coordination that is prone to failure and high gas costs.

### 2. Scope Limitations

Current intent-based solutions are restricted by domain specificity and lack of standardization.

- **Domain Specificity:** Major players like **CoW Protocol** focus predominantly on ERC-20 token swaps, leaving other primitives like lending, staking, and complex yield farming unsupported.
- **Lack of Expressivity:** Aggregators (e.g., 1inch) optimize for price but cannot interpret complex user conditions or conditional execution logic.
- **Implementation Gap:** Theoretical frameworks like **Anoma** offer powerful concepts but lack the concrete, user-facing infrastructure required for immediate application layer adoption.

### 3. The Complexity Barrier & Cognitive Overload

The cognitive load required to interact with DeFi remains prohibitively high.

- **Expertise Requirement:** Optimizing execution requires deep technical knowledge of gas markets, slippage, and routing, excluding average users from institutional-grade efficiency.
- **Operational Risks:** Manual execution exposes users to "fat-finger" errors, front-running (MEV), and emotional decision-making during market volatility.
- **Language Gap:** There is no bridge between *natural language* (how humans think) and *executable code* (how blockchains work).

### 4. The Verifiability Dilemma

DeFi faces a trade-off between smart execution and trustless verification.

- **On-Chain Limitations:** Verifying complex algorithms on-chain is transparent but computationally expensive and limited by block gas limits, making AI integration impossible.
- **Off-Chain Opacity:** Off-chain solvers can run sophisticated algorithms but operate as "black boxes," requiring users to trust centralized intermediaries without cryptographic proof of best execution.
- **The Missing Link:** There is currently no infrastructure that allows for **AI-driven ranking strategies** to be both computationally intensive (off-chain) and cryptographically verifiable (trustless).

---

## Solutions

### 1. Intent AI Agent

**The conversational gateway turning words into workflows.**

Acting as the intelligent front-end, the Agent utilizes **Natural Language Processing (NLP)** to interpret user goals and abstract away technical complexities. It automatically translates human conversation into valid **IGS Schemas**, allowing users to focus purely on outcomes rather than execution mechanics.

- **Natural Language Processing:** Users trade by simply chatting (e.g., *"Swap ETH to USDC, then bridge to Aptos"*).
- **Smart Abstraction:** Handles all underlying parameters (gas, routes, chain IDs), converting vague requests into precise, executable instructions.

### **2. Intenus General Standard - IGS Schema**

IGS serves as the universal protocol language, providing the rigorous schemas that allow **AI Agents, Solvers, and TEEs** to interoperate. It translates natural language into precise **Inputs, Outputs, and Constraints**, ensuring the entire network speaks a single, structured language for execution.

- **Dual Schema Architecture:** Explicitly defines **IGS Intent** (User goals) and **IGS Solution** (Solver execution paths) to ensure precise matching and verification.
- **AI-Native Framework:** Provides the foundational blueprints that empower AI Agents to structure, validate, and optimize complex workflows from vague commands.
- **Universal Composability:** Unifies all DeFi primitives (Swap, Lend, Bridge) into a single, extensible JSON structure that supports atomic multi-step strategies.

### **3. Universal Solver Network - USN**

USN is an open marketplace where independent solvers compete to fulfill user intents. By drawing from on-chain liquidity, P2P matching, or off-chain inventory, solvers craft optimized **IGS Solutions** that aim to outperform market benchmarks and deliver the most efficient execution.

- **Heterogeneous Strategies:** USN gives solvers full freedom to design their execution logic—ranging from DEX aggregation and CoW-style P2P matching to proprietary AI or hybrid strategies.
- **Open Competition:** A permissionless arena where solvers race to deliver the most profitable outcome, regardless of the method used.
- **Incentivized Integrity:** Staking and slashing enforce real “skin-in-the-game,” ensuring solvers stay aligned with execution quality and reliability.

### **4. Verifiable AI Ranking**

**The unbiased intelligence core for trusted optimization.**

Executed inside **Nautilus TEEs**, this engine uses Machine Learning to rank solutions based on dynamic market conditions and user constraints. It ensures every decision is mathematically optimal, bias-free, and cryptographically verifiable.

- **Adaptive Scoring:** Uses **Reinforcement Learning** to continuously improve ranking logic based on profit, gas, and reputation.
- **Two-Stage Evaluation:** Combines rigorous technical validation (dry-runs) with AI-based quality assessment.
- **Verifiable Integrity:** Generates cryptographic **Attestation Proofs** for every decision, guaranteeing merit-based selection without manipulation.

### **5. Programmable Privacy (The Shield)**

**Programmable protection where Users set the rules.**

Powered by **Seal**, this layer allows users to define exactly *who* can decrypt their intents (e.g., **Reputation > 80**, Min Stake) and *when*, effectively eliminating MEV and front-running.

- **Programmable Access:** Restricts decryption rights to only high-quality solvers based on user-defined scores or stakes.
- **MEV Immunity:** Encrypts sensitive trade details end-to-end, rendering the intent invisible to predatory bots.
- **Time-Bounded:** Grants strictly temporary access windows that auto-expire immediately after execution.

---

## Architecture

![image.png](attachment:b50a4c75-ec01-45d2-97dc-707f96caf17f:image.png)

---

## Why Walrus

**Solving the cost-scale dilemma for high-volume Intents and AI data.**

Intenus generates massive amounts of data—from complex **IGS Schemas** and Solution bytes to historical **AI Training Sets**. Walrus acts as the decentralized "hard drive," decoupling storage from execution to ensure the protocol scales exponentially without exploding gas costs.

- **90% Cost Reduction:** Offloads heavy intent data and solution payloads off-chain, making complex trading affordable.
- **AI Data Infrastructure:** Provides the persistent, low-cost storage required to house the massive datasets needed for continuous Agent training and Model optimization.

---

## Why Seal

**Solving the "Dark Forest" problem with programmable visibility.**

Standard encryption is binary (locked/unlocked), but Intenus requires *conditional* access. Seal allows us to program dynamic rules into the data itself, ensuring that privacy adapts to solver quality and market conditions to eliminate MEV.

- **MEV Immunization:** Conceals intent specifics during the solving phase, rendering front-running and sandwich attacks mathematically impossible.
- **Quality-Based Gating:** Automatically grants decryption rights *only* to solvers who meet specific **Stake** or **Reputation** thresholds, filtering out malicious actors.
- **Ephemeral Access:** Enforces time-bounded visibility windows that auto-revoke post-execution, preventing long-term data leakage.

---

## Why Nautilus

**Solving the paradox of verifiable off-chain Intelligence.**

Running complex AI Ranking on-chain is too expensive, but off-chain servers lack trust. Nautilus resolves this by securing our AI models inside **TEEs (Trusted Execution Environments)**, allowing Intenus to offer "Smart" ranking that is also "Provably Fair."

- **Verifiable AI Inference:** Enables heavy Machine Learning models to rank solutions off-chain while generating on-chain **Attestation Proofs** of integrity.
- **Blind Evaluation:** allows the engine to score encrypted solutions without ever revealing the Solvers' proprietary strategies (IP protection).
- **Tamper-Proof Execution:** Hardware-enforced security guarantees that ranking results are based purely on merit, not manipulation.

---

## Impact and Innovation

### **For Users**

- **75% reduction** in cognitive load
- Execute sophisticated strategies with simple intents
- **15-25% better outcomes** compared to direct protocol interaction

### **For DeFi Ecosystem**

- First universal intent standard
- Cross-protocol composability
- Innovation through solver competition

### **Technical Breakthroughs**

- IGS: Comprehensive DeFi intent schema
- USN: Heterogeneous solver marketplace
- First production TEE-based AI ranking for DeFi

---

## Vision and Roadmap

### **Short-term (3-6 months)**

- Launch mainnet with core DeFi operations
- Onboard 10+ specialized solvers
- Process 1000+ daily intents

### **Mid-term (6-12 months)**

- Cross-chain intent support
- Advanced ML models with federated learning
- Institutional-grade solver infrastructure

### **Long-term Vision**

- **The Intent Layer of DeFi**: Infrastructure integrated by every dApp
- **Universal DeFi Language**: IGS becomes the industry standard
- **AI-Native Finance**: Every transaction optimized by AI

---

## **Team**

### **Core Members**

#### Wyner — Tech Lead

- 3+ years in Software Development
- 1+ year in Blockchain
- 1+ year in Smart Contracts & DeFi

#### Ann — AI Developer

- 2+ years in AI Lab

#### Vanh — Backend Developer

- 3+ years in Software Development
- 1+ year in Blockchain

#### Hotcat — Researcher**

- 3+ years in Software Development
- 1+ year in Blockchain

#### Lee Duck — Backend Developer

- 3+ years in Software Development
- 1+ year in Blockchain

### **Achievements**

- **Winner – NFT Track**, *Move on Aptos Hackathon* (X404)
- **Winner – 4th DeFi Track**, *Sui Overflow 2025* (Kamo Finance)
- **Shortlist – Programmable Storage + Winner University Track**, *Sui Overflow 2025* (Chatiwal)
- **Winner – 3rd DEX/CEX Track**, *Viechain Talents Hackathon* (Vietnam Government) — Nolaswap
- **Winner – Hyperion DeFi Track**, *Ctrl Move Aptos Hackathon* (Firyx Protocol)
- **Winner – AI Track**, *UET-VNU Campathon* (Vietnam Public Service Chatbot Agent)
- **Winner – AI Track**, *UET FIT TechSpark* (Interview-Based Candidate Screening System)
