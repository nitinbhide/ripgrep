---
folder: "crates/regex"
generated_on: "2026-10-06"
num_files: 13
semantic_tags: [api, ast, byte-analysis, byte-matching, captures, cargo, case-detection, configuration, crate-metadata, documentation, error-handling, hir, hir-transformation, licensing, line-terminator, literal-extraction, matcher-interface, optimization, regex, regex-compilation, regex-hir, regex-syntax, regex-validation, rust, search-optimization, smart-case]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This crate connects Rust's regular-expression engine to the `grep-matcher` interface for line-oriented searching. Its manifest identifies the crate as `grep-regex` and describes its role as a matcher implementation used by the grep search layer. The README documents its public purpose and points users toward the higher-level `grep` facade. The implementation is organized under `src/`, with its own folder index.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

The package-level files define crate metadata, licensing terms, and user-facing guidance; matching behavior is implemented in `src/`. The source folder analyzes and transforms regex HIR, configures the regex engine, and exposes the matcher and capture APIs. Consult `src/docmap.md` for per-file responsibilities and marker details.

## Technology Notes

This is a Rust crate configured through Cargo and workspace-shared edition and minimum Rust-version settings. Its README documents use of Rust's regex engine through the grep matcher abstraction. Package dependencies are recorded in `Cargo.toml`; no dependency relationships are inferred here.

# Folder Navigation

## Merged Child Folders
- `src/` —
  This source folder implements `grep-regex`, adapting Rust's regex automata to the `grep-matcher` API. It parses patterns, applies matcher-specific configuration, compiles HIR, and provides the public matcher and capture types. Supporting modules enforce byte and line-terminator constraints and derive safe search accelerations. Tests embedded in the Rust modules exercise these transformations and matching behavior.
## Files
- `Cargo.toml` (Size : 729 bytes): Declares the `grep-regex` crate, its description, documentation and repository links, keywords, dual license, and workspace Rust settings. Its dependencies include the matcher interface, byte-string utilities, logging, regex automata, and regex syntax. The manifest explicitly positions this crate as the regex-engine implementation of the grep matcher interface. It is the package-level source for build metadata and dependency declarations.
    - Tags: [cargo, dependencies, manifest, regex, rust]

- `LICENSE-MIT` (Size : 1102 bytes): Contains the MIT License grant and conditions for use, modification, distribution, and sublicensing. It requires retaining the copyright and permission notice in copies or substantial portions. It disclaims warranties and liability. This file is one of the crate's two licensing texts.
    - Tags: [license, mit]

- `README.md` (Size : 876 bytes): Describes `grep-regex` as an implementation of the `grep-matcher` `Matcher` trait backed by Rust's regex engine for fast line-oriented search. It provides crate documentation and package links, licensing information, and a Cargo usage example. It cautions that consumers will generally want the `grep` facade instead of using this crate directly. The caution is marked with NOTE at line 16.
    - Tags: [documentation, grep, matcher, regex, rust]
    - TODO/FIXME/NOTE: L16 NOTE — `**NOTE:** You probably don't want to use this crate directly. Instead, you`

- `UNLICENSE` (Size : 1235 bytes): Dedicates copyright interest in the software to the public domain and grants broad rights to use, copy, modify, publish, compile, sell, and distribute it. It states that the software is provided without warranty and limits liability. The text directs readers to unlicense.org for more information. This file is the crate's public-domain licensing alternative.
    - Tags: [license, public-domain]
- `src/ast.rs` (Size : 6521 bytes): Defines `AstAnalysis`, which walks regex syntax AST nodes and class-set expressions to record whether literal characters exist and whether any literal is uppercase. These facts support smart-case decisions in configuration. The traversal stops early once both facts are known and skips non-literal constructs. Its tests cover escapes, classes, and representative case patterns.
    - Tags: [case-detection, regex-syntax, rust, smart-case]
- `src/ban.rs` (Size : 2757 bytes): Implements a recursive HIR check that rejects regex expressions containing a configured banned ASCII byte. It examines literal bytes and sufficiently narrow byte or Unicode classes, then descends through repetitions, captures, concatenations, and alternations. A match is reported as `ErrorKind::Banned`. Unit tests exercise literals, classes, and nested expressions.
    - Tags: [regex-hir, regex-validation, rust]
