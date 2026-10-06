---
folder: "/"
generated_on: "2026-10-06"
num_files: 28
semantic_tags: [bash, benchmarking, benchmark-runner, cargo, ci, cli, command-line, command-line-search, documentation, examples, fuzzing, glob, homebrew, libfuzzer, linux, macos, manifest, packaging, python, release, ruby, rust, search-performance, shell, testing, utf-8, windows, zsh]
todos_present: true
dependencies: []
---

# Repository Overview

ripgrep is a cross-platform command-line tool for recursively searching files with regular expressions. Its default search behavior respects ignore files and filters hidden and binary files, while its user documentation describes configurable matching, output, encoding, and preprocessing options. The repository is a Cargo workspace with a command-line executable and reusable Rust crates for traversal, matching, searching, and output. Tests, fuzz targets, CI/release helpers, packaging metadata, and historical benchmarks support development and distribution.

- Repository purpose: provide a fast, configurable, line-oriented recursive search utility.
- Business domain: command-line text search and related Rust libraries.
- Overall architecture summary: a Rust workspace separates the executable's orchestration from matcher, traversal, searcher, printer, CLI utility, and optional PCRE2/indexing crates.

## Technology Summary

Detected:

- Languages: Rust, Python, shell, Ruby, XML, and Markdown documentation.
- Frameworks and libraries: Rust regex crates, optional PCRE2 integration, glob matching, byte/string utilities, and terminal output crates.
- Databases: Not identified in the generated repository summaries.
- Build systems: Cargo workspace with a Rust 2024 edition and a declared minimum Rust version of 1.96.
- Testing frameworks: Rust unit and integration tests, Cargo fuzz/libFuzzer, and CI shell checks.

## Architecture Summary

The `rg` executable coordinates argument parsing, file traversal, search execution, and output through modular workspace crates. The matcher interface separates search orchestration from regex implementations, while the ignore-aware walker and searcher handle candidate files and input processing. Printer crates provide human-readable and JSON Lines output, and optional crates add PCRE2 and indexed-search support. Folder maps identify each module's implementation and associated tests.

## Business Capability Summary
The repository supports recursive command-line search with automatic and explicit file filtering, configurable regex matching, and multiple output modes. Its documentation also describes multiline search, compressed input, non-UTF-8 encodings, preprocessing, and configuration files. Optional PCRE2 integration adds regex features not provided by the default engine. The repository includes packaging and benchmark tooling for release and performance workflows.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
# Module Dependency Graph

Dependency graph generation is reserved for a future requirement and is not included in this index.
The `dependencies` metadata field remains an empty list until dependency extraction is implemented.

# Repository Navigation

## Specialized Cross Navigation Maps

- `FEATURE_MAP.md` — Repository capabilities with docmap-supported source, tests, documentation, and markers.
- `ARCHITECTURE_MAP.md` — Component responsibilities, architectural patterns, and explicitly documented constraints.
- `TECHNOLOGY_MAP.md` — Languages, libraries, build tooling, and version information described by docmaps.
- `TESTING_MAP.md` — Test suites, described coverage areas, fixtures, and CI test checks.
- `CHANGE_IMPACT_MAP.md` — Common change scenarios mapped to files and docmaps explicitly identified in the hierarchy.

## Merged Child Folders
`docmap.md` content from small folders is incorporated here only after every folder index has first been written in its source directory.
- `benchsuite/` —
  This folder contains the benchsuite runner used to compare command-line search tools and an archive of captured benchmark runs. The runner defines searches over Linux and subtitle corpora, invokes external search commands, measures repeated executions, and reports timing and output counts. The `runs` child keeps dated raw data, summaries, and available environment notes. Read the runner for benchmark definitions and a specific run’s docmap for its captured evidence.
- `ci/` —
  This folder contains scripts used by continuous integration and release workflows. It checks consistency between ripgrep's command-line options and its Zsh completion definitions, prepares Linux build environments, computes release checksums, and provides shared build-target helpers. The scripts cover Linux, macOS, and cross-compilation-related target handling.
