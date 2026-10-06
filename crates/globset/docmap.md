---
folder: "crates/globset"
generated_on: "2026-10-06"
num_files: 11
semantic_tags: [aho-corasick, api, benchmarking, glob-matching, glob-parsing, glob-patterns, glob-sets, hashing, hash-table, path-matching, path-parsing, performance, performance-testing, regex, rust, serde, serialization, string-processing, workspace-crate]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This folder contains the `globset` Rust crate, which compiles glob expressions for cross-platform path matching. Its public API supports both individual matchers and sets that report multiple matching patterns for one candidate. The crate uses regular-expression machinery and byte-string path support, with optional serialization and arbitrary-data features. Its source implementation and benchmark suite are indexed in child folder maps.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

The crate defines the glob and glob-set library package, its feature and dependency configuration, licensing, and user-facing documentation. Its source folder contains the implementation of parsing, matching, path handling, and serialization. The benchmark folder compares globset matching with another glob implementation.

## Technology Notes

Rust library crate; uses `regex-automata`, `regex-syntax`, `aho-corasick`, and `bstr`. Optional features include `serde1` and `arbitrary`.

# Folder Navigation

## Merged Child Folders
- `benches/` —
  This folder measures the performance of glob matching implementations. Its benchmark cases compare the glob crate against globset for extension, short-path, long-path, and multiple-pattern workloads. The results exercise both individual matchers and set-based matching against candidate paths. This folder contains one Rust benchmark source file.
- `src/` —
  This folder implements the `globset` crate's glob parsing and path-matching functionality. It provides public APIs for building individual glob patterns and sets of patterns, then matching candidate paths against them. Glob syntax is parsed into tokens and compiled into byte-oriented regular expressions, with specialized strategies to speed up common literal, basename, extension, prefix, and suffix cases. Supporting modules provide path component handling, an internal FNV hasher, and optional Serde integration.
## Files
- `Cargo.toml` (Size : 1534 bytes): Declares the `globset` Rust library crate and its package metadata. It configures the crate's `regex-automata`, `regex-syntax`, `aho-corasick`, and `bstr` dependencies, along with optional serde and arbitrary support. The `simd-accel` feature is documented as deprecated and a no-op. Development dependencies support comparison and serialization tests.
    - Tags: [cargo, dependencies, rust]

- `COPYING` (Size : 129 bytes): States that the project is free and unencumbered software released into the public domain. It summarizes permission to use, modify, and distribute the software and disclaims warranties and liability. The notice points readers to the Unlicense for additional information. It is the short public-domain licensing notice for this crate.
    - Tags: [license, unlicense]

- `LICENSE-MIT` (Size : 1102 bytes): Contains the MIT license terms and the 2015 Andrew Gallant copyright notice. It grants broad rights to use, modify, distribute, sublicense, and sell the software subject to retaining the notice. It includes the standard warranty and liability disclaimer. This file provides the MIT licensing option for the crate.
    - Tags: [license, mit]

- `README.md` (Size : 3961 bytes): Documents the crate's single-glob and glob-set matching APIs with Rust usage examples. It explains configurable matching semantics, simultaneous matching of many patterns, and performance comparisons. It describes optional Serde support and limitations relative to the `glob` crate, including no recursive directory iterator and no require-literal-leading-dot option. This is the crate's public-facing usage and capability guide.
    - Tags: [documentation, glob-matching, rust]

- `UNLICENSE` (Size : 1235 bytes): Provides the Unlicense public-domain dedication and permission terms. It states that the software may be used, copied, modified, and distributed for any purpose. It also disclaims warranties and liability. This file is one of the crate's two declared license options.
    - Tags: [license, unlicense]
- `benches/bench.rs` (Size : 2864 bytes): Defines microbenchmarks comparing the `glob` crate with globset's compiled matchers for extension, short, and long paths. It also compares sequential evaluation of many patterns with a built `GlobSet` over one candidate path. Helper functions construct glob patterns, matchers, and sets before timing assertions. The benchmark cases measure glob matching behavior rather than ripgrep's end-to-end search performance.
    - Tags: [benchmarking, glob-matching, performance-testing, rust]
