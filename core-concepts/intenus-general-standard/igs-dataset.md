# IGS Dataset

## AI Training Data Schema

**IGS Dataset** defines how interaction data is archived on Walrus for continuous AI model training, performance auditing, and protocol transparency.

## Dataset Purpose

Every intent execution generates valuable training data:

* **Intent Classification**: Teach AI to categorize new intents
* **Ranking Optimization**: Learn which solutions perform best
* **Solver Evaluation**: Track historical performance patterns
* **Market Analysis**: Understand liquidity and pricing dynamics

## Solution Schema Reference

### Schema Overview

| Definition                         | Description                                           |
| ---------------------------------- | ----------------------------------------------------- |
| `RawFeatures`                      | Raw features extracted from IGSIntent for ML training |
| `GroundTruthLabel`                 | Ground truth classification labels                    |
| `LabelingMetadata`                 | Labeling metadata                                     |
| `ExecutionOutcome`                 | Execution outcome for feedback loop                   |
| `IntentClassificationTrainingData` | Complete training sample for intent classification    |

### RawFeatures

| Property                    | Type      | Description                       |
| --------------------------- | --------- | --------------------------------- |
| `solver_window_ms`          | `number`  | Solver access window duration     |
| `user_decision_timeout_ms`  | `number`  | User decision timeout             |
| `time_to_deadline_ms`       | `number`  | Time until deadline               |
| `time_in_force`             | `string`  | Time in force policy              |
| `max_slippage_bps`          | `number`  | Maximum slippage in basis points  |
| `max_gas_cost_usd`          | `number`  | Maximum gas cost in USD           |
| `max_hops`                  | `number`  | Maximum routing hops              |
| `has_whitelist`             | `boolean` | Has protocol whitelist            |
| `has_blacklist`             | `boolean` | Has protocol blacklist            |
| `has_limit_price`           | `boolean` | Has limit price condition         |
| `optimization_goal`         | `string`  | Primary optimization goal         |
| `surplus_weight`            | `number`  | Surplus weight (0-100)            |
| `gas_cost_weight`           | `number`  | Gas cost weight (0-100)           |
| `execution_speed_weight`    | `number`  | Execution speed weight (0-100)    |
| `reputation_weight`         | `number`  | Reputation weight (0-100)         |
| `require_simulation`        | `boolean` | Requires simulation               |
| `input_count`               | `number`  | Number of input assets            |
| `output_count`              | `number`  | Number of output assets           |
| `input_asset_types`         | `array`   | Input asset type classifications  |
| `output_asset_types`        | `array`   | Output asset type classifications |
| `input_value_usd`           | `number`  | Input value in USD                |
| `expected_output_value_usd` | `number`  | Expected output value in USD      |
| `benchmark_source`          | `string`  | Benchmark data source             |
| `benchmark_confidence`      | `number`  | Benchmark confidence (0-1)        |
| `expected_gas_usd`          | `number`  | Expected gas cost in USD          |
| `expected_slippage_bps`     | `number`  | Expected slippage in basis points |
| `has_nlp_input`             | `boolean` | Has natural language input        |
| `nlp_confidence`            | `number`  | NLP parsing confidence (0-1)      |
| `client_platform`           | `string`  | Client platform identifier        |
| `tag_count`                 | `number`  | Number of tags                    |

#### Time in Force Values

| Value             | Description         |
| ----------------- | ------------------- |
| `immediate`       | Immediate execution |
| `good_til_cancel` | Good until canceled |
| `fill_or_kill`    | Fill or kill order  |

#### Optimization Goal Values

| Value               | Description             |
| ------------------- | ----------------------- |
| `maximize_output`   | Maximize output amount  |
| `minimize_gas`      | Minimize gas costs      |
| `fastest_execution` | Fastest execution speed |
| `balanced`          | Balanced optimization   |

#### Asset Type Values

| Value      | Description             |
| ---------- | ----------------------- |
| `native`   | Native blockchain token |
| `stable`   | Stablecoin              |
| `volatile` | Volatile cryptocurrency |

### GroundTruthLabel

| Property            | Type     | Description             |
| ------------------- | -------- | ----------------------- |
| `primary_category`  | `string` | Primary intent category |
| `detected_priority` | `string` | Detected user priority  |
| `complexity_level`  | `string` | Intent complexity level |
| `risk_level`        | `string` | Associated risk level   |

#### Primary Category Values

| Value          | Description           |
| -------------- | --------------------- |
| `swap`         | Token swap operation  |
| `limit_order`  | Limit order execution |
| `complex_defi` | Complex DeFi strategy |
| `arbitrage`    | Arbitrage opportunity |
| `other`        | Other intent type     |

#### Detected Priority Values

