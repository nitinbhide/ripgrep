---
folder: "crates/searcher"
generated_on: "2026-11-07"
num_files: 15
semantic_tags: [cargo, crate-manifest, documentation, example, license, line-search, mit, public-domain, rust, search, searcher, stdin, unlicense]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose

This crate provides a high-level library for fast line-oriented searches, with optional multiline searches. Its `Searcher` applies a generic matcher to input and pushes match, context, and lifecycle events to a caller-provided sink. The crate handles search concerns such as line counting, binary detection, encoding, and memory-map selection. Its Rust implementation is indexed in `src`, while `examples` contains a runnable stdin search sample.
  Additional absorbed index summary:
  This folder contains the `grep-searcher` Rust library package, its usage documentation, a stdin example, and license texts. The public API centers on `Searcher`, which applies a caller-provided matcher to files, readers, or byte slices and reports search events through a sink. Its implementation supports line-oriented and multiline search, buffering, context, binary detection, encoding, and optional memory mapping. The crate's API and implementation modules are indexed in the source map.
Absorbed folder summaries and file entries are retained inline below.
  Major responsibilities: Provide configurable search execution and the sink interface for receiving matches, context, and lifecycle events. Supporting modules handle line iteration and buffered input, while test utilities exercise search modes and output behavior.
  Technology notes: The package is Rust crate `grep-searcher`, built with Cargo in the workspace. Its runtime dependencies include `grep-matcher`, `bstr`, `encoding_rs`, `encoding_rs_io`, `memchr`, `memmap2`, and `log`; its development dependencies include `grep-regex` and `regex`.
  - Tags: [binary-detection, buffering, byte-processing, callbacks, cargo, command-line, crate-api, documentation, example, file-input, io, library, license, line-buffering, line-iteration, line-search, macro, matcher, memory-mapping, mit, public-domain, rust, search, search-configuration, searcher, searcher-api, search-events, sink, sinks, standard-input, testing, test-support, usage, workspace-manifest]. TODO/FIXME/NOTE: present; see indexed files.

# Folder Navigation

## Merged Child Folders

- `examples/` —
  - Tags: [example, rust, search, stdin]. TODO/FIXME/NOTE: none.
  This folder demonstrates using `grep-searcher` to search standard input. The example accepts a regular-expression pattern from the command line and constructs a regex matcher. It sends matching UTF-8 lines to a sink closure that prints line numbers and contents. This provides a compact usage example for the crate's search-reader API.

## Files

- `Cargo.toml` (Size : 995 bytes): Declares the `grep-searcher` package and its workspace Rust settings. Runtime dependencies provide byte handling, encoding, matcher integration, logging, byte searching, and memory mapping; development dependencies add regex-backed testing support. The legacy SIMD feature names are deprecated because runtime dispatch is used.
    - Tags: [cargo, crate-manifest, rust, searcher]
    - Additional indexed summary for `Cargo.toml` (Size : 995 bytes): Declares the `grep-searcher` package, its workspace edition and Rust-version settings, and its library metadata. Runtime dependencies provide byte handling, matcher integration, encoding, memory mapping, logging, and search utilities. Development dependencies support regex-backed tests. The manifest also retains deprecated SIMD feature flags that are documented as unused because runtime dispatch is used.
    - Tags: [cargo, rust, workspace-manifest]
- `LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License grant and conditions. It permits use, modification, distribution, sublicensing, and sale subject to retaining the copyright and permission notice. It disclaims warranties and liability. The file supplies one of the package's declared licensing options.
    - Tags: [license, mit]
    - Additional indexed summary for `LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License grant and conditions for use, copying, modification, distribution, and sublicensing. It requires the copyright and permission notice in copies or substantial portions. The text includes the standard warranty and liability disclaimer.
    - Tags: [license, mit]
- `README.md` (Size : 936 bytes): Describes `grep-searcher` as a high-level library for fast line-oriented searches. It lists contextual reporting, counting, inverted search, binary detection, UTF-16 transcoding, and memory-map choice among its responsibilities. The usage section shows the Cargo dependency declaration and links build and API documentation. It recommends the `grep` facade for most consumers.
    - Tags: [documentation, line-search, rust, searcher]
    - TODO/FIXME/NOTE: NOTE line 17 (exact marker `NOTE`)
    - Additional indexed summary for `README.md` (Size : 936 bytes): Introduces `grep-searcher` as a high-level library for line-oriented search and lists capabilities such as context reporting, binary detection, UTF-16 transcoding, and memory-map selection. It points readers to the crate documentation and recommends the `grep` facade for most direct usage. A short Cargo dependency example shows how to add the package.
    - Tags: [documentation, library, search, usage]
    - TODO/FIXME/NOTE: line 17: NOTE
- `UNLICENSE` (Size : 1235 bytes): Releases the software into the public domain and describes the associated dedication. It permits copying, modification, publication, use, compilation, sale, and distribution. It disclaims warranties and liability. The file is the second license option declared by the package manifest.
    - Tags: [license, public-domain, unlicense]
    - Additional indexed summary for `UNLICENSE` (Size : 1235 bytes): Contains the Unlicense dedication and public-domain license terms. It permits copying, modification, use, compilation, sale, and distribution for commercial or non-commercial purposes. The text also includes a warranty and liability disclaimer and refers readers to the Unlicense website.
    - Tags: [license, public-domain]
- `examples/search-stdin.rs` (Size : 788 bytes): Defines a small executable that reads a pattern from its first command-line argument and creates a `RegexMatcher`. It invokes `Searcher::search_reader` over stdin using the `UTF8` sink adapter. The callback prints each matching line with its line number. Errors are printed and cause a nonzero process exit.
    - Tags: [example, rust, search, stdin]

