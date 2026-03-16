# /session — Log a Coaching Session

## Description
Close out a coaching session by capturing what was discussed, decided, and committed to.
Updates core files with anything new. Creates a dated session file.

## How This Works

A coach takes notes — they don't ask permission to do it. Work through all steps silently, assembling everything you observed. Then write everything automatically and present a summary of what was captured.

**Never interrupt the coaching conversation to ask about note-taking.** Observe, capture, present at the end.

---

## Instructions

Work through these steps in order. Do not pause to ask for confirmation between steps — compile everything first, then present it all at once in the Final Review.

### Step 1: Session Summary

Review the conversation and extract:
- **Main topics discussed**
- **Key insights or realizations** (things the user said that revealed something important)
- **Decisions made** (what was concluded, not just discussed)
- **Commitments / action items** (what the user said they'd do, with any deadlines)
- **Questions left open** (unresolved threads worth returning to)

### Step 1b: Wins & Gains

Identify any wins from this session or since last session.

- **Name the win explicitly** — don't let it stay implicit or rush past it
- **Surface the identity question**: "I want to go back to [X] — that was a real win. What does it mean to you?" If they brushed past a win during the session, return to it here.
- **Capture their answer** for the `identity_reveal` field in profile.yaml: what this win says about who they are

### Step 2: Goals Update

Read `./core/goals.yaml`. Note any updates needed:
- Progress % changed?
- Milestone completed?
- New goal or milestone added?
- Status changed (on_track / at_risk / behind / complete)?

### Step 2b: Workbook Update (if applicable)

If `./frameworks/framework-workbook.md` exists and any workbook questions were covered:
- Note the user's answers for the relevant question fields
- Note status marker updates: `[ ]` → `[~]` if discussed, `[x]` if fully answered

### Step 3: Profile Update

Read `./core/profile.yaml`. Note anything worth capturing:
- New background context shared
- A pattern observed (strength or blind spot) — include `recurrence_count` if this has surfaced before
- A win — **always include `identity_reveal`**: what this win says about who they are (from Step 1b)
- A belief surfaced — limiting or empowering — with `status: active/shifting/resolved`
- A values clarification — any values named or confirmed
- A self-concept shift — current or emerging identity
- A challenge raised
- A key relationship mentioned
- Energy patterns observed

### Step 4: Session File

Prepare a session file for `./sessions/YYYY-MM-DD.md` using today's date:

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

Read `./core/accountability.md`. Note:
- Items to mark complete (with date)
- Items to carry forward (update status if needed)
- New commitments from this session to add
- Ask once: "Anything from last session that didn't happen? Carry it forward or drop it?"

### Step 5b: Coach Notes

Draft a narrative entry for `./core/coach-notes.md` (newest first):
- What surfaced — the real stuff, not just the agenda
- Patterns noticed — what showed up again, what was new
- What to watch for next time
- Any human moments worth remembering

Write in journal style, not bullet points.

---

### Final Review: Write and Present

Once all steps are complete, **write all files immediately** — no confirmation needed. A real coach doesn't ask permission to take notes.

Write all files at once:
1. `core/profile.yaml` — all profile updates
2. `core/goals.yaml` — all goal updates
3. `core/accountability.md` — all commitment changes
4. `frameworks/framework-workbook.md` — if applicable
5. `sessions/YYYY-MM-DD.md` — session file
6. `core/coach-notes.md` — journal entry

Then present a brief summary of what was captured:

> "Here's what I noted from today:
>
> **Wins & Gains:** [win + identity_reveal]
> **Goals:** [what changed]
> **Profile:** [what was added — beliefs, values, patterns, etc.]
> **Accountability:** [new commitments, completed items]
> **Workbook:** [if applicable]
> **Coach notes:** [brief version of the journal entry]"

If the client flags something wrong in a future session, correct it then — just like a real coach would.
