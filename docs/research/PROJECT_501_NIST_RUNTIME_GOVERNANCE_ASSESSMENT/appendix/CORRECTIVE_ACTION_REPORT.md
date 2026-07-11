# Corrective Action Report

**Phase:** Independent Audit Corrective Action Phase, per R01 指示書 (2026-07-11).
**Principle:** this phase improves the deliverable in light of the audit; it does not rewrite the audit. `appendix/INDEPENDENT_AUDIT_REPORT.md` is preserved in full and unmodified as the audit record. All findings below remain visible in that file; nothing has been deleted or overwritten. All corrections are recorded as additive, dated notes in the affected files and summarized here.
**Scope of work performed in this phase:** local file updates only, within `docs/research/PROJECT_501_NIST_RUNTIME_GOVERNANCE_ASSESSMENT/`. No `git commit`, `git push`, release, tag, or CI configuration change was performed against any repository.

---

## Major Finding 1 — `mocka-external-brain` misclassification

**Audit finding:** the project claimed `logs/bus/events.csv` "does not exist" and that the repository had "no schema file, no bus implementation." Both claims were false.

**Corrective investigation performed this phase:** read the full content of `logs/bus/events.csv` (all 4 rows) and both files under `logs/bus/rounds/`, directly from `origin/main` at the commit already cited (`6e2f58634`).

**Findings confirmed:**
- The file contains exactly **one complete Share → Ask → Reply → Decide cycle**, dated 2026-02-08: a `share` event (context-setting), an `ask` event (requests a minimal ask/reply/decide operating spec with a defined 5-part output structure), a `reply` event from a real external AI agent (`agent_perplexity`, substantive proposed design), and a `decide` event (adopts a 5-point specification, explicitly records two rejected alternatives, links to the `reply` via `evidence_ref`).
- All four rows carry populated SHA-256-format `hash` fields and correct `parent_event_id`/`evidence_ref` chaining consistent with the schema the README describes.
- This confirms the protocol was **genuinely exercised, once, with a real external AI participant** — not fabricated or templated content.
- It does **not** confirm live, automated, or ongoing multi-round operation. No bus-server, scheduler, or orchestration code exists in this repository to have produced this data automatically. The actual automation code for MoCKA's multi-agent system lives in the `MoCKA` core repository (`core_kernel/orchestra/`, `gateway/`), confirmed separately during the original Phase 1 review (`03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §2).

**Classification correction:** `mocka-external-brain` moves from "documentation-only, Architecturally Defined" to **Partially Implemented, Layer 1 (Public)** — real execution data exists, but no automation code in this specific repository.

**Files updated this phase:**
- `appendix/evidence/full_repository_survey.md` §6 — added the full 4-event breakdown as a Corrective Action Phase addendum, on top of the Independent Audit's initial correction.
- `05_COMPARATIVE_ANALYSIS.md` (Multi-Agent Coordination row) — refined with the specific event count and cross-reference to where the real automation code actually lives.
- `appendix/evidence/repository_evidence_register.md` — backfilled a full row (was previously only a correction-note, not a table row).
- `10_REFERENCES.md` — added Reference 19 citing the specific file and read date.

**Residual scope not addressed this phase:** whether the single 2026-02-08 cycle represents a one-time test/demo or was intended as an ongoing practice that was subsequently discontinued is **Evidence Pending** — no commit history analysis of *why* activity stopped after one round was performed, as it was outside this corrective action's scope (which is to correct the classification error, not to conduct a new investigation into repository history/intent).

---

## Major Finding 2 — `m-sirius-k/m-sirius-k` repository coverage gap

**Audit finding:** a ninth public repository under the `m-sirius-k` org was never surveyed, and it contains a CI verification check with a 12/12 failure rate.

**Corrective investigation performed this phase:** full repository survey (file tree, all document content, workflow definition, verification script source, CI run history) via `gh api`, since no local clone exists. Full results: `appendix/evidence/REPOSITORY_SURVEY_ADDENDUM_m-sirius-k.md`.

