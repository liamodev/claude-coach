# Destiny Coach

A structured coaching operating system built on Claude Code. It integrates Dr. Peter J. Daniels' *Destiny of the 3rd Millennium* program with ongoing business strategy, accountability, and founder development.

Claude operates as a **business coach and mentor** — not an assistant. It challenges thinking, surfaces uncomfortable truths, holds you accountable, and tracks patterns across sessions. Think Tony Robbins meets Alex Hormozi, with a structured system underneath.

---

## Quick Start

Open this folder in Claude Code. Then:

- **`/start`** — Begin a session. Claude reads all context files, flags overdue commitments, and opens with what needs attention.
- **`/session`** — Close a session. Walks through capturing everything and updating all files.

---

## How the System Works

This is a six-layer system. Each layer feeds the next.

### Layer 1 — Role Definition (`CLAUDE.md`)

`CLAUDE.md` is Claude's operating manual. It defines coaching mode, style, guardrails, how to handle goals and profile updates, how to integrate the Destiny framework, and what "always-on" responsibilities look like.

Key behaviors it enforces:
- Default posture: **clarity → challenge → decision → action → reflect**
- Coaching modes (Strategy, Accountability, Problem-Solve, Reflect, Explore, Plan) — Claude infers the right one
- Max 3 clarifying questions per session
- Recommendation over neutral summary
- Never expand scope without flagging it
- Surface stalled goals (no progress in 14+ days) proactively

**Explore mode** suspends the "push hard" mandate. Invoke it by saying *"explore"* or *"just thinking out loud."*

---

### Layer 2 — Long-Term Memory (Persistent Files)

These files build over time and are read at the start of every session. They are the system's memory.

#### `profile.yaml`
The most important context file. Tracks everything about you as a founder and person:
- Background, professional history, and founder story
- CliftonStrengths + Dalio personality assessment (wiring, strengths, gaps, coaching implications)
- Patterns across sessions — strengths and recurring blind spots
- Vision (short, medium, and long-term)
- Financial context
- Personal context (family, faith, constraints)
- Key relationships and their status
- Energy drains and fit-check rubric
- Wins worth remembering
- People admired and why

Every entry is dated. Context builds across months, not just sessions. New Claude instances reading this file know who you are immediately.

#### `goals.yaml`
Source of truth for active goals. Tracks:
- Priority ranking
- Progress percentage
- Status (on_track, at_risk, stalled, complete)
- Key results with individual due dates and statuses
- Notes on context and decisions

Goals are never silently stalled. If a goal hasn't moved in 14+ days, Claude names it.

#### `accountability.md`
Every commitment made in a session lands here with a due date. Checked at the start of every session via `/start`. Nothing slides without being named.

Format: commitment, owner, due date, status (not started / in progress / complete / dropped).

#### `coach-notes.md`
Claude's private coaching journal. Updated after every session. Contains:
- **Session entries** — what surfaced, how it was said, what it revealed, what to watch
- **Overarching patterns** — themes that have appeared across multiple sessions

Written like a coach's private notes, not structured data. This is where coaching insight lives between sessions. It accumulates over time and is what enables pattern recognition across months of work.

#### `destiny-workbook.md`
All workbook questions from all 6 Destiny lessons, with your answers and status markers:
- `[ ]` — not yet addressed
- `[~]` — partially addressed or in progress
- `[x]` — fully answered

Questions are integrated naturally into sessions (1–3 per session), not drilled mechanically. When a question is answered, the response is captured here and the status updated.

---

### Layer 3 — Short-Term Memory (Session Context)

Each session, Claude reads the long-term memory files and constructs working context:
- What goals are on track vs. at risk
- Which commitments are overdue or due soon
- Where you are in the workbook
- What patterns have been surfacing recently (from coach-notes)

This is "re-hydrated" at the start of every session via `/start`. It's not stored in a separate file — it's the live synthesis of the long-term files at session open.

Session notes are captured in `sessions/YYYY-MM-DD.md` (see Layer 5).

---

