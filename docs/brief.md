# Brief

An extension starts from a brief: a document in which the maintainer
hands over what is already decided and what is already known, so that the
first session neither derives it again nor guesses it. It is the input of the
[reconnaissance](reconnaissance.md) and of the first spec. It is not a spec.

## How it is gathered

By default the coding agent interviews the maintainer and writes the brief
from the answers:

1. It verifies by itself what it can: the source of the project, its
   releases, the names that are free. Those are facts, not questions.
2. It asks for the decisions a step at a time, one to three related
   questions in a step, in the order of the
   [brief template](../templates/brief.md). Each question offers choices,
   its proposal first, and says what each choice leads to. The maintainer
   may answer in words of their own instead.
3. It writes each answer down as it arrives, in the session notes, with the
   words of the maintainer when they wrote their own. An answer in words may
   change the questions that follow.
4. It writes the brief from the template and the answers, and tells the
   maintainer where it is.

A maintainer who prefers to write the brief starts from the template.

## What it holds

1. **Decisions already made.** What is not open for discussion, and what
   nobody else can decide: the name; the repository, its owner and whether it
   is public; the npm scope of the package; the license, the author and the
   copyright holder; the first version number, and whether a prerelease may
   come before it and what for; the release of Freelens the extension
   targets; the version of the kit; who the maintainer is and who reviews
   the domain; whether a coding agent may push and open pull requests, or do
   the work of a milestone under a
   [delegation](process.md#delegation-for-a-milestone); which machines,
   coding agents and models the work may use
   ([Dividing the work](dividing-the-work.md)).
2. **Scope by release.** The goal of the first release, in a sentence: what
   it has to be for its users. What it contains: a few things done properly.
   What comes after it, up to the first stable version, when the first
   release is not that one. Whether the README has screenshots and a video
   ([README](readme.md)).
3. **Facts about the project.** Where its source is, the release to review,
   its kinds and their API groups, what its own tools do and which
   permissions they need, what is deprecated. Each fact is marked
   `[verified]`, with the source it was checked against, or `[check]`.
4. **Existing tools and reference software.** The command line and the user
   interfaces the project already has, and what their users rely on. They are
   a functional reference for the inventory of features, never a source of
   code. The maintainer may name one of them, or another application, as the
   reference: to reach feature parity with it, or to surpass it in features
   and capabilities. The brief also says whether other software may be named
   in the repository. By default it is not.
5. **Architecture guidance.** Whether the extension is likely to need a main
   process, which existing extension is the closest reference, and the ways
   to the data in order of preference.
6. **Safety.** Read-only first. Which operations are dangerous in this
   domain, and what the extension must never do.
7. **Test environment.** What the test cluster has to contain for the views
   to be exercised: the kinds, and the states that matter, healthy and not.
   It is built before feature code.
8. **Open questions for the reconnaissance.** Numbered questions that the
   first session answers by reading the project at the release under review.

## Rules

- The decisions in it are the maintainer's. A coding agent writes the
  brief from the maintainer's answers, but it decides nothing in it.
- A fact is verified or to check, and the brief says which. A `[check]` is
  recollection: the reconnaissance confirms it before a spec relies on it. A
  brief that mixes the two without marks passes guesses on as facts.
- It holds decisions and facts, each fact with its source, and nothing
  more. What was read to write it and is more than a fact goes in a notes
  file beside it, which the reconnaissance starts from and confirms.
- It lives in the [workspace](workspace.md), outside the repository, because
  it may hold what a public repository must not: deadlines, names,
  comparisons with other tools. What is public of it reaches the repository
  through SPEC-0001 and the roadmap.
- It is not kept current. Once the roadmap and the first specs exist, they
  are the source of truth.
