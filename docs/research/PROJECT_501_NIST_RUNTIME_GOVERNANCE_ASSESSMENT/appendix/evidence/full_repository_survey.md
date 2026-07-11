# Full Repository Survey (2026-07-11)

Full narrative detail behind `repository_evidence_register.md`. **Layer 1 — Verified Public Evidence** throughout unless marked otherwise.

**Methodology:** Local git clones (where present) were checked for `origin` sync state (`git status`, `git log -1`, ahead/behind count) before being treated as equivalent to public GitHub state. Repositories without a local clone were queried via authenticated `gh` CLI. `execution-runtime-system` and all private repositories under `m-sirius-k` were excluded (see `00_PROJECT_CHARTER.md`).

---

## 1. MoCKA (core)

- **Remote:** `git@github.com:m-sirius-k/MoCKA.git` — local clone `C:/Users/sirok/MoCKA`
- **Public HEAD used for evidence:** `origin/main` @ `e7a779a4cc982e75064249bdbcd9e3f2f1d907d1`, 2026-07-10 16:28:51+09:00
- **Caveat:** local working tree has 2 unpushed commits and 60 modified/untracked files, including a new untracked `governance/human_gate_cli.py` — **not present on GitHub**. All evidence below is drawn from `origin/main`, not the working tree.
- **Scale:** 6,253 tracked files; 2,762 `.py`; 521 `.md`; 95 files under `tests/` directories.
- **README:** describes MoCKA as a "deterministic governance architecture" implementing Observation→Record→Incident→Recurrence→Prevention→Decision→Action→Audit, with dual-path `mocka_Movement`/`shadow_Movement`.
- **Governance artifacts (paths):**
  - Architecture: `ARCHITECTURE.md`, `GATE_ARCHITECTURE_v1.md` (7 named "Gates," RATIFIED v1), `CONSTITUTION.md`, `docs/architecture/ARCHITECTURE_MOCKA_2_0_v1.md`
  - Decision: `decision/decision_engine.py`, `decision/decision_model.py`, `decision/decision_registry.py`, `decision/risk_analyzer.py`, `decision/priority_scorer.py` (explicitly non-executing; defers to Governance Layer GL1-7)
  - Human Gate: `governance/human_gate_continuity.py` (public, tested by `tests/test_human_gate_continuity.py`)
  - Audit: `audit/system_audit.py`, `audit/drift_report.py`, `audit/ed25519/{key_manager,daily_signature,governance_chain_verify}.py`, `verify_all.py`, `verify_full_chain_and_signature.py`, `self_audit/audit_engine.py`
  - Drift: `audit/drift_report.py`, `core_kernel/governance/intelligence/drift_interpreter.py`, `core_kernel/governance/self_verification/traceability/drift_detection.py` (explicit "Implementation drift" vs "Evidence/Audit drift" docstring distinction; "never recomputes a Decision or rewrites a record — it only flags mismatches")
  - Role/schema: `governance/keys/role_policy.json`, `governance/verify_role_policy.py` (schema `mocka.keys.role.definition.v1`)
  - Tests: `tests/test_canary_overrides.py`, `tests/test_seal_governance_gate.py`, `tests/test_shadow_seal_adapter.py`, `core_kernel/governance/tests/unit/test_traceability.py`, `core_kernel/governance/tests/integration/test_event_to_audit_flow.py`
  - CI: `.github/workflows/{canary_overrides,mocka_guard,mocka_regression,phase18_determinism_matrix,phios_regression,transparency}.yml`
- **Verdict:** the only repository in the survey with extensive, tested, cross-referenced implementation alongside its documentation.

## 2. mocka-runtime

- **Remote:** `https://github.com/m-sirius-k/mocka-runtime.git` — local clone in sync, HEAD `c995e5a9ee623c65068ebdec75db2b65926fd522`, 2026-06-17
- **README:** "Five Engine Architecture" (Runtime, Observatory, Knowledge Core, Storage, Audit), "Single Entry Point" guarantee ("No side effects, No hidden execution paths, No unrecorded actions")
- **Full tracked file list (5 total):** `ARCHITECTURE.md`, `CONCEPTS.md`, `README.md`, `llms.txt`, `llms-ja.txt`. **Zero source code files.**
- **Verdict:** documentation-only. `ARCHITECTURE.md` §8 ("Error Handling and Recovery") and §11 ("Design Principles") describe interfaces (`execute()`, `observe()`, `process()`, `store()`, `audit()`) with no corresponding code anywhere in the repository.

