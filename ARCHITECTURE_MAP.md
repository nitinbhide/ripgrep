# Architecture Map

This map is derived only from the generated root and folder docmaps.

## Overview

The repository is a Cargo workspace. The `rg` executable coordinates argument
handling, file traversal, searching, and output through reusable Rust crates.
The crate-level maps describe separable responsibilities for traversal,
matching, search, printing, command-line utilities, and the public `grep`
facade. Optional PCRE2 and index features are represented by separate crates
and core integration maps.

## Layers and Responsibilities

| Layer | Responsibilities | Navigation |
| --- | --- | --- |
| CLI entry and orchestration | Dispatch command modes, configure traversal/search, report errors and exit status | `crates/core/docmap.md` |
| Flag parsing and CLI documentation | Parse options and organize flag definitions, help, man-page content, and completions | `crates/core/flags/docmap.md` |
| Candidate traversal and filtering | Select haystacks, walk directories, and apply ignore, glob, and file-type rules | `crates/core/docmap.md` and `crates/ignore/docmap.md` |
| Matcher abstraction and engines | Define the matcher interface and provide Rust-regex, PCRE2, and glob matching | `crates/docmap.md`, `crates/regex/docmap.md` |
| Search execution | Apply matchers to input and handle line/context events, buffering, binary detection, and encoding | `crates/searcher/src/docmap.md` |
| Output and reporting | Format ordinary, summary, path, and JSON Lines results | `crates/printer/src/docmap.md` |
| Shared CLI support | Provide process, pattern, decompression, and terminal utilities | `crates/cli/docmap.md` |
| Public facade | Re-export component crates under a higher-level `grep` API | `crates/docmap.md` |
| Optional indexed search | Provide index storage/query support and feature-gated CLI integration | `crates/docmap.md`, `crates/core/docmap.md` |

## Architectural Patterns

- Matcher implementations conform to a shared matcher abstraction, allowing
  search code to use different engines.
- Search execution reports matches and contextual events to sinks; printer
  implementations format those results.
- File walking and search may use sequential or parallel paths, as described
  in the core and ignore crate maps.
- `grep` offers a facade over component crates.

## Constraints Explicitly Documented

- The `unstable-index` feature is described in the root manifest as in active
  development and potentially having serious bugs.
- The PCRE2, regex, searcher, printer, and matcher README summaries recommend
  most consumers use the `grep` facade rather than depending on individual
  component crates directly.
- The `core` README describes that crate as the executable core rather than an
  intended independent library.

## Not Available in the Generated Docmaps

- A formal architecture decision record set and a complete architectural
  constraint specification are not identified.
- No dependency graph is generated; dependency extraction is explicitly
  deferred.
