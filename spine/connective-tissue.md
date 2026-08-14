---
status: DRAFT — Lyra, 2026-07-26, staging for three-leg joint paper
section: Connective tissue — "Why cohomology at all" (Leg 1 → Leg 2)
---

# Why cohomology at all

Leg 1 delivers its verdict in the currency of pairs. The empirical signature of
model monoculture — models that fail on the same inputs more often than chance
would allow — is reported as a mean pairwise error correlation $\bar\rho$, a mean
pairwise agreement-on-failure $\varphi$, and an effective number of independent
judges $n_{\mathrm{eff}}$ (a Kish-style deflation of the nominal panel size by
that same correlation). Each of these is, structurally, a *marginal* over the
$\binom{m}{2}$ two-agent sub-problems: a number one computes by looking at agents
two at a time and averaging. This is not incidental to how the measurements were
taken; it is the shape of the object. $\bar\rho$, $\varphi$, and $n_{\mathrm{eff}}$
live on the edges of the agent graph, never on its higher faces.

The trouble is that the question we actually want answered lives on those higher
faces. When a deployment fields $m \ge 3$ judges and asks *"are these agents
failing independently?"*, it is asking about a joint law over $m$ binary
failure indicators. And here is the wall that motivates everything downstream:
**no pairwise statistic can certify that $m \ge 3$ agents fail independently.**
One can construct joint failure laws that are pairwise-consistent to any desired
tolerance — every $\bar\rho$, every $\varphi$, every marginal matched — yet
harbor an irreducibly three-way (or higher) dependence that no pair, and hence no
average over pairs, can see. Pairwise independence does not imply mutual
independence; the gap between them is not a measurement error one can shrink with
more data at the pairwise level, because the information was never in the pairwise
projection to begin with. It was summed away. $H^1$ of the co-failure sheaf is
precisely the object that this summing-away deletes: the first cohomology of the
presheaf of local (low-order) failure sections is the obstruction to gluing them
into a globally consistent joint law, and it is by construction invisible to
$\bar\rho$ and $\varphi$. That is the entire reason Leg 2 is not ornamental. If
the pairwise numbers could carry the independence certificate, cohomology would
be a categorical restatement of what we already knew; they cannot, so it is the
only object that can carry the certificate they cannot.

We arrive at this position by way of a genuine reversal, and it is worth stating
the reversal in full rather than presenting only its conclusion. An earlier
conjecture of ours — call it the C400 *factorization bridge* — proposed that the
log-growth rate of co-failure could simply be *read off* from $\dim H^1$ via an
additive decomposition of the joint failure KL into pairwise contributions. Had
it held, it would have given a clean dictionary between the cohomological
invariant and an operational co-failure rate. It does not hold. It is refuted by
the third-order log-linear interaction coefficient $\theta_{123}$ — the
coefficient of $x_1 x_2 x_3$ in $\log p(x)$ on $\{0,1\}^3$, equivalently the
irreducible three-way log-odds ratio, the residual that no pairwise fit captures
(not a cup product: $\theta_{123}$ is Möbius-independent of all edge data
$\theta_{ij}$, so it cannot be a product of edge cocycles; and $H^2$ of the
triangle nerve $= 0$, making the cup map $H^1 \times H^1 \to H^2$ identically
zero) — (2026-07-27: corrected label — see theta123-not-a-cup-product).
$\theta_{123}$ is exactly the piece an additive pairwise split cannot reproduce:
the joint failure of three agents carries a term that is not any product or sum
of two-agent terms, and $\theta_{123}$ is its name. The additive bridge died
because it assumed this term away.

But now observe the turn. The same $\theta_{123}$ that killed the bridge is what
makes Leg 2 non-trivial. The bridge was a claim that the higher-order object
*factors* — that the joint reduces to the pairwise. Leg 2 is the claim that it
*does not* — that there is an irreducible higher-order obstruction, and that this
obstruction is a computable cohomology class. These are the same statement read
from opposite sides. If pairwise measures could certify independence, one would
not need cohomology; and if one did not need cohomology, the factorization bridge
would have held. It didn't, so one does. The object that refuted the theorem is
the object that justifies the leg. We spent an iteration trying to make the
three-way term disappear, which is to say we spent an iteration fighting the very
phenomenon the paper is about; the correction was to stop trying to factor it and
start treating its non-factorability as the load-bearing fact.