- `src/fnv.rs` (Size : 795 bytes): Defines a crate-private `HashMap` alias configured with the module's `Hasher`, and implements the Fowler–Noll–Vo hash by XORing each input byte and multiplying with wrapping arithmetic. The hasher is used by the glob-set matching strategies for their lookup tables. Its implementation satisfies `std::hash::Hasher` through `finish` and `write`, with `Default` initializing the standard 64-bit FNV offset basis. No TODO, FIXME, or NOTE markers were found.
    - Tags: [hashing, hash-table, performance, rust]
- `src/glob.rs` (Size : 62457 bytes): Defines `Glob`, `GlobBuilder`, and `GlobMatcher`, along with token and parser machinery that translates glob syntax into regular expressions. Builder options control case sensitivity, separator matching, backslash escapes, and other parsing or matching semantics. `MatchStrategy` recognizes patterns that can use literal, basename, extension, prefix, or suffix checks before falling back to regex matching; tests exercise parsing and match behavior. The file's documentation describes supported glob syntax and byte-oriented regex usage.
    - Tags: [glob-matching, glob-parsing, regex, rust]
    - TODO/FIXME/NOTE: NOTE line 41 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 314 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 349 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 505 (exact marker `Note`)
- `src/lib.rs` (Size : 41980 bytes): Provides the crate-level documentation and public API for `GlobSet`, `GlobSetBuilder`, `Candidate`, and glob parsing errors. It builds a set from patterns, prepares candidate paths, and returns whether any or all patterns match or the indices of matching patterns. Its internal matcher partitions patterns into specialized hash-map lookups and Aho–Corasick prefix/suffix searches, with regex-set and required-extension strategies handling the remaining cases. Tests and examples document set matching behavior; a TODO discusses the regex-set pattern pool and a future API change.
    - Tags: [api, glob-sets, path-matching, rust]
    - TODO/FIXME/NOTE: NOTE line 91 (exact marker `Note`)
    - TODO/FIXME/NOTE: TODO line 970 (exact marker `TODO`)
    - TODO/FIXME/NOTE: NOTE line 1119 (exact marker `note`)
- `src/pathutil.rs` (Size : 4548 bytes): Implements byte-oriented helpers for extracting a path's final filename and extension while preserving borrowed data where possible. Its extension definition includes the leading dot and treats names such as `.rs` as having an extension, supporting the glob matcher’s extension optimizations. Platform-specific `normalize_path` keeps Unix paths unchanged and converts recognized non-Unix separators to `/`. Unit tests cover filename, extension, and normalization cases.
    - Tags: [path-parsing, rust, string-processing]
    - TODO/FIXME/NOTE: NOTE line 26 (exact marker `Note`)
- `src/serde_impl.rs` (Size : 3308 bytes): Adds Serde implementations for `Glob` and `GlobSet` when the feature is enabled. A glob is serialized as its pattern string and deserialized through `Glob::new`, while a set is deserialized from a sequence by adding its patterns to `GlobSetBuilder` and building the result. Its tests cover borrowed and owned glob deserialization, invalid-pattern errors, JSON round trips, and set matching. No TODO, FIXME, or NOTE markers were found.
    - Tags: [rust, serde, serialization]

---

## Links Child Folder docmaps
None.
# Related Features

Single-glob matching, simultaneous glob-set matching, and configurable path matching.

# Agent Guidance

## Read When

Working on the globset crate's public API, package configuration, documentation, licensing, or benchmarks.

## Modify When

Changing crate dependencies, features, usage documentation, legal notices, or implementation indexed in the linked source map.

## Avoid Modifying When

Changing ripgrep command-line search behavior outside glob matching; inspect the relevant core, ignore, or grep crate maps instead.
