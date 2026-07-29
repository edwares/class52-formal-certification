# Class 52 clean-room verification report

## Result

**PASS — 30/30 required instances independently verified in this fresh environment.**

Under the scope encoded by this bundle and its corrected PB reduction, this clean-room run reproduces the formal elimination of link class 52. This does not establish `C(13,7,4)=30`, novelty, or anything about the other 67 link classes.

## Archive integrity

- Computed ZIP SHA-256: `c4c1ddc812affd9bd05c452855bdfcd614a68906f8bf536fab8bcd4b3123ae56`
- Supplied checksum: `c4c1ddc812affd9bd05c452855bdfcd614a68906f8bf536fab8bcd4b3123ae56`
- Checksum match: yes
- Fresh extraction comparison: 425/425 archive members matched byte-for-byte
- Post-restoration comparison: 425/425 archive members matched byte-for-byte

## Verification workflow

- Bundled command: `python3 verify_all.py`
- VeriPB option: `--requireUnsat` on every certificate
- Workflow exit code: 0
- Passed/completed/expected: 30/30/30
- `all_passed`: `true`
- VeriPB proof rules checked: 236,083
- Sum of per-instance verification times: 1076.021 seconds
- Verification logs: 30 stdout + 30 stderr
- All stderr logs were empty
- Every stdout log contained `Verification succeeded.`

## Independent audits

- Original/formula/compressed-proof/uncompressed-proof hash audit: 30/30 passed
- Formula equivalence audit: 30/30 passed
- Three verifier formulas differed textually from their originals (`eq4`, `eq7`, `eq8`). Independent affine normalization found 643/643 nontrivial constraints equal in the same order and multiset for each; the verifier formula added only one tautological `>= 0` row.
- Independent log/result audit: 30/30 passed

## Runtime compatibility and anomalies

- Environment: Linux x86-64; Python 3.13.5; bundled VeriPB CPython 3.13 extensions imported successfully.
- No missing dependency, verifier incompatibility, timeout, hash mismatch, nonzero VeriPB exit, or certificate failure occurred.
- Python regenerated 10 bundled `.pyc` cache files during imports because the extraction path differed. This was recorded in `extraction_integrity_postrun_before_restore.json`; no formula, proof, manifest, verifier source, or compiled extension changed. The 10 caches were restored byte-for-byte from the ZIP, after which all 425 archive members matched.

## Per-instance results

| Instance | Result | VeriPB exit | Rules | Seconds |
|---|---:|---:|---:|---:|
| `c52_case19_profile002.opb` | PASS | 0 | 16 | 0.887 |
| `c52_case19_profile007.opb` | PASS | 0 | 88 | 1.417 |
| `c52_case19_profile011.opb` | PASS | 0 | 6 | 0.639 |
| `c52_case21_profile011.opb` | PASS | 0 | 46 | 0.884 |
| `c52_case21_profile014_pair12_eq10.opb` | PASS | 0 | 4 | 0.635 |
| `c52_case21_profile014_pair12_eq11.opb` | PASS | 0 | 4 | 0.598 |
| `c52_case21_profile014_pair12_eq12.opb` | PASS | 0 | 4 | 0.576 |
| `c52_case21_profile014_pair12_eq13.opb` | PASS | 0 | 4 | 0.624 |
| `c52_case21_profile014_pair12_eq14.opb` | PASS | 0 | 4 | 0.699 |
| `c52_case21_profile014_pair12_eq4.opb` | PASS | 0 | 30,711 | 142.513 |
| `c52_case21_profile014_pair12_eq5.opb` | PASS | 0 | 100 | 1.190 |
| `c52_case21_profile014_pair12_eq6.opb` | PASS | 0 | 10 | 0.660 |
| `c52_case21_profile014_pair12_eq7.opb` | PASS | 0 | 81,388 | 763.430 |
| `c52_case21_profile014_pair12_eq8.opb` | PASS | 0 | 122,403 | 143.446 |
| `c52_case21_profile014_pair12_eq9.opb` | PASS | 0 | 4 | 0.608 |
| `c52_case21_profile015.opb` | PASS | 0 | 54 | 0.926 |
| `c52_case22_profile012.opb` | PASS | 0 | 56 | 0.975 |
| `c52_case22_profile014.opb` | PASS | 0 | 22 | 0.752 |
| `c52_case22_profile015.opb` | PASS | 0 | 371 | 2.901 |
| `c52_case22_profile017.opb` | PASS | 0 | 44 | 0.846 |
| `c52_case23_profile008.opb` | PASS | 0 | 18 | 0.725 |
| `c52_case23_profile009.opb` | PASS | 0 | 44 | 0.858 |
| `c52_case23_profile011.opb` | PASS | 0 | 18 | 0.753 |
| `c52_case23_profile012.opb` | PASS | 0 | 42 | 0.878 |
| `c52_case23_profile014.opb` | PASS | 0 | 18 | 0.720 |
| `c52_case23_profile015.opb` | PASS | 0 | 282 | 2.341 |
| `c52_case23_profile017.opb` | PASS | 0 | 42 | 0.896 |
| `c52_case24_profile011.opb` | PASS | 0 | 22 | 0.714 |
| `c52_case24_profile016.opb` | PASS | 0 | 62 | 0.999 |
| `c52_case24_profile017.opb` | PASS | 0 | 196 | 1.930 |

## Returned artifacts

- `verification_results.json`: exact generated workflow result file.
- `verification_logs/`: all per-instance VeriPB stdout/stderr logs.
- `independent_hash_audit.json`: independent hash and size recomputation.
- `independent_formula_equivalence_audit.json`: independent normalization/equivalence check.
- `independent_verification_audit.json`: cross-check of return codes, success markers, logs, and hashes.
- Extraction-integrity and runtime-cache audit records.
- `cleanroom_workflow_console.log`: complete workflow console output.
