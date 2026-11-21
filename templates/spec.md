# SPEC-NNNN: Title

- **Status:** Draft
- **Milestone:** `M<n>` (see [ROADMAP.md](../development/ROADMAP.md))
- **Reviewed project:** release tag and commit
- **Freelens:** release the extension is built and tested against
- **Dependencies:** approved specs this one builds on, or none
- **Approval:** Pending; later the role, the date and the scope, without names,
  or the delegation it was approved under

## Goal

What the user can do when this is done, in one or two sentences.

## Upstream reference

The concepts of the project, the commands of its own tools and the pages of
its documentation that this feature relates to, with links. They are a
functional and domain reference only: no code, style or text is copied from
them.

## Scope

What is included. What is explicitly excluded, and where it goes instead.

## Design

- **Standard or ad hoc view, and why.** Whether the task is best served by a
  list with its details or by an ad hoc view, such as an overview, a
  topology, a timeline or a live panel, and what makes it the best experience
  for the task ([DESIGN.md](../development/DESIGN.md)). For an ad hoc view,
  describe its parts: what each one shows, where its data come from and what
  each click leads to.
- The kinds and the endpoints involved and the fields read, from the schemas
  of the reviewed release and the facts recorded in SPEC-0001.
- The Freelens extension points used: pages, details panels, menu items.
- The columns, the panels and their content, as a sketch or a description.
- The states that are not the happy one: loading, empty, restricted, failed.
- Conformance to [DESIGN.md](../development/DESIGN.md), in a dark and in a
  light theme. A
  deviation is declared here and updates DESIGN.md in the same pull request,
  or is dropped.
- **Safety.** What the feature reads. That it writes nothing, and how the
  tests prove it.

## Tests

- Unit: `<test file>`: `<cases>`
- In Freelens, on the definitions of the project and static objects:
  `<what the session asserts>`
- With the real project, only if a controller has to answer:
  `<what is checked>`
- Manual verification, if any: the exact steps and the expected outcome of
  each. Later, the recorded result: date, role, outcome.

## Notes and deviations

Filled during implementation, when reality diverges from the plan: what
changed, why, and whether it was decided while implementing or approved by
the maintainer.
