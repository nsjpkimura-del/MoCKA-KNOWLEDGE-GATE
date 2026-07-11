# Independent Audit Report — PROJECT_501 / MRS-001

**Auditor:** Independent audit agent, no prior involvement in producing this project.
**Date:** 2026-07-11
**Audit type:** Phase 4 Independent Audit (per `README.md` R01 Review Status table).
**Scope of authority:** Read/write confined to `docs/research/PROJECT_501_NIST_RUNTIME_GOVERNANCE_ASSESSMENT/`. No `git commit`/`git push`/write operations performed against any of the 8 (or 9 — see Finding 2) MoCKA repositories.

---

## 1. Methodology and Scope

This audit treated PROJECT_501 as an unverified third-party submission. No claim, citation, self-reported correction, or narrative about the project's own rigor (including the `appendix/REVIEW_LOG.md` Phase 1 corrections) was accepted at face value; every factual/evidentiary claim checked below was re-verified directly against a primary source by this auditor.

**What was checked:**

- **Repository coverage:** ran `gh repo list m-sirius-k --limit 30 --json name,visibility,description` independently to get the current authoritative repo list, rather than trusting the project's stated list of 8 repositories.
- **Git/commit-hash verification:** for all 8 locally-cloned repositories (`C:/Users/sirok/{MoCKA,mocka-runtime,mocka-outfield,mocka-public,mocka-civilization,mocka-external-brain,mocka-transparency,mocka-knowledge-gate}`), ran `git status`, `git rev-list --left-right --count HEAD...origin/main`, and `git rev-parse HEAD` / `git rev-parse origin/main`, and cross-checked against the commit hashes cited in `10_REFERENCES.md`.
- **File-existence/content verification:** used `git ls-tree -r origin/main`, `git show origin/main:<path>`, and `git cat-file -s` — never the local working tree — to check specific claims: `verify_chain.py`/`verify_all.py` absence in `mocka-public`/`mocka-transparency`; `logs/bus/events.csv` and `events\outfield_log.csv` existence claims; `data/MOCKA_OVERVIEW.json`'s `classification` field and commit hash; `governance/human_gate_cli.py`'s absence from `origin/main` and presence as an untracked local file; `mocka_events.db` size; TODO-register file commit hash; Event Ledger sample file counts under `data/storage/infield/` and `data/storage/outbox/PILS_DONE/`; Orchestra file listing; CI workflow file listing; role-policy files; `CONSTITUTION.md` content; file/line counts for `mocka-runtime`, `mocka-civilization`, `mocka-knowledge-gate` CI-disabled directory.
- **NIST source verification:** fetched the Concept Note PDF directly from its canonical NIST URL and read the extracted text of both pages in full, then compared every quoted phrase in `02_NIST_REQUIREMENT_ANALYSIS.md` §2 word-for-word against the source.
- **Internal ledger spot-checks:** used the MCP-exposed `mocka_integrity_get`, `mocka_decision_get`, `mocka_search`, and `mocka_get_todo` tools to directly retrieve and read 9 individually cited internal records in full (`IC_20260708_004`, `DC_20260708_001`, `DC_20260706_004`, `IC_20260705_020`, `IC_20260707_005`, `DC_20260707_011`, `TODO_412`, `TODO_430`, `TODO_444`) and confirmed the existence (via `mocka_get_todo` + grep) of `TODO_398`–`TODO_405`, `TODO_427`, `TODO_438`.
- **Three-way evidence classification:** every Layer 1/2/3 tag encountered during the above checks was independently re-derived from the primary source, not read off the document's own label.

**What was not fully checked (see §4, Remaining Issues):**

