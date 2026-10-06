# Feature Map

This map is derived from the repository `DOCMAP.md` and surviving folder
`docmap.md` files. It records only capabilities and relationships described
there.

## Recursive Search and File Selection

- **Requirement/documentation:** Recursively search files while respecting
  ignore rules and filtering hidden or binary files by default; options and
  examples are documented in `README.md`, `GUIDE.md`, and `FAQ.md`.
- **Design/source:** The executable coordinates CLI dispatch and search in
  `crates/core/main.rs` and `crates/core/search.rs`. Candidate handling is in
  `crates/core/haystack.rs`; ignore-aware walking and file filtering are
  described in `crates/ignore`.
- **Tests:** `tests/feature.rs`, `tests/misc.rs`, and `tests/regression.rs`
  entries in `tests/docmap.md` describe feature, general behavior, and
  issue-referenced regression cases.
- **Documented markers:** See the TODO/FIXME/NOTE entries for those files in
  `tests/docmap.md` and the root `DOCMAP.md`.

## Pattern Matching

- **Requirement/documentation:** Search patterns use the default Rust regex
  engine; glob and file-type filtering are documented in `GUIDE.md`.
  Optional PCRE2 supports additional regex syntax as described in `README.md`.
- **Design/source:** The matcher contract, PCRE2 integration, and glob
  matching are summarized in `crates/docmap.md`; the Rust regex backend is
  indexed in `crates/regex/docmap.md`. Core flag parsing and search dispatch
  are described in `crates/core/docmap.md`.
- **Tests:** The feature, regression, and multiline entries in
  `tests/docmap.md` cover CLI behavior. Matcher tests are summarized in
  `crates/docmap.md`.
- **Documented markers:** The crate summary and regex map record their
  respective API or implementation notes and TODO markers.

## Search Output

- **Requirement/documentation:** User-facing output and JSON Lines behavior
  are described in `GUIDE.md`, `FAQ.md`, and `README.md`.
- **Design/source:** Human-readable and JSON printers are documented in
  `crates/printer/src/docmap.md`; core connects search results and output in
  `crates/core/search.rs`.
- **Tests:** `tests/json.rs`, `tests/misc.rs`, and `tests/feature.rs` exercise
  JSON and other CLI output cases.
- **Documented markers:** Consult the linked file entries for marker details.

## Multiline, Binary, Encoding, and Compressed Input

- **Requirement/documentation:** The README, guide, and FAQ describe multiline
  searching, binary handling, non-UTF-8 encodings, compressed input, and
  preprocessing.
- **Design/source:** Search execution and preprocessing are described in
  `crates/core/search.rs`; line buffering, binary handling, and encoding are
  indexed under `crates/searcher/src/docmap.md`; decompression utilities are
  summarized in `crates/cli/docmap.md`.
- **Tests:** The multiline, binary, feature, and regression entries in
  `tests/docmap.md` cover corresponding CLI behavior. Compressed corpus
  fixtures are summarized in the merged `tests/data` section of that map.
- **Documented markers:** See the source and test map entries for explicit
  notes and TODOs.

## Optional Indexed Search

- **Requirement/documentation:** `Cargo.toml` declares the `unstable-index`
  feature and documents it as active development that may have serious bugs.
- **Design/source:** Index APIs and literal-to-ngram query construction are
  summarized in `crates/docmap.md`; feature-gated CLI integration is
  described in `crates/core/docmap.md`.
- **Tests:** The merged index-test section of `tests/docmap.md` identifies
  integration tests for index-mode behavior and disallowed options.
- **Documented markers:** The `unstable-index` limitation is explicit in the
  root manifest description; see the index and test maps for any file markers.

## Release, Packaging, and Performance Support

- **Requirement/documentation:** `RELEASE-CHECKLIST.md` documents release
  steps; packaging guidance and historical benchmark purposes are indexed in
  `pkg` and `benchsuite`.
- **Design/source:** CI scripts and the benchmark runner are summarized
  inline in the root map; archived run records are indexed in
  `benchsuite/runs/docmap.md`. Packaging files are also summarized inline in
  the root map.
- **Tests:** The root map describes a CI check that compares CLI help options
  with Zsh completion definitions. Benchmark records are archived under
  `benchsuite/runs/docmap.md`.
- **Documented markers:** Consult the corresponding docmap file summaries.

## Areas Not Available in the Generated Docmaps

- A formal requirements specification linking every feature to acceptance
  criteria is not available in the generated docmaps.
- No standalone feature-to-test traceability document is identified.
