---
folder: "crates/ignore"
generated_on: "2026-11-07"
num_files: 21
semantic_tags: [api, benchmark-harness, benchmarking, benchmark-methodology, bom-handling, cargo, crate-manifest, default-types, directory-matching, directory-traversal, directory-walking, documentation, error-handling, example, file-filtering, filename-matching, filesystem-fixtures, file-types, gitignore, glob-matching, ignore-crate, ignore-overrides, ignore-rules, incremental-matching, integration-tests, license, licensing, mit, parallelism, path-filtering, path-normalization, public-domain, python-workloads, regression-tests, rust, terms, test-fixture, test-fixtures, testing, unlicense, usage-example, utf-8, walker, whitelist]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This crate provides Rust APIs for matching ignore rules and for walking directory trees while honoring those rules. Its README describes filtering based on ignore files, globs, and file types, with lower-level matcher APIs available alongside the walker. `Cargo.toml` records the crate's Rust package settings and traversal, glob, and matching dependencies. The package includes a basic walker example and dual-license notices. The `benches` folder documents and implements performance workloads for traversal and incremental matching, indexed inline below.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

The package root documents installation and the public traversal use case; detailed implementations and tests are indexed in child folders. The `examples` folder demonstrates basic walking, and `src` contains the ignore matching and traversal implementation. The `tests` folder covers gitignore ancestor matching and byte-order-mark handling. The standalone `benches` folder contains workloads for directory discovery and incremental ignore matching.

## Technology Notes

The package is implemented in Rust and built with Cargo. Its documentation describes `.ignore` and `.gitignore` behavior; the manifest includes `walkdir`, `globset`, and regex-automata-based matching components. The benchmark harness uses Rust's nightly test harness.

# Folder Navigation

## Merged Child Folders
- `benches/` —
  - Tags: [benchmark-harness, benchmark-methodology, benchmarking, directory-traversal, filesystem-fixtures, gitignore, ignore-crate, incremental-matching, parallelism, python-workloads, rust, testing]. TODO/FIXME/NOTE: none.
  This folder documents and implements performance benchmarks for directory discovery and incremental ignore matching in the `ignore` crate. The workloads model file-discovery and indexing operations described for Python development tools, including Ruff, ty, and uv. Synthetic project trees exercise variations in package layout, ignore rules, and traversal configuration. The benchmarks measure crate operations rather than end-to-end application performance.
  Major responsibilities: `benches/README.md` explains the benchmark scenarios, fixture assumptions, and comparison methodology. `benches/workloads.rs` creates and removes deterministic filesystem fixtures, runs serial and parallel walks, and measures matcher construction and cached path checks. Assertions verify expected Python-file counts or match outcomes before and during timed iterations.
  Technology notes: The benchmark harness is Rust code using the nightly `test` harness and the `ignore` crate's walker and matcher APIs. It creates filesystem fixtures locally and models ignore behavior with `.ignore`, `.gitignore`, and Git exclude rules.
  Related features: This folder supports performance evaluation of the ignore-aware directory traversal and incremental path-matching capabilities described in `docmap.md`. Its benchmark scenarios focus on configurations and workloads associated with Python project discovery.
  Read when: Read these files when evaluating traversal or ignore-matching performance, selecting a benchmark workload, or interpreting benchmark comparisons.
  Modify when: Modify `benches/workloads.rs` when adding or adjusting a measured workload or its synthetic fixtures; update `benches/README.md` when benchmark coverage or measurement guidance changes.
  Avoid modifying when: Avoid changing these benchmark files for functional changes to ignore matching or traversal; those implementations are indexed in the crate's `src` section.

- `examples/` —
  - Tags: [directory-traversal, example, ignore-crate, rust]. TODO/FIXME/NOTE: none.
  This folder demonstrates using the `ignore` crate to traverse a directory tree. Its example accepts a root path and supports ordinary sequential walking as well as parallel walking. A third mode uses `walkdir` directly for comparison. All modes emit the discovered entry paths through a buffered stdout thread.
