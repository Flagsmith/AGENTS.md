# How We Comment Code

Best practices for writing code comments, in any language, in any repository. The goal is comments that add value to future readers who have no context beyond the merged code.

Benefits are a codebase that explains itself, less noise in reviews, and comments that stay true as the code evolves.

Rules are numbered for easy reference in conversation (e.g. "see CM003").

## CM001: Use doc comments for public functions and classes

Use the language's idiomatic doc comment format — e.g. docstrings in Python — for public functions and classes.

## CM002: Comment only what the code cannot say

We avoid comments unless they reveal useful context only seen outside the code — a dependency's behaviour, a spec, an upstream bug, an external constraint, a business rule. If a comment restates what the code already says, delete it and clarify the code instead.

When a comment is necessary, we prefer terse, one-line comments over long paragraphs. It reveals context as it is, never how the code came to be, so it survives the code across time and adds value to readers with no context. For example:

- "Float sums drift on large totals."
- "Webhooks may arrive out of order."
- "Empty Content-Length is rejected upstream."
- "TODO: https://github.com/org/repo/issues/1234"

## CM003: Avoid deictic comments

A deictic comment references something that exists only in the work session — a conversation, an investigation, a draft — rather than in the code. A future reader has none of that context. For example:

- "This fixes the failing test in CI" — deixis about a situation.
- "The cache was returning stale segments here" — deixis about a debugging session.
- "TODO: remove this logic branch before shipping to production" — deixis about team dynamics.
- "Decision 3: evaluate in the view" — deixis about a decision-making process.
- "Switched from offset pagination to cursors" — deixis about a prior draft.
- "We no longer recompute this on every request" — deixis about a discarded approach.
