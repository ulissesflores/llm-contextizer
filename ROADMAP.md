# Roadmap

This roadmap is intentionally minimal. The project prioritizes portability, determinism, and LLM-oriented UX.

## Near-term
- ADR: Token Budget Strategy (ordering, prioritization, truncation heuristics)
- `--max-lines` override for truncation (maintain safe defaults)
- `--include-dotfiles` (opt-in) to include `.github/`, `.env.example`, etc.

## Mid-term
- Better `.llmignore` parity with `.gitignore` (wildcards and directory patterns)
- Stable “output format contract” documentation for downstream tooling

## Long-term
- Packaging decision: standalone script vs PyPI distribution