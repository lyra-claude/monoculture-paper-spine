---
status: DRAFT — Lyra, 2026-07-26, staging for three-leg joint paper
section: The $\Omega_{\mathrm{blind}}$ subsection (Leg 3 — operational e-value SLA)
---

> **Terminology is pinned in the Leg-3 body (`leg3-eprocess.md`) and reproduced here so the
> two sections agree.** Let X_s be the per-step betting increment (in Leg 3, X_s = U_s − V_s).
> **Martingale / supermartingale:** the multiplicative wealth process M_t = ∏_{s≤t}(1+λX_s),
> started at M_0 = 1 and nonnegative, satisfies E[1+λX_s | F_{s-1}] = 1 under the *exact* null
> (a *test martingale*), demoted to E[1+λX_s | F_{s-1}] ≤ 1 (a *test supermartingale*) once the
> δ_k drift-slack of the Leg-3 body §5 is subtracted under approximate stratification; this
> multiplicative process (not the additive running sum) is the object Ville's inequality applies to.
> **E-process:** the process {M_t} — equivalently its Robbins mixture over λ — is an e-process;
> an average of e-processes is an e-process.
> **E-value:** the value M_τ at a fixed/stopping time τ, with E[M_τ] ≤ 1 by optional stopping;
> an average of e-values is an e-value.
> **Ville's inequality:** P(sup_t M_t ≥ 1/α) ≤ α under H₀ — the anytime-valid level-α SLA.

# The blind spot: $\Omega_{\mathrm{blind}}$

**A naming guard, stated before any mathematics.** The apparatus below shares its
skeleton with a batch result of Han (arXiv 2607.13918), and a reader who notices
the resemblance will be tempted to treat the two as one — so we name the analogy
out loud and separate the estimands in the same breath. Han's reliability cascade
$r_k$ and our streaming per-pair co-failure e-value SLA are built on the *same*
de Finetti structure: a latent per-instance quantity drawn from a mixture with a
blind-spot atom of mass $(1-\pi)$ — equivalently, a $\pi$-weighted non-blind
component plus that atom. That is the same *phenomenon* in two *formalisms*,
and the two numbers are **not interchangeable**. Han's $r_k$ is a *batch*
reliability-after-$k$-checks quantity — the probability that a serial verifier
cascade has caught the error after $k$ gates. Ours is a *streaming, per-pair
co-failure rate* monitored by an e-process — a nonnegative test supermartingale — that
prices the ongoing rate at which a *pair* of judges fails together. Same latent
atom, different estimand: one is a survivor probability after a fixed number of
serial stages, the other is a rate under continuous parallel monitoring. Plugging
Han's $r_k$ into the SLA's rate, or the SLA's rate into Han's reliability, is a
category error — the exact substitution this subsection exists to forbid. We
invoke Han for the *structure* of the blind spot, never for its numbers.

**Polynomial decay, not immunity.** With that guard in place, Han's batch
analysis of his serial cascade is the reference point. Under partial correlation
between checkers, reliability does *not* improve exponentially with more checks.
Han's Theorem 3.5 — a result about the *batch* cascade — gives the residual
failure of that cascade decaying only polynomially,
$$1 - r_k \;\asymp\; k^{-b},$$
where $b$ is the upper-tail exponent of the batch mixing law. This is Han's
result about the batch/serial object, not a statement about the streaming
per-pair e-process. Whether the streaming per-pair e-process's
residual inherits the same exponent $b$ — rather than a different function of
the mixture shaped by continuous monitoring rather than discrete serial gates —
is an open serial-to-parallel transfer question, flagged for two independent
blind reads and not assumed here. What does transfer, as a qualitative point of
principle, is the regime-claim: correlated checks cannot reach the exponential
independence-rate no matter how many are stacked. This is the exact,
qualitative form of the discipline we impose throughout: *claim the decay rate,
not immunity.* Stacking more correlated checkers helps — the residual does go
down — but for the batch cascade it goes down as a power of $k$, never at the
exponential independence-rate one would get from genuinely decorrelated checks.
You buy improvement at a polynomial price and you never reach the independence
regime by buying more of the same.

**The $-\ln(1-\pi)$ ceiling.** Polynomial decay is the slope; there is also a
hard ceiling, and it is the load-bearing number of this subsection. Han's Theorem
3.6 takes the mixing law to be $G = \pi\,\mathrm{Beta}(a,b) + (1-\pi)\,\delta_1$ —
a $\pi$-weighted non-blind Beta component plus an atom of mass $(1-\pi)$ at
$\alpha = 1$, the region where the verifier accepts the error with probability
one — and shows that the total achievable log-odds gain is capped:
$$\sup_k \,(\ell_k - \ell_0) \;=\; -\ln(1-\pi).$$
A naming hazard must be obeyed exactly here. $\pi$ is the weight of the
*non-blind* Beta component; the **blind-spot mass is $(1-\pi)$** — the atom at
$\alpha=1$. One must **not** call $\pi$ the blind-spot rate; the blind-spot rate
is $(1-\pi)$. Read correctly, the theorem says: no matter how many correlated
checkers you stack, your total reliability gain is bounded above by
$-\ln(1-\pi)$, a finite ceiling fixed by the mass of the shared blind spot. It is
not a slope you can outrun with volume; it is a wall. As the blind-spot mass
$(1-\pi) \to 0$ the ceiling diverges and checking becomes unboundedly useful; as
$(1-\pi)$ grows, the best any cascade of correlated checkers can do is capped, and
capped low.

