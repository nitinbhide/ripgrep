---
folder: "benchsuite/runs"
generated_on: "2026-10-06"
num_files: 29
semantic_tags: [benchmark-archive, benchmark-context, benchmark-data, benchmark-results, benchmark-setup, build-configuration, csv, glibc, jemalloc, linux, musl, performance-measurements, performance-results, performance-summary, search-tools, setup-documentation, tool-versions]
todos_present: false
dependencies: []
---

# Folder Overview

## Purpose
This folder groups 12 documented benchmark runs dated from 2016-09-17 through 2022-12-16. Each run docmap describes a raw CSV of per-command measurements and a text summary of aggregate timings for search cases on Linux corpora. Two 2016 runs document Ubuntu 16.04 EC2 setup, while later run notes identify Arch Linux hosts; the 2016-12-24 snapshots additionally distinguish glibc or musl and jemalloc or system-allocator labels. README or setup notes in several runs record invocations, tool versions, build details, or host information. The child indexes are the navigation point for each run’s specific evidence.
This index also incorporates small child folders inline; their original summaries and file entries are retained below.
## Major Responsibilities

This folder provides navigation among the independent run snapshots and distinguishes them by date, host, and documented configuration. It has no direct files in the retained inventory; its contents at this level are the child run folders, each with a standalone docmap.

## Technology Notes

Child runs record Linux search-tool measurements in CSV and text formats. The run documentation identifies variations in dates, host names, libc, and allocator labels.

# Folder Navigation

## Merged Child Folders
- `2016-09-17-ubuntu1604-ec2/` —
  This folder preserves a benchmark run dated 2016-09-17 on an Ubuntu 16.04 EC2 host, as identified by its directory name and setup notes. It contains the raw measurements and a human-readable comparison report produced by the benchsuite runner. The setup notes document the machine, search-tool installation steps, corpus preparation, and invocation used for the run. Together, these files support inspection and reproduction of this historical performance snapshot.
- `2016-09-20-ubuntu1604-ec2/` —
  This folder preserves a benchmark run dated 2016-09-20 on an Ubuntu 16.04 EC2 host, as identified by its directory name and setup notes. It contains the raw measurements and a human-readable comparison report produced by the benchsuite runner. The setup notes document the machine, search-tool installation steps, corpus preparation, and invocation used for the run. Together, these files support inspection and reproduction of this historical performance snapshot.
- `2016-09-22-archlinux-cheetah/` —
  This folder preserves benchmark results dated 2016-09-22 for the Arch Linux host identified as `cheetah` in its directory name. The raw table records command-level measurements, and the summary presents aggregate comparisons across search cases. The visible summary covers Linux corpus searches including alternate patterns, case-insensitive matching, literals, regexes, and Unicode. These files provide a dated performance snapshot without a separate setup note in this folder.
- `2016-12-24-archlinux-cheetah/` —
  This folder preserves benchmark results dated 2016-12-24 for the Arch Linux host identified as `cheetah`. The raw table records individual command timings, while the summary formats results by benchmark and pattern. The summary includes Linux search cases such as literals, alternations, word matching, and Unicode matching. The directory name and result content identify this as one of a set of runs from the same date with different runtime configurations.
- `2016-12-24-archlinux-cheetah-glibc-jemalloc/` —
  This folder preserves benchmark results dated 2016-12-24 for the Arch Linux `cheetah` run labeled `glibc-jemalloc`. The raw table records individual command timings, while the summary formats results by benchmark and pattern. The results cover Linux search cases such as literal, alternation, word, and Unicode matching. The folder label distinguishes this recorded run from other same-date allocator and libc variants.
- `2016-12-24-archlinux-cheetah-glibc-system/` —
  This folder preserves benchmark results dated 2016-12-24 for the Arch Linux `cheetah` run labeled `glibc-system`. The raw table records individual command timings, while the summary formats results by benchmark and pattern. The results cover Linux search cases such as literal, alternation, word, and Unicode matching. The folder label distinguishes this recorded run from other same-date allocator and libc variants.
- `2016-12-24-archlinux-cheetah-musl-jemalloc/` —
  This folder preserves benchmark results dated 2016-12-24 for the Arch Linux `cheetah` run labeled `musl-jemalloc`. The raw table records individual command timings, while the summary formats results by benchmark and pattern. The results cover Linux search cases such as literal, alternation, word, and Unicode matching. The folder label distinguishes this recorded run from other same-date allocator and libc variants.
- `2016-12-24-archlinux-cheetah-musl-system/` —
  This folder preserves benchmark results dated 2016-12-24 for the Arch Linux `cheetah` run labeled `musl-system`. The raw table records individual command timings, while the summary formats results by benchmark and pattern. The results cover Linux search cases such as literal, alternation, word, and Unicode matching. The folder label distinguishes this recorded run from other same-date allocator and libc variants.
