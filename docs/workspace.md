# Workspace

The method takes what it knows from sources, not from memory. How Freelens
behaves is read in its code. How an extension is put together is read in the
template and in the extensions that exist. What the project does is read in
the project. So the work happens in one folder that holds them side by side,
where a person or a coding agent can read them all.

## Layout

```text
workspace/
  freelens/                        Freelens, at the tag of the targeted release
  freelens-example-extension/      the template, at main
  freelens-extension-kit/          this kit, at the version the extension follows
  freelens-<other>-extension/      one or more existing extensions
  <project>/                       what the extension is for, at one release
  <reference>/                     optional: other software taken as a reference
  freelens-<name>-extension/       the new extension
  notes/                           the brief and the session notes
```

| Checkout                               | At                                | Read for                                                                                                                                                                        |
| -------------------------------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| freelensapp/freelens                   | The tag of the release it targets | How the host behaves: what a list, a details panel or a menu does, and what the host gives an extension. It also runs as Freelens dev for the integration tests.                |
| freelensapp/freelens-example-extension | `main`                            | The patterns of an extension and the reason of each, in its `AGENTS.md`.                                                                                                        |
| This kit                               | The version the extension follows | The method.                                                                                                                                                                     |
| Existing extensions, one or more       | Their latest release              | Worked examples close to the new extension ([Examples](examples.md)).                                                                                                           |
| What the extension is for              | The release under review          | The [reconnaissance](reconnaissance.md): an operator or any other software, the schemas of its kinds and what its own tools do. A reference for behavior, not a source of code. |
| Other software taken as a reference    | A release that is written down    | Optional. What its users can do, when the [brief](brief.md) names it as the one to match or to surpass, or as an inspiration.                                                   |

Copyright and license hold for every checkout. Each one is read under its own
license, which `SPEC-0001` notes, and nothing is copied from it: no code, no
style, no text. Where a license does not allow more, the software is used and
its documentation is read, and its source is left alone.

Three rules hold for the checkouts that are not the new extension:

- They are read only. A problem found in one of them is reported where it
  belongs, not patched in place: a gap in the Freelens documents, in
  `@freelensapp/extensions` or in the skills to
  [freelensapp/freelens](https://github.com/freelensapp/freelens/issues), one
  in the template to
  [freelensapp/freelens-example-extension](https://github.com/freelensapp/freelens-example-extension/issues),
  one in the method to this kit
  ([Maintenance](maintenance.md#the-version-of-the-kit)).
- Each one is at a known commit. Check it before relying on what the checkout
  says: a checkout left behind states things that are no longer true.
- `notes/` is outside every repository, so that nothing in it can be
  committed by mistake.

## Laying it out

```sh
git clone --branch <tag> https://github.com/freelensapp/freelens.git
git clone https://github.com/freelensapp/freelens-example-extension.git
git clone --branch <version> https://github.com/freelensapp/freelens-extension-kit.git
git clone --branch <tag> <repository of an existing extension>
git clone --branch <tag> <repository of the project>
git clone --branch <tag> <repository of the reference software>
git -C <checkout> describe --tags --always
```

The last command says where a checkout is. The [brief](brief.md) names the
release of Freelens, the existing extensions, the repository of the project
and the reference software, if there is one. A project whose tools live in a
repository of their own takes a checkout for each.

The skills of freelensapp/freelens are part of its releases from 2.1.0 on,
so they are read in the same checkout, at the tag of the targeted release.

When the folder already holds checkouts with these names at other commits,
the pinned ones go in a folder of their own, and the session notes say
which.

## What the machine needs

- Git, and network access to github.com.
- Node.js at the version of `.nvmrc` and pnpm through corepack, as "Build from
  the source" in the README of the template says.
- For the test environment, a running Docker daemon, with
  [kind](https://kind.sigs.k8s.io/) and `kubectl` on `PATH`.
- For the trials on what users run, the official Freelens package of the
  targeted release.
- On Linux, the shared libraries Electron needs at run time, which
  `DEVELOPMENT.md` of Freelens names.

One machine and one coding agent are enough. With more of either, or with a
model that runs on a machine of one's own,
[Dividing the work](dividing-the-work.md) says how to use them.

## The checks in the application

Whoever writes a feature verifies it in the application as a person would:
every page, details panel and menu item, in a dark and in a light theme.
There are two places to do it:

- **Freelens dev.** `pnpm dev` in the Freelens checkout, once it is set up as
  `DEVELOPMENT.md` of Freelens says, starts the application with a debugging
  port, and the integration tests, a script or a browser automation tool
  attach to it. "Checking the Extension in Freelens Dev" in the `AGENTS.md` of
  the template says how to install the checkout, drive the interface and read
  the console.
- **The official package.** What users run. A release is tried there
  ([Release](release.md)).

[Tools](tools.md#running-the-checks-with-any-agent) says how a coding agent
runs these checks.

## Where a coding agent starts

A coding agent loads the instruction file of the folder it is started in. So
it is started in the folder of the extension, where `AGENTS.md` has the guide
of the template and the method sections that point to this kit. Before that
file exists, it is started in the workspace, and the request names the
`AGENTS.md` of the kit.

## Session notes

Building an extension takes many sessions, and a coding agent starts each one
knowing nothing of the last. What carries the work across is a file:

- one for each extension, in `notes/`, started from the
  [template](../templates/session-notes.md);
- at its top, where the work stands and what comes next, so that a session
  resumes from the first lines;
- below, the decisions, each with its date and the words of who took it;
- read at the start of every session, and updated when a decision is taken
  and when the session ends.

Once the repository has its roadmap and its specs, they are the source of
truth for scope and progress. The notes keep the state of the session and
what does not belong in a repository. The file works the same for every tool,
with or without a memory of its own.

The [brief](brief.md) lives in `notes/` too.
