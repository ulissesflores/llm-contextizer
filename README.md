
# LLM Contextizer

**A zero-dependency CLI tool that converts entire codebases into optimized textual contexts for Large Language Models (LLMs).**

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License">
  <img src="https://img.shields.io/badge/python-3.8%2B-blue" alt="Python">
  <img src="https://img.shields.io/badge/status-stable-green" alt="Status">
  <img src="https://img.shields.io/badge/dependencies-zero-brightgreen" alt="Dependencies">
</p>

### TL;DR

> **LLM Contextizer** scans a project, builds a readable directory tree, and emits a **single, token-efficient text context** --- ready to paste into ChatGPT, Claude, Gemini, or any LLM.

What problem does it solve?
---------------------------

Large Language Models have **limited context windows**.

**Real-world codebases:**

-   Are large

-   Contain noise (binaries, caches, lock files)

-   Break token budgets quickly

**LLM Contextizer** solves this by:

-   Selecting only what matters

-   Structuring context for comprehension

-   Eliminating setup and dependencies

✨ Key Features
--------------

-   **Automatic Context Optimization**\
    Skips irrelevant directories and artifacts (`.git`, `node_modules`, `venv`, binaries).

-   **Smart File Truncation**\
    Large logs and CSVs are truncated while preserving headers and early rows.

-   **Project Tree Visualization**\
    Emits an ASCII tree so LLMs understand structure *before* reading code.

-   **Configurable via `.llmignore`**\
    Per-project ignore rules using familiar `.gitignore` syntax.

-   **Zero Dependencies**\
    Uses only the Python standard library. No `pip`, no virtual environments.

📦 Installation
---------------

Clone the repository --- that's it.

`git clone https://github.com/ulissesflores/llm-contextizer.git
cd llm-contextizer`

 Set Global Alias

`alias llmctx='python3 /path/to/llm-contextizer/src/contextizer.py'`


🛠 Usage
--------

From any project directory:

`llmctx`

Save output to a file:

`llmctx > context.txt`

Target a different directory:

`llmctx ../other-project`

Pipe directly into your clipboard:

`llmctx | pbcopy   # macOS`
`llmctx | xclip    # Linux`


⚙️ Configuration (`.llmignore`)
-------------------------------

Customize exclusions by adding a `.llmignore` file to the project root.

```bash 
# Directories
secret_keys/
legacy_code/

# File types
*.mp4
*.log

# Specific files
sensitive_data.json
```

🧱 Architecture Decision Record
-------------------------------

### ADR 0001 --- Zero Dependencies Policy

**Status:** Accepted\
**Date:** 2026-01-20

**Decision:**\
LLM Contextizer uses **only the Python standard library**.

**Rationale:**

-   Maximum portability

-   No environment friction

-   Lower security and supply-chain risk

This constraint is deliberate and foundational.

🏗 Development Notes
--------------------

Make the script executable:

```bash
chmod +x src/contextizer.py
```

Initialize the repository:
```bash
git init
git add .
git commit -m "feat: initial release of LLM Contextizer"
git branch -M main
```


🤝 Contributing
---------------

Contributions are welcome and encouraged.

1.  Fork the repository

2.  Create a branch from `main`

3.  Follow **PEP 8**

4.  Add docstrings (Google style)

5.  Test locally

6.  Open a Pull Request 🚀

* * * * *

📄 License
----------

This project is licensed under the **MIT License**.\
See the `LICENSE` file for details.