- `2016-12-30-archlinux-cheetah/` —
  This folder preserves benchmark results dated 2016-12-30 for the Arch Linux host identified as `cheetah`. The raw table records command-level measurements, and the summary presents aggregate comparisons by benchmark and pattern. The visible output covers Linux corpus searches such as alternations and literals. These files form a separate dated snapshot from the 2016-12-24 results.
- `2018-01-08-archlinux-cheetah/` —
  This folder preserves benchmark results dated 2018-01-08 for the Arch Linux host identified as `cheetah`. Its README records the benchmark invocation, compared tool versions, and ripgrep build details, while the CSV and summary contain raw and aggregated results. The README says these results are most directly comparable to the 2016-09-22 Arch Linux run. Together, the files provide a dated snapshot with enough environment details to interpret the comparisons.
- `2020-10-14-archlinux-frink/` —
  This folder preserves benchmark results dated 2020-10-14 for the Arch Linux host identified as `frink`. Its README gives the benchsuite command, measured tool versions, ripgrep source revision, and host description. The raw CSV stores per-command observations, and the summary formats them into benchmark-by-benchmark comparisons. These records support analysis of the search-tool results in the context of the run’s stated environment.
- `2022-12-16-archlinux-duff/` —
  This folder preserves benchmark results dated 2022-12-16 for the Arch Linux host identified as `duff`. Its README records the benchsuite invocation, measured search-tool versions, ripgrep source revision, and machine hardware. The raw CSV stores per-command observations, and the summary formats them into benchmark-by-benchmark comparisons. Together, these files capture a later performance snapshot with its stated build and system context.
## Files
- `2016-09-17-ubuntu1604-ec2/README.SETUP` (Size : 2257 bytes): Documents the Ubuntu 16.04 EC2 machine profile, system package setup, corpus download procedure, and installation steps for the search tools used in the benchmark. It records the benchmark command and says the run took about 30 minutes. The instructions include specific tool builds and versions available on the machine. This is the environment and reproduction guide for the adjacent result files.
    - Tags: [benchmark-setup, linux, search-tools, setup-documentation]
