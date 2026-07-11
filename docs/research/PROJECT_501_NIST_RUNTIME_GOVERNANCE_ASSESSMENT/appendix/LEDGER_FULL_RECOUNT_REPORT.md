# Ledger Full Recount Report

**Phase:** Final Evidence Closure (Ledger Full Recount), per R01 指示書, 2026-07-11.
**Purpose:** close the single remaining Evidence Gap from `appendix/FINAL_VERIFICATION_REPORT.md` (Part 2, item 1) via full recount of every record, not sampling. No figure below is transcribed from any prior document in this project — every number was independently computed from a fresh primary-source query performed during this phase.

---

## Methodology (stated up front, per instruction, so results are independently reproducible)

Both ledgers are exposed via MCP tools (`mcp__caaeec1f-f353-4fb6-bd7c-4fff0fe700fc__mocka_decision_list`, `..._mocka_integrity_list`), each supporting an optional `status` filter. Two independent counting methods were used and cross-checked against each other:

1. **Unfiltered pull + direct parse:** call the tool with no `status` filter to retrieve every record, then independently count records (not trust the tool's self-reported `count` field alone) via a separate check — array length, and count of unique ID values (to rule out duplicate-record inflation).
2. **Filtered-query cross-check:** call the tool once per possible `status` value, sum the resulting per-status counts, and confirm the sum equals the unfiltered total.

A result is only treated as confirmed where methods (1) and (2) agree.

---

## Task 1 — Decision Ledger Full Recount

**Data source:** `mocka_decision_list` (no filter), queried 2026-07-11. Because the raw response (120,963 characters, 1,593 lines) exceeds this session's inline tool-output limit, the harness auto-saved it to a local file, which was then parsed directly and reproducibly with Python's `json` module (not read/summarized by eye):

```
python3 -c "
import json
data = json.load(open(r'<saved-tool-output-path>', encoding='utf-8'))
print('reported count field:', data.get('count'))
decisions = data['decisions']
print('actual len(decisions):', len(decisions))
ids = [d.get('decision_id') for d in decisions]
print('unique decision_ids:', len(set(ids)))
import collections
print('status value counts:', dict(collections.Counter(d.get('status') for d in decisions)))
"
```

**Result:**
- Tool-reported `count` field: **56**
- `len(decisions)` (actual array length): **56** — matches
- Unique `decision_id` values: **56** — matches (0 duplicate IDs)
- `min(ids)` = `DC_20260705_001`, `max(ids)` = `DC_20260711_002`
- Status breakdown from direct parse: **`{"Active": 56}`** — all 56 records carry `status: "Active"` in the literal field; zero records have any other `status` value

**Cross-check via individual filtered queries** (`mocka_decision_list(status=...)`, called separately, sequentially — not in the same parallel batch as other calls, see Anomaly note below):
- `status="Active"` → 56 records returned (full match)
- `status="Superseded"` → **0** records
- `status="Withdrawn"` → **0** records
- Sum: 56 + 0 + 0 = 56 — matches the unfiltered total exactly.

**Lineage nuance (not a discrepancy, but worth recording precisely):** two record pairs carry non-null `supersedes`/`superseded_by` relational fields despite both records in each pair having `status: "Active"`:
- `DC_20260707_003.supersedes = "DC_20260707_002"` (and `DC_20260707_002.superseded_by` was checked and found `None` — the relationship is recorded one-directionally, from the newer record pointing back)
- `DC_20260705_009.supersedes = "DC_20260705_008"` (same one-directional pattern)

This confirms the schema's `status` field tracks record validity/append-only integrity (i.e., "this ledger entry is a legitimate, non-retracted record"), not "this is still the currently operative decision" — that second, practically-relevant notion of currency is carried by the `supersedes` pointer instead. Prior project text describing this ("all status=Active... except DC_20260707_002→superseded by DC_20260707_003, and DC_20260705_008→corrected by DC_20260705_009") was **accurate** and is confirmed by this recount, precisely because it already reflected this same status/lineage distinction rather than conflating the two.

**Anomaly observed (documented for transparency, does not affect the result above):** when `status="Active"`, `status="Superseded"`, and `status="Withdrawn"` were first queried together in a single parallel batch of six simultaneous MCP calls (alongside four `mocka_integrity_list` calls), all three decision-ledger filtered queries anomalously returned `{"count": 0, "decisions": []}` — including `status="Active"`, which should self-evidently return 56 records given the direct-parse result above. Re-running each filtered query individually and sequentially (not in a large parallel batch) produced the correct, consistent results reported above. This is recorded as an observed tool-behavior anomaly under high concurrent load, not a data integrity issue — the authoritative figures in this report rely on the unfiltered direct-parse method (which does not depend on the filter parameter at all) and are confirmed by the sequential filtered re-query.

### Task 4 Classification — Decision Ledger: **Verified**

Existing project claim ("56 records, all status=Active, with 2 lineage-superseded pairs") matches the full recount exactly, on every sub-figure checked. No difference found.

---

## Task 2 — Integrity Classification Ledger Full Recount

**Data source:** `mocka_integrity_list`, queried 2026-07-11, four separate calls: no filter (total), `status="Open"`, `status="Resolved"`, `status="Superseded"`. All four returned inline (no size-limit truncation), so no file-parse step was needed — each response's `count` field and `classifications` array length were both checked and agree in every case.

**Result:**

| Query | Tool-reported `count` | `len(classifications)` | Agree? |
|---|---|---|---|
| No filter (total) | 31 | 31 | Yes |
| `status="Open"` | 21 | 21 | Yes |
| `status="Resolved"` | 10 | 10 | Yes |
| `status="Superseded"` | 0 | 0 | Yes |

**Sum check:** 21 (Open) + 10 (Resolved) + 0 (Superseded) = **31** — matches the unfiltered total exactly.

**Independent second cross-check:** the 31 `classification_id`s returned by the unfiltered query were manually tallied by `status` field value directly from the returned JSON (not inferred), producing the identical split: 21 Open, 10 Resolved. The specific IDs in each filtered query's result set were compared against this manual tally — **identical ID sets in both methods**, for both Open and Resolved.

**Full ID lists (for independent reproducibility by a third party):**
- **Open (21):** `IC_20260708_004`, `IC_20260707_005`, `IC_20260707_004`, `IC_20260707_003`, `IC_20260707_002`, `IC_20260707_001`, `IC_20260705_021`, `IC_20260705_020`, `IC_20260705_018`, `IC_20260705_017`, `IC_20260705_015`, `IC_20260705_014`, `IC_20260705_013`, `IC_20260705_012`, `IC_20260705_011`, `IC_20260705_009`, `IC_20260705_008`, `IC_20260705_007`, `IC_20260705_006`, `IC_20260705_004`, `IC_20260705_003`
- **Resolved (10):** `IC_20260708_003`, `IC_20260708_002`, `IC_20260708_001`, `IC_20260707_006`, `IC_20260705_019`, `IC_20260705_016`, `IC_20260705_010`, `IC_20260705_005`, `IC_20260705_002`, `IC_20260705_001`

### Task 4 Classification — Integrity Ledger: **Not Verified** (on the Open/Resolved sub-count specifically) / **Verified** (on the total record count)

The total record count (31) matches every prior citation in this project exactly and is confirmed. **The "8 Open" figure, cited repeatedly throughout this project since v1.0, is incorrect. The correct figure, from a full, cross-validated recount, is 21 Open (and 10 Resolved, previously never stated at all).**

---

## Task 3 — Evidence detail (data source, commands, judgment basis)

Provided inline above, per query. Summary: all figures in this report are computed directly from live MCP tool responses queried on 2026-07-11 (session-local timestamps on the underlying tool-result files confirm this), using either direct Python parsing of a saved JSON dump (Decision Ledger, due to size) or direct inspection of inline tool responses cross-checked against a second independent filtered-query method (Integrity Ledger). No figure was taken from `appendix/INDEPENDENT_AUDIT_REPORT.md`, `appendix/CORRECTIVE_ACTION_REPORT.md`, `appendix/FINAL_VERIFICATION_REPORT.md`, or any earlier project file.

---

## Discrepancy Analysis — Integrity Ledger Open Count (8 vs. 21)

- **Magnitude:** the stated figure (8) understates the correct figure (21) by 13 records — a 62% undercount, not a rounding or off-by-one error.
- **Where the error originated:** the "8 Open" figure was first stated in `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` §4 (originally §1 in v1.0), during this project's initial Phase 1 evidence-gathering, at a point where the full 31-record Integrity Ledger had been retrieved inline in the conversation but was not systematically tallied by status — the "8" figure was almost certainly an unverified estimate rather than a count, though this project has no way to reconstruct the exact reasoning behind the original number.
- **Why three prior review passes (v1.0 authoring, Independent Audit, Corrective Action Phase) did not catch this:** the Independent Audit's methodology explicitly scoped ledger-total verification as a **sampling** exercise (9 individual records read in full, chosen because they were each cited elsewhere in the project for their content) rather than a full recount, and explicitly flagged this as a "Remaining Issue" for exactly this reason (`appendix/INDEPENDENT_AUDIT_REPORT.md` §4, item 1) — i.e., the audit correctly identified that it had not verified this figure, rather than incorrectly asserting that it had. The Corrective Action Phase inherited and re-stated the same open item rather than resolving it, since resolving it was explicitly out of that phase's stated scope (`appendix/CORRECTIVE_ACTION_REPORT.md`, item 1: "not attempted this phase"). This phase (Final Evidence Closure) is the first to have actually performed the full recount.
- **Impact scope:** the incorrect "8 Open" figure appears in `03_RUNTIME_GOVERNANCE_SPECIFICATION.md`, `appendix/CORRECTIVE_ACTION_REPORT.md`, and `appendix/FINAL_VERIFICATION_REPORT.md` (all corrected in this phase, see below). It does **not** appear in `01_EXECUTIVE_SUMMARY.md`, `10_REFERENCES.md`, `05_COMPARATIVE_ANALYSIS.md`, or `07_GAP_ANALYSIS.md`, which either omit the specific Open count or reference individual Integrity IDs by name rather than the aggregate figure. `appendix/INDEPENDENT_AUDIT_REPORT.md` is preserved unmodified per the no-rewrite principle — it correctly described the "31 records, 8 Open" figure as an *unverified inherited claim*, which remains an accurate description of that report's own methodology at the time it was written, even though the underlying "8" is now known to be wrong.
- **Does this change any substantive conclusion?** No architectural, comparative, or requirement-mapping conclusion in this project depends on the exact Open count. The qualitative point made throughout this project — that MoCKA's Integrity Classification Ledger is an actively used, non-trivial internal risk register with a meaningful population of unresolved findings — is, if anything, **more strongly supported** by the corrected figure (21 Open out of 31, i.e., roughly two-thirds still open) than by the original, understated one (8 of 31, roughly one-quarter). This is analogous to the `mocka-external-brain` and `m-sirius-k/m-sirius-k` findings from the Independent Audit: a factual correction that reinforces rather than undermines the project's existing narrative.

## Corrections Applied This Phase

| File | Location | Change |
|---|---|---|
| `03_RUNTIME_GOVERNANCE_SPECIFICATION.md` | §4 | "of which 8 remain Open" → corrected to 21, with a dated note |
| `appendix/CORRECTIVE_ACTION_REPORT.md` | Remaining Issues item 1 | Marked Closed this phase, corrected figure recorded |
| `appendix/FINAL_VERIFICATION_REPORT.md` | Part 2, item 1; Part 3 | Status changed from Open to Closed; verdict re-evaluated (see below) |
| `appendix/REVIEW_LOG.md` | New entry, this phase | Full summary appended |

`appendix/INDEPENDENT_AUDIT_REPORT.md` — **not modified**, per the explicit instruction to preserve the audit record; its Remaining Issues item describing this figure as unverified remains historically accurate as a description of that phase's own scope.