- `src/` —
  - Tags: [api, default-types, directory-matching, directory-traversal, error-handling, filename-matching, file-types, gitignore, glob-matching, ignore-crate, ignore-overrides, ignore-rules, incremental-matching, parallelism, path-filtering, path-normalization, rust, walker, whitelist]. TODO/FIXME/NOTE: present; see indexed files.
  This folder implements the crate's ignore-aware traversal and path-filtering behavior. It combines hierarchical `.ignore` and gitignore matchers, override globs, file-type selections, hidden-path checks, and path utilities. `walk.rs` exposes sequential and parallel traversal, while `incremental.rs` provides cached path matching for callers that do not want to traverse a full tree. The modules use shared matcher state and directory ancestry to apply filtering in precedence order.
- `tests/` —
  - Tags: [bom-handling, gitignore, ignore-rules, integration-tests, rust, test-fixture, testing, utf-8]. TODO/FIXME/NOTE: none.
  This folder contains integration tests and fixture files for gitignore matching behavior. One test exercises path-or-parent matching over root and nested file and directory cases. Another verifies that a UTF-8 byte-order mark at the start of an ignore file is skipped. The fixtures encode the expected pattern rules used by these tests.
## Files
- `Cargo.toml` (Size : 1203 bytes): Declares the `ignore` Rust package, version, description, workspace edition, and Rust 1.88 minimum. It lists glob matching, traversal, logging, file identity, regex-automata, and Windows-specific dependencies; development dependencies support byte strings and channels. The manifest also declares the deprecated no-op `simd-accel` feature.
    - Tags: [cargo, crate-manifest, ignore-rules, rust]

- `COPYING` (Size : 129 bytes): States that the package is dual-licensed under the Unlicense and MIT licenses. It permits use under either license. The file serves as the package-level license selector. Full license terms are in the adjacent license files.
    - Tags: [license, licensing, terms]