## 3. mocka-outfield

- **Remote:** `https://github.com/m-sirius-k/mocka-outfield.git` — local clone in sync, HEAD `5639f15f86b9b9bfc3feb1d3dd15049287e1009b`, 2026-06-17
- **README:** "sanitized boundary between the outside world and MoCKA core," cross-agent synchronization
- **17 tracked files:** 6 `.md`, 4 `.svg`, 3 `.txt`, 3 `.json`. No code.
- **Governance artifacts:** `governance/OUTFIELD_CONSTITUTION.md`, `governance/ai_participation_guide.md`, `ledger/events_public.json` — **verified empty (`[]`)**
- **Verdict:** documentation-only with an empty stub ledger. README Quick Start references `events\outfield_log.csv`, which does not exist in the tracked repo.

## 4. mocka-public

- **Remote:** `https://github.com/m-sirius-k/mocka-public.git` — local clone in sync, HEAD `f99b418ccd118296a4256b936d07ab07cf3239e5`, 2026-05-16
- **README:** "cryptographic proof" repo; Quick Start instructs `python verify_chain.py`
- **46 tracked files:** 30 `.md`, 8 `.pdf` (technical notes: XYZST, SPP, DNA, FCM, TRUST, AB2, CIVLOOP, plus a draft), 3 CI `.yml`, 2 `.txt`, 1 `.json`, 1 `.html`. **No `.py` files.**
- **Present:** `docs/PROOF.md`, `docs/SEAL.md`, `docs/SHADOW_MOVEMENT_PRINCIPLE.md`, `docs/PHASE13B_FREEZE.md`, `docs/PHASE17_STABLE_DECLARATION.md`, `docs/PHASE15_PROOF_DICTIONARY.md` — all Markdown declarations, not executable proofs
- **CI:** `.github/workflows/{phase18_determinism_matrix,research-gate-demo,transparency}.yml` present as files; no in-repo code for them to run against
- **Verdict:** documentation/paper-publication repo. `verify_chain.py`, referenced in the README's own Quick Start, **does not exist anywhere in the repository** (confirmed via full-repo search) — a direct discrepancy between claimed and actual contents.

## 5. mocka-civilization

- **Remote:** `https://github.com/m-sirius-k/mocka-civilization.git` — local clone in sync, HEAD `2efdaeae0148587dd366e7308dd42209557dd159`, 2026-03-29
- **README:** "the constitution of a knowledge civilization" — six "Immutable Principles" (Transparency, Reproducibility, Accountability, Immutability, Neutrality, Continuity), 21-phase roadmap (Phase 9-29)
- **146 tracked files, 139 `.md`.** No code (`governance/` contains only two `README.md` files).
- **Structure:** `blueprint/v1.0/`, `phase9/`-`phase29/`, `genesis/`, `lineage-registry/`, `derived-civilizations/`, `civilization-integration/`
- **Verdict:** pure documentation/doctrine repo. No ledger, no verification code, no tests, no CI.

## 6. mocka-external-brain

- **Remote:** `https://github.com/m-sirius-k/mocka-external-brain.git` — local clone in sync, HEAD `6e2f58634e0f6aabafa8087de9b3501cd78ac308`, 2026-03-29
- **README:** multi-agent deliberation council (Gemini/Perplexity/Claude/ChatGPT), "share → ask → reply → decide" protocol, structured messages (`motion_type`, `parent_event_id`, `evidence_ref`, `hash`)
- **19 tracked files, 11 `.md`.** No code. `logs/` exists but has no tracked content beyond structure.
- **Verdict (ORIGINAL, INCORRECT — see correction below):** ~~documentation-only. Protocol specified entirely in README prose; no schema file, no bus implementation. Quick Start references `logs\bus\events.csv`, which does not exist.~~

