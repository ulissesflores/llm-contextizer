
# LLM Contextizer

**A zero-dependency CLI tool that converts entire codebases into optimized textual contexts for Large Language Models (LLMs).**

<p align="center">
  <img src="https://img.shields.io/badge/license-Apache--2.0-blue.svg" alt="License">
  <img src="https://img.shields.io/badge/python-3.8%2B-blue" alt="Python">
  <img src="https://img.shields.io/badge/dependencies-zero-brightgreen" alt="Dependencies">
  <img src="https://img.shields.io/badge/status-stable-green" alt="Status">
</p>

### TL;DR

`LLM Contextizer` scans a project directory, prints a readable ASCII tree, and then emits a single concatenated text output of file contents — optimized for copy/paste into ChatGPT, Claude, Gemini, or any LLM.

```bash
python3 src/contextizer.py /path/to/project > context.txt
```
**Why this exists**
-------------------

LLMs have limited context windows, and real repositories contain:

-   dependency folders (node_modules, venv, etc.)

-   build artifacts, caches, binaries

-   large data/log files that explode token budgets

This tool aims to be:

-   **portable** (standard library only)

-   **deterministic** (stable ordering)

-   **safe-by-default** (avoids common footguns)

-   **LLM-friendly** (tree first, then contents)

* * * * *

**Key features**
----------------

-   **Project tree visualization**

    Outputs an ASCII directory tree before the content dump.

-   **Noise filtering by default**

    Skips common junk folders and binary extensions (.git, node_modules, venv, images, archives, etc.).

-   **Truncation for "large/log-like" files**

    Truncates certain file types (e.g., .csv, .log) to the first N lines.

-   **Per-project configuration via** **.llmignore**

    Add a .llmignore at the project root to exclude additional paths.

-   **Output safety: avoids self-inclusion**

    If you redirect stdout to a file inside the scanned root, the tool attempts to detect and exclude that output file.

* * * * *

**Installation**
----------------

Clone the repo --- no dependencies.

```bash
git clone https://github.com/ulissesflores/llm-contextizer.git
cd llm-contextizer
```

Optional: make it easy to call from anywhere.

```bash
alias llmctx='python3 /absolute/path/to/llm-contextizer/src/contextizer.py'
```


**Usage**
---------

Run against the current directory:
```bash
python3 src/contextizer.py
# or (with alias)
llmctx
```

Target another directory:
```bash
python3 src/contextizer.py ../some-project
```

Save to a file:
```bash
python3 src/contextizer.py . > context.txt
```

Pipe to clipboard:
```bash
python3 src/contextizer.py . | pbcopy   # macOS
python3 src/contextizer.py . | xclip    # Linux
```

**Output format**
-----------------

The output has two parts:

1.  PROJECT STRUCTURE

2.  PROJECT FILE CONTENTS with file separators and relative paths

This consistent structure helps an LLM understand the repository before reading the code.


**Configuration**
-------------------

**.llmignore**
--------------

Create a .llmignore file at the project root you are scanning.

### **Supported syntax (intentionally minimal)**

-   dir/ ignores a directory (by name)

-   *.ext ignores a file extension

-   filename ignores a specific file name

Example:


```txt
# directories (by name)
dist/
build/
coverage/
__pycache__/

# secrets
.env
.env.*
*.pem
*.key

# large/noisy
*.log
*.csv
*.tsv
*.jsonl
```


Tip: the repository includes a ready-to-copy template: .llmignore.example.

**Architectural Decisions (ADRs)**
----------------------------------

Core decisions are documented under docs/adr/:

-   ADR 0001: Zero Dependencies Policy

-   ADR 0002: Output Safety (Prevent self-inclusion on stdout redirect)


**Versioning**
--------------

This project follows **Semantic Versioning** and maintains a human-readable changelog in CHANGELOG.md.

-   Patch: bug fixes (0.1.x)

-   Minor: backwards-compatible feature additions (0.x.0)

-   Major: breaking changes (x.0.0)


**Contributing**
----------------

Contributions are welcome.

1.  Fork the repository

2.  Create a branch from main

3.  Keep changes focused (one concern per PR)

4.  Add/update docs when behavior changes

5.  Open a PR

## Citation

If you use this software in academic or research contexts, please cite the Zenodo archival release (immutable snapshot):

**LLM Contextizer v0.1.1**  
DOI: https://doi.org/10.5281/zenodo.18343438

**License**
-----------

Licensed under the Apache License 2.0. See LICENSE.

The DOI currently points to the archived v0.1.1 snapshot on Zenodo; later tags may not yet be archived.