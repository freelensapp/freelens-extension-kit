# Dividing the work

The method needs one machine and one coding agent. Many people have more: a
second machine, a subscription to more than one coding agent, a model that
runs on a machine of their own. This document says how to use them: what goes
where, and the rules that keep the work verifiable when it is divided.

It is optional, and nothing else in the kit depends on it.

## Taking stock

At the start, the coding agent asks the maintainer what the work may use, and
writes the answer in the [session notes](../templates/session-notes.md). It
does not look for machines or accounts on its own.

- **Machines.** For each one: the operating system, how it is reached, when
  it is on, and what it is good at: cores, memory, a GPU.
- **Coding agents.** Which ones, on which machine, and the limits of each
  plan: requests, hours, a monthly amount.
- **Models.** Which models each agent can use, and whether a model runs on a
  machine of the maintainer.
- **Limits.** What may leave the main machine, what each agent may do without
  asking, and how much may be spent.

The maintainer decides. The agent proposes a division, and waits for the
answer when the division costs money or starts something on another machine.

## What goes where

| Work                                                                        | Where                                                                              |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Decisions, specs, the review of what comes back, commits, pushes            | One place: the main session, on the machine the maintainer works at                |
| Builds, type checks, unit and integration tests, the test and demo clusters | The fastest machine. A long suite runs there while the main session goes on        |
| The trial on another operating system                                       | A machine that has it, with the official Freelens package                          |
| A closed task with its checks ([Review](review.md#delegated-tasks))         | A second session, a second coding agent, or a lighter model                        |
| A search over many files, an extraction from a log, a check that repeats    | A model on a machine of one's own, where there is one: nothing leaves that machine |
| What needs judgement: the reconnaissance, a spec, a diagnosis, a review     | The most capable model at hand ([Tools](tools.md#choosing-a-model))                |

What does not depend on anything else can go on at the same time: a suite on
one machine, a closed task on another, the reading for the next spec in the
main session. The work with the maintainer stays one thing at a time.

## Rules

- **One writer for each checkout.** Every machine and every agent works in a
  clone or a worktree of its own, on a branch of its own. What it did comes
  back as a branch, never as files copied over.
- **The same tools everywhere.** A second machine is set up like the first
  ([Workspace](workspace.md#what-the-machine-needs)), with the same pinned
  versions. A result from other versions is not a result.
- **Everything that comes back is verified** in the main session, like any
  other work: its tests, its checks, its final report
  ([Review](review.md#delegated-tasks)).
- **One place publishes.** Pushes, pull requests and releases leave from the
  main session, when the maintainer has said that they may.
- **What is not public stays where it is.** A delegated agent gets public
  material and synthetic data. Data of a real environment, secrets and
  unpublished texts never go to a machine, an agent or a service the
  maintainer has not named for them
  ([Safety](safety.md#data-of-real-environments)).
- **Spending has a ceiling.** For an agent paid by use: a ceiling, a log of
  what each task cost, a word to the maintainer at half of it, and a stop
  before it.
- **Nothing is left running.** Clusters and containers are removed at the
  end, on every machine.
- **Say what did what.** A job ends with two or three lines on what each
  machine, agent and model was used for. What was learned about dividing the
  work goes in the session notes.

## What a small local model is for

A model small enough for a consumer GPU did well where a machine could check
the answer: finding the failing test in a long log, extracting fields as
data, small tasks with an automatic check. It misread a change of code. So it
is not used to understand code, to review, or to write a text someone will
read.

## Used, tried and not proven

Used on the extensions built so far: a second machine for builds and tests, a
second coding agent for closed tasks, several sessions of one agent at the
same time.

Tried, on tasks of the kinds named above: a small model on a machine of one's
own.

Not proven: one extension divided among the subscriptions of several vendors
at the same time. The rules above are where to start, and what such a
division teaches goes back into this document.
