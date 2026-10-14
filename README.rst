TinyDB Seeded Bug Benchmark
===========================

OVERVIEW
--------

A controlled bug-seeding benchmark built on TinyDB, a lightweight document-oriented database written in Python.

This repository contains a seeded version of TinyDB 4.9.0 with 10 intentionally introduced bugs across caching, table operations, query handling, storage, middleware, and utility modules.

The benchmark is designed to evaluate debugging and software-engineering workflows by investigating unexpected behavior, identifying root causes, and developing targeted fixes.

BASE REPOSITORY
---------------

Upstream project: https://github.com/msiemens/tinydb
Version: TinyDB 4.9.0
Base commit: 6d7c4fc3e04d398b1282876514660a33a7897b41
Seeded branch: seeded

SEEDED BUG CATEGORIES
---------------------

P1-A: LRU cache recency updates
P1-B: Query caching and cacheability checks
P2-A: String addition behavior in operations
P2-B: Handling missing document IDs during updates
P3-A: Table registry cleanup
P3-B: ID reset after table truncation
I1: Caching middleware flush threshold
I2: Parent directory creation in storage
I3: Regular-expression search flags
I4: Recursive freezing of dictionary values

SETUP
-----

Requirements:
- Python
- Git

Clone the repository:

git clone -b seeded https://github.com/Prerna2222/tinydb-seeded-benchmark.git

cd tinydb-seeded-benchmark

Create and activate a virtual environment:

python3 -m venv .venv
source .venv/bin/activate

Install the project and testing dependencies:

python -m pip install -e .
python -m pip install pytest

RUNNING TESTS
-------------

Run the test suite:

python -m pytest -p no:cacheprovider -o addopts="" -q --tb=short

Generate a JUnit XML report:

mkdir -p ../results

python -m pytest -p no:cacheprovider -o addopts="" -q --tb=short --junitxml=../results/seeded.xml

CURRENT VALIDATION STATUS
-------------------------

Baseline on the unmodified upstream version:
228 tests passed.

Latest recorded run on the seeded branch:
193 tests passed.
35 tests failed.
228 tests total.

These results represent a cumulative run with all seeded defects active simultaneously. They do not prove that each defect independently causes a distinct set of failures. Independent reproduction and reference-fix validation remain outstanding.

BENCHMARK SCOPE
---------------

The benchmark supports:
- Reproducing failing tests.
- Tracing failures to their root causes.
- Developing targeted patches.
- Running regression tests.
- Recording test outcomes for evaluation.

NOTES
-----

The seeded branch intentionally differs from upstream TinyDB.

The recorded test results describe the current seeded state and should not be interpreted as proof that every defect has been independently validated.

Keep benchmark answer keys, reference patches, and private evaluation artifacts separate from any repository distributed to participants.

ACKNOWLEDGEMENTS
----------------

This benchmark is based on TinyDB, an open-source Python project.

Upstream repository: https://github.com/msiemens/tinydb
