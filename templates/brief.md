# Freelens extension for `<Project>`: brief

Input for the reconnaissance and for SPEC-0001, not a spec. Facts marked
`[verified]` were checked against the source named next to them. Facts marked
`[check]` are recollection: the reconnaissance confirms them before a spec
relies on them.

## 1. Decisions already made

- Name: "Freelens extension for `<Project>`".
- Repository: `<owner>/freelens-<name>-extension`, public or private.
- Package: `<scope>/<name>-extension`, in an npm scope the publisher owns.
- License: `<license>`. Author and copyright holder: `<who>`. Written from
  scratch.
- First version number: `<version>`. The first stable version is `1.0.0`.
- Prerelease before the first release: none, or what it is for.
- Freelens: the release the extension targets.
- Method: the Freelens extension kit, version `<version>`.
- Maintainer: who approves the specs and reviews the milestones. Reviewer of
  the domain: who checks what the views say about the project.
- What a coding agent may do on its own: nothing; push and open pull
  requests; or the work of a milestone, under the
  [delegation](../docs/process.md#delegation-for-a-milestone), and what the
  delegation leaves out.
- Machines, coding agents and models the work may use, and the limits of
  each.
- A rule of the template that restricts a model, if it has one: kept as it
  is, or replaced by the rule of choosing the model for the task
  ([Choosing a model](../docs/tools.md#choosing-a-model)).
- Workflows of the template the repository will run: release, scheduled
  maintenance, the CI agent.
- Anything else that is not open for discussion.

## 2. Scope

**Goal of the first release:** what it has to be for its users, in one
sentence.

**First release:** what it contains, the features that only read first.

1. A few things done properly.

**After it, up to the first stable version:** the rest, in the order it is
likely to come.

**README:** with screenshots and a demo video, or text only
([README](../docs/readme.md)).

## 3. Facts about the project

- Source: the repository of the project, and of its tools when they live
  elsewhere `[verified: source]`.
- Release to review: `<version>` `[verified: source]`, or the latest stable
  one on the day the reconnaissance starts. Every spec records the release
  it was written against.
- Kinds: `<group>/<version>`: `<kinds>` `[verified: source]` or `[check]`.
- What its own tools do: the command, what it reads or writes, which
  permissions it needs `[verified: source]` or `[check]`.
- Deprecated or changing: what must not be shown or generated as the default
  `[verified: source]` or `[check]`.
- Name: whether it is a trademark, and whose `[verified: source]` or
  `[check]`.

## 4. Existing tools and reference software

The command line and the user interfaces the project already has, and what
their users rely on. A functional reference for the inventory of features,
never a source of code.

- The reference to match or to surpass: which one, or none. How far: feature
  parity, or the features and capabilities to do better.
- Other software named in the repository: no, or which and where.

## 5. Architecture guidance

- Renderer only, or a main process too, and why.
- The closest reference extension, and what to take from it.
- The ways to the data, in order of preference.

## 6. Safety rules

- Read-only first. Each write gets its own later spec, behind an explicit
  confirmation that names the target. Or: this extension never writes.
- The operations that are dangerous in this domain.
- What the extension must never do.

## 7. Test environment, before feature code

A kind cluster with the definitions of the project at the release under
review, one object of each kind in each state that matters, healthy and not,
and what needs the real project running.

## 8. Open questions for the reconnaissance

1. A question that the first session answers by reading the project at the
   release under review.
