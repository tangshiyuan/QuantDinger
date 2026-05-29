# QuantDinger + Claude Code Development Plan (v4)

# Purpose

This document governs DEVELOPMENT MODE ONLY.

It defines HOW Claude Code should modify and extend the QuantDinger repo safely.

This document is NOT the operation workflow.

---

# Local Folder Discipline

There should be TWO separate local clones.

Recommended structure:

```text
~/projects/quantdinger-dev
~/projects/quantdinger-ops
```

---

## quantdinger-dev

Purpose:
- development
- feature implementation
- integrations
- experiments
- architecture work

Default mode:

```text
DEVELOPMENT MODE
```

Use:
- dev branch
- feature branches

Do NOT use this folder for stable operational workflows.

---

## quantdinger-ops

Purpose:
- stable workflows
- reports
- backtests
- paper trading
- operational usage

Default mode:

```text
OPERATION MODE
```

Branch:

```text
main only
```

Do NOT perform development/refactoring work here.

---

# Promotion Flow

Recommended release flow:

```text
feature/* → dev → test → main
                               ↓
                    quantdinger-ops pulls main
```

---

# Updating Ops Clone

Recommended ops update flow:

```bash
cd ~/projects/quantdinger-ops
git checkout main
git pull origin main
docker compose up -d --build
```

Ops clone should consume ONLY stable `main`.

---

# Mode Discipline

This project intentionally separates:

1. DEVELOPMENT MODE
2. OPERATION MODE

---

# DEVELOPMENT MODE

Claude Code SHOULD:
- inspect architecture
- modify source code
- add integrations
- add scripts
- improve workflows
- improve reporting

Claude Code SHOULD NOT:
- run live trades
- create unattended loops
- autonomously execute strategies
- continuously self-modify workflows

Default assumptions:

```text
research-only
backtest-first
paper-only
human approval required
```

---

# OPERATION MODE

Operation workflows belong in:

```text
docs/local_operator/operation_workflow.md
```

This file should contain:
- daily workflows
- analysis workflows
- report workflows
- backtest workflows
- paper trade workflows

It should NOT contain:
- implementation details
- architecture refactors
- infrastructure changes

---

# Switching Modes

The USER controls the active mode.

---

## DEVELOPMENT MODE requests

Examples:

```text
Implement Phase 2
Modify the Moomoo adapter
Refactor the validator
Add workflow scripts
```

---

## OPERATION MODE requests

Examples:

```text
Analyze NVDA
Generate a strategy report
Run paper trade workflow
```

If ambiguous:
- default to DEVELOPMENT MODE

---

# Repository Strategy

Recommended setup:

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

# Branch Discipline

## main

Purpose:

```text
stable operational branch
```

Use for:
- operations
- reports
- backtests
- paper trading

Avoid development work here.

---

## dev

Purpose:

```text
integration/staging branch
```

Use for:
- integrating features
- staging systems
- compatibility testing

---

## feature/*

Purpose:

```text
isolated implementation work
```

Claude Code should mostly work here.

Examples:

```text
feature/manual-llm-bridge
feature/moomoo-opend
feature/report-system
```

---

## ops-experiment/*

Purpose:

```text
operational workflow experimentation
```

Use for:
- prompt experimentation
- workflow experimentation
- report experimentation

WITHOUT contaminating stable operational flows.

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

# CLAUDE.md Expectations

CLAUDE.md MUST remain:

```text
short
stable
constitutional
high-level
```

It should contain:
- role definition
- safety rules
- local folder discipline
- mode routing
- branch discipline
- approval phrases
- forbidden actions
- git discipline

It should NOT contain:
- massive implementation specs
- huge prompt dumps
- architecture deep dives

---

# Recommended CLAUDE.md Sections

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

# Important Context

QuantDinger already includes:
- Agent Gateway
- MCP support
- strategy systems
- backtesting systems

Implementation should EXTEND controlled interfaces.

Do NOT bypass safety systems.

---

# Phase 0 — Repository Inspection

## Goal

Understand repository BEFORE modifications.

---

## Tasks

Inspect:
- README
- docker-compose
- backend structure
- docs/agent/
- strategy modules
- backtest modules
- Agent Gateway
- MCP integrations
- broker adapters

Produce:

```text
docs/local_operator/REPO_INSPECTION.md
```

---

