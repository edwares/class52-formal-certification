# Reduction, formula semantics, and certified case split for link class 52

**Project:** Formal elimination of link class 52 in the `C(13,7,4)` covering-design search  
**Author:** Eric Dwares  
**Date:** 2026-07-28  
**Status:** Documents the audited corrected reduction and the 30 formally verified pseudo-Boolean instances.

## 1. Purpose and scope

This note explains the mathematical reduction behind the 30 pseudo-Boolean (PB) formulas in the class-52 certification bundle. It records:

1. why a hypothetical 29-block `(13,7,4)` cover reduces to a 15-block `(12,6,3)` link plus 14 extension blocks;
2. what the 792 Boolean variables and each constraint family mean;
3. how symmetry and degree accounting reduce the class-52 extension problem to 20 exact degree profiles;
4. why one profile is partitioned into 11 pair-multiplicity branches, producing 30 final formulas;
5. what the VeriPB certificates establish.

The result is deliberately narrow. It eliminates one classified link type under the audited corrected reduction. It does not by itself establish `C(13,7,4)=30`, resolve the other 67 link classes, or establish novelty or priority.

## 2. The covering problem

A `(v,k,t)` covering design is a family of `k`-subsets, called blocks, of a `v`-point set such that every `t`-subset is contained in at least one block. The covering number `C(v,k,t)` is the minimum number of blocks in such a design.

The HorizonMath target is the open gap

```text
28 <= C(13,7,4) <= 30.
```

A proof that no 29-block cover exists would establish `C(13,7,4)=30`. The class-52 project addresses only one of the link types that a hypothetical 29-block cover would have to contain.

## 3. Reduction to a minimum `(12,6,3)` link

Assume that `D` is a `(13,7,4)` cover with 29 blocks. For a point `p`, let `d(p)` denote the number of blocks containing `p`.

Delete `p` from every block containing it. The resulting 6-subsets of the other 12 points cover every 3-subset, so they form a `(12,6,3)` cover. Gordon, Patashnik, Petro, and Taylor proved

```text
C(12,6,3) = 15.
```

Therefore every point satisfies

```text
d(p) >= 15.
```

Double-counting point-block incidences gives

```text
sum_p d(p) = 29 * 7 = 203.
```

If every point had degree at least 16, the sum would be at least `13*16=208`, a contradiction. Hence some point, denoted `infinity`, has degree exactly 15.

The 15 blocks containing `infinity`, with that point deleted, form a minimum `(12,6,3)` cover. This is the **link at infinity**.

The 1995 classification contains exactly 68 nonisomorphic minimum `(12,6,3)` covers. The project indexes them from 1 through 68. Thus:

- 15 blocks contain `infinity` and determine one of the 68 links;
- the remaining 14 blocks avoid `infinity` and are 7-subsets of the other 12 points.

Eliminating class 52 removes one of these 68 link-extension possibilities.

## 4. Labeled class-52 representative

The formulas use the point set

```text
V = {0,1,...,11}.
```

The labeled 15-block class-52 link is:

1. `{0,1,2,3,4,8}`
2. `{0,1,4,5,8,9}`
3. `{0,1,6,7,10,11}`
4. `{0,2,4,6,8,10}`
5. `{0,2,5,7,9,11}`
6. `{0,3,4,7,8,11}`
7. `{0,3,5,6,9,10}`
8. `{0,4,5,6,7,8}`
9. `{0,4,8,9,10,11}`
10. `{1,2,4,7,9,10}`
11. `{1,2,5,6,8,11}`
12. `{1,3,4,6,9,11}`
13. `{1,3,5,7,8,10}`
14. `{2,3,4,5,10,11}`
15. `{2,3,6,7,8,9}`

Its point-degree vector is

```text
ell = (9,7,7,7,9,7,7,7,9,7,7,7).
```

Independent checks give:

- 15 blocks, each of size 6;
- every 3-subset of `V` is covered;
- pair multiplicities: 45 pairs occur three times, 18 occur four times, and the three pairs among `{0,4,8}` occur six times;
- triple multiplicities: 159 triples occur once, 45 occur twice, 15 occur three times, and one occurs six times;
- 279 of the 495 four-subsets of `V` are not contained in a link block.

