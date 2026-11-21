# The README and its media

The README is what a user reads before installing an extension, and for many
the only document they read. This document says which sections it has, in
which order, and how its screenshots and its video are made.

It is optional. An extension that keeps the README of the template, with the
names changed, follows the kit just the same. An extension that asks for
[adoption](adoption.md) needs the sections below.

## Sections

The README starts as the one of the template, which the `create-extension`
skill adapts: "Install" and "Build from the source" carry over with the names
replaced. The rest is written for the extension, in this order:

| Section               | Holds                                                                                                   |
| --------------------- | ------------------------------------------------------------------------------------------------------- |
| Title and badges      | The name of the package, then the badges of the template                                                |
| Overview              | What the extension is for, where it lives in Freelens and what each view shows. Then the media          |
| Authors               | Who created the extension, when it is not who maintains it                                              |
| Requirements          | The releases of Freelens and of the project it was tested with                                          |
| Supported APIs        | The API groups and versions, with the kinds of each                                                     |
| Permissions           | What a user needs to read the views, and every write with the permission it needs ([Safety](safety.md)) |
| Install               | From the registry, from a release tarball, from a directory, as in the template                         |
| Getting started       | The first minutes: where to click and what to expect                                                    |
| Features              | One subsection for each group of views, the write actions last                                          |
| Limits                | What the extension does not do, and where the user does that instead                                    |
| Development           | Optional, for contributors: the checks before a pull request and the test environment                   |
| Build from the source | As in the template                                                                                      |
| License               | The license and the copyright notice                                                                    |

## Rules

- It says what the extension does, factually. No claim of priority or
  superiority, no individuals apart from the authors, and no other software
  that does the same job by name, unless the maintainer has said otherwise.
- It is true for the release it describes. A change of behavior changes the
  README in the same pull request ([Process](process.md)).
- What it promises was seen in the application, on the release it names.

## Screenshots

- They are taken on the
  [demo cluster](review.md#the-demo-cluster-and-its-walkthrough), whose
  objects are synthetic and have realistic names. A real environment is
  never photographed ([Safety](safety.md#data-of-real-environments)).
- They show the application users run: the official Freelens package of the
  targeted release, with the extension installed the way a user installs it.
- One theme for all of them, the default dark one, and one window size. The
  picture is the window, with nothing of the desktop around it.
- They are PNG files in `docs/screenshots/`, named after the view.
- Two to four go in the Overview: the views that say most about the
  extension. More go under "Features", where a picture explains something.
- The alternative text says what the picture shows, and the theme.
- A view that changes gets its screenshot again in the same pull request. The
  [pre-review pass](review.md#the-pre-review-pass) already takes one for each
  view, so they come from a script.

## Video

A short video in the Overview shows the extension at work.

- Under a minute.
- Scripted, so that it can be taken again after a change: a script drives the
  application, as the integration tests do, and records its window.
- A title card, then six to eight scenes of a few seconds, each with one idea
  and a short caption, then an end card with the name of the package and the
  address of the repository.
- The setup is not recorded. The extension is installed, the cluster is
  connected and the namespace is chosen before the recording starts.
- The data are those of the demo cluster. No name in the picture says "test".
- The application runs with a fresh profile of its own, as the integration
  sessions of the template do, so that the Freelens of whoever records is not
  touched.
- The demo namespace is reset between takes, so that every take starts from
  the same state.
- The file is an MP4, H.264, at 30 frames a second.
- It is attached through the web interface of GitHub, which gives it an
  address that plays in the page. A file among the assets of a release does
  not play there. The link goes in the Overview, right above the
  screenshots, with the text "Video Demo".

The READMEs of the extensions in [Examples](examples.md) were written this
way.
