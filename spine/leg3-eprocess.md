---
status: DRAFT SCAFFOLD — Lyra, 2026-08-02, Leg-3 body for the three-leg joint paper (JUDGe-2026)
section: Leg 3 — the anytime-valid co-failure monitor (e-process SLA)
note: This is a scaffold — construction, structure, and honest gap-flags, not a final polished draft.
      All numbers marked ⟦from simulation…⟧ are indicative and pending revalidation on the RoPoLL testbed.
      All ⟦CITE⟧ / ⟦GAP⟧ markers are load-bearing TODOs, not decoration.
---

> **Terminology, pinned here for the whole paper (this is the object the $\Omega_{\mathrm{blind}}$
> subsection defers to).** The per-step bet $e_s = 1 + \lambda(U_s - V_s)$ satisfies
> $\mathbb{E}[e_s \mid \mathcal{F}_{s-1}] = 1$ under the *exact* null (§3) — a **martingale**
> increment — and $\mathbb{E}[e_s \mid \mathcal{F}_{s-1}] \le 1$ once the $\delta_k$
> drift-slack of §5 is subtracted, with $e_0 = 1$ and $e_s \ge 0$ throughout. So the running
> product $M_t = \prod_{s \le t} e_s$ is a **nonnegative martingale under the exact null**
> (a *test martingale*, since $M_0 = 1$), demoted to a **nonnegative supermartingale** (a
> *test supermartingale*) precisely by the $\delta_k$ slack under approximate stratification —
> which is all Ville needs. The process $\{M_t\}_{t\ge 0}$ —
> equivalently its Robbins mixture over $\lambda$ — is an **e-process**. By **Ville's inequality**,
> $\mathbb{P}\big(\sup_t M_t \ge 1/\alpha\big) \le \alpha$ under $H_0$, which is the operational,
> anytime-valid level-$\alpha$ test (the SLA). An **e-value** is the value $M_\tau$ at any stopping
> time $\tau$, with $\mathbb{E}[M_\tau] \le 1$ by optional stopping. We use these four terms in
> exactly these senses throughout; the $\Omega_{\mathrm{blind}}$ subsection's terminology
> header is reconciled to this definition.

# Monitoring the collapse: an anytime-valid co-failure e-process

## 1. The diagnostic is settled; the monitor is not

Start with what the field now agrees on. Across judge panels and model panels, the
*effective number of independent voters* collapses. Where a naive count would report
$m$ nominally distinct judges, the co-failure–deflated count saturates at
$n_{\mathrm{eff}} \approx 2$, rarely climbing past $2$–$3$ no matter how many members
are added. This is the Kish/Kohli effective-sample-size applied to the failure axis:
given a mean pairwise co-failure correlation $\bar\varphi$, the panel's effective size
deflates as $n_{\mathrm{eff}} = m / \big(1 + (m-1)\bar\varphi\big) \to 1/\bar\varphi$ for
large $m$ — a $1/\bar\varphi$-type ceiling, not a linear return on membership
⟦CITE — needed: Kohli (Leg-1 primary); Kish effective sample size⟧. Concretely, Kohli
measures $n_{\mathrm{eff}}$ falling from $\approx 2.18$ to $\approx 1.93$ across judge
panels ⟦CITE: Kohli 2605.29800⟧: **the collapse of effective panel size is the established
diagnostic, established by Leg 1.**

⟦GAP for Claudius: the deleted "two labs, one stylized fact" move needs an HONEST second
independent $n_{\mathrm{eff}}$ landing. Best primary-verified candidate = Shu et al.
2608.06940, "Blind to the Pivotal Vote": panel $n_{\mathrm{eff}} \approx 2.61$, SAME
judge-panel domain, restates Kohli's "nine judges $\approx$ two." Second candidate =
Begin 2606.26583 (DPO $n_{\mathrm{eff}}$ 1.38–2.19) but that is prediction-market
forecasting, NOT judge panels — domain caveat. The former RoPoLL numbers
($\bar\gamma_W \in [0.45,0.53]$, $N \approx 2$–$3$) were fabricated — not in the paper,
traced to an un-verified browse note — and are REMOVED, not replaced. Pick the framing.⟧