Those 279 uncovered four-subsets are the residual covering obligations for the 14 extension blocks.

## 5. Extension variables

There are

```text
binom(12,7) = 792
```

possible 7-subsets of `V`. They are ordered lexicographically as produced by

```python
list(itertools.combinations(range(12), 7))
```

For each 7-subset `B`, the Boolean variable

```text
x_B in {0,1}
```

means that `B` is selected as one of the 14 extension blocks.

## 6. Constraint families

### 6.1 Residual four-set coverage

For every four-subset `Q` not contained in any link block, at least one extension block must contain `Q`:

```text
sum_{B superset Q} x_B >= 1.
```

There are 279 such rows. Each row contains `binom(8,3)=56` variables.

### 6.2 Point degrees

For `i in V`, define the extension degree

```text
e_i = sum_{B contains i} x_B.
```

The full degree of `i` is `ell_i + e_i`, which must be at least 15. Thus

```text
e_i >= 15 - ell_i.
```

For class 52, the baseline extension lower bounds are

```text
(6,8,8,8,6,8,8,8,6,8,8,8).
```

The final formulas fix exact extension-degree profiles rather than only these lower bounds.

### 6.3 Pair degrees

For a pair `P`, the blocks containing `P`, with `P` deleted, form an `(11,5,2)` cover. Since `C(11,5,2)=7`, the extension must satisfy

```text
sum_{B superset P} x_B >= 7 - lambda_L(P),
```

where `lambda_L(P)` is the pair multiplicity in the link.

Across the 66 pair rows, the right-hand sides are:

```text
3 rows with RHS 1
18 rows with RHS 3
45 rows with RHS 4.
```

Each pair row contains `binom(10,5)=252` variables.

The native formulas also retain companion upper rows emitted by the corrected model generator. In the unsplit formulas these are redundant because their right-hand sides exceed the total of 14 selected blocks, but they were preserved verbatim for auditability.

### 6.4 Triple degrees

For a triple `T`, the blocks containing `T`, with `T` deleted, cover the ten remaining points by 4-subsets. Since

```text
C(10,4,1) = 3,
```

the extension must satisfy

```text
sum_{B superset T} x_B >= 3 - lambda_L(T)
```

whenever the right-hand side is positive.

For class 52 this gives 204 rows:

```text
45 rows with RHS 1
159 rows with RHS 2.
```

Each triple row contains `binom(9,4)=126` variables.

### 6.5 Exactly 14 extension blocks

The formulas impose

```text
sum_B x_B = 14,
```

represented by two PB inequalities.

## 7. Finite degree-profile reduction

The 29 blocks contain `29*7=203` point incidences. The distinguished point contributes 15, leaving 188 incidences across `V`.

If every point of `V` had full degree exactly 15, the total would be 180. Define the nonnegative degree excesses

```text
r_i = (ell_i + e_i) - 15.
```

They satisfy

```text
sum_i r_i = 8.
```

Therefore at least four of the 12 points have zero excess. The class-52 automorphism computation used in the project has order 36 and reduces the 495 choices of four minimum-degree points to 26 orbits. Exact profile enumeration and the corrected screening rules reduce those orbit cases to the 20 extension-degree profiles listed below.

A standalone public script that regenerates the orbit/profile enumeration would be a useful future end-to-end reproducibility enhancement. The final 20 vectors and their 30 emitted formulas are fixed by the published corpus and manifests.

## 8. The 20 exact extension-degree profiles

