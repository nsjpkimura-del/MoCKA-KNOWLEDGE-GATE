# MRS-001 — Comparative Technical Assessment against NIST AI RMF Profile

**Project ID:** PROJECT_501_NIST_RUNTIME_GOVERNANCE_ASSESSMENT
**Institutional Series Identifier:** MRS-001 (MoCKA Research Series) — stable across all future revisions
**Version:** **v1.0-rc1 — SEALED (Release Candidate), 2026-07-11.** See [RELEASE_CANDIDATE_MANIFEST.md](RELEASE_CANDIDATE_MANIFEST.md) for the SHA-256 hash of every file in this version. No further edits shall be made under this version identifier — corrections go to v1.1+.
**Status:** Reviewed — Approved with Notes — Sealed
**Review Status:** Not yet reviewed by R01 or external party
**Verification Status:** Partially Verified (see Evidence Policy below; individual claims carry their own per-statement evidence tag)
**Owner:** R01 (Audit)
**Implementation Lead (per registration order):** Codex
**Supporting Roles (per registration order):** Claude, Gemini, ChatGPT (R01)
**Content authorship note:** v1.0 of this project's written content (all files below) was drafted by Claude (Sonnet 5) at the project owner's direction, using evidence gathered directly from public GitHub repositories, the NIST Concept Note, and MoCKA's internal MCP-exposed governance ledgers. No other AI system in the Supporting Roles roster contributed text to v1.0. Their listed roles reflect this registration order's institutional assignment, not a claim of authorship.
**Classification:** Research Project
**Priority:** Highest
**Institutional Classification:** MoCKA Research Series (MRS)
**Research Category:** Comparative AI Governance Assessment
**Related Repositories:** `m-sirius-k/MoCKA`, `m-sirius-k/mocka-runtime`, `m-sirius-k/mocka-outfield`, `m-sirius-k/mocka-public`, `m-sirius-k/mocka-civilization`, `m-sirius-k/mocka-external-brain`, `m-sirius-k/mocka-transparency`, `m-sirius-k/MoCKA-KNOWLEDGE-GATE`
**Related Decisions (internal):** DC_20260705_001–DC_20260711_002 (see `06_EVIDENCE_TREE.md`, `07_GAP_ANALYSIS.md`)
**Related Runtime Components:** Human Gate, Living Context (`MOCKA_OVERVIEW.json`), Decision Ledger, Event Ledger, Shadow Verification (`shadow_Movement`), Runtime Governance (GL1–GL7), Orchestra

---

## What this project is

A permanent, versioned MoCKA institutional research asset comparing the MoCKA Runtime Governance Framework against the NIST AI RMF Profile on Trustworthy AI in Critical Infrastructure. It is designed to be reused as MoCKA's comparative-governance baseline for future assessments against other frameworks (ISO/IEC, OECD, EU AI Act, OpenAI Preparedness Framework, Anthropic Constitutional AI, etc.) — see `08_STRATEGIC_ASSESSMENT.md` and `09_ROADMAP.md`.

This project does not attempt to demonstrate that MoCKA is superior to any external framework. It exists to answer, as precisely as available evidence allows: what does the reference framework require, what has MoCKA actually built, what evidence supports that, and what remains open.

## Document index

