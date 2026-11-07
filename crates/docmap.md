---
folder: "crates"
generated_on: "2026-10-06"
num_files: 38
semantic_tags: [api, api-facade, benchmarking, bom-handling, byte-analysis, captures, cargo, cargo-workspace, case-detection, cli, command-dispatch, configuration, crate-documentation, crate-manifest, default-types, directory-matching, directory-traversal, documentation, error-handling, error-reporting, example, facade, file-input, filename-matching, file-traversal, file-types, filtering, gitignore, glob-matching, glob-parsing, glob-sets, grep, grep-printer, grep-searcher, hashing, hash-table, hir-transformation, hyperlinks, ignore-crate, ignore-overrides, ignore-rules, incremental-matching, integration-tests, interpolation, library, library-facade, license, licensing, line-buffering, line-search, line-terminator, literal-analysis, literal-extraction, logging, macros, matcher, matcher-interface, matching, memory-mapping, mit, optimization, parallelism, path-encoding, path-filtering, path-matching, path-normalization, path-parsing, pcre2, performance, performance-testing, preprocessing, printer, public-domain, recursive-search, re-exports, regex, regex-compilation, regex-hir, regex-search, regex-syntax, regex-validation, replacement, rust, search, search-configuration, searcher, search-events, searching, search-output, serde, serialization, sinks, smart-case, statistics, stdin, streaming-io, string-processing, terminal-output, terms, test-fixture, testing, test-organization, test-support, unlicense, uri-conversion, utf-8, walker, whitelist, workspace-crate]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This folder contains the Rust crates that make up ripgrep's executable and reusable search libraries. The packages separate command-line orchestration, file traversal, matching, searching, and output into focused modules. Supporting crates provide glob matching and optional PCRE2 integration. Package maps and the inline core entries identify source, examples, tests, configuration, and documentation.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

The `core` crate implements the `rg` executable's command dispatch and search orchestration, while `cli` provides reusable command-line utilities. `ignore`, `matcher`, `regex`, `pcre2`, `searcher`, `printer`, and `grep` supply the traversal, matching, search, output, and facade layers. `globset` handles glob expressions and sets.

## Technology Notes

The packages are Rust Cargo workspace members using the Rust 2024 workspace edition. The maps describe Rust regex and PCRE2 matcher implementations, glob matching, file walking, line-oriented search, and printer output. Dependency relationships are intentionally not inferred.

# Folder Navigation

## Merged Child Folders
- `core/` —
  - Tags: [cli, command-dispatch, crate-documentation, error-reporting, file-traversal, filtering, logging, macros, matching, preprocessing, rust, search, statistics, streaming-io]. TODO/FIXME/NOTE: present; see indexed files.
  This folder contains the executable core of ripgrep: its entry point, command dispatch, traversal coordination, search orchestration, and user-facing messages. The core README describes it as the layer that defines the CLI and connects matcher, searcher, and printer crates. File selection is mediated by haystack wrappers and the ignore-aware walker, while flag parsing prepares runtime configuration. The flag subsystem is documented in its surviving child map.
  Major responsibilities: `core/main.rs` dispatches special modes, ordinary searches, file listing, type listing, and generated output, then maps results and errors to process exit codes. `core/search.rs` coordinates matcher, searcher, printer, preprocessors, and parallel workers. Supporting modules define candidate haystacks, logging, and conditional user-message/exit-error state.
  Technology notes: The executable is implemented in Rust and composes the workspace's `grep`, `ignore`, and terminal-output facilities. Parallel traversal and search are used when configured.
  Related features: Ripgrep command execution, file traversal, search and output coordination, and command-line parsing.
  Read when: Changing top-level CLI behavior, traversal or search dispatch, candidate-file selection, message handling, or integration of the core search components.
  Modify when: The change affects the executable's coordination of parsing, walking, searching, output, or exit status.
  Avoid modifying when: The change is isolated to a reusable matcher, printer, walker, or CLI utility crate and does not affect core orchestration.

- `grep/` —
  - Tags: [api, cargo, cli, crate-manifest, documentation, example, facade, library, license, licensing, mit, pcre2, public-domain, recursive-search, re-exports, rust, terms, unlicense]. TODO/FIXME/NOTE: present; see indexed files.
  This crate presents ripgrep's component crates as a high-level Rust library facade. Its public library re-exports command-line helpers, matcher implementations, printers, and searchers under a single `grep` namespace. The crate manifest makes PCRE2 support optional and keeps older SIMD feature names as deprecated no-op compatibility features. `README.md` documents installation and explicitly notes the lack of a high-level integration guide.
