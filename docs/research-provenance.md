# Research provenance: origin and development of the class-52 program

**Project:** Formal elimination of link class 52 in the `C(13,7,4)` covering-design search  
**Author:** Eric Dwares  
**Date of reconstruction:** 2026-07-29  

## Purpose

This document records how the class-52 research program developed across multiple ChatGPT research sessions. It distinguishes the initial reduction and model-development work from the later proof-generation, formal-certification, clean-room reproduction, and publication phases.

It is a provenance record, not a substitute for the mathematical reduction or the machine-checkable certificates.

## 1. Initial objective

The project began with the broader question of whether a 29-block `(13,7,4)` covering design could exist, with the long-term goal of determining whether

```text
C(13,7,4) = 30.
```

At the outset there was no class-52 elimination, no pseudo-Boolean proof corpus, and no formal certification pipeline.

## 2. Baseline reproduction

The first phase reproduced the known 30-block construction and checked the existing HorizonMath verification workflow.

No novelty or priority claim was made. The purpose was to establish a correct computational baseline before attempting new work.

## 3. Direct constructive search

The project next attempted to construct a 29-block cover directly. Explored methods included:

- exact mixed-integer linear programming;
- local search;
- neighborhood repair;
- replacement searches.

The closest constructions remained incomplete. This suggested that continued direct constructive search would be inefficient and motivated a change of strategy.

## 4. Development of the link-class reduction

The initial research chat developed the reduction that became the foundation of the later project:

1. every point in a hypothetical 29-block `(13,7,4)` cover has degree at least 15 because its link is a `(12,6,3)` cover;
2. total incidence counting forces at least one point to have degree exactly 15;
3. deleting that point from its 15 incident blocks produces a minimum `(12,6,3)` cover;
4. the Gordon–Patashnik–Petro–Taylor classification gives exactly 68 nonisomorphic minimum links;
5. therefore the global problem decomposes into 68 link-extension problems.

This reduction did not eliminate any class by itself. It converted one large problem into a finite family of structured subproblems.

## 5. Why class 52 was selected

Class 52 was selected as a prototype, not because of a theorem asserting that it was uniquely difficult or mathematically privileged.

The intended purpose was to:

- build the link-extension machinery;
- test stronger reductions;
- debug the computational model;
- develop a proof pipeline that could later be applied to other link classes.

Accordingly, the successful class-52 certification remains a one-class result. The other 67 link classes are outside its scope.

## 6. Degree-profile and symmetry reduction

Within class 52, the project developed increasingly strong finite reductions based on:

- point-degree accounting;
- total incidence constraints;
- link automorphisms;
- orbit representatives;
- exact extension-degree profiles;
- pair and triple multiplicity bounds.

The retained project history records the following case structure:

- the automorphism group of the labeled class-52 link has order 36;
- the 495 four-subsets of the 12-point set reduce to 26 automorphism orbits;
- exact profile generation produced 107 symmetry-reduced degree profiles;
- the screening history records a `70 / 17 / 20` partition;
- the 20 affected profiles were recomputed after the model correction;
- 19 became individual corrected profile formulas;
- one difficult profile was split into 11 exact pair-multiplicity branches;
- the final corrected corpus therefore contains `19 + 11 = 30` PB formulas.

The published certification proves all 30 formulas UNSAT. For a fully self-contained end-to-end audit, the executable source that regenerates the 26-orbit and 107-profile enumeration should also be published with a deterministic manifest.

## 7. Discovery and withdrawal of an incorrect model

A central event in the initial research chat was the discovery that an earlier pair-degree upper-bound inequality was wrong.

The derivation had double-counted the contribution of the link pair degree. Once this was recognized:

- the earlier computational elimination claim was explicitly withdrawn;
- the inequality was re-derived correctly;
- every affected profile was regenerated and rerun;
- no proof or status from the incorrect model was carried forward as evidence for the corrected claim.