This is not an isolated observation. Within a single week, and from three
different fields, the same wall was described three times — a convergence worth
recording, though it must be weighted honestly rather than tallied as three
independent votes. Kim (arXiv 2607.20768) shows that standard LLM diversity metrics are
algebraically non-separable from capability at the pairwise level — a
non-identifiability result: you cannot decompose the pairwise numbers into a
diversity component and a capability component, because the projection that
produces $\bar\rho$ and $\varphi$ conflates both. The inference we draw from
Kim is our own, built on that result: if diversity and capability are
non-separable at the pairwise level, then pairwise numbers cannot certify
failure independence; Kim does not himself compute co-failure rates, and we do
not attribute that inference to him. Chen et al. (arXiv 2604.18005) supply an
independent AI-side instance of structural coupling, but the quantity they
report — a collapse to "two or three effective ideas" — is a *response-space
/ output-diversity* estimand (a Vendi-style count on semantic output diversity)
rather than the failure-axis $n_{\mathrm{eff}}$ (Kish deflation of error-vector
correlation) that Leg 1 uses. The distinction matters. If $N$ agents were
genuinely independent, one would expect $\sim N$ effective ideas in the
Vendi/output-diversity sense; communication collapses that to 2–3, which is
the collapse the Chen number names. What transfers to our argument is the
*coupling mechanism* — communication induces a structural collapse of output
diversity, and the same coupling logic applies to failure modes — not the
number 2–3 itself; we do not import it into our $n_{\mathrm{eff}}$. Chen's
additional observation — that *denser topologies and stronger models make it
worse* — confirms that the collapse is not an artifact of weak members. Sargsyan
(arXiv 2607.15629), working in cubical type theory and machine-verified in
Cubical Agda, exhibits a Specker triangle in which pairwise-consistent local data
admit no global model at all, the obstruction being a computable $H^1$ class with
holonomy $\neq 1$.

The honest weighting: these are not three fully independent confirmations. Kim
and collaborators are part of a coordinated Garg/Raghavan research program, so
the Kim datapoint and its programmatic siblings should be read as one line of
work reaching the wall, not as an outside vote — the "three fields agree"
rhetoric must be discounted accordingly. Chen supplies an independent AI-side
instance of the coupling; Sargsyan supplies an independent, machine-verified
instance of the *shape* of the obstruction from outside AI entirely.

That last point requires a sharp boundary, because it is exactly the kind of
place our own recurring error — a true statement about the wrong quantity — would
strike. Sargsyan's result is the same cohomological *machinery* — Čech cohomology
of a presheaf of local sections, with holonomy detecting the obstruction to
gluing — deployed on a *different base* carrying a *different meaning*. His base
is the space of measurement *contexts*; his stalks are possibilistic outcome
labellings; his $H^1 \neq 0$ says that pairwise-consistent local outcomes admit
no globally consistent *labelling*. That is contextuality, failure-to-glue in the
Abramsky–Brandenburger sense — an obstruction to a global assignment of
*outcomes*. Our co-failure sheaf sits on a different base (agents / judges) and
its $H^1$ carries a different meaning (statistical dependence of *failures*).
What we are entitled to say, and all we are entitled to say, is this: *the same
cohomological machinery has just been machine-verified to obstruct global gluing
from pairwise-consistent data.* We are **not** entitled to say that Sargsyan's
$H^1$ *is* our co-failure $H^1$, nor that Sargsyan verified our framework — his
result is analogous in *shape* only. The step from gluing-consistency (his
estimand) to failure-independence (ours) is a Künneth-epistemic transfer that
**we** must argue on its own terms; it is not something the analogy hands us for
free. Sargsyan makes the machinery computable and machine-checked; he does not
close our gate, and we should not let the elegance of the parallel tempt us into
saying he did.

⟦GAP: the phrase "co-failure sheaf" and its $H^1$ should be given a one-sentence
forward-reference to the precise definition in the Leg 2 body (base = agents,
stalks = local failure sections, sheaf condition = consistency of restrictions).
I have not stated that definition here; connective tissue should point to it.⟧

⟦GAP: verify the arXiv IDs and author attributions for all three convergence
papers from primary before this ships — 2607.20768 (Kim et al.), 2604.18005
(Chen et al.), 2607.15629 (Sargsyan). The Sargsyan reading (measurement-context
base, possibilistic stalks, Specker triangle, holonomy $\neq 1$) is Lyra's
primary read of 2026-07-26; the Kim coordinated-program flag needs a citable
basis, not just the browse-agent note.⟧

⟦RESOLVED 2026-07-27: the "$\theta_{123}: H^1 \times H^1 \to H^2$ cup product"
formulation was an overclaim and has been corrected above. $\theta_{123}$ is now
labelled as the third-order log-linear (Möbius) interaction coefficient; the
cup-product framing is explicitly refuted (Möbius-independence of edges + $H^2 = 0$
on the triangle nerve). If Clio's graded construction later establishes a genuine
$H^2$ object, this label can be revisited — but that gate must be argued, not
assumed. See theta123-not-a-cup-product memory note.⟧