- `grep/examples/` —
  - Tags: [cli, example, recursive-search, rust]. TODO/FIXME/NOTE: none.
  This folder contains a runnable example of assembling ripgrep's library components into a simple recursive search program. The example parses a pattern and optional paths from command-line arguments. It traverses files, skips non-files, searches them with a regex matcher, and sends output through the standard printer. It also demonstrates terminal-aware color selection and per-path error reporting.
- `grep/src/` —
  - Tags: [api, facade, re-exports, rust]. TODO/FIXME/NOTE: none.
  This folder defines the public library facade for the `grep` crate. Its single source file re-exports the crate components that provide command-line helpers, matchers, printers, regex support, and searching. PCRE2 is conditionally re-exported only when its feature is enabled. The module documentation says that constituent crates have API documentation but that high-level integration guidance and examples remain sparse.
- `matcher/` —
  - Tags: [api, captures, cargo, crate-manifest, documentation, integration-tests, interpolation, license, matcher, matcher-interface, mit, public-domain, regex, replacement, rust, search, testing, test-organization, test-support, unlicense]. TODO/FIXME/NOTE: present; see indexed files.
  This crate defines a low-level, implementation-independent interface for regex and substring matchers used by grep search. The manifest names the package `grep-matcher` and describes a trait oriented toward line-based search. Its `src/` module provides the public API, while `tests/` contains integration coverage using the regex crate. Separate folder maps document both code areas.
- `matcher/src/` —
  - Tags: [api, captures, interpolation, matcher-interface, replacement, rust, search]. TODO/FIXME/NOTE: present; see indexed files.
  This source folder defines the public `grep-matcher` API and the helper used to expand capture references in replacement text. It provides implementation-neutral abstractions for byte-oriented matching and line search. The core trait supplies required operations alongside defaults for iteration, captures, replacement, and fast search hints. The neighboring `tests/` folder exercises the contract through concrete regex adapters.
- `matcher/tests/` —
  - Tags: [integration-tests, matcher, regex, rust, testing, test-organization, test-support]. TODO/FIXME/NOTE: none.
  This folder contains integration tests for the `grep-matcher` trait and utilities that adapt the `regex` crate to that trait. The test harness is explicitly wired through the crate manifest as the `integration` test target. Tests cover matching, captures, iteration, and replacement behavior. The parent crate map links to this standalone test index.
- `pcre2/` —
  - Tags: [api, cargo, crate-manifest, documentation, error-handling, license, matcher-interface, matching, mit, pcre2, public-domain, rust, unlicense]. TODO/FIXME/NOTE: present; see indexed files.
  This folder contains the `grep-pcre2` crate, which adapts PCRE2 to the grep ecosystem's matcher interface. It lets line-oriented search use PCRE2's matching capabilities through the grep facade. The package manifest declares the matcher, logging, and PCRE2 dependencies and inherits workspace edition metadata. Its implementation is indexed in the `src` child map.
- `pcre2/src/` —
  - Tags: [api, error-handling, matcher-interface, matching, pcre2, rust]. TODO/FIXME/NOTE: present; see indexed files.
  This folder implements ripgrep's PCRE2-backed regular-expression matcher. It exposes a small crate-level API for constructing matchers, obtaining capture information, and handling regex errors. The matcher adapts PCRE2's byte-oriented engine to the `grep_matcher` traits used by the rest of the project. Inline tests cover matcher options and line matching behavior.
- `printer/` —
  - Tags: [cargo, crate-manifest, documentation, license, mit, printer, public-domain, rust, search-output, unlicense]. TODO/FIXME/NOTE: present; see indexed files.
  This crate provides printers that consume search results from `grep-searcher`. Its public API offers human-readable standard output, aggregate summaries, path-only output, and JSON Lines output. The package manifest and README define the crate's published identity and intended use. The implementation is split into the `src` folder, whose standalone index describes the printer types and supporting utilities.
- `searcher/` —
  - Tags: [cargo, crate-manifest, documentation, example, license, line-search, mit, public-domain, rust, search, searcher, stdin, unlicense]. TODO/FIXME/NOTE: present; see indexed files.
  This crate provides a high-level library for fast line-oriented searches, with optional multiline searches. Its `Searcher` applies a generic matcher to input and pushes match, context, and lifecycle events to a caller-provided sink. The crate handles search concerns such as line counting, binary detection, encoding, and memory-map selection. Its Rust implementation is indexed in `src`, while `examples` contains a runnable stdin search sample.