| Value      | Description       |
| ---------- | ----------------- |
| `speed`    | Speed-focused     |
| `cost`     | Cost-focused      |
| `output`   | Output-focused    |
| `balanced` | Balanced priority |

#### Complexity Level Values

| Value      | Description         |
| ---------- | ------------------- |
| `simple`   | Simple operation    |
| `moderate` | Moderate complexity |
| `complex`  | High complexity     |

#### Risk Level Values

| Value    | Description |
| -------- | ----------- |
| `low`    | Low risk    |
| `medium` | Medium risk |
| `high`   | High risk   |

### LabelingMetadata

| Property           | Type     | Description                   |
| ------------------ | -------- | ----------------------------- |
| `labeling_method`  | `string` | Method used for labeling      |
| `labeled_by`       | `string` | Entity that created the label |
| `labeled_at`       | `number` | Labeling timestamp            |
| `label_confidence` | `number` | Label confidence (0-1)        |
| `notes`            | `string` | Additional labeling notes     |

#### Labeling Method Values

| Value           | Description                   |
| --------------- | ----------------------------- |
| `expert_manual` | Manual expert labeling        |
| `rule_based`    | Rule-based automatic labeling |
| `outcome_based` | Based on execution outcomes   |
| `user_feedback` | User feedback labeling        |
| `synthetic`     | Synthetically generated       |

### ExecutionOutcome

| Property               | Type      | Description                   |
| ---------------------- | --------- | ----------------------------- |
| `executed`             | `boolean` | Whether intent was executed   |
| `chosen_solution_rank` | `number`  | Rank of chosen solution       |
| `chosen_solution_id`   | `string`  | ID of chosen solution         |
| `actual_metrics`       | `object`  | Actual execution metrics      |
| `user_satisfaction`    | `number`  | User satisfaction score (1-5) |
| `executed_at`          | `number`  | Execution timestamp           |

#### Actual Metrics Object

| Property                   | Type     | Description                           |
| -------------------------- | -------- | ------------------------------------- |
| `actual_output_usd`        | `number` | Actual output value in USD            |
| `actual_gas_cost_usd`      | `number` | Actual gas cost in USD                |
| `actual_execution_time_ms` | `number` | Actual execution time in milliseconds |
| `actual_slippage_bps`      | `number` | Actual slippage in basis points       |

### IntentClassificationTrainingData

| Property            | Type               | Description                   |
| ------------------- | ------------------ | ----------------------------- |
| `sample_id`         | `string`           | Unique sample identifier      |
| `intent_metadata`   | `object`           | Intent metadata object        |
| `raw_features`      | `RawFeatures`      | Raw feature data              |
| `ground_truth`      | `GroundTruthLabel` | Ground truth labels           |
| `label_info`        | `LabelingMetadata` | Labeling metadata             |
| `execution_outcome` | `ExecutionOutcome` | Execution outcome data        |
| `dataset_version`   | `string`           | Dataset version identifier    |
| `created_at`        | `number`           | Sample creation timestamp     |
| `full_intent_ref`   | `string`           | Reference to full intent data |

#### Intent Metadata Object

| Property      | Type     | Description                |
| ------------- | -------- | -------------------------- |
| `intent_id`   | `string` | Intent identifier          |
| `intent_type` | `string` | Intent type classification |
| `created_at`  | `number` | Intent creation timestamp  |

## Data Storage

### Walrus Integration

All dataset entries stored on Walrus:

* **Cost Efficiency**: Cheap decentralized storage
* **Availability**: Distributed redundancy
* **Integrity**: Cryptographic verification
* **Permanence**: Long-term archival

### Storage Format

```
walrus://{blob_id}

Blob contains:
- Compressed JSON
- Metadata header
- Cryptographic hash
- Version identifier
```

## Continuous Learning

### Model Retraining Cycle

1. **Data Collection**: New executions archived hourly
2. **Preprocessing**: Anonymization and validation
3. **Training**: Updated models trained weekly
4. **Validation**: Performance tested on holdout set
5. **Deployment**: Gradual rollout to production

### Reinforcement Learning

**Positive Examples**:

* Solutions that outperformed estimates
* High user satisfaction indicators
* Novel successful strategies

**Negative Examples**:

* Solutions that underperformed
* Failed executions
* User complaints or reverts

### Archival Process

Older data progressively compressed:

1. **Day 1-90**: Full JSON on Walrus
2. **Day 91-730**: Compressed + indexed
3. **Day 731+**: Aggregated summaries only

## Learn More

* [IGS Core](igs-core.md) - Data type definitions
* [AI-Powered Ranking](../ranking-engine.md) - How data is used
* [Privacy Protection](../../technical-documentation/privacy-protection.md) - Security details

## References

{% file src="../../.gitbook/assets/dataset-schema.json" %}
