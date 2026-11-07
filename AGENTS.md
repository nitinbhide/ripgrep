## Source and Documentation Index

The root `DOCMAP.md` and the cross-cutting maps are the preferred entry points for repository navigation. They are authoritative for high-level understanding and for deciding where to read source code and documentation.

### Project Root Docmap

- `DOCMAP.md` — repository-wide overview, package navigation, capabilities, and change-impact guidance. The repository root is also the sole Designated Root Folder, so this index serves both roles.

Use the repository navigation maps (docmaps) in this order:

1. Start at `DOCMAP.md` for the repository overview, package entry points, and top-level navigation.
2. Read the cross-cutting maps to understand capability, architecture, technology, testing, schema, and change-impact before drilling into implementation:
   - `FEATURE_MAP.md`
   - `ARCHITECTURE_MAP.md`
   - `TECHNOLOGY_MAP.md`
   - `TESTING_MAP.md`
   - `CHANGE_IMPACT_MAP.md`
   - `SCHEMA_MAP.md`
3. Then read the authoritative folder-level `docmap.md` files under the relevant package or app folder.
4. Only read source files after narrowing to the right module or feature area.

## Additional Behavioral Requirements

### Primary File Selection Must Be Docmaps-Driven

Determine candidate files exclusively from DOCMAPS during the primary selection phase.

- DOCMAPS are the authoritative descriptions of file purpose.
- File selection must be based on DOCMAP entries.
- Do not infer file relevance from filenames, directory structure, or keyword similarity during primary selection.

### Heuristic Scanning Is a Secondary Fallback

Heuristic scanning (grep, find, ripgrep, keyword search, symbol search, regex search, or complete directory traversal) is prohibited during primary file selection.

Heuristic scanning is allowed only if DOCMAP-based selection produces zero candidate files and the task cannot proceed without identifying relevant files. When used, explicitly declare it as fallback, justify every candidate, reevaluate candidates against DOCMAPS where possible, and discard any candidate that contradicts them.

### Mandatory File-Selection Pipeline

1. Identify candidate files based solely on DOCMAP descriptions.
2. Check whether DOCMAP-based selection produced zero candidates.
3. Only then use and declare fallback heuristic scanning, if necessary.
4. Produce a `FILE SELECTION JUSTIFICATION` section. For each candidate, quote the DOCMAP entry or explain the zero-result fallback and its relevance.
5. Modify only files selected and justified in that section.

If heuristic-selected files entered the primary DOCMAP phase improperly, discard them without opening or modifying them and rerun the selection pipeline.

Before producing a final response, verify that DOCMAPS were the primary source, fallback scanning was used only when permitted, every selected file has a valid justification, and no implicit or unjustified file access occurred.

### Failure Mode Handling

If DOCMAPS produce zero results and permitted fallback scanning also produces zero results, do not guess; request clarification.

### Absolute Rules for File Selection

- DOCMAPS are the primary authority.
- Heuristic scanning is allowed only when DOCMAP-based selection yields zero files.
- Only justified files may be modified.
- No implicit or unjustified file access is allowed.
- Self-verification is mandatory.
