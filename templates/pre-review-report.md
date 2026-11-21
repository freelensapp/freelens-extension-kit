# Pre-review report

The report the [pre-review pass](../docs/review.md#the-pre-review-pass)
writes next to its screenshots, and hands to the maintainer before the review
of a milestone. The pass writes it: nobody fills it in by hand.

## Rules

- A check is a sentence that names the view and the rule, so that a failure
  can be read without opening the code.
- A failed check keeps its detail: what was expected and what was found.
- "For human judgment" lists what the pass looked at and cannot decide. It is
  written with the checks, not after a run.
- The report and the screenshots hold synthetic data only.

## Report

```markdown
# Pre-review pass

- Date: <when the pass ran>
- Extension: <version, or commit>
- Freelens: <version>
- Cluster: <the demo cluster, with the project and its version>
- Verdict: <every automated check passed, or the number of checks that failed>

## Checks

| Check                              | Outcome                  |
| ---------------------------------- | ------------------------ |
| <The view and the rule it follows> | passed                   |
| <The view and the rule it follows> | FAILED: <what was found> |

## Screenshots

- `<theme>-<view>.png`

## For human judgment

- <What the pass cannot decide: wording, balance, whether a view is the best
  one for its task.>
```
