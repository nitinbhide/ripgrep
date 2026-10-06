---
folder: "crates/core/flags"
generated_on: "2026-10-06"
num_files: 21
semantic_tags: [argument-parsing, bash, build-metadata, cli, completions, configuration, cpu-features, documentation, documentation-generation, documentation-metadata, encodings, fish, flags, help, man-page, markup, parsing, pcre2, powershell, roff, rust, search-configuration, shared-interface, shell, shell-completion, template, text, typed-configuration, version, zsh]
todos_present: true
dependencies: []
---

# Folder Overview

## Purpose
This folder defines ripgrep's command-line flag model, parser, and conversion from raw user arguments into validated search configuration. It separates low-level values captured from individual flags from higher-level settings that require filesystem, environment, or matcher setup. Flag metadata is centralized so it can also drive help, manual, and shell-completion output. Configuration-file arguments are loaded through the `RIPGREP_CONFIG_PATH` mechanism.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

The modules describe available flags and how they update low-level state, parse command-line names and values, and build the high-level `HiArgs` used by search execution. They also apply flag override semantics, special early-exit modes, and configuration arguments. Child modules render flag documentation and provide shell completions.

## Technology Notes

This is Rust code using typed enums and structs to represent CLI settings, `anyhow` for construction errors, and `LazyLock`/`OnceLock`-backed shared flag/parser metadata. The completion and documentation subfolders generate shell or help output from the flag definitions.

# Folder Navigation

## Merged Child Folders
- `complete/` —
  - Tags: [bash, cli, completions, encodings, fish, powershell, rust, shell, shell-completion, zsh]. TODO/FIXME/NOTE: present; see indexed files.
  This folder provides shell completion resources and generators for ripgrep's command-line flags. Bash, Fish, and PowerShell completion text is generated from the shared flag metadata, while the Zsh completion is maintained as a detailed hand-written script. Shared encoding aliases and Fish helper logic are included by the generators. The files must stay aligned with the flags in the parent module.
- `doc/` —
  - Tags: [build-metadata, cli, cpu-features, documentation, documentation-generation, help, man-page, markup, pcre2, roff, rust, template, text, version]. TODO/FIXME/NOTE: present; see indexed files.
  This folder renders ripgrep's flag metadata into user-facing help text, a roff man page, and build/version descriptions. The Rust generators draw descriptions and categories from the shared flag definitions, while the three templates provide the output layouts. This keeps documentation generation tied to the executable's actual supported options. Feature-gated index documentation is replaced with a not-supported notice when indexing is unavailable.