## Rules

Do NOT:
- modify source code
- touch .env
- touch secrets
- place orders

---

# Phase 1 — Add Governance & Workflow Structure

## Goal

Create governance layer.

---

## Files

```text
CLAUDE.md

docs/local_operator/
  development_plan.md
  operation_workflow.md
  safety_rules.md
  manual_llm_bridge.md

ai_workflows/
  market_analysis.md
  strategy_generation.md
  backtest_review.md
  report_generation.md
  moomoo_execution_checklist.md
```

---

## Acceptance Criteria

- CLAUDE.md exists
- mode separation explicit
- local folder discipline documented
- branch discipline documented
- safety rules documented

---

# Phase 2 — Add Safe AI Operator Scripts

## Goal

Provide safe repeatable scripts.

---

## Scripts

```text
scripts/ai_operator/
  create_agent_snapshot.py
  fetch_market_data.py
  validate_strategy.py
  run_backtest.py
  generate_report.py
  summarize_latest_run.py
```

---

## Requirements

Scripts must:
- fail safely
- log actions
- avoid destructive behavior
- avoid broker execution
- avoid secret exposure

---

# Phase 3 — Strategy Generation Workflow

## Goal

Allow Claude Code to generate strategies safely.

---

## Rules

Generated strategies:
- deterministic only
- no broker calls
- no network calls
- no credential access
- must pass validation

---

## Workflow

```text
generate strategy
→ validate
→ fix if needed
→ backtest
→ generate report
→ stop before execution
```

---

# Phase 4 — Manual LLM Bridge

## Goal

Optional copy-paste bridge.

---

## Flow

```text
generate prompt
→ paste externally
→ paste response back
→ parse result
→ save artifact
```

This is OPTIONAL.

Primary architecture:
- Claude Code as operator

NOT:
- embedded autonomous chat system

---

# Phase 5 — Agent Gateway / MCP Integration

## Goal

Use QuantDinger controlled interfaces safely.

---

## Rules

Use:
- scoped permissions
- minimum required access
- paper-only execution

Do NOT:
- bypass Agent Gateway
- bypass approval systems
- expose tokens

---

# Phase 6 — Moomoo OpenD Adapter

## Goal

Add paper-first Moomoo support.

---

## Default Env

```env
MOOMOO_LIVE_TRADING_ENABLED=false
```

---

## Live Trading Requirements

Live execution requires:
- explicit approval
- risk checks
- approval phrase
- logging

---

## Rules

Paper-first only.

No unattended live execution.

---

# Phase 7 — Reporting Integration

## Goal

Expose outputs cleanly.

Outputs:
- reports
- strategy files
- backtest artifacts
- approval status

---

# Phase 8 — End-to-End Dry Run

## Goal

Run full workflow WITHOUT live execution.

---

## Flow

```text
analyze
→ generate strategy
→ validate
→ backtest
→ generate report
→ optionally paper trade
```

Live trading remains disabled.

---

# Phase 9 — Optional Future API Migration

## Goal

Support future migration to:
- OpenRouter
- OpenAI API
- Anthropic API

without rewriting workflows.

---

## Provider Abstraction

```python
class LLMProvider:
    def generate(...)
```

Implement:
- ManualProvider
- OpenRouterProvider
- OpenAIProvider
- AnthropicProvider

---

# Recommended Claude Code Working Style

DO:
- work phase-by-phase
- summarize changes
- keep commits scoped
- preserve upstream compatibility
- prefer wrappers/adapters

DO NOT:
- implement everything at once
- create autonomous loops
- deeply rewrite core systems
- modify unrelated files

---

# Recommended Claude Code Prompt Pattern

Example:

```text
Read CLAUDE.md first.

You are in DEVELOPMENT MODE.

Implement Phase 2 only.

Before editing:
- summarize expected file changes

After editing:
- summarize files changed
- summarize commands run
- summarize risks
- explain how to test
```

---

# Non-Goals

Do NOT implement initially:

```text
fully autonomous live trading
high-frequency trading
continuous self-modifying agents
unattended execution
```

---

# Final Target State

Desired workflow:

```text
You ask Claude Code for research or strategy work
→ Claude Code uses QuantDinger locally
→ strategy/report generated
→ validation + backtest performed
→ report generated
→ user optionally approves paper trade
→ live trading disabled by default
```