What *nobody does* is monitor the collapse as it happens. The prior art is batch. Han's
de Finetti cascade gives a fixed-sample reliability ceiling ⟦CITE: Han 2607.13918⟧; Li &
Hai derive a state-dependent copula floor on co-failure, batch, via a train/test (odd/even index) split
⟦CITE: Li & Hai 2607.23931⟧. The
one streaming instrument in the neighborhood — Xie's sequential monitor
⟦CITE: Xie 2606.07624⟧ — watches *marginal* scalars, one stream at a time: it can tell
you that judge $i$'s fail-rate is drifting, but it says nothing about whether $i$ and $j$
are drifting *together*. Every existing object is either batch or marginal.

Our contribution is precisely the cell those two axes leave empty: **a second-order,
anytime-valid monitor of the dependence channel itself.** Not the marginals — the
*co-failure between* two streams, tracked sequentially, with a false-alarm guarantee
that holds at every stopping time and under a null whose nuisance parameters (the
marginal fail-rates) are allowed to drift arbitrarily. By the third paragraph the
novelty should already be legible: the diagnostic quantity is $n_{\mathrm{eff}}$
(equivalently $\bar\varphi$), and the monitor is a betting process on an *observed*
co-failure baseline that we now construct.

## 2. The null, and the naive-plug-in trap

Fix two judges (or two models) $i, j$. On item $s$ let $W_i^s \in \{0,1\}$ indicate that
judge $i$ *fails* on item $s$. The marginal fail-rates $p_i, p_j$ are **unknown** and
**drift** along the stream — this is not a technical convenience, it is the empirical
regime (judges degrade, prompts shift, difficulty is non-stationary). The composite null
is the natural one:
$$
H_0:\quad \text{conditional on the stream filtration } \mathcal{F}_{s-1},\ \
W_i^s \perp\!\!\!\perp W_j^s \ \text{within item } s,
\qquad\text{i.e. } \mathbb{E}[W_i^s W_j^s \mid \mathcal{F}_{s-1}] = p_i^s\, p_j^s .
$$
Co-failure equals the product of marginals; any excess is the signal we hunt.

The obvious construction is a Ville-style betting skeleton. Let $Z^t$ be the observed
same-item co-failure indicator and $m_t$ the predicted baseline product; bet
$$
e_t = 1 + \lambda_t\,(Z^t - m_t).
$$
This is textbook-valid *if $m_t$ is known*: then $\mathbb{E}[e_t \mid \mathcal{F}_{t-1}]
= 1 + \lambda_t(\mathbb{E}[Z^t] - m_t) = 1$ under $H_0$, and the product is a test
martingale. But $m_t = p_i^s p_j^s$ is exactly the drifting nuisance we do not know. Any
*predictable plug-in* $\hat m_t$ — a running estimate formed from $\mathcal{F}_{t-1}$ —
that systematically *underestimates* the drifting baseline makes
$\mathbb{E}[e_t \mid \mathcal{F}_{t-1}] = 1 + \lambda_t(m_t - \hat m_t) > 1$ under $H_0$.
The wealth process drifts up with no signal present, and Ville's inequality is voided:
the test rejects a true null. In simulation this is not a marginal effect —
a plug-in monitor under drifting marginals produced a **false-reject rate of $\approx 90\%$**
⟦from simulation, to be revalidated on the RoPoLL testbed⟧.

This is worth naming precisely, because it is the paper's recurring failure mode wearing
a new coat: **it is an estimand-substitution failure.** The bet is honest — it is a true
bet on a co-failure excess — but it is placed against a *mis-estimated* baseline, so the
quantity actually being tested is not the co-failure excess but "co-failure excess plus
plug-in bias." A true wager on the wrong estimand. The rest of this section is the
construction that removes the estimation entirely, so there is no baseline to
mis-estimate.

## 3. The discharge: cross-item pairing gives an *observed* baseline

The claim of this section is that the cross-item pairing bet is not an ad-hoc device but
the **canonical, complete-class-optimal e-variable** for the $K$-stratum co-failure null
⟦CITE: 2606.06769⟧. The contribution is the *construction*: cross-item pairing ($s \ne t$)
yields a **margins-free observed baseline** $V$ with $\mathbb{E}[V] = a\cdot b$ *without any
estimation* — precisely the object that SKCI, Kuai, and every other monitor in the
neighborhood must instead fit or estimate. Clerico's complete-class theorem then enters only
as an **optimality certificate**: it tells us this natural, estimation-free object is also
optimal-in-class, and nothing more. We build $V$ (the margins-free baseline), read off
$(\Phi, S, \sigma)$, and identify the result as Clerico's canonical affine member; optimality
is then immediate.

