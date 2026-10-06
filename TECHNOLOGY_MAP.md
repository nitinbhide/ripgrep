# Technology Map

This map consolidates technology facts stated in the generated root and
folder-level docmaps. It does not infer additional dependency relationships.

## Languages and Formats

- **Rust:** Primary implementation language for the executable and workspace
  libraries; the workspace uses edition 2024 and declares Rust 1.96 as its
  minimum version.
- **Python:** Used by the benchmark runner and the example-extraction script.
- **Shell:** Used for CI, release, setup, and validation utilities.
- **Ruby:** Used by the Homebrew formula.
- **XML:** Used for the Windows application manifest.
- **Markdown, CSV, and text:** Used for project and crate documentation,
  benchmark measurements, and summaries.

## Rust Workspace and Build

- Cargo workspace: root `Cargo.toml`, `Cargo.lock`, and `build.rs`.
- Formatting: `rustfmt.toml` sets a 79-character width, small-heuristics mode
  `max`, and edition 2024.
- Windows MSVC build integration embeds `pkg/windows/Manifest.xml` and enables
  linker options via `build.rs`.
- The `fuzz` folder has its own Cargo manifest and lockfile for its fuzzing
  package.

## Libraries and Frameworks Identified

- **Regex and matching:** Rust regex crates, `regex-automata`,
  `regex-syntax`, `grep-matcher`, and optional PCRE2 integration.
- **Glob and traversal:** `globset`, `ignore`, and directory-walking support.
- **Search and output:** `grep-searcher`, `grep-printer`, `grep-cli`,
  `termcolor`, JSON Lines serialization, and byte-string handling.
- **Fuzzing:** `cargo-fuzz`, libFuzzer, and the `arbitrary` feature for the
  globset fuzz target.
- **Benchmarking:** Python standard-library facilities and external
  command-line search tools.
- **Platform packaging:** Homebrew formula DSL and Windows application
  manifest settings.

## Testing and CI Tooling

- Rust unit and integration tests, including CLI tests under `tests`.
- Cargo fuzz target for glob parsing/construction.
- Shell checks for CLI/Zsh completion consistency and release checksum
  generation.
- CI scripts for package installation and build-target selection.

## Version Facts

- Root package version is recorded in `Cargo.toml`; the workspace minimum Rust
  version is 1.96.
- The generated docmaps do not provide a complete current version matrix for
  every external library or platform tool.
