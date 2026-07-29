# Reduction, formula semantics, and exhaustiveness status for link class 52

**Project:** Formal elimination of link class 52 in the `C(13,7,4)` covering-design search  
**Author:** Eric Dwares  
**Date:** 2026-07-28  
**Status:** Formula semantics and certificate layer audited; publication of the original case-enumeration generator remains necessary for a fully self-contained exhaustiveness audit.

## 1. Purpose of this document

This note explains the mathematical reduction behind the 30 pseudo-Boolean (PB) formulas in the class-52 certification bundle. It answers four separate questions:

1. Why a hypothetical 29-block `(13,7,4)` cover can be reduced to a 15-block `(12,6,3)` **link** plus 14 remaining blocks.
2. What the 792 Boolean variables and the constraint families in each published OPB file mean.
3. Why the published corpus contains 30 formulas rather than one formula.
4. Exactly which parts of the conclusion are formally certified and which parts still depend on generator provenance that should be published.

The final point matters. VeriPB proves that the published PB formulas are unsatisfiable. It does not, by itself, prove that the formula generator listed every combinatorial case. This document therefore states the strongest claim supported by the current public artifacts and identifies the remaining publication requirement without disguising it.

## 2. The original covering problem

A `(v,k,t)` covering design is a family of `k`-subsets, called blocks, of a `v`-point set such that every `t`-subset is contained in at least one block. The covering number `C(v,k,t)` is the minimum possible number of blocks.

The HorizonMath target asks for a `(13,7,4)` cover with fewer than the currently published 30 blocks. The public benchmark records the known interval

```text
28 <= C(13,7,4) <= 30.
```

A proof that no 29-block cover exists would establish `C(13,7,4)=30`. The class-52 project does **not** prove that global statement. It addresses one of 68 possible link types that a 29-block cover would have to contain.

## 3. Why every 29-block candidate has a degree-15 point

Assume, for contradiction, that `D` is a `(13,7,4)` cover with 29 blocks. For a point `p`, let `d(p)` be the number of blocks containing `p`.

Delete `p` from every block containing it. The resulting family consists of 6-subsets of the other 12 points and covers every 3-subset of those points. It is therefore a `(12,6,3)` cover. Gordon, Patashnik, Petro, and Taylor proved

```text
C(12,6,3) = 15.
```

Hence every point of `D` satisfies

```text
d(p) >= 15.
```

On the other hand, double-counting point-block incidences gives

```text
sum_p d(p) = 29 * 7 = 203.
```

If all 13 points had degree at least 16, that sum would be at least `13*16=208`, which is impossible. Therefore some point, denoted `infinity`, has degree exactly 15.

The 15 blocks containing `infinity`, with that point deleted, form a minimum `(12,6,3)` cover. This is the **link at infinity**.

## 4. Why there are 68 link classes

The 1995 classification proves that there are 68 nonisomorphic `(12,6,3)` covers with 15 blocks. The research code numbers these 68 isomorphism types from 1 through 68. “Class 52” is therefore a project-local index into that classification, not a universally standardized name in the literature.

For a hypothetical 29-block `(13,7,4)` cover:

- 15 blocks contain `infinity` and determine one of the 68 links;
- the remaining 14 blocks avoid `infinity` and are 7-subsets of the other 12 points.

Thus the global 29-block nonexistence problem can be divided into 68 link-extension problems. Eliminating class 52 removes one of those 68 possibilities; 67 remain.

## 5. The labeled class-52 link used by the formulas

The published OPBs use the 12-point set

```text
V = {0,1,...,11}.
```

A labeled 15-block representative decoded from the residual rows and link-degree data in the published formulas is:

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

The three points `0,4,8` have link degree 9; the other nine points have link degree 7.

Independent checks on this representative give:

- 15 blocks, each of size 6;
- every 3-subset of `V` is covered;
- triple multiplicity distribution: 159 triples occur once, 45 occur twice, 15 occur three times, and one occurs six times;
- pair multiplicity distribution: 45 pairs occur three times, 18 occur four times, and the three pairs among `{0,4,8}` occur six times;
- exactly 279 of the 495 four-subsets of `V` are not contained in a link block.

