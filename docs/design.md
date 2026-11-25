# Design

These directives bind every contributor, like the [process](process.md). They
rest on three commitments:

1. **Native first.** An extension feels like a part of Freelens, not like a
   website embedded in it. Where the host has a component, custom code is not
   an alternative.
2. **Desktop grade.** Freelens is a desktop application that operators use
   every day. A view is built to be scanned: state visible at a glance,
   keyboard and mouse at ease, no wait that is not shown, correct in a dark
   and in a light theme, at any window size.
3. **The best possible view for the task.** A list with its details is the
   model for a Kubernetes resource, not the ceiling of an extension. Where a
   list cannot carry the task, the extension designs an ad hoc view, held to
   the same rules.

This document holds the rules that do not depend on the domain. How each one
is built, with which component of the host and which pattern, is in the
`AGENTS.md` of the template and in the extension documents of Freelens. What
an extension decides for its own domain, its status model, its navigation and
its ad hoc views, is in its own `docs/development/DESIGN.md`.

## Start from the tasks

Before the kinds are listed, the journeys of the operator are: what they have
to notice, to understand, to decide and to do, in the order they would do it.
The views follow the journeys. An extension that renders each kind as
`kubectl get` would is a resource browser, and the host already is one.

## Lists

- A list of resources is the list layout of the host,
  `Renderer.Component.KubeObjectListLayout`. A custom table in its place is
  forbidden.
- The columns follow one grammar, in this order: Name, Namespace, the columns
  of the domain, Condition, Status, Age. The columns of the domain carry what
  the operator looks at every day, the most important first.
- A cell is one line. The list is virtualized with rows of a fixed height, so
  a long value is truncated and its tooltip carries it whole.
- A missing value says so, with "N/A". No cell is empty.
- A click on a row opens the details. A link inside a row does not fight it.

## Status

- Each family of kinds has a classifier: a pure function, covered by unit
  tests, from the object to a small closed set of states, with no markup and
  no color in it. An unknown value maps to Unknown, never to a guess.
- A list shows state in two columns: a short word that can be scanned, and
  the phase or the message of the project as it is, truncated, with its
  tooltip.
- Lifecycle and health are not pressed into one mark. An operation in flight
  stays in flight even with errors. A partial failure is not a success.
  Missing progress is indeterminate, not zero and not complete. A failed read
  is not zero failures.
- An operation in flight never holds or replaces the health that the project
  reports. It may soften the tone of the mark, and only for a bounded time,
  counted from a time the project wrote. A health held without a bound hides
  a real problem for good.
- Only real timestamps are shown. A time the project did not write is not
  made up, and one that makes no sense is unavailable.
- Words and icons carry the meaning without the color.
- A boolean is phrased so that green means healthy.
- A form the project has deprecated is shown with a label that says so, and
  is never generated.

Colors are never authored by the extension. A state maps to a semantic token
of the theme:

| Meaning                          | Token               |
| -------------------------------- | ------------------- |
| Healthy, running, ready          | `--colorOk`         |
| Completed, succeeded             | `--colorSuccess`    |
| Pending, waiting, in progress    | `--colorWarning`    |
| Failed, error                    | `--colorError`      |
| Terminated, terminating, stopped | `--colorTerminated` |
| Informational, neutral           | `--colorInfo`       |
| Unknown                          | `--colorVague`      |

A scale the project has of its own, such as a severity, is mapped to these
tokens in the status model of the extension, which `SPEC-0001` proposes and
its approval settles.

## Details

- The details of a kind render content only: the host draws the title, the
  toolbar and the way to close them.
- What the host already renders is not rendered again. Look in a real
  Freelens at what the details of the kind show before the extension adds its
  part, and check that nothing shows twice.
- An optional row is hidden when it has no value. A value that has to show as
  absent says "N/A".
- A reference to another object is a link, when its target exists. Otherwise
  it is plain text. A link that fails is a defect.
- Dates go through the date components of the host, which follow the time
  zone the user chose. Ages update as time passes.
- A large blob, YAML or JSON, is in the read-only editor of the host, with a
  bounded height that does not trap the scrolling of the page.
- Repeated parts of an object are a nested table of the host, or sections
  that disappear when they have nothing to show.

## Navigation

- One root entry with an icon. Its children are text only.
- Past a handful of resources, the root holds a few groups of the domain and
  the resources hang under them.
- One entry for each resource, not for each API version. The version is
  chosen inside the page: the newest one the cluster serves.
- Titles are humanized, in Title Case. When one would collide with a title
  the host already uses in the same sidebar, such as Cluster or Service, it
  is qualified with the word of its domain.
- Icons are original, monochrome SVG with no fill of their own, so that the
  host colors them. They are never copied and never images.

## Theme

- No hardcoded color anywhere: styles, markup, inline styles, SVG, the series
  of a chart.
- A derived accent, such as a tinted background, is computed from a token
  with `color-mix`, never written as a hex value.
