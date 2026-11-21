# Review

Three different things are called review in this method, and each has its
moment:

| Review               | Who does it                                     | When                                                                   |
| -------------------- | ----------------------------------------------- | ---------------------------------------------------------------------- |
| Pre-review pass      | A script, in a real Freelens                    | Before every milestone review                                          |
| Independent reviewer | A new session with none of the author's context | On the drafts of the specs, and on a diff before its pull request      |
| Milestone review     | The maintainer, in a real Freelens              | At the end of every milestone ([Process](process.md#milestone-review)) |

The first two exist so that the third is spent on judgment.

## The pre-review pass

Before the maintainer sits down, a script has already walked the extension in
a real Freelens and checked everything a machine can check. It runs with
`pnpm pre-review`, on the demo cluster of `pnpm demo:up`
([Testing](testing.md#commands)).

In a dark theme and then in a light one, it:

1. opens every page, and the details of every object of the demo cluster, and
   takes a screenshot of each;
2. asserts on the page the rules of [Design](design.md) that can be checked
   there;
3. opens every write dialog and closes it without confirming;
4. compares what the views say with what the cluster says
   ([domain correctness](testing.md#domain-correctness)).

The pass takes the list of the views from the registrations of the extension,
not from a list of its own, so that a new view is covered without anyone
remembering to add it.

Rules it has checked on the extensions built so far:

- an object reference is a link, or plain text when its target does not
  exist, and never a link that fails;
- every link navigates without a load error, and no link is nested in a link;
- no cell of a list is empty: a missing value says so;
- quantities are humanized, never raw runs of digits;
- the columns of a list can be resized;
- a filter that matches nothing shows the empty state of the host, not a
  blank area;
- no color is authored by the extension: the colors come from the theme.

It ends with a report, in the form of the
[report template](../templates/pre-review-report.md): what passed, what
failed, the screenshots, and a list of what is left to human judgment. The
report is in the maintainer's hands before the milestone review.

In CI the pass is one more suite of the views, taken by the same rule
([Testing](testing.md#what-runs-when)). What it proves for good graduates
into the other suites as a permanent test, in the pull request that
stabilizes it.

## The demo cluster and its walkthrough

`pnpm demo:up` creates a cluster of its own, with the real project and the
objects of the test environment, in states worth looking at. It is what the
pass runs on and what the maintainer looks at.

`docs/development/TRY-IT.md` of the extension is the walkthrough, and the
path of the milestone review:

1. what the machine needs;
2. how to bring the demo cluster up;
3. how to install the extension in Freelens;
4. the walk through the views, with what to look at in each;
5. the pass that precedes a review;
6. how to tear everything down.

## The independent reviewer

Whoever wrote a spec or a change cannot see what they took for granted. So a
second session reviews it: a new session of a coding agent, or a person, that
has none of the author's context.

- **It is read only.** It changes nothing.
- **It gets the text and the sources.** The drafts of the specs, or the diff,
  and the folders it may read: the project at the reviewed release, Freelens,
  the template.
- **It checks every claim against the sources**, and cites file and line for
  each finding.
- **It lists separately what it could not verify.** The author then verifies
  those points.

It runs on the drafts of the specs before they are approved, where a wrong
fact about the project costs the most, and on the diff of a slice before its
pull request. Any coding agent can do it, as a new session started with a
task brief ([Tools](tools.md#running-the-checks-with-any-agent)).

Two checks follow every piece of work that was not done by the author's own
hands:

- **Read the final report**, when the work has ended, and not a draft it left
  on disk along the way.
- **Check the attributions.** Search the text and the commit messages for the
  role of the maintainer: every decision attributed to the maintainer has to
  be one the maintainer took. The rest is "decided while implementing".

## Delegated tasks

A task given to another session, of the same agent or of another one, is a
closed brief, written from the [task template](../templates/task-brief.md):
where the session is, the context, the task in points, the rules, the limits,
the checks to run at the end and what to report.

- One outcome for each task, small enough to verify.
- The brief says where every fact is read from. A delegated session does not
  search outside the folders it is given.
- The limits are explicit: which files may change, no commit, no push.
- What comes back is verified like any other work: its tests, its checks and
  the two checks above.
