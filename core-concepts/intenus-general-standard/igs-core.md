# IGS Core

## Foundation of Standardization

**IGS Core** defines the primitive data types and foundational schemas used throughout the Intenus Protocol. Think of it as the "dictionary" that ensures everyone speaks the same language.

## Core Schema Reference

### Schema Overview

| Definition             | Description                                                                   |
| ---------------------- | ----------------------------------------------------------------------------- |
| `SolutionSubmission`   | Solution submitted by solver (on-chain reference)                             |
| `IntentClassification` | Intent classification result from ML classifier                               |
| `PreRankingResult`     | PreRanking engine result - validation, classification, and feature extraction |
| `RankedSolution`       | Ranked solution with scoring and explanation                                  |
| `RankingResult`        | Ranking engine final result                                                   |

### SolutionSubmission

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>solution_id</code></td><td><code>string</code></td><td>true</td><td>Unique solution ID (from on-chain object)</td></tr><tr><td><code>intent_id</code></td><td><code>string</code></td><td>true</td><td>Intent ID this solution is for</td></tr><tr><td><code>solver_address</code></td><td><code>string</code></td><td>true</td><td>Solver's blockchain address</td></tr><tr><td><code>submitted_at</code></td><td><code>number</code></td><td>true</td><td>Submission timestamp (Unix ms)</td></tr><tr><td><code>blob_id</code></td><td><code>string</code></td><td>false</td><td>Tx transaction bytes reference</td></tr></tbody></table>

### IntentClassification

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>primary_category</code></td><td><code>string</code></td><td>true</td><td>Primary detected intent category</td></tr><tr><td><code>primary_category_confidence</code></td><td><code>number</code></td><td>true</td><td>Primary category confidence (0-1)</td></tr><tr><td><code>detected_priority</code></td><td><code>string</code></td><td>true</td><td>User priority detected from constraints</td></tr><tr><td><code>detected_priority_confidence</code></td><td><code>number</code></td><td>true</td><td>Priority detection confidence (0-1)</td></tr><tr><td><code>complexity_level</code></td><td><code>string</code></td><td>true</td><td>Intent complexity level</td></tr><tr><td><code>complexity_level_confidence</code></td><td><code>number</code></td><td>true</td><td>Complexity confidence (0-1)</td></tr><tr><td><code>risk_level</code></td><td><code>string</code></td><td>true</td><td>Risk assessment level</td></tr><tr><td><code>risk_level_confidence</code></td><td><code>number</code></td><td>true</td><td>Risk level confidence (0-1)</td></tr><tr><td><code>strategy</code></td><td><code>string</code></td><td>true</td><td>Detected optimal strategy</td></tr><tr><td><code>strategy_confidence</code></td><td><code>number</code></td><td>true</td><td>Strategy confidence (0-1)</td></tr><tr><td><code>weights</code></td><td><code>object</code></td><td>true</td><td>Ranking weights object</td></tr></tbody></table>

#### Primary Category Values

| Value          | Description           |
| -------------- | --------------------- |
| `swap`         | Token swap operation  |
| `limit_order`  | Limit order execution |
| `complex_defi` | Complex DeFi strategy |
| `arbitrage`    | Arbitrage opportunity |
| `other`        | Other intent type     |

#### Detected Priority Values

| Value      | Description             |
| ---------- | ----------------------- |
| `speed`    | Speed-focused priority  |
| `cost`     | Cost-focused priority   |
| `output`   | Output-focused priority |
| `balanced` | Balanced priority       |

#### Complexity Level Values

| Value      | Description         |
| ---------- | ------------------- |
| `simple`   | Simple operation    |
| `moderate` | Moderate complexity |
| `complex`  | High complexity     |

#### Risk Level Values

| Value    | Description            |
| -------- | ---------------------- |
| `low`    | Low risk assessment    |
| `medium` | Medium risk assessment |
| `high`   | High risk assessment   |

