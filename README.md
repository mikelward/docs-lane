# docs-lane

Lets housekeeping-only pull requests skip a repository's heavy CI jobs, while
one required check still reports on every pull request.

## Why this exists

A branch-protection rule can only require checks *by name*, and a required
check that never reports blocks the pull request forever. So the obvious
implementation — a `paths:` filter that skips the workflow for
documentation-only diffs — is exactly the trap: the check never runs, so it
never reports, so nothing merges.

This repository holds the way around that, extracted from the copies that grew
up in several sibling repositories: the workflow runs on *every* pull request,
a `classify` step decides whether the heavy jobs may skip, and a `gate` step —
the only one a ruleset should require — independently re-derives that decision
before blessing a skip. A classification bug becomes a red check rather than a
silent merge.

## Status

Scaffolding only. The engine, its test harness and the action manifest arrive
in the first pull request against this branch; until then there is nothing here
to consume.

## License

MIT.
