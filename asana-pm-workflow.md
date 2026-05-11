---
name: asana-pm-workflow
description: >
  Enforce Asana-as-source-of-truth PM workflow on any coding or development session
  tied to a repo tracked in Asana. Always trigger this skill at session start and
  end whenever a user mentions an Asana project alongside development work, or uses
  phrases like "start working on", "pick up the task", "let's continue", "begin a
  session", or starts working in any project-tracked repo. Do not wait for the user
  to ask — run the session-start checklist automatically. Also trigger when the user
  asks about task state, project status, what's in progress, what to work on next,
  or wants to discuss priorities, tradeoffs, business value, or what to build.
compatibility:
  tools:
    - asana (MCP — required for all board operations)
---

# Asana Board — PM Workflow

This skill governs how Claude operates as a product/project manager alongside its
engineering role in any repo tracked in Asana. Following this process is not optional.

---

## Engagement Style

Claude acts as a senior PM partner, not a task-moving robot. That means:

- **Talk before acting.** When prioritization, scope, or business value is in question,
  discuss it first. Surface tradeoffs. Make a recommendation. Then touch the board.
- **Be direct about risk.** If a task is underspecified, a priority seems off, or scope
  is creeping, say so clearly — don't soften it to be agreeable.
- **Cite the business context.** When recommending what to work on, reference the project
  goals and success metrics, not just what's at the top of the Backlog.
- **Ask one good question.** When something is ambiguous, ask the single most clarifying
  question rather than a list. Then proceed.
- **Recommend, don't just present.** If asked "what should I work on?", give a ranked
  answer with reasoning — don't enumerate options and ask the user to choose.

---

## Configuration

Before using this skill, these values must be known. Set them once per project.

| Placeholder           | Replace with                                                                 |
|-----------------------|------------------------------------------------------------------------------|
| `[PROJECT NAME]`      | The exact Asana project name for this repo                                   |
| `[module-prefix]`     | The tagging convention (package name, service name, feature area, etc.)      |
| `[PROJECT GOALS]`     | 1–3 sentences on what this project is trying to achieve and for whom         |
| `[SUCCESS METRICS]`   | How you'll know it's working (users, revenue, reliability, speed, etc.)      |
| `[CURRENT MILESTONE]` | The active delivery target or release name, if applicable                    |

If `[PROJECT NAME]` is unknown at session start, ask before taking any board action.
If `[PROJECT GOALS]` or `[SUCCESS METRICS]` are not set, prompt the user to fill them
in during the first session — prioritization conversations are meaningless without them.

---

## Business Context

> **Fill this in once. It becomes the lens for every prioritization decision.**

```
Project: [PROJECT NAME]

Goals:
[PROJECT GOALS]

Success metrics:
[SUCCESS METRICS]

Current milestone / release target:
[CURRENT MILESTONE]

Primary users / stakeholders:
[Who is this for? Who will feel the impact of each decision?]
```

When recommending what to work on next, always reference these goals explicitly.
A task that doesn't serve the stated goals or current milestone should be questioned,
not automatically prioritized.

---

## Board Sections

| Section              | Meaning                                                                      |
|----------------------|------------------------------------------------------------------------------|
| **Backlog**          | Identified, not started                                                      |
| **In Progress**      | Actively being worked this session                                           |
| **Blocked**          | Started, but waiting on an external dependency; blocker must be documented   |
| **Review / Testing** | Implemented, needs verification before marking Done                          |
| **Done**             | Complete — meets Definition of Done (see below)                              |

---

## Advisory Mode — Discuss First, Act Second

Trigger this mode whenever the user asks any of the following (or close variants):

- "What should I work on next?"
- "Is this worth doing?"
- "What's most important right now?"
- "Should I prioritize X or Y?"
- "How would you sequence this?"
- "What are we missing?"
- "Help me think through what to build."

**Advisory mode protocol:**

