# Repository Survey Addendum — `m-sirius-k/m-sirius-k`

**Purpose:** closes Independent Audit Finding 2 (Major) — this repository was omitted from the original 8-repository survey. Written during the Corrective Action Phase, 2026-07-11. All content below is **Layer 1 — Verified Public Evidence**, gathered via `gh api` (this repository has no local clone) and cross-checked against `origin/main` at commit `aa634dfb95d42671a3394fee0e9eba76b4632f43` (2026-03-22T08:03:27Z, "update: README (final bilingual + svg fix)" — the current HEAD as of this addendum).

## Repository Survey

- **Type:** GitHub special "org/user profile" repository — a repository whose name matches the account name (`m-sirius-k`) renders as the profile README on `github.com/m-sirius-k`. It is a real, independently listed public repository (confirmed via `gh repo list m-sirius-k`), not a synthetic artifact of the API.
- **Full tracked file list (12 files):** `README.md`, `VERIFICATION_ARENA.md`, `testleadME.md`, `docs/images/{mocka_architecture,mocka_dual_movement,mocka_governance_layer_perpetual_mechanism,mocka_overview,mocka_workflow}.svg`, `docs/perpetual_mechanism.svg`, `docs/verification/system_integrity.md`, `tools/make_perpetual_mechanism_svg.py`, `tools/portal_verify.py`, `.github/workflows/portal_verify.yml`, `.gitignore`.
- No `LICENSE` file is present in this tracked file list, despite `docs/verification/system_integrity.md` describing a `repo_license_presence` check as part of its (unimplemented — see Verification Survey below) 20-check specification.

## Architecture Survey

`README.md` and `testleadME.md` both describe MoCKA as a "Perpetual Mechanism" / "Governance Layer" with an Insert → Storage → Runtime → Audit cyclic architecture and a "Shadow Movement" fail-safe design maintaining ~75% capability under partial failure ("Minimum Operating Capability"). This is consistent, in substance and even specific numeric claims (75%), with the `shadow_Movement` concept documented across the `MoCKA` core repo and `mocka-public`'s `SHADOW_MOVEMENT_PRINCIPLE.md` (see `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §1, §3) — no contradiction found; this repository's architecture description is consistent with, and appears to summarize, the same architecture documented elsewhere.

`testleadME.md` additionally contains a `# Repositories` section listing 6 repos: MoCKA Core, Knowledge Gate, Transparency, External Brain, Civilization Layer, and "Core Private" (marked "Internal repository"). This list is a subset of, and consistent with, this project's own repository inventory (`00_PROJECT_CHARTER.md`) — no repository is named here that is absent from this project's scope, and no contradiction was found.

**Notable internal artifact:** `testleadME.md` is a second, unpublished README-shaped document that already satisfies several of `tools/portal_verify.py`'s required README headings (`# Architecture`, `# Repositories`, `# Research Workflow`, `# Technical Backbone`, `# Verification Architecture` are all present verbatim as H1 headings) which the live `README.md` does not fully satisfy (see CI Survey below). Its filename does not follow any evident naming convention for a draft (not `README.draft.md`, not under a `drafts/` directory) and no comment or commit message explains its purpose. **Evidence Pending** as to whether this is an abandoned in-progress replacement for `README.md`, a template retained for reference, or something else — this project has no basis to infer intent beyond what is observable.

## Workflow Survey

One workflow file: `.github/workflows/portal_verify.yml`. Trigger conditions: `workflow_dispatch` (manual) and `push` to `main` touching `README.md`, `DEMO_ARENA.md`, `tools/**`, or the workflow file itself. Single job (`verify`), single step beyond checkout/setup: `python tools/portal_verify.py`.

## CI Survey

`gh api repos/m-sirius-k/m-sirius-k/actions/runs` returns 12 runs, all triggered by `push` events, spanning 2026-03-06T02:03:45Z to 2026-03-22T08:03:32Z. **All 12 have `conclusion: "failure"`.** No run has ever succeeded since the workflow was introduced, as far as the available run history shows.

## Verification Survey

`docs/verification/system_integrity.md` documents 7 named checks (`ecosystem_doctor_integrity`, `ecosystem_structure_scan`, `canon_directory_integrity`, `artifact_directory_integrity`, `repo_entrypoints_present`, `repo_git_clean_check`, `repo_license_presence`) as prose specifications (purpose + inspection content in Japanese), part of a larger, README-advertised "Research Gate" framework of 20 total checks across four domains (System Integrity: 7, Research Process: 4, Documentation: 3, Audit and Evidence: 6 — the full 20-item list appears verbatim in both `README.md` and `testleadME.md`).

**No script, workflow, or executable artifact implementing any of these 20 named checks was found anywhere in this repository's tracked file tree.** The only executable verification artifact present is `tools/portal_verify.py`, which implements exactly 2 checks (README heading presence, DEMO_ARENA.md heading presence) — a completely different, much narrower check than the 20 documented ones. The README's claim "RESEARCH_RUN OK — Verification checks executed: 20 — All verification checks passed" therefore has **no corresponding implementation evidence in this repository** — it is either aspirational/planned, generated by tooling not present here, or describes a system that exists elsewhere and was not surveyed as part of this project's defined scope.

This is a second, independent discrepancy from the `portal_verify.py` CI failure (see `07_GAP_ANALYSIS.md` §8/9 for both, treated separately per their different evidentiary character): the CI failure is a real, verifiable, currently-broken check; the "20 checks passed" claim is a check that, as far as this repository's tracked contents show, was never actually implemented to run at all.

## Consistency Check Against the Other 9 Surveyed Repositories

- **Architecture language:** consistent (Shadow Movement, Governance Layer terminology matches `MoCKA` core and `mocka-public`).
- **Repository inventory (`testleadME.md`'s `# Repositories` table):** consistent with, and a subset of, this project's own scope — no new repository named here that this project has not already accounted for.
- **Pattern match to this project's own headline Gap Analysis finding:** this repository independently exhibits the same "advertised verification does not match actual repository state" pattern found in `mocka-public` and `mocka-transparency` (`07_GAP_ANALYSIS.md` §1) — but is a more severe instance: those two repos have an *absent* script referenced by a README; this repository has an *actively running, continuously failing* CI check, which is a stronger and more visible form of the same underlying gap, and the only one of the three with public, timestamped, machine-verifiable failure evidence (the GitHub Actions run history itself).
- **No naming/terminology conflicts** were found between this repository's content and any other surveyed repository.

## Implementation Status Summary

| Component | Status | Evidence |
|---|---|---|
| Architecture description | Architecturally Defined (documentation only) | `README.md`, `testleadME.md` |
| Repository inventory claim | Verified consistent | `testleadME.md` § Repositories vs. `00_PROJECT_CHARTER.md` |
| `portal_verify.py` (2-check verifier) | Implemented, but currently and persistently failing | `tools/portal_verify.py`, CI run history (12/12 failure) |
| "Research Gate" 20-check framework | Evidence Pending / Documentation only — no implementation found in this repository | `README.md`, `testleadME.md`, `docs/verification/system_integrity.md` (spec text only) |
| `LICENSE` file | Not present, despite being one of the 20 documented checks | File tree |