| Formula family | Extension-degree vector `(e_0,...,e_11)` |
|---|---|
| `case19/profile002` | `(7,8,8,9,7,8,8,9,9,8,9,8)` |
| `case19/profile007` | `(7,8,8,9,8,8,8,9,8,8,9,8)` |
| `case19/profile011` | `(7,8,8,10,8,8,8,9,7,8,9,8)` |
| `case21/profile011` | `(7,8,8,8,9,8,8,8,8,8,9,9)` |
| `case21/profile014` | `(8,8,8,8,8,8,8,8,8,8,9,9)` |
| `case21/profile015` | `(8,8,8,8,9,8,8,8,7,8,9,9)` |
| `case22/profile012` | `(8,8,8,8,7,8,8,9,9,8,8,9)` |
| `case22/profile014` | `(8,8,8,8,7,8,8,10,8,8,8,9)` |
| `case22/profile015` | `(8,8,8,8,8,8,8,9,8,8,8,9)` |
| `case22/profile017` | `(9,8,8,8,7,8,8,9,8,8,8,9)` |
| `case23/profile008` | `(7,8,8,8,8,8,8,9,8,8,10,8)` |
| `case23/profile009` | `(7,8,8,8,8,8,8,9,9,8,9,8)` |
| `case23/profile011` | `(8,8,8,8,7,8,8,9,8,8,10,8)` |
| `case23/profile012` | `(8,8,8,8,7,8,8,9,9,8,9,8)` |
| `case23/profile014` | `(8,8,8,8,7,8,8,10,8,8,9,8)` |
| `case23/profile015` | `(8,8,8,8,8,8,8,9,8,8,9,8)` |
| `case23/profile017` | `(9,8,8,8,7,8,8,9,8,8,9,8)` |
| `case24/profile011` | `(7,8,8,8,9,8,8,8,9,8,8,9)` |
| `case24/profile016` | `(8,8,8,8,8,8,8,8,8,8,8,10)` |
| `case24/profile017` | `(8,8,8,8,8,8,8,8,9,8,8,9)` |

Every vector sums to 98, as required for 14 extension blocks of size 7.

## 9. Why 20 profiles become 30 formulas

Nineteen profiles are represented by one PB formula each. The remaining profile,

```text
case21/profile014,
```

is partitioned by the extension multiplicity of the pair `{1,2}`.

Its base pair constraint requires

```text
sum_{B superset {1,2}} x_B >= 4.
```

Because exactly 14 extension blocks are selected, the possible integer values are

```text
4,5,6,7,8,9,10,11,12,13,14.
```

The profile is therefore replaced by 11 mutually exclusive and jointly exhaustive branches, each adding

```text
sum_{B superset {1,2}} x_B = k
```

for one of those values. Hence

```text
19 unsplit profile formulas
+ 11 pair-multiplicity branches
= 30 formulas.
```

A typical unsplit formula contains 641 constraints:

| Constraint family | Rows |
|---|---:|
| Residual four-set coverage | 279 |
| Triple lower bounds | 204 |
| Pair lower and companion upper rows | 132 |
| Exact point-profile rows | 24 |
| Exact total block count | 2 |
| **Total** | **641** |

Each split formula adds two rows for the pair equality and therefore contains 643 constraints. The complete corpus has

```text
19*641 + 11*643 = 19,252 constraints.
```

## 10. Model-correction note

An earlier exploratory model used an incorrect pair-degree upper bound that double-counted the link contribution. That preliminary result was discarded. The bound was corrected, all affected profiles were regenerated, and the certification in this repository applies exclusively to the corrected formulas.

No result from the discarded model is used as evidence in the final certification.

## 11. OPB syntax conversion

The native formulas used both `>=` and `<=` rows. The supplied RoundingSat build rejected `<=`, so the certification corpus applied only the exact algebraic conversion

```text
sum_i a_i x_i <= b
```

into

```text
sum_i (-a_i) x_i >= -b.
```

Across all 30 formulas:

- 19,252 constraints were preserved;
- 2,381 `<=` rows were sign-reversed;
- no variable was added, deleted, or renamed;
- no mathematical constraint was added or deleted;
- independent canonical row comparison matched every converted file to its source formula.

This was a syntax conversion, not a strengthening, relaxation, or modeling change.

## 12. Formal certificates

All 30 formulas have VeriPB-accepted UNSAT certificates. Every final verification used `--requireUnsat`.

The certificate inventory is:

- 20 exact LP split-tree/Farkas refutations;
- 6 direct containment cutting-planes proofs;
- 1 direct exact Farkas proof;
- 2 transformed RoundingSat proofs with formally derived strengthening rows;
- 1 conventional RoundingSat proof.