- A fallback, where one is needed, is neutral to the theme.
- Spacing and type come from the scale of the host.
- An extension styles its own subtree. It does not override the chrome of
  the host.
- An extension does not assume which themes exist, or how many. It reads the
  tokens, and where it has to tell dark from light it reads the `type` of the
  active theme, never its name.
- Every view is checked in a dark and in a light theme before its pull
  request is opened. Where the targeted Freelens lets its user add themes,
  as it does from 2.1.0 on
  ([Themes](https://github.com/freelensapp/freelens/blob/v2.1.0/docs/themes.md#extensions)),
  one that is not the default is checked too.

## States that are not the happy one

Every page handles them, and every card of an ad hoc view handles them on its
own. None of them is a blank area.

| State         | What the view does                                                                                               |
| ------------- | ---------------------------------------------------------------------------------------------------------------- |
| Loading       | Keeps a stable layout. Never a flash of empty content                                                            |
| Empty         | Says what was looked for and that nothing was found. A list uses the empty state of the host                     |
| Not installed | Says that the definitions of the project are not in the cluster. Still checking is not the same as not installed |
| Restricted    | Names what the user cannot read and the permission it takes. A refusal is never shown as an absence              |
| Failed        | Shows a readable error with its reason. A render error is caught by the error boundary of the template           |
| Partial       | Keeps the parts that work and says what is missing                                                               |
| Stale         | Keeps the last data it had, with their time and the failure of the refresh                                       |

A view decides which state it is in from the status of an answer, never from
the text of an error.

## Interaction and performance

- No work in the render path. A virtualized list stays virtualized.
- A tooltip carries the full value or the explanation. Nothing important
  lives only in a tooltip.
- Live data are polled at an interval the panel shows, with a manual refresh,
  and the polling stops when the panel is not visible.
- A rounded or humanized number has its exact value somewhere, and every
  figure has its unit.
- Controls are reachable and operable from the keyboard. Focus is visible and
  comes back after a dialog. The extension adds no global key binding that
  could shadow one of the host.
- A view holds at a small and at a large desktop window, and stays coherent
  when the user zooms.

## Ad hoc views

An overview, a topology, a timeline or a live panel is what makes an
extension more than a resource browser. It is held to the same discipline as
a list.

- **When.** A list cannot carry the task: the picture of a whole domain,
  relationships and topologies, sequences in time, live data that are in no
  resource, the way from a summary to the objects behind it.
- **Where.** A page of its own, or a section of the details. A list inside it
  is still the list of the host.
- **With what.** The components the host has: its charts and cards, badges,
  icons, tooltips and tables. Numbers follow the user's choice between charts
  and cards, as the overviews of the host do
  ([api.md](https://github.com/freelensapp/freelens/blob/v2.1.0/docs/extensions/api.md#the-overview-cards-follow-the-users-choice-of-cards-or-charts)).
  A custom component is written only for what the host has nothing for, with
  the tokens of the theme.
- **Every tile and every mark is a door.** A count opens the filtered list, a
  name opens its details, a point in time opens the object it stands for. A
  dashboard is a way in, not a dead end.
- **Desktop density.** More on a screen than a web page would dare, with
  text that stays readable, no scrolling inside a card, and a grid that
  takes fewer columns in a narrow window instead of overflowing.
- **Logic in pure functions.** Aggregations, classifiers and layouts are
  modules covered by unit tests. The component is a thin shell over them.
- **Declared in the spec.** The spec describes the parts, what each one
  shows, where its data come from and what each click leads to, and says why
  this view serves the task better than a list.

## Writes

[Safety](safety.md) has the rules. In the interface:

- the outcome of a write is always shown, as a notification of the host or
  in the view the user is in. An error the host already shows is not shown
  twice;
- its control is disabled while the operation is in flight;
- a creation form is its own confirmation, with the exact object it will
  send in view. What the project would refuse is refused in the form, before
  the submit. The recommended shape is the default.

## Forbidden

- A custom table where the list of the host fits, and a page of resources
  with no details.
- A hardcoded color, a fallback for one theme only, an image as an icon, a
  palette of the extension's own.
- The same inline style repeated from place to place, and a style that leaks
  onto the host.
- Reading an object as an untyped value where the kind can be typed.
- Names left from the template, and files nothing uses.
- Anything copied from another tool for the project.

## How it is enforced

- The Design section of every spec says whether each view is standard or ad
  hoc and why, describes its columns, its status mapping, its details and
  its states that are not the happy one, and declares every deviation from
  these directives. A deviation updates the `DESIGN.md` of the extension in
  the same pull request, or is dropped.
- A pull request that touches the interface says which themes and which
  states were checked, with screenshots from the check in the application.
- The [pre-review pass](review.md#the-pre-review-pass) asserts what a machine
  can assert.
- The [milestone review](process.md#milestone-review) asks of every view: is
  this the best possible view for the task?