> **Independent Audit correction (2026-07-11):** This verdict is factually wrong. `git ls-tree -r origin/main` and `git show origin/main:logs/bus/events.csv` confirm the file **exists** (3,835 bytes) and contains real, timestamped (2026-02-08) multi-round deliberation records with columns `event_id, timestamp, round_id, motion, actor, agent_name, kpa_id, content, content_ref, status, error_class, parent_event_id, evidence_ref, hash` — i.e., the CSV literally implements the `motion_type`/`parent_event_id`/`evidence_ref`/`hash` schema the README describes in prose. Two further tracked files, `logs/bus/rounds/round_2026-02-08-001.md` and `round_2026-02-08-002.md`, are human-readable transcripts of the same rounds. **Corrected verdict: Partially Implemented (Layer 1) — real protocol-execution data exists, though no live orchestration/bus code was found (the CSV appears to be a manually- or semi-manually-produced record, not output of an automated bus process).** File count is 19 tracked files, of which 10 are `.md` (not 11 as originally stated — minor count correction). This also invalidates this repository's inclusion among "documentation-only" repos in `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §3, `05_COMPARATIVE_ANALYSIS.md` (Multi-Agent Coordination row), and the summary table below (Traceability/Audit and Multi-Agent Coordination columns for this row are corrected to "Partial — real data, no bus code"). See `appendix/INDEPENDENT_AUDIT_REPORT.md` Finding 1.

