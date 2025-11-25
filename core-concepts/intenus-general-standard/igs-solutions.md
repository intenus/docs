# IGS Solutions

## Solution Schema Reference

**IGS Solutions** define the standardized format for solver execution proposals, enabling deterministic validation and ranking.

[https://json-schema.org/draft-07/schema#](https://json-schema.org/draft-07/schema)

### Schema Overview

The IGS Solution schema is intentionally minimal, containing only essential information for solver transaction submission to Intenus routers.

<table><thead><tr><th>Property</th><th width="236">Type</th><th data-type="checkbox">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>solver_address</code></td><td><code>string</code></td><td>true</td><td>Sui address of the solver submitting this transaction</td></tr><tr><td><code>tx_bytes</code></td><td><code>string</code></td><td>true</td><td>Serialized transaction bytes (base64 or hex encoded)</td></tr></tbody></table>

### Schema Evolution

#### Version Compatibility

| Version | Changes             | Backward Compatible |
| ------- | ------------------- | ------------------- |
| `1.0.0` | Initial release     | N/A                 |
| Future  | Potential additions | Yes (additive only) |

#### Extension Strategy

While the current schema is minimal by design, future extensions will:

* Add optional fields only
* Maintain backward compatibility
* Use semantic versioning
* Provide migration guides

## Learn More

* [IGS Core](igs-core.md) - Primitive types
* [Solutions Concept](../solutions.md) - High-level overview
* [Pre-ranking Engine](../pre-ranking-engine.md) - Validation process

## References

{% file src="../../.gitbook/assets/igs-solution-schema.json" %}