- `fuzz/` —
  This folder defines a Cargo fuzzing package and documents how to install and run its fuzz targets. The package configures `cargo-fuzz`, builds the `fuzz_glob` target, and enables the `arbitrary` feature of the local `globset` crate. Its README explains how arbitrary inputs help find conversion and stability problems that are not prevented by Rust's type system. The target implementation summary is merged into this root index.
- `fuzz/fuzz_targets/` —
  This folder contains the libFuzzer harness for checking glob parsing behavior. Its sole target receives arbitrary string inputs, ignores strings rejected by either constructor, and asserts equivalence for accepted inputs. It also checks that the parsed glob renders back to the original input string. The Cargo package manifest in the parent folder registers this target as `fuzz_glob`.
- `pkg/` —
  This folder contains platform-specific packaging metadata and documentation. The Homebrew formula packages prebuilt macOS and Linux release archives, while the Windows subfolder documents and configures application-manifest settings. There are no direct files in this folder in the retained inventory. The platform-specific contents are indexed by the child folder maps.
- `pkg/brew/` —
  This folder defines the Homebrew formula used to install ripgrep release binaries. The formula chooses a prebuilt archive according to whether Homebrew is running on macOS or Linux and pins the release version and checksums. Its install step places the executable, man page, and shell completion files in their Homebrew destinations. The formula also declares a conflict with the `ripgrep` formula.
- `pkg/windows/` —
  This folder documents and configures Windows application-manifest settings for ripgrep. The manifest declares supported Windows versions, enables the UTF-8 active code page, and enables long-path awareness. The README explains how the manifest is linked into the final binary and identifies the build limitation stated by the documentation. Together, the files describe the Windows-specific settings and their build context.
- `scripts/` —
  This folder contains a script that extracts example source files from Rust documentation code blocks. It reads a cookbook source file, recognizes fenced Rust or shortcode code blocks with marker lines, strips marker comment prefixes, and writes extracted content into a specified examples directory. The script exposes command-line options for selecting the source file and output directory. Its defaults point to the cookbook and grep example locations.
## Folders
- `benchsuite/runs/docmap.md` — Index to dated benchmark archives, each containing raw measurements and summaries, with setup or version notes where recorded.
- `crates/docmap.md` — Rust workspace crate indexes for command execution, traversal, matching, searching, and output.
- `tests/docmap.md` — CLI integration suites, shared test support, fixture data, and index-feature cases.
## Files
- `AI_POLICY.md` : Defines the project's policy for AI-assisted contributions, including human responsibility for published code and communication. It explains expectations for issue and pull-request authors and requires AI context in maintainer comments to be disclosed. It states that autonomous agents are not allowed to contribute to the project. The policy is the source of contribution-specific AI guidance.
    - Size : 1916 bytes
    - Tags: [ai-policy, contribution-guidance, project-policy]

- `build.rs` : Configures Windows MSVC linker arguments to embed the application manifest and enable long-path support. It also obtains a short Git revision and exposes it to the build as `RIPGREP_BUILD_GIT_HASH`. Missing Git output or command execution is reported as a Cargo warning rather than blocking the build. This build script connects package configuration to platform-specific linker behavior and version metadata.
    - Size : 2307 bytes
    - Tags: [build-script, cargo, rust, windows]

- `Cargo.lock` : Records resolved versions, sources, checksums, and package relationships for the Rust workspace. Its entries include the application and its library crates as well as registry dependencies. Cargo marks the file as generated and not intended for manual editing. It provides a reproducible dependency-resolution snapshot for builds.
    - Size : 14142 bytes
    - Tags: [cargo, dependency-lockfile, rust]

- `Cargo.toml` : Defines the `ripgrep` package and the workspace members for its Rust crates. It sets the workspace edition to Rust 2024 and the minimum supported Rust version to 1.96, and configures the `rg` binary, integration tests, features, and release profiles. Package dependencies and Debian packaging metadata are also declared here. This is the primary workspace and executable build configuration.
    - Size : 3670 bytes
    - Tags: [cargo, package-configuration, rust, workspace]

