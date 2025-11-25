---
description: Intent Schema
---

# IGS Intents

## Intent Schema Reference

**IGS Intents** standardize how user trading goals are expressed, ensuring consistent interpretation across solvers, AI models, and smart contracts.

[https://json-schema.org/draft-07/schema#](https://json-schema.org/draft-07/schema)

### Schema Overview

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>igs_version</code></td><td><code>string</code></td><td>true</td><td>IGS version (constant: "1.0.0")</td></tr><tr><td><code>object</code></td><td><code>IGSObject</code></td><td>true</td><td>On-chain Sui object reference</td></tr><tr><td><code>user_address</code></td><td><code>string</code></td><td>true</td><td>User address (pattern: <code>^0x[a-fA-F0-9]{1,64}$</code>)</td></tr><tr><td><code>intent_type</code></td><td><code>string</code></td><td>true</td><td>Intent type (see <a href="https://claude.ai/chat/b84db470-b129-4639-8f28-b94abc2c2ac3#intent-types">Intent Types</a>)</td></tr><tr><td><code>operation</code></td><td><code>IGSOperation</code></td><td>true</td><td>Operation specification</td></tr><tr><td><code>description</code></td><td><code>string</code></td><td>true</td><td>Human-readable description (1-500 chars)</td></tr><tr><td><code>constraints</code></td><td><code>IGSConstraints</code></td><td>false</td><td>Execution constraints</td></tr><tr><td><code>preferences</code></td><td><code>IGSPreferences</code></td><td>false</td><td>User preferences</td></tr><tr><td><code>metadata</code></td><td><code>IGSMetadata</code></td><td>false</td><td>Additional metadata</td></tr></tbody></table>

### Intent Types

| Value               | Description              | Use Case                                   |
| ------------------- | ------------------------ | ------------------------------------------ |
| `swap.exact_input`  | Exact input amount swap  | "Swap exactly 100 SUI for USDC"            |
| `swap.exact_output` | Exact output amount swap | "Get exactly 100 USDC by selling SUI"      |
| `limit.sell`        | Sell limit order         | "Sell 100 SUI when price ≥ $2.50"          |
| `limit.buy`         | Buy limit order          | "Buy SUI with 100 USDC when price ≤ $2.00" |

### IGSObject Structure

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>user_address</code></td><td><code>string</code></td><td>true</td><td>Sui object owner address</td></tr><tr><td><code>created_ts</code></td><td><code>number</code></td><td>true</td><td>Creation timestamp (milliseconds)</td></tr><tr><td><code>policy</code></td><td><code>object</code></td><td>true</td><td>Access control policy</td></tr></tbody></table>

#### Policy Object

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>solver_access_window</code></td><td><code>object</code></td><td>true</td><td>Time window for solver access</td></tr><tr><td><code>auto_revoke_time</code></td><td><code>number</code></td><td>true</td><td>Automatic access revocation time</td></tr><tr><td><code>access_condition</code></td><td><code>object</code></td><td>true</td><td>Solver access conditions</td></tr></tbody></table>

**Solver Access Window**

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>start_ms</code></td><td><code>number</code></td><td>true</td><td>Window start time (milliseconds)</td></tr><tr><td><code>end_ms</code></td><td><code>number</code></td><td>true</td><td>Window end time (milliseconds)</td></tr></tbody></table>

**Access Conditions**

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>requires_solver_registration</code></td><td><code>boolean</code></td><td>true</td><td>Must be registered solver</td></tr><tr><td><code>min_solver_stake</code></td><td><code>string</code></td><td>true</td><td>Minimum stake amount</td></tr><tr><td><code>requires_tee_attestation</code></td><td><code>boolean</code></td><td>true</td><td>Requires TEE attestation</td></tr><tr><td><code>min_solver_reputation_score</code></td><td><code>number</code></td><td>true</td><td>Minimum reputation (0-100)</td></tr></tbody></table>

### IGSOperation Structure

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>mode</code></td><td><code>string</code></td><td>true</td><td>Operation mode</td></tr><tr><td><code>inputs</code></td><td><code>array</code></td><td>true</td><td>Input assets (1-10 items)</td></tr><tr><td><code>outputs</code></td><td><code>array</code></td><td>true</td><td>Output assets (1-10 items)</td></tr><tr><td><code>expected_outcome</code></td><td><code>IGSExpectedOutcome</code></td><td>false</td><td>Expected execution outcome</td></tr></tbody></table>

#### Operation Modes

| Mode           | Description                          |
| -------------- | ------------------------------------ |
| `exact_input`  | Specify exact input amount           |
| `exact_output` | Specify exact output amount          |
| `limit_order`  | Conditional execution based on price |

### IGSAssetFlow Structure

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>asset_id</code></td><td><code>string</code></td><td>true</td><td>Asset identifier</td></tr><tr><td><code>asset_info</code></td><td><code>object</code></td><td>false</td><td>Additional asset information</td></tr><tr><td><code>amount</code></td><td><code>IGSAmount</code></td><td>true</td><td>Amount specification</td></tr></tbody></table>

#### Asset ID Format

| Format                            | Example         | Description        |
| --------------------------------- | --------------- | ------------------ |
| `0x{address}::{module}::{struct}` | `0x2::sui::SUI` | Sui Move type      |
| `native`                          | `native`        | Native chain token |

#### Asset Info Object

| Property   | Type     | Description                        |
| ---------- | -------- | ---------------------------------- |
| `symbol`   | `string` | Token symbol (e.g., "SUI", "USDC") |
| `decimals` | `number` | Decimal places (0-18)              |
| `name`     | `string` | Full token name                    |

### IGSAmount Structure

#### Exact Amount

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td><code>string</code></td><td>true</td><td>"exact"</td></tr><tr><td><code>value</code></td><td><code>string</code></td><td>true</td><td>Exact amount (integer string)</td></tr></tbody></table>

#### Range Amount

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td><code>string</code></td><td>true</td><td>"range"</td></tr><tr><td><code>min</code></td><td><code>string</code></td><td>true</td><td>Minimum amount</td></tr><tr><td><code>max</code></td><td><code>string</code></td><td>true</td><td>Maximum amount</td></tr></tbody></table>

#### All Amount

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td><code>string</code></td><td>true</td><td>"all" (use entire balance)</td></tr></tbody></table>

### IGSExpectedOutcome Structure

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>expected_outputs</code></td><td><code>array</code></td><td>true</td><td>Expected output amounts</td></tr><tr><td><code>expected_costs</code></td><td><code>object</code></td><td>false</td><td>Cost estimates</td></tr><tr><td><code>market_price</code></td><td><code>object</code></td><td>false</td><td>Current market price</td></tr></tbody></table>

#### Expected Outputs Item

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>asset_id</code></td><td><code>string</code></td><td>true</td><td>Asset identifier</td></tr><tr><td><code>amount</code></td><td><code>string</code></td><td>true</td><td>Expected amount</td></tr></tbody></table>

#### Expected Costs Object

| Property            | Type     | Description           |
| ------------------- | -------- | --------------------- |
| `gas_estimate`      | `string` | Estimated gas cost    |
| `protocol_fees`     | `string` | Protocol fee estimate |
| `slippage_estimate` | `string` | Expected slippage     |

#### Market Price Object

| Property      | Type     | Description              |
| ------------- | -------- | ------------------------ |
| `price`       | `string` | Current market price     |
| `price_asset` | `string` | Price denomination asset |

### IGSConstraints Structure

| Property           | Type     | Description                                |
| ------------------ | -------- | ------------------------------------------ |
| `max_slippage_bps` | `number` | Maximum slippage in basis points (0-10000) |
| `deadline_ms`      | `number` | Expiration timestamp                       |
| `max_inputs`       | `array`  | Maximum input amounts                      |
| `min_outputs`      | `array`  | Minimum output amounts                     |
| `max_gas_cost`     | `object` | Maximum gas cost limit                     |
| `routing`          | `object` | Routing preferences                        |
| `limit_price`      | `object` | Limit price condition                      |

#### Max Inputs/Min Outputs Item

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>asset_id</code></td><td><code>string</code></td><td>true</td><td>Asset identifier</td></tr><tr><td><code>amount</code></td><td><code>string</code></td><td>true</td><td>Amount limit</td></tr></tbody></table>

#### Routing Object

| Property              | Type     | Description                 |
| --------------------- | -------- | --------------------------- |
| `max_hops`            | `number` | Maximum routing hops (1-10) |
| `blacklist_protocols` | `array`  | Forbidden protocols         |
| `whitelist_protocols` | `array`  | Allowed protocols only      |

#### Limit Price Object

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>price</code></td><td><code>string</code></td><td>true</td><td>Limit price value</td></tr><tr><td><code>comparison</code></td><td><code>string</code></td><td>true</td><td>"gte" or "lte"</td></tr><tr><td><code>price_asset</code></td><td><code>string</code></td><td>true</td><td>Price denomination asset</td></tr></tbody></table>

### IGSPreferences Structure

| Property            | Type     | Description                 | Default    |
| ------------------- | -------- | --------------------------- | ---------- |
| `optimization_goal` | `string` | Primary optimization target | "balanced" |
| `ranking_weights`   | `object` | Custom ranking weights      | See below  |
| `execution`         | `object` | Execution preferences       | See below  |
| `privacy`           | `object` | Privacy settings            | See below  |

#### Optimization Goals

| Value               | Description                |
| ------------------- | -------------------------- |
| `maximize_output`   | Prioritize highest output  |
| `minimize_gas`      | Prioritize lowest gas cost |
| `fastest_execution` | Prioritize speed           |
| `balanced`          | Balanced optimization      |

#### Ranking Weights

| Property                 | Type     | Default | Description                           |
| ------------------------ | -------- | ------- | ------------------------------------- |
| `surplus_weight`         | `number` | 60      | Weight for surplus generation (0-100) |
| `gas_cost_weight`        | `number` | 20      | Weight for gas optimization (0-100)   |
| `execution_speed_weight` | `number` | 10      | Weight for execution speed (0-100)    |
| `reputation_weight`      | `number` | 10      | Weight for solver reputation (0-100)  |

#### Execution Preferences

| Property     | Type     | Default          | Description                 |
| ------------ | -------- | ---------------- | --------------------------- |
| `mode`       | `string` | "best\_solution" | Execution mode              |
| `show_top_n` | `number` | 3                | Show top N solutions (1-10) |

#### Privacy Settings

| Property              | Type      | Default | Description         |
| --------------------- | --------- | ------- | ------------------- |
| `encrypt_intent`      | `boolean` | false   | Encrypt intent data |
| `anonymous_execution` | `boolean` | false   | Anonymous execution |

### IGSMetadata Structure

| Property         | Type     | Description             |
| ---------------- | -------- | ----------------------- |
| `original_input` | `object` | Original user input     |
| `client`         | `object` | Client application info |
| `warnings`       | `array`  | System warnings         |
| `clarifications` | `array`  | Intent clarifications   |
| `tags`           | `array`  | Classification tags     |

#### Original Input Object

| Property     | Type     | Description                          |
| ------------ | -------- | ------------------------------------ |
| `text`       | `string` | Original text input (max 1000 chars) |
| `language`   | `string` | Language code (2 letters)            |
| `confidence` | `number` | Parse confidence (0-1)               |

#### Client Object

| Property   | Type     | Description             |
| ---------- | -------- | ----------------------- |
| `name`     | `string` | Client application name |
| `version`  | `string` | Client version          |
| `platform` | `string` | Platform identifier     |

## Learn More

* [IGS Core](igs-core.md) - Primitive types
* [Intents Concept](../intents.md) - High-level overview

## References

{% file src="../../.gitbook/assets/igs-intent-schema.json" %}
