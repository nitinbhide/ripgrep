# Testing Map

This map is based on test and CI information explicitly present in the
generated docmaps.

## Test Strategy

The repository uses Rust unit tests and integration tests. CLI integration
tests construct temporary inputs and assert on output, errors, and exit
behavior. The fuzz package exercises glob parsing and string round-tripping
with arbitrary input. A CI shell script compares `rg --help` options with the
Zsh completion definitions.

## Test Suites and Coverage Areas

| Suite or area | Coverage described in docmaps | Navigation |
| --- | --- | --- |
| CLI integration entry point | Modules for binary, feature, index, JSON, miscellaneous, multiline, and regression tests; index tests are feature-gated | `tests/docmap.md` |
| Feature tests | Encodings, pattern sources, output, globs/ignore, limits, sorting, statistics, multiline behavior, replacements, and exit status | `tests/feature.rs` entry in `tests/docmap.md` |
| Regression tests | Issue-referenced search, traversal, ignore/glob, output, regex, and exit-status cases | `tests/regression.rs` entry in `tests/docmap.md` |
| Binary handling | NUL-containing input, explicit versus recursive search, binary/text options, counts, and memory mapping | `tests/binary.rs` entry in `tests/docmap.md` |
| JSON output | JSON Lines message variants, replacements, statistics, invalid UTF-8 representation, and CRLF | `tests/json.rs` entry in `tests/docmap.md` |
| Multiline search | Overlapping matches, newline and dot-all behavior, output modes, stdin, and context | `tests/multiline.rs` entry in `tests/docmap.md` |
| Index feature | Index-mode interactions and options disallowed in index mode, summarized in its merged section | `tests/docmap.md` |
| Matcher contract | Matcher operations and default behavior using regex-backed implementations, summarized in the crate section | `crates/docmap.md` |
| Ignore rules | Gitignore ancestor matching and BOM handling | `crates/ignore/docmap.md` |
| Glob fuzzing | Glob construction path equivalence and string preservation for accepted arbitrary inputs | `DOCMAP.md` |
| Completion consistency | CLI help options compared with Zsh completion definitions, summarized inline | `DOCMAP.md` |

## Fixtures and Shared Test Support

- Shared command execution, temporary directories, assertions, and fixtures
  are described in `tests/docmap.md`.
- Compressed and NUL-containing input fixtures are summarized in the merged
  `tests/data` section of `tests/docmap.md`.
- Test suites use Rust modules and shared macros as detailed by the tests
  folder map.

## Test Plans and Coverage Gaps

- The generated docmaps do not identify a standalone test plan or quantified
  coverage report.
- A complete feature-to-test traceability matrix is not available in the
  generated docmaps.
