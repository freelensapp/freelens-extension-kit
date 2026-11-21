# Review outcome

The issue that carries the outcome of a review to the author of a community
extension: step 2 of [Adopting a community extension](../docs/adoption.md). It
is opened on the author's repository. Anywhere else, such as a discussion
where the extension was proposed, two lines with a link to the issue are
enough.

## Rules

- Every line was seen in the application or read in the code. Nothing is
  deduced from a label, a name or a message.
- "What is left before the move" holds only what truly blocks the move. With
  nothing in it, say so and remove the list.
- Each blocking point comes with a way that was tried and works, and with the
  commands that verify it, so that one round is enough. Advice uses only
  documented APIs.
- Whatever does not block goes under "The rest", for the author or for the
  alignment pull request, whichever comes first.
- No other software that does the same job is named.
- A point that an earlier review got wrong is corrected in one sentence, in
  the same place.
- The body keeps one paragraph per line: GitHub turns every newline of an
  issue body into a line break.

## Title

```text
Review of <version of the extension> in Freelens <version of Freelens>
```

## Body

Replace what is in angle brackets and remove the sections that stay empty.

```markdown
Thank you for <what the author did>.

I tried <version of the extension> in Freelens <version of Freelens>, installed <by name, or from the release tarball>, on a kind cluster with <project and version>, as an administrator and as a read-only user, and I checked every action against the cluster.

### What is left before the move

- [ ] **<What does not work, in one sentence.>** <What was observed and where it stops.>

<Why it happens, and the way that was tried and works, with its code in a fenced block.>

This is how I check it, so that you can do the same before a release:

- <Action>: `<command>` shows <the expected result>.

When this works I'll check it again. Then, if you'd like, we can move the extension to the organization as `@freelensapp/<name>-extension`, with you as its creator and maintainer. The points below need no other round: fix the ones you like, and the rest goes into the alignment pull request after the move.

### The rest, for you or for the alignment pull request

- [ ] **<Finding, in one sentence.>** <What was observed and, when known, its cause and a way out.>

### What works

- <What was tried and behaves as it should.>

### A correction on my side

<What an earlier review got wrong, in one sentence.>
```