---
    - Additional indexed summary for `examples/search-stdin.rs` (Size : 788 bytes): Provides a command-line example that takes a pattern argument, constructs a `grep_regex::RegexMatcher`, and searches standard input with `Searcher`. Its UTF-8 sink closure prints each matching line with its line number. Missing arguments and search or matcher errors are returned through the example's error path.
    - Tags: [command-line, example, rust, search, standard-input]
- `src/lib.rs` (Size : 3824 bytes): Documents the crate's search flow, in which a `Searcher` applies a `Matcher` to input and delivers results to a `Sink`. The module-level example demonstrates regex matching over a byte slice with the UTF-8 sink adapter. It re-exports the principal searcher configuration, sink, and line-iteration APIs. Private module declarations separate buffering, line operations, search execution, sink behavior, macros, and test utilities.
    - Tags: [crate-api, documentation, rust, search]
- `src/line_buffer.rs` (Size : 36153 bytes): Implements reusable buffered input for line-oriented search, with configuration for capacity, line terminators, long-line allocation, and binary detection. `LineBufferReader` fills the buffer from an `io::Read` source, retaining incomplete lines until they can be completed and exposing absolute and binary-byte offsets. Binary policies can leave bytes untouched, stop at a selected byte, or replace it with the line terminator. Allocation limits and reader failures are returned as I/O errors.
    - Tags: [binary-detection, buffering, io, rust]
    - TODO/FIXME/NOTE: line 177: Note; line 249: Note; line 399: Note
- `src/lines.rs` (Size : 16928 bytes): Defines borrowed `LineIter` and explicit-position `LineStep` APIs for iterating over lines in byte slices. Both include each line terminator in the yielded range and do not yield empty ranges. Internal helpers count terminators, remove a configured terminator, locate the line containing a match, and find preceding lines for context. The searcher and sink modules use these operations to manage line boundaries.
    - Tags: [byte-processing, line-iteration, rust]
- `src/macros.rs` (Size : 764 bytes): Defines the test-only `assert_eq_printed!` macro for comparing expected and actual output. When values differ, it panics with an optional label and both values displayed in separate delimiters. Conditional compilation restricts the macro to test builds.
    - Tags: [macro, rust, testing]
- `src/searcher/core.rs` (Size : 23699 bytes): Implements `Core`, the shared search state used by line-based and multiline execution. It tracks matcher and sink state, input offsets, line numbers, context windows, binary detection, match counts, and match limits. It selects fast or slow line matching where applicable, then emits matches, context, and search lifecycle events through `Sink`. The glue strategies provide input and invoke this shared event-processing logic.
    - Tags: [line-buffering, rust, searcher, search-events]
    - TODO/FIXME/NOTE: line 683: FIXME
- `src/searcher/glue.rs` (Size : 51498 bytes): Implements the execution strategies that connect input sources, matchers, and the shared `Core`. `ReadByLine` processes buffered readers incrementally, `SliceByLine` searches slices by line, and `MultiLine` processes whole slices for matches spanning lines. The strategies coordinate context and binary handling while forwarding match results and completion data to the sink. Multiline matches are grouped by their covered lines before reporting.
    - Tags: [line-search, rust, searcher, sinks]
    - TODO/FIXME/NOTE: line 238: Note; line 743: Note
- `src/searcher/mmap.rs` (Size : 4578 bytes): Defines `MmapChoice`, the policy controlling whether searches may use file-backed memory maps. Memory maps are disabled by default; the unsafe `auto` choice permits their use when the platform and performance heuristics allow it. Mapping failures fall back to ordinary reads and are logged at debug level. The documented safety contract requires callers to ensure the underlying file is not mutated while mapped.
    - Tags: [file-input, memory-mapping, rust, searcher]
- `src/searcher/mod.rs` (Size : 42256 bytes): Defines the public `Searcher` and `SearcherBuilder` APIs, search configuration, encoding and binary-detection options, and operations over paths, files, readers, and slices. It validates matcher/searcher configuration, chooses line or multiline execution, and delegates to the strategy implementations in `glue.rs`. It also controls buffering, transcoding, heap limits, and optional memory-map use. Multiline reader searches buffer the full input before executing.
    - Tags: [line-search, rust, search-configuration, searcher]
    - TODO/FIXME/NOTE: line 578: Note; line 882: Note
- `src/sink.rs` (Size : 23786 bytes): Defines the `Sink` callback interface used by the searcher to report matches, context lines, context breaks, binary data, and search lifecycle events. `SinkError` converts message, I/O, and configuration failures to the sink's error type. Match, context, and finish structures expose bytes, line numbers, offsets, and search summary data. Convenience adapters support closure-based handling in addition to custom sink implementations.
    - Tags: [callbacks, rust, search, sink]
    - TODO/FIXME/NOTE: line 356: Note; line 607: TODO
- `src/testutil.rs` (Size : 28365 bytes): Supplies test-only matcher, sink, and search harness utilities for exercising searcher behavior. Its regex matcher can control line-terminator and candidate-line behavior, while `KitchenSink` captures emitted events and offsets for assertions. `SearcherTester` runs configured reader and slice search combinations against expected output. The module is included only for test builds.
    - Tags: [matcher, rust, test-support]
    - TODO/FIXME/NOTE: line 313: Note; line 465: Note

## Links Child Folder docmaps

- `src/docmap.md` — Public API, buffering, sink callbacks and nested search execution modules.

## Dependency Graph

Not generated.