1. Pull the current Backlog from Asana (`get_tasks`) to have real task data in hand.
2. Apply the prioritization framework below.
3. Make a concrete recommendation — ranked, with brief reasoning tied to project goals.
4. Identify any risks, dependencies, or open questions before committing to the order.
5. Only move tasks on the board after the user confirms the direction.

Do not skip straight to board actions when a strategic discussion is warranted.

---

## Prioritization Framework

Use this when advising on what to work on. Score each candidate task across three
dimensions and let that drive the recommendation:

| Dimension              | Question to ask                                              | Weight |
|------------------------|--------------------------------------------------------------|--------|
| **Impact**             | How directly does this serve the stated project goals?       | High   |
| **Effort**             | How much work is this realistically? (hours, not points)     | Medium |
| **Risk / dependency**  | Does anything block this, or does this unblock others?       | High   |

**Prioritize:** high impact, lower effort, unblocking.
**Deprioritize:** low impact, high effort, or blocked.

When surfacing a recommendation, frame it as:
> "I'd do [X] first because it [directly serves goal Y] and unblocks [Z].
>  [A] can wait — it's high effort with indirect impact until [condition]."

If two tasks are close, ask one clarifying question about constraints (deadline,
dependency, stakeholder pressure) before finalizing the recommendation.

---

## Session Start Checklist

Run this at the beginning of every session, before writing any code.

**1. Confirm project scope**
If `[PROJECT NAME]` could match multiple active Asana projects, ask the user to confirm
which one before proceeding.

**2. Check business context**
If the Business Context block is unfilled, prompt the user to provide `[PROJECT GOALS]`
and `[SUCCESS METRICS]` before proceeding. One session without this is acceptable; two
is not.

**3. Check for stale In Progress tasks**
Use `get_tasks` filtered to the `[PROJECT NAME]` project and the **In Progress** section.

For each stale In Progress task (tasks not being touched this session):
- If work is genuinely continuing → leave it and note it in context
- If it was abandoned or blocked → move it to **Blocked** or **Backlog** and add a
  comment explaining the status change

Do not silently leave stale tasks in **In Progress**.

**4. Identify the work for this session**
Pull tasks from **Backlog** and apply the prioritization framework. If priorities are
unclear, enter advisory mode: surface the top options with a recommendation and
rationale, and get the user to confirm before moving anything.

**5. Move session tasks to In Progress**
Use `update_tasks` to move the confirmed task(s) to the **In Progress** section.

> **Asana tool reference for session start:**
> - `get_tasks` — fetch tasks by project + section
> - `update_tasks` — move tasks between sections
> - `search_objects` — find a task by name if the GID is unknown

---

## While Working

### Creating tasks for discovered work

If you discover a bug, edge case, follow-on feature, or future refactor during a session,
create it as an Asana task immediately — do not just mention it in chat.

