---
name: gateguard
description: "Fact-forcing gate: block Edit/Write before investigation. DENY→FORCE→ALLOW. Adapted from ECC gateguard with embedded-specific checks. Triggered by→subagent-driven-development, executing-plans, systematic-debugging. Signals: first edit to any file, hardware register write, peripheral config change"
---

# GateGuard — Fact-Forcing Pre-Action Gate

A PreToolUse gate that forces investigation before editing. Instead of self-evaluation ("are you sure?"), it demands concrete facts.

## Core Concept

LLM self-evaluation doesn't work. "Are you sure?" always gets "yes." But forcing concrete investigation changes output quality.

**Three-stage gate:**

```
1. DENY  — block the first Edit/Write attempt on a file
2. FORCE — list exactly which facts to gather
3. ALLOW — permit retry after facts are presented
```

## Gate Types

### Edit Gate (first edit per file)

Before editing `{file_path}`, gather and present:

1. **Importers** — list ALL files that `#include` or call functions from this file (use Grep)
2. **Public interface** — list the public functions/variables affected by this change
3. **Hardware context** — if this file touches peripheral registers, list the register addresses and which hardware blocks they belong to
4. **User instruction** — quote the user's current instruction verbatim

### Write Gate (new file creation)

Before creating `{file_path}`, gather and present:

1. **Callers** — name the file(s) and line(s) that will call/use this new file
2. **No duplication** — confirm no existing file serves the same purpose (use Glob)
3. **Hardware context** — if this file configures hardware, list affected peripherals and their current state
4. **User instruction** — quote the user's current instruction verbatim

### Destructive Bash Gate (every destructive command)

Triggers on: `rm -rf`, `git reset --hard`, `git push --force`, `make flash`, `openocd`, `stm32flash`, erase commands, fuse writes.

1. **Impact** — list all files/data/hardware this command will modify or erase
2. **Rollback** — write a one-line rollback or recovery procedure
3. **User instruction** — quote the user's current instruction verbatim

## Embedded-Specific Checks

When editing hardware-adjacent code, additionally verify:

- **Register shadow**: Does a shadow/backup register exist? Can the original value be restored?
- **Clock dependency**: Does this peripheral require a specific clock enabled before register access?
- **Interrupt state**: Should interrupts be disabled during the register write sequence?
- **DMA conflict**: Could this configuration conflict with an active DMA channel?
- **Pin mux**: Is the GPIO pin already claimed by another peripheral?

## Anti-Patterns

- **Don't use self-evaluation.** "Are you sure?" always gets "yes."
- **Don't skip the hardware context check.** Assuming a peripheral is in reset state when it isn't causes silent failures.
- **Don't gate every single Bash command.** Routine bash = once per session. Destructive bash = every time.

## When to Skip

- Adding a comment or log line (no functional change)
- Editing a file you just created in this same session (facts already known)
- Mechanical changes like renaming (facts established by prior investigation)

## Workflow Linkage

**Position in mcu-ironclad workflow:** Pre-edit quality gate, complementary to freeze and careful.

**Triggered by:**
- `subagent-driven-development` — Before first edit per task
- `executing-plans` — Before first edit per step
- `systematic-debugging` — Before any fix attempt (Phase 4)

**Relationship to other skills:**
- `freeze` restricts WHERE you can edit → gateguard ensures you know WHY and WHO YOU AFFECT before editing
- `careful` confirms destructive commands → gateguard forces investigation before the command even forms
- `verification-before-completion` checks after → gateguard investigates before
