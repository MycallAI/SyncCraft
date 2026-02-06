# Workflow Patterns

This document outlines the standard architectural patterns supported by SyncCraft. Use these patterns as templates for your `config/` files to ensure stability and predictability in your synchronization pipelines.

---

## Pattern 1: The "Mirror" (Unidirectional Sync)
**Best for:** Backups, read-only replicas, and publishing staging data to production.

In the Mirror pattern, SyncCraft treats the `source` as the single source of truth. Any changes in the `destination` that do not exist in the `source` are ruthlessly overwritten or deleted.

### Configuration Recipe
```yaml
pattern: mirror
strategy: strict_overwrite
interval: 300 # seconds

source:
  type: local_dir
  path: ./data/staging/

destination:
  type: s3_bucket
  bucket: production-assets
  prefix: /v1/

# Safety: Prevents wiping the destination if source is empty
guardrails:
  fail_if_source_empty: true