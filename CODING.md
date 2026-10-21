## Commenting (CM)

These apply to file changes.

- CM01: Avoid describing the code with a comment. Docstrings for public components are fine.
- CM02: When a comment is necessary, write it in only one line, or preferrably, next to the code in the same line.
- CM04: **Never** leave deixis in comments. All comments must survive atemporally and without context.

## Code (CO)

These apply to file changes.

- CO01: Choose right over fast. Revisiting for correctness is a waste of resources.
- CO02: Prefer to fix the source of a problem, not just the symptom.
- CO04: Before writing any code, search online for an existing library.
- CO05: **Always** look up online and use the latest stable version of runtimes and dependencies.
- CO06: Write code with meaningful types and names. Refuse to fix typing errors with meaningless types or casts.
- CO07: Add logs when the context needs. Prefer telemetry-friendly structured logs even if a library is required.
- CO09: Run any configured linters, type checkers, formatters, etc after making changes.

## Documentation

- DC01: **Always** write documentation from the use case perspective.
- DC02: Write minimal documentation. If some content is optional, it should not exist.
- DC03: When the documentation subject involves UI, **always** add screenshots in light theme.
- DC04: When a feature is only available to paid plans, make that clear.