- The Decision Ledger's claimed total of 56 records and the Integrity Classification Ledger's claimed total of 31 records (8 Open) were not independently re-tallied — the underlying MCP tool payload (1,787 lines / 210K characters for the TODO register alone) makes a full recount expensive, and a 9-record individual spot-check (100% accurate) was judged sufficient confidence for this pass. A future audit should recount the aggregate totals directly.
- NIST AI RMF 1.0 (NIST AI 100-1) trustworthiness characteristics (`02_NIST_REQUIREMENT_ANALYSIS.md` §3) were not independently re-extracted from the source PDF — the document itself already flags this as an open, unresolved extraction failure; this audit did not attempt to resolve it.
- Not every individual Decision/Integrity/TODO ID cited across `04_REQUIREMENT_MAPPING.md`, `05_COMPARATIVE_ANALYSIS.md`, and `08_STRATEGIC_ASSESSMENT.md` was read in full (e.g., `DC_20260705_008`, `DC_20260708_005`, `DC_20260708_008`, `DC_20260709_003`, `DC_20260706_001`, `IC_20260705_011`, `IC_20260708_001`, the KN-001–007 series) — existence was confirmed for those checked via search/grep, but not all were read end-to-end for content-accuracy the way the 9 records above were.
- Private-repository content (`mocka-workshop-private`, `mocka-docs`, `mocka-core-private`, `planningcaliber`, `phi-os`, `vasAI`) was not accessed, consistent with the project's own stated scope boundary.

---

## 2. Findings

### Finding 1 — [MAJOR] `mocka-external-brain` is misclassified as documentation-only; a specific "file does not exist" claim about it is false

**Location:** `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §3 (as originally written); `appendix/evidence/full_repository_survey.md` §6 and summary table; `07_GAP_ANALYSIS.md` §1 (implicitly, via the "documentation with no corresponding code" framing); `05_COMPARATIVE_ANALYSIS.md` (Multi-Agent Coordination row, "well beyond `mocka-external-brain`'s documentation-only protocol description").

**Claim:** "documentation-only. Protocol specified entirely in README prose; no schema file, no bus implementation. Quick Start references `logs\bus\events.csv`, which does not exist."

**What I verified:** `git ls-tree -r origin/main` against the local, `origin`-synced clone at `C:/Users/sirok/mocka-external-brain` (HEAD `6e2f58634e0f6aabafa8087de9b3501cd78ac308`, matching the project's own cited commit) shows `logs/bus/events.csv` and two files under `logs/bus/rounds/` (`round_2026-02-08-001.md`, `round_2026-02-08-002.md`) as tracked files. `git show origin/main:logs/bus/events.csv` returns real content: 3,835 bytes, a CSV with header `event_id,timestamp,round_id,motion,actor,agent_name,kpa_id,content,content_ref,status,error_class,parent_event_id,evidence_ref,hash` and multiple populated rows dated 2026-02-08, including a full `share → ask → reply → decide` cycle with real deliberation text (in Japanese) and populated `parent_event_id`/`evidence_ref`/`hash` fields — i.e., the exact protocol schema the README describes in prose is not just described but actually instantiated with data.

**Discrepancy:** The claim that the file "does not exist" is false — it exists and is substantive. The broader verdict "documentation-only... no schema file, no bus implementation" is also inaccurate: a schema is implicitly present (the CSV header) and it has been exercised at least once with real content. This is not proof of a live, automated bus process (no orchestration code was found), so "Partially Implemented" (real data, no automation code) is the accurate classification — not "documentation-only" and not "Fully Implemented" either.

**Verdict:** CONFIRMED.

### Finding 2 — [MAJOR] Repository Coverage gap: a ninth public repository, `m-sirius-k/m-sirius-k`, was never surveyed

**Location:** `README.md`, `00_PROJECT_CHARTER.md` (repository list), `appendix/evidence/full_repository_survey.md`, `appendix/evidence/repository_evidence_register.md`, `10_REFERENCES.md` — none of these list this repository.

**Claim (implicit):** The project's repository survey is presented as covering "the MoCKA core repository... and seven adjacent public repositories under the `m-sirius-k` GitHub organization" (`00_PROJECT_CHARTER.md`), i.e., a complete accounting of public, non-excluded MoCKA repositories.

**What I verified:** `gh repo list m-sirius-k --limit 30 --json name,visibility,description` returns 18 repositories total. Cross-referencing against the project's stated 8-repo survey list and its explicitly-excluded list (`execution-runtime-system`, and 6 named private repos — all of which matched exactly what `gh repo list` shows as `PRIVATE`), one public repository is unaccounted for: `m-sirius-k/m-sirius-k`. This is GitHub's special "org/user profile" repository (a repo whose name matches the account name renders as the profile README). `gh api repos/m-sirius-k/m-sirius-k/git/trees/main?recursive=true` shows it contains `README.md` (MoCKA "Governance Layer" / "Shadow Movement" architecture prose, closely paralleling language in the core `MoCKA` README), `VERIFICATION_ARENA.md` (a "public verification index" claiming "public execution evidence" via a linked GitHub Actions workflow), `tools/portal_verify.py` (a real Python script), and `.github/workflows/portal_verify.yml` (a real, active CI workflow).

I additionally checked this workflow's run history: `gh api repos/m-sirius-k/m-sirius-k/actions/runs` shows its 12 most recent runs (spanning 2026-03-06 to 2026-03-22) **all have `conclusion: "failure"`**. Reading `tools/portal_verify.py`, the failure is structural: the script requires a file `DEMO_ARENA.md` with specific headings (`# MoCKA Demo Arena`, `# Demo 1 Browser Demo`, etc.), but the repository only contains `VERIFICATION_ARENA.md` with different headings — the script's required filename and the tracked filename do not match, so the check fails on every run by construction.