Work within a *stratum* — a block of items on which both marginals are approximately
constant, $p_i \approx a$ and $p_j \approx b$. (Section 5 makes "approximately" precise
and pays for it.) Pick two distinct items $s \ne t$ in the stratum and form two
statistics:
$$
U \;:=\; W_i^s \, W_j^s
\qquad\text{(same-item co-failure — carries the within-item dependence, if any),}
$$
$$
V \;:=\; W_i^s \, W_j^t
\qquad\text{(cross-item product — judge $i$ on item $s$, judge $j$ on a *different* item $t$).}
$$
The whole construction turns on one observation. Because $s \ne t$, the indicators
$W_i^s$ and $W_j^t$ come from *different items*, and are therefore independent
**regardless of any within-item dependence structure** — the within-item coupling that
$H_0$ is about simply cannot reach across two different items. Hence
$$
\mathbb{E}[V \mid \mathcal{F}] \;=\; \mathbb{E}[W_i^s]\,\mathbb{E}[W_j^t] \;=\; a\cdot b
\qquad\textbf{exactly.}
$$
$V$ is an **observed, margins-free baseline for the product $a b$**: it estimates the
independence baseline *without estimating $p_i$ or $p_j$ anywhere*. No plug-in, no running
mean of the marginals, no predictable nuisance — the baseline is a directly observed
random variable with the correct expectation by construction. This is what closes the
trap of §2: there is nothing left to mis-estimate.

**The one structural fact that carries the whole guarantee.** The baseline $V$ is an
*observed product, never an estimate*: $\mathbb{E}[V \mid \mathcal{F}_{k-1}] = a\cdot b$
holds **exactly** by cross-item independence ($W_i^s \perp\!\!\!\perp W_j^t$ for $s \ne t$),
for **any** marginals $a, b$ — including drifting ones. Because $a\cdot b$ cancels
*symbolically* in the martingale identity $\mathbb{E}[e \mid \mathcal{F}_{k-1}] = 1$, no
marginal probability is ever formed as a number. This single structural fact delivers
**both** finite-sample validity (no concentration or consistency assumption) **and**
robustness to drifting marginals — they are one property, not two. Everything below is
bookkeeping on this one cancellation.

**The bet — assembling the canonical member.** With the observed baseline in hand, wager
$$
\boxed{\,e \;=\; 1 + \lambda\,(U - V), \qquad \lambda \in [0,1].\,}
$$
This is exactly the shape of Clerico's canonical affine one-step e-variable, and the data
it needs are now all in hand: the score is $\Phi = U - V$, its support is
$S = [-2\varepsilon, 2\varepsilon]$, whose half-width is the drift slack $\delta_k = 2\varepsilon$ that §5 derives from the within-stratum marginal radius $\varepsilon$, and its support
function is $\sigma(\lambda) = 2\varepsilon|\lambda|$. Reading off Clerico's admissibility
set $\Lambda_{\Phi,S}$ from these data gives **both** admissible ranges at once. For the
**exact-null bet** ($\delta_k = 0$, the stratum-constant case) the only binding constraint is
nonnegativity of $e$, which holds on $\lambda \in [0,1]$. For the **drift bet**
($\delta_k = 2\varepsilon$, §5) admissibility is
$1 + \lambda(U - V) \ge \sigma_{\Phi,S}(\lambda) = 2\varepsilon|\lambda|$, solved at the worst
case $U - V = -1$, which gives $\lambda \in [0, 1/(1+2\varepsilon)]$.

*Nonnegativity.* $U, V \in \{0,1\}$, so $U - V \in \{-1, 0, 1\}$, hence
$e \in [1-\lambda,\, 1+\lambda] \subseteq [0, 2]$ for $\lambda \le 1$. In particular
$e \ge 0$, so the running product is a genuine nonnegative wealth process. ✓ The drift-bet
range is strictly tighter because the subtracted slack eats into the margin. By a second,
direct route: at $\lambda = 1$
the outcome $U = 0, V = 1$ gives $e = 1 - (1 + 2\varepsilon) = -2\varepsilon < 0$, so
$\lambda = 1$ is inadmissible under drift and the range shrinks to
$[0, 1/(1+2\varepsilon)]$ — matching the admissibility computation above.