- `CHANGELOG.md` : Records release history, grouped by version with platform changes, performance improvements, feature enhancements, and bug fixes. Recent entries describe improvements to ignore matching, line buffering, command-line options, and platform support. The document provides historical context for behavior changes and release notes. A top-level unreleased section is present.
    - Size : 91904 bytes
    - Tags: [changelog, release-history, rust]
    - TODO/FIXME/NOTE: line 211: `todo!()`; line 337: `note`; line 365: `note`; line 576: `note`; line 584: `note`; line 821: `note`; line 962: `note`; line 1109: `note`; line 1278: `note`; line 1457: `note`; line 1653: `note`; line 1668: `note`; line 1804: `note`; line 1814: `note`; line 1830: `note`

- `CONTRIBUTING.md` : Directs contributors to follow the repository's AI Policy for AI use in contributions. It says contributions that do not follow that policy will be closed. The document is a short entry point to contribution-specific guidance. The linked policy contains the detailed requirements.
    - Size : 221 bytes
    - Tags: [ai-policy, contribution-guidance, documentation]

- `COPYING` : States that the project is dual-licensed under the Unlicense and MIT licenses. It directs users to choose either license for use of the code. The file is a short pointer to the full license texts. Those complete texts are provided in the neighboring license files.
    - Size : 129 bytes
    - Tags: [license, mit, unlicense]

- `FAQ.md` : Answers common questions about ripgrep's behavior, configuration, output, installation, and platform-specific usage. Topics include shell completion, encodings, compressed and multiline searches, PCRE2, colors, path behavior, and compatibility with grep-like tools. It points readers to the guide and changelog for further detail. The document serves as troubleshooting and feature-reference material.
    - Size : 43306 bytes
    - Tags: [faq, troubleshooting, user-documentation]
    - TODO/FIXME/NOTE: line 83: `Note`; line 138: `Note`; line 149: `note`; line 395: `Note`; line 423: `Note`; line 633: `note`; line 741: `note`; line 894: `Note`

- `GUIDE.md` : Introduces ripgrep's command-line search model and documents its user-facing capabilities. Sections cover basic patterns, recursive search, automatic and manual filtering, replacements, configuration, encodings, binary data, preprocessing, and common options. Examples explain command behavior and platform considerations. This is the main in-depth usage guide.
    - Size : 41920 bytes
    - Tags: [configuration, filtering, regex, search, user-documentation]
    - TODO/FIXME/NOTE: line 63: `Note`; line 148: `Note`; line 251: `Note`; line 292: `Note`; line 303: `Note`; line 535: `note`; line 617: `note`; line 763: `Note`; line 808: `Note`; line 851: `Note`

- `HomebrewFormula` : Contains the literal text `pkg/brew`. Its purpose is not explained by the file contents alone. The adjacent Homebrew package map describes the formula under `pkg/brew`. This entry has low confidence because the file is only eight bytes long.
    - Size : 8 bytes
    - Tags: [low-confidence, packaging]
    - Confidence: low

- `LICENSE-MIT` : Contains the MIT License terms and the project's 2015 Andrew Gallant copyright notice. It permits use, modification, distribution, sublicensing, and sale subject to retaining the notice. It disclaims warranties and liability. This is one of the two licenses identified by `COPYING`.
    - Size : 1102 bytes
    - Tags: [license, mit]

- `README.md` : Introduces ripgrep as a cross-platform, line-oriented recursive search tool and explains its default respect for ignore rules and automatic filtering. It compares example search workloads, describes the regex and traversal strategies, and links to installation instructions and further documentation. The README also summarizes supported encodings, compressed inputs, preprocessing, configuration, and optional PCRE2 use. It is the primary project overview and entry point for user documentation.
    - Size : 22140 bytes
    - Tags: [command-line-search, documentation, regex, rust]
    - TODO/FIXME/NOTE: line 217: `Note`; line 432: `Note`; line 434: `Note`; line 468: `NOTE`

- `RELEASE-CHECKLIST.md` : Lists the maintainer steps for preparing a ripgrep release, from dependency review and changelog updates through packaging, CI, signing, and publication. It identifies crate release checks and the release ordering described by the project. The checklist also includes the required product blurb for release notes and Homebrew checksum updates. It is operational release documentation.
    - Size : 2935 bytes
    - Tags: [cargo, release-process, documentation]
    - TODO/FIXME/NOTE: line 55: `Note`

