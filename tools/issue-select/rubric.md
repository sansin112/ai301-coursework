# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer Activity | `repo-facts block` and comment history | The repository shows recent activity and is actively maintained (not archived, unmaintained, or abandoned). | required |
| Unclaimed Work | `comment thread` and assignees list | The issue is currently unassigned and has no active linked Pull Request or user claiming it. | required |
| Clear Problem Statement | `issue body` | The issue describes a bug, feature request, task, or documentation fix to work on. | required |
| Bounded Feature Scope | `issue body` | The task is a self-contained bug fix or minor feature (fails if it asks to introduce major core dependencies, refactor central architectures, or rewrite multi-module components). | required |
| Standard Contributor Scope | `issue body` | The issue does NOT require modifying CI/CD deployment pipelines, GitHub Actions (`.github/workflows`), repository permissions, build configurations, or security secrets. | required |
| Beginner Friendly | issue labels and `issue body` | Has a beginner-friendly tag (like `good first issue`, `easy`, `help wanted`) OR describes an accessible entry-level contribution. | preferred |

## Verdict rule

Accept if EVERY `required` check passes. If any `required` check fails, the verdict is REJECT. Any check with a result of `unclear` is treated as a FAIL for that check. Checks marked as `preferred` do not affect the binary accept/reject verdict, but higher counts of passing preferred checks rank accepted issues higher.
