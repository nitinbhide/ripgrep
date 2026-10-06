---
folder: "tests"
generated_on: "2026-10-06"
num_files: 22
semantic_tags: [binary-fixtures, binary-search, binary-test-fixture, cli, compressed-data, compressed-test-fixture, compression, indexing, integration-tests, json, nul-byte, options, regression-tests, rust, search-tests, test-data, test-organization, test-suite, text-corpus]
todos_present: true
dependencies: []
confidence: high
---

# Folder Overview

## Purpose
This folder contains ripgrep's CLI integration tests and the shared test support used to run them. The Rust suites exercise core search features, binary data, JSON output, multiline matching, and historical regressions. A shared corpus, macros, and command helpers make test cases concise and consistent.
The tests are grouped into modules, with fixed data and indexing cases documented in standalone child-folder maps.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

Defines the integration-test suite through `tests.rs` and provides helpers for isolated working directories, command execution, output checks, and fixture data. Child folders contain fixed test data and focused index-feature tests, each with its own standalone docmap.

## Technology Notes

The folder uses Rust test modules and exercises the ripgrep command-line executable. The source shows shared integration-test macros and support utilities; no dependency graph is generated.

# Folder Navigation

## Merged Child Folders
- `data/` —
  This folder contains fixed input fixtures used by the integration tests. The fixtures include compressed forms of a Sherlock Holmes text and a text corpus containing a NUL byte. Eight compressed files are binary and cannot be summarized from their payloads here. Their intended test role is visible in the test sources, so confidence for those file descriptions is low.
- `index/` —
  This folder contains integration tests for ripgrep's indexing feature. Its module file groups a basic index interaction test and a suite documenting currently disallowed behavior. The tests use the shared integration-test command and directory helpers.
  The source comments identify the disallowed cases as restrictions that may change over time.
## Files
- `binary.rs` (Size : 18214 bytes): Tests detection and reporting of binary input, especially how NUL bytes interact with explicit versus recursive searches, `--binary`/`--text`, counts, and memory mapping. It uses the NUL-containing fixture in `data` to exercise matches before and after the binary marker. Assertions check output and whether searches fail or succeed for each mode. Comments note that memory-mapped handling differs and that some mmap tests are excluded on macOS.
    - Tags: [binary-detection, integration-tests, mmap, rust]
    - TODO/FIXME/NOTE: line 20 — `note`; line 31 — `Note`; line 66 — `Note`

- `feature.rs` (Size : 39718 bytes): Contains feature-oriented CLI integration tests, with many cases linked in comments to issue numbers. The cases cover encoding, pattern sources, output fields, glob and ignore handling, depth and size limits, sorting, statistics, multiline and CRLF behavior, replacements, and exit statuses. Its test cases construct temporary fixtures and check CLI output or errors. The suite is the stated location for tests of new ripgrep features.
    - Tags: [cli-features, integration-tests, rust, search]

- `hay.rs` (Size : 851 bytes): Defines shared Sherlock Holmes text constants in LF and CRLF forms. Other integration tests use these fixtures to check matching, line endings, and output formatting. The contents are string constants rather than test functions. The distinct line endings let callers select the matching fixture.
    - Tags: [crlf, rust, test-fixture, text]

- `json.rs` (Size : 12995 bytes): Tests the CLI's JSON Lines output by deserializing messages into typed begin, end, match, context, and summary variants. Cases check normal matches, replacements, quiet statistics, invalid UTF-8 byte encoding, and CRLF behavior. The structures reject unknown fields where declared, helping assertions validate the emitted schema. Test commands provide the JSON text consumed by the decoder.
    - Tags: [integration-tests, json, rust, serialization]

- `macros.rs` (Size : 1644 bytes): Defines `rgtest!`, which registers test functions and reruns them with the PCRE2 feature enabled, and output-comparison macros that report expected-versus-actual text. These macros are shared by the integration test modules. The comparison macros include both ordinary and debug-formatted output variants. Their failure message displays the expected and captured values.
    - Tags: [macros, rust, test-support]

- `misc.rs` (Size : 39815 bytes): Contains miscellaneous CLI tests for common searches, output formats, filtering and ignore rules, replacement, context, sorting, compressed input, and binary handling. Its opening comment says additions should generally go in the feature or regression suite instead. The tests use the shared Sherlock fixture and test helpers. Individual tests set up small directory trees and verify command results.
    - Tags: [cli, integration-tests, rust, search]

- `multiline.rs` (Size : 4123 bytes): Tests multiline search behavior, including overlapping matches, newline matching, dot-all mode, only-matching output, vimgrep formatting, stdin input, and context lines. The cases exercise ripgrep with the multiline option and compare exact results. Several cases use the shared Sherlock text fixture. The overlap tests create their own input text.
    - Tags: [integration-tests, multiline-search, rust, search]

- `regression.rs` (Size : 56506 bytes): Collects issue-referenced regression tests for search, path traversal, ignore and glob rules, output formats, regex behavior, and command exit statuses. Cases build minimal directories and assert results for previously reported edge cases, including platform-specific cases. Tests use the shared fixture and test-command helpers where needed. The source also records two unresolved TODO comments and two NOTE comments.
    - Tags: [integration-tests, regression-tests, rust, search]
    - TODO/FIXME/NOTE: line 179 — `TODO`; line 192 — `TODO`; line 574 — `Note`; line 1447 — `note`

