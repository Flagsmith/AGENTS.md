# How We Collaborate With Pull Requests

This is the playbook the Flagsmith engineering team and our review agents follow when working with pull requests. External contributors should start at [CONTRIBUTING.md](CONTRIBUTING.md).

Benefits are improved changelog quality, and reduced friction in collaborating in code, which leads to better DevEx, team bonding, and ultimately faster releasing.

Rules are numbered for easy reference in conversation (e.g. "see PR008") and grouped by phase of the PR lifecycle.

## Before opening the PR

### PR001: One concern per PR

Keep PRs focused on a single change: one bug fix, one feature, one refactor. Never mix unrelated changes. Use stacked PRs for large features.

### PR002: Write a PR title that belongs in a changelog

Use the [Conventional Commits](https://www.conventionalcommits.org/) format: `type(Scope): Imperative description`. The title should express *why*, not *how* — a reader scanning a PR list should understand the scope without opening it. The title is what [release-please](https://github.com/googleapis/release-please) lifts into the changelog and what humans use to refer to the change in conversation.

The accepted `type` values are the ones our [Conventional Commit labeller](.github/workflows/platform-pull-request.yml) recognises. A title outside that set silently skips labelling — fix the title rather than adding the label by hand.

When the PR resolves an issue, reuse the issue title verbatim so the link between problem and fix is obvious from the PR list:

- `fix(UI): Edit button is unresponsive after creating feature`
- `feat(Webhooks): Delivery retry with exponential backoff`
- `refactor(Auth): Extract token refresh into shared middleware`

### PR003: Fill in the PR template properly

This repository's [pull request template](.github/pull_request_template.md) is not a formality — every section drives part of the review:

- **Changes** — a product-level summary of what the PR does, with `Closes #N` or `Contributes to #N` linking the issue. Do not list files or describe the diff; the diff already does that. The reader should be a product person, not a compiler.
- **How did you test this code?** — concrete steps a reviewer can re-run, or a clear statement that automated tests cover it. "Tested locally" on its own is not an answer.

Tick the checklist boxes only after the work behind them is actually done. Unchecked boxes signal to the reviewer that the PR is not yet ready.

### PR004: Honour the repository's CONTRIBUTING guide

[CONTRIBUTING.md](CONTRIBUTING.md) is the contract with external contributors and the source of truth for repo-level expectations the PR template doesn't capture — target branch, deployment story, test coverage policy, local setup. Re-read it when something feels off; following it upfront avoids review round-trips that exist only because the rules were not in shared view.

### PR005: Open the PR as Draft early, and use it to self-review

Push the branch and open a Draft PR as soon as there is a working direction — even before the code is complete. The Draft PR is a self-review tool: use the GitHub diff view to catch leftover debug code, missing tests, unclear naming, and incomplete descriptions. CI also runs on drafts, so failures surface early.

## Requesting review

### PR006: Mark Ready for Review

When self-review is done and CI is green, move the PR out of Draft. We have automation in GitHub to select reviewers on a rotating basis.

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

## Addressing feedback

### PR013: Link every comment to the commit that addresses it

Each commit should solve one issue. When replying to a comment thread, include the SHA of the commit that resolves it. Multiple comments may point to the same issue — reply to each with the same SHA. A single comment may surface several issues — reference a separate commit for each.

A reviewer should be able to look at any blocking comment and jump straight to the exact change that addressed it. Never leave a thread without a response.

### PR014: Whoever opens a thread, closes it

Only the comment author resolves their own thread, unless it doesn't need a response, or explicitly allowed otherwise. The PR author can reply, push changes, and signal readiness — but the reviewer decides when their concern is satisfied.

## Merging

### PR015: Merge promptly after approval

Don't let approved PRs sit. Stale PRs accumulate conflicts and drift from main.