*Validity under $H_0$.* Within-item independence gives $\mathbb{E}[U \mid \mathcal{F}]
= a b$, and the cross-item argument gives $\mathbb{E}[V \mid \mathcal{F}] = a b$. The two
baselines coincide, so
$$
\mathbb{E}[e \mid \mathcal{F}] \;=\; 1 + \lambda\big(\mathbb{E}[U \mid \mathcal{F}]
- \mathbb{E}[V \mid \mathcal{F}]\big) \;=\; 1
\qquad\textbf{exactly, for every } \lambda \in [0,1].
$$
So under the *exact* null — A1 cross-item independence, A2 stratum-constant marginals, and
within-item independence — the increment is a **martingale** increment, not merely a
supermartingale one: $\mathbb{E}[e_k \mid \mathcal{F}_{k-1}] = 1$. Started at $e_0 = 1$, the
product $M_t = \prod_{s \le t} e_s$ is a **nonnegative test martingale**. It is only the
$\delta_k$ slack under *approximate* stratification (finite strata whose marginals match
within $\varepsilon$, see §5) that demotes it to a **supermartingale**,
$\mathbb{E}[e_k \mid \mathcal{F}_{k-1}] \le 1$ — which is all Ville needs. Either way it is
an e-process, and Ville's inequality delivers the anytime-valid SLA:
$\mathbb{P}(\sup_t M_t \ge 1/\alpha) \le \alpha$.

*Ville validity conditions.* This anytime-valid guarantee is not automatic; it holds only
under the following four conditions, stated explicitly because each is load-bearing:
1. **Predictability.** Each bet $\lambda_k$ is $\mathcal{F}_{k-1}$-measurable — it may not
   depend on the current increment's data $(U_k, V_k)$. A bet tuned to the increment it
   wagers on breaks the martingale property.
2. **Bounded bet $\lambda_k \in [0,1]$.** This is load-bearing for nonnegativity $e_k \ge 0$:
   if $\lambda_k > 1$ then the outcome $U = 0, V = 1$ gives $e_k = 1 - \lambda_k < 0$, the
   wealth process can go negative, and Ville's guarantee breaks. (Under the drift null,
   further restricted to $\lambda \in [0, 1/(1+2\varepsilon)]$; see above.)
3. **Within-item null per increment.** The within-item independence null
   $\mathbb{E}[U_k \mid \mathcal{F}_{k-1}] = a b$ holds at each increment $k$.
4. **Disjoint pairs and global A2.** The item-pairs across increments are disjoint /
   independent, *and* A2 (stratum-constant marginals) holds **globally across all paired
   items, not merely within a single pair**. Otherwise the two-sided drift bias of §5
   accumulates across increments, $\mathbb{E}[P_n]$ can exceed $1$, and Ville is violated.

*Removing $\lambda$ (Robbins mixture).* The tuning parameter $\lambda$ trades power for
robustness and there is no oracle value. Rather than pick one, mix: place a prior
$\mu(\mathrm{d}\lambda)$ on $[0,1]$ and integrate the wealth,
$$
\bar M_t \;=\; \int_0^1 \Big(\textstyle\prod_{s\le t}\big(1 + \lambda(U_s - V_s)\big)\Big)\,\mu(\mathrm{d}\lambda),
$$
a mixture of e-processes, hence itself an e-process — the mixture is where the tuning
disappears and the guarantee survives. Indicative operating numbers, to be treated as
*pending*, not established: $\approx 0.1\%$ false-reject and $\approx 68\%$ power at a
co-failure excess of $r = 0.4$ ⟦from simulation, to be revalidated on the RoPoLL
testbed⟧.

**What kind of object this is.** The construction is the sequential-betting analogue of a
**permutation test for independence.** $V$ is the "permuted" statistic — the same-item
pairing $W_i^s W_j^s$ with one index shuffled to a different item, which under $H_0$ has
the identical expectation and destroys any within-item coupling — and $U$ is the observed
same-item statistic. Betting on $U - V$ is betting that the observed pairing beats its own
permutation, adjudicated online and at any stopping time rather than against a fixed
reference distribution.

