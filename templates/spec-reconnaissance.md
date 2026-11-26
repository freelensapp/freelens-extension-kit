# SPEC-0001: Reconnaissance

- **Status:** Draft
- **Milestone:** `M1` (see [ROADMAP.md](../development/ROADMAP.md))
- **Reviewed project:** release tag and commit
- **Freelens:** release the extension is built and tested against
- **Dependencies:** none
- **Approval:** Pending; later the role, the date and the scope, without names

This spec has no code of its own. It goes from Draft to Approved and stays
there: the specs that build on it carry the implementation.

## Goal

Fix the facts about the project that every other spec builds on, and the
first decisions that follow from them.

## Upstream reference

The sources that were read, by path, at the tag and commit of the release,
with the license of each: the manifests with the schemas of the kinds, the
controllers and the code they call to decide, the project's own tools, its
documentation at that release. They are a reference for behavior: nothing is
copied from them.

## Scope

What this reconnaissance covers, and what it leaves to a later one. The open
questions of the brief that it answers.

## Digest

Numbered facts, each one a sentence with its source.

### R1. The surface

Groups, versions, kinds and their scope. Which release serves which version.
What is deprecated.

### R2. What a status holds

For each kind, the fields the views will read. Phases and condition types as
closed sets: every value, and what each one means. For every field a view
will sort by, filter on or show as a time, the states in which it is not
written. What a controller rewrites of what the user submitted.

### R3. What ties objects together

Labels, annotations, owner references and names.

### R4. How the project's own tools do it

For each operation the extension will offer: the requests, their order and
the permissions they need.

### R5. Other endpoints

Status or metrics endpoints besides the Kubernetes API: port, scheme and
authentication, and whether the API server can reach them for the extension,
without credentials.

### R6. Permissions

What a user needs for each read, and what the cluster answers without it.

### R7. The host

What Freelens shows of these kinds without the extension, what its own
components do with them, how the extensions of the organization that touch
the same kinds read them, and the release of Freelens the extension declares
it needs. Each fact cites Freelens at its release tag, and says so when it
does not hold at every release that `engines.freelens` admits.

### Corrections to the brief

Every `[check]` of the brief: confirmed, corrected or dropped.

## Architecture decisions

- **A1.** Renderer only, or a main process too, and why.
- **A2.** How the data are reached, in order of preference.
- **A3.** What the extension never does.
- **A4.** The contracts of the project as typed modules: the types written
  from the schemas, and a tested parser for every value that is not a plain
  field, such as a date in a layout of its own or a quantity.
- **A5.** Deprecated forms are shown with a label and never generated.

## Status model

- **H1.** The states the views show, as a closed set, and the rule that maps
  the states of the project to each one. A scale the project has of its own,
  such as a severity, is mapped here too. An unknown value or a missing
  status is Unknown, never healthy.

The model lives in pure functions that the lists, the details and the
overview share.

## Spikes

- **S1.** What can only be proven by trying, and the spec that will try it.
  Later, the result.

## Versions

The release of the project, the Kubernetes of the test cluster and the
release of Freelens that the work is pinned to.

## Notes and deviations

Filled later: the results of the spikes, and what a drift watch changed.
