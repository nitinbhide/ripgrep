---
folder: "crates/printer/src"
generated_on: "2026-10-06"
num_files: 13
semantic_tags: [formatting, grep-printer, hyperlinks, path-encoding, path-formatting, path-matching, rust, search-output, terminal-output, uri-conversion]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This folder implements the printer crate's output APIs and their shared formatting support. Its modules cover standard grep-like output, JSON serialization, aggregate summaries, path output, colors, statistics, and byte/path utilities. The public surface is re-exported by `lib.rs`, while implementations use `grep-searcher` sinks to receive matches and context. Hyperlink parsing and alias definitions are maintained in the child folder indexed at `hyperlink/docmap.md`.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

Translate search events into configurable text or JSON output, with shared path, color, hyperlink, replacement, and statistics support. The folder also contains the crate's public API declarations and test assertion macro.

## Technology Notes

The implementation is Rust and integrates with `grep-searcher`, `grep-matcher`, `termcolor`, `bstr`, and optional `serde`/`serde_json` support. Printer output can include terminal colors and hyperlinks when the writer supports them.

# Folder Navigation

## Merged Child Folders
- `hyperlink/` —
  This folder contains hyperlink format configuration and the built-in alias table used by printer output. It supports templates whose variables are interpolated from paths, line positions, and process environment information. The format and environment APIs are exposed through the parent crate's public re-exports. The alias file supplies named presets for common editor and terminal URL schemes.
## Files
- `color.rs` (Size : 13554 bytes): Defines errors for invalid color specifications, user-provided color specifications, and merged `ColorSpecs` used by printer output. It parses supported output targets and style/color attributes and supplies conservative defaults. The resulting specs are consumed by the crate's standard, summary, and path printers. Errors implement Rust's standard error and display interfaces.
    - Tags: [color, configuration, rust, terminal-output]
- `counter.rs` (Size : 2364 bytes): Wraps a writer and counts successfully written bytes, retaining both the current count and the total across resets. It forwards `Write` and `WriteColor` operations, including color and hyperlink capabilities, to the wrapped writer. `reset_count` moves the current count into the accumulated total. Printer modules use it where output byte statistics are needed.
    - Tags: [io, rust, statistics, writer]
- `json.rs` (Size : 38745 bytes): Implements the configurable JSON printer and its sink integration, including JSON Lines output, optional pretty formatting, begin/end messages, and replacement handling. The builder freezes configuration into a printer that processes match and context callbacks from `grep-searcher`. It uses the `jsont` module's borrowed serialization data types to encode message payloads. The printer also tracks written bytes and exposes its writer through its API.
    - Tags: [json, json-lines, printer, rust, serialization]
    - TODO/FIXME/NOTE: line 270: ``///   starting offsets. Note that it is possible for this array to be empty,``
    - TODO/FIXME/NOTE: line 300: ``///   their starting offsets. Note that it is possible for this array to be``
- `jsont.rs` (Size : 10240 bytes): Defines the borrowed message and data structures serialized by the JSON printer. It models begin, end, match, and context events and implements `serde::Serialize` without defining deserialization. The structures borrow paths and result bytes to avoid unnecessary allocation during serialization. Its message shape supplies the structured payloads consumed by `json.rs`.
    - Tags: [json, rust, serialization]
- `lib.rs` (Size : 3655 bytes): Documents the printer crate's three primary output styles and demonstrates standard output with a regex matcher and searcher. It re-exports the standard, summary, path, color, hyperlink, and statistics APIs, plus JSON types when the `serde` feature is enabled. The module declarations keep implementation details private. It also defines the maximum look-ahead used by multiline replacement logic.
    - Tags: [crate-api, documentation, rust]
    - TODO/FIXME/NOTE: line 86: `// Note that this kludge is only active in multi-line mode.`
- `macros.rs` (Size : 694 bytes): Defines the test-only exported `assert_eq_printed!` macro. The macro compares expected and actual rendered text and, on mismatch, prints both values in a visibly delimited panic message. Its conditional compilation limits it to tests. It supports readable assertions for printer output.
    - Tags: [macro, rust, testing]
