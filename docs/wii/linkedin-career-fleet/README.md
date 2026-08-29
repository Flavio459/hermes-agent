# LinkedIn Career Fleet — Hermes

Status: **SPECIFIED / NOT YET PROVEN IN RUNTIME**

Owner authorization: 2026-08-29

Operational coordination:
- Wii Ops Center issue: `Flavio459/wii-ops-center#347`
- Resolution Loop command: `RES-LINKEDIN-HERMES-BOOTSTRAP-001` in `Flavio459/wii-ops-center#262`

## Purpose

Configure a persistent Hermes multi-Bot fleet for LinkedIn career operations without turning one general agent into a monolith.

The system must use native Hermes primitives:

- **Profiles / Bot Mode** for persistent specialist identities;
- **Kanban** for durable tasks, dependencies, handoffs and audit trail;
- **`message_agent` / @mentions** for punctual bot-to-bot communication;
- **`delegate_task`** only for temporary child work inside a specialist;
- **Routines/Cron** only for recurring work that is later explicitly approved.

This packet is an implementation overlay for this fork. It must not require a special-case modification to Hermes core.

## MVP fleet

1. `linkedin-master`
2. `linkedin-profile-auditor`
3. `linkedin-job-intel`
4. `linkedin-evidence`
5. `linkedin-writer`
6. `linkedin-executor`

Dedicated board, when supported by the installed runtime:

```text
slug: linkedin-career
name: LinkedIn Career Operations
```

## Canonical flow

```text
USER OBJECTIVE
    ↓
linkedin-master
    ↓
KANBAN ROOT TASK
    ↓
SPECIALIST TASK(S)
    ↓
STRUCTURED HANDOFF
    ↓
linkedin-master evaluation
    ↓
HUMAN APPROVAL when material
    ↓
linkedin-executor
    ↓
READ-BACK VERIFICATION
    ↓
REPORT / AUDIT TRAIL
```

## Safety boundary

The current authorization does **not** include:

- changing the real LinkedIn profile;
- publishing posts;
- sending messages or connection requests;
- capturing/importing LinkedIn cookies or credentials;
- updating Hermes automatically;
- changing OmniRoute/provider routing unless separately authorized;
- moving this fleet to VPS/production;
- creating additional bots beyond the MVP.

The `linkedin-executor` must initially have **no real LinkedIn write capability**. Its mutation contract is first proven against a mock file/state only.

## Separation of responsibility

- The Master orchestrates; it does not replace specialists.
- The Auditor reads and diagnoses; it does not write.
- Job Intel researches; it does not apply.
- Evidence verifies claims; it does not rewrite facts to sound stronger.
- Writer drafts from approved facts; it does not publish.
- Executor mutates only exact, explicitly authorized values.

## Source of truth

Workflow state belongs in Kanban once the fleet is running. Bot chats are communication surfaces, not the canonical state store.

This repository packet defines the intended configuration and tests. The local Hermes runtime is the source of truth for what is actually installed/configured. Do not claim implementation merely because these files exist.

## Files in this packet

- `IMPLEMENTATION.md` — steps for Antigravity/local executor.
- `SOULS.md` — standing instructions for each profile.
- `TEST_PLAN.md` — deterministic acceptance and safety tests.
- `STATUS.md` — runtime evidence ledger; update only with observed facts.

## Definition of ready

The fleet may be called `READY_FOR_LINKEDIN_INTEGRATION` only after all gates in `TEST_PLAN.md` pass with runtime evidence and the real LinkedIn account remains untouched.
