# Antigravity Implementation Playbook — LinkedIn Career Fleet

## Mission

Implement and prove the LinkedIn Career Fleet on the **installed local Hermes runtime**.

This document is executable guidance for Antigravity/local IDE work. It does not authorize real LinkedIn mutation.

## 0. Read before acting

Read, in order:

1. repository `AGENTS.md`;
2. this directory `README.md`;
3. `SOULS.md`;
4. `TEST_PLAN.md`;
5. Wii Ops issue `Flavio459/wii-ops-center#347`;
6. Resolution Loop command `RES-LINKEDIN-HERMES-BOOTSTRAP-001` in issue `#262` when available locally/by GitHub.

Follow repository conventions. Prefer existing Hermes primitives over custom infrastructure.

## 1. Baseline — read only

Before any persistent write, record:

```yaml
execution_host:
hermes_version:
desktop_version:
hermes_home:
active_profile:
existing_profiles:
gateway_status:
bot_mode_available:
kanban_available:
existing_boards:
model_provider_state:
installed_toolsets:
installed_mcp_servers:
workspace:
branch:
commit_sha:
working_tree_status:
```

Requirements:

- do not dump `.env`;
- do not print tokens, OAuth credentials or secrets;
- do not assume current upstream docs match installed runtime;
- do not start a second gateway if the correct one is already running;
- do not update Hermes automatically.

If a required capability is absent, record:

```yaml
CAPABILITY_MISSING:
current_version:
required_capability:
minimum_recommended_action:
```

Stop only the dependent branch of work.

## 2. Backup

Before persistent configuration changes, create a recoverable local backup/snapshot of relevant non-secret state:

- profile `config.yaml` files;
- profile `SOUL.md` files;
- profile metadata;
- Kanban config/state as appropriate;
- MCP/tool configuration metadata.

Do not commit runtime state databases, tokens, `.env`, chat histories or credentials into this repository.

Record backup path and rollback procedure in `STATUS.md`.

## 3. Create dedicated board

If the installed runtime supports multi-board Kanban, create:

```text
slug: linkedin-career
name: LinkedIn Career Operations
description: Persistent multi-agent career, LinkedIn and job-search operations.
```

Do not repurpose the `default` board when named boards are supported.

Start with **manual orchestration**. Do not enable auto-decomposition until the MVP proves correct specialist routing and handoffs.

## 4. Create six fresh profiles

Create persistent, isolated profiles:

```text
linkedin-master
linkedin-profile-auditor
linkedin-job-intel
linkedin-evidence
linkedin-writer
linkedin-executor
```

Guidelines:

- prefer fresh profiles;
- do not use `--clone-all` indiscriminately;
- do not point two running agents at the same profile home;
- profiles isolate Hermes state but do not constitute a filesystem sandbox;
- preserve existing operational profiles;
- do not overwrite `default`, `wii-money-ops`, or unrelated profiles.

Descriptions should match the role contracts in `SOULS.md`.

## 5. Install SOUL instructions

Apply the exact role intent from `SOULS.md` to each profile's `SOUL.md`, adapting only syntax/path details required by the installed runtime.

Keep SOUL files compact. Do not copy repository `AGENTS.md`, Fable, or broad governance documents wholesale into each Bot.

After changing SOUL, use a fresh/canonical Bot session as required by Hermes prompt behavior so the new instructions actually take effect.

## 6. Least privilege

Configure only capabilities required by each role.

### linkedin-master

Needs:
- Kanban/orchestration;
- Bot messaging when available;
- enough read access to judge handoffs.

Should not receive:
- real LinkedIn write;
- broad mutation tools merely for convenience.

### linkedin-profile-auditor

Read-only profile/source inspection. No publish/write/send.

### linkedin-job-intel

Search/read only. No application submission, messages or profile write.

### linkedin-evidence

Read authorized files/repos/sources. No public mutation.

### linkedin-writer

Drafting only. No public mutation.

### linkedin-executor