- `searcher/examples/` —
  - Tags: [example, rust, search, stdin]. TODO/FIXME/NOTE: none.
  This folder demonstrates using `grep-searcher` to search standard input. The example accepts a regular-expression pattern from the command line and constructs a regex matcher. It sends matching UTF-8 lines to a sink closure that prints line numbers and contents. This provides a compact usage example for the crate's search-reader API.
## Files
- `core/README.md` (Size : 689 bytes): Describes the role of the ripgrep core crate, identifying `main.rs` as the executable entry point and summarizing the CLI definition and glue between matcher, searcher, and printer crates. It notes that core is not planned as an independent library and that reusable heavy lifting lives in constituent crates. Tags: [crate-documentation, rust, search].

- `core/haystack.rs` (Size : 5901 bytes): Wraps ignore-walker directory entries in `Haystack` and filters entries that should be searched. Explicitly supplied non-directory entries and stdin are retained, while implicitly discovered candidates must be files; walker errors are reported through the core message path. The builder can also strip a leading `./` from displayed paths. Tags: [file-traversal, filtering, rust, search]. TODO/FIXME/NOTE: NOTE line 128 (exact marker `note`).

- `core/logger.rs` (Size : 2196 bytes): Implements a small `log::Log` backend that writes records to stderr with available target, file, and line metadata. It relies on the global maximum log level for filtering and initializes itself as the process-wide logger. Tags: [logging, rust].

- `core/main.rs` (Size : 18962 bytes): Implements ripgrep's process entry point and routes parsed arguments to special modes, search, file listing, type listing, or generated output. Search and listing use sequential or parallel traversal according to the configured thread count, with the ignore-aware walker and core search worker handling candidates. It writes generated help, version, man-page, and shell-completion output, and reports search statistics when requested. Broken pipes are treated as graceful termination, while other failures and accumulated non-fatal errors determine the process exit status. Tags: [cli, command-dispatch, error-handling, file-traversal, rust, search, statistics]. TODO/FIXME/NOTE: NOTE line 430 (exact marker `Note`).

- `core/messages.rs` (Size : 5182 bytes): Defines atomic process-wide switches for ordinary and ignore-related messages and tracks whether a non-fatal error occurred. Its macros serialize stderr output against stdout writes and update error state so the executable can choose an exit code. Tags: [error-reporting, logging, macros, rust]. TODO/FIXME/NOTE: NOTE line 121 (exact marker `Note`).

- `core/search.rs` (Size : 16364 bytes): Defines the search-worker builder and worker that connect a pattern matcher, searcher, and printer. It handles file-level preprocessing and decompression before passing content to the searcher, and provides the per-path and reader search routines used by core execution. Tags: [matching, preprocessing, rust, search, streaming-io]. TODO/FIXME/NOTE: NOTE line 121 (exact marker `Note`).
---

- `grep/Cargo.toml` (Size : 1053 bytes): Declares the `grep` Rust library package and inherits its edition and minimum Rust version from the workspace. Its dependencies assemble the component crates behind the facade, with PCRE2 optional and enabled through the `pcre2` feature. Development dependencies support the example's terminal-aware output and filesystem traversal. The legacy SIMD feature names are explicitly deprecated because runtime dispatch is used.
    - Tags: [cargo, crate-manifest, pcre2, rust]
- `grep/COPYING` (Size : 129 bytes): States that the package is dual-licensed under the Unlicense and MIT licenses. It permits use under either license. The file serves as a brief package-level license selector. Full license terms are in the adjacent license files.
    - Tags: [license, licensing, terms]
