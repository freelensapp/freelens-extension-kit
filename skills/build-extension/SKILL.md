---
name: build-extension
description: Build a new Freelens extension feature by feature with the method of the Freelens extension kit, from the brief to the release. Use when the user wants to plan, specify, implement, test, review or release a Freelens extension that is developed spec first, or asks how the work on one is organized. It starts from a repository created with the create-extension skill of freelensapp/freelens, which covers the technical setup. Not for porting an extension from the v1 extension API; port-extension-to-v2 of freelensapp/freelens covers that.
license: MIT
compatibility: Needs network access to github.com for the kit, the Freelens documents and the template, unless they are checked out side by side in the workspace.
---

# Build a Freelens extension with the kit

This skill is a pointer. The method is the
[Freelens extension kit](https://github.com/freelensapp/freelens-extension-kit),
and its `AGENTS.md` is the text to follow. Nothing of it is repeated here, so
that nothing drifts.

## What to do

1. Find the kit. When the `AGENTS.md` of the extension names a version of the
   kit, use that version. When a checkout of the kit is in the workspace, read
   it there. Otherwise read it from its repository, at its latest release.
2. Read `AGENTS.md` of the kit: "The path of an extension" and "Rules that
   hold at every step".
3. Find the step the work is at, as that `AGENTS.md` says: from the session
   notes of the workspace, the roadmap and the specs of the extension. Read
   the document of that step before acting.
4. For a repository that does not exist yet, the `create-extension` skill of
   [freelensapp/freelens](https://github.com/freelensapp/freelens/tree/v2.1.0/plugins/freelens)
   comes first, as step 3 of the path says. The kit begins where that skill
   ends.

## Explaining the kit

When the user asks what the kit is, how it works or how to use it, answer
from the `README.md` of the kit, "How it works" and "How to use it", and name
the step their work is at.

## When the kit does not answer

When the kit is wrong or silent, say so: "The version of the kit", in
`docs/maintenance.md` of the kit, says what happens next. Nothing is worked
around in the extension without a word. A gap in the
Freelens documents, in the SDK or in the skills is reported to
[freelensapp/freelens](https://github.com/freelensapp/freelens/issues), and
one in the template to
[freelensapp/freelens-example-extension](https://github.com/freelensapp/freelens-example-extension/issues).
