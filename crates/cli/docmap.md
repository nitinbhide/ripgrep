---
folder: "crates/cli"
generated_on: "2026-10-06"
num_files: 12
semantic_tags: [api, buffering, byte-handling, cargo, child-process, cli-utilities, color, compression, crate-documentation, crate-manifest, error-handling, error-reporting, escaping, glob-matching, hostname, human-readable-size, license, mit, parsing, pattern-parsing, platform-specific, process-management, rust, search, stdin-detection, stdout, streaming-io, system-information, terminal, unlicense, utf-8]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This folder is the standalone `grep-cli` crate, a library of common utilities for search-oriented command-line programs. Its manifest declares the crate metadata and dependencies, while its README describes the intended API and directs ripgrep consumers toward the higher-level `grep` facade. The implementation modules are indexed separately in `src/docmap.md`. The crate aims to support Windows, macOS, and Linux.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

The crate provides reusable support for terminal output, process execution, pattern and byte handling, decompression, and other CLI concerns. The top-level source index links to these facilities at the module level. License files record the project's dual-licensing terms.

## Technology Notes

The crate is written in Rust and uses Cargo workspace settings for its edition and minimum Rust version. Its dependencies include `bstr`, `globset`, `log`, and `termcolor`, with platform-specific dependencies for Windows and Unix.

# Folder Navigation

## Merged Child Folders
- `src/` —
  - Tags: [api, buffering, byte-handling, child-process, cli-utilities, color, compression, error-handling, error-reporting, escaping, glob-matching, hostname, human-readable-size, parsing, pattern-parsing, platform-specific, process-management, rust, stdin-detection, stdout, streaming-io, system-information, terminal, utf-8]. TODO/FIXME/NOTE: present; see indexed files.
  This folder implements the reusable Rust utility API exposed by the `grep-cli` crate. Its modules cover terminal output, process and stream helpers, input pattern handling, byte escaping, compression, and platform information. The code is designed for search-oriented command-line programs and contains focused unit tests alongside the implementations. Public exports are collected in `lib.rs`.
## Files
- `Cargo.toml` (Size : 848 bytes): Defines the `grep-cli` package metadata, documentation and repository URLs, Rust workspace edition/version settings, and dependencies. It includes conditional dependencies on `winapi-util` for Windows and `libc` for Unix. Tags: [cargo, crate-manifest, rust].
- `LICENSE-MIT` (Size : 1102 bytes): Contains the MIT license terms applicable to the crate. It establishes the conditions for use, modification, distribution, and warranty disclaimer. Tags: [license, mit].
- `README.md` (Size : 951 bytes): Introduces `grep-cli` as a portable utility library for search-oriented command-line applications and outlines its purpose and usage. It describes the library at a high level and points readers to docs.rs; it recommends the `grep` facade for most consumers. Tags: [cli-utilities, crate-documentation, rust]. TODO/FIXME/NOTE: NOTE line 18 (`NOTE`).
- `UNLICENSE` (Size : 1235 bytes): Contains the Unlicense dedication and terms for placing the crate's work in the public domain. It also includes the standard disclaimer of warranty. Tags: [license, unlicense].
- `src/decompress.rs` (Size : 20695 bytes): Provides builders and readers that match file paths against glob rules and stream decompressed content from external commands. `DecompressionMatcher` keeps matching rules and command arguments, while `DecompressionReaderBuilder` delegates process execution and falls back to reading the original file if no rule matches or a decompressor cannot be started. It documents default decompressor associations and customizable command resolution. Tags: [compression, glob-matching, process-management, streaming-io]. TODO/FIXME/NOTE: NOTE line 269 (`Note`); NOTE line 317 (`Note`); NOTE line 413 (`Note`); NOTE line 442 (`Note`).
- `src/escape.rs` (Size : 4423 bytes): Converts arbitrary byte sequences into readable escaped strings and reverses supported escapes into bytes. It exposes OS-string variants and tests control-byte, NUL, backslash, and invalid UTF-8 cases. Invalid hexadecimal forms are left as literal text rather than treated as escapes. Tags: [byte-handling, escaping, utf-8]. TODO/FIXME/NOTE: NOTE line 75 (`Note`).
- `src/hostname.rs` (Size : 3072 bytes): Provides a system hostname lookup returning an `OsString` and `io::Result`. Unix uses `gethostname` with a system-reported buffer limit and validates NUL termination; Windows uses the physical DNS hostname API. Unsupported platforms return an explicit error. Tags: [hostname, platform-specific, system-information].
- `src/human.rs` (Size : 4375 bytes): Parses byte-size strings with optional `K`, `M`, or `G` suffixes into `u64` byte counts. A structured `ParseSizeError` distinguishes malformed input, integer parsing failures, and overflow, with a user-readable `Display` implementation. Unit tests exercise supported suffixes and invalid input. Tags: [error-reporting, human-readable-size, parsing].
- `src/lib.rs` (Size : 11993 bytes): Defines the crate-level documentation and re-exports the utility API implemented by the sibling modules. Its documented capabilities include stdin detection, terminal-aware output, byte escaping, UTF-8 pattern validation, subprocess output, decompression, and size parsing. It also implements platform-specific readability heuristics for stdin and retains deprecated terminal-detection wrappers around `IsTerminal`. Tags: [api, cli-utilities, rust, stdin-detection, terminal].
    - TODO/FIXME/NOTE: NOTE line 69 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 160 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 255 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 274 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 287 (exact marker `Note`)
- `src/pattern.rs` (Size : 5934 bytes): Converts byte strings and OS strings into UTF-8 regular-expression patterns, reporting the first invalid byte offset through `InvalidPatternError`. It also reads newline-separated patterns from paths, stdin, or generic readers and adds source and line context to failures. The tests cover invalid UTF-8 in byte and Unix OS-string inputs. Tags: [error-reporting, pattern-parsing, utf-8]. TODO/FIXME/NOTE: NOTE line 118 (`Note`).
- `src/process.rs` (Size : 11460 bytes): Implements `CommandReader` and its builder for streaming a child process's stdout while retaining stderr for useful failures. The reader supports synchronous or asynchronous stderr collection, with asynchronous collection enabled by default to avoid a full stderr pipe blocking the child. `CommandError` represents spawn/I/O failures and stderr output. Tags: [child-process, error-handling, streaming-io]. TODO/FIXME/NOTE: NOTE line 125 (`Note`).
- `src/wtr.rs` (Size : 5020 bytes): Wraps terminal color writers with line-buffered and block-buffered stdout options. The default constructor chooses line buffering for a terminal and block buffering otherwise, and the wrapper forwards `Write` and `WriteColor` operations to the selected implementation. Tags: [buffering, color, stdout, terminal].

---

## Links Child Folder docmaps
None.
# Related Features

Reusable utilities consumed by ripgrep's core and other search-oriented command-line applications.

# Agent Guidance

## Read When

Changing the `grep-cli` crate API, its build metadata, or the common utility modules under `src`.

## Modify When

A change should be reusable by search-oriented CLI clients rather than being specific to ripgrep's search behavior.

## Avoid Modifying When

The change belongs to ripgrep's core flags, file traversal, or search execution.

## Dependency Graph

Not generated.
