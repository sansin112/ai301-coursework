# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
paste the output here, including the closing JSON block
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
Issue link:
[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69)

Verdict output:

❯ issue-select: grade these candidate first issues: <https://github.com/codepath/pathreview-ai301-fa26-s1/issues/17> <https://github.com/codepath/pathreview-ai301-fa26-s1/issues/1> <https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69>

I'll load the issue-select skill to get the rubric.

⏺ Skill(issue-select)
Successfully loaded skill

I'll read the skill's rubric, scope, and evidence guide.

  Read 3 files

Rubric and scope loaded. Note two gaps in scope.md I'll come back to. Now gathering evidence.

  Ran 13 shell commands

⏺ Auto mode lets Claude handle permission prompts automatically — Claude checks each tool call for risky actions and prompt injection before executing. Actions Claude identifies as safe are executed, while actions Claude identifies as risky are blocked and Claude may try a different approach. Ideal for long-running tasks. Sessions are slightly more expensive. Claude can make mistakes that allow harmful commands to run, it's recommended to only use in isolated environments. Shift+Tab to change mode.

Evidence gathered (gh isn't installed here, so I used the public GitHub API). Two gaps in scope.md to flag first:

- Repo line is still the placeholder <ORG>/<PATH-REVIEW-REPO>. I graded anyway because all three candidates are in one repo whose own description reads "PathReview — AI301 Fall 2026 Section 1 student copy. Fork this repo, claim an issue, open your PR here." — that is the course Path Review repo. Paste it into scope.md so the scope check is real next time.
- Fit profile is empty ("(Write a few sentences here.)"), so I could not rank the accepted issues by fit. I ranked them by the preferred check instead and say so below.

Repo facts (all three share these): not archived, last default-branch commit 2026-09-16 by Aburke225 (the issue author/maintainer), last push 2026-09-16, repo updated 2026-09-21, 72 open issues, no releases. No AI-contribution ban in docs/CONTRIBUTING.md — it does require green CI on all five jobs and deletion of the covering xfail marker as part of any seeded-bug fix.

#69 — Output parser crashes on top-level JSON array fallback — ACCEPT (rank 1)
- Maintainer Activity: pass — commit 6 days before today, repo not archived.
- Unclaimed Work: pass — assignees: [], timeline shows no linked PR, the only open PR (#74) belongs to issue #60. Two claim comments from classmate jacho15 (author_association: NONE) are ignored per the Path Review house rule; claim it anyway.
- Clear Problem Statement: pass — names the crash, the call site, and the fix boundary: _parse_json_output runs for key, value in data.items() on a list (confirmed at rag/generator/output_parser.py:68).
- Bounded Feature Scope: pass — two files, one function, plus removing the @pytest.mark.xfail for manifest id H-02; 2–4 h.
- Standard Contributor Scope: pass — no workflow, build-config, permission, or secret work in the body.
- Beginner Friendly: pass — carries the good first issue label outright (also tier-1).

#1 — Duplicate embeddings on re-ingest — ACCEPT (rank 2)
- Maintainer Activity: pass — same repo facts.
- Unclaimed Work: pass — assignees: [], timeline has label events only, no linked or mentioned PR.
- Clear Problem Statement: pass — root cause given exactly: self.db_session.query("IngestedSource") at ingestion/pipeline.py:298, swallowed by a broad except Exception.
- Bounded Feature Scope: pass — IngestedSource already exists at core/models/ingested_source.py:17, so this is a string→model-class swap plus narrowing the except; no migration, no new dependency.
- Standard Contributor Scope: pass — the devops label sounds like pipeline work, but the body asks only for application-code changes. Worth a second look before you start, since the label is the one thing pointing outward.
- Beginner Friendly: pass on the "accessible entry-level contribution" branch — the defect and its fix are pinpointed — but no beginner tag, and 4–6 h vs #69's 2–4 h, which is why it ranks second.

#17 — Agent state not persisted across API restarts — REJECT
- Sank on Bounded Feature Scope: the body asks that in-flight session state, currently held in memory and written only at completion, survive restarts. agent/memory/context_manager.py is by its own docstring an "In-memory context manager for memoization" with no Redis path, and agent/orchestrator.py:65-68 persists once after the whole plan finishes. Satisfying this means making that component durable and adding mid-run persistence plus resume logic across both modules — a multi-module rework of the agent subsystem's state management, which the rubric's condition excludes. tier-3, 7–10 h.
- Its other required checks pass (active repo, unassigned with no linked PR, clear problem statement, no CI/secrets work), and Beginner Friendly fails, but one required failure is decisive.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69",
    "checks": [
      {"name": "Maintainer Activity", "grade": "pass", "evidence": "Not archived; last default-branch commit 2026-09-16 by Aburke225, six days before today's 2026-09-22."},
      {"name": "Unclaimed Work", "grade": "pass", "evidence": "assignees: []; timeline shows no linked PR; classmate jacho15's claim comments (author_association NONE) do not block under the Path Review house rule."},
      {"name": "Clear Problem Statement", "grade": "pass", "evidence": "\"output_parser.py calls .items() on the parsed value and raises AttributeError\" — confirmed at rag/generator/output_parser.py:68."},
      {"name": "Bounded Feature Scope", "grade": "pass", "evidence": "Two files, one fallback branch, plus removing the xfail marker for manifest id H-02; estimated 2-4 hours."},
      {"name": "Standard Contributor Scope", "grade": "pass", "evidence": "Body names only rag/generator/output_parser.py and tests/unit/test_output_parser.py; no workflows, build config, permissions, or secrets."},
      {"name": "Beginner Friendly", "grade": "pass", "evidence": "Labels: ['bug', 'good first issue', 'rag', 'tier-1']."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/1",
    "checks": [
      {"name": "Maintainer Activity", "grade": "pass", "evidence": "Not archived; last default-branch commit 2026-09-16 by Aburke225; repo updated 2026-09-21."},
      {"name": "Unclaimed Work", "grade": "pass", "evidence": "assignees: []; zero comments; timeline has label events only and no linked PR."},
      {"name": "Clear Problem Statement", "grade": "pass", "evidence": "\"_check_skip() ... passes the string \\\"IngestedSource\\\" to db_session.query() instead of the model class\" — confirmed at ingestion/pipeline.py:298."},
      {"name": "Bounded Feature Scope", "grade": "pass", "evidence": "IngestedSource already exists at core/models/ingested_source.py:17, so the fix is a string-to-class swap plus narrowing a broad except; no new dependency or migration."},
      {"name": "Standard Contributor Scope", "grade": "pass", "evidence": "Body asks only for changes in ingestion/pipeline.py and core/models/ingested_source.py; the 'devops' label is not matched by any CI, build-config, or secrets work in the text."},
      {"name": "Beginner Friendly", "grade": "pass", "evidence": "No beginner tag (labels: bug, devops, ingestion, tier-2), but the body pinpoints the exact broken call and its fix, an accessible entry-level contribution."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/17",
    "checks": [
      {"name": "Maintainer Activity", "grade": "pass", "evidence": "Not archived; last default-branch commit 2026-09-16 by Aburke225, six days before today's 2026-09-22."},
      {"name": "Unclaimed Work", "grade": "pass", "evidence": "assignees: []; zero comments; timeline has two label events only and no linked PR."},
      {"name": "Clear Problem Statement", "grade": "pass", "evidence": "\"Long-running reviews ... that span a server restart lose their progress\" with the two owning files named."},
      {"name": "Bounded Feature Scope", "grade": "fail", "evidence": "Requires making the by-design in-memory ContextManager durable and adding mid-run persistence plus resume in orchestrator.py (which persists once at agent/orchestrator.py:65-68) — a multi-module rework of the agent's state management; tier-3, 7-10 hours."},
      {"name": "Standard Contributor Scope", "grade": "pass", "evidence": "Body names only agent/memory/context_manager.py and agent/orchestrator.py; no workflows, build config, permissions, or secrets."},
      {"name": "Beginner Friendly", "grade": "fail", "evidence": "Labels are ['agent', 'tier-3'] with a 7-10 hour estimate and no beginner-friendly tag."}
    ],
    "verdict": "reject"
  }
]

2. What the verdict identified correctly, and what you weighed that the rubric could not.

The verdict correctly identified that Issue #69 is highly bounded (localized to two files with clear step-by-step reproduction details), carries the `good first issue` label, and has an active maintainer with no existing PRs linked. 

What the rubric could not weigh is my personal learning goals and domain interest. While the rubric evaluates technical safety and clarity, I manually weighed that fixing JSON output parsing logic in `rag/generator/output_parser.py` aligns directly with the practical Python unit testing and backend debugging experience I want to build for Software Engineering internship preparation.

3. The anticipated difficulty in claiming it.]
The anticipated difficulty in claiming this issue is very low. The issue has no assigned contributors and no linked Pull Requests. While there are discussion comments from another classmate, the course's Path Review house rules permit claiming unclaimed issues that do not have active PRs attached.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
