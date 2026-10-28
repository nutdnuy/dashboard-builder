# Onboarding and project setup

Use this for a first run or a change to the stack/data connection. Keep the
process conversational. Complete facts by inspection; ask the user for goals,
business rules, and choices the environment cannot establish.

## Inspect before asking

Identify the actual project root and read its applicable agent instructions,
README, dependency manifests/lockfiles, run scripts, existing dashboard pages,
data adapters, tests, and design conventions. Check working-tree changes before
editing. Reuse the project's glossary and architecture decisions when present.

Inspect environment variable **names and presence**, preferably through an
example file or configuration schema. Keep secret values out of chat, generated
docs, logs, screenshots, fixtures, and bundles.

For an empty workspace, choose a new, clearly named project directory. Avoid
scaffolding over existing files or introducing a nested repository by accident.
GitHub login, a remote repository, and an issue tracker are optional for local
dashboard work.

## Conduct a short intake

Collect only unresolved inputs. Useful groups for a first round:

| Topic | What to establish |
| --- | --- |
| Purpose | Audience, question/decision, 3–5 priority metrics or a smaller useful starting set |
| Data | File/API/database, sample schema, date grain, timezone, refresh cadence, access/privacy |
| Experience | Existing/new project, primary device, brand/reference, must-have controls, delivery scope |

Offer a recommended starting view when the user has a domain but no layout.
Use familiar language and explain technical choices only when a decision needs
them. Do not make the user choose every library. If source access or a business
definition is missing, ask precisely for that input; proceed on unaffected work.

Use [the project brief](../assets/project-brief.md) as a seed, not a questionnaire
to present in full. Keep answered decisions, stated assumptions, and unresolved
questions distinct. Resume from this record next time.

## Choose the smallest suitable setup

| Situation | Default |
| --- | --- |
| Existing application | Its current framework, package manager, UI kit, chart library, and conventions |
| New browser dashboard using files or public APIs | React + TypeScript + Vite, unless the user's preferences call for another stack |
| Authentication, private service credentials, or server-side processing | Existing backend/server framework, or a scoped backend chosen for the requirement |
| User chooses Python, BI tooling, or another framework | Follow that choice; preserve the same data and verification contract |

Reuse installed chart/components libraries. Add dependencies only for needed
capabilities, verify their current official documentation, and keep one package
manager/lockfile. Preserve existing version constraints; do not upgrade the
project as an incidental setup step.

For a new Vite project, verify current runtime requirements and scaffolding
options in the [official setup guide](https://vite.dev/guide/) before execution.
An npm example for an unused `my-dashboard` directory is:

```sh
npm create vite@latest my-dashboard -- --template react-ts --no-interactive
cd my-dashboard
npm install
npm run dev -- --host 127.0.0.1
```

Replace the example name with the chosen target. Check that the target is unused
before running it. For an existing project, run its documented install/start
commands instead. A missing system runtime is a specific setup blocker; explain
what is missing rather than silently changing global system configuration.

## Make setup reproducible

1. Install project dependencies using the selected runtime/package manager and
   preserve the lockfile. Record actual versions only after observing them.
2. Configure the required source adapter. Keep labeled synthetic/sample data
   separate from live data and use the same normalized contract for both.
3. Add an `.env.example` only if configuration is needed, with variable names,
   safe placeholders, and explanations. Keep secret-bearing files and private
   data excluded from version control; verify the applicable ignore rules.
4. Keep credentials on the server or in an approved credential store. A static
   browser app cannot keep a service secret. In Vite, `VITE_*` values are public
   client data; see [Vite's environment guide](https://vite.dev/guide/env-and-mode.html).
5. Set up the project's relevant lint/typecheck/build commands and meaningful
   tests for the behavior being built. Record the commands that actually exist;
   do not document an imaginary test script. Git hooks and CI are optional scope.
6. Update the project README with install, configuration, development, checks,
   and build instructions. Add a short pointer to the project record in an
   existing agent instruction file when useful; preserve surrounding rules.

For a human-only step such as provider login or credential issuance, present the
specific missing action, verified provider link, required variable name, and
secure destination. Let the human enter secrets in their own terminal or secret
manager. Continue work that does not depend on that step. Generate a repeatable
manual setup wizard only when it adds value; it is not a prerequisite for normal
onboarding, and this skill does not require Matt Pocock's wizard template.

## Check readiness and support reruns

Start the application and inspect a real page. Verify that the expected data
mode loads and that a relevant build/check succeeds. An HTTP 200 alone does not
prove the UI rendered. Record the actual command, local URL, and evidence.

If there are no dashboard features yet, verify the starter and describe it as
such. If dependencies, login, or data are blocked, record the exact blocker and
separate verified local/sample readiness from unverified live readiness.

On a repeated setup run, inspect first and update only missing or changed
configuration. Preserve user edits, source connections, lockfiles, environment
values, and project instructions. Do not append duplicate setup sections or
recreate the project. Finish with a compact summary of prepared items and the
next useful dashboard slice.
