# QuantDinger + Claude Code Operator Blueprint (v4)

# Purpose

This document defines the OVERALL ARCHITECTURE and OPERATING PHILOSOPHY for building a Claude-Code-driven local AI operator workflow around QuantDinger.

This blueprint intentionally separates:

1. DEVELOPMENT MODE
2. OPERATION MODE

These MUST remain logically separated.

---

# System Vision

Target workflow:

```text
Claude Code OAuth / subscription
+ QuantDinger repo
+ CLAUDE.md operating constitution
+ local workflow scripts
+ QuantDinger Agent Gateway / MCP
+ optional manual LLM bridge
+ optional Moomoo OpenD adapter
+ paper-first execution
```

This system is intentionally:

```text
local-first
human-in-the-loop
paper-first
safety-first
reviewable
git-driven
non-autonomous-by-default
```

This system is NOT intended to become:

```text
unattended live trading agent
continuously self-modifying AI system
fully autonomous execution engine
```

---

# Two-Folder Local Architecture

Use TWO separate local clones.

Recommended structure:

```text
~/projects/quantdinger-dev
~/projects/quantdinger-ops
```

This separation is intentional and important.

---

## quantdinger-dev

Purpose:
- development
- implementation
- architecture work
- feature branches
- Claude Code modifications
- integration testing

Default mode:

```text
DEVELOPMENT MODE
```

