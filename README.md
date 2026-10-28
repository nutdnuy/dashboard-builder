# Dashboard Builder

An agent skill for building web dashboards, with guided onboarding, repeatable project setup, explicit metric definitions, working filters, and verification.

Adapted from selected [Matt Pocock skills](https://github.com/mattpocock/skills). See [provenance and adaptations](skills/dashboard-builder/SOURCE.md) and the [MIT license](LICENSE).

## Workflow

**Onboarding → Setup → Specification → Build → Verify**

- Discover the audience, decisions, data source, and minimum useful dashboard.
- Reuse an existing project or prepare a suitable new one.
- Define metric formulas, data quality rules, and filter behavior.
- Build one useful end-to-end slice, then expand.
- Verify calculations, interactions, presentation, and project checks.
- Save project decisions so later sessions can resume.

GitHub is the source of the upstream methods, not a required dashboard data source or hosting target. The original Matt Pocock skills are not runtime dependencies.

## Install

Clone this repository, then install the `skills/dashboard-builder` folder into your agent's skill directory. For Codex, use `$CODEX_HOME/skills` or `~/.codex/skills` when `CODEX_HOME` is unset. The installed layout should contain `dashboard-builder/SKILL.md` and its supporting folders.

Preserve an existing installation rather than overwriting it without checking. Nuth's original installation already points to the canonical local source; this repository is a distributable snapshot.

## Use

```text
Use $dashboard-builder to build a sales dashboard from this CSV.
Start with onboarding and setup.
```

Setup only:

```text
Use $dashboard-builder for onboarding and setup only.
```

Existing dashboard:

```text
Use $dashboard-builder to add date and category filters to this dashboard.
```

## Package

| File | Purpose |
| --- | --- |
| [SKILL.md](skills/dashboard-builder/SKILL.md) | Workflow and scope |
| [Onboarding and setup](skills/dashboard-builder/references/onboarding-setup.md) | First-run setup and safe reruns |
| [Data and verification](skills/dashboard-builder/references/data-and-verification.md) | Metrics, filters, UI states, and verification |
| [Project brief](skills/dashboard-builder/assets/project-brief.md) | Resumable project record |
| [Codex metadata](skills/dashboard-builder/agents/openai.yaml) | Display name and starter prompt |

## Validation status

Skill schema, UI metadata, internal links, and the original local Codex deployment were checked structurally. The workflow was manually reviewed. It has not yet been evaluated by using it to build a real dashboard end to end.