## Files
- `config.rs` (Size : 4961 bytes): Reads `RIPGREP_CONFIG_PATH` and converts each nonblank, non-comment line into one shell argument. It reports read and parse errors through ripgrep's message mechanism while preserving successfully parsed arguments, and tests normal and platform-dependent invalid-byte handling. Tags: [configuration, parsing, rust].
- `defs.rs` (Size : 254514 bytes): Defines the complete flag metadata table and individual `Flag` implementations, including each option's names, aliases, values, categories, descriptions, and effects on low-level arguments. The ordered `FLAGS` list is the shared source used by parsing and generated help, man-page, and completion output. Its extensive documentation strings are also the source material for user-facing flag descriptions. Tags: [cli, documentation-metadata, flags, rust]. TODO/FIXME/NOTE: NOTE lines 5, 964, 1346, 1357, 1365, 1421, 1428, 1484, 1800, 2273, 2442, 2616, 2871, 2880, 3029, 3067, 3370, 3779, 4282, 4464, 4620, 5082, 5181, 5477, 5741, 6398, 6467, 6611, 6725, 6827, 6921, 7269, 7338, 7364, 7424, 7753 (exact marker `Note`).
- `hiargs.rs` (Size : 60086 bytes): Converts parsed low-level values into `HiArgs`, resolving settings that require completed parsing or environment state, such as globs, pattern sources, output configuration, and search construction. It provides the accessors and builders used by core search, traversal, and printer code. It also rejects combinations unsupported by the optional indexing mode. Tags: [argument-parsing, rust, search-configuration, typed-configuration]. TODO/FIXME/NOTE: NOTE lines 969, 984, 1131 (exact marker `Note`).
- `lowargs.rs` (Size : 27039 bytes): Defines the typed low-level argument collection and enums for search, output, indexing, file selection, and special modes. This representation stays close to CLI input and leaves environment-dependent construction to `HiArgs`. Its methods encode mutually exclusive command modes and flag override semantics. Tags: [argument-parsing, cli, rust, typed-configuration]. TODO/FIXME/NOTE: NOTE lines 151, 443, 515, 585, 619 (exact marker `Note`).
- `mod.rs` (Size : 12397 bytes): Defines flag categories, the `Flag` interface, completion metadata, and shared module exports for configuration, definitions, parsing, and argument representations. This module establishes the contract used by each option implementation and by help/completion generators. It also holds shared indexing capability information. Tags: [cli, flags, rust, shared-interface]. TODO/FIXME/NOTE: NOTE lines 65, 262 (exact marker `Note`).
- `parse.rs` (Size : 18269 bytes): Parses OS-string command-line arguments into low-level typed state, then converts that state into `HiArgs` unless a special mode should short-circuit processing. It supports configuration-file arguments, logging and message-level setup, and fast lookup of flag metadata. The `Parser` maintains name-to-flag mappings, and test-only entry points exercise raw argument parsing. Tags: [argument-parsing, cli, rust, typed-configuration].
- `complete/bash.rs` (Size : 2877 bytes): Builds Bash completion output from the central flag metadata, including long, short, and negated option names. It creates file-completion cases for ordinary values and choice-completion cases when flag metadata supplies choices, then inserts them into the Bash function template. Tags: [bash, cli, completions, rust]. TODO/FIXME/NOTE: NOTE line 61 (`Note`).
- `complete/encodings.sh` (Size : 1482 bytes): Lists encoding aliases used as completion candidates by the shell completion implementations. Its comments identify the source list and explain that shell brace expansion is relied on. Tags: [encodings, shell-completion].
- `complete/fish.rs` (Size : 2740 bytes): Generates Fish completion declarations from shared flag metadata and prepends the helper prelude. It chooses argument completion behavior based on the flag's completion type, including file, executable, filetype, encoding, and enumerated choices, and emits negated forms where available. Tags: [cli, completions, fish, rust].
- `complete/mod.rs` (Size : 226 bytes): Declares the Bash, Fish, PowerShell, and Zsh generator modules and embeds shared encoding candidates from `encodings.sh`. It acts as the common module interface for completion generation. Tags: [cli, completions, rust].
- `complete/powershell.rs` (Size : 2792 bytes): Generates a PowerShell native argument completer for `rg`, formatting completions from the common flag list. It emits long names, short aliases, and negated names, with flag descriptions attached to each result. Its source notes that the current completions reflect the older Clap 2-era output. Tags: [cli, completions, powershell, rust]. TODO/FIXME/NOTE: NOTE line 41 (`Note`).
- `complete/prelude.fish` (Size : 945 bytes): Defines the Fish helper that detects options already present in the command line and incorporates arguments from the ripgrep config file. The helper caches config contents for the shell session and recognizes long and short option spellings. Tags: [fish, shell-completion].
- `complete/rg.zsh` (Size : 29547 bytes): Contains the hand-maintained Zsh completion function and its option reference material. The function groups options, handles aliases and negations selectively, and uses completion context for relevant values; its comments describe manual maintenance requirements for negated flags. Tags: [cli, completions, shell, zsh]. TODO/FIXME/NOTE: NOTE line 25 (`Note`).
- `complete/zsh.rs` (Size : 1286 bytes): Generates Zsh completion output by substituting encoding candidates and hyperlink alias descriptions into the hand-maintained `rg.zsh` resource. It obtains the hyperlink aliases from the printer crate rather than duplicating their descriptions. Tags: [cli, completions, rust, zsh].
- `doc/help.rs` (Size : 9973 bytes): Produces condensed and detailed help text from the shared flag list, grouping flags by category and formatting aligned flag and description columns. It uses short and long help templates and replaces the indexing section with a disabled-feature message when appropriate. Tags: [cli, documentation-generation, help, rust].
- `doc/man.rs` (Size : 4053 bytes): Generates ripgrep's complete roff man page by grouping flag descriptions by category and inserting them into the man-page template. It renders custom flag markup into roff references and adds standard negation descriptions for switch flags. Tags: [documentation-generation, man-page, roff, rust].
- `doc/mod.rs` (Size : 1293 bytes): Exposes the help, man-page, and version modules and implements the shared renderer for custom `\tag{...}` markup in flag documentation. The renderer walks each occurrence and delegates replacement text generation to the caller. Tags: [documentation-generation, markup, rust].
- `doc/template.long.help` (Size : 1602 bytes): Supplies the static layout for verbose `--help` output, with named placeholders for flag categories and explanatory sections. The generator fills these slots from the flag definitions. Tags: [cli, help, template, text].
- `doc/template.rg.1` (Size : 14316 bytes): Supplies the roff structure and explanatory content for the `rg(1)` manual, including overview, usage, regex syntax, options, and configuration sections. Category placeholders are filled from the Rust man-page generator. Tags: [documentation, man-page, roff, template]. TODO/FIXME/NOTE: NOTE line 92 (`Note`); NOTE line 277 (`Note`).
- `doc/template.short.help` (Size : 821 bytes): Supplies the compact `-h` output layout, defining usage text and insertion points for option categories. It is formatted separately from the long-help template to support a concise display. Tags: [cli, help, template, text].
- `doc/version.rs` (Size : 5707 bytes): Builds numeric, short, and detailed version strings from the package version, optional Git hash, enabled features, SIMD target features, and PCRE2 availability. Compile-time and runtime CPU feature reporting are separated, and PCRE2's version/JIT state is reported when compiled in. Tags: [build-metadata, cpu-features, pcre2, rust, version]. TODO/FIXME/NOTE: NOTE line 127 (`note`).
---

## Links Child Folder docmaps
None.
# Related Features

Command-line options, configuration-file overrides, generated help and version display, and shell completions.

# Agent Guidance

## Read When

Changing a flag, argument parsing, option override behavior, search configuration, completion generation, or help text.

## Modify When

The CLI contract or the conversion from user-provided options into ripgrep's runtime settings must change.

## Avoid Modifying When

The change is limited to search algorithms or output implementation and does not alter option semantics.

## Dependency Graph

Not generated.
