# IGS Core

## Foundation of Standardization

**IGS Core** defines the primitive data types and foundational schemas used throughout the Intenus Protocol. Think of it as the "dictionary" that ensures everyone speaks the same language.

## Core Primitives

### Address Types

```json
{
  "SuiAddress": "0x[64 hex characters]",
  "PackageId": "0x2::sui::SUI",
  "ObjectId": "0x..."
}
```

**Validation**:
- Must start with `0x`
- Valid hexadecimal characters only
- Correct length for type

### Numeric Types

```json
{
  "BigInt": "1000000000",
  "Percentage": 500,  // basis points (5.00%)
  "Timestamp": 1699123456000  // milliseconds since epoch
}
```

**Why Strings for BigInt?**
- JavaScript Number.MAX_SAFE_INTEGER = 2^53 - 1
- DeFi amounts often exceed this
- String representation prevents precision loss

### Amount Specifications

Flexible amount representation for different use cases:

**Exact Amount**:
```json
{
  "type": "exact",
  "value": "1000000000"
}
```

**Range Amount**:
```json
{
  "type": "range",
  "min": "950000",
  "max": "1000000"
}
```

**Percentage Amount**:
```json
{
  "type": "percentage",
  "percent": 5000,  // 50%
  "of": "available_balance"
}
```

### Cryptographic Types

```json
{
  "Signature": {
    "scheme": "ed25519",
    "value": "0x[128 hex characters]",
    "public_key": "0x..."
  },
  "Hash": "0x[64 hex characters]"
}
```

## Asset Identification

### Token Standard

```json
{
  "asset_id": "0x2::sui::SUI",
  "name": "Sui",
  "symbol": "SUI",
  "decimals": 9
}
```

**Format**: `{package_id}::{module}::{type}`

**Examples**:
- Native SUI: `0x2::sui::SUI`
- USDC: `0x{package}::usdc::USDC`
- LP Token: `0x{package}::pool::LP<SUI, USDC>`

### Amount Normalization

All amounts stored as smallest unit:

```
User Input: 1.5 SUI
Stored As: "1500000000" (1.5 × 10^9)

User Input: 100 USDC
Stored As: "100000000" (100 × 10^6)
```

## Constraint System

### Time Constraints

```json
{
  "deadline_ms": 1699123456000,
  "valid_after_ms": 1699120000000,
  "max_duration_ms": 300000
}
```

### Economic Constraints

```json
{
  "max_slippage_bps": 50,        // 0.5%
  "min_output": "950000",
  "max_gas_price": "1000",
  "max_price_impact_bps": 100    // 1%
}
```

### Protocol Constraints

```json
{
  "allowed_protocols": ["Cetus", "Turbos"],
  "excluded_protocols": ["ProtocolX"],
  "require_whitelisted": true
}
```

## Privacy Metadata

```json
{
  "encryption": {
    "algorithm": "seal-aes-256",
    "key_id": "key_abc123",
    "encrypted_fields": ["amount", "target_price"]
  },
  "access_control": {
    "solver_access_window_ms": 300000,
    "requires_solver_registration": true,
    "min_solver_stake": "10000000000",
    "auto_revoke_time": 1699123456000
  }
}
```

## Versioning

### Schema Version Format

```json
{
  "igs_version": "1.0.0",
  "schema_type": "intent",
  "backward_compatible": true
}
```

**Semantic Versioning**:
- **Major (1.x.x)**: Breaking changes
- **Minor (x.1.x)**: Backward-compatible additions
- **Patch (x.x.1)**: Bug fixes, clarifications

### Compatibility Rules

```typescript
function is_compatible(schema_version, client_version) {
  // Major version must match
  if (schema_version.major != client_version.major)
    return false;

  // Schema minor version must be <= client minor
  if (schema_version.minor > client_version.minor)
    return false;

  return true;
}
```

## Validation Rules

### Required Fields

All IGS messages must include:
- `igs_version`: Schema version
- `id`: Unique identifier
- `timestamp`: Creation time
- `signature`: Cryptographic signature

### Optional Fields

Context-dependent fields:
- `metadata`: Additional information
- `tags`: Classification labels
- `references`: Links to related objects

### Field Ordering

While JSON is unordered, IGS recommends:
1. Version and type first
2. Identification fields
3. Core data
4. Constraints
5. Metadata and signatures

**Rationale**: Easier parsing and validation

## Error Handling

### Validation Errors

```json
{
  "error_type": "validation_error",
  "field": "amount.value",
  "message": "Amount exceeds maximum safe integer",
  "code": "IGS_E001"
}
```

### Common Error Codes

| Code | Description |
|------|-------------|
| IGS_E001 | Invalid numeric format |
| IGS_E002 | Missing required field |
| IGS_E003 | Invalid address format |
| IGS_E004 | Version incompatibility |
| IGS_E005 | Invalid timestamp |
| IGS_E006 | Signature verification failed |

## Best Practices

### For Developers

✅ **Always validate inputs** against IGS schemas
✅ **Use BigInt libraries** for amount handling
✅ **Check version compatibility** before processing
✅ **Preserve decimal precision** in conversions
✅ **Include all required fields** in submissions

### For Solvers

✅ **Cache asset metadata** to reduce lookups
✅ **Normalize amounts early** in processing
✅ **Validate signatures** before expensive operations
✅ **Handle version upgrades** gracefully
✅ **Log validation errors** for debugging

## Implementation Support

### TypeScript Types

```typescript
type SuiAddress = string;  // 0x[64 hex]
type BigIntString = string;
type Timestamp = number;

interface Amount {
  type: "exact" | "range" | "percentage";
  value?: BigIntString;
  min?: BigIntString;
  max?: BigIntString;
  percent?: number;
  of?: string;
}
```

### Validation Libraries

**JavaScript/TypeScript**:
```bash
npm install @intenus/igs-validator
```

**Rust**:
```bash
cargo add intenus-igs
```

**Python**:
```bash
pip install intenus-igs
```

## Learn More

- [IGS Intents](igs-intents.md) - Intent schema specification
- [IGS Solutions](igs-solutions.md) - Solution schema specification
- [IGS Dataset](igs-dataset.md) - Training data format
