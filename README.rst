# TinyDB Seeded Bug Benchmark

A controlled bug-seeding benchmark built on [TinyDB](https://github.com/msiemens/tinydb), a lightweight document-oriented database written in Python.

## Overview

This repository contains a seeded version of TinyDB 4.9.0 with **10 intentionally introduced bugs** across its caching, table operations, query handling, storage, middleware, and utility modules.

The benchmark is intended to support systematic evaluation of debugging and software-engineering workflows. Participants can investigate unexpected behavior, identify root causes, and develop targeted fixes against an existing test suite.

## Base Repository

- **Upstream project:** [msiemens/tinydb](https://github.com/msiemens/tinydb)
- **Version:** TinyDB 4.9.0
- **Base commit:** `6d7c4fc3e04d398b1282876514660a33a7897b41`
- **Seeded branch:** `seeded`

## Seeded Bug Categories

| ID | Area | Intended behavior affected |
|---|---|---|
| P1-A | LRU cache | Cache recency updates |
| P1-B | Query caching | Cacheability checks |
| P2-A | Operations | String addition behavior |
| P2-B | Table updates | Handling missing document IDs |
| P3-A | Database | Table registry cleanup |
| P3-B | Table operations | ID reset after truncation |
| I1 | Middleware | Cache flush threshold |
| I2 | Storage | Parent directory creation |
| I3 | Queries | Regular-expression search flags |
| I4 | Utilities | Recursive freezing of dictionary values |

These identifiers group the seeded defects by benchmark category. The actual code changes and observed test failures should be used to determine the precise behavior of each defect.

## Setup

Requirements:

- Python
- Git

Clone the repository and switch to the seeded branch:

```bash
git clone -b seeded https://github.com/Prerna2222/tinydb-seeded-benchmark.git
cd tinydb-seeded-benchmark
```

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the project and its test dependencies as required by the repository:

```bash
python -m pip install -e .
python -m pip install pytest
```

## Running Tests

Run the test suite:

```bash
python -m pytest -p no:cacheprovider -o addopts="" -q --tb=short
```

To generate a JUnit XML report, create a `results` directory in the parent workspace or adjust the report path to a directory that exists:

```bash
mkdir -p ../results
python -m pytest -p no:cacheprovider -o addopts="" -q --tb=short --junitxml=../results/seeded.xml
```

## Current Validation Status

The recorded baseline on the unmodified upstream version was **228 passing tests**.

The latest cumulative run on the seeded branch reported:

- **193 passed**
- **35 failed**
- **228 total**

These are cumulative results with all seeded defects active simultaneously. They do not establish that each defect independently causes a distinct set of failures. Independent reproduction and reference-fix validation remain separate validation tasks.

## Benchmark Scope

The current scope focuses on planted defects in an existing Python codebase. It is intended to support:

- Reproducing failing tests
- Tracing failures to their underlying causes
- Developing minimal, targeted patches
- Running regression tests
- Recording test outcomes for evaluation

## Notes

- The seeded branch intentionally differs from upstream TinyDB.
- The cumulative test results are a snapshot of the current seeded state, not a claim that every defect has been independently validated.
- Keep benchmark answer keys, reference patches, and private evaluation artifacts separate from any repository distributed to participants.

## Acknowledgements

This benchmark is based on [TinyDB](https://github.com/msiemens/tinydb), an open-source Python project.