- `grep/LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License and identifies Andrew Gallant's 2015 copyright. It permits use, copying, modification, distribution, and sublicensing when the notice and permission text are retained. The terms provide the software without warranty and disclaim liability. This is one of the two licensing options named by the package.
    - Tags: [license, mit, terms]
- `grep/README.md` (Size : 910 bytes): Introduces the crate as ripgrep's library interface and points readers to its docs.rs documentation. It gives the Cargo dependency declaration and describes the optional PCRE2 matcher feature. The README says that the crate is not yet ready for wide use and lacks high-level guidance on composing its parts. This documents the API's integration-documentation limitation.
    - Tags: [documentation, library, pcre2, rust]
    - TODO/FIXME/NOTE (line 15):
      ```
      NOTE: This crate isn't ready for wide use yet. Ambitious individuals can
      ```
- `grep/UNLICENSE` (Size : 1235 bytes): Publishes the software into the public domain and permits use, modification, compilation, sale, and distribution. It describes the dedication of copyright interest and supplies an as-is warranty and liability disclaimer. The file is the Unlicense option named by the package's dual-license notice. It includes a pointer to the Unlicense website.
    - Tags: [license, public-domain, unlicense]
- `grep/examples/simplegrep.rs` (Size : 2043 bytes): Implements a small command-line recursive search example that requires a pattern and defaults the path to the current directory. It builds a line regex matcher, configures binary detection and a searcher, and selects printer colors according to whether stdout is a terminal. It walks paths with `walkdir`, searches regular files, and reports errors without aborting the remaining paths. The example exercises the grep facade's CLI, regex, searcher, and printer modules together.
    - Tags: [cli, example, recursive-search, rust]
- `grep/src/lib.rs` (Size : 677 bytes): Documents the crate as a library facade and describes the lack of a high-level guide for composing its components. It publicly re-exports `grep-cli`, `grep-matcher`, `grep-printer`, `grep-regex`, and `grep-searcher` under short module names. It conditionally re-exports `grep-pcre2` when the `pcre2` feature is active. The file is the crate's public entry point rather than a search implementation.
    - Tags: [api, facade, re-exports, rust]
- `matcher/Cargo.toml` (Size : 643 bytes): Declares the `grep-matcher` package and its line-oriented matcher purpose, crate metadata, dual license, and workspace Rust settings. It disables automatic integration-test discovery and explicitly declares the `integration` test target. `memchr` is the runtime dependency and `regex` is used for development tests.
    - Tags: [cargo, crate-manifest, matcher, rust]
- `matcher/LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License grant and conditions for use, modification, distribution, and sublicensing. It requires preservation of the copyright and permission notice in copies or substantial portions. It disclaims warranties and liability. This is one of the crate's two licensing texts.
    - Tags: [license, mit]
- `matcher/README.md` (Size : 851 bytes): Describes the crate as a low-level interface for regular-expression matchers, used to make the regex engine in the `grep` crate pluggable. It links to package documentation and includes a Cargo dependency example. It cautions consumers to prefer the `grep` facade over direct use. That caution is marked NOTE on line 16.
    - Tags: [documentation, matcher-interface, rust]
    - TODO/FIXME/NOTE: NOTE line 16 (exact marker `NOTE`)
- `matcher/UNLICENSE` (Size : 1235 bytes): Dedicates the software's copyright interest to the public domain and grants broad rights to use, copy, modify, publish, compile, sell, and distribute it. It states that the software is provided without warranty and limits liability. It directs readers to unlicense.org for more information. This is the crate's public-domain licensing alternative.
    - Tags: [license, public-domain, unlicense]
- `matcher/src/interpolate.rs` (Size : 8946 bytes): Implements capture-reference expansion over replacement bytes, recognizing numbered and named references, braced names, and escaped dollar signs. A callback resolves capture indices and writes matched bytes while a second callback maps names to indices. The parser restricts names to ASCII letters, digits, and underscores and leaves malformed references literal. Unit tests cover parsing and replacement edge cases.
    - Tags: [captures, interpolation, replacement, rust]
- `matcher/src/lib.rs` (Size : 48016 bytes): Defines the crate's public matcher contract and supporting `Match`, `LineTerminator`, `ByteSet`, `Captures`, `NoCaptures`, `NoError`, and `LineMatchKind` types. `Matcher` requires offset-based search and capture construction, then provides generic defaults for iteration, capture iteration, replacement, match checks, shortest matches, and line candidates. Its design uses internal callback-driven iteration to support backends that need to drive search. Marker lines note capture semantics and method guarantees.
    - Tags: [api, matcher-interface, rust, search]
    - TODO/FIXME/NOTE: NOTE line 375 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 404 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 414 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 436 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 883 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 998 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1020 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1121 (exact marker `Note`)
- `matcher/tests/test_matcher.rs` (Size : 6682 bytes): Exercises search, successive match iteration, shortest matches, named and indexed capture access, capture iteration, and callback short-circuit/error behavior. It also verifies replacement with and without captures, including interpolation. The tests use the helper adapters declared in `util.rs`. Assertions target the shared `Matcher` behavior rather than regex parsing features.
    - Tags: [integration-tests, matcher, rust, testing]
