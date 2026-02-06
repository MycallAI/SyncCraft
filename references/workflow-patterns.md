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

pattern: aggregator
strategy: merge_by_timestamp

upstreams:
  - id: agent_alpha
    path: ./data/agents/alpha/logs.json
  - id: agent_beta
    path: ./data/agents/beta/logs.json

downstream:
  path: ./data/global_context.json

# Conflict Resolution: How to handle colliding keys
resolution:
  on_conflict: prefer_latest
  ignore_nulls: true

pattern: governor
strategy: diff_and_wait

source:
  type: git_branch
  branch: develop

destination:
  type: git_branch
  branch: main

# Approval Logic
gate:
  require_manual_approval: true
  diff_threshold: 15% # Auto-reject if changes exceed 15% of file volume
  notify:
    slack_webhook: ${SLACK_WEBHOOK_URL}