**Optimality of the form.** We have now assembled exactly Clerico's canonical affine member
— $\Phi = U - V$, support $S = [-2\varepsilon, 2\varepsilon]$, support function
$\sigma(\lambda) = 2\varepsilon|\lambda|$ — and its complete-class theorem ⟦CITE: 2606.06769⟧
therefore certifies the construction as optimal-in-class for the $K$-stratum null we test:
any e-process for a null defined by finitely many conditional-moment constraints is
dominated, at every stage, by a predictable product of affine one-step e-variables, and ours
*is* that dominating affine member. The drift bet coincides exactly with Clerico's canonical
affine e-variable $e_\lambda = 1 + \lambda\Phi - \sigma_{\Phi,S}(\lambda)$: the slack
$\delta_k = 2\varepsilon$ *is* the support function $\sigma_{\Phi,S}$ itself, not an ad-hoc
robustness margin.

Three scope notes keep this honest:

(i) *Horizon-clean.* The domination is stagewise, not asymptotic — it carries no
infinite-horizon assumption. The $\infty$-stages caveat belongs to the *size* question
(log-optimal Kelly tuning), which we decline; see §5.

(ii) *Scope, not suboptimality.* Optimality is for the finite $K$-stratum null actually
tested; the continuous-difficulty ideal is a refinement of the *null* — a discretization
away — not a stronger optimality we forgo.

(iii) *One-sided by design, not by restriction.* Clerico's admissible class $\Lambda_{\Phi,S}$
places no sign constraint on $\lambda$; for our two-sided drift null ($S = [-2\varepsilon,
2\varepsilon]$) it is the symmetric set $\{\lambda : 1 + \lambda(U - V) \ge 2\varepsilon|\lambda|\}$,
which contains negative $\lambda$. We use only $\lambda \ge 0$ because our *alternative* is
one-sided (excess co-failure): a negative-$\lambda$ bet is admissible but power-optimal
against the benign anti-co-failure alternative we do not monitor, so excluding it costs no
power against excess co-failure. On the $\lambda \ge 0$ side, admissibility gives the
admissible range computed above.

## 4. Where this sits relative to $\Omega_{\mathrm{blind}}$ and Leg 2

The $\Omega_{\mathrm{blind}}$ subsection uses Han's batch de Finetti ceiling as the
*structural twin* of this streaming monitor and is careful never to import Han's numbers
into the streaming estimand. This section supplies the streaming object that twin is a
twin *of*: the per-pair co-failure e-process defined in §3. The serial-to-parallel
transfer flagged there — whether the streaming residual inherits Han's batch exponent $b$
— remains open and is *not* discharged here; §3 constructs the monitor, it does not claim
Han's ceiling transfers to it.

The link to Leg 2 is deliberately kept **qualitative**, matching the scope fixed in
$\Omega_{\mathrm{blind}}$. An $H^1$-informed prior may up-weight *which pairs to monitor*
— steering the betting toward pairs the Leg-2 obstruction class flags as coupled — but
this is a prior on *where to bet*: it affects power, never validity, and enters no bound.
No quantitative $H^1$-weighting formula appears in this section, and none should; if one
ever does, it re-opens the scope question flagged in $\Omega_{\mathrm{blind}}$. We claim
the co-failure estimand and a qualitative cohomological framing of *where* to spend
statistical power; we do not claim any quantitative cohomological bound on the e-process.

## 5. The open piece: per-stratum slack $\delta_k$

The one place the construction spends an assumption is the stratification, and honesty
requires stating exactly what it buys and what it still owes. Real strata match marginals
only *approximately*, and the resulting bias is **two-sided** — this is the subtle point
that determines how the slack must be sized. Suppose within a stratum judge $j$'s marginal
drifts between the two paired items, $\mathbb{P}(W_j^s = 1) = b_s$ and
$\mathbb{P}(W_j^t = 1) = b_t$, while within-item independence still holds exactly. Writing
$a$ for judge $i$'s marginal, the per-increment bias is
$$
\mathbb{E}[e] - 1 \;=\; \lambda\,a\,(b_s - b_t),
$$
whose **sign matches $\operatorname{sign}(b_s - b_t)$ and can therefore be either sign** —
it is not one-sided. When $b_s > b_t$ the bias pushes $\mathbb{E}[e]$ *above* $1$,
manufacturing a spurious co-failure alarm out of pure marginal drift; when $b_s < b_t$ it
pushes below. The magnitude bound is tight:
$$
\big|\mathbb{E}[e] - 1\big| \;=\; \lambda\,a\,|b_s - b_t| \;\le\; 2\lambda a\varepsilon \;\le\; 2\varepsilon,
$$
using $|b_s - b_t| \le 2\varepsilon$ (both within $\varepsilon$ of the stratum center) and
$\lambda, a \le 1$, where $\varepsilon$ is the within-stratum marginal radius.

