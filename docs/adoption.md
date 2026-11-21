# Adopting a community extension

A Freelens extension does not need the Freelens organization. Anyone can build
one, publish it under an npm scope of their own and keep it in their own
repository: the `create-extension` skill of
[freelensapp/freelens](https://github.com/freelensapp/freelens/tree/v2.1.0/plugins/freelens)
starts an extension that way.

This document is about the other case: an extension written in the community
whose author would like it to become an official one, in the
[freelensapp](https://github.com/freelensapp) organization on GitHub, next to
the extensions the organization builds itself. It says what adoption means,
the criteria an adopted extension meets, and the path from the author's
repository to the first release from the organization. Every criterion and
every step comes from extensions that were adopted this way.

## What adoption means

- The repository lives in the organization as `freelens-<name>-extension`,
  created from the template,
  [freelens-example-extension](https://github.com/freelensapp/freelens-example-extension),
  with the settings of the template.
- The package is published as `@freelensapp/<name>-extension` and described as
  "Freelens extension for" followed by the name of the project.
- The author remains the creator and the maintainer of the extension, and the
  "Authors" section of the README says so.
- The code keeps its history: it enters through a pull request that is merged
  with a merge commit.
- From then on the author works through pull requests from a fork. The
  maintainers of the organization review them, merge them and launch the
  releases.
- The license and the package fields are those of the template: MIT, with the
  copyright notice of the organization's repositories.

The author asks for it in the
[discussions of freelensapp/freelens](https://github.com/freelensapp/freelens/discussions).
The maintainers of the organization decide after the review.

## Criteria

The first six hold in the author's repository before the move, and the review
checks them. The last four hold by the first release from the organization:
the alignment pull request brings what is missing, so the author is not asked
for them beforehand.

### Before the move

1. **License and provenance.** A permissive license, MIT in the organization's
   repositories. The code is the author's own, or its origin and its license
   are clear.
2. **A clean history.** No secret, no personal path and no reference to an
   employer, a customer or a private environment, in any commit. The history
   is imported as it is, so it has to be clean before it enters.
3. **Freelens 2.** The extension is written for the v2 extension API and
   declares `engines.freelens` as the template does. An extension written for
   the v1 API is ported first, with the `port-extension-to-v2` skill.
4. **It works in Freelens.** On the official Freelens package, installed the
   way a user installs it, against a [kind](https://kind.sigs.k8s.io/) cluster
   that runs the real project, as an administrator and as a read-only user.
   Every page, details panel and menu item is opened. Every action is checked
   by reading the cluster before and after it: an interface that shows no
   error proves nothing.
5. **Writes are confirmed.** Whatever changes the desired state of a resource,
   interrupts a workload or deletes something first asks for an explicit
   confirmation, which names the target and lists what will be written. The
   one exception is an action that only asks the controller to reconcile
   again: it may run without a confirmation when the README declares it and
   the interface shows its outcome. [Safety](safety.md) has the whole rule.
6. **Unit tests.** They exist and they pass.

### By the first release from the organization

7. **The shape of the template.** The tooling and the agent files that the
   `create-extension` skill lists as kept, and every workflow, are those of
   the template, with nothing added. `AGENTS.md` keeps the generic sections of
   the template as they are. The README has the sections of the organization's
   extensions ([README](readme.md)): Overview, with a short video and
   screenshots, Authors,
   Requirements, Supported APIs, Permissions, Install, Getting started,
   Features, Limits, Build from the source, License. "Permissions" declares
   everything the extension writes to the cluster and the permission each
   write needs.
8. **Integration tests in Freelens.** They follow the pattern of the template:
   at least the session that installs the extension and fails on any error
   either process logs. The sessions that walk its views on a kind cluster
   with fixtures are expected too.
9. **Releases through the workflow of the template.** A version tag publishes
   the package to npm and creates a GitHub release with the tarball, its
   checksum and an SBOM. Once the package exists on npm, trusted publishing is
   set up for it, and from then on every release carries its provenance.
   Nothing is published from a workstation.
10. **Renovate.** The `.renovaterc.json` of the template, with the Renovate
    app on the repository.

## The path

1. **Review.** A maintainer of the organization does it, read only and in
   this order:
   1. The code, before anything runs: the repository cloned at a pinned
      commit, the published package compared with the source, the
      dependencies and their install scripts, network access, child
      processes, dynamic evaluation, obfuscated code, credentials,
      environment variables and workflows. The extension runs only after
      this check is clean.
   2. Readiness for Freelens 2 (criterion 3).
   3. Quality next to the official extensions: structure, tests, README,
      loading, empty and error states, a dark and a light theme, writes and
      their confirmations.
   4. Coverage: which kinds and which features of the project the extension
      shows.
   5. The trial in the application (criterion 4).
2. **Outcome to the author.** An issue on the author's repository, written
   from the [outcome template](../templates/review-outcome.md), with three
   parts in this order: what is left before the move, the rest, what works.
   The author is asked only for what truly blocks the move, and each of those
   points comes with a way that was already tried and with the commands that
   verify it. The rest is for the author or for the alignment pull request,
   whichever comes first, so that a review does not turn into round after
   round.
3. **Repository in the organization.** The maintainers create it from the
   template, with the settings of the template, and invite the author as a
   collaborator.
4. **Import pull request.** The author opens a pull request from a fork that
   brings the code with its whole history. The maintainers check that its tree
   is the one that was reviewed, review any commit added since, and check the
   history against criterion 2. It is merged with a merge commit. A history
   that needs cleaning is cleaned before the pull request is opened. If
   something turns up later, the author rewrites the branch of that same pull
   request, so that no ref of the organization's repository keeps the old
   commits.
5. **Alignment pull request.** The maintainers open it. It brings the tooling
   and the workflows of the template, the package renamed to
   `@freelensapp/<name>-extension`, the integration tests, the agent files
   and the README in its sections, with the author credited as creator and
   maintainer. It can also take what the review left open. The author reviews
   it.
6. **First release from the organization.** It is made with the release
   workflow of the template, after a trial of the production tarball in the
   official Freelens package. Then the author deprecates the old package on
   npm, pointing to the new name, and archives the old repository.
7. **After the release.** What is still left of the review becomes improvement
   issues on the organization's repository. Not earlier: until the first
   release the review lives in the issue of step 2. The extension is
   announced on the Freelens channels and in the community of the project it
   is for.

## Working on an adopted extension

The author opens pull requests from the fork and says when one is ready. The
maintainers verify it and merge it, and before a release they try the
production tarball in the official Freelens package. An adopted extension is
maintained like every other extension of the organization:
[Maintenance](maintenance.md) covers the dependencies, the template and the
project the extension follows.
