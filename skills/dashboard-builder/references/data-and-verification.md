# Dashboard data and verification contract

Apply the parts relevant to the requested change. A dashboard is trustworthy
when a reader can explain a number, change a filter, and reconcile the result
with its source.

## Define metrics before drawing them

For each requested metric, record its name, meaning, source fields, row grain,
formula/aggregation, unit, date/timezone, inclusion rules, and filter scope.
Also resolve the applicable edge cases:

- Stable keys and duplicates; join cardinality and how double counting is avoided.
- Null/missing/invalid values versus real zero; rows rejected or only partially usable.
- Currency/unit conversions, rounding for presentation, and negative values.
- Time boundaries, date-only versus timestamp fields, and partial periods.
- Comparison periods, denominators, and the result when a denominator is zero.
- For rates/percentages, whether to use aggregate numerators and denominators
  or a justified alternative; never silently average incompatible percentages.

Treat CSV, API payloads, database rows, and labels as untrusted data. Validate the
contract at the boundary and render text safely. Keep private data out of public
assets, static bundles, and screenshots intended for sharing. Show validation
failures or excluded-row counts when they change interpretation.

Keep one normalized dataset and shared filter/aggregation definitions. Give
unfiltered benchmarks or independently filtered panels explicit labels. Explain
the scope of table sorting, pagination, drilldowns, and exports when present.
An export should state whether it includes all filtered rows or only the page.

## Specify interactions and states

Write observable outcomes for the controls the user actually requested:

- A filter updates the intended cards, series, and table; reset returns to the
  recorded default scope.
- Search and sorting use declared fields and types; a page change keeps active
  filters; drilldown retains context where appropriate.
- Loading, no matching rows, missing/invalid source, stale cached data, and
  partial results have distinct, accurate presentations.
- With asynchronous sources, the newest requested filters win even if an older
  request returns later. Failures do not silently become a zero-valued dataset.
- Data freshness reflects the actual source/update time, not the current time
  rendered on every page load.

Use plain labels, units, meaningful axes, and comparison baselines. Provide a
readable summary or table for chart information that otherwise depends on hover
or color alone. Evaluate the layout at the user's target sizes, including a
narrow screen when the dashboard is expected to be responsive.

## Use independent examples

Keep a small fixture with known results to verify business behavior. For example,
if a fixture has East transactions of 100 and 50 and a West transaction of 40,
the all-region total is 190, the East filter shows 150, and resetting restores
190. Derive expectations from the documented rule or hand-worked source rows,
not from the same production function being tested.

This is a sales example, not a default schema or KPI set. Choose equivalent
examples for the user's domain. Exercise the edge cases that can materially
change the requested metrics rather than creating exhaustive UI snapshots.

## Verify at the right boundaries

| Layer | Evidence to collect |
| --- | --- |
| Source and calculations | Representative source rows, independently computed results, and focused behavior tests |
| User interaction | Change a filter, inspect all affected outputs, exercise reset and relevant empty/error cases |
| Presentation | Running UI at target sizes; legible labels, keyboard/focus, meaningful chart alternative, reduced-motion behavior when motion exists |
| Project | Existing lint/type checks, relevant tests, and build; failures distinguished from pre-existing issues |
| Deployment, only if requested | Successful deployment plus direct inspection of the actual served URL and data mode |

Use the available browser/test tooling for real interaction. A screenshot proves
only the state pictured; a build proves only that the build passed. If browser
access is unavailable, run what is possible and explicitly leave visual and
interaction verification unverified. Do not claim end-to-end completion.

Review the actual modified and new files in two passes: **Requirements** against
the brief and data contract, and **Engineering** against project standards and
maintainability. Keep their findings separate. The review can be performed by
one agent; independent agents are optional when authorized and useful.

When a check fails, reproduce the failure, identify the smallest cause, repair
it, and rerun the affected checks. Stop extending scope once the requested
behavior and required checks pass. Record exact checks and meaningful limitations
in the project record so a later session can resume without re-onboarding.
