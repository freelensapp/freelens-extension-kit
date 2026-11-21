# Task brief

A closed brief for a task given to another session: a coding agent of the
same kind or of another one, or the independent reviewer of
[Review](../docs/review.md). Whoever receives it knows nothing else, so the
brief holds everything the task needs and nothing the task does not.

## Rules

- One outcome, small enough to verify.
- Every fact has a place it is read from, inside the folders the brief names.
- The limits are explicit: the files that may change, no commit, no push.
- The brief names no person and no private environment: it may end up in a
  log.
- For a reviewer, the task is to check and to report. Its limits say that no
  file changes at all.

## Brief

Replace what is in angle brackets.

```text
You are in a checkout of <repository>: <what it is, and the state it is in>.

Context: <what is true now and what the task builds on>. The reference
material is in <folders>, read only.

Task: <the outcome, in one sentence>.
- <A point: what to do, and where its facts are read from.>
- <A point.>

Rules:
- <The writing or coding rules that apply to the result.>

Limits:
- Change no file other than <files>.
- Do not commit, push or open anything.
- Read only <folders>.

When done, check that <the checks to run>. Reply with <what to report>. Cite
file and line for every finding, and list separately what you could not
verify.
```