- `rustfmt.toml` : Configures Rust formatting with a 79-character maximum width and the small-heuristics setting `max`. It selects Rust edition 2024 for formatting. These settings are consumed by rustfmt rather than by the runtime application. The file is the repository's Rust formatting configuration.
    - Size : 64 bytes
    - Tags: [configuration, formatting, rust, rustfmt]

- `UNLICENSE` : Provides the Unlicense public-domain dedication and terms. It grants broad rights to use, copy, modify, publish, compile, sell, and distribute the software. It disclaims warranties and liability. This is the second license identified by `COPYING`.
    - Size : 1235 bytes
    - Tags: [license, public-domain, unlicense]
- `benchsuite/benchsuite` (Size : 48003 bytes): Implements the Python command-line benchmark runner for comparing search utilities on Linux and subtitle corpora. Benchmark definitions cover literal, case-insensitive, word, alternation, regex, and Unicode searches, with commands for ripgrep and other available search tools. `Benchmark`, `Command`, and `Result` coordinate command execution, repeated samples, timing, output-line counts, and result statistics. The CLI supports corpus selection/download, benchmark filtering and iteration settings, and writes readable summaries plus optional raw CSV rows.
    - Tags: [benchmarking, command-line-tool, performance-measurement, python]
    - TODO/FIXME/NOTE: NOTE line 513 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 675 (exact marker `Note`)
    - TODO/FIXME/NOTE: NOTE line 1196 (exact marker `Note`)
- `ci/sha256-releases` (Size : 621 bytes): Accepts a release version and downloads the Linux/macOS binary archives and source archives to calculate and print SHA-256 checksums. The two nested loops enumerate architecture and target combinations, then a second loop handles ZIP and tar.gz source formats. Its inputs and output format are expressed directly in the shell script. The script has no additional argument beyond the required version.
    - Tags: [checksums, release, shell, verification]
- `ci/test-complete` (Size : 2969 bytes): Runs the built `rg` executable's help output through option extraction and compares the result with the options defined by the Zsh completion function. It locates release or debug binaries and the completion source relative to the script, then fails if either input is missing or the option lists differ. The script uses Zsh extended globbing and a temporary-process substitution to obtain completion arguments. It is a consistency test for CLI help and shell completion.
    - Tags: [completion, shell, testing, validation]
- `ci/ubuntu-install-packages` (Size : 564 bytes): Installs the system packages used by Ubuntu-based build/test environments. It detects whether `sudo` is available, installs it when needed, then updates apt metadata and installs zsh, compression tools, musl tooling, and a C++ compiler. The comments explain the script's use in minimal environments. Package installation is performed without recommended extras.
    - Tags: [ci, linux, package-installation, shell]
- `ci/utils.sh` (Size : 2069 bytes): Defines shared Bash helpers for CI build and target selection. `cargo_out_dir` finds the most recent ripgrep build stamp, while other functions derive host, architecture, GCC prefix, operating-system predicates, and whether a target uses musl. `builder` selects `cross` for x86_64 musl targets and otherwise selects Cargo. The helpers use the CI environment variables `TRAVIS_OS_NAME` and `TARGET`.
    - Tags: [build-support, ci, shell, target-configuration]
- `fuzz/Cargo.lock` (Size : 4784 bytes): Records resolved package versions, registry sources, checksums, and dependency entries for the fuzz package and its Rust crates. The lockfile includes the local `fuzz` and `globset` packages alongside crates such as `libfuzzer-sys` and `arbitrary`. It is Cargo-generated and explicitly marked as not intended for manual editing. It is a resolution snapshot rather than explanatory package documentation.
    - Tags: [cargo, dependency-lockfile, rust]
- `fuzz/Cargo.toml` (Size : 437 bytes): Declares the unpublished Rust package named `fuzz`, its edition, and cargo-fuzz metadata. It configures a `fuzz_glob` binary at `fuzz_targets/fuzz_glob.rs` with test and documentation generation disabled, and sets release debug information. The manifest declares `libfuzzer-sys` and the local `globset` crate with its `arbitrary` feature. A single-member workspace prevents this manifest from interfering with the surrounding workspace.
    - Tags: [cargo, cargo-fuzz, package-configuration, rust]