**From diagnosis to prescription: decorrelate the oracle.** The ceiling tells us
the cure is not more members, and it also tells us — if read one term deeper —
*what* the cure must attack. Han's theorem fixes the ceiling $-\ln(1-\pi)$ for a
*given* mixture with a given blind-spot mass $(1-\pi)$; it does not by itself
prove that structural decorrelation will reduce $(1-\pi)$. The logic is one step
longer: adding more correlated checkers does not change the mixture — they share
the same atom — so they all hit the same ceiling. The *aim* of decorrelation is to
change the mixture itself, to reduce the blind-spot mass $(1-\pi)$ and thereby
raise the ceiling. Han's result *motivates* that aim (it shows the ceiling is what
binds, and that the ceiling is set by $(1-\pi)$), but establishing that structural
decorrelation *actually lowers* $(1-\pi)$ in practice is a separate, open claim we
must argue on its own terms. With that caveat stated, the conceptual target is
clear: the ceiling $-\ln(1-\pi)$ is tightest when the oracle is built from the same
substrate as what it checks — when the checker shares the checked system's failure
modes, the atom at $\alpha=1$ is inflated by precisely that shared architecture,
which is the component that structural decorrelation is designed to remove. The
operational move follows: make the checking apparatus structurally *different* from
what it checks — decorrelate the *oracle* — rather than adding more correlated
voters, who leave the shared atom untouched and only crawl down the polynomial
slope toward a ceiling they cannot move. This is [diversity works, not by vendor]
applied at the oracle itself: it is not the count of checkers that sets the
ceiling, but whether they share the checked system's blind spot.

One further caveat is required: the attribution of part of $(1-\pi)$ to
"architectural coupling" is an *informal conceptual decomposition*, a target for
the prescription rather than a computable partition. No concrete estimator for
"the coupling-attributable share of the blind-spot mass" is given in this
subsection; establishing one is an open item for the Leg-3 body.

**A note on scope, and the honest novelty claim.** Two boundaries keep this
subsection from overreaching. First, the transfer from Han's *serial* verifier
cascade (an atom at $\alpha=1$ in a batch pipeline) to our *parallel* co-failing
model-pairs monitored in a stream is a transfer of *structure*, not an inherited
theorem: the exact ceiling was proved for the serial batch case, and its
quantitative carry-over to the streaming per-pair setting is an open gate we must
argue, not assert. We use Han as the batch/serial twin of a streaming register,
not as a lemma we may cite for our own numbers. Second, on novelty:
anytime-valid e-processes for LLM-*judge* monitoring already exist — Li,
"Who Drifted?" (arXiv 2606.15474) builds exactly such an e-process. But their
estimand is the *temporal drift of a single judge* against a human anchor. Ours
is a different estimand: a *per-pair* e-process monitoring correlated
*co-failure across a pair of judges*, with pairs optionally up-weighted by a
**qualitative** $H^1$-informed prior (a prior on *where to bet* — it affects
power, not validity, and enters no bound; see the Leg-3 body,
`leg3-eprocess.md` §4). No quantitative
$H^1$-weighting of the e-process is claimed. The honest sentence is therefore:
e-processes for judge-monitoring exist (Li, 2026); our contribution is the
co-failure / per-pair application of that anytime-valid machinery, together with
a **qualitative** $H^1$-informed *weighting prior* linking the failure-axis
statistic to the Leg-2 obstruction class — the prior steers power, it enters no
bound, and no quantitative $H^1$-weighting is defined (see the Leg-3 body,
`leg3-eprocess.md` §4). We claim the
estimand and its **qualitative** cohomological framing; we do not claim the
anytime-valid apparatus underneath it, nor any quantitative cohomological bound.

⟦RESOLVED 2026-08-02: the $H^1$-informed weighting prior is scoped as
**qualitative** (steers power / where to bet; enters no bound; no quantitative
object defined). The §[Leg 3] forward-reference now resolves to the Leg-3 body
`leg3-eprocess.md` §4, which confirms *in text* that no quantitative
$H^1$-weighting formula appears and that introducing one would re-open this scope
question. Scope is consistent across the two sections.⟧

⟦RESOLVED 2026-08-02: "supermartingale" vs "e-process / e-value" is now pinned in
the Leg-3 body (`leg3-eprocess.md`, terminology header) and reproduced in this
subsection's header above. The intended object is: the per-step bet builds a
**nonnegative test supermartingale** (E[e_s | F_{s-1}] ≤ 1, e_0 = 1); the running
product $\{M_t\}$ / its Robbins mixture is an **e-process**; Ville's inequality
gives the anytime-valid level-$\alpha$ SLA; an **e-value** is $M_\tau$ at a
stopping time with E[M_τ] ≤ 1. The streaming object is thus pinned; the Han side
remains stated in log-odds $\ell_k$ (batch), and the serial-to-parallel transfer
between the two is the open gate flagged in the scope note, NOT a terminology
mismatch.⟧

⟦GAP: verify from primary that Li "Who Drifted?" is arXiv 2606.15474 and that its
estimand is single-judge temporal drift against a human anchor (not already a
pairwise or co-failure object). This is Lyra's primary read of 2026-07-26 per the
brief; the ID and the estimand claim should be re-confirmed before the novelty
sentence is load-bearing in submission.⟧

⟦GAP: the bracketed cross-reference [diversity works, not by vendor] is an
internal pointer to another section/memory note, not a citation; replace with the
paper's actual section anchor when the spine is assembled.⟧
