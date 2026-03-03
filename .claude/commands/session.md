# /session — Log a Coaching Session

## Description
Close out a coaching session by capturing what was discussed, decided, and committed to.
Updates core files with anything new. Creates a dated session file.

## Instructions

You are closing a coaching session. Work through these steps in order.

### Step 1: Session Summary

Review the conversation and extract:
- **Main topics discussed**
- **Key insights or realizations** (things the user said that revealed something important)
- **Decisions made** (what was concluded, not just discussed)
- **Commitments / action items** (what the user said they'd do, with any deadlines)
- **Questions left open** (unresolved threads worth returning to)

### Step 1b: Wins & Gains

Before logging anything else, surface and anchor any wins from this session or since last session.

- **Name the win explicitly** — don't let it stay implicit or rush past it
- **Ask the identity question**: "What does this tell you about who you are?" Capture their answer.
- **Propose adding to profile.yaml** wins section with `identity_reveal` field: `{ win: "...", date: "YYYY-MM-DD", context: "...", identity_reveal: "..." }`
- If they brushed past a win during the session, return to it now: "I want to go back to [X] — that was a real win. What does it mean to you?"

Wait for confirmation before writing to profile.yaml.

### Step 2: Goals Update

Read `./core/goals.yaml`. Identify any updates needed:
- Progress % changed?
- Milestone completed?
- New goal or milestone added?
- Status changed (on_track / at_risk / behind / complete)?

Propose each change explicitly. Wait for "Y" or "update it" before writing.

### Step 2b: Workbook Update (if applicable)

If `./frameworks/framework-workbook.md` exists and any workbook questions were covered during this session:
- Record the user's answers in the relevant question fields
- Update the status marker: `[ ]` → `[~]` if discussed, `[x]` if fully answered
- Propose the additions. Wait for "Y" or "looks right" before writing.

### Step 3: Profile Update

Read `./core/profile.yaml`. Identify anything worth capturing:
- New background context shared
- A pattern observed (strength or blind spot) — include `recurrence_count` if this has surfaced before
- A win to record — **always include `identity_reveal`**: what this win says about who they are (captured in Step 1b; carry it forward here)
- A belief surfaced — limiting or empowering — add to `beliefs` section with `status: active/shifting/resolved`
- A values clarification — update `values.core` if any were named or confirmed
- A self-concept shift — update `self_concept.current` or `self_concept.emerging`
- A challenge raised
- A key relationship mentioned
- Energy patterns observed — update `energy` section if relevant

Propose additions. Wait for confirmation before writing.

### Step 4: Write Session File

Create a file at `./sessions/YYYY-MM-DD.md` using today's date.

Use this format:

```markdown
# Session — YYYY-MM-DD

## Topics Covered
- ...

## Key Insights
- ...

## Decisions
- ...

## Commitments
| What | Owner | Due |
|------|-------|-----|
| ... | You | ... |

## Open Questions
- ...

## Goals Updated
- [goal name]: [what changed]

## Profile Updated
- [what was added/changed]
```

### Step 5: Accountability Update

Read `./core/accountability.md`. Check any open commitments against what was discussed today:
- Mark completed items with the date
- Carry forward items still open (update status if needed)
- Add any new commitments made in this session
- Ask: "Anything from last session that didn't get done? Want to carry it forward or drop it?"

Propose all changes. Wait for "Y" or confirmation before writing.

### Step 5b: Coach Notes Update

Add a brief narrative entry to `./core/coach-notes.md` under Session Entries (newest first):
- What surfaced — the real stuff, not just the agenda
- Patterns noticed — what showed up again, what was new
- What to watch for next time
- Any human moments worth remembering

Write in journal style, not bullet points. This is the coaching memory that builds over time. Propose the entry. Wait for "Y" before writing.
