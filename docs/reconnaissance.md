# Reconnaissance

Before any view is specified, the project the extension is for is read at one
release, and what was read is written down. That document is `SPEC-0001`: the
facts every other spec builds on, and the first decisions that follow from
them. It answers the open questions of the [brief](brief.md), it is written
from the [reconnaissance template](../templates/spec-reconnaissance.md), and
it is approved like any other spec ([Process](process.md)).

## What is read

The whole source of the release, at a tag and a commit that are written down,
in the [workspace](workspace.md) and not in the repository of the extension:

- the schemas of its kinds, from the manifests of the release;
- its controllers, and the code they call to decide;
- its own tools, the command line first: what each command reads, creates,
  patches or deletes, and in which order;
- its documentation at that release.

Not memory, not the main branch, not an article. Reading a few controller
files is not enough either: the function that decides whether a field is
written is often somewhere else.

The release is the one the brief names, or the latest stable one on the day
the reconnaissance starts. `SPEC-0001` records it, and the maintainer
approves it with the spec.

## Reference, never source

The project is read to understand fields and semantics. Nothing is taken from
it:

- no code, style, UI text, status logic or generated client is copied, from
  the project or from any other tool for it, and their texts are not
  reproduced;
- the TypeScript types of the kinds are written in the extension from the
  schemas of the release;
- what the project's own tools do is reproduced as behavior, not as code.

The license of every source is noted in `SPEC-0001`. A license that does not
allow reuse changes nothing here, because nothing is reused, but it has to be
known.

When the brief names a reference to match or to surpass, it is read the same
way: what a user can do with it, feature by feature, from its documentation
and from using it. That inventory is kept in the notes of the
[workspace](workspace.md), where the reference can be named. The roadmap is
then checked against it: each feature of the reference is in a milestone, or
out of scope with a reason. What goes into the repository names no other
software, unless the maintainer has said otherwise.

## Questions to answer

- **The surface.** Groups, versions, kinds and their scope. Which release
  serves which version, and what is deprecated.
- **What a status holds.** For each kind, the fields the views will read.
  Phases and condition types are written as closed sets: every value, and
  what each one means.
- **When a field is not written.** For every field a view sorts by, filters
  on or shows as a time: in which states does the controller leave it empty?
  A list sorted by a start time hides exactly the objects that never started.
- **What a controller rewrites.** For every field shown as what the user
  submitted: does a controller fill in defaults or expand it?
- **What ties objects together.** Labels, annotations, owner references and
  names.
- **How the project's own tools do it.** For each operation the extension
  will offer: the requests, their order and the permissions they need.
- **Other endpoints.** Status or metrics endpoints besides the Kubernetes
  API: port, scheme and authentication, and whether the API server can reach
  them for the extension, without credentials.
- **Permissions.** What a user needs for each read, and what the cluster
  answers without it.
- **The host.** What Freelens already shows of these kinds without the
  extension, what its own components do with them, such as its list, its
  details panel and its menus, how the extensions of the organization that
  touch the same kinds read them, and the release of Freelens the extension
  declares it needs. Freelens is read at the release tag the work is pinned
  to, like the project, and at every other release that `engines.freelens`
  admits, since what a view relies on can be missing from an older one. What
  the source leaves open is settled by a probe in the running application, at
  each of those releases.

## Dividing the reading

A project of more than a few kinds is read in parts, by sessions that each
get a closed brief ([task template](../templates/task-brief.md)):

1. Read-only sessions, one for each area: a group of kinds, the project's
   own tools, the host. Each one writes a single note in the notes of the
   [workspace](workspace.md), every fact with its source.
2. The digest is drafted from the notes, in parts when it is long.
3. Each part is checked against the sources by an
   [independent reviewer](review.md#the-independent-reviewer). A digest
   drafted from notes carries wrong and imprecise facts that only this check
   finds.
4. The findings are applied by a session that checks each one against the
   source before it applies it, since a reviewer can be wrong too.

The decisions of `SPEC-0001`, from the architecture to the status model, are
written in the main session, from the reviewed digest.

## What SPEC-0001 holds

1. **Upstream reference.** The sources that were read, by path, at the tag
   and commit of the release, with the license of each.
2. **The digest.** The facts, numbered, each one a sentence with its source.
   A `[check]` of the brief becomes a fact here, or is dropped. Where the
   brief was wrong, the digest says what is true instead.
3. **Architecture decisions.** Whether the extension needs a main process,
   how it reaches the data in order of preference, what it never does, and
   that deprecated forms are shown and never generated. The contracts of the
   project become typed modules: the types written from the schemas, and a
   tested parser for every value that is not a plain field, such as a date in
   a layout of its own or a quantity.
4. **The status model.** How the states of the project map to what the views
   show, as closed sets in pure functions that the lists, the details and
   the overview share, so that they never disagree. An unknown value or a
   missing status is unknown, never healthy.
5. **Spikes.** What can only be proven by trying, each one assigned to the
   spec that will try it. The result is recorded when it comes.
6. **Versions.** The release of the project, the Kubernetes of the test
   cluster and the release of Freelens the work is pinned to.

## Rules

- Released behavior and behavior that exists only on the main branch are
  told apart. Only the first is something the extension relies on.
- A synthetic object of the test environment carries only what the
  controller would write in that state ([Testing](testing.md)). An object
  that carries more makes the tests pass on a view that is wrong.
- The drafts of the specs that state how the project behaves are checked by
  the [independent reviewer](review.md#the-independent-reviewer) against the
  source, before their pull request.
- The reconnaissance is repeated, in small, at every drift watch
  ([Maintenance](maintenance.md)): a new release is read for what changed,
  and the specs it affects record the release they were reviewed against.