- `2016-09-17-ubuntu1604-ec2/raw.csv` (Size : 64975 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-09-17-ubuntu1604-ec2/summary` (Size : 10737 bytes): Reports aggregate timings for the search cases in this benchmark run. It groups results by benchmark and pattern, then lists search-tool timings, variation, and matched-line counts. The visible cases include Linux alternation and literal searches, with ripgrep and other available tools compared. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2016-09-20-ubuntu1604-ec2/README.SETUP` (Size : 2265 bytes): Documents the Ubuntu 16.04 EC2 machine profile, system package setup, corpus download procedure, and installation steps for the search tools used in the benchmark. It records the benchmark command with three warm-up iterations and ten measured iterations, and says the run took about 120 minutes. The instructions include specific tool builds and versions available on the machine. This is the environment and reproduction guide for the adjacent result files.
    - Tags: [benchmark-setup, linux, search-tools, setup-documentation]
- `2016-09-20-ubuntu1604-ec2/raw.csv` (Size : 226710 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-09-20-ubuntu1604-ec2/summary` (Size : 11172 bytes): Reports aggregate timings for the search cases in this benchmark run. It groups results by benchmark and pattern, then lists search-tool timings, variation, and matched-line counts. The visible cases include Linux alternation and literal searches, with ripgrep and other available tools compared. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2016-09-22-archlinux-cheetah/raw.csv` (Size : 69211 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-09-22-archlinux-cheetah/summary` (Size : 11161 bytes): Reports aggregate timings for the search cases in the 2016-09-22 run. It groups results by benchmark and pattern, then lists search-tool timings, variation, and matched-line counts. The visible cases include Linux alternation and literal searches, with ripgrep and other available tools compared. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2016-12-24-archlinux-cheetah/raw.csv` (Size : 21026 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-12-24-archlinux-cheetah/summary` (Size : 5991 bytes): Reports aggregate timings for the 2016-12-24 Arch Linux `cheetah` run. It groups results by benchmark and pattern, listing tool timings, variation, and matched-line counts. The visible output includes Linux alternation and case-insensitive alternation measurements. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2016-12-24-archlinux-cheetah-glibc-jemalloc/raw.csv` (Size : 21047 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-12-24-archlinux-cheetah-glibc-jemalloc/summary` (Size : 5991 bytes): Reports aggregate timings for the 2016-12-24 Arch Linux `cheetah` run labeled `glibc-jemalloc`. It groups results by benchmark and pattern, listing tool timings, variation, and matched-line counts. The visible output includes Linux alternation and case-insensitive alternation measurements. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2016-12-24-archlinux-cheetah-glibc-system/raw.csv` (Size : 21028 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-12-24-archlinux-cheetah-glibc-system/summary` (Size : 5991 bytes): Reports aggregate timings for the 2016-12-24 Arch Linux `cheetah` run labeled `glibc-system`. It groups results by benchmark and pattern, listing tool timings, variation, and matched-line counts. The visible output includes Linux alternation and case-insensitive alternation measurements. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2016-12-24-archlinux-cheetah-musl-jemalloc/raw.csv` (Size : 21044 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-12-24-archlinux-cheetah-musl-jemalloc/summary` (Size : 5991 bytes): Reports aggregate timings for the 2016-12-24 Arch Linux `cheetah` run labeled `musl-jemalloc`. It groups results by benchmark and pattern, listing tool timings, variation, and matched-line counts. The visible output includes Linux alternation and case-insensitive alternation measurements. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2016-12-24-archlinux-cheetah-musl-system/raw.csv` (Size : 21044 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-12-24-archlinux-cheetah-musl-system/summary` (Size : 5991 bytes): Reports aggregate timings for the 2016-12-24 Arch Linux `cheetah` run labeled `musl-system`. It groups results by benchmark and pattern, listing tool timings, variation, and matched-line counts. The visible output includes Linux alternation and case-insensitive alternation measurements. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2016-12-30-archlinux-cheetah/raw.csv` (Size : 21038 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2016-12-30-archlinux-cheetah/summary` (Size : 5991 bytes): Reports aggregate timings for the 2016-12-30 Arch Linux `cheetah` run. It groups results by benchmark and pattern, listing tool timings, variation, and matched-line counts. The visible output includes Linux alternation and case-insensitive alternation measurements. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2018-01-08-archlinux-cheetah/README` (Size : 1559 bytes): Documents that the results were captured using the repository’s benchsuite runner and gives the command, warm-up and benchmark iteration counts, and tool versions. It identifies the run as most comparable to the 2016-09-22 Arch Linux results. It also describes how ripgrep was built from a source commit with SIMD and AVX features enabled. This file supplies the environment context for the adjacent raw and summarized results.
    - Tags: [benchmark-context, build-configuration, linux, tool-versions]
- `2018-01-08-archlinux-cheetah/raw.csv` (Size : 114939 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover Linux alternation searches and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2018-01-08-archlinux-cheetah/summary` (Size : 11162 bytes): Reports aggregate timings for the 2018-01-08 Arch Linux `cheetah` run. It groups results by benchmark and pattern, listing search-tool timings, variation, and matched-line counts. The visible output includes Linux alternation and case-insensitive alternation measurements with several tools compared. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2020-10-14-archlinux-frink/README.md` (Size : 1080 bytes): Documents the benchmark runner command, iteration settings, search-tool versions, the ripgrep source revision and build feature, and the host hardware. It identifies the captured run as dated 2020-10-14. This file gives the environment context required to interpret the neighboring measurements. It does not itself contain the result tables.
    - Tags: [benchmark-context, build-configuration, linux, tool-versions]
- `2020-10-14-archlinux-frink/raw.csv` (Size : 91922 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover the Linux literal-default search and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2020-10-14-archlinux-frink/summary` (Size : 9567 bytes): Reports aggregate timings for the 2020-10-14 Arch Linux `frink` run. It groups results by benchmark and pattern, listing tool timings, variation, and matched-line counts. The visible output begins with default and ordinary literal searches for `PM_RESUME` across ripgrep and other tools. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]
- `2022-12-16-archlinux-duff/README.md` (Size : 1162 bytes): Documents the benchmark runner command, iteration settings, search-tool versions, ripgrep source revision and build feature, and host hardware. It identifies the captured run as dated 2022-12-16. This file gives the environment context required to interpret the neighboring measurements. It does not itself contain the result tables.
    - Tags: [benchmark-context, build-configuration, linux, tool-versions]
- `2022-12-16-archlinux-duff/raw.csv` (Size : 55797 bytes): Stores individual command-run measurements emitted by the benchmark suite. Its header identifies benchmark, warm-up and measured iteration settings, tool name, command, duration, matched-line count, and environment. The initial records cover the Linux literal-default search and include repeated timing samples. Use this table to inspect the raw observations underlying this run’s summary.
    - Tags: [benchmark-data, csv, performance-measurements, search-tools]
- `2022-12-16-archlinux-duff/summary` (Size : 9564 bytes): Reports aggregate timings for the 2022-12-16 Arch Linux `duff` run. It groups results by benchmark and pattern, listing tool timings, variation, and matched-line counts. The visible output begins with default and ordinary literal searches for `PM_RESUME` across ripgrep and other tools. Asterisks are retained as report annotations on selected results.
    - Tags: [benchmark-results, performance-summary, search-tools]

---

## Links Child Folder docmaps
None.
# Related Features

Archive of historical command-line search-tool benchmark runs.

# Agent Guidance

## Read When

Read this index to locate a particular dated benchmark or host configuration, then follow that run’s standalone docmap.

## Modify When

Modify this index when adding or removing a run folder or updating the organization of the benchmark archive.

## Avoid Modifying When

Avoid changing individual run results here; update the files in the corresponding run folder instead.
