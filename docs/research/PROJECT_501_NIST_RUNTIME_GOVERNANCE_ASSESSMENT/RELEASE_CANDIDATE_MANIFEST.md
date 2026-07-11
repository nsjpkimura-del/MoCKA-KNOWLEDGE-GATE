# Release Candidate Manifest — PROJECT_501 / MRS-001 v1.0-rc1

**Sealed:** 2026-07-11
**Sealed by:** Claude (Sonnet 5), at the project owner's direction, following R01's four review phases (Phase 1 Repository Inventory → Independent Audit → Corrective Action → Ledger Full Recount) and final verdict **Approved with Notes** (`appendix/FINAL_VERIFICATION_REPORT.md`).
**Purpose:** fix the exact byte-for-byte content of every file in this deliverable as of the seal date, so this version can be cited, referenced, or compared against without ambiguity about what "v1.0" actually contained. Per explicit instruction, this is a **freeze**, not an edit — no file content was changed as part of producing this manifest (two trivial reference-precision fixes, listed below, were made immediately before the freeze, as part of the pre-seal reference-consistency check, not after it).

---

## Pre-seal reference-consistency check (performed before sealing, per instruction)

- **Markdown hyperlinks** (`[text](path)` syntax): 19 relative-link targets found across all 22 files, checked by resolving each against its source file's directory. **0 broken.**
- **Backtick file-name citations** (the dominant citation style in this project, e.g. `` `07_GAP_ANALYSIS.md` §9 ``): 424 citations found, 55 distinct filenames. The large majority resolve to files in the external MoCKA repositories this project surveys (e.g. `CONSTITUTION.md`, `VERIFICATION_ARENA.md`, `logs/bus/events.csv`'s sibling files) and are correctly *not* present in this local deliverable tree — they are evidence citations, not internal cross-references. Of the citations referring to this project's own 22 files, 2 used a bare filename (`REPOSITORY_SURVEY_ADDENDUM_m-sirius-k.md`) where the real file lives in a subdirectory (`appendix/evidence/`) — corrected to the full relative path in `appendix/FINAL_VERIFICATION_REPORT.md` (2 occurrences) immediately before sealing. No other internal ambiguity or breakage found (verified by basename-collision check: only `README.md` exists in two places — the project root and `appendix/diagrams/` — and every citation of `README.md` found in context refers to an external repository's own README, not this project's; no cross-reference conflates the two).
- **Method used, for reproducibility:** a Python script walking the file tree, extracting both link syntaxes via regex, and resolving each target against the filesystem. Not committed to the repository (this project's scope is documentation, not tooling), but the exact commands are reproducible from the description above by any reviewer with access to this file tree.

---

## SHA-256 File Manifest

All hashes computed via `sha256sum` over the exact file bytes, 2026-07-11. Paths are relative to `docs/research/PROJECT_501_NIST_RUNTIME_GOVERNANCE_ASSESSMENT/`.

```
ac6027b4c35359bdd5b6fcf1b4f1959308d797c0ecd6ff1968befe12cb568b9d  00_PROJECT_CHARTER.md
060c5db02357e4e4964e47750fdd664566b6721655fc0c93e8061ec4aa7bf2c4  01_EXECUTIVE_SUMMARY.md
09efa317b8e404e4517f87c53796e6fa5c169d35e571ce6b0a043a99ac49a4b1  02_NIST_REQUIREMENT_ANALYSIS.md
649b875c80a1fce2523d91ba59b13e49873290252d417ad4ff49b43249e29b09  03_RUNTIME_GOVERNANCE_SPECIFICATION.md
f25783ba9380c57ee30c66799ad5851981dd0849462beec5a5624e2be516b8e8  04_REQUIREMENT_MAPPING.md
ea760b0eaaa2bed696191d2cdc5ba490710fbe789a26a6cd5f029a77ce475565  05_COMPARATIVE_ANALYSIS.md
4f699a594c3db83cf8e58218470978d38ba5f446f24b15d55169391261f2f806  06_EVIDENCE_TREE.md
e5b9c8eb61d80f8090435ef76470330a575717f6b1cb163e6a74f7865efdc900  07_GAP_ANALYSIS.md
015983547fc1d1322ef56cc4a916ac4ba7300b078291b3c99a7c18507ab837ef  08_STRATEGIC_ASSESSMENT.md
f1c292135f7c54de0323289a3a0c6f8b2242e08c3194bc1a05fa685aa415bbe0  09_ROADMAP.md
b41b4a7a9b23e8fb7aee9b93198387dbfa0bd8a810115d455ef868d941ac5f1c  10_REFERENCES.md
d323cb9cc67b3f2f94597a15c79aa554c873e90f192c3c4f84de9ad87b553500  README.md
e215c3ac97add0a1687b055ef1b28980922f2f079e0b381da275220a9d414855  appendix/CORRECTIVE_ACTION_REPORT.md
ccce4aceb30f47c2d72c57330c097bb4cb5ed5568f4f1f142c0a767719b84e55  appendix/FINAL_VERIFICATION_REPORT.md
7744d7cdce5dee7bdef59e9f878b2b113ee66f27a0be29fa37368129e828f712  appendix/INDEPENDENT_AUDIT_REPORT.md
1b8a65fb8fa1448682ee640a8d627a13911b3f070afb2fbf37db190f7e0bff08  appendix/LEDGER_FULL_RECOUNT_REPORT.md
d11a7285fa3fa1228fba884eebfb8717bff7362c121a895489e10588d4b9a3cb  appendix/REVIEW_LOG.md
ff680e044c418e0943c3b27302123e64f7a90047b4014a64d60a156f31ffa295  appendix/diagrams/README.md
6c8b87beaccde96cde15929906800b9a534c5cdae9caca3202346615fbc81647  appendix/evidence/REPOSITORY_SURVEY_ADDENDUM_m-sirius-k.md
71e35495856436f9c6c09fbad224f491c3c3ba0cc385e2902c32e84993e8f70d  appendix/evidence/full_repository_survey.md
a6b48e944a7ffdceb9a167fd179c889515dad7ce99ef94577852efdfa435db2d  appendix/evidence/repository_evidence_register.md
31b976f926201411969e13c53b675843c313487ce9842c307513fd7ad5c46c18  appendix/tables/abbreviated_evidence_trees.md
```

**22 files sealed.** Each hash independently verifiable by any reviewer with this file tree via `sha256sum <path>`.

## Manifest Meta-Hash

A SHA-256 computed over the 22-line manifest above itself (path + hash pairs, one per line, sorted by path, LF-joined), as a single value that changes if *any* file's hash or the file list itself changes — the "hash of the hash list":

```
4c508efd709cdf75b89a3797c6c7c43fc1f6a3006be3177bcaaf6666c1c40277
```

Reproduction command (run from the project root, `docs/research/PROJECT_501_NIST_RUNTIME_GOVERNANCE_ASSESSMENT/`):
```
find . -type f ! -name RELEASE_CANDIDATE_MANIFEST.md | sort | sed 's|^\./||' | while read -r f; do sha256sum "$f" | awk -v f="$f" '{print $1"  "f}'; done | sha256sum
```

**Self-correction note:** this manifest's `README.md` and `appendix/REVIEW_LOG.md` hashes were initially computed *before* those two files' freeze-declaration edits (updating `README.md`'s version header/status and appending `REVIEW_LOG.md`'s final entry) were made — an unavoidable sequencing issue, since recording the seal necessarily touches the files that describe it. This was caught by re-hashing all files immediately before finalizing this manifest and diffing against what had been written; exactly those 2 hashes (and no others) had changed, confirming no other file was altered in the interim. Both hashes above, and the meta-hash, reflect the true final state of all 22 sealed files as they exist at the moment this manifest was completed.

---

## Version Freeze Declaration

- **Version identifier:** PROJECT_501 / MRS-001, **v1.0-rc1 (Release Candidate)**
- **Status:** SEALED as of 2026-07-11. This is the baseline version.
- **Scope of the seal:** all 22 files listed above, exactly as hashed. This manifest file itself is not included in its own hash list (a manifest cannot seal itself); its own integrity is anchored by being sealed alongside the package in this same commit-free, local working-tree state.
- **Change policy going forward:** no further edits shall be made to any of the 22 sealed files under this v1.0-rc1 identifier. Any future correction, addition, or revision — including resolution of the three Notes carried forward in `appendix/FINAL_VERIFICATION_REPORT.md` Part 3 — shall be made under a new version identifier (**v1.1**, **v1.2**, **v2.0**, etc.), per `00_PROJECT_CHARTER.md`'s statement that the MRS-001 series identifier remains stable across such revisions while the version number advances. A v1.1 (or later) revision should itself restate which of this v1.0-rc1 manifest's hashes it changes, so the diff between versions remains as auditable as this seal.
- **What "Release Candidate" means here:** this manifest fixes content for citation and comparison purposes. It does **not** constitute publication, and it does not authorize `git commit`, `git push`, tagging, or any GitHub Release. Per R01's standing instruction across all four prior review phases, those actions remain separate decisions for the project owner, to be taken (if ever) outside this documentation-freeze step.

---

*This manifest is itself part of the sealed local working tree — see the parent `README.md` for the project's institutional registration and full document index.*
