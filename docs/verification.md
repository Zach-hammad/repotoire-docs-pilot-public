# Documentation verification

The default port is `9006`, as defined by `src/service.py#default_port`.

The check reads the source syntax without executing it. Exit 0 means both claims agree; exit 1 means stale documentation; exit 2 means the claim cannot be verified.

```json verification-metadata
{
  "schema": "repotoire.verification_metadata.v1",
  "profiles": [
    {
      "profile_id": "documentation-contract",
      "kind": "test",
      "command": [
        "tools/check-docs"
      ],
      "source_file": "tools/check-docs",
      "runtime": "repository-tool",
      "languages": [
        "markdown",
        "python"
      ],
      "confidence": "high",
      "tier": "fast",
      "expected_wall_time_ms": 10000,
      "expected_summary": "Both documented default ports match the source declaration.",
      "known_debt": [],
      "required": true
    },
    {
      "profile_id": "documentation-current",
      "kind": "test",
      "command": [
        "tools/check-docs"
      ],
      "source_file": "tools/check-docs",
      "runtime": "repository-tool",
      "confidence": "high",
      "read_only": {
        "environment": {},
        "timeout_ms": 10000,
        "passed_exit_code": 0,
        "failed_exit_code": 1,
        "document": {
          "scope": [
            {
              "kind": "exact",
              "path": "README.md"
            }
          ],
          "condition": "The default port documented in README.md matches src/service.py#default_port."
        }
      }
    }
  ]
}
```