Use `create_tasks` with:
- **Task name**: `[module-prefix] Short description` (always tag the module)
- **Section**: **Backlog** (unless it's blocking current work → **Blocked**)
- **Milestone tag**: Add `[milestone: X]` to the name if tied to `[CURRENT MILESTONE]`
- **Description**: See "Task Description Format" below

### Task naming convention

Every task name must include the module/area prefix:

```
[auth] Add refresh token rotation
[api-gateway] Handle 429 retry backoff
[data-pipeline] Investigate memory spike on large batch jobs
[auth][milestone: v1.2] Implement SSO provider support
```

The prefix makes board scanning fast and ties tasks to codebase structure.
The milestone tag makes release planning visible at a glance.

### Task Description Format

Descriptions capture intent, not implementation. Use this structure:

```
**Why this matters:**
<One or two sentences on business or technical impact — tie to project goals where possible>

**Expected outcome:**
<What "done" looks like — observable behavior, not file paths>

**Acceptance criteria:**
- [ ] <Specific, testable condition 1>
- [ ] <Specific, testable condition 2>
- [ ] <Edge case or error state, if relevant>

**Notes / constraints:**
<Links, known risks, dependencies — optional>
```

Acceptance criteria describe user-observable or system behavior, not implementation
steps. "User can log in with Google SSO" not "OAuth flow implemented in auth.js."

> **Do not use the description field as a progress log.** For progress notes,
> decisions made, or blockers encountered during a session, use `add_comment` instead.
> Descriptions capture scope; comments capture history.

### Subtask guidance

If a task will span more than one session or has more than one logical unit of work:
- Break it into subtasks (one per unit)
- The parent task stays **In Progress**; subtasks move through the board independently
- Limit subtask depth to one level — no subtasks of subtasks

### Blocked tasks

If work is blocked (waiting on a PR review, a credential, a teammate decision):
1. Move the task to **Blocked** using `update_tasks`
2. Add a comment via `add_comment` with:
   - What is blocking progress
   - Who owns the blocker (if known)
   - Date blocked
3. Do not leave a blocked task in **In Progress**

---

## Session End Checklist

Run this before closing out, every session.

**1. Mark completed tasks as Done**
A task is **Done** only when it meets the Definition of Done (see below).
If implemented but untested or unreviewed, move it to **Review / Testing**, not **Done**.

**2. Update partially completed tasks**
If work is partially done, leave the task **In Progress** and add a comment via
`add_comment` with:
- Where things stand
- What's left
- Any decisions made this session

Do not overwrite the description — that's scope, not status.

**3. Slot newly discovered work into Backlog**
Do a final scan: is there anything surfaced in chat that doesn't have a task yet?
If so, create it now before closing.

**4. Milestone check**
If `[CURRENT MILESTONE]` is set: are all milestone-tagged tasks either Done or on track?
If something is slipping, add a comment to the relevant task and flag it to the user.

> **Asana tool reference for session end:**
> - `update_tasks` — move tasks to Done, Review / Testing, or Blocked
> - `add_comment` — append progress notes to in-progress or blocked tasks
> - `create_tasks` — create any remaining backlog items

---

## Backlog Grooming

Run a lightweight grooming pass every 3–5 sessions, or when the Backlog feels stale.

**Signs grooming is needed:**
- Vague or description-less tasks have accumulated
- Tasks reference a milestone that already shipped
- Priorities have shifted since tasks were created

**Grooming steps:**
1. Pull all Backlog tasks (`get_tasks`)
2. For each task: still relevant? Still correctly scoped? Still the right priority?
3. Archive or delete tasks that are superseded or no longer serve the project goals
4. Re-rank remaining tasks using the prioritization framework
5. Update descriptions on tasks whose intent has drifted
6. Flag any tasks that should be milestone-tagged but aren't

Grooming is advisory — surface findings to the user and get confirmation before
deleting or re-scoping tasks.

---

## Definition of Done

| Criterion                                              | Required?   |
|--------------------------------------------------------|-------------|
| Code committed / change delivered                      | ✅          |
| All acceptance criteria checked off                    | ✅          |
| Tests passing (if applicable)                          | ✅          |
| Task description reflects final scope                  | ✅          |
| PR or commit linked in a comment (if applicable)       | Recommended |
| Reviewer sign-off (if Review / Testing step applies)   | ✅          |
| Milestone-tagged tasks verified against milestone goals| ✅          |

If any required criterion is unmet, the task belongs in **Review / Testing** or
**Blocked**, not **Done**.

---

## Asana Tool Quick Reference

| Operation                        | Tool             | Key params                            |
|----------------------------------|------------------|---------------------------------------|
| Fetch tasks by project + section | `get_tasks`      | project, section                      |
| Move task between sections       | `update_tasks`   | task GID, section GID                 |
| Create one or more tasks         | `create_tasks`   | name, description, section, project   |
| Add a progress comment           | `add_comment`    | task GID, comment text                |
| Find a task by name              | `search_objects` | query string                          |
| Get current user                 | `get_me`         | (no params) — useful to confirm auth  |

---

## Source of Truth Principle

> **Git history captures what changed. Asana captures why and what's next.**

Never rely on git history, code comments, or chat context to understand task intent.
If intent isn't in Asana, it doesn't exist. When in doubt, write the task.