Because the bias can be *positive*, the slack $\delta_k$ is **not a passive correction**:
it must be sized to *dominate the worst-case positive excursion*, not merely to absorb a
one-signed offset. Set
$$
e \;=\; 1 + \lambda\big(U - V - \delta_k\big), \qquad \boxed{\,\delta_k = 2\varepsilon\,,}
$$
subtracting $\delta_k$ from the bet so that $\mathbb{E}[e \mid \mathcal{F}] \le 1$ holds
conservatively against the worst-case positive drift. Equivalently, pair only items whose
marginals are *provably* within $\varepsilon$. Either way the supermartingale property is
restored at a cost in power proportional to $\delta_k$.

The admissible range for the drift bet is $\lambda \in [0, 1/(1+2\varepsilon)]$ — the range
derived in §3 from Clerico's admissibility set — not the $[0,1]$ of the exact-null bet. For
small $\varepsilon$ it shaves only an $O(\varepsilon)$ sliver off the top of the range
($1/(1+2\varepsilon) \approx 1 - 2\varepsilon$).

**The paper adopts the $a$-free worst-case slack $\delta_k = 2\varepsilon$.** It uses only
the chosen radius $\varepsilon$ and the worst-case bounds $\lambda, a \le 1$ — no marginal
appears in it — and *this is exactly why we adopt it*: being marginal-free, it preserves the
§3 estimation-free guarantee end-to-end.

*Rider — what $\delta_k = 2\varepsilon$ does NOT give.* The size of $\delta_k$ is the
worst-case margins-free slack derived above; it does not come from, and is not log-optimal in
the sense of the GRO (Growth-Rate Optimal) e-process class characterised by ⟦CITE: Grünwald, de Heide & Koolen, "Safe Testing", JRSS-B 86(5) pp. 1091–1128 (2024), arXiv:1906.07801 — GRO defined §2.1, GROW defined §3⟧. The GRO framework supplies no constructive
Kelly fraction for few-strata settings: its log-optimality explicitly assumes $\infty$ stages, which is the
wrong regime here, as Brannath–Fischer ⟦CITE: 2606.00878⟧ (an equivalence result between confirmatory adaptive designs and anytime-valid sequential e-value tests) makes clear in its background gloss on log-optimality. $\delta_k = 2\varepsilon$ stands as a robust, exact, margins-free
commitment; any GRO refinement would require a large-strata
assumption and is not adopted here.

*Honesty riders on the §3 optimality claim.* The complete-class optimality established in §3
is precise but bounded in scope, and two open directions are worth naming explicitly here.
First (§3, scope note (ii)): the optimality claim is for the finite $K$-stratum null we
actually test; the continuous-difficulty ideal is a discretization refinement of the *null
itself* — a better stratification would shrink $\varepsilon$, narrowing $S$, but that is a
refinement of what is being tested, not a failure of optimality within the stated null.
Second (§3, scope note (iii)): the complete-class statement is for the $\lambda \ge 0$
family; whether the dominating e-variable ever requires $\lambda < 0$ remains open, and the
two-sided extension is not claimed.

The tighter bound $\delta_k = 2\lambda a\varepsilon$
is **not adopted**, despite its constant-factor power gain, because it embeds the marginal
$a$: forming it as a number requires estimating $a$, which reintroduces marginal estimation
through a side door and sacrifices the exact-baseline property that §3's whole construction
exists to secure. We trade a constant factor of power for keeping the baseline exactly
observed. The gain is not worth reopening the §2 trap.

