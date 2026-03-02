---
name: sync-craft
description: A shared brain for builders. Practical guidance on writing, refactoring, and reviewing code that actually scales.
version: 1.0.0
dependencies:
  - python>=3.10
---

# SyncCraft

A shared brain for builders. Practical guidance on writing, refactoring, and reviewing code that actually scales.

## Overview

SyncCraft is a curated collection of engineering best practices designed to help developers write better, more maintainable code. It provides actionable guidance across Python and Rust, from fundamentals to advanced patterns.

## Skills

### Friendly Python

Practical guidance for writing, refactoring, and reviewing Python code with a Pythonic, readable, and maintainable style.

**Topics:**
- Principles (correctness first, clarity next, performance last)
- Error Handling
- API Design
- Extension Architecture
- OOP Design
- Reuse & Composition
- Portability & Pythonic
- CLI Argparse
- Code Review Checklist

### Piglet

Python fundamentals for developers learning or brushing up on core concepts.

**Topics:**
- Variables and Naming
- Branching and Conditions
- Numbers, Strings, Containers
- Functions and Returns
- Exception Handling
- Loops and Iteration
- Decorators
- Imports and Dependencies
- Rules and File I/O
- SOLID in Python
- Edge Cases
- Walrus Operator

### Fast Rust

Guidance for writing optimized, idiomatic Rust code.

**Topics:**
- Compilation Optimization
- Error Design
- Type Exercise

## Usage

OpenCode will automatically discover these skills. When working on Python or Rust code, the relevant guidance will be available.

Browse the full documentation:

```bash
mkdocs serve
```

Then visit `http://localhost:8000`

## Layout

```
SyncCraft/
├── skills/                      # Skill definitions
│   ├── friendly-python/         # Python best practices
│   ├── piglet/                  # Python fundamentals
│   └── fast-rust/               # Rust optimization
├── references/                 # Shared reference docs
├── overrides/                   # MkDocs theme overrides
├── mkdocs.yml                   # Documentation config
└── opencode.json                # OpenCode configuration
```

## Building Documentation

```bash
pip install mkdocs mkdocs-terminal pymdown-extensions
mkdocs build
```

Output is in the `site/` directory.
