# Provenance and adaptations

Created for Nuth on 2026-10-28. This is a manually authored dashboard workflow
adapted from selected methods in [Matt Pocock's skills](https://github.com/mattpocock/skills),
not an upstream Matt Pocock release or endorsement.

The upstream files below were read at commit
[`59db609eb1e18aaf59b63284d0e52255aff0c63c`](https://github.com/mattpocock/skills/commit/59db609eb1e18aaf59b63284d0e52255aff0c63c).
The bundled [LICENSE.txt](LICENSE.txt) preserves the upstream MIT notice.

| Source | Method retained | Dashboard adaptation |
| --- | --- | --- |
| [setup-matt-pocock-skills](https://github.com/mattpocock/skills/blob/59db609eb1e18aaf59b63284d0e52255aff0c63c/skills/engineering/setup-matt-pocock-skills/SKILL.md) | Inspect before setup; reuse per-project configuration | A resumable dashboard record and real local startup; tracker setup is optional |
| [grilling](https://github.com/mattpocock/skills/blob/59db609eb1e18aaf59b63284d0e52255aff0c63c/skills/productivity/grilling/SKILL.md) | Resolve dependent decisions; investigate facts | Short rounds of material questions, with routine defaults and existing answers respected |
| [to-spec](https://github.com/mattpocock/skills/blob/59db609eb1e18aaf59b63284d0e52255aff0c63c/skills/engineering/to-spec/SKILL.md) | Synthesize requirements, implementation decisions, and test boundaries | Compact local brief with KPI and filter contracts; no automatic tracker publication |
| [prototype](https://github.com/mattpocock/skills/blob/59db609eb1e18aaf59b63284d0e52255aff0c63c/skills/engineering/prototype/SKILL.md) | A disposable prototype answers a specific uncertainty | Optional layout/interaction experiment; no mandatory throwaway branch or publication |
| [tdd](https://github.com/mattpocock/skills/blob/59db609eb1e18aaf59b63284d0e52255aff0c63c/skills/engineering/tdd/SKILL.md) | Vertical slices, public behavior, independent expected values | Prioritize metric, parsing, and filter correctness; do not test trivial styling or require seam approval on every task |
| [code-review](https://github.com/mattpocock/skills/blob/59db609eb1e18aaf59b63284d0e52255aff0c63c/skills/engineering/code-review/SKILL.md) | Separate requirements and engineering review | Includes uncommitted/new work; usable without mandatory subagents |
| [wizard](https://github.com/mattpocock/skills/blob/59db609eb1e18aaf59b63284d0e52255aff0c63c/skills/engineering/wizard/SKILL.md) | Human steps have a concrete origin and destination | Guidance for login/credential setup only when necessary; no dependency on upstream shell templates |

Authoring also used the locally installed `mattpocock-writing-for-agents`
reference for conditional context pointers and observable completion criteria.
It is not a dependency of the resulting skill.

New dashboard-specific material covers metric semantics, source validation,
cross-view consistency, freshness, accessibility, responsive inspection, and
verification evidence. Existing host persona, privacy, visual routing, motion,
and authorization rules remain authoritative.

Vite setup and browser environment guidance were checked against the official
[getting-started](https://vite.dev/guide/) and
[environment](https://vite.dev/guide/env-and-mode.html) documentation on 2026-10-28.
Recheck current requirements when creating a real project; no runtime version
or chart-library version is pinned by this skill.

The original skills remain unchanged. Validation of this package is reported
separately from running it to build a real dashboard; structural validation does
not establish end-to-end behavior or measured quality improvement.
