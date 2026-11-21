# Worked examples

The kit was not designed first and applied later. It is what four extensions
of the Freelens organization have in common, written down. Their
repositories are public: the specs, the tests and the history of pull
requests of each one show the method applied to a real domain, one slice at a
time.

They were built before the kit existed. Three of them follow one another,
each a little further than the one before: KubeSwift, CloudNativePG, Velero.
Kafka has forms of its own. So none of them has exactly the layout this kit
describes, and where an example and the kit differ, the kit is the current
form.

| Extension                       | Read it for                                                              |
| ------------------------------- | ------------------------------------------------------------------------ |
| [Kafka](#kafka)                 | An extension with a main process                                         |
| [KubeSwift](#kubeswift)         | Many kinds, read-only first, and the design directives                   |
| [CloudNativePG](#cloudnativepg) | The reconnaissance, live data without credentials, domain correctness    |
| [Velero](#velero)               | Protected writes, the two tiers of the test environment, a first release |

## Kafka

[freelens-kafka-extension](https://github.com/freelensapp/freelens-kafka-extension)
talks to a system that is not a Kubernetes API, so most of it runs in the main
process.

- [connectivity-engine.md](https://github.com/freelensapp/freelens-kafka-extension/blob/main/docs/connectivity-engine.md):
  how the main process reaches what it has to read.
- [TESTING-SAFETY.md](https://github.com/freelensapp/freelens-kafka-extension/blob/main/TESTING-SAFETY.md):
  the safety of tests and of browser automation.
- [009-write-operations.md](https://github.com/freelensapp/freelens-kafka-extension/blob/main/docs/specs/009-write-operations.md)
  and
  [write-mode.ts](https://github.com/freelensapp/freelens-kafka-extension/blob/main/src/main/write-mode.ts):
  writes that stay off until the user turns them on.

Its specs use an earlier form: numbers without the `SPEC` prefix, and
requirement IDs in every spec.

## KubeSwift

[freelens-kubeswift-extension](https://github.com/freelensapp/freelens-kubeswift-extension)
shows many kinds across several API groups, milestone after milestone.

- [DESIGN.md](https://github.com/freelensapp/freelens-kubeswift-extension/blob/main/docs/development/DESIGN.md):
  design directives in full, with their file references.
- [SPEC-0003](https://github.com/freelensapp/freelens-kubeswift-extension/blob/main/docs/specs/SPEC-0003-e2e-infrastructure.md),
  [SPEC-0005](https://github.com/freelensapp/freelens-kubeswift-extension/blob/main/docs/specs/SPEC-0005-local-demo-cluster.md)
  and
  [SPEC-0006](https://github.com/freelensapp/freelens-kubeswift-extension/blob/main/docs/specs/SPEC-0006-pre-review-agent-pass.md):
  the test environment, the demo cluster and the pre-review pass, each
  specified as a feature.
- [SPEC-0010](https://github.com/freelensapp/freelens-kubeswift-extension/blob/main/docs/specs/SPEC-0010-m6-guest-actions.md):
  write actions and their confirmations.
- [SPEC-0017](https://github.com/freelensapp/freelens-kubeswift-extension/blob/main/docs/specs/SPEC-0017-m7-console-and-exec.md)
  and
  [console-commands.ts](https://github.com/freelensapp/freelens-kubeswift-extension/blob/main/src/renderer/components/console-commands.ts):
  a command handed to a terminal, with its quoting.

## CloudNativePG

[freelens-cnpg-extension](https://github.com/freelensapp/freelens-cnpg-extension)
shows the state of databases, most of which is in no resource.

- [SPEC-0001](https://github.com/freelensapp/freelens-cnpg-extension/blob/main/docs/specs/SPEC-0001-recon-and-architecture.md):
  the reconnaissance as the first spec.
- [SPEC-0006](https://github.com/freelensapp/freelens-cnpg-extension/blob/main/docs/specs/SPEC-0006-m2-live-database-view.md):
  live data read through the API server, without credentials.
- [SPEC-0007](https://github.com/freelensapp/freelens-cnpg-extension/blob/main/docs/specs/SPEC-0007-m2-open-psql.md):
  a session opened in a terminal tab.
- [SPEC-0008](https://github.com/freelensapp/freelens-cnpg-extension/blob/main/docs/specs/SPEC-0008-m2-pre-review-pass-and-demo-cluster.md)
  and
  [TRY-IT.md](https://github.com/freelensapp/freelens-cnpg-extension/blob/main/docs/development/TRY-IT.md):
  the pre-review pass and the walkthrough of a review.
- [TESTING.md](https://github.com/freelensapp/freelens-cnpg-extension/blob/main/docs/development/TESTING.md):
  domain correctness checks and the non-regression policy.
- [SPEC-0020](https://github.com/freelensapp/freelens-cnpg-extension/blob/main/docs/specs/SPEC-0020-m6-write-actions-ground-rules-and-backup-now.md)
  and
  [SPEC-0025](https://github.com/freelensapp/freelens-cnpg-extension/blob/main/docs/specs/SPEC-0025-m7-creation-forms-ground-rules-and-create-cluster.md):
  the ground rules of write actions and of creation forms.

## Velero

[freelens-velero-extension](https://github.com/freelensapp/freelens-velero-extension)
is the most recent, and the one whose process the kit started from.

- [ROADMAP.md](https://github.com/freelensapp/freelens-velero-extension/blob/main/docs/development/ROADMAP.md):
  a roadmap as the single source of truth.
- [SPEC-0009](https://github.com/freelensapp/freelens-velero-extension/blob/main/docs/specs/SPEC-0009-write-gate.md)
  and
  [write-gate.ts](https://github.com/freelensapp/freelens-velero-extension/blob/main/src/main/write-gate.ts):
  writes off until they are turned on, enforced in the main process.
- [SPEC-0010](https://github.com/freelensapp/freelens-velero-extension/blob/main/docs/specs/SPEC-0010-diagnostic-request-and-transport.md):
  a request that creates an object is a write.
- [SPEC-0017](https://github.com/freelensapp/freelens-velero-extension/blob/main/docs/specs/SPEC-0017-write-actions.md):
  write actions with numbered requirements and their tests.
- [SPEC-0004](https://github.com/freelensapp/freelens-velero-extension/blob/main/docs/specs/SPEC-0004-test-environment-every-platform.md),
  [views-tests.yaml](https://github.com/freelensapp/freelens-velero-extension/blob/main/.github/workflows/views-tests.yaml)
  and
  [e2e-tests.yaml](https://github.com/freelensapp/freelens-velero-extension/blob/main/.github/workflows/e2e-tests.yaml):
  the two tiers of the test environment, and what runs when.
- [SPEC-0015](https://github.com/freelensapp/freelens-velero-extension/blob/main/docs/specs/SPEC-0015-freelens-v2-host.md):
  following a new major version of Freelens.
- [SPEC-0018](https://github.com/freelensapp/freelens-velero-extension/blob/main/docs/specs/SPEC-0018-release-readiness.md):
  a first release.

## Adopted extensions

Two extensions written in the community were
[adopted](adoption.md) in the form this kit describes:
[freelens-eso-extension](https://github.com/freelensapp/freelens-eso-extension)
and
[freelens-keda-extension](https://github.com/freelensapp/freelens-keda-extension).
The first pull requests of each are the import, which keeps the history of
its author, and the alignment with the template. Their READMEs have the
sections of the organization's extensions.