- `tests.rs` (Size : 693 bytes): Declares the integration-test modules for shared macros, corpus, utilities, and the binary, feature, index, JSON, miscellaneous, multiline, and regression suites. The index suite is conditionally included when the `unstable-index` feature is enabled. Its comments describe the focus of several suites and indicate where new feature tests should go. It is the module entry point for these integration tests.
    - Tags: [integration-tests, rust, test-organization]

- `util.rs` (Size : 18504 bytes): Implements shared test helpers: temporary test directories, construction of ripgrep commands, input and output handling, assertions, line sorting, external-command checks, and cross-runner selection. `Dir` and `TestCommand` centralize setup and diagnostics for integration cases. The helper types provide methods for creating files and directories and configuring commands. Output failures include command, working-directory, and captured-output information.
    - Tags: [rust, test-support, utilities]
    - TODO/FIXME/NOTE: line 296 — `Note`
- `data/sherlock-nul.txt` (Size : 90314 bytes): A Study in Scarlet text corpus with an embedded NUL byte. `tests/binary.rs` loads it as bytes and uses it to check binary detection, NUL handling, and memory-mapped search behavior. The readable text includes the novel's opening and a NUL-bearing line. Its test role is directly identified in the source.
    - Tags: [binary-test-fixture, nul-byte, search-tests, text-corpus]
- `data/sherlock.Z` (Size : 286 bytes): Compressed binary test data with a `.Z` filename. The payload is not readable as text. `tests/misc.rs` includes it in a compressed-search test. Details beyond this test-fixture role are unknown.
    - Tags: [compressed-test-fixture, compression, search-tests]
- `data/sherlock.br` (Size : 186 bytes): Compressed binary test data with a Brotli-style `.br` filename. The payload is not readable as text. `tests/misc.rs` includes it in a compressed-search test. Details beyond this test-fixture role are unknown.
    - Tags: [compressed-test-fixture, compression, search-tests]
- `data/sherlock.bz2` (Size : 272 bytes): Compressed binary test data with a `.bz2` filename. The payload is not readable as text. `tests/misc.rs` includes it in a compressed-search test. Details beyond this test-fixture role are unknown.
    - Tags: [compressed-test-fixture, compression, search-tests]
- `data/sherlock.gz` (Size : 263 bytes): Compressed binary test data with a `.gz` filename. The payload is not readable as text. `tests/misc.rs` includes it in a compressed-search test. Details beyond this test-fixture role are unknown.
    - Tags: [compressed-test-fixture, compression, search-tests]
- `data/sherlock.lz4` (Size : 365 bytes): Compressed binary test data with a `.lz4` filename. The payload is not readable as text. `tests/misc.rs` includes it in a compressed-search test. Details beyond this test-fixture role are unknown.
    - Tags: [compressed-test-fixture, compression, search-tests]
- `data/sherlock.lzma` (Size : 286 bytes): Compressed binary test data with a `.lzma` filename. The payload is not readable as text. `tests/misc.rs` includes it in a compressed-search test. Details beyond this test-fixture role are unknown.
    - Tags: [compressed-test-fixture, compression, search-tests]
- `data/sherlock.xz` (Size : 332 bytes): Compressed binary test data with an `.xz` filename. The payload is not readable as text. `tests/misc.rs` includes it in preprocessing and compressed-search tests. Details beyond this test-fixture role are unknown.
    - Tags: [compressed-test-fixture, compression, search-tests]
- `data/sherlock.zst` (Size : 249 bytes): Compressed binary test data with a `.zst` filename. The payload is not readable as text. `tests/misc.rs` includes it in a compressed-search test. Details beyond this test-fixture role are unknown.
    - Tags: [compressed-test-fixture, compression, search-tests]
- `index/basic.rs` (Size : 193 bytes): Declares a basic index UX test module. Its comment states that it covers basic user interactions with an index. The module declaration points to the implementation in the separate `basic` test module. The file itself contains no additional test logic.
    - Tags: [indexing, integration-tests, rust, test-organization]
- `index/disallowed.rs` (Size : 4903 bytes): Tests command options that are rejected when indexing is enabled, including binary/text handling, encodings, engine selection, ignore controls, globbing, traversal, preprocessing, and unrestricted modes. Each case invokes ripgrep and checks for an error. The tested list is explicitly described as restrictions that may be lifted. Shared test helpers provide the command and temporary test directory.
    - Tags: [indexing, integration-tests, options, rust]
- `index/mod.rs` (Size : 226 bytes): Declares the index test modules and documents their roles: basic index interactions and currently disallowed features. It serves as the index test suite's module entry point. The declarations keep the cases separated by subject. The comments frame the disallowed-feature list as current behavior rather than a permanent restriction.
    - Tags: [indexing, integration-tests, rust, test-organization]

---

## Links Child Folder docmaps
None.
# Related Features

The root test modules cover CLI search and output behavior, binary detection, JSON output, multiline matching, and regressions. The child indexes detail the fixed input data and indexing-specific test coverage.

# Agent Guidance

## Read When

Changing ripgrep CLI behavior or locating integration coverage for search, output, filtering, binary handling, or regressions.

## Modify When

Adding or updating integration tests, shared fixtures, test macros, or test utilities.

## Avoid Modifying When

Changing implementation code without a test change, or editing child-folder fixtures when the change only affects test harness behavior.
