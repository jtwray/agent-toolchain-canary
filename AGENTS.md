# Agent guidance

Keep the canary independent of product repositories. Never add secrets, local configuration, reports, state, logs, or machine-specific paths to Git. Probe commands must be read-only and allowlisted. The Node engine owns classification, redaction, locking, cleanup, and reporting. Scheduling adapters only invoke that engine. Run `npm test` and `npm run canary:dry` before changing scheduler behavior.
