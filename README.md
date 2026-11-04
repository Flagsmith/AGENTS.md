Artefacts for LLM agents used in Flagsmith.

Table of contents:

- [How We Write Code, Tests, and Documentation](#how-we-write-code-tests-and-documentation)
- [How We Collaborate With Pull Requests](#how-we-collaborate-with-pull-requests)

# How We Write Code, Tests, and Documentation

## Honesty (HO)

These apply to tool calls, file changes, and human interactions.

- HO01: **Never** be sycophant. If the user is wrong, be clear.
- HO02: **Never guess.** Either get to the bottom of the topic, or be clear about lacking background.
- HO03: **Never** make any decision based on likelihood. You're encouraged to stop for help.

## Operations (OP)

These apply to tool calls.

- OP01: Locate and use each codebase's standard entrypoints, e.g. `make` targets, before inventing ways to run code.
- OP02: If a request is related to an issue, e.g. in GitHub, **always** fetch it, plus any related issues, pull requests, and all comments within.

## Commenting (CM)

These apply to file changes.

- CM01: Avoid describing the code with a comment. Docstrings for public components are fine.
- CM02: When a comment is necessary, write it in only one line, or preferrably, next to the code in the same line.
- CM03: **Never** write comments that need context. All comments must survive atemporally and without context.

## Code (CO)

These apply to file changes.

- CO01: Choose right over fast. Revisiting for correctness is a waste of resources.
- CO02: Prefer to fix the source of a problem, not just the symptom.
- CO04: Before writing any code, search online for an existing library.
- CO05: **Always** look up online and use the latest stable version of runtimes and dependencies.
- CO06: Write code with meaningful types and names. Refuse to fix typing errors with meaningless types or casts.
- CO07: Add logs when the context needs. Prefer telemetry-friendly structured logs even if a library is required.
- CO08: Run any configured linters, type checkers, formatters, etc after making changes.

## Documentation (DC)

These apply to file changes.

- DC01: **Always** write documentation from the use case perspective.
- DC02: Write minimal documentation. If some content is optional, it should not exist.
- DC03: When the documentation subject involves UI, **always** add screenshots in light theme.
- DC04: When a feature is only available to paid plans, make that clear.

## Tests (TE)

These apply to file changes.

- TE01: Prefer practicing TDD, and start code with functional tests, plus any type contracts.
- TE02: Provide the services to run integration tests against, e.g. to a docker-compose file.
- TE03: **Always** structure every test with `# Given` + `# When` + `# Then`, or `# Given / When` + `# Then` comments without narrative.
- TE04: Aim for 100% diff coverage.
- TE05: Include expected logs in every test body, when the code path involves logging.
- TE06: Avoid tests myopic to the current goal. Prefer improving the existing test suite, such that it will read like the problem being fixed never existed when the work is completed.
- TE07: Avoid utility functions, constants, etc. Tests should be dumb. Tooling such as fixtures and mocks are encouraged.
- TE08: Name a test not from a how-centric perspective. A product person should be able to understand the test goal.
- TE09: **Never** write tests only to meet acceptance criteria, but commit to their responsibility of keeping a semantic reading of the product use cases.

# How We Collaborate With Pull Requests

Best practices and processes for creating and iterating over pull requests. The goal is to make PR reviews faster, easier, and more reliable.

Benefits are improved changelog quality, and reduced friction in collaborating in code, which leads to better DevEx, team bonding, and ultimately faster releasing.

Rules are numbered for easy reference in conversation (e.g. "see PR008") and grouped by phase of the PR lifecycle.

## Before Opening the PR

### PR001: One concern per PR

Keep PRs focused on a single change: one bug fix, one feature, one refactor. Never mix unrelated changes. Use stacked PRs for large features.

### PR002: Write a PR title that belongs in a changelog

Use [Conventional Commits](https://www.conventionalcommits.org/) format: `type(Scope): Imperative description`. The title should express *why*, not *how*. A reader scanning a PR list should understand the scope without opening it.

When the PR fixes a bug or resolves an issue, use the issue name directly in the title: `fix(Scope): <issue name>`. This creates a human-readable link between the PR and the problem it solves — anyone scanning the PR list can immediately recognise which issue was addressed without cross-referencing a tracker.

Examples:

- `fix(Flags): Edit button is unresponsive after creating feature` — traces directly to the reported issue.
- `feat(Webhooks): Delivery retry with exponential backoff` — describes the new capability.
- `refactor(Auth): Extract token refresh into shared middleware` — explains the structural change.

### PR003: Write a description for humans, not machines

Follow the repository's pull request template if one exists. If there isn't one, use this format:

```markdown
Short description of changes. One paragraph. Describe _why_ not _how_.

## Changes
- [ ] High-level list of changes.
- [ ] Items checked according to actual progress.
- [ ] Do not list files, or each change. _How_ is not important here.
- [ ] Each item here must be understood by a product person.

Closes / Contributes to [issue URL]

Review effort: N/5
```

Key points:

- The opening paragraph explains the *motivation* — what's broken, who's affected, or what capability is being added.
- The checklist tracks progress at a product level, not a file level. A product manager should be able to read it.
- Link the issue so anyone can trace the PR back to the original request.
- **Review effort** (1–5) sets expectations: a `1/5` is a trivial rename; a `5/5` needs focused time. This helps reviewers plan their day.

### PR004: Follow the repository's CONTRIBUTING guide

Before opening a PR, check for a `CONTRIBUTING.md` (or similar) in the repository root. It may specify test requirements and other expectations. Following these upfront avoids unnecessary review round-trips.

## Requesting Review

### PR007: CI must be green before requesting review

Do not ask a human to review code that the machines have not let through yet. Fix lint, type, and test failures first.

## Reviewing

### PR008: Submit all comments as a single batch review

Use GitHub's "Start a review" → "Submit review" workflow. Avoid posting individual comments one at a time.

### PR009: Label comments by intent

Some review comments don't have to be addressed.

Be sure to clearly communicate this to the PR author, for example, by using a "suggestion:" or "nitpick:" prefix. There's a more detailed [Conventional Comments](https://conventionalcomments.org/) framework that you can follow to label your intent more specifically.

### PR010: Use neutral, non-accusatory language

Say "This function doesn't close the connection" instead of "You forgot to close the connection." Ask questions instead of giving commands: "What do you think about extracting this?" rather than "Extract this." Avoid "just," "simply," "obviously."

### PR011: Approve when the PR improves code health, not when it's perfect

If the PR makes the codebase better and passes all checks, approve it. There is no such thing as perfect code, only better code. Don't block for polish.

### PR012: Use "Request Changes" without hesitation

If a PR has issues that must be addressed before merging, submit the review as **Request Changes** — not as a Comment with suggestions. This is not a personal judgement; it is a clear signal that the PR is not ready yet. Use it as many times as necessary until the PR actually looks good to merge. Approving out of politeness helps no one.

## Addressing Feedback

### PR013: Link every comment to the commit that addresses it

Each commit should solve one issue. When replying to a comment thread, include the SHA of the commit that resolves it. Multiple comments may point to the same issue — reply to each with the same SHA. A single comment may surface several issues — reference a separate commit for each.

A reviewer should be able to look at any blocking comment and jump straight to the exact change that addressed it. Never leave a thread without a response.

### PR014: Whoever opens a thread, closes it

Only the comment author resolves their own thread, unless it doesn't need a response, or explicitly allowed otherwise. The PR author can reply, push changes, and signal readiness — but the reviewer decides when their concern is satisfied.

## Merging

### PR015: Merge promptly after approval

Don't let approved PRs sit. Stale PRs accumulate conflicts and drift from main.
