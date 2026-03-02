# /session — Log a Coaching Session

## Description
Close out a coaching session by capturing what was discussed, decided, and committed to.
Updates goals.yaml and profile.yaml with anything new. Creates a dated session file.

## Instructions

You are closing a coaching session with Liam OBrien. Work through these steps in order.

### Step 1: Session Summary

Review the conversation and extract:
- **Main topics discussed**
- **Key insights or realizations** (things Liam said that revealed something important)
- **Decisions made** (what was concluded, not just discussed)
- **Commitments / action items** (what Liam said he'd do, with any deadlines)
- **Questions left open** (unresolved threads worth returning to)

### Step 2: Goals Update

Read `./goals.yaml`. Identify any updates needed:
- Progress % changed?
- Milestone completed?
- New goal or milestone added?
- Status changed (on_track / at_risk / behind / complete)?

Propose each change explicitly. Wait for "Y" or "update it" before writing.

### Step 2b: Workbook Update

Read `./destiny-workbook.md`. If any workbook questions were covered during this session:
- Record Liam's answers in the relevant question fields
- Update the status marker: `[ ]` → `[~]` if discussed, `[x]` if fully answered
- Propose the additions. Wait for "Y" or "looks right" before writing.

### Step 3: Profile Update

Read `./profile.yaml`. Identify anything worth capturing:
- New background context shared
- A pattern observed (strength or blind spot)
- A win to record
- A challenge raised
- A key relationship mentioned

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
| ... | Liam | ... |

## Open Questions
- ...

## Goals Updated
- [goal name]: [what changed]

## Profile Updated
- [what was added/changed]
```

### Step 5: Accountability Prompt

Read `./accountability.md`. Check any open commitments against what was discussed today:
- Mark completed items with the date
- Carry forward items still open (update status if needed)
- Add any new commitments made in this session
- Ask: "Anything from last session that didn't get done? Want to carry it forward or drop it?"

Propose all changes. Wait for "Y" or confirmation before writing.

### Step 5b: Coach Notes Update

Add a brief narrative entry to `./coach-notes.md` under Session Entries (newest first):
- What surfaced — the real stuff, not just the agenda
- Patterns noticed — what showed up again, what was new
- What to watch for next time
- Any human moments worth remembering

Write in journal style, not bullet points. This is the coaching memory that builds over time. Propose the entry. Wait for "Y" before writing.
