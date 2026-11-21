# Coding agents

The kit is plain Markdown that any coding agent can follow, and `AGENTS.md` is
its one instruction file. This document says how each agent finds that file,
what else it needs, how the model for a task is chosen, and how the checks of
the method are run with a tool that is not the one they were first run with.

Two words are used strictly:

- **Documented**: what the documentation or the source of the tool says, read
  at the versions listed under [Sources](#sources).
- **Proven**: an extension was built with the tool, following this method.

What is said below about a tool is documented. Only Claude Code is proven.

## Instruction files

| Agent          | What it reads in a repository                                                            | How it gets `AGENTS.md`                                                      |
| -------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Claude Code    | `CLAUDE.md`, in the working directory and above it                                       | Through a `CLAUDE.md` that imports it with `@AGENTS.md`                      |
| GitHub Copilot | `.github/copilot-instructions.md`, `.github/instructions/*.instructions.md`, `AGENTS.md` | Directly: its cloud agent, Copilot CLI and Copilot Chat in VS Code           |
| Codex          | `AGENTS.md`, from the root of the project down to the working directory                  | Directly, within a size budget                                               |
| Cursor         | `.cursor/rules`, and `AGENTS.md` in the root and in subdirectories                       | Directly                                                                     |
| Gemini CLI     | `GEMINI.md`                                                                              | Through a `GEMINI.md` that imports it with `@./AGENTS.md`, or with a setting |
| OpenCode       | `AGENTS.md`, from the workspace directory upward                                         | Directly                                                                     |

So one instruction file and two pointers reach all six: `AGENTS.md`,
`CLAUDE.md` and `GEMINI.md`. This repository has the three of them, and the
template has the first two.

Notes:

- Without any `CLAUDE.md`, recent versions of Claude Code read `AGENTS.md` on
  their own. The pointer works with every version.
- Copilot CLI also reads `CLAUDE.md` and `GEMINI.md`, and follows the import
  of a `CLAUDE.md`. Which other surfaces of Copilot read agent instructions is
  in its
  [reference](https://docs.github.com/en/copilot/reference/custom-instructions-support).
- Gemini CLI can read `AGENTS.md` without a pointer when `context.fileName`
  in its settings names it.

## The size of AGENTS.md

Codex reads the instructions of a project within a budget,
`project_doc_max_bytes`, of 32768 bytes by default, and truncates what goes
beyond it. The `AGENTS.md` of the template is larger than that. Two things
follow:

- the [method sections](../templates/agents-method-sections.md) of an
  extension go right after "Project Overview", inside the budget;
- who works with Codex raises `project_doc_max_bytes` in its configuration,
  to read the whole file.

## Skills

A skill in the [Agent Skills](https://agentskills.io/specification) format is
read by all six agents, but not from the same folder:

| Agent          | Project folders                                        |
| -------------- | ------------------------------------------------------ |
| Claude Code    | `.claude/skills`                                       |
| GitHub Copilot | `.github/skills`, `.claude/skills`, `.agents/skills`   |
| Codex          | `.agents/skills`                                       |
| Cursor         | `.agents/skills`, `.cursor/skills`, `.claude/skills`   |
| Gemini CLI     | `.gemini/skills`, `.agents/skills`                     |
| OpenCode       | `.opencode/skills`, `.claude/skills`, `.agents/skills` |

No folder is read by all of them. That is why every procedure of the kit is a
document that can be followed without a skill, and why its one skill,
[build-extension](../skills/build-extension/SKILL.md), is a thin wrapper
around `AGENTS.md`. To use it, copy or link its folder into a folder the
agent reads.

The same holds for the skills of freelensapp/freelens. An agent that does not
load them reads their `SKILL.md` as a document, in the checkout of
Freelens, and follows it.

## Where an agent starts

An agent loads the instruction file of the folder it is started in. Started
in the folder of the extension, it reads the `AGENTS.md` of the extension,
whose method sections point to this kit. Started one level above, in the
workspace, it loads none at the start, and the request has to name the file
([Workspace](workspace.md#where-a-coding-agent-starts)).

## Choosing a model

The method does not depend on a model. The kit names none, and neither do
the sections it adds to an extension. Whoever starts a session chooses the
model for the task, and chooses again for the next one:

- the most capable model at hand for what needs judgement: a spec and the
  reconnaissance behind it, a diagnosis, a conflict, the
  [independent review](review.md#the-independent-reviewer);
- a lighter one for a [delegated task](review.md#delegated-tasks) that its
  brief closes: a lookup, a broad search, a check that repeats.

When a model does not get a task done, the task is repeated with a more
capable one, and the report says so. No check is loosened to fit a model:
the approved spec, the tests, the verification in the application and the
review hold whatever wrote the change.

With more than one machine, coding agent or model at hand,
[Dividing the work](dividing-the-work.md) says what goes where.

## Running the checks with any agent

- **The independent reviewer.** A new session, not a continuation of the
  author's one, started with a [task brief](../templates/task-brief.md) that
  says no file changes. Afterwards, check that none did. A tool that can
  start a session from inside another one can run the reviewer that way: its
  report is read when it has ended ([Review](review.md)).
- **The checks in the application.** They are scripts: the integration tests
  of the template and the pre-review pass. Any agent that runs a command runs
  them. A tool with browser automation can also drive Freelens directly, under
  the rules of [Safety](safety.md#browser-automation).
- **Continuity between sessions.** The session notes of the
  [workspace](workspace.md#session-notes) serve every tool, with or without a
  memory of its own.
- **Secret files.** The template denies Claude Code the reading of secret
  files with a settings file of that tool, which applies when the agent is
  started in the folder of the extension. For every other agent, only the
  written rule in `AGENTS.md` holds.

## Sources

| Agent          | Read in                                                                                                                                                                                 |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Claude Code    | [Memory](https://code.claude.com/docs/en/memory) and [Skills](https://code.claude.com/docs/en/skills) of its documentation                                                              |
| GitHub Copilot | [github/docs](https://github.com/github/docs) at `63b6c72cd`: custom instructions, their support by surface, agent skills, custom instructions of Copilot CLI                           |
| Codex          | [openai/codex](https://github.com/openai/codex) at `e20ccdfa8`: `codex-rs/config/defaults.toml`, `codex-rs/core/src/agents_md.rs`; [Skills](https://developers.openai.com/codex/skills) |
| Cursor         | [Rules](https://cursor.com/docs/context/rules) and [Skills](https://cursor.com/docs/context/skills) of its documentation                                                                |
| Gemini CLI     | [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) at `4fa64e71b`: `docs/cli/gemini-md.md`, `docs/reference/memport.md`, `docs/cli/skills.md`                      |
| OpenCode       | [anomalyco/opencode](https://github.com/anomalyco/opencode) at `887f6cd44`: `instructions.mdx` and `skills.mdx` of its documentation                                                    |
