# Release

A release is made by the workflows of the template, never by hand. This
document says what an extension checks before and after one, and what is
different the first time a package is published.

## The flow

The template has three workflows for it. The `create-extension` skill lists
them, with the environment and the secret each one needs, under "Workflows
tied to the repository":

1. The version workflow opens a pull request that changes the version.
   Nothing else changes it.
2. When that pull request is merged, the tag workflow tags `main`.
3. The tag starts the release workflow: it builds, packs, publishes the
   package to npm and creates a GitHub release with the tarball and its SBOM,
   each with its checksum, and attests where each file was built.

A version with a hyphen is a prerelease: it goes to the `next` tag of npm, and
its GitHub release is marked as a prerelease.

Nothing is published from a workstation, and no tag is created by hand.

## An extension that is not published

An extension in a private repository, or one that is not meant for the
registry, keeps every check of this document and drops the publication. It
removes the release workflows
([Starting the repository](repository.md#what-the-skill-leaves-open)), and it
is installed from a tarball or from a directory, as "Install" in the README
of the template says. From Freelens 2.1.0 on, a tarball without its
`.tgz.sha256` beside it installs disabled, and the user enables it on the
Extensions page
([Delivery](https://github.com/freelensapp/freelens/blob/v2.1.0/docs/extensions/api.md#delivery)).

## The first release of a package

npm sets up trusted publishing in the settings of a package, so the package
has to exist before it can be used:

1. The first version is published by the release workflow with an npm token,
   kept as a secret of its `publishing` environment.
2. Then trusted publishing is configured for the package, the repository and
   the release workflow, and the token is removed from the environment and
   revoked. While the secret is there, the workflow keeps using it.
3. A new configuration has to complete a successful publication within two
   days, or it expires and has to be created again. A prerelease validates it
   without inventing a release.
4. From then on every release goes through trusted publishing and carries its
   provenance. A version published with a token has none.

## Before a release

- Every spec of the release is Verified, and the roadmap says so
  ([Process](process.md)).
- The drift watches were run ([Maintenance](maintenance.md)).
- The extension was tried in the official Freelens package of the release it
  targets, installed the way a user installs it, on a cluster that runs the
  real project: every page, details panel, menu item and action.
- The README describes what is about to ship: requirements, supported APIs,
  permissions, limits. Its screenshots, and its video where there is one,
  show the release ([README](readme.md)).

## After a release

Check what was published, not what was meant to be:

- the version on npm is the new one, under the right tag. The registry can
  take a minute to show it: ask again before deciding that it failed;
- the tarball on npm is, byte for byte, the tarball of the GitHub release,
  and its checksum is the one in the `.sha256` beside it. A tarball built on
  another machine is not a reference;
- the version carries its provenance, when it went through trusted
  publishing;
- the extension installs by name in the official Freelens package, and works
  there.

Then close it:

- the roadmap and the specs say what shipped;
- the pull request with the next version, which the version workflow opens
  after a release, is merged;
- the notes of the GitHub release say what changed for the user;
- the release is announced where its users are: in the community of the
  project the extension is for and, for an extension of the Freelens
  organization, on the Freelens channels.

The Velero extension specified its first release as a spec of its own
([Examples](examples.md)).
