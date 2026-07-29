# C(13,7,4) class-52 formal certification — complete

Date: 2026-07-28

## Bottom line

All **30 required class-52 PB instances** have independently verified UNSAT certificates. Under the corrected PB corpus and its audited class-52 reduction, **link class 52 is formally eliminated**.

This does **not** establish `C(13,7,4)=30`, does not establish novelty, and does not address the 67 other link classes.

## Final audit

- Master ledger: 30 `VERIFIED_UNSAT`, zero SAT, zero timeout, zero error.
- Independent final rerun: 30/30 VeriPB checks exited 0 and printed `Verification succeeded.`
- Every verifier run used `--requireUnsat`.
- Every non-identical RoundingSat formula was independently canonicalized against its original OPB; all equivalence checks passed.
- Formula and proof hashes were recomputed and matched the ledger.
- Stored certificate bytes audited: 381,424,587.
- Total VeriPB proof rules rechecked: 236,083.

## Certificate methods

- Direct containment cutting-planes proof: 6 instances
- Exact Farkas cutting-planes proof: 1 instance
- Exact LP split-tree/Farkas refutation: 20 instances
- RoundingSat + derived-row proof transformation: 2 instances
- RoundingSat proof: 1 instance

## Per-instance verification

| Instance | Method | Stored proof | Rules | VeriPB time |
|---|---:|---:|---:|---:|
| `c52_case19_profile002.opb` | Exact LP split-tree/Farkas refutation | 238,942 B | 16 | 0.77 s |
| `c52_case19_profile007.opb` | Exact LP split-tree/Farkas refutation | 1,486,819 B | 88 | 1.17 s |
| `c52_case19_profile011.opb` | Exact LP split-tree/Farkas refutation | 68,853 B | 6 | 0.67 s |
| `c52_case21_profile011.opb` | Exact LP split-tree/Farkas refutation | 776,217 B | 46 | 0.97 s |
| `c52_case21_profile014_pair12_eq10.opb` | Direct containment cutting-planes proof | 57 B | 4 | 0.72 s |
| `c52_case21_profile014_pair12_eq11.opb` | Direct containment cutting-planes proof | 57 B | 4 | 0.67 s |
| `c52_case21_profile014_pair12_eq12.opb` | Direct containment cutting-planes proof | 57 B | 4 | 0.67 s |
| `c52_case21_profile014_pair12_eq13.opb` | Direct containment cutting-planes proof | 57 B | 4 | 0.67 s |
| `c52_case21_profile014_pair12_eq14.opb` | Direct containment cutting-planes proof | 57 B | 4 | 0.67 s |
| `c52_case21_profile014_pair12_eq4.opb` | RoundingSat proof | 128,093,567 B | 30,711 | 132.51 s |
| `c52_case21_profile014_pair12_eq5.opb` | Exact LP split-tree/Farkas refutation | 1,612,300 B | 100 | 1.22 s |
| `c52_case21_profile014_pair12_eq6.opb` | Exact Farkas cutting-planes proof | 35,439 B | 10 | 0.67 s |
| `c52_case21_profile014_pair12_eq7.opb` | RoundingSat + derived-row proof transformation | 202,200,876 B | 81,388 | 748.03 s |
| `c52_case21_profile014_pair12_eq8.opb` | RoundingSat + derived-row proof transformation | 24,840,307 B | 122,403 | 137.96 s |
| `c52_case21_profile014_pair12_eq9.opb` | Direct containment cutting-planes proof | 57 B | 4 | 0.67 s |
| `c52_case21_profile015.opb` | Exact LP split-tree/Farkas refutation | 958,331 B | 54 | 0.97 s |
| `c52_case22_profile012.opb` | Exact LP split-tree/Farkas refutation | 955,661 B | 56 | 1.02 s |
| `c52_case22_profile014.opb` | Exact LP split-tree/Farkas refutation | 344,776 B | 22 | 0.82 s |
| `c52_case22_profile015.opb` | Exact LP split-tree/Farkas refutation | 6,416,199 B | 371 | 2.93 s |
| `c52_case22_profile017.opb` | Exact LP split-tree/Farkas refutation | 744,349 B | 44 | 0.92 s |
| `c52_case23_profile008.opb` | Exact LP split-tree/Farkas refutation | 270,075 B | 18 | 0.72 s |
| `c52_case23_profile009.opb` | Exact LP split-tree/Farkas refutation | 743,419 B | 44 | 0.97 s |
| `c52_case23_profile011.opb` | Exact LP split-tree/Farkas refutation | 265,846 B | 18 | 0.87 s |
| `c52_case23_profile012.opb` | Exact LP split-tree/Farkas refutation | 710,754 B | 42 | 0.92 s |
| `c52_case23_profile014.opb` | Exact LP split-tree/Farkas refutation | 272,261 B | 18 | 0.82 s |
| `c52_case23_profile015.opb` | Exact LP split-tree/Farkas refutation | 4,857,285 B | 282 | 2.42 s |
| `c52_case23_profile017.opb` | Exact LP split-tree/Farkas refutation | 731,839 B | 42 | 0.87 s |
| `c52_case24_profile011.opb` | Exact LP split-tree/Farkas refutation | 358,653 B | 22 | 0.77 s |
| `c52_case24_profile016.opb` | Exact LP split-tree/Farkas refutation | 988,162 B | 62 | 1.02 s |
| `c52_case24_profile017.opb` | Exact LP split-tree/Farkas refutation | 3,453,315 B | 196 | 1.87 s |

## Validated corpus

- 30 converted OPB instances.
- 792 variables per instance.
- 19,252 constraints across the corpus.
- 2,381 original `<=` rows converted only by coefficient/RHS sign reversal.
- No variables or constraints added or deleted by syntax conversion.
- Converted-file hashes match the conversion manifest.

## Reproducibility artifacts

- `master_class52_status.json`: authoritative 30-instance ledger.
- `final_audit/class52_final_audit.json`: independent final verification and hash manifest.
- `final_audit/logs/`: per-instance VeriPB stdout/stderr from the final rerun.
- `instances_roundingsat/`: the 30 audited converted OPB formulas.
- `remaining_split_trees/`, `direct_proofs/`, `results_direct_containment/`, `results_transformed_eq7/`, `results_transformed_eq8/`, and `smoke/`: certificate sources.

## Scope guardrails

- The claim is limited to formal elimination of link class 52 under the audited corrected reduction.
- Sixty-seven other link classes remain outside this certification.
- No global covering-number conclusion follows from this result alone.
- No priority or novelty claim is made.
