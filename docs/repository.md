# Starting the repository

The repository of an extension starts as a copy of the template, made with
the `create-extension` skill of
[freelensapp/freelens](https://github.com/freelensapp/freelens/tree/v2.1.0/plugins/freelens).
The skill says what to keep, adapt, remove and rewrite, and how to verify the
result. This document says what the kit adds to it: whose repository it is,
who does what, what the skill leaves open, and what the repository holds
before its first spec.

## Whose repository it is

The repository belongs to whoever builds the extension: a personal account or
any organization, public or private. Nothing here needs the Freelens
organization. A repository there is started only by someone who has the
permission to create one; everyone else starts in a repository of their own,
and [adoption](adoption.md) is a later and separate step.

## Who does what

- **The maintainer** creates the empty repository and decides what cannot be
  guessed: its owner and whether it is public, the npm scope of the package,
  the author and the copyright holder, the first version number, and which
  workflows of the template the repository will run. These are in the
  [brief](brief.md). The secrets, the environments and the apps those
  workflows need are the maintainer's to set up.
- **The contributor** fills the repository with the skill, and stops at a
  repository that builds.
- A coding agent pushes, and opens pull requests, only when the maintainer
  has said that it may.

An agent that loads skills runs `create-extension`. One that does not reads
its `SKILL.md` as a document and follows it. Either way the skill is read in
the checkout of Freelens, at the tag of the targeted release.

## What the skill leaves open

| The skill says                                             | In an extension built with the kit                                                                  |
| ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Remove the `Example` feature, or replace it                | Remove it. Nothing replaces it yet: a feature needs an approved spec                                |
| Keep the preferences store, or remove it                   | Remove it, until a spec needs a setting                                                             |
| Keep the integration tests, or remove them as a whole      | Keep them: the method tests every view in Freelens ([Testing](testing.md))                          |
| Keep the release, version and tag workflows only if wanted | Keep them when the extension will be published with them. Remove them when it will not be published |
| Keep the scheduled maintenance workflows only if wanted    | Keep them, with their environment and its token                                                     |
| Keep the workflows of the CI agent only if wanted          | The maintainer's choice                                                                             |

## What the repository holds before its first spec

- The tooling and the workflows of the template, unchanged.
- No feature: the `Example` kinds, pages, details and menu items are gone,
  and nothing has taken their place.
- `package.json`, `README.md` and `LICENSE` with the names of the brief.
- `AGENTS.md` adapted as the skill says, with the
  [method sections](../templates/agents-method-sections.md) of the kit right
  after "Project Overview".
- Every check the skill lists passes, and the extension installs in Freelens
  without an error in either log.

That is the first commit of the repository, or its first pull request when
the repository already asks for one. It has no spec, because it has no
feature.

The documents of the extension come later, each one with the first thing it
has to say ([Process](process.md#where-the-method-lives-in-an-extension)).
