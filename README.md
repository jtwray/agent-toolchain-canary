# Agent Toolchain Canary

A public, standalone template for checking the developer toolchain from the current user's machine. It checks Node/npm/Git/CLI availability, read-only GitHub access, HTTPS endpoints, and a loopback HTML fixture. Optional Netlify CLI status is separate from deployment identity. Results are redacted, classified across runs, and kept only in ignored `local/` storage.

## Five-minute setup

1. Clone this template to a directory you control and run `npm ci` (Node 20+).
2. Copy `config/canary.config.example.json` to `local/config.json`. The `local/` directory is ignored. Set your own repository, endpoint, and provider names; never enter a secret value.
3. Run `npm test`, `npm run canary:dry`, `npm run auth:doctor`, and `npm run canary`.
4. Inspect `npm run schedule:plan` and install with `npm run schedule:install -- --confirm`.
5. Check `npm run schedule:status`. Remove only this canary schedule with `npm run schedule:remove -- --confirm`.

Default schedule: Monday at 09:00 local time. The scheduler runs the absolute Node executable and this CLI as the current user. It never pulls, installs, deploys, or modifies tracked files. A lock prevents overlap. Confirmed probe failures produce a nonzero exit code; optional absent Netlify CLI is skipped. Reports are JSON in `local/reports/` and readable Markdown through `npm run report`.

## Authentication

HTTPS users can sign into GitHub CLI and Git Credential Manager in their own account. SSH users can load their own key into ssh-agent and select `ssh`. CI users can supply a named environment variable externally and select `environment`. The canary checks presence and harmless access; it never reads key files or credential-helper responses. Scheduler environments may not inherit SSH agent sockets or interactive environment variables. See [authentication](docs/authentication.md).

## Scheduling

Windows uses Task Scheduler with an interactive current-user token, no stored password, and one task named `Agent Toolchain Canary`. macOS uses a user LaunchAgent. Linux prefers a user systemd timer and falls back to a tagged user crontab entry. Git Bash is only a convenient manual wrapper and is not a Windows cron service. Inspect exact plans with `npm run schedule:plan -- --platform=win32` (or `darwin`, `linux`, `cron`). See [scheduling](docs/scheduling.md).

## Incidents and limits

The first distinct failure is a candidate; the same signature in two consecutive runs is recurring. A previously failing path that passes once is recovered; two passing runs mark it as a retirement candidate. Humans approve durable compatibility guidance changes. The canary never edits that guidance or opens issues.

An ordinary Node process started by Task Scheduler, launchd, systemd, or cron cannot directly invoke Codex connected plugins or Codex desktop screenshot/viewport tooling. Connected Netlify-plugin deployment identity and Codex browser/screenshot behavior remain optional manual or agent-assisted checks. The automatic suite does not claim to test them. See [compatibility](docs/integration-compatibility.md), [operations](docs/operations.md), and [adding a probe](docs/adding-a-probe.md).
