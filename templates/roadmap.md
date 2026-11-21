# Roadmap

Goal for v1.0.0: the outcome for the user, in two or three sentences.

This file is the single source of truth for scope and progress. Update it in
every pull request that starts, completes or re-scopes a feature. Nothing
moves out of the agreed scope without a decision recorded here.

The extension is built for Freelens `<release>`. It follows `<project>`
`<release>`, reviewed in [SPEC-0001](../specs/SPEC-0001-short-slug.md).

## Releases

- **`<version>`**: the milestones it contains and what the user gets.

## Feature inventory and milestones

Derived from the reconnaissance: the kinds of the project at the reviewed
release, its own tools, and what its users do with them.

Status values: `Planned`, `Draft` (the spec is written, not approved),
`Approved`, `In PR`, `Done`.

### M1 - Name of the milestone (read-only)

| Feature                                                 | Spec                                          | Status  |
| ------------------------------------------------------- | --------------------------------------------- | ------- |
| Reconnaissance, and how the extension reaches a cluster | [SPEC-0001](../specs/SPEC-0001-short-slug.md) | Done    |
| Test environment: kind, definitions and fixtures        | [SPEC-NNNN](../specs/SPEC-NNNN-short-slug.md) | Planned |
| List and details of a kind                              | [SPEC-NNNN](../specs/SPEC-NNNN-short-slug.md) | Planned |

Exit of M1: what is true when the milestone is ready for its review.

### Mn - Write actions (behind explicit confirmation)

| Feature                                                 | Spec                                          | Status  |
| ------------------------------------------------------- | --------------------------------------------- | ------- |
| Ground rules of the write actions, and the first action | [SPEC-NNNN](../specs/SPEC-NNNN-short-slug.md) | Planned |

The first write spec sets the ground rules of every action of the milestone.
Nothing in it ships without a test that reads the result back from the
cluster.

## Out of scope

- What the extension does not do, and where the user does it instead.

## Release criteria for v1.0.0

- Every milestone implemented, each feature behind an approved spec.
- Every feature covered by non-regression tests that run green in CI.
- The documents (specs, architecture, roadmap) aligned with what ships.
