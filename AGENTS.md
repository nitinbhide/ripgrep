## Source and Documentation Index

The root `DOCMAP.md` and the cross-cutting maps are the preferred entry points for repository navigation. They are authoritative for high-level understanding and for deciding where to read source code and documentation.

Use the repository navigation maps (docmaps) in this order:

1. Start at `DOCMAP.md` for the repository overview, package entry points, and top-level navigation.
2. Read the cross-cutting maps to understand capability, architecture, technology, testing, and change-impact before drilling into implementation:
   - `FEATURE_MAP.md`
   - `ARCHITECTURE_MAP.md`
   - `TECHNOLOGY_MAP.md`
   - `TESTING_MAP.md`
   - `CHANGE_IMPACT_MAP.md`
3. Then read the authoritative folder-level `docmap.md` files under the relevant package or app folder.
4. Only read source files after narrowing to the right module or feature area.

## Additional Behavioral Requirements

### Primary File Selection Must Be Docmaps-Driven

Determine candidate files exclusively from DOCMAPS during primary selection. DOCMAPS is the authoritative description of file purpose; do not infer file relevance from filenames, directory structure, or keyword similarity during that phase.

### Heuristic Scanning Is a Secondary Fallback

Heuristic scanning (grep, find, ripgrep, keyword search, symbol search, regex search, or complete directory traversal) is allowed only when DOCMAPS-based selection produces zero candidate files and the task cannot proceed without identifying relevant files. Explicitly declare fallback scanning, justify each candidate, reevaluate it against DOCMAPS where possible, and discard any candidate that contradicts DOCMAPS.

### Mandatory File-Selection Pipeline

1. Identify candidates based solely on DOCMAPS descriptions.
2. Check whether DOCMAPS produced zero candidates.
3. Only after zero results, use and declare fallback heuristic scanning if necessary.
4. Produce a `FILE SELECTION JUSTIFICATION` section. For each candidate, quote the DOCMAPS entry or explain the zero-result fallback, and explain relevance.
5. Modify only files selected and justified in that section.

If heuristic-selected files entered the primary DOCMAPS phase improperly, discard them without opening or modifying them and rerun the selection pipeline. Before final output, verify that DOCMAPS was the primary source, fallback was used only when permitted, all selected files have valid justifications, and no implicit or unjustified file access occurred.

If DOCMAPS and permitted fallback scanning produce zero candidates, do not guess; ask the user for clarification.

These rules apply to source-file selection for reading and writing. They do not prohibit narrow searches used to verify generated indexes or locate documentation entries after the primary file-selection phase.
