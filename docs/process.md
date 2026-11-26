# Process

An extension built with this kit is developed spec first: a feature is
written down and approved before it is coded, and it is done when its tests
run green on `main` and its documents say so. The process is binding for
every contributor, a person or a coding agent.

It covers an extension that is built feature by feature. Porting an extension
written for the v1 extension API is a different job, which the
`port-extension-to-v2` skill of
[freelensapp/freelens](https://github.com/freelensapp/freelens/tree/v2.1.0/plugins/freelens)
covers.

## Roles

- **The maintainer** answers for the extension: approves the specs, or
  delegates their approval for a milestone, holds the review at the end of
  each milestone and decides the releases. In a repository of the Freelens
  organization it is the lead maintainer of the extension. In a community
  repository it is the author; when the extension is
  [adopted](adoption.md), the review of the organization comes on top.
- **The contributor** writes specs, code and tests: a person, a coding agent,
  or the maintainer.
- **The reviewer of the domain** knows the project the extension is for: the
  maintainer, or people from the community of that project.

Approvals and reviews are recorded by role and date, never by personal name.
A decision that the contributor takes while implementing is recorded as
"decided while implementing", and is never attributed to the maintainer.

## Where the method lives in an extension

| Place                              | What it holds                                                                                                         | Created with                     |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| `AGENTS.md`                        | The guide of the template, with the [method sections](../templates/agents-method-sections.md) of the kit near its top | The repository                   |
| `docs/specs/`                      | One spec per feature ([Specs and roadmap](specs.md))                                                                  | SPEC-0001                        |
| `docs/development/ROADMAP.md`      | Scope and progress. The single source of truth for both                                                               | The approval of SPEC-0001        |
| `docs/development/ARCHITECTURE.md` | How the extension reaches the cluster, what runs in which process, and the decisions the specs share, as they are now | The approval of SPEC-0001        |
| `docs/development/TESTING.md`      | The layers, the commands and the fixtures of this extension, on top of [Testing](testing.md)                          | The spec of the test environment |
| `docs/development/DESIGN.md`       | The design decisions of this extension, on top of [Design](design.md)                                                 | The first spec of a view         |
| `docs/development/TRY-IT.md`       | The walkthrough of the views on the demo cluster, which is the path of the milestone review                           | The demo cluster                 |

A spec records a decision when it is taken. These documents say how things
are now: when a later spec changes a decision, its pull request updates the
document. None of them has a template, because each one is about its own
extension.

The process itself is not copied into the extension: its `AGENTS.md` points
here, at a pinned version of the kit. A copy drifts.

## The loop

1. **Spec before code.** Every feature starts as a spec in `docs/specs/`,
   named `SPEC-NNNN-short-slug.md` and written from a template of the kit;
   [Specs and roadmap](specs.md) says which one. No implementation pull
   request without an approved spec. The first spec of an extension is its
   [reconnaissance](reconnaissance.md).
2. **Approval.** The contributor opens the pull request that introduces the
   spec, and the maintainer approves the spec there, or the coding agent
   does under a [delegation](#delegation-for-a-milestone). The contributor
   then records the approval in the spec: role, date and scope, which is
   what the approval covers, the spec as drafted or with the changes it
   names. A draft, however complete, is not approval to implement.
3. **Implementation.** One pull request per feature slice, and the pull
   request links the spec. The implementation does not silently diverge from
   the spec: when reality forces a change, the spec is updated in the same
   pull request and the description calls the change out.
4. **Tests are part of the feature.** A feature without its non-regression
   tests is not done. See [Testing](testing.md).
5. **Documents in the same pull request.** The status in the roadmap, the
   status of the spec and, when the structure changed, the architecture
   document are updated with the code. A pull request that leaves them stale
   is incomplete.
6. **Verification.** After the merge, the spec becomes Verified only when its
   non-regression tests run green in CI on `main`, and after the manual check
   when the spec asks for one.
7. **Closure after the merge.** Merging is not the end of the loop. Whoever
   merges checks the CI runs on `main`, then lands a small follow-up that
   moves the rows of the roadmap from "In PR" to "Done" and the spec to
   Verified, and corrects any sentence of the documents that the merge made
   stale. A pull request can only say "In PR" about itself, so this step
   cannot be folded into it. It exists because it is the easiest one to
   forget.

## Delegation for a milestone

The maintainer may delegate the work inside a milestone to a coding agent,
so that the gate held by a person is the review at the end of the
milestone. The delegation is given in words, for one milestone or until it
is withdrawn, and the session notes keep those words. Under it the coding
agent:

- approves the specs of the milestone, and records in each one that it was
  approved under the maintainer's delegation for that milestone and is
  reviewed with the rest of it at its review;
- takes the decisions that the specs leave open, and lists them in the
  report of the milestone for the maintainer to confirm;
- pushes, opens its pull requests and merges them once CI is green, and
  does the closure after each merge;
- stops at the end of the milestone, and starts the next one only at the
  maintainer's word.

The delegation changes who approves, never what is checked: every step of
the loop, every test and every rule of [Safety](safety.md) still holds. The
reconnaissance and the roadmap stay with the maintainer, because they fix
the scope that the milestones follow. A spec that writes to a cluster is
covered too, unless the maintainer leaves it out.

It covers nothing that leaves the repository: no release, no package, no
announcement, no other repository, no issue or pull request of someone
else. A question that cannot be undone, that is about the domain or that
changes the scope still goes to the maintainer before the work goes on.
Scope is added to an approved roadmap as
[Specs and roadmap](specs.md#adding-to-the-scope) says: a proposal first,
then the decision of the maintainer, recorded in the roadmap.

## Rules on top of the loop

- One small, testable slice per pull request. The agreed scope is never
  reduced silently: what moves out of it is a decision recorded in the
  roadmap.
- Read-only features come first. The first spec that writes to the cluster
  sets the ground rules for every write of the extension
  ([Safety](safety.md)).
- Each spec records the release of the project it was written against, tag
  and commit. Behavior that exists only on the main branch of the project is
  design guidance, never something the extension relies on.
- A local run is evidence for a pull request, not a status. A CI result is
  never assumed.
- An exploratory check in the application does not replace a deterministic
  test.
- A blocker of scope, safety, compatibility or platform is escalated to the
  maintainer. It is never covered by a claim of completion that was not
  verified.

## The design question every spec answers

Freelens offers a standard vocabulary: list pages, details panels, menus. An
extension uses it wherever a Kubernetes resource is the subject, but it is
not the ceiling. For every task of the user, the Design section of the spec
says whether the view is standard, a list with its details, or ad hoc, such
as an overview, a topology, a timeline or a guided flow, and why that is the
best experience for the task. See [Design](design.md).

## Manual testing escalation

Some behavior cannot be verified automatically: the outcome of an operation
on a production-like cluster, a large payload over a slow link, a terminal on
every desktop platform. In that case:

1. The spec lists the manual steps and the expected outcome of each.
2. The contributor asks the maintainer to run them.
3. The result is recorded in the spec, with date, role and outcome, before
   the feature becomes Verified.

A manual test never sends the data of a real environment to an agent, to a
remote service or to hosted CI ([Safety](safety.md)).

## Milestone review

Automated tests prove behavior. They do not prove the experience. At the end
of every milestone, after the closure step, the maintainer reviews the
extension in a real Freelens before the next milestone starts:

1. The pre-review pass has run and its report is in the maintainer's hands
   ([Review](review.md)). Everything that can be automated is already
   verified, so the session covers judgment, the "for human judgment" list of
   the report and what cannot be automated.
2. The demo environment is up, with the walkthrough of `TRY-IT.md`.
3. Every view the milestone introduced is walked through, in a dark and in a
   light theme, asking of each one: is this the best possible view for the
   task?
4. What the views say about the project is checked by the reviewer of the
   domain.
5. Under a [delegation](#delegation-for-a-milestone), the maintainer
   confirms the specs approved under it and the decisions listed in the
   report, or reopens them.
6. The findings become issues, and the outcome of the session, with date,
   role and verdict, is recorded in the specs involved.
7. Blocking findings are fixed before the next milestone begins, through the
   normal loop.

The review is per milestone, not once at the end and not after every task:
the feedback on one milestone has to arrive before its patterns are repeated
in the next.

## Drift watches

An extension follows three things that move on their own schedule: the
project it is for, Freelens and the template. At the start of every milestone
and before every release of the extension, each one is checked against the
version the extension was written from, and so is the version of this kit.
[Maintenance](maintenance.md) has the procedure.

## Working agreements

- Branch names are short and in kebab case, such as `add-backup-views`.
- Commit messages are plain: no Conventional Commits prefixes, no emoji.
- Pull requests go against `main`, are squash merged and need CI green.
- A coding agent pushes, and opens pull requests, only when the maintainer
  has said that it may. It merges them only under a
  [delegation](#delegation-for-a-milestone).
- Packages are published only by the release workflow of the template, never
  from a workstation. Tags are created only by its tag workflow, and the
  version changes only through the pull request of its version workflow.
- External contributions follow the same loop. The maintainer helps a
  contributor write the spec when needed.