This is a **defensible bound, not a structural hole** — the bias is bounded (by $2\varepsilon$)
and removable by a slack whose size we can name — but precisely because it is two-sided the
slack must dominate the positive excursion rather than cancel a known offset. With the
*constant* now committed to the $a$-free $\delta_k = 2\varepsilon$, what remains genuinely
open is the *granularity*: choosing the block size too coarse makes $\varepsilon$ large and
throws away power, too fine leaves strata with too few items to pair, and the optimal
stratification granularity (how finely to block the stream so that $\varepsilon$ is small but
strata still contain enough items to pair) is a design question we have not closed.

⟦GAP: choose the stratification granularity, and clear the adaptive-$\varepsilon$ risk.
The slack *constant* is settled — the paper commits to the $a$-free $\delta_k = 2\varepsilon$
and deliberately declines the tighter $\delta_k = 2\lambda a\varepsilon$, which would embed
the marginal $a$ and reintroduce marginal estimation, forfeiting §3's exact-baseline
property for a constant-factor gain. Open sub-questions: (i) [FLAGGED OPEN RISK — not
adopted] an adaptive stratification that estimates $\varepsilon$ per block from data; this
is *itself estimation*, so before it can be used it must be shown not to resurrect the §2
plug-in trap — treat as an open risk, never as part of the committed construction; (ii) a
power accounting for the $\delta_k = 2\varepsilon$ penalty against the $r = 0.4$ operating
point.⟧

## 6. The unification: cross-item pairing *is* Barber–Candès–Ramdas conditional validity

Two threads that entered from different doors turn out to be the same requirement. The
cross-item pairing of §3 is valid **iff** the two paired items $s, t$ share the same
marginals $(p_i, p_j)$ — that is the exact condition under which $\mathbb{E}[V] = ab$ and
$V$ is an observable baseline. Independently, calibrated anytime-valid coverage for a
composite null of this shape holds **iff** one conditions on the covariate that indexes
the nuisance — the Barber–Candès–Ramdas conditional-validity requirement
⟦CITE: Barber–Candès–Ramdas–Tibshirani 1903.04684⟧. These are not two assumptions that
happen to co-occur; they are one assumption seen from two sides. The stratum is the
conditioning event; matching marginals within a stratum is both what makes $V$ an
observable baseline *and* what makes the coverage conditionally valid.

> *The stratification condition that makes the baseline observable is identically the
> condition under which calibrated coverage holds.*

The *mai nafka minah* — the practical difference this identity buys — is that the
stratification is not a modeling convenience we could relax with more cleverness; it is
forced by BCR from the validity side and forced by estimability from the construction
side, and any attempt to drop it fails on both axes at once. That is why §5's slack is an
honest open piece and not a removable inconvenience: BCR tells us the conditioning cannot
be conditioned away for free.

## 7. Related work: non-partitioned changepoint detection (Saha–Ramdas 2607.28322)

Saha & Ramdas, "Non-partitioned e-detectors for nonparametric sequential change detection" (arXiv:2607.28322, 30 Jul 2026), build an anytime-valid e-detector for the **single-stream** setting where *both* the pre- and post-change distributions are unknown and share a composite class (no pre-specified P₀/P₁ partition). Primitives are REGROW e-processes aggregated Shiryaev–Roberts-style; a "countable local REGROW witness basis" (their Def. 6.8) supplies the regularity that replaces global weak-compactness. Weights choose ARL vs. PFA control.

**Relation to Leg-3.** This is the nearest anytime-valid *changepoint* machinery, and its non-partitioned assumption removes exactly the pre/post-distribution knowledge we lack under drifting, unknown marginals. Two scope caveats keep it honest:
- It monitors a **scalar change in one stream** — it does *not* detect dependence, and it is not joint/second-order across streams. Our per-pair co-failure object is a different problem; the cross-item-pairing e-process remains the core Leg-3 deliverable and Saha–Ramdas does not replace it.
- The exact all-start detector is **O(t) memory / quadratic total cost** (constant per-start cost needs a fixed portfolio) — it is *not* the O(1) construction (that is the Rao–Blackwellized streaming e-process, 2607.21958; do not conflate).

**Candidate extension (novelty UNVERIFIED — gate before claiming).** Running a non-partitioned e-detector on the per-pair bet increment (U − V) as its observation stream would monitor the *onset* of co-failure drift. Whether a dependence-changepoint monitor of this kind is unclaimed in the literature has not been verified; treat as future work until a citation search clears it.

## 7.1. Closest competitors: conditional-independence co-failure tests