Those 279 uncovered four-subsets are the residual covering obligations encoded first in every OPB.

## 6. Extension variables

Let `E` be the 14 blocks of a hypothetical 29-block cover that do not contain `infinity`.

There are

```text
binom(12,7) = 792
```

possible 7-subsets of `V`. They are ordered lexicographically as produced by

```python
list(itertools.combinations(range(12), 7))
```

and the variable

```text
x_B in {0,1}
```

means that the 7-subset `B` is selected as one of the 14 extension blocks.

This accounts for the 792 Boolean variables in every formula.

## 7. The basic extension condition

Every 4-subset of the original 13-point set must be covered.

A 4-subset containing `infinity` has the form `{infinity} union T`, where `T` is a 3-subset of `V`. It is already covered because the link is a `(12,6,3)` cover.

For a 4-subset `Q` contained entirely in `V`:

- if `Q` lies in a link block `A`, then the corresponding original block `{infinity} union A` covers it;
- otherwise at least one extension block must contain `Q`.

Let `R(L)` denote the four-subsets not contained in any link block. For every `Q in R(L)`, the formula includes

```text
sum_{B superset Q} x_B >= 1.
```

For class 52, `|R(L)|=279`. Each such row contains 56 variables because a fixed 4-subset extends to a 7-subset by choosing three of the remaining eight points:

```text
binom(8,3) = 56.
```

These 279 rows are the core covering constraints.

## 8. Necessary degree consequences

The corrected model also includes valid lower bounds obtained by inducing smaller covers.

### 8.1 Point degrees

For `i in V`, let

```text
e_i = sum_{B contains i} x_B
```

be the extension degree of point `i`. The full degree is `ell_i + e_i`, which must be at least 15. Therefore

```text
e_i >= 15 - ell_i.
```

For class 52 the baseline extension lower bounds are

```text
(6,8,8,8,6,8,8,8,6,8,8,8).
```

The final formulas go further and fix an exact extension-degree profile, as explained below.

### 8.2 Pair degrees

For a pair `P`, the blocks containing `P`, with `P` deleted, form an `(11,5,2)` cover. The required minimum size is 7. If the link contains `P` in `lambda_L(P)` blocks, the extension must satisfy

```text
sum_{B superset P} x_B >= 7 - lambda_L(P).
```

All 66 pairs receive such a row. In the published class-52 formulas, the right-hand sides are distributed as:

```text
3 rows with RHS 1
18 rows with RHS 3
45 rows with RHS 4.
```

Each pair row contains `binom(10,5)=252` variables.

The native generator also emitted one companion upper row for every pair. In the 19 unsplit formulas these upper bounds are all at least 16, while exactly 14 blocks are selected, so they are redundant and do not change feasibility. They are retained because the certification audited the generator output rather than silently simplifying it.

### 8.3 Triple degrees

For a triple `T`, the blocks containing it, with `T` deleted, cover the ten remaining points by 4-subsets. At least

```text
C(10,4,1) = ceil(10/4) = 3
```

such blocks are required. Hence

```text
sum_{B superset T} x_B >= 3 - lambda_L(T)
```

whenever the right-hand side is positive.

For the labeled class-52 link this produces 204 rows:

```text
45 rows with RHS 1
159 rows with RHS 2.
```

The other 16 triples already occur at least three times in the link and need no extension lower-bound row. Each triple row contains `binom(9,4)=126` variables.

### 8.4 Exactly 14 extension blocks

The formulas include both sides of

```text
sum_B x_B = 14.
```

This is represented as two PB inequalities. It is exact because a 29-block design with a degree-15 distinguished point has precisely 14 blocks avoiding that point.

## 9. Why degree profiles are finite

The 29 blocks contain `29*7=203` point incidences. The distinguished point contributes 15, leaving 188 incidences across `V`.

If every point in `V` had full degree exactly 15, the total would be 180. Therefore the degree excesses

```text
r_i = (ell_i + e_i) - 15
```

are nonnegative integers satisfying

```text
sum_i r_i = 8.
```