**Discrepancy:** This repository was not surveyed, so this project's repository-count claims ("eight ... repositories," `07_GAP_ANALYSIS.md` §1) are incomplete, and — notably — this repository independently exhibits the exact "advertised verification does not match actual repository state" pattern the project already identifies as its single most significant Gap Analysis finding elsewhere (§1). Missing it means the project's own headline finding is under-evidenced relative to what a complete survey would show (this instance is more severe than the others found: not just an absent script, but an actively-run, 100%-failing CI check).

**Verdict:** CONFIRMED.

### Finding 3 — [MINOR/MODERATE] CI workflow count for the core `MoCKA` repository undercounts by one

**Location:** `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §2; `appendix/evidence/full_repository_survey.md` (repo #1 detail and summary table); `appendix/evidence/repository_evidence_register.md`; `09_ROADMAP.md` item 5.

**Claim:** "six active GitHub Actions workflows (`canary_overrides.yml`, `mocka_guard.yml`, `mocka_regression.yml`, `phase18_determinism_matrix.yml`, `phios_regression.yml`, `transparency.yml`)."

**What I verified:** `git ls-tree -r origin/main --name-only -- .github/workflows/` in the `MoCKA` core repository returns **seven** files: the six listed, plus `research-gate-demo.yml`.

**Discrepancy:** Undercount by one, repeated consistently across four files (suggesting the omission happened once, early, and propagated rather than being independently re-checked each time it was repeated) — a copy-paste consistency issue more than an independent-verification issue, but each of the four instances individually reads as "Verified Public Evidence" without actually being a fresh count.

**Verdict:** CONFIRMED.

### Finding 4 — [MINOR] Event Ledger sample file count: "27 files" is stated in two places as if it is the combined total across two directories, but is only the count for one of them

**Location:** `05_COMPARATIVE_ANALYSIS.md` (Traceability row); `10_REFERENCES.md` (item 17). Note: `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §4 is worded correctly ("27 files under `data/storage/infield/` and further files under `data/storage/outbox/PILS_DONE/`") and was not in error.

**Claim:** "a small, stale April-2026 public sample of raw Event Ledger records under `data/storage/infield/` and `data/storage/outbox/PILS_DONE/` — 27 files" (05); "`data/storage/infield/*` and `data/storage/outbox/PILS_DONE/*` (Event Ledger sample, 27 files...)" (10).

