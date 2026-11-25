# Testing

Every feature ships with its tests, at every layer that applies. A feature
without its non-regression tests is not done ([Process](process.md)).

The harness itself is upstream: the unit test setup and the integration tests
in Freelens are those of the template, described in its `AGENTS.md`. This
document says what an extension adds to them and how it uses them. The SDK,
here and elsewhere, is `@freelensapp/extensions`, the package an extension
takes the API of Freelens from.

## Layers

| Layer                   | Runs on                                                                        | Proves                                                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| Unit                    | Vitest, with the stub of the SDK the template provides                         | Models built from realistic objects, status and health as pure functions, parsers, composed commands, components with logic       |
| Integration in Freelens | The harness of the template: Freelens, the extension installed, a kind cluster | That the extension installs and activates with no error in either process, and every view against the objects of the test cluster |
| With the real project   | A kind cluster that runs the project at the reviewed release                   | What only a controller can answer: that what the extension writes is accepted and acted on, and what real objects look like       |
| Pre-review pass         | The same machinery on the demo cluster, before a milestone review              | Every view in a dark and in a light theme against the rules a machine can check, with a report ([Review](review.md))              |
| Manual                  | The maintainer, in a real Freelens                                             | What cannot be automated, and judgment ([Process](process.md#manual-testing-escalation))                                          |

## The test environment has two tiers

**Definitions only.** A kind cluster with the definitions of the project at
the reviewed release and nothing that reconciles them. Each session places
objects of its own, with the status written by hand, which no controller
reads. The integration tests and the suites of the views run here, except the
few that need what only the real project produces. They test the views, not
the project, so they cannot depend on what a controller would do, and a run
waits for none.

**The real project.** A kind cluster with the project installed at the
reviewed release, from its official artifacts at pinned versions. It serves
what needs a controller to answer, the demo cluster of a review, and the few
jobs of CI that need it.

The first tier makes the many tests of the views fast and deterministic, and
it can show any state, also the failures the project does not produce on
demand. The second keeps them honest. Three rules tie them together:

- A static object carries only what the controller would write in that state
  ([Reconnaissance](reconnaissance.md)), and each one is there to cover a
  state its views tell apart.
- A write is tested on the first tier by reading back from the cluster the
  request the extension sent. What the controller then does with it is
  proven on the second.
- A schema is never weakened to let a synthetic case pass. Values the schema
  rejects, such as an unknown phase or an impossible time, are tested at the
  unit layer.

The objects of the first tier are best captured from the second: the real
project brings its clusters into each state, and a script reads the objects
back and writes them as files. Two things make a capture worth trusting:

- **It waits until the state has settled.** A state is captured when every
  controller that reports on it has reported, a health check that counts the
  new machines included, and not when the main conditions first turn.
- **It cleans what the capture machine leaves.** Besides what the API server
  adds, a controller can copy facts of the machine it runs on into a status,
  such as the capacity of the host. The cleaning replaces them with fixed
  values, and a test scans every captured set for them.

## What runs when

| Suite                               | On a pull request                                                                                                       | On `main` | Every night |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | --------- | ----------- |
| Type check, lint, unit tests        | Always                                                                                                                  | Always    |             |
| Integration tests: the installation | Always                                                                                                                  | Always    |             |
| Views                               | The suites that the changed files reach                                                                                 | All       | All         |
| With the real project               | Only when it changes what they run: the scripts of the environment, the main process, the shared modules, the toolchain | All       | All         |

The pre-review pass is run in full, with its report and its screenshots,
before the review of a milestone. In CI it is one more suite of the views,
taken by the same rule.

## Commands

The harness of the template has `pnpm test:unit` and `pnpm test:integration`.
An extension adds the environment, under the same names in every extension:

| Command                           | What it does                                                                          |
| --------------------------------- | ------------------------------------------------------------------------------------- |
| `pnpm e2e:cluster:up`             | Creates the test cluster with the real project and verifies it. Run again, it resumes |
| `pnpm e2e:cluster:up:definitions` | Creates the test cluster with the definitions alone                                   |
| `pnpm e2e:cluster:down`           | Deletes the cluster the scripts created, and nothing else                             |
| `pnpm demo:up`, `pnpm demo:down`  | The environment with its objects left in place, to look at in Freelens                |
| `pnpm pre-review`                 | The pass before the review of a milestone                                             |

The versions of the project, of kind and of Kubernetes are pinned in one
file of the scripts of the environment, and Renovate follows the pins. The
spec of the test environment chooses them. The scripts own what they create
and touch nothing else: the rules are in [Safety](safety.md).

## Checks worth trusting

- **A check must be seen failing.** A new test, guard or script is run once
  against the broken case before it is trusted, and the line that was broken
  on purpose is printed: a mutation that did not apply proves nothing.
- **A fixture that injects the hypothesis proves nothing about the cause.**
  Reproduce a defect from what really produces it.
- **An action is verified on the cluster.** Read the cluster before and after
  it. An interface that shows no error proves nothing.
- **The interface follows the cluster with a delay.** Wait for the expected
  content, not for a fixed time, before deciding that a view is empty or
  wrong.
- **The same pattern lives in sibling paths.** When a defect is fixed, search
  the code for the same pattern before closing the fix.
- **What was tested is what is in the commit.** Check the commit, not the
  working tree.
- **A test that was not run is unverified, not passed.** A fallback is partial
  evidence. A working tier is not discarded because another prerequisite
  failed, and it is never replaced by a write to a real cluster.
- **An expected error is left out narrowly.** A session that has to accept
  an error it cannot avoid, such as one the host logs for a view of its own,
  leaves out that one message, decided when it arrives from the frame and
  the page that logged it, and never a pattern for the whole session.

## Domain correctness

The users of an extension know the project well. So the suite compares what
the extension shows with what the project's own tool reports on the same
cluster: the same state, the same numbers, the same units. These comparisons
are test cases, not manual steps.

## Non-regression policy

- Each spec lists its regression tests by name: the file and the case.
- A red layer blocks the merge.
- When a defect is found, by CI, by a manual test or by a user, the fix adds
  a test that fails without it. No silent fixes.
- A test weakened to tolerate a difference nobody explained, of a platform, a
  timing or a runner, keeps that tolerance only until the difference is
  explained. Then the tolerance goes, or the weakened assert silently becomes
  the contract.
- Nothing is verified only once. Every check that can be codified, from the
  pre-review pass or from an exploratory session, graduates into the suite.
