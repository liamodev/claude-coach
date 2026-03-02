# Adding Your Own Coaching Framework

This folder is where your coaching framework lives — the program, book, or methodology that structures your sessions alongside the core coaching system.

**The framework is optional.** The coaching agent works fully without one. If you're not working through a specific program, skip this folder entirely.

---

## What a Framework Adds

Without a framework, Claude coaches from first principles using your goals, profile, and session history.

With a framework, Claude also has:
- **Structured questions** it works through with you over time (via `frameworks/framework-workbook.md`)
- **Specific guides or tools** it can pull into sessions when a topic surfaces (e.g. a confidence formula, a goal-setting template, a decision filter)
- **A sequenced arc** — the framework's progression becomes the arc of the coaching relationship

---

## Folder Structure

```
frameworks/
├── README.md               # This file
├── guides_index.md         # Lookup table for all guides (required if using guides)
└── guides/
    ├── guide-one.md
    ├── guide-two.md
    └── ...
```

---

## Step 1: Add Your Guides

A guide is any tool, formula, checklist, or framework that Claude should use in sessions. Think: "What tools would a coach trained in this program use?"

**Each guide is a separate markdown file** in `frameworks/guides/`. Name it descriptively.

Example guide file (`frameworks/guides/goal-setting-formula.md`):
```markdown
# Goal Setting Formula

## The Six Steps

1. **Define the goal** — write it in one sentence
2. **Set the strategy** — how will you achieve it?
3. **Anticipate problems** — what could go wrong?
4. **Build reserves** — what resources do you need?
5. **Set timeframes** — by when?
6. **Create a master plan** — what's the first action?

## Questions to Ask
- Is this goal specific and measurable?
- Does it align with your long-term vision?
- What's the cost of not achieving it?
```

---

## Step 2: Build the Index

Create `frameworks/guides_index.md` — a lookup table Claude reads to find the right guide for any topic.

**Each entry needs:**
- File name
- One-line summary of what it does
- "When To Use" — a few words describing the situation that calls for it

Example:
```markdown
# Guides Index

**File:** guides/goal-setting-formula.md
**Summary:** Six-step structure for setting and architecting any major goal.
**When To Use:** When setting or revising a major goal and you need a clear, repeatable structure.

---

**File:** guides/confidence-formula.md
**Summary:** How to build confidence under pressure using preparation and rehearsal.
**When To Use:** When confidence is low, fear is blocking action, or a high-stakes situation is coming up.
```

Claude reads this index first, then reads the specific guide file, then coaches from that material.

---

## Step 3: Set Up the Workbook (optional)

If your framework has workbook questions — exercises meant to be answered progressively over time — add them to `framework-workbook.md` in this folder (`frameworks/framework-workbook.md`).

See the template in [framework-workbook.md](framework-workbook.md) for the question/answer format.

---

## Tips

- **Less is more.** A few great guides used often beats 40 that never get read.
- **Write for Claude.** Guides should be clear and self-contained — Claude reads them mid-session.
- **"When To Use" is the key field.** If it's vague, Claude won't know when to pull the guide.
- **Name files clearly.** Claude references them by name in conversation.
- **Keep guides focused.** One tool, one guide. Don't bundle unrelated content.

---

## What Claude Does With Your Framework

When a relevant topic comes up in session:
1. Claude reads `guides_index.md` and scans "When To Use" to find the right guide
2. Claude reads that specific guide file
3. Claude integrates that material directly into the coaching conversation — not generically, not by quoting it verbatim, but by coaching from it

The workbook questions are woven into sessions naturally (1–3 per session), not mechanically assigned as homework. When you answer a question, Claude records your answer and marks it complete.
