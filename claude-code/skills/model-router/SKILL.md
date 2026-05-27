---
name: model-router
description: Guidance for delegating tasks to the right model tier to balance cost and capability. Apply at the start of any non-trivial task that could plausibly be split across cheaper subagents.
---

# Model Router

A decision rubric for the main thread to pick *when* and *to whom* to delegate, so cheap work runs on Haiku and only hard work pays for Opus.

## The three tiers

| Tier   | Model  | Use for                                                                   |
| ------ | ------ | ------------------------------------------------------------------------- |
| Cheap  | Haiku  | Single-file reads, targeted greps, "where is X" lookups, existence checks |
| Medium | Sonnet | Routine coding, multi-file edits, standard refactors, test writing        |
| Heavy  | Opus   | Architecture decisions, gnarly debugging, novel design, deep review       |

## Decision flow

Before starting any task, ask in order:

1. **Narrow lookup with a clear answer?** → Delegate to the `cheap-lookups` agent (Haiku).
2. **Open-ended exploration across many files?** → Delegate to the `Explore` agent (Haiku-pinned).
3. **Routine implementation where the design is obvious?** → Stay on the main thread if already Sonnet; otherwise delegate to a Sonnet subagent.
4. **Real reasoning — tricky bug, design tradeoff, code that smells wrong?** → Stay on Opus / escalate.

## When NOT to delegate

Delegation has overhead. Don't route to a subagent when:

- The task takes fewer than ~3 tool calls anyway (delegation cost exceeds savings).
- You need to act on the result with the *same* context you already have loaded.
- The output format matters and you'd have to re-format the subagent's reply.
- The session is short — model-switching busts the prompt cache, which is model-specific.

## Cache awareness

The Anthropic prompt cache is per-model. Bouncing between Haiku/Sonnet/Opus on a long session can cost *more* than staying on one model. Rough rule: only route if the subagent's work would have added 5K+ tokens to your main context.

## What this is NOT

This is a decision aid, not an autonomous router. The main thread still does the dispatching — this skill just supplies the rubric.