- `LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License and identifies Andrew Gallant's 2015 copyright. It permits use, copying, modification, distribution, and sublicensing when the notice and permission text are retained. The terms provide the software without warranty and disclaim liability. This is one of the two licensing options named by the package.
    - Tags: [license, mit, terms]

- `README.md` (Size : 1712 bytes): Introduces `ignore` as a fast recursive directory iterator that respects filters such as globs, file types, and `.gitignore` rules. It links to docs.rs, provides a Cargo dependency example, and shows a basic walk that handles entries and errors. A second example demonstrates disabling the default hidden-file filtering through `WalkBuilder`. The README directs readers to `WalkBuilder` documentation for additional options.
    - Tags: [documentation, gitignore, rust, usage-example, walker]

- `UNLICENSE` (Size : 1235 bytes): Publishes the software into the public domain and permits use, modification, compilation, sale, and distribution. It describes the dedication of copyright interest and supplies an as-is warranty and liability disclaimer. The file is the Unlicense option named by the package's dual-license notice. It includes a pointer to the Unlicense website.
    - Tags: [license, public-domain, unlicense]
- `benches/README.md` (Size : 5932 bytes): Documents the workspace-discovery benchmark suite and maps its workloads to file-discovery and indexing operations used by Ruff, ty, and uv. It describes synthetic project layouts and the traversal, ignore-rule, and incremental-matching cases they exercise. It explains fixture setup, count checks, warm-cache measurement, and the exclusion of parsing and other application work from the measurements. It also gives nightly Cargo benchmark commands and guidance for comparable runs, including compiler settings, CPU affinity, and focused cases.
    - Tags: [benchmark-methodology, benchmarking, directory-traversal, ignore-crate, incremental-matching, python-workloads, rust, testing]

- `benches/workloads.rs` (Size : 19316 bytes): Implements nightly Rust benchmarks for the `ignore` crate's directory walking and incremental path matching. Its `Workspace` fixture builds synthetic Python project trees with configurable package counts, nesting, file counts, and ignore rules, then removes each tree after use. Benchmarks cover serial and parallel traversal, explicit and multiple roots, ignored workspace members, matcher construction, cold and cached matching, and configured glob or file-type filters. The harness checks expected file counts and match results, and measures crate operations without invoking the Python tools whose use cases the scenarios model.
    - Tags: [benchmark-harness, directory-traversal, filesystem-fixtures, gitignore, ignore-crate, incremental-matching, parallelism, rust]

- `examples/walk.rs` (Size : 1817 bytes): Reads command-line arguments to choose a path and a traversal mode. It demonstrates standard `ignore::Walk`, six-thread `WalkBuilder::build_parallel`, and direct `walkdir::WalkDir` iteration. Results are sent through a bounded channel and written as lossy path bytes by a buffered stdout thread. A local enum adapts both crates' directory-entry types to a common path accessor.
    - Tags: [directory-traversal, example, ignore-crate, rust]
- `src/default_types.rs` (Size : 13899 bytes): Defines the crate's sorted built-in file-type names and their filename globs. The table covers many language, document, build, configuration, and data formats and is consumed by `TypesBuilder::add_defaults`. Aliases can map multiple names to the same extension patterns. The file also contains tests for representative default definitions.
    - Tags: [default-types, filename-matching, file-types, rust]
    - TODO/FIXME/NOTE: NOTE line 207 (exact marker `note`)
- `src/dir.rs` (Size : 63562 bytes): Implements the walker's persistent, directory-hierarchical `Ignore` matcher. It creates child matchers from local and parent `.ignore`/`.gitignore` rules, custom ignore files, Git excludes, global sources, and shared override and file-type matchers; compiled parent matchers are cached for reuse. Matching applies those sources with the crate's precedence rules and accounts for hidden paths. The module also handles partial errors, Git worktree metadata, and internal builder configuration.
    - Tags: [directory-matching, gitignore, ignore-rules, rust]
    - TODO/FIXME/NOTE: NOTE line 119 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 193 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 267 (exact marker `Note`)
- `src/gitignore.rs` (Size : 33308 bytes): Implements Git-compatible parsing and matching for ignore-file globs without invoking the Git command-line program. `GitignoreBuilder` reads files or lines, compiles glob sets, and preserves valid rules alongside partial errors; `Gitignore` matches paths and can test each ancestor up to its root. The module also handles BOM-prefixed files and discovers global exclude-file locations from Git configuration and environment settings. Its tests cover parsing, precedence, and matching behavior.
    - Tags: [gitignore, glob-matching, ignore-rules, rust]
    - TODO/FIXME/NOTE: NOTE line 5 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 101 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 217 (exact marker `NOTE`)
    - TODO/FIXME/NOTE: NOTE line 332 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 377 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 405 (exact marker `Note`)
    - TODO/FIXME/NOTE: TODO line 556 (exact marker `TODO`)
    - TODO/FIXME/NOTE: NOTE line 585 (exact marker `Note`)
- `src/incremental.rs` (Size : 52787 bytes): Implements `IncrementalIgnore`, a matcher built from `WalkBuilder` configuration for checking individual root-relative paths without walking the whole tree. It lazily loads ignore matchers as paths are checked and caches allowed or ignored directories for repeated queries. `normalize` optionally converts absolute paths to root-relative form, while matching reports ignore, whitelist, depth, and descent status and can return load errors. The matcher snapshots each directory's ignore files when first loaded, so callers must rebuild it to observe later edits.
    - Tags: [ignore-rules, incremental-matching, path-filtering, rust]
    - TODO/FIXME/NOTE: NOTE line 189 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 193 (exact marker `Note`)
- `src/lib.rs` (Size : 19177 bytes): Defines the crate-level `Error` and generic `Match` types and their supporting conversions and formatting. It declares the internal traversal, matching, and utility modules while publicly exposing the gitignore, override, and file-type modules. The crate root re-exports the walker and incremental matcher APIs. Its tests cover shared error and match behavior.
    - Tags: [api, error-handling, ignore-crate, rust]
- `src/overrides.rs` (Size : 10336 bytes): Provides public override-glob matchers and a builder for include/exclude-style patterns. It adapts gitignore glob parsing while reversing the interpretation of leading `!` for override semantics. A whitelist set treats nonmatching files as ignored, and the builder controls case sensitivity and unclosed character classes. Unit tests cover empty sets and matching behavior.
    - Tags: [glob-matching, ignore-overrides, rust, whitelist]
    - TODO/FIXME/NOTE: NOTE line 20 (exact marker `Note`)
    - TODO/FIXME/NOTE: TODO line 157 (exact marker `TODO`)
- `src/pathutil.rs` (Size : 6591 bytes): Provides internal path utilities shared by ignore matching and traversal. It detects hidden paths and directory entries, checking the Windows hidden attribute as well as dot-prefixed names on Windows and dot-prefixed names elsewhere. It also strips path prefixes, detects bare filenames, and extracts the final normal path component. Unix implementations use encoded path bytes, with tests for dot components and trailing-dot names.
    - Tags: [path-filtering, path-normalization, rust]
- `src/types.rs` (Size : 20424 bytes): Implements file-type definitions and a matcher that selects or negates groups of filename globs. `TypesBuilder` adds custom definitions, includes existing type definitions, adds defaults, and validates selections before compiling a `GlobSet`. The matcher reports whitelisted, ignored, or unmatched paths and uses pooled temporary match storage. Module documentation includes examples for defaults, negation, and custom type definitions.
    - Tags: [file-types, glob-matching, ignore-rules, rust]
    - TODO/FIXME/NOTE: NOTE line 10 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 61 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 103 (exact marker `Note`)
- `src/walk.rs` (Size : 97323 bytes): Implements directory entries, walker configuration, sequential iteration, and parallel traversal. `WalkBuilder` configures roots, ignore sources, depth and size limits, link handling, sorting, and filters; it can build a `Walk`, a parallel walker, or per-root `IncrementalIgnore` matchers. `Walk` yields filtered entries through the hierarchical ignore matcher, while `WalkParallel` distributes work to worker threads and calls per-thread visitors that can continue, skip descent, or stop. The module also handles traversal errors, symlink loops, file-system boundaries, stdout avoidance, and platform-specific entry metadata.
    - Tags: [directory-traversal, parallelism, rust, walker]
    - TODO/FIXME/NOTE: NOTE line 457 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 469 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 549 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 558 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 580 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 698 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 769 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 785 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 972 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 991 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1040 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1043 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1131 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1141 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1333 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1459 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1589 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1720 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1731 (exact marker `Note`)
- `tests/gitignore_matched_path_or_any_parents_tests.gitignore` (Size : 2569 bytes): Supplies gitignore patterns annotated with expected match or no-match cases. Its sections cover root-level and nested files and directories, including rooted patterns, wildcards, and `**` forms. The companion Rust integration test uses these rules to verify direct and ancestor matching. Comments in the fixture make the intended test cases readable alongside the assertions.
    - Tags: [gitignore, ignore-rules, test-fixture]
- `tests/gitignore_matched_path_or_any_parents_tests.rs` (Size : 12814 bytes): Builds a `Gitignore` matcher from the companion fixture and tests `matched_path_or_any_parents`. The assertions cover root and nested files, directories, and descendants across positive and negative pattern cases. A separate test asserts that passing a path outside the configured root panics with the documented message. The suite validates parent-directory matching behavior.
    - Tags: [gitignore, integration-tests, rust, testing]
- `tests/gitignore_skip_bom.gitignore` (Size : 61 bytes): Begins with a UTF-8 byte-order mark and then contains a rule that ignores `ignore/this/path`. The leading marker is intentional test input rather than formatting noise. The companion regression test loads this fixture through `GitignoreBuilder`. It verifies compatibility with Git's handling of a BOM-prefixed ignore file.
    - Tags: [gitignore, test-fixture, utf-8]
- `tests/gitignore_skip_bom.rs` (Size : 585 bytes): Defines a regression test that loads the BOM-prefixed ignore fixture with `GitignoreBuilder`. It asserts that the fixture opens without an error and that the configured path is ignored after building the matcher. The test documents the expected Git-compatible BOM behavior. It references the neighboring `.gitignore` file by path.
    - Tags: [bom-handling, gitignore, integration-tests, rust]

---

## Links Child Folder docmaps
# Related Features

Ignore-file matching, file-type and glob filtering, and sequential or parallel recursive directory traversal.

# Agent Guidance

## Read When

Working on the `ignore` crate's package API, traversal options, filtering behavior, or tests.

## Modify When

Changing crate metadata, documented usage, or the example of configuring a walker.

## Avoid Modifying When

Changing ripgrep's search orchestration or grep output formatting; those concerns are in other crates.