### Layer 4 — The Destiny Framework

The coaching arc follows 6 lessons from *Destiny of the 3rd Millennium*:

**Dream → Vision → Commitment → Goal → Mission → Destiny**

This isn't just content to cover — it sequences the coaching relationship itself. Lesson 1 establishes vision. Lesson 4 builds the goal architecture. Lesson 6 is the culmination. The progression through lessons *is* the arc of the engagement.

#### The Workbook (`destiny-workbook.md`)
Every question from all 6 lessons lives here. Questions are woven into conversation, not assigned as homework. When a workbook question surfaces a pattern or genuine insight, it's logged in `coach-notes.md` — that's where the coaching gold lives.

#### The Guides (`frameworks/destiny/guides/`)
40+ specific guides, formulas, and cheat sheets extracted from the Destiny program. Organized by purpose:

| Category | Examples |
|----------|---------|
| Dream & Vision | Five-Step Plan for Life Dreams, Six Principles to Identify Dream Stealers, Destiny Directed Imageology |
| Time & Lifestyle | Principles of Time Management, Time Savers and Reminders, Concentrate on Essentials |
| Commitment & Willpower | Endeavors Filters Twelve Questions, Eight Principles of Creating Strong Willpower, The Threshold of Performance |
| Goal & Strategy | The Goals Formula, Clarifying Your Goals Four Areas, The Mediocre vs the Magnificent |
| Mission | Creating a Mission Statement Eight Steps, Five Ways to Monitor Your Mission Statement |
| Leadership | Special Distinctives of a Leader, Leaders vs Power Holders, The Essentials of Leadership |
| Resilience & Confidence | Formula for Supreme Confidence, Formula for Handling a Major Financial Crisis, Formula for Being Motivated All the Time |

When a relevant topic surfaces in session (confidence crisis, financial pressure, willpower, goal-setting, leadership), Claude doesn't improvise. It:
1. Checks `frameworks/destiny/guides_index.md` to find the right guide
2. Reads that guide from `frameworks/destiny/guides/`
3. Coaches directly from that material

The **Endeavors Filters** (12 questions) is the major commitment evaluation tool — used before committing to any significant direction or goal.

#### The Index (`frameworks/destiny/guides_index.md`)
Lookup table for all 40+ guides. Organized by topic with "When to Use" descriptions. Claude uses this before every guide application.

---

### Layer 5 — Session Capture (`sessions/`)

One markdown file per coaching session. Created during `/session`. Standard format:

```
# Session — YYYY-MM-DD

## Topics Covered
## Key Insights
## Decisions
## Commitments (table: What | Owner | Due)
## Open Questions
## Goals Updated
## Profile Updated
```

Sessions are the audit trail. They don't drive future sessions directly — the long-term memory files (goals, profile, coach-notes, accountability) do that. But sessions are the source of truth for what was discussed, decided, and committed to on any given date.

---

### Layer 6 — Commands (`/start` and `/session`)

Two custom Claude Code commands make the mechanics seamless.

#### `/start` — Begin a Coaching Session

Reads all context files and opens with maximum relevance. Workflow:

1. Read `goals.yaml`, `profile.yaml`, `accountability.md`, `destiny-workbook.md`, `coach-notes.md`
2. Identify overdue commitments and those due within 7 days
3. Find the next unanswered workbook questions
4. Open in 2–4 sentences:
   - **Accountability first** if anything is overdue — direct, no softening
   - **Workbook question** if no urgency — offered naturally, not mechanically
   - **Open door** — "What's on your mind today?"

#### `/session` — Close a Coaching Session

5-step structured close. Each step proposes changes and waits for confirmation before writing.

**Step 1 — Session Summary**
Topics discussed, key insights, decisions made, commitments with deadlines, open questions.

**Step 2 — Goals Update**
Reads `goals.yaml`. Identifies progress changes, completed milestones, status updates, new goals. Proposes each change; writes on confirmation.

**Step 2b — Workbook Update**
Reads `destiny-workbook.md`. Records any answers given during session. Updates status markers (`[ ]` → `[~]` or `[x]`). Proposes additions; writes on confirmation.

