---
folder: "crates/searcher/src"
generated_on: "2026-10-06"
num_files: 10
semantic_tags: [binary-detection, file-input, line-buffering, line-search, memory-mapping, rust, search, search-configuration, searcher, searcher-api, search-events, sink, sinks]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This folder defines the searcher crate's public API and core supporting modules. `lib.rs` exposes the searcher, sink, line iteration, and configuration types, while line buffering and sink modules support the data path and result callbacks. Tests use the local matcher and assertion utilities in `testutil.rs` and `macros.rs`. The child folder `searcher` contains the search execution core, dispatch, and memory-map policy.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

Provide public searcher and sink types, iterate through lines, buffer input, and supply shared test support. The nested execution folder owns the detailed search strategies.

## Technology Notes

The source is Rust and uses byte-oriented search types from `bstr` and `grep-matcher`, plus standard I/O and encoding-aware search components.

# Folder Navigation

## Merged Child Folders
- `searcher/` —
  This folder implements the internal engines behind the public `Searcher` API. A core component tracks offsets, line numbers, context, match counts, and binary status while delivering events to a sink. Glue code selects and coordinates line-by-line or multiline search over buffered, slice, and reader inputs. The mmap module controls whether file-backed memory maps are considered for a search.
## Files
- `lib.rs` (Size : 3824 bytes): Documents the searcher's role in applying a matcher to input and pushing match, context, and lifecycle results to a sink. It describes line- and multiline-search responsibilities and gives a `Searcher`/`UTF8` example. The public API re-exports searcher configuration, sink types, and line iterators. Private modules separate buffering, line processing, search execution, sink behavior, and tests.
    - Tags: [crate-api, documentation, rust, search]
- `line_buffer.rs` (Size : 36153 bytes): Implements buffered byte input for line-oriented processing, including configurable capacity, long-line allocation policy, and binary-data handling. Its reader/buffer abstractions track offsets and expose line-oriented data to search execution. Binary behavior can be disabled, terminate reads, or convert a selected byte to the configured line terminator. The module also reports allocation-limit and read errors to its callers.
    - Tags: [binary-detection, buffering, io, rust]
    - TODO/FIXME/NOTE: line 177: `    /// Note that this setting only applies to the amount of *additional*`
    - TODO/FIXME/NOTE: line 249: `    /// returned. (Note that if this line buffer's binary detection is set to`
    - TODO/FIXME/NOTE: line 399: `    /// returned. (Note that if this line buffer's binary detection is set to`
- `lines.rs` (Size : 16928 bytes): Defines `LineIter` for borrowed iteration over lines and `LineStep` for explicit stepping through byte ranges without retaining a borrow. Both treat a terminator as part of its line and yield non-empty ranges. `LineStep` advances through a supplied slice and can return ranges or matcher `Match` values. These types are re-exported by `lib.rs` for use by searchers and callers.
    - Tags: [byte-processing, line-iteration, rust]
- `macros.rs` (Size : 764 bytes): Defines the test-only `assert_eq_printed!` macro for comparing expected and actual output. It optionally accepts a label and includes both rendered values in a delimited panic message when they differ. Conditional compilation restricts it to test builds. Searcher tests use it to make output mismatches readable.
    - Tags: [macro, rust, testing]
- `sink.rs` (Size : 23786 bytes): Defines `Sink`, the callback interface through which a searcher reports matches, contextual lines, search start/finish, and gaps. `SinkError` converts I/O, configuration, and displayable errors into the sink's error type; `SinkMatch`, context, and finish values carry event data. Convenience sink adapters support simpler closure-based uses. The search execution modules drive these callbacks using a push model.
    - Tags: [callbacks, rust, search, sink]
    - TODO/FIXME/NOTE: line 356: ``    /// Note that since this is an absolute byte offset, it cannot be relied``
    - TODO/FIXME/NOTE: line 607: `                // TODO: In theory, it should be possible to amortize`
- `testutil.rs` (Size : 28365 bytes): Provides test-only matcher and sink utilities used to exercise searcher behavior. Its local regex matcher can configure line terminators and candidate-line behavior to test optimized and fallback search paths. Additional helpers support test input, expected events, and failure diagnostics. It is included only under test configuration from `lib.rs`.
    - Tags: [matcher, rust, test-support]
    - TODO/FIXME/NOTE: line 313: `    /// Note that in order to see these in tests that aren't failing, you'll`
    - TODO/FIXME/NOTE: line 465: `    /// Note that this must account for whether the test is using multi line`
- `searcher/core.rs` (Size : 23699 bytes): Implements `Core`, the shared state machine used while searching. It maintains matcher and sink state, offsets, line numbering, context windows, binary data status, match state, and counts. It reports lifecycle, match, contextual, and binary events through the sink interface. The line-oriented and multiline glue engines use this core.
    - Tags: [line-buffering, rust, searcher, search-events]
    - TODO/FIXME/NOTE: FIXME line 683 (exact marker `FIXME`)
- `searcher/glue.rs` (Size : 51498 bytes): Coordinates concrete search strategies, including buffered line-by-line reading, slice-based searching, and multiline processing. The strategy structs connect line buffers, line stepping, matchers, and the shared `Core`. They advance input while preserving offsets and context and handle binary-detection transitions. This module is the execution bridge between the public searcher configuration and the core event processor.
    - Tags: [line-search, rust, searcher, sinks]
    - TODO/FIXME/NOTE: NOTE line 238 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 743 (exact marker `Note`)
- `searcher/mmap.rs` (Size : 4578 bytes): Defines `MmapChoice`, which controls whether search may use a file-backed memory map. The default and `never` choice disable mapping, while the unsafe `auto` choice enables a heuristic that may consider platform and file size. If mapping cannot be used or is not considered advantageous, callers can fall back to ordinary reads. The module documents that the caller must uphold the safety assumption that the mapped file will not be mutated.
    - Tags: [file-input, memory-mapping, rust, searcher]
- `searcher/mod.rs` (Size : 42256 bytes): Defines public searcher configuration and execution entry points, including `Searcher`, `SearcherBuilder`, encoding configuration, and binary-detection behavior. It describes input-specific detection semantics and re-exports the `MmapChoice` policy from `mmap.rs`. Search operations dispatch to the line or multiline implementations in `glue.rs`, which use the `Core` in `core.rs`. Its API combines matching, I/O, decoding, buffering, and sink reporting.
    - Tags: [line-search, rust, search-configuration, searcher]
    - TODO/FIXME/NOTE: NOTE line 578 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 882 (exact marker `Note`)

---

## Links Child Folder docmaps
None.
# Related Features

Searcher public APIs, buffered line input, line iteration, sink callbacks, and test support.

# Agent Guidance

## Read When

Changing searcher API types, line buffering, line iteration, sink callbacks, or shared tests.

## Modify When

Implementing search input or result handling behavior that spans the public interfaces or their shared support modules.

## Avoid Modifying When

The requested change is isolated to one of the execution strategies in `searcher/docmap.md`.