- `src/config.rs` (Size : 14828 bytes): Defines the matcher configuration and `ConfiguredHIR`, which retains the options used to construct an expression. It parses or directly builds pattern alternations, handles smart case and fixed strings, transforms for line and word matching, and applies banned-byte and line-terminator rules. It then compiles the HIR into `regex-automata` and derives non-matching-byte information. The retained configuration also governs later optimization regexes.
    - Tags: [configuration, regex-compilation, regex-hir, rust]
- `src/error.rs` (Size : 3277 bytes): Defines the public `Error` wrapper and non-exhaustive `ErrorKind` variants for regex build failures, disallowed line terminators, invalid line terminators, and banned bytes. Constructors translate regex automata and parser/build errors into the crate's error model. `Display` formats each variant for callers, including byte-oriented messages. This module is used by configuration and HIR transformation routines.
    - Tags: [error-handling, regex, rust]
- `src/lib.rs` (Size : 341 bytes): Documents the crate as a `grep-matcher` implementation powered by Rust's regex engine and denies missing public documentation. It re-exports the error types, `RegexMatcher`, `RegexMatcherBuilder`, and `RegexCaptures`. The remaining implementation modules are private. This is the public crate entry point.
    - Tags: [api, regex, rust]
- `src/literal.rs` (Size : 39143 bytes): Defines `InnerLiterals` and an extractor that derives bounded literal sequences from regex HIR for a faster auxiliary line-search regex. It combines literals across concatenations and alternations, accounts for repetitions and character classes, and applies size, count, and quality heuristics to avoid weak or excessive candidates. Extraction is skipped when configuration or the compiled regex makes the extra optimization unnecessary or unsafe. Tests cover exact and inexact literals, complex expressions, and heuristic selection.
    - Tags: [literal-extraction, optimization, regex-hir, rust]
    - TODO/FIXME/NOTE: NOTE line 51 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 202 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 221 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 925 (exact marker `Note`)
- `src/matcher.rs` (Size : 26267 bytes): Implements `RegexMatcherBuilder` and `RegexMatcher`, exposing configuration options and the `grep-matcher::Matcher` operations backed by compiled regex automata. Building a matcher applies whole-line or word constraints, computes non-matching bytes, and may create a literal-based candidate-line regex. `RegexCaptures` adapts automata capture storage to the matcher capture interface. Embedded tests cover configuration, line terminators, captures, and candidate matching.
    - Tags: [captures, matcher-interface, regex, rust]
    - TODO/FIXME/NOTE: NOTE line 219 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 250 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 317 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 516 (exact marker `Note`)
    - TODO/FIXME/NOTE: FIXME line 637 (exact marker `FIXME`)
- `src/non_matching.rs` (Size : 5414 bytes): Computes a `ByteSet` of bytes guaranteed not to occur in any match by traversing HIR literals, classes, assertions, and composite expressions. Unicode classes are translated through UTF-8 byte sequences, while byte classes are handled as ranges. The result supports higher-level search-path decisions without claiming that a byte outside the set must match. Tests cover literals, classes, dots, and anchors. The file documents known limitations in anchor handling.
    - Tags: [byte-analysis, optimization, regex-hir, rust]
    - TODO/FIXME/NOTE: FIXME line 31 (exact marker `FIXME`)
    - TODO/FIXME/NOTE: FIXME line 150 (exact marker `FIXME`)
- `src/strip.rs` (Size : 6499 bytes): Transforms HIR so that it cannot match a configured ASCII line terminator, removing that byte from eligible character classes and rejecting literal occurrences that cannot be safely transformed. CRLF mode applies the transformation to both carriage return and line feed. Recursive handling preserves repetitions, captures, concatenations, and alternations, while empty classes that would result in invalid behavior produce an error. Unit tests cover these transformations and rejection cases.
    - Tags: [hir-transformation, line-terminator, regex, rust]
    - TODO/FIXME/NOTE: NOTE line 21 (exact marker `Note`)

---

## Links Child Folder docmaps
None.
# Related Features

Line-oriented regular-expression matching through the `grep-matcher` abstraction, including configuration-sensitive compilation and matcher optimizations.

# Agent Guidance

## Read When

Read this folder when determining the crate's packaging, user-facing purpose, license, or the location of its regex matcher implementation.

## Modify When

Modify package-level files when changing crate metadata, package guidance, or licensing documentation. For implementation changes, read `src/docmap.md` and the relevant source file.

## Avoid Modifying When

Avoid changing package metadata or licensing files for matcher behavior changes unless the package interface, build configuration, or licensing text itself must change.