- `matcher/tests/tests.rs` (Size : 32 bytes): Declares `util` as a test helper module and `test_matcher` as the integration test module. It contains no matching logic itself. The declarations organize the test crate's source modules. This file is the test harness entry point.
    - Tags: [integration-tests, rust, test-organization]
- `matcher/tests/util.rs` (Size : 2604 bytes): Defines regex-backed `Matcher` adapters with capture support and without it, plus a `RegexCaptures` wrapper over regex capture locations. The capture-capable adapter implements core search and capture methods while leaving other methods to exercise trait defaults. The no-capture adapter exposes `NoCaptures` and only implements required operations. Tests in `test_matcher.rs` use these helpers to validate the trait contract.
    - Tags: [matcher, regex, rust, test-support]
- `pcre2/Cargo.toml` (Size : 578 bytes): Declares the `grep-pcre2` Rust package and its metadata, inheriting edition and minimum Rust version from the workspace. Its dependencies are `grep-matcher`, `log`, and the PCRE2 binding crate. The manifest configures the adapter package used to connect PCRE2 matching to grep.
    - Tags: [cargo, crate-manifest, pcre2, rust]
- `pcre2/LICENSE-MIT` (Size : 1102 bytes): Contains the MIT license terms and the 2015 Andrew Gallant copyright notice. It grants rights to use, modify, distribute, sublicense, and sell the software subject to retaining the notice. It includes the standard warranty and liability disclaimer. This file provides the MIT licensing option for the crate.
    - Tags: [license, mit]
- `pcre2/README.md` (Size : 1030 bytes): Describes `grep-pcre2` as an implementation of the `grep-matcher` crate's `Matcher` trait for PCRE2-backed line-oriented search. It explains that consumers should generally use the `grep` facade instead of depending on this crate directly. It also points users seeking general Rust PCRE2 bindings to the `pcre2` crate and includes package usage guidance. The README contains an uppercase NOTE advising against direct use.
    - Tags: [documentation, matcher-interface, pcre2, rust]
    - TODO/FIXME/NOTE: NOTE line 16 (exact marker `NOTE`)
- `pcre2/UNLICENSE` (Size : 1235 bytes): Provides the Unlicense public-domain dedication and permission terms. It states that the software may be used, copied, modified, and distributed for any purpose. It also disclaims warranties and liability. This file is one of the crate's two declared license options.
    - Tags: [license, public-domain, unlicense]
- `pcre2/src/error.rs` (Size : 1386 bytes): Defines the crate's public `Error` wrapper and non-exhaustive `ErrorKind` enum for regex-related failures. Its crate-private constructor converts underlying standard errors into a regex error string. The `kind` accessor lets callers inspect the failure category. `Display` and `std::error::Error` implementations expose the message and a general description.
    - Tags: [error-handling, pcre2, rust]
- `pcre2/src/lib.rs` (Size : 324 bytes): Documents this crate as an implementation of `grep_matcher`'s `Matcher` trait for PCRE2. It re-exports PCRE2's JIT-availability and version functions together with the crate's error, capture, matcher, and builder types. The implementation modules remain private while selected types form the crate-level API. A crate attribute denies missing documentation on public items.
    - Tags: [api, matcher-interface, pcre2, rust]
- `pcre2/src/matcher.rs` (Size : 18396 bytes): Implements the PCRE2-backed `RegexMatcherBuilder`, `RegexMatcher`, and `RegexCaptures` types. The builder configures PCRE2 behavior, combines multiple patterns, optionally escapes fixed strings, and tracks named capture indices; the matcher adapts PCRE2 searches and captures to `grep_matcher` types. Inline tests exercise word matching, CRLF line endings, smart case, and candidate-line matching. The documentation notes that smart-case detection is approximate and that some capture groups may be absent in an individual match.
    - Tags: [matching, pcre2, rust]
    - TODO/FIXME/NOTE: NOTE line 112 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 218 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 383 (exact marker `Note`)
- `printer/Cargo.toml` (Size : 1445 bytes): Declares the `grep-printer` package, its metadata, and workspace Rust settings. The default `serde` feature enables optional serialization dependencies; runtime dependencies cover byte strings, matcher and searcher APIs, logging, terminal colors, and JSON serialization. A regex development dependency supports tests, while docs.rs is configured to build all features with documentation-only cfg support.
    - Tags: [cargo, crate-manifest, printer, rust]