**What I verified:** `git ls-tree -r origin/main --name-only -- data/storage/infield/ | wc -l` = 27. `git ls-tree -r origin/main --name-only -- data/storage/outbox/PILS_DONE/ | wc -l` = 22. Combined total = 49, not 27.

**Discrepancy:** Internal inconsistency between `03` (correct) and `05`/`10` (both undercount by treating "27" as the combined total). Minor in impact (doesn't change any Layer classification or conclusion — the sample is stale either way), but a genuine same-fact contradiction across files, which the audit brief specifically asked to check for (Internal Consistency, checklist item 6).

**Verdict:** CONFIRMED.

### Finding 5 — [MINOR] `CONSTITUTION.md` citation is ambiguous and, read literally, points to the wrong file

**Location:** `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §1.

**Claim:** "The general principle is stated in the public `MoCKA` repository's `CONSTITUTION.md` (Layer 1)" — referring to the "Event Ledger is append-only" / "5W1H" principles.

**What I verified:** The `MoCKA` repository has a root-level `CONSTITUTION.md` (5 lines) that is an unrelated UTF-8 encoding policy document ("MoCKA Encoding Policy v1.01") containing no mention of append-only ledgers or 5W1H. The actual source is a different file, `docs/CONSTITUTION.md` (25 lines), which does state "Event ledger is append-only" and "All decisions preserve 5W1H" verbatim.

**Discrepancy:** The underlying factual claim (that MoCKA's public repository states these constitutional principles) is true and now correctly cited. The original citation, unqualified as `CONSTITUTION.md`, was ambiguous at best and pointed to the wrong file when read as the root-level path — a real, if narrow, citation-precision defect given that a same-named-but-unrelated file exists at the root.

**Verdict:** CONFIRMED.

### Finding 6 — [Informational, no error found] NIST Concept Note quotations are verbatim-accurate

**Location:** `02_NIST_REQUIREMENT_ANALYSIS.md` §2.

I fetched the Concept Note PDF directly from its canonical NIST URL and extracted the full text of both pages. All eight of the quoted "example AI system" bullets in `02_NIST_REQUIREMENT_ANALYSIS.md` §2 match the source **word-for-word**. All eight quoted/paraphrased "activities" (a)–(h) also check out — the verbatim-quoted fragments (e.g., "legacy systems, physically distributed assets, and resourcing"; "rigorous testing, evaluation, validation, and verification (TEVV)"; "promoting visibility and collaboration across the supply chain of AI") are exact matches, and the paraphrased portions preserve meaning without overstatement. The document's date attribution ("2026-04-07") matches the PDF's own header date exactly (the "2026/04/08" in the hosting URL is NIST's upload-folder date, not the document's stated date — no error there). No mention of a "July 2026 discussion draft" or public-comment window exists anywhere in this 2-page Concept Note, consistent with the project's own conclusion that this claim is unverifiable from a primary NIST source. **This is the most carefully fact-checked section of the entire project** and no correction was needed.

### Finding 7 — [Informational, no error found] Extensive numeric/file-existence claims verified accurate

The following claims were checked directly against `origin/main` (not local working trees) and found accurate exactly as stated: `data/MOCKA_OVERVIEW.json`'s `"classification": "PRIVATE - ローカルのみ管理"` field and its commit hash `b7439e26d`; `governance/human_gate_cli.py`'s absence from `origin/main` and presence as an untracked local-only file; `mocka_events.db` being 0 bytes on `origin/main`; `data/MOCKA_TODO_ACTIVE.json`'s commit hash `3755c107f`; the full Orchestra file listing (`core_kernel/orchestra/`, `core_kernel/orchestra_core/`, gateway files); the 95-file test count; `mocka-runtime`'s exact 5-file, zero-code repository; `mocka-civilization`'s exact 146-file/139-`.md` count; `MoCKA-KNOWLEDGE-GATE`'s exact 13 disabled / 0 active workflow split; `mocka-outfield`'s empty `ledger/events_public.json` and its README's reference to a genuinely non-existent `events\outfield_log.csv`; `mocka-public`'s and `mocka-transparency`'s genuinely non-existent `verify_chain.py`/`verify_all.py`; the `MoCKA` repository's local working-tree state (60 modified/untracked files, 2 unpushed commits, matching the stated caveat exactly); and all 9 individually-retrieved Decision/Integrity/TODO records (`IC_20260708_004`, `DC_20260708_001`, `DC_20260706_004`, `IC_20260705_020`, `IC_20260707_005`, `DC_20260707_011`, `TODO_412`, `TODO_430`, `TODO_444`), each of which matched the project's characterization of its content closely. This gives reasonably high confidence in the internal-ledger evidence layer specifically, beyond what a smaller sample would justify.

---

## 3. Corrections Applied

All corrections were applied as additive, dated notes (matching the `appendix/REVIEW_LOG.md` convention) — no prior text was deleted, per the remediation policy.

| # | File | Location | Description |
|---|---|---|---|
| 1 | `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` | §3, `mocka-external-brain` bullet | Added correction note reclassifying from "Layer 3 only, no schema/bus" to "Layer 1, Partially Implemented" with the specific verified evidence (Finding 1) |
| 2 | `07_GAP_ANALYSIS.md` | §1 | Added correction note on the `mocka-external-brain` mischaracterization (Finding 1) |
| 3 | `07_GAP_ANALYSIS.md` | New §8 | Logged the `m-sirius-k/m-sirius-k` repository coverage gap and its failing-CI finding (Finding 2) |
| 4 | `appendix/evidence/full_repository_survey.md` | §6 (`mocka-external-brain`), summary table | Struck through the incorrect verdict, added corrected verdict, corrected `.md` file count (10, not 11), corrected the "Traceability/Audit" and "Multi-Agent Coordination" summary-table cells for this repo (Finding 1); added a note on the missed 9th repository (Finding 2) |
| 5 | `appendix/evidence/repository_evidence_register.md` | Correction-note block | Logged both the missing `mocka-external-brain` row and the missing `m-sirius-k/m-sirius-k` repository (Findings 1, 2) |
| 6 | `05_COMPARATIVE_ANALYSIS.md` | Multi-Agent Coordination row | Added correction note on `mocka-external-brain` (Finding 1) |
| 7 | `05_COMPARATIVE_ANALYSIS.md` | Traceability row | Corrected Event Ledger sample file count from "27" (ambiguous) to "27 + 22 = 49" (Finding 4) |
| 8 | `10_REFERENCES.md` | Reference 17 | Same file-count correction (Finding 4) |
| 9 | `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` | §2, Testing and CI bullet | Corrected CI workflow count from six to seven, named the omitted file (Finding 3) |
| 10 | `appendix/evidence/full_repository_survey.md` | Summary table, MoCKA (core) row | Same CI workflow count correction (Finding 3) |
| 11 | `appendix/evidence/repository_evidence_register.md` | CI / Runtime Governance row | Same CI workflow count correction (Finding 3) |
| 12 | `09_ROADMAP.md` | Item 5 | Same CI workflow count correction (Finding 3) |
| 13 | `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` | §1 | Corrected `CONSTITUTION.md` citation to `docs/CONSTITUTION.md`, with an explanation of the root-level file's unrelated content (Finding 5) |

---

## 4. Remaining Issues (for the project owner)

1. **Decision Ledger (56 records) and Integrity Classification Ledger (31 records, 8 Open) aggregate totals not independently re-tallied.** A 9-record spot-check was 100% accurate, but the stated totals themselves were not recounted against a full ledger export in this pass. Recommend a future audit (or a scripted count) directly verify these totals before the numbers are cited in any external-facing summary.
2. **`mocka-external-brain` and `m-sirius-k/m-sirius-k` have not been backfilled as full entries** in `appendix/evidence/full_repository_survey.md`'s per-repository detail sections or `appendix/evidence/repository_evidence_register.md`'s row table, or added to `10_REFERENCES.md`'s citation list. This audit logged both gaps and made minimal corrective notes (per the remediation policy's "do not silently rewrite" instruction) but did not attempt a full re-survey write-up of either repository, since that is closer to original authorship than minimal correction. Recommend the project owner (or the next revision cycle) complete a proper survey entry for both.
3. **`m-sirius-k/m-sirius-k`'s failing CI (12/12 recent runs) has not been triaged for whether it represents a real regression or a long-standing broken check.** Worth a brief look before deciding whether to fix the script, fix the filename, or remove the workflow.
4. **NIST AI RMF 1.0 (NIST AI 100-1) trustworthiness-characteristics list remains unverified from a re-extracted primary source** (`02_NIST_REQUIREMENT_ANALYSIS.md` §3) — this was already disclosed as an open item by the project itself, and this audit did not attempt to resolve it (out of the scope of confirming already-flagged items vs. finding new ones).
5. **Not every individually cited internal Decision/Integrity/TODO ID was read end-to-end.** IDs confirmed to exist via search/grep but not read in full for content-accuracy include `DC_20260705_008`, `DC_20260708_005`, `DC_20260708_008`, `DC_20260709_003`, `DC_20260706_001`, `DC_20260706_003`, `IC_20260705_011`, `IC_20260708_001`, and the `TODO_398`–`TODO_405`/KN-001–007 series. Given the 100% accuracy rate on the 9 records read in full, this is a reasonable-confidence gap rather than a known problem, but a future pass could close it.
6. **This report's own claims about GitHub Actions run history (Finding 2) and file listings were gathered via `gh api`/`git ls-tree` at a single point in time (2026-07-11)** and could drift if the repositories are updated before a reader checks this report.

---

## 5. Final Verdict

**Conditional Approval.**

Justification: This audit found and corrected 2 Major and 3 Minor factual/completeness errors across a 12-file, densely cross-referenced research project. None of the errors found undermine the project's core comparative conclusions — the `MoCKA` core repository's real, tested governance code; the broader repository constellation's documentation/implementation gap pattern; the internal-vs-public visibility gap; and the open, unresolved `IC_20260708_004` Human Gate enforcement finding all remain accurate and, if anything, are reinforced by the newly-found `m-sirius-k/m-sirius-k` evidence (Finding 2), which is an additional instance of the project's own headline Gap Analysis pattern that the original survey missed. The project's own NIST-quotation accuracy (Finding 6) and internal-ledger citation accuracy (Finding 7, 9/9 sampled) are both very high — this is a project with real evidentiary discipline that nonetheless had specific, findable gaps, consistent with any first-pass survey of this scope.

The Major findings (mocka-external-brain misclassification; the missed 9th repository) are exactly the class of error this Independent Audit step (per `README.md`'s own review table) exists to catch, and both have now been logged and minimally corrected in place, with fuller backfill work explicitly left to the project owner (§4, items 1–2) rather than performed unilaterally by this audit, consistent with the remediation policy's instruction not to silently rewrite prior claims.

**Approval is conditional on:** (a) the project owner reviewing the two Major-finding corrections in §3 and deciding whether to complete the fuller backfill noted in §4 items 1–2 before any external citation; (b) the Decision/Integrity Ledger aggregate totals (§4 item 1) being independently reconfirmed before those specific numbers ("56 records," "31 records," "8 Open") are used in any public-facing summary; (c) `m-sirius-k/m-sirius-k`'s failing CI (§4 item 3) being triaged, since it is now a disclosed, citable fact about the org's public surface. None of these conditions require re-doing the comparative analysis itself — they are targeted follow-ups on the specific gaps this audit surfaced.
