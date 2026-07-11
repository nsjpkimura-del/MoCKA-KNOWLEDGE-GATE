# 00 — Project Charter

## Mission

Register and maintain, as a permanent MoCKA institutional research asset, an evidence-based engineering comparison between the MoCKA Runtime Governance Framework and the NIST AI RMF Profile on Trustworthy AI in Critical Infrastructure. The document shall function simultaneously as: Technical Specification, Architecture Review, Institutional Audit Report, Comparative Research, Evidence Report, Engineering Baseline, Community of Interest Reference, and Future Standardization Baseline.

This is not a promotional document. It does not argue MoCKA's superiority over any external framework. It exists so that an independent reviewer — NIST, an academic reviewer, an engineering auditor, or an industrial AI governance expert, with no prior MoCKA knowledge — can determine: what the reference framework requires, what MoCKA has actually implemented, what evidence supports that, what remains under development, and where MoCKA's concepts extend beyond the current external discussion.

## Registration metadata

| Field | Value |
|---|---|
| Project ID | PROJECT_501_NIST_RUNTIME_GOVERNANCE_ASSESSMENT |
| Series Identifier | MRS-001 (MoCKA Research Series) — stable across v1.1, v1.2, v2.0, etc. |
| Version | 1.0 |
| Status | Draft — Institutional Review |
| Owner | R01 (Audit) |
| Review Status | Not yet reviewed |
| Verification Status | Partially Verified — see Evidence Policy; every individual claim in this project carries its own evidence tag rather than a single project-wide status |
| Institutional Classification | Research Project / MoCKA Research Series |
| Research Category | Comparative AI Governance Assessment |
| Related Repositories | See `README.md` |
| Related Decisions | Internal Decision Ledger `DC_20260705_001`–`DC_20260711_002` |
| Related Runtime Components | Human Gate, Living Context, Decision Ledger, Event Ledger, Shadow Verification, Runtime Governance (GL1–GL7), Orchestra |

## Scope

**In scope:**
- The NIST AI RMF Profile on Trustworthy AI in Critical Infrastructure, as represented by the sole verifiable public NIST document as of 2026-07-11: the Concept Note dated 2026-04-07 (`02_NIST_REQUIREMENT_ANALYSIS.md`).
- The MoCKA core repository (`m-sirius-k/MoCKA`, public) and eight adjacent public repositories under the `m-sirius-k` GitHub organization (updated Corrective Action Phase, 2026-07-11: `m-sirius-k/m-sirius-k`, the org-profile repository, was added after the Independent Audit found it had been omitted — see `appendix/evidence/REPOSITORY_SURVEY_ADDENDUM_m-sirius-k.md`).
- Internal MoCKA governance records (Decision Ledger, Integrity Classification Ledger, TODO Register) as of 2026-07-11, used only for Gap Analysis and Strategic Assessment, and always labeled per the Evidence Policy below.

**Explicitly out of scope:**
- `execution-runtime-system` — per the project owner's own governance record, this is a separate, unrelated project with a defined boundary rule prohibiting bidirectional integration with MoCKA. Excluded from all mapping in this project.
- `sirius-lab` and `sirius-lab-products` — public repositories under the `m-sirius-k` org, understood to be a separate product line (AI productivity Chrome extensions/apps) distinct from the MoCKA governance framework this project compares against NIST. **Added Corrective Action Phase, 2026-07-11** — these were not surveyed and not previously listed here; noted as an Observation-priority documentation gap in `appendix/CORRECTIVE_ACTION_REPORT.md` item 7. This exclusion has not been independently re-verified with the same rigor as the `execution-runtime-system` boundary rule (which is grounded in a specific internal governance record); it reflects the project owner's general product-line understanding.
- Private MoCKA-family repositories (`mocka-workshop-private`, `mocka-docs`, `mocka-core-private`, `planningcaliber`, `phi-os`, `vasAI`) — not surveyed for Layer 1 (Public Evidence) claims.
- Any legal, regulatory, or compliance determination. Engineering/architecture comparison only.

## Evidence Policy

Evidence is classified into three independent layers. **Evidence levels shall never be mixed** — no statement may combine claims from more than one layer without explicitly labeling each component.

| Layer | Name | Definition |
|---|---|---|
| **Layer 1** | Public Evidence | Externally verifiable by any reviewer: public GitHub repositories, public NIST documents, published papers, public commit history. Reproducible by a third party without any access grant from the project owner. |
| **Layer 2** | Internal Institutional Evidence | Institutionally verified (queried directly from MoCKA's internal systems during this assessment) but not publicly reproducible: Decision Ledger, Integrity Classification Ledger, TODO Register, private repositories, internal governance documents. Always labeled **"Internal Evidence (Not Publicly Verifiable)"** at point of use. |
| **Layer 3** | Conceptual Architecture | Designed concepts, documented intent, or stated design principles with no implementation evidence located in either Layer 1 or Layer 2 during this assessment. Labeled **"Architecture Documented (no implementation evidence found)"** at point of use. |

A secondary, per-statement status tag is also applied throughout this project, drawn from: **Verified Public Evidence, Verified Internal Evidence, Architecture Documented, Implementation In Progress, Planned, Evidence Pending.** These per-statement tags operate within a layer; they do not substitute for the layer classification.

## Evidence classification methodology

All **Layer 1 / Verified Public Evidence** claims in this project were established by one of: (a) direct retrieval and reading of a publicly hosted document via its canonical URL, (b) direct inspection of a local, `git status`-confirmed-clean, `origin`-synced clone of a public GitHub repository, or (c) `gh` CLI queries against GitHub's API under an authenticated, read-scoped session. All **Layer 2 / Verified Internal Evidence** claims were established by direct query of MoCKA's internal MCP-exposed governance tools (Decision Ledger, Integrity Classification Ledger, TODO Register) on 2026-07-11. No claim in this project was generated by inference from either the NIST Concept Note's or MoCKA's own aspirational documentation without a corresponding direct-evidence check.

## No-advocacy principle

This project does not attempt to prove MoCKA superior to any existing or future framework. Every section objectively states which requirements are addressed, partially addressed, under development, or out of current scope, and explicitly discloses open internal governance findings (see `07_GAP_ANALYSIS.md`) rather than omitting them.
