# Specs and roadmap

A spec is the contract of one feature: what the user can do when it is done,
what is in and out of scope, how it is designed and how it is tested. The
roadmap lists the features and the state of each. Together they are the trace
of an extension: a reader who follows the roadmap from the first spec to the
last one sees why each thing was built the way it was.

[Process](process.md) says when a spec is written, approved and closed. This
document says what a spec and a roadmap contain.

## Files

- A spec is `docs/specs/SPEC-NNNN-short-slug.md`. Numbers are assigned in
  order and never reused.
- The roadmap is `docs/development/ROADMAP.md`, written from the
  [roadmap template](../templates/roadmap.md).
- One spec per feature. A spec may cover a few closely related tasks, as long
  as each one stays a slice that can be implemented and tested on its own.
- `SPEC-0001` is the [reconnaissance](reconnaissance.md): the facts about the
  project that every other spec builds on.

## Three templates

| Template                                                      | For                                                                                       | What it has                                                                                       |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| [spec-reconnaissance.md](../templates/spec-reconnaissance.md) | `SPEC-0001`                                                                               | The sources, the facts, the first decisions, the status model, the spikes and the versions        |
| [spec.md](../templates/spec.md)                               | A feature that only reads from the cluster                                                | Goal, upstream reference, scope, design, tests, deviations                                        |
| [spec-write-action.md](../templates/spec-write-action.md)     | A feature that writes to the cluster: an action, a form, a request that creates an object | The same, plus user scenarios, requirements with an ID and a table that ties each one to its test |

The second template keeps a read-only view cheap to specify. The third one
buys traceability where a mistake costs the most: every requirement of a
write has a named check, and a review can follow it from the sentence to the
test.

A new spec is a copy of one of the three, taken from the version of the kit
the extension follows. The extension keeps no template of its own.

`SPEC-0001` has no code of its own. It goes from Draft to Approved and stays
there, and its row in the roadmap is `Done` when it is approved.

An extension with requirement IDs keeps an index, `docs/specs/README.md`: a
row for each spec that has them, with its range of IDs, and the next free ID.
IDs are `REQ-NNN`, unique across the extension, and never reused or given
another meaning after approval. An extension without them needs no index: the
roadmap lists the specs.

## Header

Every spec starts with the same fields:

- **Status**: one of the statuses below.
- **Milestone**: the milestone of the roadmap it belongs to.
- **Reviewed project**: the release of the project the spec was written
  against, tag and commit.
- **Freelens**: the release of Freelens the extension is built and tested
  against.
- **Dependencies**: the approved specs it builds on.
- **Approval**: pending, then role, date and scope. The scope is what the
  approval covers: the spec as drafted, or with the changes it names. Never a
  personal name. A spec approved under a
  [delegation](process.md#delegation-for-a-milestone) says so.

## Statuses

| Status      | Meaning                                                                                       | Moved by                                     |
| ----------- | --------------------------------------------------------------------------------------------- | -------------------------------------------- |
| Draft       | Written, not approved. Not approval to implement.                                             | The contributor                              |
| Approved    | The maintainer approved it, or the coding agent under a delegation. Implementation can start. | The maintainer, or the delegation            |
| Implemented | The code and its tests are merged.                                                            | The pull request that implements it          |
| Verified    | Its tests run green in CI on `main`, and its manual checks are recorded.                      | The closure after the merge                  |
| Superseded  | Replaced. It keeps a link to its replacement; nothing is deleted.                             | The pull request that brings the replacement |

## What a spec says about design

Two questions have an answer in every spec:

- **Standard or ad hoc view, and why.** See
  [the design question](process.md#the-design-question-every-spec-answers).
- **Safety.** What the feature reads and what it writes. A feature that only
  reads says so, and says how its tests prove it. A feature that writes says
  what it writes, which confirmation it asks for and what it never does
  ([Safety](safety.md)). A request that creates an object in the cluster is a
  write, even when the user only asked to look at something.

The design also names the kinds and the fields it reads, taken from the
schemas of the reviewed release, the extension points it registers, the
columns and the panels, and the states that are not the happy one: loading,
empty, restricted and failed, in a dark and in a light theme.

## Evidence

A spec holds what a later reader needs: what diverged from the plan and why,
and the outcome of the manual checks, with date, role and result. The rest
stays where it was produced: the commands, their output and the counts in the
pull request, the runs in CI. A spec that collects every run becomes too long
to review.

A change to an approved spec is made in the spec, in the pull request that
needs it, under "Notes and deviations", and the description of the pull
request calls it out. A decision taken while implementing is recorded there
as such.

An open question is marked `NEEDS CLARIFICATION` only when no reasonable
default exists: at most three in a spec, each with a concrete question.

## The roadmap

The roadmap is the single source of truth for scope and progress. It is
written once `SPEC-0001` is approved, in a pull request of its own, and the
maintainer approves it by approving that pull request. From then on it is
updated in every pull request that starts, completes or re-scopes a feature.

- It states the goal of the first stable version, `1.0.0`, and the releases
  that lead to it, the first one being the first release of the brief.
- It lists the features by milestone, each with its spec and its status:
  `Planned`, `Draft`, `Approved`, `In PR`, `Done`.
- Every milestone keeps the whole agreed scope. Nothing moves out of it
  without a decision recorded in the roadmap.
- It says what is out of scope, and where the user does that instead.

The inventory of the features comes from the reconnaissance, not from a
guess: the kinds of the project at the reviewed release, its own tools, and
what its users do with them. When the brief names a reference to match or to
surpass, the roadmap covers the inventory of that reference too: each of its
features is in a milestone, or out of scope with a reason.