- `path.rs` (Size : 6426 bytes): Implements `PathPrinterBuilder` and `PathPrinter` for emitting paths without executing a search. Builder configuration controls colors, hyperlinks, path separators, and terminators. The printer normalizes paths through the shared path utility and writes styling or hyperlink spans when its writer supports them. This offers path output consistent with the other printers.
    - Tags: [hyperlinks, path-output, printer, rust, terminal-color]
- `standard.rs` (Size : 140275 bytes): Implements the configurable grep-like `Standard` printer and its `Sink` behavior for match and context events. Its builder controls headings, path and line display, per-match output, replacements, separators, color, hyperlinks, and statistics, while search configuration supplies additional context. Shared utilities handle path formatting, match iteration, and replacement. The implementation also includes output accounting and supports the crate's standard printer API.
    - Tags: [context-lines, grep-output, printer, rust, terminal-color]
    - TODO/FIXME/NOTE: line 1569: `/// Note that this doesn't just return whether the searcher is in multi`
- `stats.rs` (Size : 5008 bytes): Defines `Stats`, an aggregate record for elapsed time, searches, searches with matches, bytes searched and printed, matched lines, and match counts. It provides getters and methods to add each measure. `Add` and `AddAssign` combine independent records, and the `serde` feature enables serialization. Printers use the record to report accumulated search results.
    - Tags: [aggregation, rust, serde, statistics]
- `summary.rs` (Size : 41480 bytes): Implements the summary printer and its builder for count, path, and quiet output modes. It handles per-search sink events and can include statistics, configurable separators, colors, and hyperlinks. `SummaryKind` describes modes including counting lines or matches and selecting paths based on whether a match occurred. Its output can provide aggregate information without printing matching lines.
    - Tags: [aggregate-output, printer, rust, search-results]
    - TODO/FIXME/NOTE: line 86: ``/// Note that if `stats` is enabled, then searching continues in order to``
    - TODO/FIXME/NOTE: line 92: ``/// Note that if `stats` is enabled, then searching continues in order to``
    - TODO/FIXME/NOTE: line 262: ``/// Note that some output modes, such as `CountMatches`, automatically``
    - TODO/FIXME/NOTE: line 536: `/// Note that this doesn't just return whether the searcher is in multi`
- `util.rs` (Size : 21199 bytes): Provides internal helpers shared across printer implementations, including reusable match replacement storage, contextual match iteration, path formatting, and numeric formatting. The replacement helper collects captures and output spans while limiting allocation through retained buffers. Other routines adapt searcher context and path data for printer needs. `standard.rs`, `summary.rs`, and `path.rs` use these shared facilities.
    - Tags: [formatting, io, path, replacement, rust]
    - TODO/FIXME/NOTE: line 342: `/// Note that a hyperlink may not be able to be created from a path.`
- `hyperlink/aliases.rs` (Size : 2621 bytes): Defines a sorted table of named hyperlink aliases, including the default platform-aware file scheme and formats for Cursor, grep+, Kitty, MacVim, TextMate, VS Code, VS Code Insiders, and VSCodium. Each entry supplies a description and URL template, with display priority assigned to the default and disabled aliases. Small constructors create ordinary and prioritized `HyperlinkAlias` values. The table is consumed by the hyperlink module.
    - Tags: [hyperlinks, path-matching, rust, terminal-output]
- `hyperlink/mod.rs` (Size : 42342 bytes): Defines the public hyperlink configuration, format, environment, alias, and error APIs, along with internal interpolation logic. Formats parse variables and aliases into reusable parts; environment values such as host information are captured for interpolation. The module writes link spans through `termcolor::WriteColor` and delegates named presets to `aliases.rs`. Printer builders expose these settings for path and match output.
    - Tags: [hyperlinks, path-encoding, rust, uri-conversion]
    - TODO/FIXME/NOTE: NOTE line 800 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 807 (exact marker `note`)

---

## Links Child Folder docmaps
None.
# Related Features

Standard, JSON Lines, summary, and path output; terminal colors; hyperlink formatting; replacements; and printer statistics.

# Agent Guidance

## Read When

Changing result rendering, printer configuration, output serialization, or shared formatting and statistics helpers.

## Modify When

Implementing or adjusting printer behavior, adding an output format, or changing how match/context events are translated to output.

## Avoid Modifying When

The requested change belongs to file traversal, pattern matching, or search-buffer processing rather than output.
