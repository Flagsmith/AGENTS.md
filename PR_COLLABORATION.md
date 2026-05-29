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

### PR005: Open the PR as Draft early, and use it to self-review

Push the branch and open a Draft PR as soon as there is a working direction — even before the code is complete. The Draft PR is a self-review tool: use the GitHub diff view to catch leftover debug code, missing tests, unclear naming, and incomplete descriptions. CI also runs on drafts, so failures surface early.

## Requesting Review

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

## Addressing Feedback

### PR013: Link every comment to the commit that addresses it

Each commit should solve one issue. When replying to a comment thread, include the SHA of the commit that resolves it. Multiple comments may point to the same issue — reply to each with the same SHA. A single comment may surface several issues — reference a separate commit for each.

A reviewer should be able to look at any blocking comment and jump straight to the exact change that addressed it. Never leave a thread without a response.

### PR014: Whoever opens a thread, closes it

Only the comment author resolves their own thread, unless it doesn't need a response, or explicitly allowed otherwise. The PR author can reply, push changes, and signal readiness — but the reviewer decides when their concern is satisfied.

## Merging

### PR015: Merge promptly after approval

Don't let approved PRs sit. Stale PRs accumulate conflicts and drift from main.
