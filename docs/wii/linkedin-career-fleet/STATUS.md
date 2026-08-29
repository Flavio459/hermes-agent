# LinkedIn Career Fleet — Runtime Status Ledger

Last specification update: 2026-08-29

Current state: **NOT YET IMPLEMENTED / RUNTIME PROOF PENDING**

Do not change this state based only on configuration files or plans.

## Coordination references

```yaml
wii_ops_issue: Flavio459/wii-ops-center#347
resolution_loop_issue: Flavio459/wii-ops-center#262
resolution_command: RES-LINKEDIN-HERMES-BOOTSTRAP-001
implementation_repo: Flavio459/hermes-agent
implementation_packet: docs/wii/linkedin-career-fleet/
```

## Runtime baseline

```yaml
execution_host: PENDING
hermes_version: PENDING
desktop_version: PENDING
hermes_home: PENDING
active_profile: PENDING
existing_profiles: PENDING
gateway_status: PENDING
bot_mode_available: PENDING
kanban_available: PENDING
existing_boards: PENDING
model_provider_state: PENDING
installed_toolsets: PENDING
installed_mcp_servers: PENDING
workspace: PENDING
branch: PENDING
commit_sha: PENDING
working_tree_status: PENDING
```

## Backup

```yaml
backup_created: PENDING
backup_path: PENDING
rollback_procedure: PENDING
secrets_committed: MUST_BE_FALSE
```

## Profiles

| Profile | Exists | Separate home | SOUL installed | Least privilege checked | Evidence |
|---|---|---|---|---|---|
| linkedin-master | PENDING | PENDING | PENDING | PENDING | PENDING |
| linkedin-profile-auditor | PENDING | PENDING | PENDING | PENDING | PENDING |
| linkedin-job-intel | PENDING | PENDING | PENDING | PENDING | PENDING |
| linkedin-evidence | PENDING | PENDING | PENDING | PENDING | PENDING |
| linkedin-writer | PENDING | PENDING | PENDING | PENDING | PENDING |
| linkedin-executor | PENDING | PENDING | PENDING | PENDING | PENDING |

## Kanban

```yaml
board_linkedin_career_exists: PENDING
manual_orchestration: PENDING
root_task_id: PENDING
child_task_ids: PENDING
handoffs_proven: PENDING
```

## Tests

| Test | Status | Evidence |
|---|---|---|
| Runtime baseline | PENDING | |
| Six profiles | PENDING | |
| Dedicated board | PENDING | |
| Master delegates | PENDING | |
| Evidence gate | PENDING | |
| Writer respects evidence | PENDING | |
| Executor refuses unauthorized mutation | PENDING | |
| Authorized mock mutation | PENDING | |
| State drift fail-closed | PENDING | |
| Bot-to-bot messaging | PENDING | |
| Persistence | PENDING | |
| Permission boundary audit | PENDING | |

## Telemetry

```yaml
profiles_spawned: PENDING
runs: PENDING
handoffs: PENDING
failures: PENDING
retries: PENDING
duration_seconds: PENDING
model_provider_per_profile: PENDING
tokens: PENDING
cost: PENDING
human_interventions: PENDING
unauthorized_mutation_attempts: PENDING
unauthorized_mutations_executed: PENDING
```

Hard invariant after testing:

```text
unauthorized_mutations_executed = 0
```

## LinkedIn integration inventory

```yaml
linkedin_read: PENDING
linkedin_search: PENDING
linkedin_write: PENDING
linkedin_message: PENDING
browser_fallback: PENDING
mcp_server: PENDING
plugin: PENDING
permission_granularity: PENDING
```

## Blockers

```text
PENDING RUNTIME BASELINE
```

## Final readiness

```text
NOT_READY
```

Only change to `READY_FOR_LINKEDIN_INTEGRATION` after the acceptance tests in `TEST_PLAN.md` have runtime evidence.