**Findings beyond what the Independent Audit had time to establish:**
- The CI failure has **two independent causes**, not one: (a) the script's hardcoded filename (`DEMO_ARENA.md`) doesn't match the tracked file (`VERIFICATION_ARENA.md`); (b) independently, the live `README.md` is missing 3 of 6 headings the script requires, so fixing (a) alone would not fix the check.
- A second, distinct discrepancy was found: the README's claim of "20 verification checks passed" (a "Research Gate" framework) has **no corresponding implementation anywhere in the repository** — only the unrelated, much narrower `portal_verify.py` (2 checks) actually exists and runs.
- A candidate explanation for the mismatch was found: `testleadME.md`, an untracked-by-any-workflow file, already satisfies 5 of the 6 required README headings — possibly an abandoned in-progress fix, though this project has no basis to confirm intent.

**Classification:** the repository is documentation-heavy with one small, real, but persistently-failing verification script — the most severe instance of this project's "advertised vs. actual" pattern found anywhere in the survey (an actively-run, publicly-timestamped, continuously-failing CI check, vs. the merely-absent scripts found elsewhere).

**Files created/updated this phase:**
- **New:** `appendix/evidence/REPOSITORY_SURVEY_ADDENDUM_m-sirius-k.md` — full Repository/Architecture/Workflow/CI/Verification survey, plus a consistency check against the other 9 repositories (no conflicts found).
- `appendix/evidence/full_repository_survey.md` — added full `## 9. m-sirius-k/m-sirius-k` section and summary-table row; updated the "Key takeaway" to reflect 9 repositories surveyed.
- `appendix/evidence/repository_evidence_register.md` — backfilled 2 new rows.
- `10_REFERENCES.md` — added Reference 20.
- `07_GAP_ANALYSIS.md` §8 — marked CLOSED, pointing to the new addendum.

---

## CI Investigation — `DEMO_ARENA.md` / `VERIFICATION_ARENA.md` mismatch

Recorded as its own independent Gap per explicit instruction, separate from the general repository-coverage gap above. Full cause / impact scope / reproduction steps / remediation options are in **`07_GAP_ANALYSIS.md` §9** (new section, this phase). Status: **Open** — this project has documented the finding and presented remediation options (conform content to checker; conform checker to content; retire the check) without prescribing one, consistent with the no-advocacy principle. Implementing a fix is a decision for the project owner.

---

## Minor Findings — re-verification

All three Minor Findings from the Independent Audit were independently re-verified from primary sources during this phase (not merely re-read from the audit report):

| Finding | Re-verification performed | Result |
|---|---|---|
| CI workflow count (6 vs. 7) | `git ls-tree -r origin/main -- .github/workflows/` in `MoCKA` core repo, 2026-07-11 | **Confirmed: 7 files.** `research-gate-demo.yml` was indeed the omitted file. Audit's correction was accurate. |
| Event Ledger sample count (27 vs. 49) | `git ls-tree -r origin/main -- data/storage/infield/` (27) and `-- data/storage/outbox/PILS_DONE/` (22), 2026-07-11 | **Confirmed: 27 + 22 = 49.** Audit's correction was accurate. |
| `CONSTITUTION.md` citation | `git show origin/main:CONSTITUTION.md` (root — unrelated encoding-policy doc, 5 lines) vs. `git show origin/main:docs/CONSTITUTION.md` (25 lines, contains the actual quoted principles) | **Confirmed.** Audit's correction was accurate. |

No further corrections were needed for the Minor Findings; the Independent Audit's original fixes were verified sound. This is recorded in `appendix/REVIEW_LOG.md`.

---

## Remaining Issues — reclassified by priority

Per R01 instruction, the Independent Audit's 6 "Remaining Issues" are reclassified below using Critical / Major / Minor / Observation, each with content, impact, evidence, and recommended action.

