# AGENTS.md

This file guides coding agents, and the people who work with them, through
the Freelens extension kit: the method for building a Freelens extension
feature by feature, distilled from the extensions of the Freelens
organization that were built this way.

The kit is documents, not code. Each step below points to the document that
holds it. Read a document when you reach its step, and follow the document,
not a summary of it.

## Explaining the kit

When someone asks what the kit is, how it works or how to use it, answer from
[README.md](README.md): "How it works" and "How to use it". Then say which
step of the path their work is at, and name the document of that step. Do not
explain the kit from memory.

## What the kit does not repeat

The technical half lives upstream:

- the extension API and its contracts, in the
  [extension documents](https://github.com/freelensapp/freelens/tree/v2.1.0/docs/extensions)
  of Freelens;
- the build, type-check, test, lint and CI patterns, in the `AGENTS.md` of
  the template,
  [freelens-example-extension](https://github.com/freelensapp/freelens-example-extension);
- how to start an extension, or port one from the v1 API, in the
  `create-extension` and `port-extension-to-v2` skills of
  [freelensapp/freelens](https://github.com/freelensapp/freelens/tree/v2.1.0/plugins/freelens).

When a rule of the kit contradicts one of them, they win and the kit has a
defect to report.

## The path of an extension

1. **Brief.** What is decided and what is known, from the answers of the
   maintainer ([docs/brief.md](docs/brief.md)).
2. **Workspace.** This kit, Freelens, the template, existing extensions, the
   project and any software taken as a reference, side by side
   ([docs/workspace.md](docs/workspace.md)).
3. **Repository.** Start it with the `create-extension` skill and add the
   [method sections](templates/agents-method-sections.md) to its `AGENTS.md`
   ([docs/repository.md](docs/repository.md)).
4. **Reconnaissance.** Read the project at one release and write SPEC-0001
   ([docs/reconnaissance.md](docs/reconnaissance.md)).
5. **Roadmap.** Once SPEC-0001 is approved, the features by milestone,
   read-only first, from the [template](templates/roadmap.md)
   ([docs/specs.md](docs/specs.md#the-roadmap)).
6. **Test environment.** Before feature code
   ([docs/testing.md](docs/testing.md)).
7. **Features.** One spec, one approval and one pull request at a time
   ([docs/process.md](docs/process.md)), under the rules of
   [docs/design.md](docs/design.md) and [docs/safety.md](docs/safety.md).
8. **Milestone review.** The pre-review pass, then the maintainer in a real
   Freelens ([docs/review.md](docs/review.md)).
9. **Release.** With the workflows of the template
   ([docs/release.md](docs/release.md)).
10. **Maintenance.** The project, Freelens, the template and this kit move:
    the extension follows ([docs/maintenance.md](docs/maintenance.md)).

To find the step the work is at, read the session notes of the workspace,
then the roadmap of the extension and the status of its specs:

| What is there                                         | The work is at                       |
| ----------------------------------------------------- | ------------------------------------ |
| No brief                                              | Step 1                               |
| A brief, and a workspace that lacks a checkout        | Step 2                               |
| No repository, or one that is still the bare template | Step 3                               |
| A repository that builds, and no approved SPEC-0001   | Step 4                               |
| SPEC-0001 approved, and no roadmap                    | Step 5                               |
| A roadmap, and no test environment                    | Step 6                               |
| Features of the roadmap that are not done             | Step 7, at the first one that is not |
| Every feature of a milestone done                     | Step 8                               |

With no brief, gather it from the maintainer, one question at a time, as
[docs/brief.md](docs/brief.md) says. Do not decide in their place.

Also: how a community extension becomes an official one
([docs/adoption.md](docs/adoption.md)), the worked examples
([docs/examples.md](docs/examples.md)), and how each coding agent reads these
files and runs the checks ([docs/tools.md](docs/tools.md)).

Two documents are optional. Offer them, and follow them when the maintainer
wants them:

- the README of the extension, with its screenshots and its video
  ([docs/readme.md](docs/readme.md));
- the division of the work when there is more than one machine, coding agent
  or model ([docs/dividing-the-work.md](docs/dividing-the-work.md)).

## Rules that hold at every step

- **Sources, not memory.** Read the code of Freelens, the template and the
  project at the versions the work is pinned to, and Freelens also at every
  release that `engines.freelens` admits
  ([Reconnaissance](docs/reconnaissance.md)). Most extension code found
  elsewhere is written for the v1 API, which Freelens 2 does not load.
- **Verify, then say.** Verify everything before reporting it, the interface
  included, as a person would use it. Say what could not be verified, as
  such. A check that was never seen failing proves nothing.
- **Ask what is not yours to decide.** Scope, safety and what is meant to be
  public belong to the maintainer. Do not guess them. Push, open pull
  requests and merge them only as far as the maintainer has said that you
  may ([delegation](docs/process.md#delegation-for-a-milestone)).
- **Spec before code.** No implementation without an approved spec. Approvals
  are recorded by role and date, or with the delegation they were given
  under.
- **Read-only first.** A write to a cluster needs its own spec and an explicit
  confirmation. Development and tests write only to a disposable cluster.
  Data of a real environment never leave the machine that read them.
- **Reference, never source.** The project and the other tools for it show
  what to build, and the brief may name one to match or to surpass. No code,
  style or text is copied from them.
- **Plain text rules.** English. No emoji and no em dash. In any file meant
  for publication, no individuals apart from authorship, and no other
  software that does the same job by name, unless the maintainer says
  otherwise.
- **The model for the task.** Whoever starts a session chooses its model for
  the task at hand, and no check is loosened to fit a model
  ([docs/tools.md](docs/tools.md#choosing-a-model)).
- **Fix the kit first.** When the kit is wrong or silent, say so, and the
  kit is changed. Nothing is worked around in the extension without a word
  ([docs/maintenance.md](docs/maintenance.md#the-version-of-the-kit)).

## Working on the kit itself

- Extract, do not design. A rule enters the kit after it was used on a real
  extension. The pull request says where it comes from; the document does
  not.
- One source. A rule lives in one document and the others link to it.
  Procedures are plain Markdown that any agent or person can follow. A skill,
  or any file for one tool, is a thin wrapper around them and never the only
  place where a rule lives.
- Documents carry no issue numbers, dates or history of decisions. Git and
  the pull requests hold those. Only the README says which versions the kit
  was last checked against.
- No person, company, machine or private environment is named anywhere in
  the repository.
- Links to the Freelens documents and skills point to a release tag. The
  template is read at `main`.
- Markdown follows the format of the organization's repositories: lines of
  80 columns, aligned tables, one top-level heading and a language on every
  code block.
- A version of the kit is a tag, `vX.Y.Z`, with release notes on GitHub.
  There is no changelog file.
