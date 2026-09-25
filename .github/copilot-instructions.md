## Commit messages

Generate all commit messages in **Conventional Commits** format:

```
<type>(<optional scope>): <description>

[optional body]

[optional footer(s)]
```

**Rules:**

- **Type** is required and must be one of:
  - `feat` — a new feature
  - `fix` — a bug fix
  - `docs` — documentation only
  - `style` — formatting, whitespace, no code-behavior change
  - `refactor` — code change that neither fixes a bug nor adds a feature
  - `perf` — a performance improvement
  - `test` — adding or correcting tests
  - `build` — build system or dependency changes
  - `ci` — CI/CD configuration changes
  - `chore` — routine maintenance, no production code change
  - `revert` — reverts a previous commit
- **Scope** is optional and given in parentheses after the type (e.g. `feat(identity):`). Use a short, lowercase area name when it adds clarity.
- **Description** is a short, imperative-mood summary ("add", not "added"/"adds"), lowercase, no trailing period, ideally ≤ 72 characters.
- **Body** (optional) explains the *what* and *why*, not the *how*. Separate it from the description with one blank line.
- **Breaking changes** are indicated with a `!` before the colon (e.g. `feat!:`) and/or a `BREAKING CHANGE:` footer describing the change.
- Reference issues/PRs in the footer where relevant (e.g. `Closes #123`).

**Examples:**

```
feat(identity): add bulk user offboarding endpoint
fix(graph): handle expired token on retry
docs: update authentication model overview
refactor(standards)!: rename remediation parameter
```


## vexp <!-- vexp v3.1.0 -->

### Context strategy: call run_pipeline ONCE at task start
If the task already names the files/symbols to touch, SKIP vexp. Otherwise one
`run_pipeline({ "task": "..." })` returns ranked pivot files with line ranges and
blast radius. Do NOT open files one by one to find your way around - every extra
tool call costs a turn. Call it again ONLY when the task moves to a new area.
`get_skeleton` for files to understand, not edit. `verify_done` before calling a
multi-file task complete, then RUN the tests it names.

### Query shape (do this)
Anchor the task on real identifiers (ClassName, functionName) or file paths:
`run_pipeline({ "task": "fix JWT expiry in AuthService.validateToken" })`

vexp runs entirely on this machine, index in `.vexp/`;
`run_pipeline` transmits nothing to any external service.
On `status: "degraded"` or 0 pivots the index is still building - use your own tools.
For literal string sweeps use your native search - do NOT route text sweeps through vexp.
Repo SOURCE only: logs, dist/, node_modules/ and files outside the repo are NOT indexed.
<!-- /vexp -->