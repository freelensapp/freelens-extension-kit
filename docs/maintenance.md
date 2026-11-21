# Maintenance

An extension depends on four things that move on their own schedule. Each one
has a watch, run at the start of every milestone and before every release
([Process](process.md#drift-watches)), and each watch leaves a trace: the
version that was reviewed, written where the extension pins it.

| What moves   | Where the extension pins it                               | Watch                                             |
| ------------ | --------------------------------------------------------- | ------------------------------------------------- |
| The project  | The reviewed release, in SPEC-0001 and in each spec       | [Upstream drift](#upstream-drift)                 |
| Freelens     | `engines.freelens`, the SDK and the Freelens of the tests | [A release of Freelens](#a-release-of-freelens)   |
| The template | The files the extension shares with it                    | [Template alignment](#template-alignment)         |
| This kit     | The version in the method sections of `AGENTS.md`         | [The version of the kit](#the-version-of-the-kit) |

## Upstream drift

The project releases when it wants, and its API gains fields, states and
kinds as it does.

1. Read the latest release of the project and its release notes.
2. Compare the schemas of its kinds with the release the types were written
   from.
3. Record the tag and the commit that were reviewed in the specs they affect.
4. Open an issue for every breaking change, for every state the status model
   does not know, and for every field newly deprecated that the extension
   still shows as current.

It is a [reconnaissance](reconnaissance.md) in small. Behavior that exists
only on the main branch of the project is design guidance, never something to
rely on.

Renovate follows the versions of the test environment. A pull request that
moves the project there asks for this watch before it is merged.

## A release of Freelens

`engines.freelens` names the oldest release the extension runs on, and stays
there. Renovate brings each release of the SDK. Before that pull request is
merged:

1. Read what the release changed in the extension API, in its documents and
   in the template.
2. Move together every place that names the version of Freelens: the
   Freelens the tests run on, and the documents.
3. Record the reading in the pull request: the release, what changed for the
   extension, and what was taken in or why nothing was.

A new major version of Freelens needs a spec of its own.

## Template alignment

The tooling, the workflows and the generic sections of `AGENTS.md` are those
of the template: the `create-extension` skill lists them. The template moves,
and an extension that does not follow it drifts, one file at a time.

1. Compare the shared files with the template at `main`: what the skill lists
   under "Keep as is", the workflows, the generic sections of `AGENTS.md`.
2. Open one alignment pull request that brings them over, with nothing else
   in it. Its title says what is aligned.
3. A defect found in a shared file is reported to the template and fixed
   there first. The extension then takes the fix by aligning.

What an extension adds of its own, such as the workflows of its test
environment, stays its own. What it shares stays identical.

## The version of the kit

The method sections of `AGENTS.md` name the version of the kit the extension
follows. At the start of a milestone, look for a newer one, read its release
notes, apply what changed, and move the version in the same pull request.

When the kit is wrong or silent, nothing is worked around in the extension
without a word:

1. The contributor tells the maintainer what is wrong or missing, with the
   file and the line, and what it would do instead.
2. The change goes to the kit: a pull request from who can open one, an issue
   from who cannot.
3. The work goes on with the answer the maintainer gives. Until a version of
   the kit carries it, that answer is written in the session notes, or in the
   spec it affects, as an assumption.

So the work never waits for a release of the kit, and the kit learns from
every extension built with it.

## Dependencies

Renovate keeps the dependencies current, with the configuration of the
template. Its `AGENTS.md` explains every setting, and why some libraries take
the version Freelens has instead of the newest one.

The scheduled workflows of the template open pull requests of their own,
which are reviewed and merged like any other.

## An extension written for the v1 API

It is ported with the `port-extension-to-v2` skill of
[freelensapp/freelens](https://github.com/freelensapp/freelens/tree/v2.1.0/plugins/freelens):
a migration issue with numbered steps, and one issue for each feature. That
is not the loop of this kit, which starts where a port ends.

## Defects

A defect reported by a user becomes an issue, and its fix a pull request with
a test that fails without it ([Testing](testing.md#non-regression-policy)).
A new feature goes through the loop: a spec first.