Consequently at least four of the 12 points have zero excess. The exploratory reduction classified choices of four minimum-degree points under the automorphism group of the class-52 link; the retained research artifact records 26 orbits of 4-subsets. Further corrected screening reduced the surviving possibilities to the 20 exact degree profiles encoded in the final PB corpus.

## 10. The 20 profile cases and the 30 certified formulas

The final corpus represents 20 exact extension-degree profiles. Nineteen profiles are encoded by one formula each. One profile, `case21/profile014`, is divided into eleven exact pair-multiplicity branches, producing 30 formulas in total.

The exact extension-degree vectors recoverable from the published formulas are:

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

Every vector sums to 98, as required for 14 extension blocks of size 7. Adding the link-degree vector gives full degrees summing to 188 on `V`, or 203 after restoring the distinguished point.

The numeric `case` and `profile` labels are generator identifiers. This document does not assign them an additional mathematical interpretation that is not present in the surviving artifacts. The degree vectors, formula hashes, and formula contents—not the labels—are the auditable objects.

## 11. Why `case21/profile014` becomes eleven formulas

The unsplit profile `case21/profile014` was further partitioned by the exact extension multiplicity of a designated pair, called `pair12` in the generator metadata. Its baseline pair lower bound is 4, and no pair can occur in more than all 14 extension blocks. Therefore the possible integer values are exactly

```text
4,5,6,7,8,9,10,11,12,13,14.
```

The eleven formulas

```text
c52_case21_profile014_pair12_eq4.opb
...
c52_case21_profile014_pair12_eq14.opb
```

add one equality fixing that pair multiplicity to the indicated value. These branches are mutually exclusive and jointly exhaustive for the unsplit profile.

The high branches `eq9` through `eq14` have especially short contradictions: the support of a pair is a subset of the support of either endpoint, while the relevant endpoint degree is 8. Thus a pair multiplicity of at least 9 is impossible. The lower branches `eq4` through `eq8` require the larger certified arguments described in the technical report.

This split explains the final count:

```text
19 unsplit profile formulas
+ 11 pair-equality formulas replacing one profile
= 30 formulas.
```

## 12. Native OPB structure

A typical unsplit formula contains 641 constraints. The split formulas contain additional equality rows. The exact ordering is generator-defined, but the principal families can be recognized directly by support size and right-hand side:

| Family | Number in a typical unsplit formula | Variables per row | Meaning |
|---|---:|---:|---|
| Residual 4-set coverage | 279 | 56 | Every uncovered 4-set is covered by an extension block |
| Triple lower bounds | 204 | 126 | Full triple degree is at least 3 |
| Pair lower bounds | 66 | 252 | Full pair degree is at least 7 |
| Pair companion upper bounds | 66 | 252 | Redundant generator bounds retained verbatim |
| Exact point-profile rows | 24 | 462 | Twelve extension degrees fixed by lower and upper inequalities |
| Total block count | 2 | 792 | Exactly 14 extension blocks |

The count is

```text
279 + 204 + 66 + 66 + 24 + 2 = 641.
```

Each support size follows from elementary containment counting:

```text
4-set: binom(8,3) = 56
triple: binom(9,4) = 126
pair:   binom(10,5) = 252
point:  binom(11,6) = 462.
```

This regular structure gives an independent way to audit that the formulas have the intended combinatorial shape rather than being opaque solver inputs.

## 13. Corrected syntax conversion

The native formulas used both `>=` and `<=` rows. The supplied RoundingSat build rejected `<=` syntax, so the certification corpus applied only the algebraic identity

```text
sum_i a_i x_i <= b
```

if and only if

```text
sum_i (-a_i) x_i >= -b.
```

Across the 30 formulas:

- 19,252 constraints were preserved;
- 2,381 `<=` rows were sign-reversed;
- no variable was added, deleted, or renamed;
- no constraint was added or deleted;
- independent canonical row comparison matched every converted file to its source formula.

This was a syntax conversion, not a strengthening, relaxation, or modeling change.

## 14. How the proof strategy developed

