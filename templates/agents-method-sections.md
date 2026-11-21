# Method sections for AGENTS.md

The `AGENTS.md` of an extension starts as the one of the template, adapted as
the `create-extension` skill says. The kit adds four sections to it and
nothing else: licensing and provenance, development process, safety, text
rules. They hold what an agent has to know before it touches anything, and
they name the version of the kit the extension follows.

## Where they go

Right after "Project Overview" and before "Common Commands". Some coding
agents read only the first part of a long instruction file, and the guide of
the template is long: what binds has to come first. [Tools](../docs/tools.md)
has the detail.

## How to fill them

- Replace what is in angle brackets. `<Project>` is the name of the project
  the extension is for.
- Fill what the brief answers when the repository starts. The sentence on
  the trademark and the rules of the extension are completed in the pull
  request of `SPEC-0001`, when the reconnaissance has the facts.
- Keep the other rules as they are. Remove the rules about writes only when
  the maintainer has said that the extension will never write: "no write is
  planned" is not never.
- The text rules bind what the extension writes. The generic sections of the
  template stay as they are, as the `create-extension` skill says, apart
  from a rule that restricts a model when the brief replaces it.
- The first rule names MIT, the license of the template and of the
  organization's extensions. An extension under another license names its
  own.
- The text rules keep other software that does the same job out of the
  repository. When the brief says that some may be named, say which and
  where.
- Keep the sections short. The reasons and the procedures are in the kit:
  these sections hold what binds.
- When the extension moves to a newer version of the kit, change the version
  here, in the pull request that applies what changed.

## The sections

```markdown
## Licensing and provenance constraints (critical)

- This extension is MIT and written from scratch, on the structure of
  freelens-example-extension.
- <Project>, its own tools and the other user interfaces for it are
  functional and domain references only. Never copy code, styles, UI strings,
  status logic or generated clients from them. Reading their documentation
  and their CRD schemas to understand fields and semantics is fine; do not
  reproduce their texts verbatim.
- The TypeScript types of the kinds of <Project> are written in this
  repository from the CRD schemas of the reviewed release, never imported or
  copied.
- Use only official upstream repositories, release images and binaries, at
  pinned versions. Do not patch, fork or rebuild an upstream project to make
  the extension work: keep the fix in the extension and in its own setup
  code, and tell the maintainer what the upstream problem blocks.
- The product name is "Freelens extension for <Project>". Never present the
  extension as a product of <Project>. <If the name is a trademark, say whose
  it is.>

## Development process (binding)

This repository follows the Freelens extension kit, version `<version>`:
`https://github.com/freelensapp/freelens-extension-kit/tree/<version>`. It is
developed spec first. Before implementing anything, read these, as far as
they exist yet:

- `docs/process.md` of the kit: spec before code, documents updated in the
  same pull request, closure after the merge, manual testing escalation,
  milestone review.
- `docs/development/ROADMAP.md`: scope and progress. It is the single source
  of truth for both.
- `docs/development/ARCHITECTURE.md`: how the extension reaches the cluster,
  what runs in which process, the decisions the specs share.
- `docs/development/DESIGN.md`: the design decisions of this extension. No UI
  work without reading it.
- `docs/development/TESTING.md`: the test layers, the commands of the test
  environment and the fixtures.
- `docs/specs/`: one spec per feature. SPEC-0001 is the reconnaissance every
  other spec builds on.

Rules that hold on top of the process:

- A draft spec is not approval to implement. Approval is recorded in the
  spec, by role and date, or with the delegation it was given under.
- One small, testable slice per pull request. Do not silently reduce the
  agreed scope.
- Record in each spec the release of <Project> it was written against, tag
  and commit. Behavior present only on its main branch is design guidance.
- A local run is evidence for a pull request, not a status. Never assume or
  invent a CI result.
- A decision taken while implementing is recorded as such, never attributed
  to the maintainer.
- Escalate a blocker of scope, safety, compatibility or platform instead of
  claiming a completion that was not verified.

## Safety rules (binding)

- Read-only first. Every feature that writes to a cluster needs its own
  approved spec.
- Whatever changes the desired state of a resource, interrupts a workload or
  deletes something first asks for an explicit confirmation, which names the
  target and lists what will be written. An action that only asks the
  controller to reconcile again may skip it, if the README declares it and
  the interface shows its outcome.
- Every write is declared in the README, with the permission it needs.
- Development and tests write only to a disposable kind cluster created by
  the scripts of this repository. Never use a shared, remote or real cluster
  as a test target, and never the first or the current context.
- A real cluster is read only when the user named it and authorized the read.
  Connectivity or an entry in a kubeconfig is not permission.
- Data read from a real environment stay on the machine that read them. They
  never go into source, fixtures, specs, documents, logs, screenshots, test
  reports or Git history, and never to an agent, a remote service or hosted
  CI. Fixtures are synthetic.
- Never store, log or forward credentials or signed URLs.
- <The rules of this extension: what it must never do.>

## Text rules

- Project documents, comments and UI text are in English.
- No emoji in Markdown, comments, UI strings, commit messages or pull request
  text.
- No em dash anywhere: use commas, colons, parentheses or full stops.
- No Conventional Commits prefixes in commit subjects or pull request titles.
- Do not name other software that does the same job, and do not mention
  individuals apart from authorship, in any file meant for publication:
  documents, comments, fixtures, screenshots, package metadata, release
  notes. <If the maintainer allows some to be named, say which and where.>
  Authorship is the package fields, the license and the "Authors" section of
  the README. Describe what the extension does factually, without claims of
  priority or superiority.
```
