# Claude Code Coaching Agent

A structured coaching operating system built on [Claude Code](https://claude.ai/code). Drop in your own coaching framework, or use it without one.

Claude operates as a **business coach and mentor** — not an assistant. It challenges thinking, surfaces uncomfortable truths, holds you accountable, and tracks patterns across sessions.

---

## Quick Start

**1. Open this folder in Claude Code**

**2. Run `/onboard`**

Claude will interview you and populate `profile.yaml` and `goals.yaml` for you. Have any supporting documents ready to paste (resume, business plan, job description — whatever's relevant).

**3. (Optional) Add a coaching framework**

Drop your framework content into `./frameworks/`. See [frameworks/README.md](frameworks/README.md) for structure.

**4. Run `/start` to begin your first session**

---

## Three Commands

- **`/onboard`** — Run this once before your first session. Claude interviews you, accepts supporting documents (resume, business plan, job description, etc.), and populates `profile.yaml` and `goals.yaml` — no YAML editing required.
- **`/start`** — Begin a session. Claude reads all context files, flags overdue commitments, and opens with what needs attention.
- **`/session`** — Close a session. Walks through capturing everything and updating all files.

---

## How the System Works

This is a six-layer system. Each layer feeds the next.

### Layer 1 — Role Definition (`CLAUDE.md`)

`CLAUDE.md` is Claude's operating manual. It defines coaching style, guardrails, how to handle goals and profile updates, how to use an optional framework, and what "always-on" responsibilities look like.

Key behaviors:
- Default posture: **clarity → challenge → decision → action → reflect**
- Coaching modes (Strategy, Accountability, Problem-Solve, Reflect, Explore, Plan) — Claude infers the right one
- Max 3 clarifying questions per session
- Recommendation over neutral summary
- Surface stalled goals (no progress in 14+ days) proactively

**Explore mode** suspends the "push hard" mandate. Invoke with *"explore"* or *"just thinking out loud."*

---

### Layer 2 — Long-Term Memory (Persistent Files)

These files build over time and are read at the start of every session.

#### `profile.yaml`
The most important context file. Tracks everything about you as a founder and person:
- Background, professional history, and founder story
- Personality wiring, strengths, gaps, and coaching implications
- Patterns across sessions — strengths and recurring blind spots
- Vision (short, medium, and long-term)
- Financial context, personal context, key relationships
- Wins worth remembering

Every entry is dated. Context builds across months, not just sessions.

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

Written like a coach's private notes, not structured data. This is where coaching insight lives between sessions.

#### `framework-workbook.md` *(optional)*
If you're working through a structured coaching program, this file tracks your progress through the workbook questions. Status markers:
- `[ ]` — not yet addressed
- `[~]` — discussed, answer in progress
- `[x]` — fully answered

Questions are integrated naturally into sessions (1–3 per session), not drilled mechanically.

---

### Layer 3 — Short-Term Memory (Session Context)

Each session, Claude reads the long-term memory files and constructs working context:
- What goals are on track vs. at risk
- Which commitments are overdue or due soon
- Where you are in the workbook (if using one)
- What patterns have been surfacing recently (from coach-notes)

This is "re-hydrated" at the start of every session via `/start`. It's not stored separately — it's the live synthesis of the persistent files at session open.

---

### Layer 4 — Optional Coaching Framework

If you have a structured program, book, or methodology you're working through, drop it into `./frameworks/`. The system supports:

- **A workbook** (`framework-workbook.md`) — questions you work through over time
- **Guides** (`frameworks/guides/`) — specific tools, formulas, or cheat sheets Claude uses when a topic arises
- **A guide index** (`frameworks/guides_index.md`) — lookup table Claude reads to find the right guide

When a topic surfaces in session, Claude checks the index, reads the relevant guide, and coaches from that material directly — rather than improvising.

See [frameworks/README.md](frameworks/README.md) for how to structure your own framework.

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

Sessions are the audit trail. The long-term memory files (goals, profile, coach-notes, accountability) drive future sessions — but sessions are the source of truth for what was discussed on any given date.

---

### Layer 6 — Commands (`/start` and `/session`)

#### `/start` — Begin a Session

1. Read `goals.yaml`, `profile.yaml`, `accountability.md`, `coach-notes.md`
2. Read `framework-workbook.md` if it exists
3. Identify overdue commitments and those due within 7 days
4. Find the next unanswered workbook questions (if applicable)
5. Open in 2–4 sentences:
   - **Accountability first** if anything is overdue — direct, no softening
   - **Workbook question** if no urgency — offered naturally, not mechanically
   - **Open door** — "What's on your mind today?"

#### `/session` — Close a Session

5-step structured close. Each step proposes changes and waits for your confirmation before writing.

| Step | What happens |
|------|-------------|
| 1 — Session Summary | Topics, insights, decisions, commitments, open questions |
| 2 — Goals Update | Progress %, milestones, status changes, new goals |
| 2b — Workbook Update | Record answers, update status markers (if using workbook) |
| 3 — Profile Update | New context, patterns, wins, relationships |
| 4 — Session File | Create `./sessions/YYYY-MM-DD.md` |
| 5 — Accountability Update | Mark complete, carry forward, add new |
| 5b — Coach Notes | Narrative journal entry on what surfaced |

Nothing gets written to any file without your explicit confirmation ("Y" or "update it").

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
├── framework-workbook.md              # Optional: workbook questions and answers
│
├── sessions/
│   └── YYYY-MM-DD.md                  # One file per coaching session
│
├── frameworks/
│   ├── README.md                      # How to add your own framework
│   ├── guides_index.md                # Optional: lookup table for guides
│   └── guides/                        # Optional: individual guide files
│
└── .claude/
    └── commands/
        ├── onboard.md                 # /onboard command definition
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
| `framework-workbook.md` | `/session` Step 2b | Workbook questions answered in session |
| `coach-notes.md` | `/session` Step 5b | End of every substantive session |
| `sessions/YYYY-MM-DD.md` | `/session` Step 4 | End of every session |

**Nothing is ever written without confirmation.** Claude proposes changes; you approve them.

---

## Safety Rules

- Claude never writes to any file without proposing the change and receiving "Y" or "update it"
- Treat all business information (financials, customer names, strategy) as confidential
- Decisions that have been made aren't reopened unless material new information surfaces
- If a topic doesn't connect to any active goal, Claude names it

---

## What Makes This System Different from a Chatbot

**Memory builds.** Every session adds to `profile.yaml` and `coach-notes.md`. After 10 sessions, Claude knows your wiring, your blind spots, your patterns, your financial situation. That context doesn't reset.

**Accountability is structural.** Commitments live in a file with due dates. `/start` surfaces them at the top of every session. There's no friction-free way to avoid them.

**Pattern recognition persists.** `coach-notes.md` accumulates observations across sessions. Recurring themes are named and tracked — not forgotten after one session.

**The framework is yours.** Drop in any program, book, or methodology. The system coaches from your material directly — not improvised generic advice.

**The coach role is enforced.** `CLAUDE.md` holds Claude to a standard: challenge, don't validate; recommend, don't summarize; close decisions, don't reopen them; name conflicts, don't soften them.
