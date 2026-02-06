# Architecture & Patterns

## Data Schema
SyncCraft expects input data to follow the strict schema defined below.

| Field | Type | Description |
| :--- | :--- | :--- |
| `sync_id` | UUID | Unique identifier for the sync event. |
| `payload` | JSON | The data payload to be synchronized. |

## Output Patterns
When SyncCraft successfully executes, it produces artifacts following this structure:

```json
{
  "status": "success",
  "timestamp": "ISO-8601",
  "artifacts": [
    "path/to/artifact_1"
  ]
}