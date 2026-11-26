# Safety

An extension runs inside a desktop application that is connected to real
clusters, and any of them may be production. Safety has two sides: what the
extension does to a cluster, and what development and tests do while it is
being built. The rules below bind both.

## Reading

- **Through the host.** An extension reaches a cluster through the connection
  Freelens already has, never with a client and credentials of its own. The
  [extension documents](https://github.com/freelensapp/freelens/tree/v2.1.0/docs/extensions)
  of Freelens say how, in the contracts C12 and C15 of `api.md`.
- **Missing data is unknown, not healthy.** A status the extension cannot
  read, or does not recognize, is shown as unknown. Nothing turns green by
  default.
- **No credentials.** An extension does not store, log or forward
  credentials. When the data can be reached without them, that is the way to
  take. When a spec decides that a service outside the cluster needs one,
  the host keeps it encrypted
  ([Credentials](https://github.com/freelensapp/freelens/blob/v2.1.0/docs/extensions/api.md#credentials-keeps-an-extensions-values-encrypted-at-rest)),
  never a file, a store of the extension or a log.

## Writing

Read-only comes first. Every feature that writes gets its own approved spec,
from the [write template](../templates/spec-write-action.md), and the first
of them sets the ground rules for every write of the extension.

**What a write is.** Whatever creates, patches or deletes an object. A request
that creates an object is a write, even when the user only asked to look at
something, such as a log that the project serves through a request object. So
is a removal that the host offers on a page of the extension. A page hands the
list layout of the host a store that selects and removes nothing: the layout
offers to remove what its store has selected, even on a page that shows no
checkbox, and a store of the host keeps what was selected in the host's own
list of the kind.

**Confirmation.** Whatever changes the desired state of a resource, interrupts
a workload or deletes something first asks for an explicit confirmation. The
confirmation names the target, the cluster and the namespace or the object,
and lists the writes it will perform, in their order. The most destructive
actions ask for more, such as typing the name of the object.

**The one exception.** An action that only asks the controller to reconcile
again may run without a confirmation, when the README declares it and the
interface shows its outcome.

**After the write.** The interface is not optimistic: it shows what the
cluster says. A failure is reported with its reason, never swallowed. A
control that cannot work is disabled and says why. Every write has a test
that reads the result back from the cluster.

**Declared.** The "Permissions" section of the README lists everything the
extension writes, with the permission each write needs.

**Write mode, recommended.** An extension that writes can keep writes off
until the user turns them on, for one cluster, with the switch enforced in
the main process. The confirmation is still asked. The Kafka and Velero
extensions work this way ([Examples](examples.md)).

## Commands handed to a terminal

An extension can compose a command line and hand it to a terminal tab of
Freelens, where it runs under the user's own credentials. The command is then
text typed into a shell, so:

- it is composed by pure functions, covered by unit tests;
- every interpolated value is single-quoted;
- a value that comes from the cluster, such as a name or an annotation,
  passes a strict allowlist of characters before it is used at all;
- when the command has consequences the user may not expect, such as the
  identity it connects with, the interface and the README say so.

What the extension executes on its own is a fixed string, never text the user
typed.

## The main process

- A signed URL, or any value that grants access, stays in the main process.
  It is used promptly and never logged, stored, cached or shown.
- Every operation has a timeout, and what comes back is bounded in size and
  in time.
- TLS is verified. Skipping the verification is explicit, for one cluster,
  visibly unsafe, and never a fallback tried on its own after a failure.

## Development and tests

- **A disposable cluster.** Every write of development and tests goes to a
  kind cluster that the scripts of the repository created, on a developer
  machine or on a CI runner. Never to a shared, remote or real cluster.
- **Never the first cluster, never the current context.** The scripts work
  with a kubeconfig of their own that holds one target, check the identity of
  that target before they read or write, and refuse an API server that is not
  local. They never write the developer's kubeconfig or change its current
  context.
- **Down deletes what up created.** Nothing else, on that cluster or on any
  other. A cleanup that failed is reported, not passed over.
- **A real cluster is read, at most.** Only when the user named it and
  authorized the read. Being able to connect, or an entry in a kubeconfig, is
  not permission. Any cluster may be production: when unsure, it is. If a
  check would write to a real cluster, stop and ask.
- **Cloud accounts need their own authorization**, which names the target and
  the operation, also for a read. Credentials that happen to be on the
  machine authorize nothing.
- **Official artifacts, pinned.** The project is installed from its official
  releases at pinned versions. It is never patched or rebuilt to make a test
  pass.

## Data of real environments

- They stay on the machine that read them, in a private directory outside
  every repository. Ignoring a file in Git is not enough.
- They never go into source, fixtures, specs, documents, logs, screenshots,
  videos, test reports, packages or Git history. That includes names,
  endpoints, manifests, kubeconfigs and the error messages that carry them.
- They are never sent to a chat, to an agent, to tool output a model reads,
  to a remote service or to hosted CI. A local check on a real environment
  may report only a verdict with no data in it.
- Fixtures are synthetic, created on their own. A real dataset with its
  identifiers renamed is still a real dataset.
- The private state of the test environment, such as its kubeconfig and its
  generated credentials, is never uploaded as a CI artifact.

## Browser automation

A tool that drives Freelens, a script or an automation server, is not a
security boundary: it controls every page of the application it is attached
to, and so every cluster that application can reach.

- Give that Freelens a kubeconfig with the test cluster alone, in a profile of
  its own.
- Select a cluster by its exact name. Never click the first row.
- Do not export storage state, Secret values or credentials into the output
  of the tool.
- The console of the application can carry the shell prompt, account names
  and paths of the user. Keep only warnings, errors and the lines of the
  extension, and never paste a full console into a pull request, an issue or
  a report.
- A real cluster is never shown to a tool that sends screenshots or page
  content to an agent.
- What such a session finds does not replace a deterministic test.
