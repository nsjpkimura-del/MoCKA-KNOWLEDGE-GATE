# 06 — Evidence Tree

Full Evidence Tree form (Requirement → MoCKA Architecture → Repository → Documentation → Implementation → Verification Method → Current Status → Remaining Work → Assessment) for four representative requirement themes. Remaining themes (R3, R4, R5, R7, R8, R9, R10, R12) are covered in abbreviated form in `appendix/tables/abbreviated_evidence_trees.md`.

## R1 — Human-in-the-loop oversight

- **Requirement:** NIST Concept Note Example 8 and Activity (c) — human-in-the-loop oversight, deterministic/fail-safe behavior.
- **MoCKA Architecture:** Human Gate mechanism; Governance Layer (GL1–GL7); Decision Layer explicitly non-executing.
- **Repository:** `m-sirius-k/MoCKA` (public); internal references also touch `phi_os/human_gate.py` and `governance/mocka_git_safe_commit.py` (not confirmed public in this assessment).
- **Documentation:** `CONSTITUTION.md`, `GATE_ARCHITECTURE_v1.md`, `docs/audits/MOCKA_HUMAN_GATE_FINALIZATION_AUDIT_v1.md` (public).
- **Implementation:** `governance/human_gate_continuity.py` (public, tested).
- **Verification Method:** `tests/test_human_gate_continuity.py` (public, unit test); internally, live regression-test pass records cited in Decision Ledger.
- **Current Status:** Partially Implemented (Layer 1) / Under Construction (Layer 2).
- **Remaining Work:** Internal record IC_20260708_004 (Open, discovered 2026-07-08) documents that the `/audit/seal` (MANUAL_SEAL) endpoint currently reaches an audit-sealing action after passing only an automated policy check (GL7 `pre_execution_check()`), whose own docstring states that mechanical approval is explicitly *not* equivalent to Human Gate approval — yet no code path enforces the additional human step at this endpoint. Disclosed here as a genuine, currently open internal finding, unresolved as of this project's date.
- **Assessment:** MoCKA has real, tested human-gate code and an internal process mature enough to have found and logged this exact class of gap itself. The finding demonstrates the internal audit process functioning as intended even where the control it is auditing is incomplete — a materially different, more favorable signal than either "no oversight mechanism" or "silent/undisclosed gap" — but the gap itself remains open and unresolved.

## R2 — Traceability / auditable rationale

- **Requirement:** Concept Note Example 3 — "traceable, auditable rationales."
- **MoCKA Architecture:** Event Ledger (append-only) → Decision Ledger → Ed25519 signature chain → `anchor_record.json` seal.
- **Repository:** `m-sirius-k/MoCKA` (public, core audit modules); `mocka-transparency` (public, signing/verification tooling); `MoCKA-KNOWLEDGE-GATE` (public, ledger-flow description and middleware).
- **Documentation:** `docs/PROOF.md`, `docs/SEAL.md` (`mocka-public`, public).
- **Implementation:** `audit/ed25519/*.py` (public); `tools/verify_sig.py`, `tools/rfc3161_stamp.py` (`mocka-transparency`, public).
- **Verification Method:** `verify_all.py`, `verify_full_chain_and_signature.py` (public); per-sample verify scripts in `mocka-transparency` (public).
- **Current Status:** Partially Implemented (Layer 1 — real code, but `mocka-public`'s advertised `verify_chain.py` and `mocka-transparency`'s advertised root-level `verify_chain.py`/`verify_all.py` do not exist in either repository as tracked files; actual entry points are named differently and per-sample rather than unified).
- **Remaining Work:** Reconcile README "Quick Start" claims with actual script names/locations in `mocka-public` and `mocka-transparency`; publish a single, documented, unified verification entry point if that is the intended public-facing guarantee.
- **Assessment:** The underlying cryptographic mechanism (Ed25519 signing, hash chaining, RFC3161 timestamping) is real and present in public code — a stronger evidentiary position than most other repositories surveyed. The gap is documentation accuracy (README vs. actual file layout), not missing cryptographic substance.

## R6 — TEVV (Testing, Evaluation, Validation, Verification)

- **Requirement:** Concept Note Activity (e) — "rigorous testing, evaluation, validation, and verification (TEVV)."
- **MoCKA Architecture:** Repository-wide test suite; CI workflows; internal regression-test-pass records tied to specific decisions.
- **Repository:** `m-sirius-k/MoCKA` (public).
- **Documentation:** None dedicated; test intent implicit in CI workflow naming (`mocka_regression.yml`, `phios_regression.yml`).
- **Implementation:** 95 files under `tests/` directories (public, counted directly).
- **Verification Method:** Six active GitHub Actions workflows (public, confirmed present as files; this assessment did not independently confirm recent green CI run history).
- **Current Status:** Partially Implemented (Layer 1 — presence confirmed; historical pass/fail rate not independently verified) / Partially Implemented (Layer 2 — Decision Ledger records specific pass counts for specific changes, e.g. "7/7 regression tests passed" for TODO_415, DC_20260706_004).
- **Remaining Work:** An external reviewer cannot, from repository inspection alone, confirm current CI health without direct access to GitHub Actions run history, which was not part of this assessment's scope.
- **Assessment:** Structurally strong (real tests, real CI config) but this project cannot independently attest to current pass/fail status — flagged **Evidence Pending** for that specific sub-claim.

## R11 — Drift detection

- **Requirement:** Concept Note Example 2 — "monitored for changes in the environment outside verified regions of validity."
- **MoCKA Architecture:** Dedicated drift-detection modules with an explicit implementation/evidence-drift distinction.
- **Repository:** `m-sirius-k/MoCKA` (public).
- **Documentation:** Inline docstrings in the modules themselves (public); no separate standalone drift-detection design document located in the public survey.
- **Implementation:** `audit/drift_report.py`, `core_kernel/governance/intelligence/drift_interpreter.py`, `core_kernel/governance/self_verification/traceability/drift_detection.py` (all public).
- **Verification Method:** Not independently re-executed in this assessment; presence and docstring content confirmed by direct file read.
- **Current Status:** Partially Implemented (Layer 1) / Partially Implemented (Layer 2 — MCP Tool Registry Drift, a distinct but related internal drift category, is recorded as recurring and only partially mitigated, most recently recurring 2026-07-09).
- **Remaining Work:** The public drift-detection code addresses ledger/audit-record drift; not confirmed to cover the NIST framing of *operational/environmental* drift (an AI system's behavior moving outside a verified region of validity in a live control setting) — MoCKA's drift detection is evidenced for its own governance-record integrity, not for external system monitoring in an OT/ICS sense.
- **Assessment:** A real capability exists, but its scope (internal record-integrity drift) is narrower than NIST's illustrative framing (operational/environmental drift in deployed control systems). A genuine scope mismatch, stated plainly rather than elided.