- `fuzz/README.md` (Size : 1655 bytes): Documents fuzz testing's role in generating arbitrary inputs to expose stability and conversion problems. It gives installation instructions for `cargo-fuzz`, explains how to list targets, and shows how to run a named target. The examples also show `-max_total_time` for bounding a run, and the text explains that a discovered failure returns a non-zero status and displays the input. It mentions checking object conversions in both directions as a fuzzing use case.
    - Tags: [fuzzing, libfuzzer, rust, testing]
    - TODO/FIXME/NOTE: NOTE line 41 (exact marker `Note`)
- `fuzz/fuzz_targets/fuzz_glob.rs` (Size : 531 bytes): Defines a libFuzzer target whose input is an arbitrary string interpreted as a glob. It attempts to construct a `Glob` using both `Glob::new` and `FromStr`, returning early if either parse fails. For strings accepted by both paths, it asserts the resulting values are equal and that `Glob::glob()` returns the original string. These assertions encode the target's parser consistency and round-trip invariants.
    - Tags: [fuzzing, glob-matching, libfuzzer, rust]
- `pkg/brew/ripgrep-bin.rb` (Size : 827 bytes): Defines the `RipgrepBin` Homebrew formula and pins it to version `15.0.0`. It selects macOS or Linux release tarballs with their SHA-256 checksums based on the host operating system. The install method adds `rg`, the `rg.1` man page, and Bash and Zsh completions to Homebrew-managed locations. It declares a conflict with the `ripgrep` formula.
    - Tags: [homebrew, packaging, release, ruby]
- `pkg/windows/Manifest.xml` (Size : 1451 bytes): Declares compatibility with Windows 7, 8, 8.1, 10, and 11 through supported OS identifiers. Its application settings request the UTF-8 active code page and enable long-path awareness. The XML structure uses Windows application-manifest namespaces for assembly, compatibility, and Windows settings. The accompanying README explains how this manifest is used by the build.
    - Tags: [application-manifest, long-path-awareness, utf-8, windows]
- `pkg/windows/README.md` (Size : 725 bytes): Explains that the Windows manifest enables `longPathAware`, allowing paths longer than 260 characters, and documents how the manifest is linked into the final binary through linker arguments applied in `build.rs`. It states that the setting currently applies only to MSVC builds and invites patches if a straightforward GNU-build approach exists. The text links to the Windows manifest documentation and a related Rust compiler change. It provides context for the neighboring manifest file.
    - Tags: [application-manifest, documentation, windows]
- `scripts/copy-examples` (Size : 1147 bytes): Implements a Python command-line utility for extracting examples from a Rust cookbook source file. Regular expressions identify fenced or shortcode Rust blocks and marker lines that name output files; the script strips leading marker comments from the block body. `--rust-file` and `--example-dir` options select the source and output locations, with defaults of `src/cookbook.rs` and `grep/examples`. Each marked block is written as a UTF-8 example file.
    - Tags: [documentation-extraction, rust-examples, scripts, tooling]

---

# Instructions for AI Coding Agents

## When to Use This Index/DOCMAP

- Use docmaps to identify candidate files before searching or opening source.
- Read the specialized maps and relevant folder maps to narrow work to a module or feature.
- Read source files only after the index hierarchy identifies the likely implementation area.
- Do not infer file relevance from names or directory structure when docmap descriptions provide the decision source.

## How This Index Is Organized

This repository uses progressive disclosure. The root `DOCMAP.md` summarizes the project and links to cross-cutting maps and surviving folder indexes. Folder `docmap.md` files provide more detail about their own files, responsibilities, markers, and child indexes. Small-folder content is represented inline in its parent map after the separate merge pass.

## How to Use This Index/DOCMAP

1. Start with this `DOCMAP.md` for the repository overview and top-level navigation.
2. Read the specialized maps for feature, architecture, technology, testing, and change-impact context.
3. Follow the relevant folder docmap links and use their file summaries to select source and tests.
4. Read actual source files before making changes.
5. Use semantic tags and TODO/FIXME/NOTE entries to focus review and testing.
