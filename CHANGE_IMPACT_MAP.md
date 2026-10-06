# Change Impact Map

These scenarios are navigation guidance derived from explicit file summaries
in the generated docmap hierarchy. They are not a dependency graph or an
independent impact analysis.

## CLI Option or Command Behavior

- Start with `crates/core/flags/docmap.md` for option parsing and
  `crates/core/docmap.md` for dispatch and orchestration.
- Consult `crates/core/flags/docmap.md` for flag definitions, generated help,
  man-page content, and completion summaries.
- Review relevant CLI cases in `tests/docmap.md`, especially feature and
  regression coverage.

## File Traversal, Ignore Rules, or Candidate Selection

- Read `crates/core/docmap.md` for candidate and search orchestration.
- Read `crates/ignore/docmap.md` for ignore rules, file types, and walking.
- Review relevant behavior tests in `tests/docmap.md`, including the
  regression and feature suites.

## Regex, PCRE2, or Glob Matching

- Read the matcher interface, PCRE2, and glob summaries in `crates/docmap.md`,
  and the Rust regex engine index in `crates/regex/docmap.md`.
- Review matcher tests in the `crates/matcher` section of `crates/docmap.md`
  and CLI regex, glob, and regression coverage in `tests/docmap.md`.
- For PCRE2 CLI option integration, consult the core flags map.

## Search Buffering, Multiline, Encoding, or Binary Behavior

- Read `crates/searcher/src/docmap.md` for searcher behavior and
  `crates/core/docmap.md` for its use by the executable.
- Read `crates/cli/docmap.md` for decompression utilities.
- Review `tests/multiline.rs`, `tests/binary.rs`, feature/regression suites,
  and the merged fixture section of `tests/docmap.md` as relevant.

## Output Format or Printer Behavior

- Read `crates/printer/src/docmap.md` for standard, summary, path, and JSON
  output.
- Read `crates/core/docmap.md` for output coordination.
- Review `tests/json.rs` and the output-related cases listed in
  `tests/docmap.md`.

## Indexed Search

- Read the index crate summary in `crates/docmap.md` and feature-gated
  integration summary in `crates/core/docmap.md`.
- Review the merged index-test section of `tests/docmap.md`.
- The root manifest describes `unstable-index` as active development and
  potentially having serious bugs.

## Packaging or Release Workflow

- Read the CI summary and packaging entries in the root `DOCMAP.md`, plus
  `benchsuite/runs/docmap.md` and `RELEASE-CHECKLIST.md` as applicable.
- For Windows manifest integration, also consult the root `build.rs`,
  `pkg/windows/README.md`, and `pkg/windows/Manifest.xml` entries in
  `DOCMAP.md`.
- For Homebrew packaging, consult the `pkg/brew/ripgrep-bin.rb` entry in
  `DOCMAP.md`.

## Test Harness or Test Data

- Read `tests/docmap.md` for the test modules and shared helpers.
- Read the merged fixture section of `tests/docmap.md`.
- Read the `fuzz` and fuzz-target summaries in `DOCMAP.md` for fuzz package
  configuration and target navigation.

## Not Available in the Generated Docmaps

- The maps do not provide a complete generated dependency graph or
  machine-verified file-impact graph.
