---
description: Intent Schema
---

# IGS Intents

## Intent Schema Reference

**IGS Intents** standardize how user trading goals are expressed, ensuring consistent interpretation across solvers, AI models, and smart contracts.

[https://json-schema.org/draft-07/schema#](https://json-schema.org/draft-07/schema)

### Schema Overview

| Property       | Type             | Required                        | Description                                                                                                |
| -------------- | ---------------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `igs_version`  | `string`         | <i class="fa-check">:check:</i> | IGS version (constant: "1.0.0")                                                                            |
| `object`       | `IGSObject`      | <i class="fa-check">:check:</i> | On-chain Sui object reference                                                                              |
| `user_address` | `string`         | <i class="fa-check">:check:</i> | User address (pattern: `^0x[a-fA-F0-9]{1,64}$`)                                                            |
| `intent_type`  | `string`         | <i class="fa-check">:check:</i> | Intent type (see [Intent Types](https://claude.ai/chat/b84db470-b129-4639-8f28-b94abc2c2ac3#intent-types)) |
| `operation`    | `IGSOperation`   | <i class="fa-check">:check:</i> | Operation specification                                                                                    |
| `description`  | `string`         |                                 | Human-readable description (1-500 chars)                                                                   |
| `constraints`  | `IGSConstraints` |                                 | Execution constraints                                                                                      |
| `preferences`  | `IGSPreferences` |                                 | User preferences                                                                                           |
| `metadata`     | `IGSMetadata`    |                                 | Additional metadata                                                                                        |

### Intent Types

| Value               | Description              | Use Case                                   |
| ------------------- | ------------------------ | ------------------------------------------ |
| `swap.exact_input`  | Exact input amount swap  | "Swap exactly 100 SUI for USDC"            |
| `swap.exact_output` | Exact output amount swap | "Get exactly 100 USDC by selling SUI"      |
| `limit.sell`        | Sell limit order         | "Sell 100 SUI when price ≥ $2.50"          |
| `limit.buy`         | Buy limit order          | "Buy SUI with 100 USDC when price ≤ $2.00" |

### IGSObject Structure

| Property       | Type     | Required                        | Description                       |
| -------------- | -------- | ------------------------------- | --------------------------------- |
| `user_address` | `string` | <i class="fa-check">:check:</i> | Sui object owner address          |
| `created_ts`   | `number` | <i class="fa-check">:check:</i> | Creation timestamp (milliseconds) |
| `policy`       | `object` | <i class="fa-check">:check:</i> | Access control policy             |

#### Policy Object

| Property               | Type     | Required                        | Description                      |
| ---------------------- | -------- | ------------------------------- | -------------------------------- |
| `solver_access_window` | `object` | <i class="fa-check">:check:</i> | Time window for solver access    |
| `auto_revoke_time`     | `number` | <i class="fa-check">:check:</i> | Automatic access revocation time |
| `access_condition`     | `object` | <i class="fa-check">:check:</i> | Solver access conditions         |

**Solver Access Window**

| Property   | Type     | Required                        | Description                      |
| ---------- | -------- | ------------------------------- | -------------------------------- |
| `start_ms` | `number` | <i class="fa-check">:check:</i> | Window start time (milliseconds) |
| `end_ms`   | `number` | <i class="fa-check">:check:</i> | Window end time (milliseconds)   |

**Access Conditions**

| Property                       | Type      | Required                        | Description                |
| ------------------------------ | --------- | ------------------------------- | -------------------------- |
| `requires_solver_registration` | `boolean` | <i class="fa-check">:check:</i> | Must be registered solver  |
| `min_solver_stake`             | `string`  | <i class="fa-check">:check:</i> | Minimum stake amount       |
| `requires_tee_attestation`     | `boolean` | <i class="fa-check">:check:</i> | Requires TEE attestation   |
| `min_solver_reputation_score`  | `number`  | <i class="fa-check">:check:</i> | Minimum reputation (0-100) |

### IGSOperation Structure

| Property           | Type                 | Required                        | Description                |
| ------------------ | -------------------- | ------------------------------- | -------------------------- |
| `mode`             | `string`             | <i class="fa-check">:check:</i> | Operation mode             |
| `inputs`           | `array`              | <i class="fa-check">:check:</i> | Input assets (1-10 items)  |
| `outputs`          | `array`              | <i class="fa-check">:check:</i> | Output assets (1-10 items) |
| `expected_outcome` | `IGSExpectedOutcome` |                                 | Expected execution outcome |

#### Operation Modes

| Mode           | Description                          |
| -------------- | ------------------------------------ |
| `exact_input`  | Specify exact input amount           |
| `exact_output` | Specify exact output amount          |
| `limit_order`  | Conditional execution based on price |

### IGSAssetFlow Structure

| Property     | Type        | Required                        | Description                  |
| ------------ | ----------- | ------------------------------- | ---------------------------- |
| `asset_id`   | `string`    | <i class="fa-check">:check:</i> | Asset identifier             |
| `asset_info` | `object`    |                                 | Additional asset information |
| `amount`     | `IGSAmount` | <i class="fa-check">:check:</i> | Amount specification         |

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

| Property | Type     | Required                        | Description                   |
| -------- | -------- | ------------------------------- | ----------------------------- |
| `type`   | `string` | <i class="fa-check">:check:</i> | "exact"                       |
| `value`  | `string` | <i class="fa-check">:check:</i> | Exact amount (integer string) |

#### Range Amount

| Property | Type     | Required                        | Description    |
| -------- | -------- | ------------------------------- | -------------- |
| `type`   | `string` | <i class="fa-check">:check:</i> | "range"        |
| `min`    | `string` | <i class="fa-check">:check:</i> | Minimum amount |
| `max`    | `string` | <i class="fa-check">:check:</i> | Maximum amount |

#### All Amount

| Property | Type     | Required                        | Description                |
| -------- | -------- | ------------------------------- | -------------------------- |
| `type`   | `string` | <i class="fa-check">:check:</i> | "all" (use entire balance) |

### IGSExpectedOutcome Structure

| Property           | Type     | Required                        | Description             |
| ------------------ | -------- | ------------------------------- | ----------------------- |
| `expected_outputs` | `array`  | <i class="fa-check">:check:</i> | Expected output amounts |
| `expected_costs`   | `object` |                                 | Cost estimates          |
| `market_price`     | `object` |                                 | Current market price    |

#### Expected Outputs Item

| Property   | Type     | Required                        | Description      |
| ---------- | -------- | ------------------------------- | ---------------- |
| `asset_id` | `string` | <i class="fa-check">:check:</i> | Asset identifier |
| `amount`   | `string` | <i class="fa-check">:check:</i> | Expected amount  |

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

| Property   | Type     | Required                        | Description      |
| ---------- | -------- | ------------------------------- | ---------------- |
| `asset_id` | `string` | <i class="fa-check">:check:</i> | Asset identifier |
| `amount`   | `string` | <i class="fa-check">:check:</i> | Amount limit     |

#### Routing Object

| Property              | Type     | Description                 |
| --------------------- | -------- | --------------------------- |
| `max_hops`            | `number` | Maximum routing hops (1-10) |
| `blacklist_protocols` | `array`  | Forbidden protocols         |
| `whitelist_protocols` | `array`  | Allowed protocols only      |

#### Limit Price Object

| Property      | Type     | Required                        | Description              |
| ------------- | -------- | ------------------------------- | ------------------------ |
| `price`       | `string` | <i class="fa-check">:check:</i> | Limit price value        |
| `comparison`  | `string` | <i class="fa-check">:check:</i> | "gte" or "lte"           |
| `price_asset` | `string` | <i class="fa-check">:check:</i> | Price denomination asset |

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
