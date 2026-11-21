# Freelens extension kit

The method for building a [Freelens](https://freelens.app) extension with an
AI coding agent, from the first brief to the release.

> This kit is not a theory. It is the method distilled from four official
> Freelens extensions built this way: Kafka, KubeSwift, CloudNativePG and
> Velero. Their specs and histories are public and serve as worked examples.

The kit is being proven on the first extension built with it, for Cluster
API.

Anyone can use it, for an extension of their own, in a repository of their
own, public or private. No step needs the Freelens organization: it comes in
only when an extension is proposed for [adoption](docs/adoption.md).

## How it works

- **Spec first.** An extension is built one feature at a time. A feature is
  written down as a spec, approved, implemented in one pull request with its
  tests, and verified on `main`. No spec, no code.
- **Three roles.** The maintainer decides: approves the specs, or delegates
  them for a milestone, reviews each milestone, decides the releases. The
  contributor, a person or a coding agent, writes the specs, the code and
  the tests. Someone who knows the project checks what the views say about
  it.
- **Facts before views.** The project is read at one release before anything
  is designed. What was read becomes the first spec, and every later spec
  builds on it.
- **A reference, when there is one.** The brief may name other software to
  match feature by feature, or to surpass. It is studied for what its users
  can do, never copied, and by default it is not named in the repository.
- **Read-only first.** The milestones that only read come first. A write to a
  cluster needs its own spec and an explicit confirmation.
- **Verified, then reviewed.** Every feature is tested in a real Freelens. At
  the end of a milestone a script walks every view, and then the maintainer
  reviews the extension by hand.
- **A trace.** Brief, reconnaissance, roadmap, specs, tests, pull requests
  one by one: whoever comes later can read why each thing was built the way
  it was.

## How to use it

1. **Give a brief**: what is decided, the goal and the scope of the first
   release, what you know about the project and what is still to check. Your
   coding agent can gather it, one question at a time with a proposal for
   each, or you write it from [templates/brief.md](templates/brief.md)
   ([docs/brief.md](docs/brief.md)).
2. **Lay out a workspace**: one folder with this kit, Freelens, the template,
   one or more existing extensions, the project the extension is for and any
   other software taken as a reference, side by side, each under its own
   license ([docs/workspace.md](docs/workspace.md)).
3. **Create the repository**, empty, where the extension will live: under
   your own account or organization, public or private. The
   `create-extension` skill of freelensapp/freelens fills it from the
   template: run it yourself, or let your coding agent do it as its first
   task ([docs/repository.md](docs/repository.md)).
4. **Start your coding agent** and point it at the kit, with a request such
   as:

   ```text
   Follow AGENTS.md of freelens-extension-kit to build the extension in
   freelens-<name>-extension. The brief is notes/<name>-brief.md. Find the
   step the work is at, tell me, and stop when the next thing is ready for
   my approval.
   ```

   Until the repository has an `AGENTS.md` of its own, start the agent in the
   workspace and name the kit as above. From then on start it in the folder
   of the extension, so that its `AGENTS.md` loads by itself.

5. **Approve one thing at a time**: the reconnaissance, the roadmap, then
   each spec before it is implemented. Review and merge one pull request for
   each feature slice. Or delegate the work of a milestone to your coding
   agent and review it at the end ([docs/process.md](docs/process.md)).
6. **Review each milestone** in a real Freelens, with the report of the
   pre-review pass in hand ([docs/review.md](docs/review.md)).
7. **Release** with the workflows of the template
   ([docs/release.md](docs/release.md)), and keep the extension current
   ([docs/maintenance.md](docs/maintenance.md)).

Without a coding agent the steps are the same, done by hand.

Two documents are optional: how to write the README of the extension, with
its screenshots and its video ([docs/readme.md](docs/readme.md)), and how to
divide the work when there is more than one machine, coding agent or model
([docs/dividing-the-work.md](docs/dividing-the-work.md)).

Two other cases have a way in of their own: an extension written in the
community that wants to become an official one
([docs/adoption.md](docs/adoption.md)), and an extension written for the v1
extension API, which the `port-extension-to-v2` skill of freelensapp/freelens
ports.

## What is in it

- [AGENTS.md](AGENTS.md): the path of an extension, step by step, and the
  rules that hold at every step. It is the one text a coding agent starts
  from.
- [docs/](docs): one document for each step, from the
  [brief](docs/brief.md) to [maintenance](docs/maintenance.md), the two
  optional ones, and
  [how a community extension becomes an official one](docs/adoption.md).
- [templates/](templates): what an extension starts from. The brief, the
  session notes, the roadmap, the three forms of a spec and the method
  sections of its `AGENTS.md`.
- [skills/](skills): one skill in the Agent Skills format, a thin pointer to
  `AGENTS.md` for the agents that load skills.

## What is not in it

The technical half, which lives upstream and is not repeated here:

- the extension API, in the
  [extension documents](https://github.com/freelensapp/freelens/tree/v2.1.0/docs/extensions)
  of Freelens;
- the template of an extension,
  [freelens-example-extension](https://github.com/freelensapp/freelens-example-extension),
  with the reason of every pattern in its `AGENTS.md`;
- the `create-extension` and `port-extension-to-v2` skills of
  [freelensapp/freelens](https://github.com/freelensapp/freelens/tree/v2.1.0/plugins/freelens).

The kit begins where `create-extension` ends: with a repository that builds,
and the question of what to put in it and in which order.

## Coding agents

The kit is plain Markdown that any agent can follow. `AGENTS.md` is its only
instruction file; the other two are pointers to it.

| Agent          | Reads `AGENTS.md`                     | An extension was built with it this way |
| -------------- | ------------------------------------- | --------------------------------------- |
| Claude Code    | Through `CLAUDE.md`, which imports it | Yes                                     |
| GitHub Copilot | Directly                              | Not yet                                 |
| Codex          | Directly                              | Not yet                                 |
| Cursor         | Directly                              | Not yet                                 |
| Gemini CLI     | Through `GEMINI.md`, which imports it | Not yet                                 |
| OpenCode       | Directly                              | Not yet                                 |

The second column is what the documentation of each agent says.
[Tools](docs/tools.md) has the details.

## Versions

The kit targets Freelens 2. It was last checked against Freelens 2.1.0 and
against the template at commit `5c75d60`.

An extension names the version of the kit it follows in its `AGENTS.md`, and
moves to a newer one with a pull request. When the kit is wrong or silent,
the kit is fixed first.

## License

Copyright (c) 2025-2026 Freelens Authors.

[MIT License](https://opensource.org/licenses/MIT)
