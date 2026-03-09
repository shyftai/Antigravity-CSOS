---
name: cs:feedback
description: Submit feedback, report a bug, or request a feature for CS:OS
argument-hint: "[feedback]"
---
<objective>
Collect user feedback about CS:OS and submit it as a GitHub issue on the CSOS repo.

Type: $ARGUMENTS (optional — will ask if not provided)
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // FEEDBACK >>`

2. If no type specified, ask:
```
  What kind of feedback?

  1. Bug report — something isn't working right
  2. Feature request — something you wish CS:OS could do
  3. Idea — general improvement or suggestion

  >> 1, 2, or 3?
```

3. Based on type, collect the relevant info:

**Bug report:**
- What happened?
- What did you expect to happen?
- Which command were you running? (if applicable)
- Which workspace/customer? (if applicable)

**Feature request:**
- What do you want CS:OS to do?
- Why is this useful? What problem does it solve?
- How urgent is this for your workflow?

**Idea:**
- What's the idea?
- Any additional context?

4. Draft the feedback as a GitHub issue:
```
  +-- FEEDBACK PREVIEW ----------------------------+
  |                                                 |
  |  Type:    {Bug / Feature / Idea}                |
  |  Title:   {auto-generated from description}     |
  |                                                 |
  |  {formatted body}                               |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
  >> Submit to GitHub? (y/n)
```

5. On approval, create the issue:
   - Run: `gh issue create --repo shyftai/CSOS --title "{title}" --body "{body}" --label "{type}"`
   - Labels: `bug`, `enhancement`, `idea`
   - Add system context automatically:
     - CS:OS version (latest commit hash)
     - Active workspace name (if any)
     - Tools connected (from TOOLS.md, if loaded)

6. Display confirmation:
```
---------------------------------------------------

  Feedback submitted. Thanks for helping improve CS:OS.

  Issue: {url}

---------------------------------------------------
```

7. If `gh` CLI is not available or not authenticated:
   - Save feedback locally to `global/feedback-log.md` instead
   - Tell the user they can submit it manually at the repo's issues page
</process>
</output>