- `printer/LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License grant and conditions. It permits use, modification, distribution, sublicensing, and sale subject to retaining the copyright and permission notice. It disclaims warranties and liability. The file supplies one of the package's declared licensing options.
    - Tags: [license, mit]
- `printer/README.md` (Size : 770 bytes): Introduces `grep-printer` as an implementation of the grep crate's sink for human-readable, aggregate, or JSON Lines search output. It links build status, crate publication, and API documentation. The usage section shows how to add the crate as a Cargo dependency. It advises most consumers to use the `grep` facade instead.
    - Tags: [documentation, printer, rust, search-output]
    - TODO/FIXME/NOTE: NOTE line 15 (exact marker `NOTE`)
- `printer/UNLICENSE` (Size : 1235 bytes): Releases the software into the public domain and describes the associated dedication. It permits copying, modification, publication, use, compilation, sale, and distribution. It disclaims warranties and liability. The file is the second license option declared by the package manifest.
    - Tags: [license, public-domain, unlicense]
- `searcher/Cargo.toml` (Size : 995 bytes): Declares the `grep-searcher` package and its workspace Rust settings. Runtime dependencies provide byte handling, encoding, matcher integration, logging, byte searching, and memory mapping; development dependencies add regex-backed testing support. The legacy SIMD feature names are deprecated because runtime dispatch is used.
    - Tags: [cargo, crate-manifest, rust, searcher]
- `searcher/LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License grant and conditions. It permits use, modification, distribution, sublicensing, and sale subject to retaining the copyright and permission notice. It disclaims warranties and liability. The file supplies one of the package's declared licensing options.
    - Tags: [license, mit]
- `searcher/README.md` (Size : 936 bytes): Describes `grep-searcher` as a high-level library for fast line-oriented searches. It lists contextual reporting, counting, inverted search, binary detection, UTF-16 transcoding, and memory-map choice among its responsibilities. The usage section shows the Cargo dependency declaration and links build and API documentation. It recommends the `grep` facade for most consumers.
    - Tags: [documentation, line-search, rust, searcher]
    - TODO/FIXME/NOTE: NOTE line 17 (exact marker `NOTE`)
- `searcher/UNLICENSE` (Size : 1235 bytes): Releases the software into the public domain and describes the associated dedication. It permits copying, modification, publication, use, compilation, sale, and distribution. It disclaims warranties and liability. The file is the second license option declared by the package manifest.
    - Tags: [license, public-domain, unlicense]
- `searcher/examples/search-stdin.rs` (Size : 788 bytes): Defines a small executable that reads a pattern from its first command-line argument and creates a `RegexMatcher`. It invokes `Searcher::search_reader` over stdin using the `UTF8` sink adapter. The callback prints each matching line with its line number. Errors are printed and cause a nonzero process exit.
    - Tags: [example, rust, search, stdin]

---

## Links Child Folder docmaps
- `cli/docmap.md` — Reusable Rust CLI utilities for terminal output, process handling, pattern and byte processing, and decompression.
- `core/flags/docmap.md` — Defines ripgrep's CLI flag model, parser, and conversion of raw arguments into validated search configuration; shared flag metadata also drives help, manual, and shell-completion output, and configuration arguments are loaded through `RIPGREP_CONFIG_PATH`.

- `globset/docmap.md` — Rust crate for compiling glob expressions into cross-platform path matchers and sets, with optional serialization and arbitrary-data features; source and benchmarks are indexed separately.
- `ignore/docmap.md` — Rust APIs for matching ignore rules and walking directory trees while honoring ignore files, globs, and file types; includes examples, implementation, tests, and traversal benchmarks.
- `printer/src/docmap.md` — Describes printer implementations, formatting helpers, and the crate's public API.
- `regex/docmap.md` — Connects Rust's regular-expression engine to the `grep-matcher` interface for line-oriented search, with matcher configuration, HIR processing, and source details indexed separately.
- `searcher/docmap.md` — Searcher crate package files and public API; implementation details are indexed in its `src` child map.
# Related Features

Rust implementation of the ripgrep executable and its reusable traversal, matching, search, and output libraries.

# Agent Guidance

## Read When

Changing how the executable or search libraries coordinate, or selecting the crate responsible for traversal, matching, search execution, or output.

## Modify When

Adding or reorganizing workspace crates or changing how the repository's Rust modules are divided.

## Avoid Modifying When

Changing a crate-specific behavior without first reading that crate's own folder index and implementation map.
