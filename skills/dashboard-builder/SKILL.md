---
name: dashboard-builder
description: Builds and improves web dashboards with guided onboarding, project setup, defined metrics, working filters, and verification. Use for a new dashboard, dashboard onboarding/setup, or a feature in an existing dashboard project.
license: MIT; see LICENSE.txt and SOURCE.md
---

# Dashboard Builder

Turn a dashboard request into a runnable, data-grounded application. Start with
the decision the dashboard helps someone make, then connect its data, metrics,
controls, and views. Adapt the engineering methods described in [SOURCE.md](SOURCE.md);
the original Matt Pocock skills are not runtime dependencies.

## Choose the entry point

Infer the mode from the request; these are workflow modes, not separate tools.

| Request | Work to complete |
| --- | --- |
| Build a new dashboard | Onboard → set up → implement → verify |
| Onboard or set up only | Record the brief, prepare the project, verify the starter, then stop |
| Improve an existing dashboard | Read its project record, inspect the change, implement and verify that scope |
| Review a dashboard | Inspect against its requirements and data contract; report actionable findings |

Use the existing project's documentation layout. For a new project, keep the
brief, setup facts, and evidence in `<project>/docs/dashboard/project.md`, starting from
[assets/project-brief.md](assets/project-brief.md). Reuse the record on later
invocations; repeat only onboarding questions whose answers are missing or changed.

Continue routine, reversible work within the user's request. Surface material
choices without making every phase an approval gate. If required information is
missing, ask only the dependent questions and continue independent work.

## 1. Onboard and prepare the project

Read [references/onboarding-setup.md](references/onboarding-setup.md) on a first
run, a setup-only request, or a material change to the stack or data connection.

Inspect existing files before asking the user for facts. Establish:

- Who uses the dashboard, the decision it supports, and the minimum useful view.
- The actual data source, permitted use, refresh needs, and key metric meanings.
- An existing project or a new target folder, brand/style, access requirements,
  and what counts as done.

Ask a small round of up to three material questions with suggested answers.
Honor answers already in the conversation. Make low-impact defaults explicit;
leave unresolved business rules visible instead of inventing them.

**Ready to build:** the project starts locally, the chosen source or an explicitly
labeled sample is available, and the first useful interaction has an observable
acceptance condition. When within the requested scope, a blocked live connection
can be explored with a clearly marked sample prototype; live integration remains
unverified until the actual connection works.

## 2. Define the dashboard contract

Read [references/data-and-verification.md](references/data-and-verification.md)
before implementing or changing a metric, data connection, or filter, and when
reviewing an existing dashboard.

Record only decisions relevant to this scope: metric formulas and grain, data
quality rules, filter scope, interactions, important UI states, and acceptance
examples. Existing definitions and public module interfaces take priority.

For a small dashboard, a compact brief and task list are enough. For larger work,
split it into independently useful slices with dependencies. Store specs/tasks
locally unless the user requested publishing to a tracker. A source repository
or example repository is never the destination for the user's project tickets.

**Ready to implement:** every requested KPI and control has defined behavior,
and the critical calculations have small examples with independently known
results. Resolve missing business semantics before implementing those metrics.

## 3. Build one useful slice, then expand

Start with one source → one metric → one view → one working filter. Use a source
adapter and shared metric/filter logic so cards, charts, tables, and exports
agree. Follow existing module boundaries; add abstractions only for real reuse.

When the layout or interaction is genuinely uncertain, make a small, disposable
prototype that answers that question. Mark its data and limitations. Capture
the decision it establishes, then implement the production behavior. A request
with an established design does not need a separate prototype round.

Follow the owner's configured visual-design routing and the project's design
system. Read the installed `transitions-dev` skill before implementing UI motion
when available; use the matching recipes/tokens and preserve reduced-motion
support. If it is unavailable, follow existing motion conventions and disclose
that limitation only when it affects the result.

Build to the dashboard's purpose:

- Make the main comparison and active filters easy to read; display units,
  date range, source/freshness, and sample status where they affect interpretation.
- Connect every presented control to real behavior. Omit unimplemented actions,
  or explain an intentionally disabled action.
- Provide the applicable loading, empty, error/retry, stale, and partial-data
  states; distinguish missing data from numeric zero.
- Support the requested screen sizes, keyboard operation, focus, and readable
  chart alternatives. Preserve meaningful content when motion is reduced.

For consequential calculations, parsing, and filter behavior, use one failing
behavior test → minimal implementation → passing test at a time. Test through
public interfaces with independently derived expected results. Use visual
inspection for low-impact layout changes instead of implementation-mirroring
tests. Fix failures before expanding to the next slice.

## 4. Verify and hand over

Apply the verification section of
[references/data-and-verification.md](references/data-and-verification.md).
Run the relevant existing checks, inspect the running UI, and reconcile at least
one important metric with source rows. Include new and uncommitted files when
reviewing; a committed diff alone can omit the actual work.

Keep these two review conclusions separate:

- **Requirements:** requested behavior, correct metrics, missing work, scope drift.
- **Engineering:** project conventions, boundaries, maintainability, and defects
  not already caught by automated checks.

Repair findings within scope and repeat only the affected verification. Record
checks as passed, failed, or not run, with evidence. Never equate a successful
build with correct data or a verified browser experience.

For a full build, deliver the runnable dashboard, accurate startup instructions,
data/setup notes, and verification results. State sample versus live data and
any remaining dependencies. For setup-only work, explicitly report that the
starter is ready and dashboard features remain to be built.

Deployment, public sharing, repository creation, tracker posting, and recurring
refresh jobs follow the user's requested scope and existing authorization; a
dashboard build by itself does not request these actions. If deployment is
requested, choose a compatible target, verify its actual URL, and distinguish
local success from remote deployment evidence.