#### Weights Object

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>gt_weight_surplus_usd</code></td><td><code>number</code></td><td>true</td><td>Weight for surplus in USD</td></tr><tr><td><code>gt_weight_surplus_percentage</code></td><td><code>number</code></td><td>true</td><td>Weight for surplus percentage</td></tr><tr><td><code>gt_weight_gas_cost</code></td><td><code>number</code></td><td>true</td><td>Weight for gas cost</td></tr><tr><td><code>gt_weight_protocol_fees</code></td><td><code>number</code></td><td>true</td><td>Weight for protocol fees</td></tr><tr><td><code>gt_weight_total_hops</code></td><td><code>number</code></td><td>true</td><td>Weight for total routing hops</td></tr><tr><td><code>gt_weight_protocols_count</code></td><td><code>number</code></td><td>true</td><td>Weight for number of protocols</td></tr><tr><td><code>gt_weight_estimated_execution_time</code></td><td><code>number</code></td><td>true</td><td>Weight for execution time</td></tr><tr><td><code>gt_weight_solver_reputation_score</code></td><td><code>number</code></td><td>true</td><td>Weight for solver reputation</td></tr><tr><td><code>gt_weight_solver_success_rate</code></td><td><code>number</code></td><td>true</td><td>Weight for solver success rate</td></tr></tbody></table>

### PreRankingResult

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>intent_id</code></td><td><code>string</code></td><td>true</td><td>Intent ID being processed</td></tr><tr><td><code>intent_classification</code></td><td><code>IntentClassification</code></td><td>true</td><td>Intent classification result</td></tr><tr><td><code>passed_solution_ids</code></td><td><code>array</code></td><td>true</td><td>Solution IDs that passed validation</td></tr><tr><td><code>failed_solution_ids</code></td><td><code>array</code></td><td>true</td><td>Failed solutions with reasons</td></tr><tr><td><code>feature_vectors</code></td><td><code>array</code></td><td>true</td><td>Solution feature vectors</td></tr><tr><td><code>dry_run_results</code></td><td><code>array</code></td><td>true</td><td>Simulation results</td></tr><tr><td><code>stats</code></td><td><code>object</code></td><td>true</td><td>Processing statistics</td></tr><tr><td><code>processed_at</code></td><td><code>number</code></td><td>true</td><td>Processing timestamp (Unix ms)</td></tr></tbody></table>

#### Failed Solution Item

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>solution_id</code></td><td><code>string</code></td><td>true</td><td>Solution identifier</td></tr><tr><td><code>failure_reason</code></td><td><code>string</code></td><td>true</td><td>Reason for failure</td></tr><tr><td><code>errors</code></td><td><code>array</code></td><td>true</td><td>Error details array</td></tr></tbody></table>

#### Feature Vector Item

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>solution_id</code></td><td><code>string</code></td><td>true</td><td>Solution identifier</td></tr><tr><td><code>features</code></td><td><code>object</code></td><td>true</td><td>Feature data object</td></tr></tbody></table>

#### Features Object

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>surplus_usd</code></td><td><code>number</code></td><td>true</td><td>Surplus value in USD</td></tr><tr><td><code>surplus_percentage</code></td><td><code>number</code></td><td>true</td><td>Surplus as percentage</td></tr><tr><td><code>gas_cost</code></td><td><code>number</code></td><td>true</td><td>Gas cost estimate</td></tr><tr><td><code>protocol_fees</code></td><td><code>number</code></td><td>true</td><td>Protocol fees total</td></tr><tr><td><code>total_cost</code></td><td><code>number</code></td><td>true</td><td>Total execution cost</td></tr><tr><td><code>total_hops</code></td><td><code>number</code></td><td>true</td><td>Number of routing hops</td></tr><tr><td><code>protocols_count</code></td><td><code>number</code></td><td>true</td><td>Number of protocols used</td></tr><tr><td><code>estimated_execution_time</code></td><td><code>number</code></td><td>true</td><td>Estimated execution time</td></tr><tr><td><code>solver_reputation_score</code></td><td><code>number</code></td><td>true</td><td>Solver reputation score</td></tr><tr><td><code>solver_success_rate</code></td><td><code>number</code></td><td>true</td><td>Solver historical success rate</td></tr></tbody></table>

#### Dry Run Result Item

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>solution_id</code></td><td><code>string</code></td><td>true</td><td>Solution identifier</td></tr><tr><td><code>result</code></td><td><code>object</code></td><td>true</td><td>Raw simulation result from Sui</td></tr></tbody></table>

#### Stats Object

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>total_submitted</code></td><td><code>number</code></td><td>true</td><td>Total solutions submitted</td></tr><tr><td><code>passed</code></td><td><code>number</code></td><td>true</td><td>Number that passed validation</td></tr><tr><td><code>failed</code></td><td><code>number</code></td><td>true</td><td>Number that failed validation</td></tr><tr><td><code>dry_run_executed</code></td><td><code>number</code></td><td>true</td><td>Number of dry runs executed</td></tr><tr><td><code>dry_run_successful</code></td><td><code>number</code></td><td>true</td><td>Number of successful dry runs</td></tr></tbody></table>

