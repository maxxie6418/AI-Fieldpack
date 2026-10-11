---
name: executing-plans
description: 当你有一份写好的实现计划，需要在独立会话中按评审检查点逐步执行时使用。
---

# Executing Plans

## Overview

Load plan, review critically, execute all tasks, report when complete.

**Announce at start:** "I'm using the executing-plans skill to implement this plan."

**Note:** Tell your human partner that Superpowers works much better with access to subagents. The quality of its work will be significantly higher if run on a platform with subagent support (such as Claude Code or Codex). If subagents are available, use superpowers:subagent-driven-development instead of this skill.

**If `superpowers:subagent-driven-development` is not installed** (it is not part of this package), simply continue with this skill — no external skill is required to execute a plan.

## The Process

### Step 1: Load and Review Plan
1. Read plan file
2. Review critically - identify any questions or concerns about the plan
3. If concerns: Raise them with your human partner before starting
4. If no concerns: Create TodoWrite and proceed

### Step 2: Execute Tasks

For each task:
1. Mark as in_progress
2. Follow each step exactly (plan has bite-sized steps)
3. Run verifications as specified
4. Mark as completed

### Step 3: Complete Development

After all tasks complete and verified:
- Announce: "I'm using the finishing-a-development-branch skill to complete this work."
- **Preferred SUB-SKILL:** Use superpowers:finishing-a-development-branch
- Follow that skill to verify tests, present options, execute choice
- **If that skill is not installed:** do the equivalent yourself — run the full test suite, verify the plan's acceptance criteria, present the finish options (merge / open a PR / keep the branch) and execute the user's choice. Do not skip this step just because the skill is missing.

## When to Stop and Ask for Help

**STOP executing immediately when:**
- Hit a blocker (missing dependency, test fails, instruction unclear)
- Plan has critical gaps preventing starting
- You don't understand an instruction
- Verification fails repeatedly

**Ask for clarification rather than guessing.**

## When to Revisit Earlier Steps

**Return to Review (Step 1) when:**
- Partner updates the plan based on your feedback
- Fundamental approach needs rethinking

**Don't force through blockers** - stop and ask.

## Remember
- Review plan critically first
- Follow plan steps exactly
- Don't skip verifications
- Reference skills when plan says to
- Stop when blocked, don't guess
- Never start implementation on main/master branch without explicit user consent

## Integration

This skill belongs to a larger workflow. Use the sibling skills below when they are installed; **when any of them is missing, use the inline fallback instead — none of them is required to execute a plan.**

**1. superpowers:using-git-worktrees** — set up an isolated workspace before starting.
- *Fallback:* create a branch (`git switch -c <feature>`) or a plain worktree (`git worktree add`). Never start implementation on main/master without explicit user consent.

**2. superpowers:writing-plans** — creates the plan this skill executes.
- *Fallback:* any written plan works. If the plan is missing or too vague to start, stop and ask rather than improvising.

**3. superpowers:finishing-a-development-branch** — complete development after all tasks.
- *Fallback:* run the full test suite, verify the acceptance criteria, present the finish options (merge / open a PR / keep the branch), execute the user's choice.