**Step 3 — Profile Update**
Reads `profile.yaml`. Captures new context: background facts, observed patterns, wins, challenges, relationships. Facts only, not interpretations. Dated entries. Proposes; writes on confirmation.

**Step 4 — Session File**
Creates `./sessions/YYYY-MM-DD.md` in standard format.

**Step 5 — Accountability Update**
Reads `accountability.md`. Marks completed items. Carries forward open items (updates status). Adds new commitments from session. Asks whether anything from last session should be dropped.

**Step 5b — Coach Notes Update**
Adds a narrative entry to `coach-notes.md` under Session Entries (newest first). What surfaced, patterns noticed, what to watch, human moments worth remembering. Written like a private journal. Proposes; writes on confirmation.

Nothing gets written to any file without explicit confirmation ("Y" or "update it").

---

## Directory Structure

```
.
├── CLAUDE.md                          # Claude's coaching operating manual
├── README.md                          # This file
├── goals.yaml                         # Active goals and milestones
├── profile.yaml                       # Your evolving context and history
├── accountability.md                  # Active commitments with due dates
├── coach-notes.md                     # Rolling coach journal across sessions
├── destiny-workbook.md                # All 6 lessons, all questions, your answers
│
├── sessions/
│   └── YYYY-MM-DD.md                  # One file per coaching session
│
├── frameworks/
│   └── destiny/
│       ├── guides_index.md            # Lookup table for all guides
│       ├── guides/                    # 40+ extracted guides and formulas
│       │   ├── formula-for-supreme-confidence.md
│       │   ├── endeavors-filters-twelve-questions.md
│       │   └── ...
│       └── foundations/               # Full lesson PDFs (Lessons 0–6)
│
└── .claude/
    └── commands/
        ├── start.md                   # /start command definition
        └── session.md                 # /session command definition
```

---

## What Gets Updated and When

| File | Updated by | Trigger |
|------|-----------|---------|
| `goals.yaml` | `/session` Step 2 | Progress discussed, milestone hit, new goal set |
| `profile.yaml` | `/session` Step 3 | New context, patterns, wins, relationships shared |
| `accountability.md` | `/session` Step 5 | New commitments made; old ones resolved |
| `destiny-workbook.md` | `/session` Step 2b | Workbook questions answered in session |
| `coach-notes.md` | `/session` Step 5b | End of every substantive session |
| `sessions/YYYY-MM-DD.md` | `/session` Step 4 | End of every session |

**Nothing is ever written without confirmation.** Claude proposes changes; you approve them.

---

## Safety Rules

- Claude never writes to any file without proposing the change and receiving "Y" or "update it"
- Treat all business information (financials, customer names, strategy) as confidential
- Decisions that have been made aren't reopened unless material new information surfaces
- If a goal or topic doesn't connect to any active goal, Claude names it: *"This doesn't map to any active goal — is this a new priority, or should we stay focused?"*

---

## What Makes This System Different from a Chatbot

**Memory builds.** Every session adds to `profile.yaml` and `coach-notes.md`. After 10 sessions, Claude knows your wiring, your blind spots, your relationship patterns, your family context, your financial situation. That context doesn't reset.

**Accountability is structural.** Commitments live in a file with due dates. `/start` surfaces them at the top of every session. There's no friction-free way to avoid them.

**Pattern recognition persists.** `coach-notes.md` accumulates observations across sessions. Recurring themes (analysis paralysis, dormant relationships, avoidance patterns) are named and tracked — not forgotten after one session.

**The framework is real.** 40+ guides from the Destiny program are applied when relevant, not improvised. The 12 Endeavors Filters are used before major commitments. The workbook progression sequences the engagement over months.

**The coach role is enforced.** `CLAUDE.md` holds Claude to a standard: challenge, don't validate; recommend, don't summarize; close decisions, don't reopen them; name conflicts, don't soften them. The quality of the coaching is structural, not session-dependent.