### RankedSolution

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>rank</code></td><td><code>number</code></td><td>true</td><td>Ranking position (1 = best)</td></tr><tr><td><code>score</code></td><td><code>number</code></td><td>true</td><td>Overall score (0-100)</td></tr><tr><td><code>solution_id</code></td><td><code>string</code></td><td>true</td><td>Solution ID reference</td></tr><tr><td><code>solver_address</code></td><td><code>string</code></td><td>true</td><td>Solver address</td></tr><tr><td><code>transaction_bytes</code></td><td><code>string</code></td><td>true</td><td>Transaction bytes for execution</td></tr><tr><td><code>score_breakdown</code></td><td><code>object</code></td><td>true</td><td>Score breakdown object</td></tr><tr><td><code>reasoning</code></td><td><code>object</code></td><td>true</td><td>Ranking reasoning</td></tr><tr><td><code>personalization_applied</code></td><td><code>boolean</code></td><td>true</td><td>Whether personalization was applied</td></tr><tr><td><code>warnings</code></td><td><code>array</code></td><td>true</td><td>Warning messages array</td></tr><tr><td><code>expires_at</code></td><td><code>number</code></td><td>true</td><td>Expiration timestamp (Unix ms)</td></tr><tr><td><code>user_fit_score</code></td><td><code>number</code></td><td>true</td><td>User preference fit score</td></tr></tbody></table>

#### Score Breakdown Object

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>surplus_score</code></td><td><code>number</code></td><td>true</td><td>Score for surplus generation</td></tr><tr><td><code>cost_score</code></td><td><code>number</code></td><td>true</td><td>Score for cost optimization</td></tr><tr><td><code>speed_score</code></td><td><code>number</code></td><td>true</td><td>Score for execution speed</td></tr><tr><td><code>reputation_score</code></td><td><code>number</code></td><td>true</td><td>Score for solver reputation</td></tr></tbody></table>

#### Reasoning Object

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>primary_reason</code></td><td><code>string</code></td><td>true</td><td>Main reason for ranking</td></tr><tr><td><code>secondary_reasons</code></td><td><code>array</code></td><td>true</td><td>Additional ranking factors</td></tr><tr><td><code>risk_assessment</code></td><td><code>string</code></td><td>true</td><td>Risk level assessment</td></tr><tr><td><code>confidence_level</code></td><td><code>number</code></td><td>true</td><td>Confidence in ranking (0-1)</td></tr></tbody></table>

#### Risk Assessment Values

| Value    | Description          |
| -------- | -------------------- |
| `low`    | Low risk solution    |
| `medium` | Medium risk solution |
| `high`   | High risk solution   |

### RankingResult

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>intent_id</code></td><td><code>string</code></td><td>true</td><td>Intent identifier</td></tr><tr><td><code>ranked_solutions</code></td><td><code>array</code></td><td>true</td><td>Array of ranked solutions</td></tr><tr><td><code>best_solution</code></td><td><code>RankedSolution</code></td><td>true</td><td>Top-ranked solution</td></tr><tr><td><code>metadata</code></td><td><code>object</code></td><td>true</td><td>Ranking metadata</td></tr><tr><td><code>ranked_at</code></td><td><code>number</code></td><td>true</td><td>Ranking timestamp</td></tr><tr><td><code>expires_at</code></td><td><code>number</code></td><td>true</td><td>Result expiration timestamp</td></tr></tbody></table>

#### Metadata Object

<table><thead><tr><th>Property</th><th>Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>total_solutions</code></td><td><code>number</code></td><td>true</td><td>Total number of solutions ranked</td></tr><tr><td><code>average_score</code></td><td><code>number</code></td><td>true</td><td>Average score across all solutions</td></tr><tr><td><code>strategy</code></td><td><code>string</code></td><td>true</td><td>Ranking strategy used</td></tr><tr><td><code>intent_category</code></td><td><code>string</code></td><td>true</td><td>Intent category classification</td></tr></tbody></table>

## Learn More

* [IGS Intents](igs-intents.md) - Intent schema specification
* [IGS Solutions](igs-solutions.md) - Solution schema specification
* [IGS Dataset](igs-dataset.md) - Training data format

## References

{% file src="../../.gitbook/assets/core-schema.json" %}
