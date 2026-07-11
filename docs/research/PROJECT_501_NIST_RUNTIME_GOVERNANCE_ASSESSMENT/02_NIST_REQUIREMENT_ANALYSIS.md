# 02 — NIST Requirement Analysis

## 1. Evidentiary status of the "Community of Interest Discussion Draft, July 7, 2026"

This project was originally commissioned to compare MoCKA against a "NIST AI RMF Profile on Trustworthy AI in Critical Infrastructure (Community of Interest Discussion Draft, July 7, 2026)." During evidence-gathering, the following was established:

- **[Layer 1 — Verified Public Evidence]** NIST published a **Concept Note** titled *"Artificial Intelligence Risk Management Framework: Trustworthy AI in Critical Infrastructure Profile"* on **2026-04-07**, authored by Raymond Sheh and Martin Stanley (NIST Information Technology Laboratory), contact `aiframework@nist.gov`. Hosted at:
  `https://www.nist.gov/system/files/documents/2026/04/08/Concept%20Note_%20Development%20of%20the%20NIST%20AI%20RMF%20Trustworthy%20Use%20of%20AI%20in%20Critical%20Infrastructure%20Profile.pdf`
  The document was read in full (both pages) directly from this URL during this assessment.
- **[Layer 1 — Verified Public Evidence]** NIST's program page (`nist.gov/programs-projects/concept-note-ai-rmf-profile-trustworthy-ai-critical-infrastructure`) confirms project status "Ongoing," describes formation of a "Community of Interest," and states the development pathway as: Concept Note → Community of Interest formation → Draft Profile development → Public comment & finalization. It does **not** reference a discussion draft dated 2026-07-07.
- **Evidence Pending.** Several secondary sources (industry news aggregators, regulatory trackers) surfaced in web search reference a "discussion draft released July 7, 2026" and a public-comment window open through mid-August 2026. None could be traced to a primary NIST-hosted document during this assessment. Recorded as **Evidence Pending**, not fact.

**Conclusion:** Per explicit project-owner instruction, this project uses the verified Concept Note (2026-04-07) as the normative NIST reference throughout, and does not infer or reconstruct requirement language attributed to an unverified draft. Every characterization of NIST's position in this project cites either the Concept Note text quoted in §2 below, or NIST AI RMF 1.0 (NIST AI 100-1) as background reference (§3). If the July 2026 discussion draft is later obtained with a verifiable primary source, this project requires a full revision, particularly this file, `04_REQUIREMENT_MAPPING.md`, and `05_COMPARATIVE_ANALYSIS.md`.

## 2. Concept Note content, as read (2026-04-07) — [Layer 1, Verified Public Evidence]

The Concept Note states its purpose as launching development of "the AI RMF Trustworthy AI in Critical Infrastructure Profile," intended to "guide CI operators towards specific risk management practices... and help them to communicate their trustworthiness requirements in an actionable way to teams, developers, and other stakeholders across the AI and CI lifecycles and supply chains." It targets Information Technology (IT), Operational Technology (OT), and Industrial Control Systems (ICS) within critical infrastructure.

The Concept Note illustrates desired system properties through eight example AI system types, each paired with a specific trustworthiness feature (verbatim quotations):

1. "AI agents for autonomous cybersecurity incident response that include tested, evaluated, validated, and verified guardrails."
2. "AI-enabled facility and plant monitoring systems that are hardened against adversarial input and monitored for changes in the environment outside verified regions of validity."
3. "AI-enhanced deterministic diagnostic assistants that utilize AI bills of materials to provide traceable, auditable rationales for recommendations."
4. "Physics-informed neuro-symbolic AI systems for predicting and maintaining system stability that include verifiable performance guarantees."
5. "Autonomous robots and vehicles that leverage multimodal sensing, redundant safety systems, and deterministic fail-safe controllers."
6. "AI-powered digital twins for proactively managing distributed critical data centers to maintain operation during emergencies without overloading fragile utility infrastructure."
7. "AI optimization systems that degrade gracefully and transparently in response to adverse conditions while alerting human supervisors to take additional measures."
8. "AI-enabled, transparent, and explainable compliance and risk monitoring systems to improve governance responsiveness while maintaining human-in-the-loop oversight."

The Concept Note further states the profile "will apply the AI RMF in ways that include, but are not limited to" eight activities: (a) harmonizing cross-domain terminology; (b) tailoring risk-management requirements analysis to CI's "legacy systems, physically distributed assets, and resourcing"; (c) addressing "the need for deterministic behavior, explainability, graceful degradation, and fail-safe operation"; (d) "emphasizing the heightened need for adversarial robustness in all lifecycle stages"; (e) "rigorous testing, evaluation, validation, and verification (TEVV)"; (f) illuminating capability/trade-off comparisons between AI techniques; (g) "promoting visibility and collaboration across the supply chain of AI"; and (h) providing "practical, actionable, and measurable steps" usable "at any level of AI expertise and risk management maturity."

The document closes by inviting a "Community of Interest" to contribute via seminars, working sessions, RFIs, position papers, and drafts.

## 3. Background reference — AI RMF 1.0 trustworthiness characteristics — [Layer 3, Architecture Documented / background reference]

NIST AI RMF 1.0 (NIST AI 100-1, 2023) defines trustworthy AI systems in general terms as: **Valid and Reliable**, **Safe**, **Secure and Resilient**, **Accountable and Transparent**, **Explainable and Interpretable**, **Privacy-Enhanced**, and **Fair — with Harmful Bias Managed**. This characterization is drawn from established public record rather than re-extracted from the source PDF in this session — automated text extraction of `nist.ai.100-1.pdf` failed during this assessment (the retrieved copy rendered as non-text/image content to the extraction tooling used). **Flagged for direct-source verification before this project is finalized for external use.**

## 4. Requirement Decomposition (R1–R12)

Because no requirement-numbered draft profile is currently verifiable (§1), this project decomposes the Concept Note's themes into a working comparison-theme set. This decomposition is an **Analytical Interpretation** by this project's authors, not a NIST-authored requirement list.

| ID | Theme | Concept Note source |
|---|---|---|
| R1 | Human-in-the-loop oversight | Example 8; general framing |
| R2 | Traceability / auditable rationale | Example 3 |
| R3 | Deterministic behavior & fail-safe operation | Activity (c); Examples 4, 5 |
| R4 | Graceful, transparent degradation | Activity (c); Example 7 |
| R5 | Adversarial robustness (full lifecycle) | Activity (d); Example 2 |
| R6 | Testing, Evaluation, Validation, Verification (TEVV) | Activity (e); Example 1 |
| R7 | Explainability | Activity (c); Example 8 |
| R8 | Supply-chain visibility / collaboration | Activity (g) |
| R9 | Terminology harmonization / cross-sector interoperability | Activity (a) |
| R10 | Governance responsiveness / compliance monitoring | Example 8 |
| R11 | Verified operational monitoring outside validity regions | Example 2 |
| R12 | Practicality across expertise/maturity levels | Activity (h) |

`04_REQUIREMENT_MAPPING.md` and `06_EVIDENCE_TREE.md` map MoCKA's architecture and evidence against R1–R12.