The certification did not rely on one solver mode for all instances. The workflow evolved after the first large RoundingSat certificates showed that a single proof-generation strategy would be wasteful.

The final certificate inventory is:

- 20 exact LP split-tree/Farkas refutations;
- 6 direct containment cutting-planes proofs;
- 1 direct exact Farkas proof;
- 2 RoundingSat proofs transformed to replace strengthening axioms by explicit derivations;
- 1 conventional RoundingSat proof.

The guiding principle was fail-closed certification: a solver report of `UNSAT` was never counted by itself. An instance entered the ledger as `VERIFIED_UNSAT` only after the corresponding proof was accepted by VeriPB and the expected formula/proof hashes matched.

### 14.1 Conventional RoundingSat proof

The `eq4` branch produced a standard RoundingSat proof in PB proof format 1.0. The compatible legacy VeriPB checker accepted it with `--requireUnsat`.

### 14.2 Derived-row transformations

For `eq7` and `eq8`, implied partition and overlap constraints greatly accelerated search. Those constraints were not treated as new axioms in the final certification. Each added load was replaced by its cutting-planes derivation from the original formula, preserving the subsequent proof identifiers. VeriPB then checked the transformed proof against a formula canonically equivalent to the original OPB.

### 14.3 Exact Farkas certificates

When an LP relaxation was infeasible, exact rational/integer multipliers were reconstructed and audited for coefficient cancellation. The resulting cutting-planes derivation produces an explicit contradiction rather than trusting a floating-point optimizer status.

### 14.4 LP split-tree/Farkas certificates

For formulas whose root LP relaxation was feasible but whose 0-1 model was infeasible, a binary split tree was constructed. Each leaf was proved LP-infeasible by an exact Farkas certificate, yielding a valid branch clause. The leaf clauses were then resolved up the tree to the empty clause inside the PB proof system.

This method converted several solver runs that had timed out under ordinary proof logging into compact, independently checkable certificates.

## 15. What VeriPB certifies

For each formula `F_j`, the published certificate establishes

```text
F_j has no 0-1 satisfying assignment.
```

The final clean-room run independently established all of the following:

- the release ZIP matched its supplied SHA-256;
- all 425 archive members matched byte-for-byte after extraction/restoration;
- all 30 formula hashes matched;
- all compressed and uncompressed proof hashes matched;
- every VeriPB process used `--requireUnsat` and exited 0;
- every verifier stdout contained `Verification succeeded.`;
- all verifier stderr logs were empty;
- the three textually transformed formulas had the same 643 nontrivial constraints as their originals, plus only one tautological row.

Thus the unsatisfiability of the 30 published PB formulas is not merely a solver assertion. It is the strongest and most reproducible layer of the result.

## 16. The exhaustiveness implication

Let `P_1,...,P_20` denote the 20 exact degree-profile cases and let `P_*` be the profile split into the eleven pair-multiplicity branches.

The intended generator argument is:

1. Any 29-block `(13,7,4)` cover with class-52 link has an extension-degree excess vector summing to 8.
2. At least four points have minimum full degree 15.
3. Up to the automorphism group of the labeled class-52 link, the possible four-point minimum sets form 26 orbits.
4. Corrected combinatorial screening of those orbits leaves exactly the 20 profiles listed above.
5. Nineteen profiles are represented directly by one OPB each.
6. The remaining profile is exhaustively partitioned by pair multiplicity `4,...,14`.
7. Therefore every class-52 extension would satisfy at least one of the 30 formulas.
8. Since every one of those formulas is UNSAT, no class-52 extension exists.

Steps 5 through 8 are directly auditable from the published corpus. Steps 1 through 3 are mathematically reconstructable from the reduction and the preserved orbit artifact. Step 4—the exact screening from 26 orbits to the 20 retained profiles—is the principal provenance item that still needs to be published as executable source plus a deterministic output manifest.

## 17. Current claim status

It is useful to separate three levels of claim.

### Level A: fully formal and independently reproduced

> All 30 published class-52 PB formulas are UNSAT.

This is established by the VeriPB certificates and clean-room rerun.

### Level B: supported by the audited reduction and surviving research artifacts

