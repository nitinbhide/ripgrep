---
folder: "crates/ignore"
generated_on: "2026-10-06"
num_files: 19
semantic_tags: [api, bom-handling, cargo, crate-manifest, default-types, directory-matching, directory-traversal, directory-walking, documentation, error-handling, example, file-filtering, filename-matching, file-types, gitignore, glob-matching, ignore-crate, ignore-overrides, ignore-rules, incremental-matching, integration-tests, license, licensing, mit, parallelism, path-filtering, path-normalization, public-domain, regression-tests, rust, terms, test-fixture, test-fixtures, testing, unlicense, usage-example, utf-8, walker, whitelist]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This crate provides Rust APIs for matching ignore rules and for walking directory trees while honoring those rules. Its README describes filtering based on ignore files, globs, and file types, with lower-level matcher APIs available alongside the walker. `Cargo.toml` records the crate's Rust package settings and traversal, glob, and matching dependencies. The package includes a basic walker example and dual-license notices.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

The package root documents installation and the public traversal use case; detailed implementations and tests are indexed in child folders. The `examples` folder demonstrates basic walking, and `src` contains the ignore matching and traversal implementation. The `tests` folder covers gitignore ancestor matching and byte-order-mark handling.

## Technology Notes

The package is implemented in Rust and built with Cargo. Its documentation describes `.ignore` and `.gitignore` behavior; the manifest includes `walkdir`, `globset`, and regex-automata-based matching components.

# Folder Navigation

## Merged Child Folders
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
- `Cargo.toml` (Size : 1281 bytes): Declares the `ignore` Rust package, its version, description, workspace edition, and Rust version requirement. It lists glob matching, traversal, logging, file identity, and regex-automata dependencies, including a Windows-specific helper. Development dependencies support byte strings and channels. The manifest declares a deprecated no-op SIMD feature.
    - Tags: [cargo, crate-manifest, ignore-rules, rust]

- `COPYING` (Size : 129 bytes): States that the package is dual-licensed under the Unlicense and MIT licenses. It permits use under either license. The file serves as the package-level license selector. Full license terms are in the adjacent license files.
    - Tags: [license, licensing, terms]

