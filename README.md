# Formal elimination of link class 52 in the C(13,7,4) search

This repository records a formally checked elimination of **link class 52** under the audited corrected pseudo-Boolean reduction used in the HorizonMath `C(13,7,4)` covering-design search.

## Result

All **30 required class-52 instances** have independently verified UNSAT certificates.

- 30/30 VeriPB checks passed.
- Every verifier run used `--requireUnsat`.
- Formula and proof hashes matched the certification manifest.
- A fresh-environment clean-room reproduction also passed 30/30.
- Total proof rules checked: 236,083.

The clean-room reproduction report is in [`reproduction/cleanroom-verification-report.md`](reproduction/cleanroom-verification-report.md).

## Scope

The result is deliberately narrow:

> Link class 52 is formally eliminated under the audited corrected class-52 PB reduction.

It does **not** establish `C(13,7,4)=30`, resolve the other 67 link classes, or by itself establish novelty or priority.

## Immutable certification artifact

The complete formulas, certificates, verifier build, logs, and one-command verification workflow are distributed as the GitHub Release asset:

`Class52_formal_certification_complete.zip`

Expected SHA-256:

```text
c4c1ddc812affd9bd05c452855bdfcd614a68906f8bf536fab8bcd4b3123ae56
```

The checksum file is committed at [`release/Class52_formal_certification_complete.zip.sha256`](release/Class52_formal_certification_complete.zip.sha256).

## Reproduce the verification

Download the release ZIP and checksum, then run:

```bash
sha256sum -c Class52_formal_certification_complete.zip.sha256
unzip Class52_formal_certification_complete.zip
cd Class52_formal_certification_complete
python3 verify_all.py
```

A successful run ends with:

```json
{
  "passed": 30,
  "completed": 30,
  "expected": 30,
  "all_passed": true
}
```

The bundled verifier targets Linux x86-64 and CPython 3.13. The complete verification includes the large `eq4`, `eq7`, and `eq8` certificates and can take roughly 18 minutes on a typical two-core environment.

## Certificate methods

- 20 exact LP split-tree/Farkas refutations
- 6 direct containment cutting-planes proofs
- 1 direct exact Farkas proof
- 2 transformed RoundingSat proofs with formally derived strengthening rows
- 1 conventional RoundingSat proof

See [`docs/technical-report.md`](docs/technical-report.md) for the per-instance breakdown.

## Repository layout

- `docs/` — technical certification report
- `manifests/` — hashes, statuses, conversion audit, and final audit
- `reproduction/` — clean-room report, generated results, logs, and audit bundle
- `scripts/` — verification and proof-generation source
- `release/` — checksum for the immutable release artifact

## Citation

Citation metadata is provided in [`CITATION.cff`](CITATION.cff). Until a DOI is assigned, cite the tagged GitHub release and its SHA-256.

## Third-party software

The immutable release bundle includes a compatible legacy VeriPB build and RoundingSat binary for reproducibility. Those components remain under their respective upstream licenses. See [`NOTICE.md`](NOTICE.md).