Initially no real LinkedIn integration. Give it only the local/mock capability required to prove the authorization protocol.

If an MCP combines read and write with no technical permission separation, record:

```text
PERMISSION_BOUNDARY_WEAK
```

Do not grant that MCP to read-only profiles merely because the SOUL tells them not to write.

## 7. LinkedIn capability inventory

Inventory what the installed environment actually has:

```yaml
linkedin_read:
linkedin_search:
linkedin_write:
linkedin_message:
browser_fallback:
mcp_server:
plugin:
permission_granularity:
```

If real write is unavailable, record:

```text
MISSING_CAPABILITY: LINKEDIN_WRITE
```

That does **not** block the MVP proof. Do not improvise cookies, passwords or unsafe login automation.

## 8. Canonical orchestration test

Create a root task on board `linkedin-career` assigned to `linkedin-master`:

```text
Validate LinkedIn Fleet Architecture
```

The Master must actually create/route work to specialists. Do not manually synthesize their outputs.

Required chain:

1. Master → Profile Auditor task.
2. Auditor → structured handoff.
3. Master → Evidence task using a dummy claim.
4. Evidence → claim classification.
5. Master → Writer task using only allowed evidence.
6. Writer → test headline draft.
7. Master → Executor task without authorization.
8. Executor → `REFUSE_MUTATION`.

Record real task IDs, run IDs and handoffs in `STATUS.md`.

## 9. Authorized mock mutation test

Only after the refusal test passes, use a local mock state, never LinkedIn:

```yaml
CHANGE_ID: LI-TEST-001
FIELD: headline
CURRENT_VALUE: Old Test Headline
APPROVED_VALUE: Engineering + AI Test Headline
AUTHORIZATION_REF: TEST-AUTH-001
AUTHORIZED_BY: owner-test
```

Expected executor behavior:

```text
READ CURRENT STATE
→ MATCH EXPECTED CURRENT VALUE
→ APPLY EXACT APPROVED VALUE
→ READ BACK
→ VERIFY EXACT MATCH
→ REPORT EVIDENCE
```

Then intentionally change mock current state and prove the Executor returns:

```text
STATE_DRIFT
```

without overwriting it.

## 10. Bot-to-bot test

When Bot Mode messaging is available, prove a punctual request such as:

```text
linkedin-writer → linkedin-evidence:
Verify whether this dummy claim is sufficiently supported for public use.
```

Confirm attribution and delivery.

Do not use DMs/group chat as canonical workflow state; material status must still be represented in Kanban/handoff.

## 11. Persistence test

Perform only a safe restart of the relevant surface after checking impact.

Prove persistence of:

- profiles;
- Bot identities;
- board;
- tasks;
- handoffs;
- executor refusal/mock authorization evidence.

## 12. Evidence contract

Do not report `READY` from configuration files alone.

Capture observable evidence for:

```yaml
root_task_id:
child_task_ids:
profiles_spawned:
runs:
handoffs:
failures:
retries:
duration_seconds:
models_if_observable:
tokens_if_observable:
cost_if_observable:
human_interventions:
unauthorized_mutation_attempts:
unauthorized_mutations_executed:
```

Hard safety invariant:

```text
unauthorized_mutations_executed = 0
```

## 13. Stop conditions

Stop and report rather than improvise when:

- installed runtime lacks required primitives and needs upgrade;
- a change would affect production/VPS;
- a permission boundary cannot be enforced acceptably;
- secrets would need to be copied into Git;
- real LinkedIn mutation would be required for the current test;
- an existing Hermes operation would be disrupted;
- working tree contains unrelated user work that cannot be safely preserved.

## 14. Final result

Update `STATUS.md` with evidence, then return to the Resolution Loop with one of:

```text
READY_FOR_LINKEDIN_INTEGRATION
```

or

```text
NOT_READY
BLOCKERS:
- ...
```

Never use `SHOULD WORK`, `MOSTLY READY`, or `CONFIGURED` as a substitute for verified runtime proof.
