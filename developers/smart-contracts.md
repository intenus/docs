---
icon: file-lock
---

# Smart Contracts

Intenus deploys a modular contract system on Sui, with each module handling specific responsibilities:

## Core Modules

### **1. Registry Module**

Manages intent lifecycle and solution submissions

**Functions**:

* `submit_intent()`: Register new trading intent
* `cancel_intent()`: User cancellation
* `get_intent_status()`: Query intent state
* `list_active_intents()`: Discovery for solvers

### **2. Solver Registry**&#x20;

Handles solver registration and reputation

**Functions**:

* `register_solver()`: Join the solver network
* `update_stake()`: Modify staked amount
* `get_solver_profile()`: Query solver information
* `update_reputation()`: Record performance metrics

### **3. Solution Manager**&#x20;

Processes solver proposals

**Functions**:

* `submit_solution()`: Propose execution strategy
* `validate_solution()`: Check proposal validity
* `rank_solutions()`: Trigger AI ranking process
* `select_winner()`: Choose optimal solution

### **4. Slash Manager**

Implements penalties for malicious behavior

**Functions**:

* `submit_slash_evidence()`: Report violations
* `appeal_slash()`: Contest penalties
* `execute_slash()`: Apply penalties
* `resolve_appeal()`: Adjudicate disputes

### **5. TEE Verifier**

Validates attestations from Nautilus

**Functions**:

* `verify_attestation()`: Check TEE proof validity
* `register_tee_instance()`: Whitelist secure enclaves
* `update_measurement()`: Maintain security guarantees

### **6. Execution Engine**

Executes winning solutions

**Functions**:

* `execute_solution()`: Run winning strategy
* `verify_outcome()`: Confirm results
* `distribute_rewards()`: Pay solver fees
* `handle_failure()`: Manage execution errors

## Transaction Flow

### Submitting an Intent

```move
public entry fun submit_intent(
    blob_id: String,
    solver_access_start_ms: u64,
    solver_access_end_ms: u64,
    auto_revoke_ms: u64,
    requires_solver_registration: bool,
    min_solver_stake: u64,
    requires_attestation: bool,
    min_solver_reputation_score: u64,
    fee: Coin<SUI>,
    clock: &Clock,
    ctx: &mut TxContext,
) {
    let sender = tx_context::sender(ctx);
    let timestamp_ms = clock::timestamp_ms(clock);
    let fee_amount = coin::value(&fee);

    // Validate input
    assert!(blob_id.length() > 0, E_INVALID_BLOB_ID);
    assert!(solver_access_start_ms < solver_access_end_ms, E_INVALID_TIME_WINDOW);
    assert!(fee_amount >= MIN_INTENT_FEE, E_INSUFFICIENT_FEE);

    // Create intent with reference to Walrus blob
    let intent_uid = object::new(ctx);
    let intent_id = object::uid_to_inner(&intent_uid);

    let intent = Intent {
        id: intent_uid,
        user_addr: sender,
        created_ms: timestamp_ms,
        blob_id,
        policy: PolicyParams {
            solver_access_window: TimeWindow {
                start_ms: solver_access_start_ms,
                end_ms: solver_access_end_ms,
            },
            auto_revoke_ms,
            access_condition: AccessCondition {
                requires_solver_registration,
                min_solver_stake,
                requires_attestation,
                min_solver_reputation_score,
            },
        },
        intent_fee: coin::into_balance(fee),
        status: INTENT_STATUS_PENDING,
        best_solution_id: option::none(),
        pending_solutions: vector::empty(),
    };

    // Emit event
    event::emit(IntentSubmitted {
        intent_id,
        user_addr: sender,
        blob_id: intent.blob_id,
        created_ms: timestamp_ms,
        solver_access_start_ms,
        solver_access_end_ms,
        fee_amount,
    });

    // Transfer intent to user
    transfer::public_transfer(intent, sender);
}
```

### Executing a Solution

```move
public entry fun execute_solution(
    intent: &mut Intent,
    solution: &mut Solution,
    treasury: &mut Treasury,
    clock: &Clock,
    ctx: &mut TxContext,
) {
    let sender = tx_context::sender(ctx);
    let timestamp_ms = clock::timestamp_ms(clock);

    // Verify sender is the intent owner
    assert!(intent.user_addr == sender, E_UNAUTHORIZED);
    assert!(intent.status == INTENT_STATUS_BEST_SOLUTION_SELECTED, E_INVALID_STATUS_TRANSITION);

    // Verify this is the selected solution
    let selected_id = option::borrow(&intent.best_solution_id);
    let solution_id = object::uid_to_inner(&solution.id);
    assert!(*selected_id == solution_id, E_UNAUTHORIZED);

    // Verify solution is attested
    assert!(solution.status == SOLUTION_STATUS_ATTESTED, E_ATTESTATION_REQUIRED);

    // Distribute fee
    let total_fee = balance::value(&intent.intent_fee);
    let platform_fee_amount = (total_fee * PLATFORM_FEE_BPS) / 10000;
    let solver_reward_amount = total_fee - platform_fee_amount;

    // Transfer platform fee to treasury
    let platform_fee_balance = balance::split(&mut intent.intent_fee, platform_fee_amount);
    balance::join(&mut treasury.balance, platform_fee_balance);
    treasury.total_fees_collected = treasury.total_fees_collected + platform_fee_amount;

    // Transfer solver reward
    let solver_reward_balance = balance::withdraw_all(&mut intent.intent_fee);
    let solver_reward_coin = coin::from_balance(solver_reward_balance, ctx);
    transfer::public_transfer(solver_reward_coin, solution.solver_addr);

    // Update statuses
    intent.status = INTENT_STATUS_EXECUTED;
    solution.status = SOLUTION_STATUS_EXECUTED;

    // Emit event
    event::emit(IntentExecuted {
        intent_id: object::uid_to_inner(&intent.id),
        solution_id,
        user_addr: sender,
        executed_at_ms: timestamp_ms,
        solver_reward: solver_reward_amount,
        platform_fee: platform_fee_amount,
    });
}

```

## Security Features

**Access Control**

* Intent creators can cancel before execution
* Only whitelisted TEE instances can submit rankings
* Solver stake requirements enforced on-chain

**Atomic Execution**

* All multi-step solutions execute atomically via PTBs
* Failure in any step reverts entire transaction
* No partial state changes possible

**Slashing Mechanics**

* Automatic slashing for proven misbehavior
* 24-hour appeal window for contested penalties
* Governance resolution for complex cases

**Emergency Controls**

* Circuit breakers for detected anomalies
* Pause functionality for critical vulnerabilities
* Upgrade mechanisms for bug fixes
