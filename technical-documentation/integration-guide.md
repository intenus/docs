# Integration Guide

## For Clients

#### Installing the Client SDK

```bash
npm install @intenus/client-sdk
```

### Quick Start

```typescript
import { IntenusProtocolClient, IntentBuilder } from '@intenus/client-sdk';
import { Ed25519Keypair } from '@mysten/sui/keypairs/ed25519';

const client = new IntenusProtocolClient({
  network: 'testnet'
});

const keypair = Ed25519Keypair.generate();

// Get protocol stats
const stats = await client.getProtocolStats();
console.log('Registered solvers:', stats.registry.total_solvers);
console.log('Current batch:', stats.current_batch?.batch_id);

```

### Solver Registry

```typescript
// Register as solver
const stake = '1000000000'; // 1 SUI
const result = await client.solvers.register(stake, keypair);

// Get solver profile
const profile = await client.solvers.getProfile(keypair.toSuiAddress());
console.log('Stake:', profile.stake_amount);
console.log('Reputation:', profile.reputation_score);

// Update stake
await client.solvers.increaseStake('500000000', keypair);

// Unstake
await client.solvers.unstake(keypair);
```

### Batch Management

```typescript
// Get current batch
const batch = await client.batches.getCurrentBatch();

// Get batch stats for specific epoch
const epochStats = await client.batches.getBatchStats(12345);

// Get batch history
const history = await client.batches.getBatchHistory(100, 200);

// Get batch metrics
const metrics = await client.batches.getBatchMetrics(batchId);
console.log('Total intents:', metrics.total_intents);
console.log('Solver participation:', metrics.solver_participation);
```

### Seal Policies

```typescript
// Create intent policy
await client.policies.createIntentPolicy({
  policyId: 'policy_001',
  batchId: 1,
  solverWindowMs: 5000,
  routerAccessEnabled: true,
  requiresSolverRegistration: true,
  minSolverStake: '1000000000'
}, keypair);

// Create strategy policy
await client.policies.createStrategyPolicy({
  policyId: 'strat_001',
  routerAccess: false,
  isPublic: false,
  adminUnlockTime: Date.now() + 86400000
}, keypair);

// Revoke policy
await client.policies.revokePolicy('intent', policyId, keypair);
```

### Slash Management

```typescript
// Submit slash evidence
const evidence = {
  batch_id: 1,
  solution_id: 'sol_123',
  solver_address: '0x...',
  severity: SlashSeverity.SIGNIFICANT,
  reason_code: 2001,
  reason_message: 'MEV extraction detected',
  failure_context: JSON.stringify({ details }),
  attestation: '0x...',
  attestation_timestamp: Date.now(),
  tee_measurement: '0x...'
};

await client.slashing.submitEvidence(evidence, keypair);

// Appeal slash
await client.slashing.appeal(recordId, justification, keypair);

// Get slash records
const records = await client.slashing.getRecords(solverAddress);
```

### Intent Builder

```typescript
import { IntentBuilder } from '@intenus/client-sdk';

const intent = new IntentBuilder()
  .setType('spot_trade')
  .addAssetFlow({
    asset_id: '0x2::sui::SUI',
    direction: 'in',
    amount: { exact: '1000000000' }
  })
  .addAssetFlow({
    asset_id: '0x...::usdc::USDC',
    direction: 'out',
    amount: { minimum: '900000' }
  })
  .setConstraints({
    max_slippage_bps: 50,
    min_output_amount: '900000'
  })
  .setPreferences({
    optimization_goal: 'maximize_output'
  })
  .build();
```

## For Solvers

### Listen for Batches

```typescript
import { SolverListener } from '@intenus/solver-sdk';

const listener = new SolverListener('redis://localhost:6379');

listener.onNewBatch(async (batch) => {
  console.log(`New batch: ${batch.batch_id}`);
  console.log(`Intents: ${batch.intent_ids.length}`);

  // Fetch intents and build solutions
  const solution = await buildSolution(batch);

  // Submit solution
  await listener.submitSolution(solution, batch.batch_id);
});

// Send heartbeat
await listener.sendHeartbeat(solverAddress);
```

### Build Solutions

```typescript
import { SolutionBuilder } from '@intenus/solver-sdk';
import { SuiClient } from '@mysten/sui/client';

const client = new SuiClient({ url: 'https://testnet.sui.io' });
const builder = new SolutionBuilder(intentId, solverAddress);

// Add Tx operations
builder.getTx().moveCall({
  target: '0x2::sui::split',
  arguments: [/* ... */]
});

// Build submission
const { submission, txBytes } = await builder.build({ client });

// Submit to chain or backend
```

### Build IGS Solutions

```typescript
import { IGSSolutionBuilder } from '@intenus/solver-sdk';
import type { Intent as IGSIntent } from '@intenus/common';

const intent: IGSIntent = { /* ... */ };

const builder = createIGSSolutionBuilder({
  solverId: 'solver_123',
  confidenceScore: 0.95
});

const solution = builder
  .setIntent(intent)
  .addRoute({ dex: 'cetus', pool_id: '0x...' })
  .setExpectedOutput({ amount: '1000000', slippage_bps: 50 })
  .build();

// Validate solution
const isValid = validateIGSSolution(solution);
```

## Testing

### Local Development

```bash
# Start local Sui node
sui start

# Deploy Intenus contracts
npm run deploy:local

# Run integration tests
npm run test:integration
```

### Testnet Integration

```typescript
const client = new IntenusClient({
  network: 'testnet',
  rpcUrl: 'https://fullnode.testnet.sui.io',
});

// Get testnet tokens from faucet
await client.requestTestnetTokens();

// Submit test intent
const testIntent = new IntentBuilder()
  .swap()
  .exactInput('1000000', '0x2::sui::SUI')
  .outputToken('0x...::usdc::USDC')
  .build();

const result = await client.submitIntent(testIntent);
```
