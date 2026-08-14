---
status: SKETCH — Lyra, 2026-07-29, staging for three-leg joint paper
section: Directed companion — "Co-failure has direction the symmetric summaries cannot see"
note: sketch altitude — prose + a few display equations, not final LaTeX. Hedging is load-bearing; do not smooth it out.
seam: the Γ⁺ decomposition (§"Restoring Perron–Frobenius") is Claudius's contribution (email 1693); the rest is Lyra's. This is the one joint seam in an otherwise Lyra-owned companion.
---

# The directed companion

## Motivation

Legs 1 and 2 measure co-failure with *symmetric* instruments. Leg 1's joint
tail $\Pr[i \wedge j]$ is symmetric in its arguments by construction; the mean
pairwise correlation $\bar\rho$ and $n_{\mathrm{eff}}$ are averages over
unordered pairs. Leg 2's undirected spectral summary — the algebraic
connectivity $\lambda_2$ of the co-failure graph — is symmetric by definition of
the Laplacian it is drawn from. None of these can carry an arrow.

But co-failure has direction. "If the anchor model is wrong, how often is the
satellite also wrong?" and "if the satellite is wrong, how often is the anchor?"
are different questions with different answers, and a deployment that shares
weight or context asymmetrically across its panel cares which is which. Our own
C387 result is the sharp warning here: an undirected, $\pi$-based spectral
summary — a Chung directed-Laplacian eigenvalue read under a *uniform* stationary
measure — is **blind to edge direction** exactly when $\pi$ is uniform. The
symmetric summary is not merely coarser; on a class of genuinely directed
structures it returns the same number regardless of orientation. If direction is
real, we need an object that is not symmetrized before we look at it.

## The object

Define the directed coupling matrix on the panel of $m$ agents by
$$
\Gamma_{ij} \;=\; \Pr[j \text{ wrong} \mid i \text{ wrong}] \;-\; \Pr[j \text{ wrong}],
$$
the *excess* conditional failure of $j$ given $i$ has failed, over $j$'s
marginal failure rate. $\Gamma_{ij} > 0$ says $i$'s failure raises $j$'s failure
probability; $\Gamma_{ij}=0$ is the independence baseline; $\Gamma_{ij}<0$ says
$i$'s failure *lowers* $j$'s — an inhibitory, anti-correlated link. **$\Gamma$ is
therefore signed in general**, and this sign structure is not a nuisance to be
assumed away; it is what forces the careful treatment below.

The direction does **not** live in the joint. The joint co-failure
$\Pr[i \wedge j]$ is symmetric, so it cannot be the carrier of an arrow. Direction
lives in the *conditional*, and it appears the moment the marginals differ:
$$
\Pr[j \mid i] = \frac{\Pr[i \wedge j]}{\Pr[i]}, \qquad
\Pr[i \mid j] = \frac{\Pr[i \wedge j]}{\Pr[j]}.
$$
Same numerator, different denominator. Hence
$$
\Gamma_{ij} - \Gamma_{ji}
= \Pr[i \wedge j]\!\left(\frac{1}{\Pr[i]} - \frac{1}{\Pr[j]}\right),
$$
which is nonzero precisely when $\Pr[i \text{ wrong}] \neq \Pr[j \text{ wrong}]$.
The asymmetry of $\Gamma$ *is* the heterogeneity of the marginal error rates,
routed through a symmetric joint. Under equal marginals $\Gamma$ is symmetric and
carries no more than the undirected summary already does; the directed object only
earns its keep when the panel is heterogeneous.

## The bridge to C387 — stated as analogy, not identity

In C387, direction became invisible when the stationary measure $\pi$ was
*uniform*. Here, the corresponding degenerate case is *homogeneous marginal error
rates*: equal $\Pr[i \text{ wrong}]$ across the panel collapses $\Gamma$ to
symmetric, just as uniform $\pi$ collapsed the directed Laplacian to something an
undirected eigenvalue could read. So "uniform $\pi$" $\leftrightarrow$
"homogeneous marginals" is the correspondence the analogy suggests.

And real ensembles are *not* homogeneous. The characteristic monoculture panel is
a strong anchor model surrounded by weaker satellites — the asymmetric-star
topology from C387's own experiment — so the marginals are unequal, $\Gamma$ is
genuinely asymmetric, and the direction is real and invisible to undirected
$\lambda_2$.

I want to be explicit about what is *not* yet established. Whether the Perron
structure of $\Gamma^+$ (below) maps precisely onto Chung's directed-Laplacian
spectrum under the induced $\pi$ — i.e. whether "heterogeneous marginals" and
"non-uniform $\pi$" are the *same* non-degeneracy driving the *same* spectral
object, or merely two things that both happen to break symmetry — is an **open
transfer that must be argued, not asserted**. I am claiming the analogy (both
collapse in their respective uniform/homogeneous limit) and flagging the identity
as a gate. This is the recurring discipline: assert the transfer, then verify it;
do not wave at it. The C387 lesson transfers as motivation with certainty and as
machinery only on condition.

