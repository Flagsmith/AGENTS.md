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
