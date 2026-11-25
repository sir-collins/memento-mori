# Commenting standards

## Why we comment

Comments help future-you (and reviewers) understand *intent* and *decisions*.
They don't restate what the code already says. A comment that only narrates
the next line is noise, so delete it instead of writing it.

## Rule 1: document the exported API

**Go (`api/`).** Every exported identifier (type, func, const, method) gets a
doc comment, following the Go convention: a full sentence that starts with
the identifier's name.

```go
// BuildSummary returns the lived/remaining week counts for a life of
// targetYears, measured at now.
func BuildSummary(birthDate, now time.Time, targetYears int) Summary
```

Every package gets one package comment (`// Package life …`) in one of its
files. `go doc` and pkg.go.dev read these, and linters check for them.

**TypeScript (`web/`).** Exported functions, hooks, stores and non-trivial
components get a one-line TSDoc block (`/** … */`). Add `@param`/`@returns`
only when the name and type don't already say it.

## Rule 2: inline comments explain "why", never "what"

Save `//` comments for decisions that aren't obvious: why dates are
normalised to UTC midnight, why a guard clause exists, a workaround for a
library quirk. If you can tell what a line does by reading it, it needs no
comment.

## Rule 3: no stale comments

A wrong comment is worse than no comment. Update or delete a comment in the
same change that changes the code it describes.

## Rule 4: file-header comments are the exception

Most files don't need one. In Go the package comment and doc comments cover
it. Add a header only when a file's role isn't obvious from its name and
location.

## Scope

This standard applies to production code in `api/` and `web/src/`. Test files
(`*_test.go`, `*.test.ts(x)`) are exempt. Test names and table-driven case
names already document intent.