This correction is part of the provenance of the final result and should not be erased from later documentation. The formal certification applies only to the corrected PB corpus.

## 8. Corrected solver-level elimination

After the inequality was corrected, the affected profile cases were rerun. The difficult remaining profile was partitioned by exact pair multiplicity, producing the final 30 corrected instances.

At this stage the project had solver-level UNSAT results, but it did not treat solver output alone as a formal mathematical proof.

That distinction motivated the transition to proof-producing pseudo-Boolean tooling.

## 9. Development of the PB certification framework

The initial chat developed or planned the infrastructure for:

- native OPB generation;
- portable model generation;
- portable CNF generation;
- package validation;
- syntax normalization;
- RoundingSat proof logging;
- independent VeriPB checking.

The intended standard was fail-closed: an instance would not count as eliminated merely because a solver reported `UNSAT`.

## 10. RoundingSat compatibility work

The supplied RoundingSat build exposed two syntax incompatibilities:

- explicit leading `+` coefficients were rejected;
- `<=` rows were rejected, with a misleading parser message referring to non-linear constraints.

The project therefore applied only the algebraically exact conversion

```text
a <= b
```

into

```text
-a >= -b.
```

No variables or mathematical constraints were added or removed by this syntax conversion.

## 11. What did not complete in the initial chat

The first research chat did not complete the full VeriPB campaign. The environment failed at the infrastructure stage before all proof logs could be generated and independently checked.

The initial chat should therefore be credited with:

- the baseline reproduction;
- the link-class reduction;
- selection of class 52 as a prototype;
- symmetry and degree-profile methodology;
- discovery and correction of the pair-degree modeling error;
- corrected solver-level case split;
- design and preparation of the PB certification framework.

It should not be represented as the session in which all 30 certificates were completed.

## 12. Later continuation and formal certification

Later research sessions continued the program and completed the certification layer. Those later stages produced:

- proof certificates for all 30 corrected PB instances;
- successful VeriPB verification using `--requireUnsat` on every instance;
- formula and proof hash manifests;
- independent formula-equivalence audits;
- a fresh-environment clean-room reproduction passing 30/30;
- publication-oriented reports, repository structure, and immutable release artifacts.

These are continuations of the research program begun in the initial chat, not retroactive accomplishments of that first session.

## 13. Provenance phases

For citation and historical accuracy, the project should be described in three phases:

### Phase I — Initial reduction and methodology development

- baseline verification;
- direct-search attempts;
- link-class decomposition;
- class-52 prototype selection;
- degree-profile and symmetry reduction;
- discovery and correction of the model error;
- corrected solver-level rerun;
- PB framework design.

### Phase II — Proof generation and certification

- generation or construction of proof certificates;
- compatibility work for the legacy verifier stack;
- exact Farkas and split-tree certificate development;
- VeriPB checking of all 30 instances;
- final hash and status audits.

### Phase III — Independent reproduction and publication

- clean-room verification;
- archive-integrity checking;
- public GitHub release;
- technical documentation;
- DOI and archival preparation.

## 14. Scope and claim discipline

The historical development does not change the scope of the certified result:

> The 30 corrected PB instances associated with the audited class-52 reduction have independently verified UNSAT certificates.

The intended combinatorial consequence is that link class 52 is eliminated under that corrected reduction.

The result does not by itself establish `C(13,7,4)=30`, resolve the other 67 link classes, or establish novelty or priority.

## 15. Remaining provenance publication task

The reasoning and numerical audit trail for the orbit/profile reduction survive in the research history. The principal remaining provenance task is to publish or reconstruct the executable source and deterministic outputs that regenerate:

1. the order-36 automorphism group;
2. the 26 four-subset orbits;
3. the 107 symmetry-reduced exact profiles;
4. the recorded `70 / 17 / 20` screening partition;
5. the 20 corrected retained profiles;
6. the final 30 OPB instances.

This is a source-publication and end-to-end reproducibility task. It is not a defect in the already verified UNSAT certificates.