The table below positions Leg-3 against the two methods with the tightest thematic overlap.

| Method | Estimand | Anytime-valid (Ville)? | Marginals | Cross-item pairing | Drift-robust? |
|---|---|---|---|---|---|
| SKCI — He & Sutherland ⟦CITE: 2606.18993⟧ | conditional independence | yes | CME estimate | no | — |
| Kuai ⟦CITE: 2604.07650⟧ | co-failure given difficulty | **no** — batch (permutation + MC), no Ville inequality | logistic fit $p_m(d)$ | no | no |
| **Ours (JUDGe Leg-3)** | co-failure given difficulty | yes | margins-free (matched via pairing) | yes ($V = W_i^s \cdot W_j^t$) | yes |

Kuai ⟦CITE: 2604.07650⟧ is our closest competitor — the same conditional-independence-given-difficulty co-failure null on real panels (18 models, MMLU-Pro) — but it is a *batch* procedure (permutation + Monte-Carlo), **with no Ville inequality and hence no anytime-valid guarantee**. Its "Cumulative Information Gain" is a sum over a fixed sample, not a sequential statistic. SKCI (He & Sutherland, ⟦CITE: 2606.18993⟧) is anytime-valid but tests conditional independence via an estimated conditional-mean embedding, where our baseline is margins-free by construction.

## Citations owed — ⟦CITE — needed⟧

*(Do not fabricate. Verify each from primary before this section is load-bearing in
submission. arXiv IDs inlined above are collected here; author/year references still need
full bibliographic entries.)*

**Betting / e-values / game-theoretic probability**
- ⟦CITE⟧ Shafer, "Testing by betting" (JRSS-A, 2021).
- ⟦CITE⟧ Shafer & Vovk, *Game-Theoretic Foundations for Probability and Finance* / e-values (2019).
- ⟦CITE⟧ Robbins mixture — the mixture-martingale construction ⟦needed: canonical reference for the $\lambda$-mixture; likely Robbins 1970 / Howard–Ramdas–McAuliffe–Sekhon time-uniform bounds 1808.03204⟧.
- ⟦CITE⟧ Ville's inequality — ⟦needed: primary or a standard game-theoretic-probability restatement⟧.

**Conditional validity**
- ⟦CITE: Barber–Candès–Ramdas–Tibshirani 1903.04684⟧ (conditional coverage / the identity in §6).

**The diagnostic and the batch prior art**
- ⟦CITE: Han 2607.13918⟧ (de Finetti reliability ceiling; batch — the $\Omega_{\mathrm{blind}}$ twin).
- ⟦CITE: Li & Hai 2607.23931⟧ (state-dependent copula floor; batch).
- ⟦CITE: Xie 2606.07624⟧ (sequential monitor of *marginal* scalars, one stream at a time).
- ⟦CITE: Kohli 2605.29800⟧ ("Nine Judges, Two Effective Votes"; Leg-1 primary; $n_{\mathrm{eff}} \approx 2$ on $\bar\varphi$).

**N-version / common-cause failure lineage (the reliability-engineering roots of co-failure)**
- ⟦CITE⟧ Knight & Leveson (1986), "An experimental evaluation of the assumption of independence in multiversion programming."
- ⟦CITE⟧ Brilliant, Knight & Leveson (1990), correlated failures in N-version programming.
- ⟦CITE⟧ Mosleh, common-cause failure alpha-factor model (CCF reliability).

**Portfolio / response-diversity analogue (outside AI)**
- ⟦CITE⟧ Schindler et al. (2015), response diversity / the portfolio effect in ecology.

⟦GAP: cross-check that every arXiv ID above is verified from primary (Han 2607.13918,
Li & Hai 2607.23931, Xie 2606.07624, BCR 1903.04684, Kohli 2605.29800). Li & Hai and Xie
are cited here from the brief and have NOT yet been Lyra-primary-verified; flag them as
such until confirmed, exactly as the connective-tissue section flags its own
convergence-paper IDs. (RoPoLL 2606.30931 REMOVED as a co-failure-weight source — its
$\bar\gamma_W$/$N$ numbers were fabricated in an un-verified browse note; RoPoLL's real
content is robust geometric-median panel aggregation under contamination, not co-failure
measurement, and it is not otherwise cited in this section.)⟧