- `LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License and identifies Andrew Gallant's 2015 copyright. It permits use, copying, modification, distribution, and sublicensing when the notice and permission text are retained. The terms provide the software without warranty and disclaim liability. This is one of the two licensing options named by the package.
    - Tags: [license, mit, terms]

- `README.md` (Size : 1712 bytes): Introduces `ignore` as a fast recursive directory iterator that respects filters such as globs, file types, and `.gitignore` rules. It links to docs.rs, provides a Cargo dependency example, and shows a basic walk that handles entries and errors. A second example demonstrates disabling the default hidden-file filtering through `WalkBuilder`. The README directs readers to `WalkBuilder` documentation for additional options.
    - Tags: [documentation, gitignore, rust, usage-example, walker]

- `UNLICENSE` (Size : 1235 bytes): Publishes the software into the public domain and permits use, modification, compilation, sale, and distribution. It describes the dedication of copyright interest and supplies an as-is warranty and liability disclaimer. The file is the Unlicense option named by the package's dual-license notice. It includes a pointer to the Unlicense website.
    - Tags: [license, public-domain, unlicense]
- `examples/walk.rs` (Size : 1817 bytes): Reads command-line arguments to choose a path and a traversal mode. It demonstrates standard `ignore::Walk`, six-thread `WalkBuilder::build_parallel`, and direct `walkdir::WalkDir` iteration. Results are sent through a bounded channel and written as lossy path bytes by a buffered stdout thread. A local enum adapts both crates' directory-entry types to a common path accessor.
    - Tags: [directory-traversal, example, ignore-crate, rust]
- `src/default_types.rs` (Size : 13899 bytes): Defines the crate's sorted built-in file-type names and their filename globs. The table covers many language, document, build, configuration, and data formats and is consumed by `TypesBuilder::add_defaults`. Aliases can map multiple names to the same extension patterns. The file also contains tests for representative default definitions.
    - Tags: [default-types, filename-matching, file-types, rust]
    - TODO/FIXME/NOTE: NOTE line 207 (exact marker `note`)
- `src/dir.rs` (Size : 59980 bytes): Implements the internal hierarchical `Ignore` matcher used by the walker. It builds child matchers from directory-local `.ignore`, `.gitignore`, custom ignore files, Git exclude files, and parent/global sources, retaining parent relationships and caching compiled directory matchers. Matching combines override globs, ignore-file rules, file-type selection, and hidden-entry checks according to precedence. The module also handles partial errors, Git worktree metadata, and internal builder configuration.
    - Tags: [directory-matching, gitignore, ignore-rules, rust]
    - TODO/FIXME/NOTE: NOTE line 119 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 190 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 267 (exact marker `Note`)
- `src/gitignore.rs` (Size : 33217 bytes): Implements Git-compatible parsing and matching for ignore-file globs without invoking the Git command-line program. `GitignoreBuilder` reads files or individual lines, compiles globs, and preserves partial errors; `Gitignore` matches paths and can check ancestors. The module also discovers global exclude-file locations from Git configuration and environment settings. Its tests exercise parsing, precedence, and matching details.
    - Tags: [gitignore, glob-matching, ignore-rules, rust]
    - TODO/FIXME/NOTE: NOTE line 5 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 101 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 217 (exact marker `NOTE`)
    - TODO/FIXME/NOTE: NOTE line 332 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 374 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 402 (exact marker `Note`)
    - TODO/FIXME/NOTE: TODO line 553 (exact marker `TODO`)
    - TODO/FIXME/NOTE: NOTE line 582 (exact marker `Note`)
- `src/incremental.rs` (Size : 49383 bytes): Implements `IncrementalIgnore`, a matcher built from `WalkBuilder` configuration for checking individual root-relative paths. It lazily loads matchers for directory ancestors and caches allowed or ignored directories so repeated path checks can reuse that state. Results report ignore, whitelist, descent, and depth-filter status, with a second API for returning load errors. Its documentation notes that this snapshot-based interface is intended for sparse updates rather than full directory traversal.
    - Tags: [ignore-rules, incremental-matching, path-filtering, rust]
    - TODO/FIXME/NOTE: NOTE line 146 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 150 (exact marker `Note`)
- `src/lib.rs` (Size : 19177 bytes): Defines the crate-level `Error` and generic `Match` types and their supporting conversions and formatting. It declares the internal traversal, matching, and utility modules while publicly exposing the gitignore, override, and file-type modules. The crate root re-exports the walker and incremental matcher APIs. Its tests cover shared error and match behavior.
    - Tags: [api, error-handling, ignore-crate, rust]
- `src/overrides.rs` (Size : 10336 bytes): Provides public override-glob matchers and a builder for include/exclude-style patterns. It adapts gitignore glob parsing while reversing the interpretation of leading `!` for override semantics. A whitelist set treats nonmatching files as ignored, and the builder controls case sensitivity and unclosed character classes. Unit tests cover empty sets and matching behavior.
    - Tags: [glob-matching, ignore-overrides, rust, whitelist]
    - TODO/FIXME/NOTE: NOTE line 20 (exact marker `Note`)
    - TODO/FIXME/NOTE: TODO line 157 (exact marker `TODO`)
- `src/pathutil.rs` (Size : 4961 bytes): Contains internal path helpers used by matching and traversal. It determines hidden paths, with Windows attribute checks in addition to dot-prefixed names, and implements platform-aware prefix stripping and filename extraction. It also determines whether a path is a single filename. Unix-specific code works on encoded path bytes where needed.
    - Tags: [path-filtering, path-normalization, rust]
- `src/types.rs` (Size : 20424 bytes): Implements file-type definitions and a matcher that selects or negates groups of filename globs. `TypesBuilder` adds custom definitions, includes existing type definitions, adds defaults, and validates selections before compiling a `GlobSet`. The matcher reports whitelisted, ignored, or unmatched paths and uses pooled temporary match storage. Module documentation includes examples for defaults, negation, and custom type definitions.
    - Tags: [file-types, glob-matching, ignore-rules, rust]
    - TODO/FIXME/NOTE: NOTE line 10 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 61 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 103 (exact marker `Note`)
- `src/walk.rs` (Size : 96183 bytes): Implements directory entry types, walker configuration, sequential iteration, and parallel traversal. `WalkBuilder` configures roots, ignore sources, depth and size limits, link handling, sorting, filters, and matcher construction; `Walk` yields filtered entries using the hierarchical ignore matcher. `WalkParallel` distributes directory work to worker threads and invokes per-thread visitors that can continue, skip descent, or stop the walk. The module also handles traversal errors, symlink loops, file-system boundaries, stdout avoidance, and platform-specific entry metadata.
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
None.
# Related Features

Ignore-file matching, file-type and glob filtering, and sequential or parallel recursive directory traversal.

# Agent Guidance

## Read When

Working on the `ignore` crate's package API, traversal options, filtering behavior, or tests.

## Modify When

Changing crate metadata, documented usage, or the example of configuring a walker.

## Avoid Modifying When

Changing ripgrep's search orchestration or grep output formatting; those concerns are in other crates.
