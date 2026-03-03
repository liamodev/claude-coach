# Claude Code Coaching Agent

A structured coaching operating system built on [Claude Code](https://claude.ai/code). Drop in your own coaching framework, or use it without one.

Claude operates as a **coach** — not an assistant. It challenges thinking, surfaces uncomfortable truths, holds you accountable, tracks patterns across sessions, and coaches at the identity level — not just the tactical level.

---

## Quick Start

**1. Open this folder in Claude Code**

**2. Run `/onboard`**

Claude will interview you and populate `profile.yaml` and `goals.yaml` for you. Have any supporting documents ready to paste (resume, business plan, job description — whatever's relevant).

**3. (Optional) Build a coaching framework**

Run `/buildframework` to build a framework from any source — a book, podcast, person's teaching, or AI-generated content. Or skip this and coach from first principles.

**4. Run `/start` to begin your first session**

---

## Commands

| Command | When to run | What it does |
|---------|-------------|-------------|
| `/onboard` | Once, before your first session | Conducts a structured interview and populates `profile.yaml` and `goals.yaml`. Captures identity, values, beliefs, vision, goals, challenges, and coaching contract. Accepts supporting documents. |
| `/buildframework` | Any time — optional | Builds or updates your coaching framework from any source: book, podcast, person's teaching, AI-generated content, lesson files. Creates guide files and index. Can add to an existing framework. |
| `/start` | Start of every session | Reads all context files including the coaching methodology. Opens with a check-in, surfaces a win, then flags accountability. |
| `/session` | End of every session | Captures insights, anchors wins to identity, updates goals/profile/accountability/coach-notes. Nothing written without your confirmation. |

---

## How the System Works

This is a seven-layer system. Each layer feeds the next.

### Layer 0 — Coaching Methodology (`mastercoach/MasterCoach.md`)

`mastercoach/MasterCoach.md` is the foundational coaching standard. It defines how to coach — the philosophy, skills, and methodology that every session runs on. Read at the start of every session. **Do not modify during sessions.**

Key principles embedded in this document:
- The client is not broken — whole, capable, and resourceful
- Identity-level > behavior-level (behavior change is temporary; identity change is permanent)
- Level 3 Listening — what's NOT said matters as much as what is
- The Champion/Challenger dial — calibrated precisely, not flat pressure
- Wins & Gains — high achievers skip this; the coach interrupts that pattern
- Systems thinking — the client exists within a system, not in isolation
- Make yourself obsolete — build self-coaching capacity over time

---

### Layer 1 — Operating Rules (`CLAUDE.md`)

`CLAUDE.md` is Claude's operating manual. It defines the coaching role, guardrails, how to handle goals and profile updates, coaching modes, and always-on responsibilities. It embeds the key principles from `MasterCoach.md` so they're always active.

Key behaviors:
- Default posture: **Awareness → Restructuring → Commitment & Capacity**
- Coaching modes (Strategy, Accountability, Problem-Solve, Reflect, Explore, Plan) — inferred automatically
- Champion/Challenger dial — not flat "push hard"; calibrated to what the client needs
- Max 3 clarifying questions; recommendation over neutral summary
- Surface stalled goals (no progress in 14+ days) proactively

**Explore mode** suspends the challenge mandate. Invoke with *"explore"* or *"just thinking out loud."*

---

### Layer 2 — Long-Term Memory (Persistent Files)

These files build over time and are read at the start of every session.

#### `core/profile.yaml`
The heartbeat of the system. What makes coaching feel like a real coach who knows their client. Tracks:
- **Identity** — name, location, timezone
- **Self-concept** — current identity and emerging identity ("I am the kind of person who...")
- **Values** — core values and what they mean in practice
- **Beliefs** — limiting beliefs (with active/shifting/resolved status) and empowering beliefs being built
- **Background** — professional history, founder story, career context
- **Patterns** — strengths, blind spots (both with recurrence count), and recurring themes across sessions
- **Wiring** — personality assessments (CliftonStrengths, DISC, Enneagram, etc.)
- **Energy** — energizers, drains, and peak working time
- **Wins** — with `identity_reveal` field: what each win says about who they are
- **Challenges** — raised, resolved, and how
- **Financial context** — optional but useful for coaching in context
- **Personal context** — family, health, constraints
- **Key relationships** — who influences decisions, sources of support and drag
- **Vision** — long-term direction and purpose
- **Positioning** — niche, differentiator, ICP (if applicable)

Every entry is dated. Context builds across months, not just sessions.

#### `core/goals.yaml`
Source of truth for active goals. Tracks:
- Priority ranking
- Progress percentage
- Status (on_track, at_risk, stalled, complete)
- Key results with individual due dates and statuses
- Notes on context and decisions

Goals are never silently stalled. If a goal hasn't moved in 14+ days, Claude names it.

#### `core/accountability.md`
Every commitment made in a session lands here with a due date. Checked at the start of every session via `/start`. Nothing slides without being named.

Format: commitment, owner, due date, status (not started / in progress / complete / dropped).

#### `core/coach-notes.md`
Claude's private coaching journal. Updated after every session. Contains:
- **Session entries** — what surfaced, how it was said, what it revealed, what to watch
- **Overarching patterns** — themes that have appeared across multiple sessions

Written like a coach's private notes, not structured data. This is where coaching insight lives between sessions.

#### `frameworks/framework-workbook.md` *(optional)*
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

- **A workbook** (`frameworks/framework-workbook.md`) — questions you work through over time
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

1. Read `mastercoach/MasterCoach.md`, `core/goals.yaml`, `core/profile.yaml`, `core/accountability.md`, `core/coach-notes.md`
2. Read `frameworks/framework-workbook.md` if it exists
3. Identify overdue commitments and those due within 7 days
4. Find the next unanswered workbook questions (if applicable)
5. Open in 2–4 sentences following this sequence:
   - **Check-in** — one question on energy/mindset to calibrate where you are
   - **Wins & Gains** — surface a win before anything else (non-negotiable)
   - **Accountability** if anything is overdue — direct, no softening
   - **Workbook question** if no urgency — natural, not mechanical
   - **Open door** — "What's on your mind today?"

#### `/session` — Close a Session

6-step structured close. Each step proposes changes and waits for your confirmation before writing.

| Step | What happens |
|------|-------------|
| 1 — Session Summary | Topics, insights, decisions, commitments, open questions |
| 1b — Wins & Gains | Name wins explicitly; anchor to identity ("What does this tell you about who you are?"); write to profile.yaml with `identity_reveal` |
| 2 — Goals Update | Progress %, milestones, status changes, new goals |
| 2b — Workbook Update | Record answers, update status markers (if using workbook) |
| 3 — Profile Update | New context, patterns, beliefs, values, self-concept shifts, wins, relationships, energy |
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
├── mastercoach/
│   └── MasterCoach.md                 # Foundational coaching methodology — read-only
│
├── core/
│   ├── profile.yaml                   # Your evolving context and history (the heartbeat)
│   ├── goals.yaml                     # Active goals and milestones
│   ├── accountability.md              # Active commitments with due dates
│   └── coach-notes.md                 # Rolling coach journal across sessions
│
├── sessions/
│   └── YYYY-MM-DD.md                  # One file per coaching session
│
├── frameworks/
│   ├── README.md                      # How to add your own framework
│   ├── framework-workbook.md          # Optional: workbook questions and answers
│   ├── guides_index.md                # Optional: lookup table for guides
│   └── guides/                        # Optional: individual guide files
│
└── .claude/
    └── commands/
        ├── onboard.md                 # /onboard — initial setup interview
        ├── buildframework.md          # /buildframework — build or update framework
        ├── start.md                   # /start — begin a session
        └── session.md                 # /session — close and log a session
```

---

## What Gets Updated and When

| File | Updated by | Trigger |
|------|-----------|---------|
| `core/goals.yaml` | `/session` Step 2 | Progress discussed, milestone hit, new goal set |
| `core/profile.yaml` | `/session` Steps 1b + 3 | Wins (with identity_reveal), beliefs, values, self-concept shifts, patterns, relationships, energy |
| `core/accountability.md` | `/session` Step 5 | New commitments made; old ones resolved |
| `frameworks/framework-workbook.md` | `/session` Step 2b | Workbook questions answered in session |
| `core/coach-notes.md` | `/session` Step 5b | End of every substantive session |
| `sessions/YYYY-MM-DD.md` | `/session` Step 4 | End of every session |

**Nothing is written mid-session.** Claude observes and notes silently — like a coach writing in their notebook. At `/session` close, all changes are presented in one batch review. One "Y" writes everything.

---

## Safety Rules

- Claude never writes mid-session — all file changes are batched and presented once at `/session` close
- One "Y" writes everything; flag any specific item to adjust before writing
- `mastercoach/MasterCoach.md` is read-only — Claude does not modify it during sessions
- Treat all business information (financials, customer names, strategy) as confidential
- Decisions that have been made aren't reopened unless material new information surfaces
- If a topic doesn't connect to any active goal, Claude names it

---

## What Makes This System Different from a Chatbot

**A real coaching standard.** `mastercoach/MasterCoach.md` defines the methodology every session runs on — Level 3 Listening, Champion/Challenger calibration, identity-level coaching, Wins & Gains. It's not improvised; it's a standard.

**Memory builds.** Every session adds to `profile.yaml` and `coach-notes.md`. After 10 sessions, Claude knows your wiring, your blind spots, your limiting beliefs, your values, your patterns. That context doesn't reset.

**Accountability is structural.** Commitments live in a file with due dates. `/start` surfaces them at the top of every session. There's no friction-free way to avoid them.

**Pattern recognition persists.** `coach-notes.md` accumulates observations across sessions. Recurring themes are named and tracked — not forgotten after one session.

**The framework is yours.** Drop in any program, book, or methodology. The system coaches from your material directly — not improvised generic advice.

**The coach role is enforced.** `CLAUDE.md` holds Claude to a standard: challenge, don't validate; recommend, don't summarize; close decisions, don't reopen them; name conflicts, don't soften them.