| File | Contents |
|---|---|
| [00_PROJECT_CHARTER.md](00_PROJECT_CHARTER.md) | Mission, scope, three-layer evidence policy, registration metadata |
| [01_EXECUTIVE_SUMMARY.md](01_EXECUTIVE_SUMMARY.md) | Top-level findings |
| [02_NIST_REQUIREMENT_ANALYSIS.md](02_NIST_REQUIREMENT_ANALYSIS.md) | NIST source material status + requirement decomposition (R1–R12) |
| [03_RUNTIME_GOVERNANCE_SPECIFICATION.md](03_RUNTIME_GOVERNANCE_SPECIFICATION.md) | Current MoCKA architecture, as evidenced |
| [04_REQUIREMENT_MAPPING.md](04_REQUIREMENT_MAPPING.md) | Requirement → architecture mapping |
| [05_COMPARATIVE_ANALYSIS.md](05_COMPARATIVE_ANALYSIS.md) | 21-dimension comparative matrix |
| [06_EVIDENCE_TREE.md](06_EVIDENCE_TREE.md) | Full evidence trees for representative requirements |
| [07_GAP_ANALYSIS.md](07_GAP_ANALYSIS.md) | Documentation/implementation gaps, open internal risks |
| [08_STRATEGIC_ASSESSMENT.md](08_STRATEGIC_ASSESSMENT.md) | Analytical interpretation and strategic reading |
| [09_ROADMAP.md](09_ROADMAP.md) | Future validation roadmap |
| [10_REFERENCES.md](10_REFERENCES.md) | Full citation list |
| [appendix/evidence/](appendix/evidence/) | Full repository-by-repository evidence register |
| [appendix/tables/](appendix/tables/) | Abbreviated evidence trees, remaining requirement themes |
| [appendix/diagrams/](appendix/diagrams/) | Reserved — no diagrams produced in v1.0 |
| [RELEASE_CANDIDATE_MANIFEST.md](RELEASE_CANDIDATE_MANIFEST.md) | **Seal record** — SHA-256 of every file in this version, freeze declaration, change policy |

## Superseded material

This project supersedes the single-file draft previously written at `docs/research/mocka_runtime_governance_nist_assessment_v1.md` and `docs/research/evidence/public_repo_survey_20260711.md`. That content has been redistributed into this structure without loss; the originals are removed to avoid two diverging copies of the same claims.

## R01 Review Status (Approved with Notes, 2026-07-11 — all four review phases complete)

| Item | Status |
|---|---|
| Current Classification | Reviewed — Approved with Notes |
| Institutional Registration | Completed |
| Technical Verification | **Complete** — Decision Ledger (56) and Integrity Ledger (31) fully recounted and cross-validated; see [appendix/LEDGER_FULL_RECOUNT_REPORT.md](appendix/LEDGER_FULL_RECOUNT_REPORT.md) |
| Evidence Collection | **Complete** — 9 public repositories surveyed (was 8), 3-layer classification independently re-verified |
| Repository Investigation | **Complete** — Phase 1 correction (2026-07-11) + Independent Audit Finding 2 remediation (`m-sirius-k/m-sirius-k` fully surveyed, 2026-07-11) |
| Independent Audit | **Complete** — see [appendix/INDEPENDENT_AUDIT_REPORT.md](appendix/INDEPENDENT_AUDIT_REPORT.md) |
| Corrective Action Phase | **Complete** — see [appendix/CORRECTIVE_ACTION_REPORT.md](appendix/CORRECTIVE_ACTION_REPORT.md) |
| Ledger Full Recount | **Complete** — found and corrected a real error (Integrity Ledger Open count: 8 stated → 21 actual); see [appendix/LEDGER_FULL_RECOUNT_REPORT.md](appendix/LEDGER_FULL_RECOUNT_REPORT.md) |
| Publication Approval | **Approved with Notes** — see [appendix/FINAL_VERIFICATION_REPORT.md](appendix/FINAL_VERIFICATION_REPORT.md) Part 3 for the 3 standing notes (none are blocking conditions) |

**Per R01's explicit instruction across every phase of this review: do not commit, do not push, do not create a release.** This project remains a local working tree only. "Approved with Notes" reflects that this project's evidence and methodology are sound, with 3 disclosed, non-blocking notes carried forward (`m-sirius-k/m-sirius-k`'s CI still failing and unfixed; NIST AI RMF 1.0 characteristics not re-extracted from primary source; `sirius-lab` exclusion basis not independently verified). Whether and when to commit, push, or otherwise publish this project remains a separate decision for the project owner.

## Outstanding before this can be cited externally

See `07_GAP_ANALYSIS.md` and `09_ROADMAP.md`. In short: (1) the actual NIST discussion-draft text referenced in this project's originating brief could not be independently verified and is not yet incorporated — v1.0 is built on the verified April 7, 2026 Concept Note only; (2) several public MoCKA repositories contain README instructions referencing files that do not exist; (3) one internal governance finding (IC_20260708_004) remains open. None of this is hidden — it is documented in full in the relevant sections.