> **Corrective Action Phase addendum (2026-07-11) — Share/Ask/Reply/Decide implementation status, confirmed by full read of `logs/bus/events.csv`:** the file contains exactly **4 event rows**, forming one complete cycle, all dated 2026-02-08: (1) `share` by `orchestrator_core` — announces "Phase 2-A," establishing the protocol as shared context; (2) `ask` by `orchestrator_core` — requests a minimal ask/reply/decide operating spec, with an explicit structured-output requirement (conclusion/rationale/risk/alternative/next-action); (3) `reply` by `agent_perplexity` — a real, substantive answer proposing the Bus/event-dictionary design, linked via `parent_event_id` to the `ask` event; (4) `decide` by `orchestrator_core` — adopts a 5-point specification (Bus as primary nerve, ask/reply/decide as the 3 core motions, `parent_event_id` linkage, `evidence_ref`-based decision justification, `share` revision-within-round semantics), explicitly rejecting two alternatives (constant UI polling, OCR-as-primary-ingestion), linked via `evidence_ref` to the `reply` event. All four rows carry real SHA-256-format hash values. **This confirms the protocol was genuinely exercised at least once, by at least one real external AI (Perplexity), with real content and real cryptographic-style linkage — not a template or placeholder.** It does not confirm ongoing, automated, or multi-round operation: only one round-trip exists in the tracked data, and no scheduler/bus-server code was found anywhere in this repository to have produced it automatically (see `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §2 for where the actual automation code — `core_kernel/orchestra/`, etc. — lives, in the `MoCKA` core repository instead).

## 7. mocka-transparency

- **Remote:** `https://github.com/m-sirius-k/mocka-transparency.git` — local clone in sync, HEAD `8258711c071672cf46aa8f6133a4f2de6bcabd9d`, 2026-03-29
- **README:** "Tamper Detection Layer" — Ed25519 signatures, SHA256 append-only hash chain, public verifiability ("Not 'trust us.' 'Verify yourself.'")
- **59 tracked files (second-most code-bearing):** 10 `.py`, 12 `.md`, 9 `.json`, 6 `.ps1`, 5 `.pem`, 4 `.svg`, 4 `.bin`, 1 `.zip`, 1 `.tsr` (RFC3161 token)
- **Real implemented code:** `tools/verify_sig.py`, `tools/rfc3161_stamp.py`, `tools/generate_transparency_keys.py`, `tools/generate_outfield_rotation_key.py`, `sample01/{generate_manifest,sign_sample01}.py`, `sample02/{generate_chain_manifest,sign_chain_manifest}.py`, `sample03/{generate_rotation_manifest,sign_rotation_manifest}.py`, plus `scripts/{tamper_demo,verify_one,verify_sample02,verify_sample03,tamper_sample02,tamper_sample03}.ps1`
- **Discrepancy:** README Quick Start instructs `python verify_chain.py` and `python verify_all.py` at repo root — **neither exists anywhere in the tracked repository.** Actual entry points are the differently-named, per-sample scripts above.
- No CI workflows; no pytest-style test suite (verification is via the `.ps1` scripts).
- **Verdict:** partially implemented — real signing/verification/timestamping code and sample data exist, but the "one command verifies everything" README claim does not match actual entry points.

## 8. MoCKA-KNOWLEDGE-GATE

- **Remote:** `https://github.com/m-sirius-k/MoCKA-KNOWLEDGE-GATE.git` — local clone `C:/Users/sirok/mocka-knowledge-gate`, in sync, HEAD `29a620e221c1b217061879ce4d9dbfce3af9fe74`, 2026-03-29
- **README:** "Institutional Memory Layer" — hypothesis→attempt→validation→correction→retry as reproducible artifacts; event flow `mocka_Receptor` → `acceptor:infield` → `ledger.json` (SHA256 chain) → `governance/anchor_record.json` seal → `verify_all` check
- **359 tracked files:** 135 `.json`, 74 `.md`, 61 `.js`, 28 `.py`, 15 `.yml`, 15 `.yaml`
- **Real implemented code:** `gateway/src/server.ts` (TypeScript, has `package.json`), `middleware/server.py`, `middleware/utils.py`, `middleware/schema.sql`, `functions/mirror_github_to_gcs/main.py`, `integrations/canva_integration.py`, `law/MoCKA-law.yaml`, `mocka_api_spec.yaml`, `firestore_schema.js`
- **CI:** all 13 workflow files live under `.github/workflows.disabled/` (e.g., `mocka2-patrol.yml`, `mocka2-rollback.yml`, `mocka2-invite-verify.yml`, `phase1-pipeline.yml`) — the active `.github/workflows/` directory is **empty**
- **Docs:** `ARCHITECTURE.md`, `MOCKA-INTEGRATION-GUIDE.md`, `MOCKA_ROADMAP_PHASE4-6.md`, numerous `PHASE*_COMPLETE*.md` self-reported completion reports (narrative claims by the repo owner, not independently verifiable via tests/CI in this repository)
- **Verdict:** mixed — real server/middleware/integration code exists, but CI is present-yet-disabled, and "PHASE_COMPLETE" documents are self-attested.

---

## 9. m-sirius-k/m-sirius-k (added Corrective Action Phase, 2026-07-11 — closes Independent Audit Finding 2)

- **Remote:** `https://github.com/m-sirius-k/m-sirius-k.git` — GitHub org-profile repository (name matches org name), no local clone; surveyed via `gh api`, HEAD `aa634dfb95d42671a3394fee0e9eba76b4632f43`, 2026-03-22
- **README / testleadME.md:** "MoCKA Perpetual Mechanism" — Insert/Storage/Runtime/Audit cyclic architecture, Shadow Movement fail-safe (~75% Minimum Operating Capability), a documented but unimplemented 20-check "Research Gate" verification framework, and a `# Repositories` inventory consistent with this project's own scope
- **12 tracked files:** `README.md`, `VERIFICATION_ARENA.md`, `testleadME.md`, 6 SVG diagrams, `docs/verification/system_integrity.md`, `tools/make_perpetual_mechanism_svg.py`, `tools/portal_verify.py`, `.github/workflows/portal_verify.yml`, `.gitignore`. **No `.py` implementation beyond the two tools listed; no `LICENSE` file despite one being a documented check.**
- **CI:** `.github/workflows/portal_verify.yml`, 12/12 most recent runs (2026-03-06–2026-03-22) show `conclusion: "failure"`
- **Root cause (full detail: `07_GAP_ANALYSIS.md` §9, `appendix/evidence/REPOSITORY_SURVEY_ADDENDUM_m-sirius-k.md`):** `tools/portal_verify.py` requires a file `DEMO_ARENA.md` (repo has `VERIFICATION_ARENA.md` instead — never found) **and** 6 exact headings in `README.md` (3 of 6 missing from the live README). Either defect alone fails the check.
- **Separate discrepancy:** README's "RESEARCH_RUN OK — 20 verification checks passed" claim has no corresponding script/workflow anywhere in the repository — only the unrelated, 2-check `portal_verify.py` actually runs.
- **Verdict:** documentation-heavy with one small, real, but persistently-failing verification script. The clearest and most severe instance in this project's entire survey of the "advertised verification vs. actual repository state" pattern — unlike the absent-script cases elsewhere (`mocka-public`, `mocka-transparency`), this one is an *actively executing, publicly timestamped, continuously failing* CI check.

---

## Summary Table: Repository × Governance Theme

| Repo | Human Oversight/Gate | Traceability/Audit | Drift Detection | Explainability | Recovery/Resilience | Multi-Agent Coordination | Role Mgmt | Real Code | CI (active) |
|---|---|---|---|---|---|---|---|---|---|
| MoCKA (core) | Yes — code, tested; `human_gate_cli.py` local-only, unpublished | Yes — code | Yes — code | Partial — docs only | Yes — docs + partial code | Yes — docs | Yes — code | Yes, extensive | Yes (7 workflows; corrected from 6 by Independent Audit, 2026-07-11 — `research-gate-demo.yml` was omitted) |
| mocka-runtime | Docs only | Docs only | Not found | Docs only | Docs only | Not found | Not found | No | No |
| mocka-outfield | Docs only | Docs only; ledger empty | Not found | Not found | Not found | Docs only | Not found | No | No |
| mocka-public | Docs only | Docs only; claimed verifier absent | Not found | Not found | Docs only | Not found | Not found | No | Yes (files only, no code) |
| mocka-civilization | Docs only | Docs only | Not found | Not found | Docs only | Not found | Not found | No | No |
| mocka-external-brain | Docs only | Partial — real CSV/MD deliberation logs exist (`logs/bus/`), corrected 2026-07-11 | Not found | Not found | Not found | Yes — docs + real sample data | Not found | Partial (data, not orchestration code) | No |
| mocka-transparency | Not found | Yes — real code; claimed root verifiers absent | Not found | Not found | Docs only | Not found | Not found | Yes, partial | No |
| MoCKA-KNOWLEDGE-GATE | Docs only | Docs + partial code | Not found | Not found | Docs only | Not found | Not found | Yes, partial | Present but disabled |
| m-sirius-k/m-sirius-k | Not found | Docs only (unimplemented 20-check claim) | Not found | Not found | Docs only | Not found | Not found | Yes, minimal (2-check script) | Yes, but 12/12 runs failing |

**Key takeaway (updated, Corrective Action Phase 2026-07-11):** Of **9** public repositories now surveyed, only MoCKA (core) has substantial tested implementation. `mocka-transparency`, `MoCKA-KNOWLEDGE-GATE`, and `mocka-external-brain` have partial, real (narrower-scope) implementations — `mocka-external-brain`'s consists of genuine one-time deliberation-log data rather than live orchestration code. The remaining five (`mocka-runtime`, `mocka-outfield`, `mocka-public`, `mocka-civilization`, and now `m-sirius-k/m-sirius-k`) are documentation-primary, and three of the original five plus `m-sirius-k/m-sirius-k` have README/CI claims that don't match actual repository state — `m-sirius-k/m-sirius-k` is the most severe instance, with an actively-run, continuously-failing (12/12) public CI check.

**Resolution note:** the two gaps originally flagged by the Independent Audit (2026-07-11) — `mocka-external-brain`'s data being missed, and `m-sirius-k/m-sirius-k` being unsurveyed — are both closed as of this Corrective Action Phase update. Full detail: `appendix/CORRECTIVE_ACTION_REPORT.md`, `appendix/evidence/REPOSITORY_SURVEY_ADDENDUM_m-sirius-k.md`, `appendix/INDEPENDENT_AUDIT_REPORT.md` Findings 1–2.