| # | Content | Priority | Impact | Evidence | Recommended Action |
|---|---|---|---|---|---|
| 1 | Decision Ledger (56) / Integrity Ledger (31, 8 Open) aggregate counts not independently re-tallied | **Major** | These exact numbers are cited repeatedly across the project (Executive Summary, Runtime Governance Spec, References) as headline internal-evidence figures; if wrong, several files would need correction | 9/9 individually spot-checked records were accurate (Independent Audit Finding 7), but no full recount was performed | **Closed (Ledger Full Recount phase, 2026-07-11).** Full recount performed: Decision Ledger (56, all Active) — **Verified, matches exactly.** Integrity Ledger total (31) — **Verified.** Integrity Ledger Open count — **Not Verified as previously stated: actual is 21 Open (not 8), plus 10 Resolved (previously unstated).** Full detail, method, and corrections applied: `appendix/LEDGER_FULL_RECOUNT_REPORT.md`. |
| 2 | `mocka-external-brain` and `m-sirius-k/m-sirius-k` full survey write-ups | **Closed this phase** | — | See Major Findings 1–2 above | No further action needed |
| 3 | `m-sirius-k/m-sirius-k` failing CI not triaged for real-regression vs. long-standing-broken | **Minor** | Reputational (public-facing, continuously failing check on the org's profile repo); no operational MoCKA dependency found | `07_GAP_ANALYSIS.md` §9 — root cause fully diagnosed this phase; three remediation options presented | Project owner selects and implements one of the three remediation options in §9 |
| 4 | NIST AI RMF 1.0 trustworthiness characteristics not re-extracted from primary PDF | **Minor** | Affects only `02_NIST_REQUIREMENT_ANALYSIS.md` §3, already explicitly flagged there as unverified since v1.0; does not affect any Requirement Mapping conclusion, which is sourced from the Concept Note directly, not from AI RMF 1.0 | PDF text-extraction failure, documented since v1.0 | Retry extraction with different tooling (e.g., OCR) or manually transcribe the relevant section in a future revision |
| 5 | Not every cited internal Decision/Integrity/TODO ID read end-to-end (existence confirmed via search only) | **Observation** | Low — the 9 IDs that were read in full were 100% accurate, suggesting low risk for the remainder, but this is inference, not verification | `appendix/INDEPENDENT_AUDIT_REPORT.md` §1, list of unread IDs | Optional: expand the spot-check sample in a future audit pass if these specific IDs become load-bearing for an external claim |
| 6 | Point-in-time nature of `gh api`/`git ls-tree` findings (could drift if repos change) | **Observation** | Inherent to any evidence-based audit of a live system; not a defect | N/A — methodological property, not a finding | Re-run the relevant verification commands before any future external submission, rather than relying on this report's snapshot indefinitely |

**New item surfaced this phase (not in the original Remaining Issues list):**

| # | Content | Priority | Impact | Evidence | Recommended Action |
|---|---|---|---|---|---|
| 7 | `sirius-lab` and `sirius-lab-products` (public repos under `m-sirius-k`, per `gh repo list`) are outside this project's stated scope but were never explicitly excluded in `00_PROJECT_CHARTER.md`'s "Explicitly out of scope" list, unlike `execution-runtime-system` | **Observation** | Low — these are understood (per project-owner memory context, not re-verified this phase) to be a separate product line (Chrome-extension productivity tools), not part of the governance-framework comparison; but the Charter is silent on them, which is a documentation completeness gap of the same *type* (if much smaller stakes) as Major Finding 2 | `gh repo list m-sirius-k` shows both as public | If confirmed out of scope, add them to `00_PROJECT_CHARTER.md`'s exclusion list with a one-line justification, matching the treatment already given to `execution-runtime-system` |

---

## Summary of Files Touched This Phase

**New files:** `appendix/evidence/REPOSITORY_SURVEY_ADDENDUM_m-sirius-k.md`, `appendix/CORRECTIVE_ACTION_REPORT.md` (this file), `appendix/FINAL_VERIFICATION_REPORT.md` (see next).

**Updated files:** `07_GAP_ANALYSIS.md` (§8 closed, new §9), `05_COMPARATIVE_ANALYSIS.md` (Multi-Agent Coordination, Verification rows), `04_REQUIREMENT_MAPPING.md` (R6 caveat), `appendix/evidence/full_repository_survey.md` (§6 expanded, new §9, summary table + key takeaway updated), `appendix/evidence/repository_evidence_register.md` (3 new rows backfilled), `10_REFERENCES.md` (References 19–20 added), `appendix/REVIEW_LOG.md` (this phase's entry appended, see that file).

**Unmodified, preserved as audit record:** `appendix/INDEPENDENT_AUDIT_REPORT.md` — no findings deleted or overwritten.