## Restoring Perron–Frobenius: the $\Gamma^+$ decomposition

*(This section incorporates Claudius's contribution, email 1693. The distinction
it draws — spectral radius for the signed matrix, Perron root only for its
nonnegative part — is the fix for the terminology hazard in the earlier sketch,
which spoke of a "Perron root of $\Gamma$" that $\Gamma$'s sign structure does not
license.)*

Because $\Gamma$ is signed, we must be careful about what its spectrum is
entitled to mean. For a general signed matrix, the only summary we may take is the
**spectral radius**
$$
\rho(\Gamma) \;=\; \max_k |\lambda_k(\Gamma)|,
$$
the largest-modulus eigenvalue. This is *not* a Perron root: the Perron–Frobenius
theorem — which guarantees a real, positive, simple dominant eigenvalue with a
nonnegative eigenvector — requires a nonnegative matrix, and $\Gamma$ has negative
entries wherever a link is inhibitory. Calling $\rho(\Gamma)$ a "Perron root," as
an earlier draft did, is exactly the kind of borrowed-guarantee error we are on
guard against. **For the full signed $\Gamma$: spectral radius, and nothing
Perron–Frobenius comes with it for free.**

Claudius's fix is to split $\Gamma$ into its nonnegative and nonpositive parts
*entrywise*:
$$
\Gamma \;=\; \Gamma^+ - \Gamma^-, \qquad
\Gamma^+_{ij} = \max(\Gamma_{ij}, 0), \quad
\Gamma^-_{ij} = \max(-\Gamma_{ij}, 0),
$$
so that $\Gamma^+$ collects the *excitatory* couplings (one failure raises
another's probability) and $\Gamma^-$ the *inhibitory* ones (one failure lowers
another's). Both are nonnegative by construction, and $\Gamma^+$ holds exactly the
links along which a co-failure impulse can *grow*.

Now $\Gamma^+ \ge 0$ entrywise, so **Perron–Frobenius applies to $\Gamma^+$
exactly.** Its dominant eigenvalue is real, nonnegative, and carries a nonnegative
eigenvector; $\rho(\Gamma^+)$ **is** a genuine Perron root. This is the one place
in the section the term is licensed, and it is licensed *only* for $\Gamma^+$, not
for $\Gamma$.

## The Galton–Watson reading of $\Gamma^+$

With $\Gamma^+$ nonnegative, its Perron root acquires an *exact* — not
analogical — interpretation, provided we first posit a propagation dynamics (see
the weak joints below; the dynamics is a modeling choice, not something the matrix
hands us). The modeling commitment that makes the containment lemma go through is a
specific one, and worth stating plainly: we model inhibition as the **killing of
individual failure events / lineages** (a *thinning* of the branching population),
not as **continuous subtraction from a shared medium**. In the thinning model the
co-failure mass is a nonnegative *count* of surviving lineages and $\Gamma^-$ can
only remove members of that count, so the majorant coupling $X_t \le Y_t$ holds by
construction; in the continuous-medium model $\{X_t\}$ obeys a linear update
$X_{t+1} = \Gamma^+ X_t - \Gamma^- X_t$ in which a component can be driven negative,
whereupon the $-\Gamma^- X_t$ term flips sign and *re-adds* mass, breaking the
majorant. The two models agree on the mean but not on the pathwise domination the
lemma needs — which is why hypothesis (2) below is a modeling commitment to the
thinning realization, not a free consequence of the definition of $\Gamma$.
Read $\Gamma^+_{ij}$ as the expected number of "offspring" failures it
induces at $j$ per failure at $i$ — a multitype branching (Galton–Watson) process
whose mean-offspring matrix is $\Gamma^+$. For such a process the classical
criticality dichotomy is a theorem, not a metaphor:
$$
\rho(\Gamma^+) < 1 \;\Rightarrow\; \text{the } \Gamma^+ \text{ branching process is subcritical (extinction a.s.)},
$$
$$
\rho(\Gamma^+) > 1 \;\Rightarrow\; \text{supercritical (positive survival probability)},
$$
with $\rho(\Gamma^+) = 1$ the exact critical threshold. This is where "the Perron
root is the cascade threshold" earns the word *exact*: for the nonnegative
$\Gamma^+$ under a branching dynamics, the threshold at $\rho = 1$ is the standard
Galton–Watson criticality result. What was, in the earlier sketch, an *analogy*
about "a co-failure impulse decaying iff the dominant eigenvalue is sub-unit" is,
restricted to $\Gamma^+$ and its majorant process, a real criticality theorem.

## The gate — as a conservative sufficient condition

We can now state a containment criterion for the full signed system without
overclaiming. The excitatory part $\Gamma^+$ is what makes a cascade grow; the
inhibitory part $\Gamma^-$ can only *remove* mass from a co-failure impulse.
Under a propagation dynamics in which the $\Gamma^+$-only branching process
dominates the true (signed) process trajectory-by-trajectory — inhibition subtracts,
never adds — the $\Gamma^+$ process is a **majorant**, and:
$$
\boxed{\;\rho(\Gamma^+) < 1 \;\Longrightarrow\; \text{co-failure cascade contained in the full signed system.}\;}
$$
This is a **sufficient, not necessary** condition, and deliberately conservative:
it certifies containment by bounding the *worst case in which every inhibitory
link is switched off*. The real system, with $\Gamma^-$ active, is at least as
contained. A panel can therefore be safe ($\rho(\Gamma) $-behaviour benign) while
$\rho(\Gamma^+) \ge 1$ — the criterion will simply decline to certify it, never
falsely condemn it. That asymmetry is the right one for a safety gate: it errs
toward demanding more evidence, not toward false comfort.

Two things this gate does **not** say, stated here and unpacked in the weak
joints. It does not say $\rho(\Gamma^+) < 1 \Rightarrow \rho(\Gamma) < 1$ as a
spectral inequality — the standard bound $\rho(\Gamma) \le \rho(|\Gamma|)$ runs
the *other* way ($\rho(\Gamma^+) \le \rho(|\Gamma|)$ too), so the containment
claim rests on the *dynamical* majorant argument, not on comparing spectral radii.
And it does not license any threshold statement about $\rho(\Gamma)$ itself:
$\rho(\Gamma) < 1$ as a cascade gate for the signed system remains an analogy
until a signed-process criticality theorem is supplied.

## The Monotone-Majorant Containment Lemma

> ⟦DRAFT — co-lock w/ Claudius; obligations (d) and (i) discharged, C387 transfer gate still open⟧
> The following is a named statement of the gate above, promoted to lemma form so
> the proof obligations are pinned in one place. Obligation (d) — the load-bearing
> "$\Gamma^-$ genuinely contains" gap — is **discharged** (co-confirmed with
> Claudius): the lemma is a **theorem under the thinning realization** of
> $\Gamma^-$, and *fails* under continuous linear subtraction, so hypothesis (2) is
> pinned to the thinning regime. Obligation (i) — weak joint 3, "posit the
> propagation dynamics explicitly" — is now also **discharged**: the
> Poisson excitatory–inhibitory thinned branching (EITB) process of
> §"An explicit dynamics" exhibits *one* concrete rule under which hypotheses (1)
> and (2) are **theorems rather than posits**, proving the lemma's hypothesis-class
> is nonempty. What remains open is the C387 transfer gate (obligation (ii),
> Claudius's); the containment result is a **dynamical majorant under the thinning
> hypothesis, not a spectral theorem for general signed $\Gamma$**. It is written
> to be *consistent with* the weak joints §, not to supersede them: where they
> hedge, this lemma inherits the hedge.

**Lemma (Monotone-Majorant Containment).**
Let $\Gamma = \Gamma^+ - \Gamma^-$ be the signed conditional-excess co-failure
matrix on a panel of $m$ agents, with $\Gamma^+, \Gamma^- \ge 0$ entrywise (the
excitatory and inhibitory parts of §"Restoring Perron–Frobenius"). Suppose a
propagation dynamics $\{X_t\}_{t \ge 0}$ on nonnegative co-failure-mass vectors is
posited such that:

1. *(Branching interpretation.)* $\Gamma^+$ is the mean-offspring matrix of the
   multitype Galton–Watson process $\{Y_t\}$ obtained by retaining only the
   excitatory couplings — i.e. $\mathbb{E}[Y_{t+1} \mid Y_t] = \Gamma^{+\top} Y_t$; and
2. *(Nonnegativity-preserving inhibition — the thinning realization.)*
   $\Gamma^-$ is nonnegativity-preserving: inhibition operates as sub-individual
   killing (inhibition probability $\le 1$ per unit), so mass counts cannot go
   negative by construction. Under this thinning realization suppression deletes
   lineage mass, it does not reroute, reflect, or over-subtract it — so the update
   is **monotone** and the excitatory process dominates the true signed process
   pathwise: $\;X_t \le Y_t\;$ (entrywise) for all $t$, under the natural coupling
   with $X_0 = Y_0$.

Then
$$
\boxed{\;\rho(\Gamma^+) < 1 \;\Longrightarrow\; \text{the co-failure cascade of the full signed system } \{X_t\} \text{ is contained (extinguishes a.s.).}\;}
$$
The hypothesis is a **Perron root** condition on the nonnegative $\Gamma^+$ (P–F
licensed); the conclusion is containment of the *signed* cascade, and holds **only
under the posited monotone / absorptive regime** — it is not a statement about
$\Gamma$'s spectrum. The condition is **sufficient, not necessary**, and
conservative: it certifies by switching every inhibitory link off.

**(b) Why this is not a spectral inequality.**
The lemma is emphatically *not* derived from any eigenvalue comparison between
$\Gamma$ and $\Gamma^+$. By Wielandt's bound both radii are dominated by the same
nonnegative envelope, $\rho(\Gamma) \le \rho(|\Gamma|)$ **and**
$\rho(\Gamma^+) \le \rho(|\Gamma|)$, and *neither controls the other*: one cannot
conclude $\rho(\Gamma) < 1$ from $\rho(\Gamma^+) < 1$, nor vice versa. In
particular $\Gamma$ is signed, so it has no Perron–Frobenius structure and
$\rho(\Gamma)$ is a bare **spectral radius**, entitled to none of the guarantees
(real positive dominant eigenvalue, nonnegative eigenvector) that make the
$\Gamma^+$ criticality argument work. The containment result therefore lives at
the level of the **dynamics** — a pathwise majorant between two processes — and
*not* at the level of eigenvalues. Any attempt to restate it as
"$\rho(\Gamma^+) < 1 \Rightarrow \rho(\Gamma) < 1$" is exactly the borrowed-guarantee
error this companion is on guard against.

**(c) Proof sketch (majorant / coupling argument).**
Construct the auxiliary multitype Galton–Watson process $\{Y_t\}$ with
mean-offspring matrix $\Gamma^+ \ge 0$: each unit of co-failure mass at agent $i$
produces, in expectation, $\Gamma^+_{ij}$ units at $j$ in the next generation,
with *no* inhibitory bookkeeping. Since $\Gamma^+$ is nonnegative, Perron–Frobenius
applies and the classical Galton–Watson criticality dichotomy holds *exactly*:
$\rho(\Gamma^+) < 1$ makes $\{Y_t\}$ subcritical, hence
$\mathbb{E}[\mathbf{1}^\top Y_t] = \mathbf{1}^\top (\Gamma^{+\top})^t Y_0 \to 0$
geometrically and $Y_t \to 0$ a.s. (extinction) — the threshold is still
$\rho(\Gamma^+) < 1$ because $\rho(\Gamma^{+\top}) = \rho(\Gamma^+)$. Under hypotheses (1)–(2), couple
$\{X_t\}$ and $\{Y_t\}$ on a common probability space with $X_0 = Y_0$: at each
step the signed update produces the same excitatory offspring as $Y$ but *removes*
additional mass through the absorptive $\Gamma^-$ channel (never adds), so
monotonicity of the update propagates $X_t \le Y_t$ entrywise for all $t$ by
induction. Squeezing, $0 \le X_t \le Y_t \to 0$ gives $X_t \to 0$ a.s.: the true
signed cascade is contained whenever its excitatory majorant is subcritical. $\;\square$
*(sketch — the induction step in (2) is where the regime does the real work, and
where obligation (d) below is discharged or fails.)*

**(d) Proof obligation — "$\Gamma^-$ genuinely contains" — DISCHARGED.**
*Discharged (co-confirmed with Claudius): the lemma is a **theorem** under the
thinning realization of $\Gamma^-$ (sub-individual killing; counts stay $\ge 0$;
pathwise coupling $X_t \le Y_t$ holds by construction). It **fails** under
continuous linear subtraction ($X_{t+1} = \Gamma^+ X_t - \Gamma^- X_t$), where a
component can go negative and $-\Gamma^- X_t$ re-adds mass, breaking the majorant.
Claudius confirmed his intended "genealogical mass flow" IS the thinning
realization, and his own attempt to build a counterexample under thinning failed;
hypothesis (2) is now pinned to the thinning regime accordingly.*

The sketch *assumes* that inhibition is purely absorptive — that $\Gamma^-$ can
only subtract mass, so the coupling $X_t \le Y_t$ is preserved. This is **not**
free, and it is the load-bearing gap this lemma once owed. Negative feedback in a
monotone dynamical system can be subtle: a suppressive link that removes mass at
one node can, through the network, *relieve* competition elsewhere and so
indirectly permit growth — i.e. an inhibitory coupling need not be globally
stabilising even when it is locally mass-removing. The obligation, stated
explicitly and flagged as owed:

> **Obligation (Γ⁻-containment).** Exhibit a class of propagation dynamics under
> which $\Gamma^-$ acts as a strictly absorptive (mass-removing, non-redirective)
> channel *and* prove that within this class the pathwise domination $X_t \le Y_t$
> holds for all $t$ — i.e. that absorptive negative coupling cannot destabilise
> the signed process relative to its $\Gamma^+$ majorant.

*Resolution.* The class is the **thinning realization**: $\Gamma^-$ is
nonnegativity-preserving, acting as sub-individual killing (inhibition probability
$\le 1$ per unit), so the co-failure mass is a nonnegative count and suppression
can only delete members of it. Within this class the coupling $X_t \le Y_t$ holds
by construction (each step removes mass from $X$ relative to $Y$, never adds), so
the majorant survives and the Lemma is a theorem. The obligation therefore
**pins hypothesis (2) to the thinning regime** rather than leaving it a free
posit: the continuous-medium alternative, in which $\Gamma^-$ subtracts linearly
and a component may go negative, is exactly the class in which the domination
fails, and it is excluded by hypothesis (2). This resolution was **co-confirmed
with Claudius**, whose intended "genealogical mass flow" is the thinning
realization and whose own attempt at a thinning counterexample failed.

## An explicit dynamics — the EITB process (discharges obligation (i))

Weak joint 3 (obligation (i)) held that hypotheses (1)–(2) of the lemma were
*posited*, not *derived*: the containment result was conditional on the existence
of some propagation dynamics under which $\Gamma^+$ is the mean-offspring matrix
and the $\Gamma^+$-only process dominates the signed process pathwise. We now
**exhibit one such dynamics explicitly**, turning both hypotheses into theorems of
a construction. This does not claim the real co-failure system *is* this dynamics;
it shows the hypothesis-class of the lemma is **nonempty** — the two hypotheses are
jointly realizable, not vacuous or mutually inconsistent. The lemma reads, after
this section, as: *if a thinning–branching dynamics of this kind governs the panel,
then $\rho(\Gamma^+) < 1$ contains the cascade*, and such a dynamics demonstrably
exists.

Call it the **Poisson excitatory–inhibitory thinned branching (EITB) process.**

*State space.* $X_t \in \mathbb{Z}_{\ge 0}^m$, a configuration of "particles,"
each carrying an agent-type $i \in \{1, \dots, m\}$. A particle is an active
co-failure impulse; the count $X_{t,i}$ at coordinate $i$ is the number of live
impulses currently sitting at agent $i$. This is the nonnegative *count* the
thinning realization of §"Galton–Watson" requires — co-failure mass as a
population of lineages, never a continuous medium.

*One generation $X_t \to X_{t+1}$, in two stages.*

**Stage 1 (excitation / branching).** Each type-$i$ particle, independently of all
others, spawns a litter: for each target $j$ it produces
$$
K_{ij} \sim \mathrm{Poisson}(\Gamma^+_{ij})
$$
type-$j$ children, independent across targets $j$ and across particles. Write the
resulting pre-thinning configuration as $\tilde Y$.

> **Claim (a) — $\Gamma^+$ is the mean-offspring matrix.** $\mathbb{E}[\tilde Y \mid X_t] = \Gamma^{+\top} X_t$.
>
> *Proof.* Fix a target coordinate $j$. A single type-$i$ particle contributes
> $K_{ij} \sim \mathrm{Poisson}(\Gamma^+_{ij})$ type-$j$ children, so it contributes
> mean $\mathbb{E}[K_{ij}] = \Gamma^+_{ij}$ (the mean of a $\mathrm{Poisson}(\lambda)$
> is $\lambda$). There are $X_{t,i}$ type-$i$ particles, each spawning an
> independent such litter, and the litters of different parents (and different
> targets) are independent, so by linearity of expectation the total mean number of
> type-$j$ children is
> $$
> \mathbb{E}[\tilde Y_j \mid X_t] \;=\; \sum_{i=1}^m X_{t,i}\, \mathbb{E}[K_{ij}]
> \;=\; \sum_{i=1}^m \Gamma^+_{ij}\, X_{t,i} \;=\; (\Gamma^{+\top} X_t)_j .
> $$
> Row $i$ of $\Gamma^+$ is parent type $i$, so the sum $\sum_i \Gamma^+_{ij} X_{t,i}$
> pairs the $j$-th *column* of $\Gamma^+$ against $X_t$ — that is $(\Gamma^{+\top} X_t)_j$,
> not $(\Gamma^+ X_t)_j$: the mean vector evolves by the transpose $\Gamma^{+\top}$,
> consistent with the inhibitory input $I_j = (\Gamma^{-\top} X_t)_j$.
> Stacking over $j$ gives $\mathbb{E}[\tilde Y \mid X_t] = \Gamma^{+\top} X_t$. $\;\square$

Claim (a) discharges **hypothesis (1) by construction**: the excitation stage is a
multitype Galton–Watson step whose mean-offspring matrix is exactly $\Gamma^+$.
(Well-defined because $\Gamma^+_{ij} \ge 0$, so every Poisson rate is legitimate.)

**Stage 2 (inhibition / thinning).** Each type-$j$ child in $\tilde Y$ is retained
independently with probability $r_j(X_t) \in [0,1]$ and killed with probability
$1 - r_j$, where $r_j$ is *any* prescribed function that is non-increasing in the
local inhibitory input
$$
I_j \;:=\; \sum_{i=1}^m \Gamma^-_{ij}\, X_{t,i} \;=\; (\Gamma^{-\top} X_t)_j \;\ge\; 0 .
$$
The retained configuration is $X_{t+1}$. A canonical choice is $r_j = e^{-I_j}$,
which lies in $(0,1]$, equals $1$ when there is no inhibition ($I_j = 0$), and
$\to 0$ under strong inhibition; but the precise form is immaterial. **Any**
retention probability in $[0,1]$ yields a valid thinning. This is deliberate: the
containment conclusion is a property of the *mean matrix* $\Gamma^+$, not of the
inhibitory kernel $r_j$. The inhibition can be as weak or as fierce as one likes;
it only ever deletes children, never manufactures them.

**The coupling (discharges hypothesis (2)).** Define the majorant $\{Y_t\}$ on the
**same probability space**: pure excitation, no thinning. Each type-$i$ particle
in $Y_t$ spawns the *same* Poisson litters as it does in Stage 1 — we couple the
litter randomness identically per shared particle — and Stage 2 is simply skipped
for $Y$. Set $X_0 = Y_0$. Formally, couple the two populations by a
particle-matching that identifies each $X_t$-particle with its copy in $Y_t$ (valid
since $X_t \subseteq Y_t$) and assigns identical Poisson litters to matched
particles; unmatched $Y_t$-particles branch independently. This is the standard
subset coupling of exchangeable Poisson litters.

> **Invariant.** $X_t \subseteq Y_t$ as multisets (every $X$-particle is also a
> $Y$-particle) for all $t \ge 0$.
>
> *Proof by induction on $t$.* **Base:** $X_0 = Y_0$, so $X_0 \subseteq Y_0$.
> **Step:** suppose $X_t \subseteq Y_t$. Each particle shared by $X_t$ and $Y_t$
> produces, under the common coupling, an *identical* Poisson litter in both
> processes; the particles in $Y_t \setminus X_t$ produce additional $Y$-litters.
> Hence the pre-thinning excitatory offspring of $X_t$ is a sub-multiset of
> $Y_{t+1}$: writing $\tilde Y^X$ for the Stage-1 configuration generated from
> $X_t$, we have $\tilde Y^X \subseteq Y_{t+1}$. Stage-2 thinning then only
> *deletes* particles from $\tilde Y^X$ (each child is retained or killed; nothing
> is added), so $X_{t+1} \subseteq \tilde Y^X \subseteq Y_{t+1}$. $\;\square$

Because containment of multisets is entrywise count-domination, the invariant gives
$X_t \le Y_t$ **entrywise for all $t$**. This is exactly hypothesis (2)'s pathwise
domination $X_t \le Y_t$ under the natural coupling with $X_0 = Y_0$ — now a
**theorem of the construction**, not an assumption. Note where the thinning
realization does the work: Stage 2 *removes* children from a nonnegative count, so
mass can never go negative and $-\Gamma^-$ can never "re-add" mass; the pathology
that broke the continuous-linear model (§"Galton–Watson," part (d)) is structurally
absent because there is no continuous medium to drive negative.

**Conclusion.** $\{Y_t\}$ is a subcritical multitype Galton–Watson process with
mean-offspring matrix $\Gamma^+$ (Claim (a)); this is exactly the majorant process
of the existing proof sketch (§"The Monotone-Majorant Containment Lemma," part
(c)), which we do not re-prove. When $\rho(\Gamma^+) < 1$, that sketch gives
$\mathbb{E}[\mathbf 1^\top Y_t] = \mathbf 1^\top (\Gamma^{+\top})^t Y_0 \to 0$
geometrically ($\rho(\Gamma^{+\top}) = \rho(\Gamma^+)$, so the threshold is
unchanged), so the integer-valued $Y_t \to 0$ a.s. (extinction). By the squeeze
$0 \le X_t \le Y_t$ established above, $X_t \to 0$ a.s.: the signed cascade of the
EITB process is contained. Hypotheses (1) and (2) hold **as theorems** for this
dynamics, so the Monotone-Majorant Containment Lemma applies to it with no residual
posit — the hypothesis-class is nonempty, and obligation (i) is discharged.

**Two remarks — why this is the right object.**

1. *Robustness (the conclusion depends only on the mean matrix).* Poisson plays no
   essential role. Replace $\mathrm{Poisson}(\Gamma^+_{ij})$ by **any** offspring
   law with mean $\Gamma^+_{ij}$ and both Claim (a) and the coupling invariant are
   unchanged: (a) uses only $\mathbb{E}[K_{ij}] = \Gamma^+_{ij}$, and the coupling
   uses only that the parent's litter is shared and that Stage 2 deletes. A natural
   alternative is $K_{ij} \sim \mathrm{Bernoulli}(\Gamma^+_{ij})$, which is a valid
   law precisely because $\Gamma^+_{ij} \le 1$ — it is a difference of two
   probabilities, $\Pr[j \mid i] - \Pr[j] \le 1$. So containment is a property of
   $\Gamma^+$ as a *mean matrix*, invariant to the offspring distribution's higher
   moments.

2. *Repair of the linear defect.* The EITB process is the **nonnegative nonlinear
   realization** whose linearization is the defective continuous-linear model
   $X_{t+1} = \Gamma^+ X_t - \Gamma^- X_t$ that obligation (d) excluded. Take the
   canonical kernel $r_j = e^{-I_j}$ and read the *mean* update near the empty
   configuration. Since $I_j = (\Gamma^{-\top} X_t)_j$ is deterministic given $X_t$,
   $r_j = e^{-I_j}$ is constant given $X_t$, so the expected retained count at $j$ is
   $\mathbb{E}[X_{t+1,j} \mid X_t] = (\Gamma^{+\top} X_t)_j\, e^{-I_j}$ exactly (no
   $\mathbb{E}[e^{-I_j}]$ term — $I_j$ is not random given $X_t$); for
   small occupancy $e^{-I_j} \approx 1 - I_j = 1 - (\Gamma^{-\top} X_t)_j$, so
   $$
   \mathbb{E}[X_{t+1,j} \mid X_t]
   \;\approx\; (\Gamma^{+\top} X_t)_j \;-\; (\Gamma^{+\top} X_t)_j\,(\Gamma^{-\top} X_t)_j ,
   $$
   whose *first-order* (linear-in-$X_t$) term is $(\Gamma^{+\top} X_t)_j$ and whose
   inhibitory correction is the excitation mean scaled down by the inhibitory input
   — the $-\Gamma^-$ loss channel, entering as a suppression of the excitatory flow
   rather than a free-standing subtraction. (Honest scope: in this product form the
   inhibitory term is *second order* in $X_t$; it is a small-occupancy correction,
   and the signed map $\Gamma = \Gamma^+ - \Gamma^-$ is recovered as the leading
   excitatory operator *plus* this bilinear damping, not as a literal first-order
   difference of two linear maps — see the judgment note below.) The point stands
   qualitatively: EITB reproduces the intended excite-then-suppress structure of the
   signed model while staying nonnegative by construction, and so *fixes exactly*
   the mass-re-adding pathology (a driven-negative component flipping the sign of
   $-\Gamma^- X_t$) that made the continuous-linear model fail. It is the nonlinear,
   nonnegative object of which the defective linear model is the naive — and
   sign-unsafe — linearization.

## The asymmetric star, worked concretely

Make the whole apparatus concrete on the topology C387 already ran: an
asymmetric star with one anchor $a$ (strong model, low error rate $p_a$) and
$m-1$ satellites $s$ (weaker, higher error rate $p_s > p_a$), with excess
co-failure concentrated on the anchor→satellite links. Then
$$
\Gamma^+_{a \to s} \;=\; \Pr[s \text{ wrong} \mid a \text{ wrong}] - p_s
\;\;\gg\;\;
\Gamma^+_{s \to a} \;=\; \Pr[a \text{ wrong} \mid s \text{ wrong}] - p_a .
$$
The inequality is exactly the marginal-heterogeneity identity above, read on
$\Gamma^+$: because $p_a < p_s$, conditioning on the *rare* anchor failure moves
the satellite far more than conditioning on the *common* satellite failure moves
the anchor. The excitatory mass points *outward from the anchor*, and this is the
direction an undirected $\lambda_2$ cannot represent — it would symmetrize the two
links into one edge weight and report the same number whichever way the arrow
runs, precisely the C387 blindness. For a star whose excitatory couplings are
dominated by the anchor's out-row, $\rho(\Gamma^+)$ is governed by that row's mass;
the branching reading says a co-failure cascade ignites when the anchor's outward
excess-conditional couplings, summed over satellites, cross criticality — a
statement about the *anchor's outward influence* that the symmetric summary
structurally cannot make. (The estimation caveat below bites hardest exactly here:
the anchor's row is conditioned on the anchor being wrong, the rarest event on the
panel.)

## Weak joints — kept explicit, do not paper over

These are the load-bearing hedges. Each is a place where a plausible-sounding
stronger claim would be an overclaim, and the discipline is to name the weaker
true statement and stop.

1. **Full $\Gamma$ is signed ⟹ spectral radius only.** For the signed $\Gamma$ we
   may take $\rho(\Gamma) = \max_k|\lambda_k|$ and nothing more; Perron–Frobenius
   does *not* apply, so there is no guaranteed real positive dominant eigenvalue,
   no nonnegative eigenvector, and the word "Perron root" is **not** licensed for
   $\Gamma$. It is licensed for $\Gamma^+$ alone.

2. **$\rho(\Gamma) < 1$ as a full-system cascade gate is analogy, not theorem.**
   Only $\rho(\Gamma^+) < 1$ carries a proof — via Galton–Watson criticality of
   the majorant process — and even that is a *sufficient* condition for the signed
   system, established by a dynamical majorant argument, **not** by a spectral
   inequality $\rho(\Gamma^+) \ge \rho(\Gamma)$ (which is false in general: the
   standard Wielandt bound gives $\rho(\Gamma) \le \rho(|\Gamma|)$ and
   $\rho(\Gamma^+) \le \rho(|\Gamma|)$, both pointing away from what we would need).
   A criticality statement for the *signed* $\rho(\Gamma)$ itself is not
   established here.

3. **The propagation dynamics is a modeling choice — now realized explicitly
   (obligation (i) discharged).** The Galton–Watson reading — and with it the
   majorant argument underpinning the sufficient condition — requires an explicit
   generating dynamics: a rule for how a co-failure impulse at one agent propagates
   to others, under which (a) $\Gamma^+$ is the mean-offspring matrix and (b) the
   $\Gamma^+$-only process dominates the signed process. The **EITB process** of
   §"An explicit dynamics" now supplies exactly such a rule, and makes (a) and (b)
   **theorems** of the construction rather than posits — so the hypothesis-class of
   the lemma is demonstrably nonempty. The residual hedge is honest and narrow: this
   exhibits *one* consistent dynamics, it does **not** assert the real co-failure
   system is governed by it. Different dynamics could still break either the
   branching interpretation or the domination; the lemma is therefore properly read
   as *conditional on a thinning–branching dynamics of the EITB kind*, and what
   §"An explicit dynamics" settles is that such a dynamics exists and that the two
   hypotheses are jointly realizable — not that the panel must obey it.

4. **The C387 spectral identity is still analogy-only.** As in the earlier draft:
   whether $\Gamma^+$'s Perron structure coincides with Chung's
   directed-Laplacian-under-$\pi$, or merely shares the shape, must be argued from
   the definitions. The motivation transfers with certainty; the machinery only on
   condition.

## Precedent, novelty, and one hazard

The machinery — a directed matrix summarized by a spectral cascade gate — has a
precedent in arXiv 2606.20493, which builds this kind of directed spectral gate and
reports $\rho = 1.296$. But its estimand is **preference drift** (an $L^2$
weight-shift between evaluator rounds), **not co-failure**. The number 1.296 must
**not** be imported as a co-failure datapoint: it measures a different quantity, and
even on its own terms the per-link effect was not significant ($p = 0.589$), so it
is the $\rho > 1$ *regime* that survives there, not the coefficient. Right
machinery, wrong estimand — the same relationship this section has to that paper.

Two nearer papers sharpen the boundary rather than crossing it. arXiv 2603.04474
("Spark to Fire") does carry a directed matrix and a spectral-radius gate
($\beta\,\rho(A) > \delta$), but its $A$ is the binary *communication-adjacency*
matrix and its estimand is *error propagation* through a message-passing pipeline
— one agent's false claim contaminating a downstream agent's context — not the
conditional co-failure of agents erring independently on the same input.
arXiv 2606.27288 has the co-failure estimand ($\beta$, $\bar\rho$, a Gaussian
copula) but is *entirely symmetric*: no directed matrix, no Perron root.

So the specific object — a **directed, conditional-excess co-failure matrix
$\Gamma$, split into a nonnegative excitatory part $\Gamma^+$ carrying a genuine
Perron root and a branching-process criticality gate** — appears unclaimed
(novelty search, 2026-07-29; confidence ~80%). What exists is the machinery
(directed spectral gates for drift and for propagation) and the estimand (symmetric
co-failure statistics), but not their composition, and not with the $\Gamma^+$
decomposition that makes the criticality reading exact.

## Open questions

- **Estimation.** $\Gamma$ needs the conditional $\Pr[j \mid i]$, which needs
  enough *$i$-wrong* events to estimate. For a strong anchor with a low error rate,
  the conditioning event is rare and $\Gamma_{i\cdot}$ is the noisy row — the
  finite-sample behavior is worst exactly where the anchor is, which is the row we
  most care about, and the row that dominates $\rho(\Gamma^+)$ in the asymmetric
  star. A shrinkage / minimum-support treatment is needed before any
  $\rho(\Gamma^+)$ estimate is trustworthy.
- **The propagation dynamics — DISCHARGED (obligation (i)).** Posited explicitly as
  the **EITB process** (§"An explicit dynamics"): its excitation stage has
  $\Gamma^+$ as mean-offspring matrix (Claim (a)) and its thinning stage yields the
  pathwise domination $X_t \le Y_t$ (coupling invariant) — both as theorems, not
  posits. The gate is therefore conditional on a thinning–branching dynamics *of
  this kind* rather than on the unproved existence of any such dynamics; the
  hypothesis-class is nonempty. It remains a modeling choice that the real panel
  need not obey — the discharge is realizability, not identification.
- **The transfer gate.** Does $\Gamma^+$'s Perron structure actually coincide with
  Chung's directed-Laplacian-under-$\pi$, or is the C387 correspondence analogy-only?
  This must be argued from the definitions, not assumed from the shared shape.
- **Reduction to Leg 1.** Under equal marginals $\Gamma$ is symmetric; it should
  then reduce to (a function of) the symmetric joint-tail object Leg 1 already
  reports. Verifying that limit is the consistency check that keeps the directed
  companion honest as a *companion* rather than a rival.