The final audit reports:

```text
30 VERIFIED_UNSAT
0 SAT
0 timeout
0 error
236,083 VeriPB proof rules checked
```

The clean-room reproduction independently:

- matched the release ZIP SHA-256;
- matched all 425 archive members byte-for-byte;
- recomputed formula and proof hashes;
- checked formula equivalence;
- ran VeriPB with `--requireUnsat` on all 30 certificates;
- obtained 30 successful verifier exits with empty stderr logs.

The immutable certification ZIP has SHA-256

```text
c4c1ddc812affd9bd05c452855bdfcd614a68906f8bf536fab8bcd4b3123ae56
```

## 13. Certified conclusion

For each of the 30 formulas `F_j`, the published certificate establishes

```text
F_j has no 0-1 satisfying assignment.
```

The formulas encode the audited corrected class-52 case split described above. Therefore the result certified by this release is:

> Link class 52 is eliminated under the audited corrected pseudo-Boolean reduction.

This is stronger than an ordinary solver-level `UNSAT` report: every formula has a machine-checkable contradiction, and the complete verification has been independently reproduced in a fresh environment.

## 14. Reproduction checklist

### Certificate verification

1. Verify the release ZIP SHA-256.
2. Extract the immutable bundle.
3. Run `python3 verify_all.py`.
4. Confirm `30/30`, `all_passed: true`, and successful VeriPB exits.
5. Inspect formula/proof hashes and equivalence logs.

### Reduction audit

1. Verify that the 15-block link is a `(12,6,3)` cover.
2. Recompute its point, pair, triple, and residual-four-set multiplicities.
3. Recompute the 792-variable lexicographic indexing.
4. Regenerate the coverage, point, pair, triple, profile, and total-block rows.
5. Compare the regenerated rows canonically with the 30 published formulas.

A future standalone case-enumeration script could additionally regenerate the order-36 automorphism group, 26 four-subset orbits, and 20 retained profiles from the labeled link in one command.

## 15. Scope of the result

The conclusion is limited to one link class:

```text
No 29-block (13,7,4) cover can realize the classified link type numbered 52 under the audited corrected reduction.
```

It does not by itself prove

```text
C(13,7,4) = 30.
```

That global conclusion would require eliminating the other 67 link classes or supplying a different global argument.

## References

1. Daniel M. Gordon, Oren Patashnik, John Petro, and Herbert Taylor, “Minimum `(12,6,3)` Covers,” *Ars Combinatoria* 40 (1995), 161–177.
2. The class-52 certification bundle, release manifests, technical report, proof logs, and clean-room reproduction in this repository.

## Appendix A. Compact link representation

```text
012348
014589
0167AB
02468A
02579B
03478B
03569A
045678
0489AB
12479A
12568B
13469B
13578A
2345AB
236789
```

Here `A=10` and `B=11`.

## Appendix B. Exact formula inventory

```text
c52_case19_profile002.opb
c52_case19_profile007.opb
c52_case19_profile011.opb
c52_case21_profile011.opb
c52_case21_profile014_pair12_eq4.opb
c52_case21_profile014_pair12_eq5.opb
c52_case21_profile014_pair12_eq6.opb
c52_case21_profile014_pair12_eq7.opb
c52_case21_profile014_pair12_eq8.opb
c52_case21_profile014_pair12_eq9.opb
c52_case21_profile014_pair12_eq10.opb
c52_case21_profile014_pair12_eq11.opb
c52_case21_profile014_pair12_eq12.opb
c52_case21_profile014_pair12_eq13.opb
c52_case21_profile014_pair12_eq14.opb
c52_case21_profile015.opb
c52_case22_profile012.opb
c52_case22_profile014.opb
c52_case22_profile015.opb
c52_case22_profile017.opb
c52_case23_profile008.opb
c52_case23_profile009.opb
c52_case23_profile011.opb
c52_case23_profile012.opb
c52_case23_profile014.opb
c52_case23_profile015.opb
c52_case23_profile017.opb
c52_case24_profile011.opb
c52_case24_profile016.opb
c52_case24_profile017.opb
```
