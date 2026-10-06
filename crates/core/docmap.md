---
folder: "crates/core"
generated_on: "2026-10-06"
num_files: 9
semantic_tags: [cli, command-dispatch, conditional-compilation, crate-documentation, error-reporting, feature-gating, file-traversal, filtering, indexing, logging, macros, matching, preprocessing, rust, search, streaming-io]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This folder contains the executable core of ripgrep: its entry point, command dispatch, traversal coordination, search orchestration, and user-facing messages. The core README describes it as the layer that defines the CLI and connects matcher, searcher, and printer crates. File selection is mediated by haystack wrappers and the ignore-aware walker, while flag parsing prepares runtime configuration. The flag and optional-index subsystems are documented in their own child maps.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

`main.rs` dispatches special modes, ordinary searches, file listing, type listing, and generated output, then maps results and errors to process exit codes. `search.rs` coordinates matcher, searcher, printer, preprocessors, and parallel workers. Supporting modules define candidate haystacks, logging, and conditional user-message/exit-error state.

## Technology Notes

The executable is implemented in Rust and composes the workspace's `grep`, `ignore`, and terminal-output facilities. Parallel traversal/search is used when configured; the optional index route is isolated under the index feature module.

# Folder Navigation

## Merged Child Folders
- `index/` —
  - Tags: [conditional-compilation, feature-gating, indexing, rust, search]. TODO/FIXME/NOTE: none.
  This folder selects the implementation of the optional search-index operations. Its module boundary keeps indexed-search behavior behind the `unstable-index` feature while providing a consistent interface to the rest of ripgrep core. The feature-disabled implementation reports that indexing is unavailable. The enabled implementation opens or writes an index and routes searches through the regular search workers.
## Files
- `README.md` (Size : 689 bytes): Describes the role of the ripgrep core crate, identifying `main.rs` as the executable entry point and summarizing the CLI definition and glue between matcher, searcher, and printer crates. It notes that core is not planned as an independent library and that reusable heavy lifting lives in constituent crates. Tags: [crate-documentation, rust, search].
- `haystack.rs` (Size : 5901 bytes): Wraps ignore-walker directory entries in `Haystack` and filters entries that should be searched. Explicitly supplied non-directory entries and stdin are retained, while implicitly discovered candidates must be files; walker errors are reported through the core message path. The builder can also strip a leading `./` from displayed paths. Tags: [file-traversal, filtering, rust, search]. TODO/FIXME/NOTE: NOTE line 128 (exact marker `note`).
- `logger.rs` (Size : 2196 bytes): Implements a small `log::Log` backend that writes records to stderr with available target, file, and line metadata. It relies on the global maximum log level for filtering and initializes itself as the process-wide logger. Tags: [logging, rust].
- `main.rs` (Size : 19170 bytes): Implements the process entry point and dispatches parsed arguments to search, indexed search, file listing, type listing, or generated output. It selects sequential or parallel traversal based on thread settings, handles broken pipes gracefully, and derives exit status from matches and accumulated non-fatal errors. Tags: [cli, command-dispatch, file-traversal, rust, search]. TODO/FIXME/NOTE: NOTE line 436 (exact marker `Note`).
- `messages.rs` (Size : 5182 bytes): Defines atomic process-wide switches for ordinary and ignore-related messages and tracks whether a non-fatal error occurred. Its macros serialize stderr output against stdout writes and update error state so the executable can choose an exit code. Tags: [error-reporting, logging, macros, rust]. TODO/FIXME/NOTE: NOTE line 121 (exact marker `Note`).
- `search.rs` (Size : 16364 bytes): Defines the search-worker builder and worker that connect a pattern matcher, searcher, and printer. It handles file-level preprocessing and decompression before passing content to the searcher, and provides the per-path and reader search routines used by core execution. Tags: [matching, preprocessing, rust, search, streaming-io]. TODO/FIXME/NOTE: NOTE line 121 (exact marker `Note`).
- `index/disabled.rs` (Size : 329 bytes): Supplies the feature-disabled implementations of index writing and reading. Both return an error stating that indexing is not enabled in the current ripgrep build, preserving the common function signatures. Tags: [feature-gating, indexing, rust].
- `index/enabled.rs` (Size : 450 bytes): Supplies the feature-enabled index operations by opening the requested index for writes or reads. After opening for reading, it performs an exhaustive search, choosing the single-threaded or parallel implementation according to the configured thread count. Tags: [indexing, rust, search].
- `index/mod.rs` (Size : 178 bytes): Re-exports the selected implementation through a private `imp` module. A compile-time `cfg` and explicit module paths select `disabled.rs` by default or `enabled.rs` when `unstable-index` is active. Tags: [conditional-compilation, feature-gating, rust].
---

## Links Child Folder docmaps
- `flags/docmap.md` — Definitions and parsing of ripgrep CLI flags, conversion into runtime configuration, and child indexes for documentation and completions.
# Related Features

Ripgrep command execution, file traversal, search and output coordination, command-line parsing, and optional index use.

# Agent Guidance

## Read When

Changing top-level CLI behavior, traversal or search dispatch, candidate-file selection, message handling, or integration of the core search components.

## Modify When

The change affects the executable's coordination of parsing, walking, searching, output, or exit status.

## Avoid Modifying When

The change is isolated to a reusable matcher, printer, walker, or CLI utility crate and does not affect core orchestration.

## Dependency Graph

Not generated.
