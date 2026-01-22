# ADR 0002: Output Safety – Prevent Self-Inclusion When Redirecting stdout

- Status: Accepted
- Date: 2026-01-22
- Deciders: Ulisses Flores

## Context

The tool is designed to be pipe-friendly and to support typical Unix workflows such as:

- `llmctx > context.txt`
- `llmctx | pbcopy`

A critical failure mode exists when stdout is redirected to a file located inside the scanned root:
the output file can be discovered during traversal and included in the dump, causing self-inclusion and
exponential growth across repeated runs.

This is a “footgun” that violates safe-by-default expectations for CLI tooling.

## Decision

When stdout is redirected to a file path that can be determined at runtime, and the destination file
is within the scanned root, the tool SHALL exclude that output file from traversal and dumping.

## Rationale

- Prevent unbounded output growth.
- Preserve idempotence of repeated runs.
- Maintain expected Unix/pipe behavior without requiring users to add `.llmignore` rules.

## Consequences

### Positive
- Safe default for `> file` workflows.
- Users do not need to know about or manage this hazard.

### Negative
- In some environments, the destination path may not be discoverable; in that case, safety relies on
  `.llmignore` or writing output outside the scanned directory.

## Implementation Notes

- Detect whether stdout is a TTY.
- If redirected, attempt to resolve `sys.stdout.name` to a real path.
- Exclude that path during ignore checks.