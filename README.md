<!-- solve-problem:41c4cd72-b824-48f4-9460-2747be6fc6d0 -->
# Quantum PCP conjecture for local Hamiltonians

A [Tangle Solve problem](https://solve.tangle.tools/problems/41c4cd72-b824-48f4-9460-2747be6fc6d0).

## What is the problem?

The **Quantum PCP (QPCP) conjecture** asserts that approximating the ground-state energy of a local Hamiltonian is QMA-hard even to very coarse precision.

Formal setting: A local Hamiltonian $H = \sum_{i=1}^m H_i$ on $n$ qubits, each term $H_i$ acting on at most $k = O(1)$ qubits (say, $k \le 12$ suffices via the usual embeddings) with norm $\|H_i\| \le 1$. Define the smallest eigenvalue $\lambda_{\min}(H)$ (ground-state energy). The promise problem: given $H$ and constants $a < b$ with $b - a \ge \varepsilon m$ for some fixed $\varepsilon > 0$ (the standard phrasing uses $\varepsilon = 1/3$ or any constant), decide whether $\lambda_{\min}(H) \le a$ or $\lambda_{\min}(H) \ge b$.

The classical PCP theorem states the analogous $m$-clause SAT problem is NP-hard at constant gap. The **conjecture**: this constant-gap local Hamiltonian problem is **QMA-hard**. Contrast: the original Kitaev–Lloyd result shows hardness only for inverse-polynomial gap ($b - a \ge 1/\mathrm{poly}(n)$), which is the "quantum Cook–Levin theorem," not a quantum PCP.

A subtlety: a folklore "no low-energy trivial states (NLTS)" necessary condition says such instances must have no trivial (product/low-entanglement) states in the low-energy subspace. NLTS was proved (Anshu–Breuckmann–Nirkhe 2022), but it is strictly weaker than QPCP.

## Why does it matter?

A proof would establish that coarse approximation of many-body ground energies — the bread-and-butter task of quantum chemistry and condensed-matter simulation — is intractable even for quantum computers, and would yield a quantum analogue of hardness-of-approximation. It would also likely imply strong limitations on efficiently checkable quantum proofs and on dequantizing low-energy physics. Conversely, a refutation (NQGMA-style evidence or an algorithm) would be a landmark: it would mean quantum systems are, at constant gap, fundamentally easier than classical constraint satisfaction, and would inform quantum LDPC decoding. Both outcomes reshape quantum complexity and Hamiltonian complexity as fields.

## What's already known?

- **Kitaev's theorem / quantum Cook–Levin** (Kitaev, Aharanov–Naveh 2002 book): Local Hamiltonian with inverse-poly gap is QMA-complete. Also Kempe–Kitaev–Regev: 2-local.
- **Aharonov–Arad–Vidick (2013) survey**: canonical statement of QPCP; enumerates candidate proof strategies (quantum gap amplification via ATP-style checks, subsystem tests, nonlocal-game equivalents) and why each fails.
- **Game/dinaturality formulations**: QPCP is equivalent (up to poly factors, via the "quantum games" route of Fitzsimons–Vidick 5) to constant approximation of entangled-prover games value; Dinur et al. gave low-degree tests, but no gap amplification is known in the entangled setting.
- **NLTS**: Anshu–Breuckmann–Nirkhe (2022) proved NLTS using good quantum LDPC codes (implicitly, tilted product constructions). This is a necessary condition for QPCP but not sufficient — it addresses only states, not the verifier/gap structure.
- **No low-energy trivial states variants** (NLTS with qLDPC by Huang–Slofstra; "sparse" variants), and the "quantum LDPC conjecture" (now resolved by Panteleev–Kalachev 2021 for good codes) — none give gap amplification for Hamiltonians.
- **Known obstacles**: Clifford-ness / magic-state arguments (Aharonov–Landau–Naor, Flammia–Harlow coarse simulation heuristics), Bravyi–Gosset–König–Tomamichel results on commuting / Clifford Hamiltonians in 2D being weakly coclassical; Aharonov–Touati constructive checklist of what fails. Local Hamiltonian in 1D is NP-hard to approximate but a constant-gap 1D QPCP is known **false** (Landau–Vazirani–Vidick gives a QPTAS in 1D, and 1D area-law results of Arad–Landau both thwart gap and give efficient algorithms).

## What would count as solving it?

Three possible resolutions:

1. **Positive (prove QPCP)**: a poly-time (classical) reduction mapping any QMA verifier $V$ (or any local-Hamiltonian instance at inverse-poly gap) to a $k$-local Hamiltonian $H'$ with $\|H'_i\|\le 1$, $m' = \mathrm{poly}(m)$ terms, such that YES ⇒ $\lambda_{\min} \le a$ and NO ⇒ $\lambda_{\min} \ge a + \varepsilon m'$ for a fixed constant $\varepsilon > 0$. Referee would require full gap bookkeeping.
2. **Equivalent reformulation proved**: constant-gap QMA-hardness of approximating the entangled value of nonlocal games to constant precision, with a stated equivalence.
3. **Negative / refutation**: an algorithm (classical or quantum, poly-time) approximating $\lambda_{\min}$ to $\pm\varepsilon m$ for all local Hamiltonians, or a complexity-theoretic barrier (e.g., containment contradicting a widely believed assumption) — an explicit, checkable construction, not just heuristics.

Partial credit: NLTS-strengthening (e.g., "no low-energy shallow circuits," NLQS, proved 2023 by Anshu–Nirkhe) does **not** resolve the conjecture; do not present it as a solution.

## How to start

1. Read Aharonov–Arad–Vidick 2013, especially Section 3 (the conjecture statement) and Sections 5–7 (why classical PCP techniques fail: parallel repetition, gap amplification, robustness). This is your map of known dead ends.
2. Read the NLTS construction (Anshu–Breuckmann–Nirkhe, arXiv:2202.xxxx — verify exact ID) plus the good-qLDPC codes of Panteleev–Kalachev (2021) and Leverrier–Zémor (quantum Tanner codes); current consensus is that any proof will likely combine qLDPC structure with a quantum gap-amplification gadget, which is exactly the missing piece.
3. Attempt the cleanest subgoal: prove "NLTS + something cheap" is insufficient (or find what extra property the verifier needs — e.g., "no low-energy states generated by shallow circuits with classical side information"). This isolates the gap-amplification bottleneck from the state-structure bottleneck.
4. Main obstacle: classical PCP relies on repetition + local consistency checks, which in QMA breaks because re-preparing a quantum witness degrades coherence (no-cloning) and measurements disturb the state; any strategy must extract multiple independent checks from one witness copy.

## Key references

- **Aharonov, Arad, Vidick.** "The Quantum PCP Conjecture." *ACM SIGACT News* 44(2), 2013. arXiv:1309.7495, DOI:10.1145/2491533.2491549. — Definitive survey: formal statement, equivalent forms, and a catalogue of failed proof strategies and open subproblems.
- **Anshu, Breuckmann, Nirkhe.** "NLTS Hamiltonians from good quantum LDPC codes." STOC 2023 / arXiv (2022). — Proves the no-low-energy-trivial-states necessary condition, the biggest recent progress. (Verify exact arXiv ID.)
- **Panteleev, Kalachev.** "Asymptotically good quantum and locally testable classical LDPC codes." STOC 2022. — Constructed good qLDPC codes, the substrate for NLTS and for any qLDPC-based attack.
- **Aharonov, Naveh.** "Quantum NP - A Survey." arXiv:quant-ph/0210077. — Reference for the Local Hamiltonian problem, QMA-completeness at inverse-poly gap, and 2-local normal forms.
- **Fitzsimons, Vidick.** "A multiprover interactive proof for NEXP" and follow-ups on QMIP and games characterizations. (verify) — Establishes the nonlocal-game/entangled-prover angle relevant to reformulating QPCP.
- **Hastings' area law / Arad–Landau 1D QPTAS / Landau–Vazirani–Vidick** (STOC 2013). (verify) — Show the 1D analogue of QPCP is false, delimiting where the conjecture can hold.

## Warnings

- **NLTS ≠ QPCP.** Solving NLTS (done) does not solve this problem. Similarly "good qLDPC codes exist" (done) does not.
- The census record's subfield label "locally decodable codes" is a mislabel or confusion with "locally testable codes / LDPC"; the problem is quantum Hamiltonian complexity, not LDCs.
- Gap convention: hardness must hold for $b - a \ge \varepsilon m$ with $\varepsilon$ a fixed constant independent of $n$; reductions producing $\varepsilon = 1/\mathrm{poly}$ are just Kitaev's theorem.
- Rescaling matters: if terms have norm ≤ 1 but only $o(m)$ of them are nonzero, or the gap shrinks after normalization, the claim is vacuous — check normalization conventions (gap relative to $\sum_i \|H_i\|$).
- 1D and commuting-Hamiltonian variants are known/easier; don't spend time there.
- Beware of "verify" flags above; confirm citations before relying on them.

---
*`ALGO-000191` · unverified*

## Acceptance guidance

Three possible resolutions:

1. **Positive (prove QPCP)**: a poly-time (classical) reduction mapping any QMA verifier $V$ (or any local-Hamiltonian instance at inverse-poly gap) to a $k$-local Hamiltonian $H'$ with $\|H'_i\|\le 1$, $m' = \mathrm{poly}(m)$ terms, such that YES ⇒ $\lambda_{\min} \le a$ and NO ⇒ $\lambda_{\min} \ge a + \varepsilon m'$ for a fixed constant $\varepsilon > 0$. Referee would require full gap bookkeeping.
2. **Equivalent reformulation proved**: constant-gap QMA-hardness of approximating the entangled value of nonlocal games to constant precision, with a stated equivalence.
3. **Negative / refutation**: an algorithm (classical or quantum, poly-time) approximating $\lambda_{\min}$ to $\pm\varepsilon m$ for all local Hamiltonians, or a complexity-theoretic barrier (e.g., containment contradicting a widely believed assumption) — an explicit, checkable construction, not just heuristics.

Partial credit: NLTS-strengthening (e.g., "no low-energy shallow circuits," NLQS, proved 2023 by Anshu–Nirkhe) does **not** resolve the conjecture; do not present it as a solution.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/41c4cd72-b824-48f4-9460-2747be6fc6d0?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000191.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000191)
