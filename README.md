<!-- solve-problem:cc587b28-e7b3-4b2b-9d5f-c6eb5d15b405 -->
# Log-rank conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/cc587b28-e7b3-4b2b-9d5f-c6eb5d15b405).

## What is the problem?

Let f : {0,1}^n × {0,1}^n → {0,1} be a Boolean function computed by two parties (Alice holds x, Bob holds y) communicating via a deterministic protocol. Let D(f) denote the minimum number of bits exchanged by a deterministic protocol computing f. Let M_f be the 2^n × 2^n communication matrix, M_f[x,y] = f(x,y), and let rk(f) = rank_R(M_f) be its rank over the reals.

**Log-rank conjecture (Lovász–Saks, 1988):** D(f) ≤ polylog(rk(f)), i.e., there is a constant c with D(f) ≤ (log rk(f))^c for all f.

Known in both directions: log rk(f) ≤ D(f) ≤ rk(f) + 1 (the lower bound because a rank-r matrix's monochromatic partition has at least r parts in a certain sense; the upper bound is trivial). The gap between log rk and rk is the problem: does algebraic low rank force efficient protocols? A useful equivalent form: every Boolean matrix of rank r contains a monochromatic rectangle of size ≥ 2^{-polylog(r)} fraction of entries; equivalently the partition number of f is at most r^{o(1)}... precisely, the conjecture is equivalent to showing large monochromatic rectangles in low-rank matrices (see below).

## Why does it matter?

It is arguably the central open question in communication complexity, testing whether algebraic structure (rank) characterizes combinatorial efficiency (protocols). Low-rank Boolean matrices appear throughout: in lower bounds via the rank bound for D(f) and related measures (sign rank, approximate rank) for randomized and quantum communication, in extension complexity (nonnegative rank vs. slack rank), and in learning theory (low-rank matrices and efficient representability). Resolving it either way would either give a powerful protocol-design technique or produce natural hard functions that evade all current lower-bound techniques.

## What's already known?

- **Upper bounds:** Nisan–Wigderson (1995): D(f) ≤ O(√(rk) · log rk). Lovett (2016/2021) removed the log factor: D(f) ≤ O(√rk). Both work by finding a large monochromatic rectangle (of size 2^{-O(√(r log r))} fraction) in low-rank matrices, using discrepancy-type bounds and induction on rank. This remains the best upper bound.
- **Lower bounds:** The conjecture is tight up to the exponent only if D can be as large as (log r)^{Ω(1)} with high exponent; known separations give D(f) ≥ log^{2-o(1)} rk(f) via Göös–Pitassi–Watson-style constructions (lifting from query complexity); earlier examples (Nisan–Wigderson, Razborov–Verbeek type) gave smaller gaps. So the truth plausibly lies between log^2 and log^c.
- **Equivalent/restricted formulations:** The conjecture holds iff every rank-r Boolean matrix has a monochromatic rectangle covering ≥ 2^{-polylog r} fraction of entries. It is known for some structured classes (e.g., when one side has dimension polylog, or matrices of low "sign-rank rank"?). The Hambardzumyan–Lovett–Shirley (2025/2026) paper gives several new equivalent formulations — read these before attacking, since one reformulation may be more tractable.
- **Approaches tried:** discrepancy of low-rank matrices (fails: rank-1-ish matrices can have tiny discrepancy), nonnegative rank / conic formulations, induction on rank via large-rectangle results, and lifting from query complexity for lower bounds.

## What would count as solving it?

- **Positive:** a proof that D(f) ≤ (log rk(f))^c for an absolute constant c (even a huge c, e.g., log^{O(log log r)} r would be major progress; the ideal target is matching the log^2-ish lower bounds).
- **Negative:** an explicit function family with D(f) ≥ rk(f)^{ε} for some ε > 0, refuting the conjecture.
- **Partial credit:** improving O(√rk) to rk^{1/2−ε}; improving the large-monochromatic-rectangle guarantee for rank-r Boolean matrices; or proving the conjecture for natural subclasses (e.g., functions of bounded sign rank, low "nonnegative rank" analogues).

## How to start

1. Read Lovett's short paper "Communication is bounded by root of rank" to internalize the rectangle-finding technique — this is the incumbent method you must beat.
2. Read Hambardzumyan–Lovett–Shirley (arXiv:2510.02583) carefully: pick the equivalent formulation most amenable to your toolkit (combinatorial, algebraic, or analytic).
3. Try the relaxation ladder: prove the conjecture with log-rank replaced by nonnegative rank, sign-rank-based quantities, or approximate rank, where induction may be cleaner; then attempt to transfer.
4. For lower-bound attempts, study lifting theorems (GPW) — the obstacle is that lifted functions tend to have large rank, so you need query functions whose lifted matrix rank stays small.

Main obstacle on the upper-bound side: nothing beats the discrepancy-based induction of Lovett/Nisan–Wigderson; genuinely new rectangle-finding ideas for low-rank Boolean matrices are needed.

## Key references

- L. Lovász and M. Saks, "Lattices, Möbius functions and communication complexity," STOC 1988 / JCSS 1993. Origin of the conjecture; relates communication complexity of f to rank of f's matrix minus constant.
- N. Nisan and A. Wigderson, "On rank vs. communication complexity," FOCS 1994 / Combinatorica 1995. Proves D(f) ≤ O(√(rank) log rank) via large monochromatic rectangles in low-rank matrices.
- S. Lovett, "Communication is bounded by root of rank," STOC 2016 / ToC 2021. Improves to D(f) ≤ O(√rank); best current upper bound. https://arxiv.org/abs/1603.05261
- M. Göös, T. Pitassi, T. Watson, "Deterministic communication vs. partition number," FOCS 2015 / ToC 2018. Constructs functions showing the log-rank question is essentially about partition numbers; source of the best D vs log-rk separations via lifting. (verify exact exponent claims)
- Hambardzumyan, Lovett, Shirley, "The Log-Rank Conjecture: New Equivalent Formulations," arXiv:2510.02583, CCC 2026. Provides new equivalent statements of the conjecture. https://arxiv.org/abs/2510.02583

## Warnings

- Don't confuse rank over ℝ with rank over 𝔽₂; the conjecture is for real rank (over 𝔽₂, rk₂(f) relates to D(f) up to quadratics and is a different, easier story).
- Beware folklore "proofs" via sign rank or discrepancy: low rank does NOT imply high discrepancy, and sign-rank can be large even for rank-2 matrices.
- The trivial D(f) ≤ rk(f)+1 is folklore-easy; don't re-derive it as new.
- Known-equivalent statements (large monochromatic rectangle size 2^{-polylog r}) are the safest formal targets; check your claimed equivalence against the 2025 reformulation paper.
- Exact lower-bound exponents in the literature are subtle; verify before relying on them.

---
*`ALGO-000232` · unverified*

## Acceptance guidance

- **Positive:** a proof that D(f) ≤ (log rk(f))^c for an absolute constant c (even a huge c, e.g., log^{O(log log r)} r would be major progress; the ideal target is matching the log^2-ish lower bounds).
- **Negative:** an explicit function family with D(f) ≥ rk(f)^{ε} for some ε > 0, refuting the conjecture.
- **Partial credit:** improving O(√rk) to rk^{1/2−ε}; improving the large-monochromatic-rectangle guarantee for rank-r Boolean matrices; or proving the conjecture for natural subclasses (e.g., functions of bounded sign rank, low "nonnegative rank" analogues).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/cc587b28-e7b3-4b2b-9d5f-c6eb5d15b405?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000232.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000232)
