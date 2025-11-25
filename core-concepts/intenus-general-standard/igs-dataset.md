# IGS Dataset

## AI Training Data Schema

**IGS Dataset** defines how interaction data is archived on Walrus for continuous AI model training, performance auditing, and protocol transparency.

## Dataset Purpose

Every intent execution generates valuable training data:
- **Intent Classification**: Teach AI to categorize new intents
- **Ranking Optimization**: Learn which solutions perform best
- **Solver Evaluation**: Track historical performance patterns
- **Market Analysis**: Understand liquidity and pricing dynamics

## Dataset Structure

```json
{
  "dataset_version": "1.0.0",
  "entry_id": "ds_abc123",
  "timestamp": 1699123456000,
  "entry_type": "execution_complete",

  "intent": {
    // Complete intent specification (from IGS Intents)
    "intent_id": "int_xyz789",
    "intent_type": "swap.exact_input",
    // ... full intent data
  },

  "solutions_submitted": [
    {
      // Each solution proposal (from IGS Solutions)
      "solution_id": "sol_abc123",
      "solver_address": "0x...",
      "expected_output": "2495000",
      // ... full solution data
    },
    // ... more solutions
  ],

  "ranking_results": {
    "winner_id": "sol_abc123",
    "scores": {
      "sol_abc123": 9.2,
      "sol_def456": 8.7,
      "sol_ghi789": 8.1
    },
    "ranking_strategy": "swap_optimization_v1",
    "tee_attestation": "0x..."
  },

  "execution_outcome": {
    "success": true,
    "actual_output": "2492000",
    "gas_used": "525000",
    "execution_time_ms": 4800,
    "tx_hash": "0x...",
    "block_number": 12345678
  },

  "market_context": {
    "sui_price_usdc": "2.48",
    "network_gas_price": "1000",
    "cetus_tvl": "50000000",
    "turbos_tvl": "30000000"
  },

  "privacy_metadata": {
    "anonymized": true,
    "sensitive_fields_hashed": ["user_address"],
    "retention_period_days": 730
  }
}
```

## Data Categories

### Training Data

Used for model retraining:
- Intent patterns and classifications
- Solution quality indicators
- Market condition correlations
- Solver performance trends

### Audit Data

Used for verification:
- Ranking decisions and rationale
- TEE attestations
- Execution confirmations
- Dispute evidence

### Analytics Data

Used for insights:
- Protocol usage statistics
- Solver competition dynamics
- User behavior patterns
- Market efficiency metrics

## Privacy Preservation

### Anonymization

Before archiving:
- **User addresses**: Hashed with salt
- **Transaction amounts**: Optionally rounded
- **Specific strategies**: Generalized categories
- **Sensitive metadata**: Stripped or encrypted

### Access Control

Dataset access is tiered:

| Level | Access | Use Case |
|-------|--------|----------|
| Public | Aggregated statistics | Research, dashboards |
| Researcher | Anonymized full data | Model training |
| Auditor | Full data with restrictions | Dispute resolution |
| Governance | Complete access | Protocol decisions |

## Data Storage

### Walrus Integration

All dataset entries stored on Walrus:
- **Cost Efficiency**: Cheap decentralized storage
- **Availability**: Distributed redundancy
- **Integrity**: Cryptographic verification
- **Permanence**: Long-term archival

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
- Solutions that outperformed estimates
- High user satisfaction indicators
- Novel successful strategies

**Negative Examples**:
- Solutions that underperformed
- Failed executions
- User complaints or reverts

## Data Quality

### Validation Checks

Before archiving:
- ✅ Schema compliance
- ✅ Completeness (all required fields)
- ✅ Consistency (intent-solution-outcome match)
- ✅ Integrity (cryptographic verification)

### Quality Metrics

Tracked per dataset entry:
- **Completeness Score**: Percentage of fields populated
- **Accuracy Score**: Match between estimates and actuals
- **Relevance Score**: Usefulness for training

## Usage Examples

### For AI Training

```python
import intenus_dataset

# Load training data
data = intenus_dataset.load(
    start_date="2024-01-01",
    end_date="2024-12-31",
    intent_types=["swap"],
    anonymized=True
)

# Train ranking model
model = train_ranking_model(
    intents=data.intents,
    solutions=data.solutions,
    outcomes=data.outcomes
)
```

### For Analytics

```typescript
import { IntentusAnalytics } from '@intenus/analytics';

// Query solver performance
const stats = await IntentusAnalytics.query({
  metric: 'solver_accuracy',
  solver: '0x...',
  timeframe: 'last_30_days'
});

console.log(`Accuracy: ${stats.avg_accuracy}%`);
```

## Data Retention

### Retention Policy

| Data Type | Retention | Purpose |
|-----------|-----------|---------|
| Recent executions | 90 days | Hot storage, quick access |
| Historical data | 2 years | Training, analytics |
| Audit trails | 7 years | Compliance, disputes |
| Aggregated stats | Permanent | Protocol insights |

### Archival Process

Older data progressively compressed:
1. **Day 1-90**: Full JSON on Walrus
2. **Day 91-730**: Compressed + indexed
3. **Day 731+**: Aggregated summaries only

## Learn More

- [IGS Core](igs-core.md) - Data type definitions
- [AI-Powered Ranking](../ranking-engine.md) - How data is used
- [Privacy Protection](../../technical-documentation/privacy-protection.md) - Security details
