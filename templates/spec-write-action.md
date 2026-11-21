# SPEC-NNNN: Title

- **Status:** Draft
- **Milestone:** `M<n>` (see [ROADMAP.md](../development/ROADMAP.md))
- **Reviewed project:** release tag and commit
- **Freelens:** release the extension is built and tested against
- **Dependencies:** approved specs this one builds on
- **Approval:** Pending; later the role, the date and the scope, without names,
  or the delegation it was approved under

This feature writes to the cluster. Its requirement IDs come from the
[index](README.md). A completed draft is not approval to implement.

## Goal

The outcome for the user and why it matters, in one or two sentences.

## Upstream reference

How the project's own tools perform this operation: the command, the objects
it creates, patches or deletes, and in which order, with links. They are a
functional and domain reference only: no code, style or text is copied from
them.

## Scope

What is included. What is explicitly excluded, and where it goes instead.

## User scenarios

Journeys that can be tested on their own, in order of priority. Each one is a
concrete Given, When, Then with the result the user observes. At least one is
not the happy path: a refusal by the cluster, a missing permission, a target
that changed while the confirmation was open.

## Requirements

| ID      | Contract                                                              | Acceptance check                    |
| ------- | --------------------------------------------------------------------- | ----------------------------------- |
| REQ-NNN | One testable requirement, with its behavior on success and on failure | The ID of a check in the test table |

Every requirement is defined once, and the test table covers every ID. Words
that cannot be verified, such as fast, intuitive or robust, are not
requirements.

## Design

- **What is written.** Every object the feature creates, patches or deletes,
  with the exact request: verb, kind, fields and patch type. A request that
  creates an object is a write, even when the user only asked to look at
  something.
- **Confirmation.** It names the target, the cluster and the namespace or the
  object, and lists the writes it will perform, in their order. Nothing is
  sent before it is confirmed. If the extension has a write mode, say how it
  applies here.
- **After the write.** No optimistic interface: the view shows what the
  cluster says. A failure is reported with its reason, never swallowed. A
  control that cannot work is disabled and says why.
- **Permissions.** What the user needs, and what the interface shows to a
  user without it.
- **Standard or ad hoc view, and why.** See
  [DESIGN.md](../development/DESIGN.md).
- The Freelens extension points used, what runs in which process, the states
  that are not the happy one, a dark and a light theme, the keyboard,
  cancellation.

## Tests

| Check   | Layer                                                         | Requirements | Scenario and expected evidence         |
| ------- | ------------------------------------------------------------- | ------------ | -------------------------------------- |
| NAME-01 | Unit, in Freelens on static objects, or with the real project | REQ-NNN      | The concrete case and what is asserted |

Every write has a test that reads the result back from the cluster. Say which
checks prove the request alone and which need the real project to answer.

## Success criteria

Measurable outcomes for the user, and explicit failure criteria. Where
automation cannot settle a requirement, the exact manual steps and the
expected result. A test that was not run is unverified, not passed.

## Assumptions and decisions

The defaults that were chosen, and why. `NEEDS CLARIFICATION` marks only a
decision with no reasonable default: at most three, each with a concrete
question and the requirement it affects.

## Notes and deviations

Filled during implementation, when reality diverges from the plan: what
changed, why, and whether it was decided while implementing or approved by
the maintainer.