> The 30 formulas are the intended corrected case split for the class-52 link extension problem.

The formula semantics, link representative, constraint families, degree profiles, pair split, conversion, and hashes are independently auditable. The project history also records an independent row-regeneration audit for all 30 formulas.

### Level C: fully self-contained elimination from first principles

> Every possible class-52 extension is represented by one of the 30 formulas.

This is the intended conclusion and is what the project means by “class 52 is eliminated.” For the public repository to make this implication independently reproducible without trusting prior project state, it should also publish the exact enumeration/screening generator described in the next section.

Accordingly, the most careful present wording is:

> The release formally refutes all 30 instances in the audited corrected class-52 reduction. Conditional only on the exhaustiveness of that published reduction, link class 52 is eliminated.

Once the original enumeration trail is published and independently rerun, the qualification can be removed.

## 18. Missing provenance artifacts to publish

A complete self-contained exhaustiveness package should add:

1. **The 68-link source and numbering map.** The exact list of 68 minimum `(12,6,3)` representatives, the source paper/data, and the deterministic statement that project index 52 corresponds to the 15 blocks in Section 5.
2. **Automorphism computation.** Code that computes the automorphism group of the class-52 link and the 26 orbits of four-subsets, together with canonical representatives and hashes.
3. **Profile generator.** Code that maps each orbit/case to exact extension-degree profiles and explains all pruning rules.
4. **Screening manifest.** A machine-readable record showing every generated profile, whether it was discarded or retained, and the exact mathematical reason for every discard.
5. **Formula emitter.** The corrected source that emits the native OPB rows from a profile, plus a deterministic comparison against the 30 published formulas.
6. **Pair-split metadata.** The coordinates of the designated `pair12`, its lower bound, and the derivation that `eq4` through `eq14` are the complete branch range.
7. **End-to-end command.** One command that starts with the link representative and regenerates the 30 original OPBs byte-for-byte or canonically row-for-row.

Publishing these items would close the only material audit gap between “30 certified UNSAT formulas” and a self-contained computational proof eliminating the entire link class.

## 19. Reproduction checklist for an external reviewer

An external audit can be divided into two independent tracks.

### Certificate track — currently complete

1. Verify the release ZIP SHA-256.
2. Extract the immutable bundle.
3. Run `python3 verify_all.py`.
4. Confirm `30/30`, `all_passed: true`, and successful VeriPB exits.
5. Inspect formula/proof hashes and equivalence logs.

### Reduction track — partially complete pending generator publication

1. Verify the 15-block link is a `(12,6,3)` cover.
2. Recompute its point, pair, triple, and residual-four-set multiplicities.
3. Recompute the 792-variable lexicographic indexing.
4. Regenerate the core coverage, point, pair, triple, and total rows.
5. Recompute the automorphism orbits and exact profile list.
6. Regenerate all 30 formulas and compare them canonically to the release.

The first four reduction checks can already be performed from the formula corpus and surviving scripts. The fifth and sixth require the original enumeration/profile-generation source to be added to the public archive.

## 20. Scope of the result

Even after the exhaustiveness trail is fully published, the conclusion is limited to one link class:

```text
No 29-block (13,7,4) cover can have the classified link type numbered 52.
```

It does not by itself prove:

```text
C(13,7,4) = 30.
```

That global conclusion would require eliminating the other 67 link classes or supplying a different global argument.

## References

1. Daniel M. Gordon, Oren Patashnik, John Petro, and Herbert Taylor, “Minimum `(12,6,3)` Covers,” *Ars Combinatoria* 40 (1995), 161–177. The paper proves `C(12,6,3)=15` and reports exactly 68 nonisomorphic minimum covers.
2. The class-52 certification bundle, release manifests, technical report, proof logs, and clean-room reproduction in this repository.
3. The surviving research scripts `mincover_overlap.py`, `mincover_minpoints.py`, and `mincover_minpoints_highexcess.py`, and the orbit artifact `class52_minpoint4_orbits.json`, retained in the project workspace and to be added to the public provenance package.

## Appendix A. Labeled link representative

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