Allowed branches:
- dev
- feature/*
- main only for release merge

This folder SHOULD:
- contain unstable work
- contain experiments
- contain integrations in progress

This folder SHOULD NOT:
- be used for stable operational workflows
- be used for production-like execution
- be used for stable paper/live trading

---

## quantdinger-ops

Purpose:
- stable research workflows
- reports
- backtests
- paper trading
- eventual stable operations

Default mode:

```text
OPERATION MODE
```

Allowed branch:

```text
main only
```

This folder SHOULD:
- remain stable
- remain operational
- consume only tested releases

This folder SHOULD NOT:
- run development work
- checkout feature branches
- contain architecture refactors
- contain unstable integrations

---

# Promotion Flow

Recommended release flow:

```text
feature/* → dev → test → main
                               ↓
                    quantdinger-ops pulls main
```

Operations repo only consumes stable `main`.

---

# Architecture Philosophy

## QuantDinger

QuantDinger is the:
- strategy runtime
- backtesting platform
- dashboard
- research engine
- execution controller
- MCP / Agent Gateway host

QuantDinger should remain relatively stable.

Prefer:
- wrappers
- adapters
- plugins
- local scripts

Avoid:
- unnecessary deep core rewrites

---

## Claude Code

Claude Code acts as:
- AI operator
- AI researcher
- AI coding assistant
- workflow orchestrator
- report generator
- strategy generator

Claude Code is NOT:
- the broker
- the execution authority
- the final approval layer

The USER remains the final approval authority.

---

# Two Distinct Modes

# DEVELOPMENT MODE

Purpose:
- modify source code
- add integrations
- add adapters
- add workflows
- improve tooling
- improve reporting
- improve safety systems

Primary references:

```text
CLAUDE.md
docs/local_operator/development_plan.md
```

Default assumptions:

```text
repo modification only
no operation workflows
no broker execution
```

Development mode SHOULD:
- work incrementally
- use feature branches
- summarize modifications
- preserve upstream compatibility

Development mode SHOULD NOT:
- place trades
- create unattended loops
- rewrite unrelated systems

---

# OPERATION MODE

Purpose:
- run research workflows
- generate reports
- generate strategies
- run backtests
- optionally run paper trades

Primary references:

```text
CLAUDE.md
docs/local_operator/operation_workflow.md
ai_workflows/*
```

Operation mode SHOULD:
- use existing interfaces
- use stable workflows
- produce reviewable artifacts

Operation mode SHOULD NOT:
- modify architecture
- rewrite infrastructure
- change safety systems
- change adapters

---

# CLAUDE.md Philosophy

`CLAUDE.md` is CRITICAL.

Claude Code heavily follows this file.

Therefore:

`CLAUDE.md` MUST remain:

```text
short
stable
high-level
constitutional
mode-routing
safety-focused
```

It should function as:

```text
operating constitution
behavioral constraint layer
mode router
project-wide safety policy
```

It should NOT become:

```text
implementation roadmap
large prompt dump
massive workflow spec
```

Detailed implementation belongs elsewhere.

---

# Expected CLAUDE.md Structure

Recommended structure:

```text
Project Identity
Role Definition
Default Safety Rules
Local Folder Discipline
Mode Separation
Branch Discipline
Development Rules
Operation Rules
Approval Phrases
Forbidden Actions
Output Expectations
Git Discipline
```

---

# Expected CLAUDE.md Content

## Project Identity

Example:

```md
You are operating inside the QuantDinger local AI operator project.
```

---

## Role Definition

Example:

```md
You may act as:
- software engineer
- workflow orchestrator
- AI researcher
- report generator

You are NOT the final execution authority.
```

---

## Default Safety Rules

Example:

```md
- Default to paper trading only.
- Never place live trades unless explicitly approved.
- Never modify secrets unless explicitly instructed.
- Never expose credentials.
- Never bypass approval systems.
```

---

## Local Folder Discipline

Example:

```md
If current path contains `quantdinger-dev`, assume DEVELOPMENT MODE.

If current path contains `quantdinger-ops`, assume OPERATION MODE.

Never run stable operations from quantdinger-dev.

Never perform development/refactoring work from quantdinger-ops.
```

---

## Mode Separation

Example:

```md
Two modes exist:

1. DEVELOPMENT MODE
2. OPERATION MODE
```

---

## Branch Discipline

Recommended branch model:

```text
main
  stable operational branch

dev
  integration/staging

feature/*
  isolated implementation work

ops-experiment/*
  operational workflow experimentation
```

---

## Development Rules

Example:

```md
During DEVELOPMENT MODE:
- work incrementally
- keep changes scoped
- summarize files changed
- avoid unrelated modifications
```

---

## Operation Rules

Example:

```md
During OPERATION MODE:
- generate reports
- validate strategies
- run backtests
- stop before live execution unless approved
```

---

## Approval Phrases

Recommended:

| Action | Phrase |
|---|---|
| Paper trade | RUN PAPER TRADE |
| Live trade | EXECUTE LIVE TRADE |
| Modify secrets | MODIFY SECRETS |
| Modify risk limits | MODIFY RISK LIMITS |

---

## Forbidden Actions

Recommended:

```md
Forbidden unless explicitly approved:
- live trading
- destructive shell commands
- deleting repositories
- force pushing
- bypassing validation
- unattended execution loops
```

---

## Output Expectations

Claude Code should summarize:

```text
files changed
commands run
risks
how to test
rollback considerations
```

---

## Git Discipline

Recommended:

```md
- Never commit directly to main.
- Never force push.
- Prefer feature branches.
- Keep commits scoped.
- Preserve upstream compatibility where possible.
```

---

# Repository Strategy

Recommended structure:

```text
upstream QuantDinger
        ↓
your fork
        ↓
main
        ↓
dev
        ↓
feature/*
```

---

# Upstream Sync Philosophy

Use:
- your own fork
- upstream remote

Recommended remotes:

```text
origin   = your fork
upstream = original QuantDinger repo
```

Regularly sync upstream.

Prefer:
- wrappers
- adapters
- plugins
- local scripts

Avoid:
- deep core rewrites
- unnecessary auth changes
- unnecessary schema changes

---

# Recommended Repo Layout

```text
CLAUDE.md

docs/local_operator/
  development_plan.md
  operation_workflow.md
  safety_rules.md
  manual_llm_bridge.md
  moomoo_adapter_design.md

ai_workflows/
  market_analysis.md
  strategy_generation.md
  backtest_review.md
  report_generation.md
  moomoo_execution_checklist.md

scripts/ai_operator/

strategies/generated/

reports/

backtests/

data/ai_snapshots/
```

---

# Development Philosophy

Build in this order:

```text
observe
analyze
generate
validate
backtest
report
paper trade
live trade
```

Never skip:
- validation
- backtesting
- reporting
- approval gates

before execution.

---

# Final Target State

Desired workflow:

```text
You ask Claude Code for research or strategy work
→ Claude Code uses QuantDinger locally
→ strategies/reports generated
→ validation + backtest performed
→ report generated
→ user optionally approves paper trade
→ live trading remains disabled by default
```
