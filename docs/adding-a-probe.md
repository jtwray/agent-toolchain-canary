# Adding a probe

Use a stable ID and layer. Return `pass`, `fail`, `skipped`, or `inconclusive` with sanitized evidence and a stable failure signature. Add only harmless read-only operations to the command allowlist; never accept configured arbitrary shell commands. Enforce a timeout and clean listeners/children in `finally`. Add deterministic tests for failure, timeout, interruption, cleanup, and redaction. Avoid usernames, paths, credential values, and provider responses in output.
