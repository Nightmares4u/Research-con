# Caplan / Computational Memory Lab — Research Report

Prepared 2026-10-18. Research only — no reply drafted, nothing sent.
Sources verified directly: CML publications page; full texts of the papers below (PMC / author-posted PDFs); OSF code read file-by-file (nodes `7x52q`, `39cz8`, `r3ywf`).

One flag: the body of `overlap_nm.m` after line 28 did not come through in the fetch (file is 535 bytes, ends mid-statement), so its exact formula below is inferred from its docstring, its usage across all scripts, and the standard hypergeometric expectation — marked as inferred.

## (a) The 4 most relevant papers — each with its MODEL

**1. Caplan & Guitard (2024). "A feature-space theory of the production effect in recognition." *Experimental Psychology*, 71(1), 64–82.** ([PMC11296319](https://pmc.ncbi.nlm.nih.gov/articles/PMC11296319/))
Model: an **attentionally masked matched-filter model**. Memory is a vector sum of studied items after elementwise masking, **m = Σᵢ wᵢ,꜀ ⊗ fᵢ**; recognition strength is a dot product, **sₓ = fₓ · m**, judged "old" if **sₓ > θ**. Features split into three subspaces (phonological π, orthographic ω, semantic/deep σ) with **n_σ ≫ n_ω ≃ n_π**. Production (reading aloud) increases attended phonological features (**ν_π,aloud > ν_π,silent**). Because the phonological subspace is compact, its subsets can't be sparse, so cross-talk **V_xy** is large → large list-strength effect for production, unlike other "strength" manipulations. Threshold is set from the probe itself: **θᵢ,꜀ = (1/2)·νᵢ,꜀/n** (midpoint between expected target and lure means).

**2. Caplan (2023). "Sparse attentional subsetting of item features and list-composition effects on recognition memory." *Journal of Mathematical Psychology*, 116, 102802.**
Model: the foundation. Same matched filter, plus the twin assumptions: (i) only a **small subset** of an item's features is attended/encoded, (ii) roughly the **same subset re-iterates at test**. Analytic derivations show that in the **sparse regime** (ν ≪ n, deep features) cross-talk vanishes and the list-strength effect is near-null; when the attended space is compact, cross-talk is non-negligible and list-strength effects are large — one continuum, not two mechanisms. Quantified with Ratcliff et al.'s **ratio-of-ratios**: RoR = [d′(D mixed)/d′(S mixed)] / [d′(D pure)/d′(S pure)], typically ≈ 1 for null effects.

**3. Caplan & Guitard (2024). "Stimulus duration and recognition memory: an attentional subsetting account." *Journal of Memory and Language*, 139, 104556.**
Model: same framework applied to study time. **Shallow features are accessed early, deep features later**, so longer duration = more deep features encoded (ν_σ grows with duration). Key mechanism: in pure-strong lists the model can **mask out (disregard) the noisy shallow features** and rely on deep ones; in mixed lists it cannot, because the threshold/mask must serve both item types. This "nested, masked" structure explains why duration (deep-feature strength) shows near-null list-strength effects while production (compact-space strength) does not.

**4. Thomas & Caplan (2023). "Modelling constituent order despite symmetric associations in memory." *Journal of Mathematical Psychology*, 115, 102774.**
Model: four extensions of a **convolution** memory model (pair AB stored as **f ∗ g**, circular convolution; recall by correlation **f # m ≈ g**), each adding order information a different way while preserving associative symmetry: **Model A** — item–position associations, m_A = Σ αᵢ(fᵢ∗gᵢ + fᵢ∗l + gᵢ∗r); **Model Σ** — position vectors added before convolving, m_Σ = Σ αᵢ((fᵢ+l)∗(gᵢ+r)) (= A + noise term l∗r); **Model φ** — position *features* concatenated onto item vectors, m_φ = Σ αᵢ((fᵢ⊕l)∗(gᵢ⊕r)), order parameter = number of position features n_p; **Model Π** — **position-specific partial permutation**, m_Π = Σ αᵢ(p_l(fᵢ)∗p_r(gᵢ)), order parameter = number of permuted features n_perm (n_perm/n = 0 → plain convolution, no order info; = 1 → fully non-commutative). Order recognition d′ = (E[ι]−E[ρ])/√(0.5(Var[ι]+Var[ρ])) from correct- vs incorrect-position dot products. All four fit order-recognition data; only Π disambiguated AB from BC in double-function lists. Fits by direct search, compared by BIC (ΔBIC > 2 = substantial).

*Adjacent, not core:* Caplan & Guitard's newer "Spaced repetition and list-strength in recognition memory" (*Memory & Cognition*, in press) applies the same attentional-subsetting account against REM — evidence this line is active, but not read in full.

## (b) What the posted code implements

All MATLAB, script-style, no toolboxes beyond `erf` and plotting. The 7x52q README notes it "should run just as well in Octave."

**OSF `7x52q` — production + duration models (Caplan & Guitard 2024, production paper):**
- `overlap_nm.m` — the heart of the theory: expected number of overlapping features between two randomly subsetted vectors (**inferred** formula: N_M ≈ ν₁·ν₂/n, the hypergeometric mean). Called by every model script to compute cross-talk terms.
- `production_model.m` — parameter-sensitivity sweep over amount of production (ν_π = 1…16) for pure/mixed × silent/aloud; computes μ, target/lure variances (Tvar, Lvar), d′ = μ/√(0.5·(Tvar+Lvar)), threshold θ = μ/2, and hits/FAs via the normal CDF, P(hit) = 1 − (0.5 + 0.5·erf((θ−μ)/√(2σ²))). Produces paper Figures 3a,b,c. Fixed parameters from the fit: n_s = 128, n_d = 512, ν_ω = 3, ν_σ = 2, L = 50.
- `production_lse_fit.m` — **direct-search (grid) fit** to Bodner et al. (2014) Exp. 1: triple loop over ν_σ (1…32) × ν_ω (1…64) × ν_π (1…64), RMSD to 7 data points (hits/FAs across 4 list conditions), log-likelihood logL = −nn·log(rmsd²), best fit reported. Produces Figure 2a.
- `production_by_duration_model.m` — production effect as a function of stimulus duration (ν_σ sweep 1…16, ν_ω capped at 8, ν_π = 3 fixed). Figures 3g,h,i.
- `duration_model.m` — duration manipulation alone: pure/mixed × short/long, deep-feature sweep. Figures 3d,e,f.
- `homophones_fit.m` — fit to Fawcett et al. (2022): homophone lures share *identical* phonological features with a studied item. Notable technical care: when features are identical, a V_xy term becomes a V_xx term (factor 1 → 2), and a `corr_var` correction subtracts the double-counted covariance: d′ = (Tmu−Lmu)/√(0.5·(Tvar+Lvar−corr_var)). Grid search over ν_ω, number of identical orthographic features, ν_π,aloud. Figure 4b.

**OSF `39cz8` — stimulus-duration paper:**
- `duration_dprime.m` — d′ + RoR vs. number of deep features ν_σ; two variants: subject *can* mask out shallow features in pure-strong lists vs. *can't* (threshold adjusted instead). Figures 2a,b.
- `duration_hits_fas.m` — same model, hit/FA rates. Figures 3a,b.
- `preliminary_models_hits_fas.m` — two earlier/superseded models. Figures A1a,b.
- `overlap_nm.m` — byte-identical to the 7x52q copy (same MD5).

**OSF `r3ywf` — Thomas & Caplan 2023:**
- `ReadMe.rtf` — scripts generate manuscript figures; `DataFiles/` must be on the MATLAB path.
- `DataFiles/` — pre-generated direct-search prediction matrices: `AssocModelFitJan_7_2023.mat` (A), `AddModelFitJan_7_2023.mat` (Σ), `FeatureModelFitJan_7_2023.mat` (φ), `PermModelFitJan_7_2023.mat` (Π), plus `ThomEtalData.mat` / `ThomEtalData2.mat` (Thomas et al. 2022 empirical data).
- `Benchmark1a/Benchmark1a.m` (17.6 KB) — aggregate fit to order-recognition data (Benchmark 1a). Other folders (`Benchmark1b/`, `Benchmark2/`, `DirectSearchBenchmark1_ParametricPlotScripts/`, `Supplementary/`) were confirmed to exist but their individual file lists were **not** individually verified — only the ReadMe's description that they hold the figure-generating scripts.

## (c) Three specific math/methods angles Yashal could genuinely cite

**Angle 1 — Analytic moment-matching + pre-stated decision rules.**
Concept: the lab derives the *mean and variance* of the matching-strength distribution in closed form (μ_target = ν/n summed over subspaces; σ²_lure = L·V_xy; σ²_target = V_xx + (L−1)·V_xy), then applies a decision rule fixed *before* seeing the numbers (θ = μ/2, hits/FAs via erf). Source: Caplan & Guitard 2024 production paper, Assumptions 1–2 + hit/FA section; implemented in `production_model.m` (θ = mu/2; Phit/Pfa via erf).
Connection: "In my preregistered simulation study I also fixed the decision rule before seeing results — an effect counted only if positive in a supermajority of 100 seeds — and reported the null when it failed (51/100 positive). What drew me to your modelling style is the same discipline at the level of the equations: the threshold and the d′ computation are derived, not tuned after the fact."

**Angle 2 — Overlap/cross-talk as a stability analysis; RoR as a dimensionless diagnostic.**
Concept: discriminability is controlled by one structural quantity, the expected feature overlap N_M = ν₁ν₂/n (`overlap_nm.m`). Sparse subsetting (ν ≪ n) → cross-talk → 0 → stable, near-null list-strength effects; compact subspace (n_π = 64) → unavoidable overlap → large effects. The RoR index is a dimensionless ratio that cancels scale, exactly like a stability margin. Source: Caplan 2023 (sparse vs. compact regimes); Caplan & Guitard 2024 (n_σ ≫ n_ω ≃ n_π); RoR computed in every `*.m` script as `[(dp(:,4)./dp(:,3))./(dp(:,2)./dp(:,1))]`.
Connection: "My own experiment asked the same kind of question of feedback systems: under what parameter regimes does a signal persist versus get swamped by cross-talk from other components? Your result — that the *same* model yields near-null or large list-strength effects depending only on the ratio of subset size to subspace size — is a stability result, and the RoR is the kind of dimensionless diagnostic I want to learn to use."

**Angle 3 — Falsifiable fitting: direct search + BIC, few parameters, and code he could actually improve.**
Concept: models are fit by exhaustive grid search over 3–4 parameters and compared by BIC (Thomas & Caplan: ΔBIC > 2 = substantial; Model A and Π beat Σ), with the fit *earning* its keep against real data (Bodner et al. 2014; Fawcett et al. 2022) rather than by adding parameters. Source: `production_lse_fit.m` (triple loop, logL = −nn·log(rmsd²)); Thomas & Caplan 2023, Benchmarks 1a/1b + Table 1 (BIC).
Connection: "I preregistered and reported a null rather than rescuing my hypothesis, so a modelling culture where a 3-parameter model has to beat the data and where BIC adjudicates between four mechanisms is one I want to work in. Concretely, I read `production_lse_fit.m`: the O(ν_σ·ν_ω·ν_π) triple loop with erf evaluations is straightforward to vectorize, and I could port the model-code base to Python/NumPy so it runs without a MATLAB licence." (True, modest, and a real offer — not a claim of expertise he doesn't have.)

## (d) Honest fit assessment

**Strong:**
- *Mathematical style match.* Closed-form derivations → simulation to verify → parameter sweeps → model comparison against a pre-stated rule. Yashal already thinks this way (preregistration, 100-seed consistency rule, honest null).
- *Linear algebra is the lab's native language.* Vectors, dot products, elementwise masks, convolution/correlation, permutation matrices, Gaussian signal detection (erf, d′, thresholds). All within second-year CS linear algebra + programming.
- *Code is approachable.* Short, script-style MATLAB; no exotic toolboxes. Reading it is easy; porting to Python/NumPy is a genuinely useful RA-sized task.
- *Dynamical-systems intuition transfers.* Feedback, persistence, stability margins ↔ cross-talk/noise analysis and the sparse/dense regime distinction.

**Thin / gaps:**
- *MATLAB vs Python.* Lab code is MATLAB (Octave-compatible per README). Yashal reads MATLAB fine but his fluent language is Python; he'd write MATLAB/Octave or port — a small gap, not a blocker.
- *Experimental-psych methods.* The models are constrained by recognition-memory experiments (pure vs. mixed lists, hits/FAs, d′, list-strength and mirror effects). Yashal has no background in experimental design or the memory literature (REM, TODAM, MINERVA 2, Feature Model). The math is the easy part; learning *why these benchmarks matter* is the real gap.
- *Statistics.* The lab uses signal-detection theory (d′, criterion/threshold, erf), RMSD/log-likelihood fitting, BIC. Yashal's stats (CIs across seeds) is adjacent but he would need fluency in SDT and model comparison.
- *Framing risk.* His own Recursive Stability work is speculative and unpublished; Caplan's lab is about precise, falsifiable, small-scale models. In any follow-up, the pitch must stay at the **methods** level (angles above) — leading with consciousness/emergence framing would misfire. Caplan's own "if not (most likely outcome), no worries" sets the bar: a genuine connection to the modelling style, not enthusiasm for memory per se.

## (e) Where to start

- **Single paper:** Caplan & Guitard (2024), "A feature-space theory of the production effect in recognition" (*Experimental Psychology*, 71(1), 64–82; open access via [PMC11296319](https://pmc.ncbi.nlm.nih.gov/articles/PMC11296319/)). It contains the complete model — mask, matched filter, threshold, duration extension, homophone fit — and is the paper the main code base implements. The 2023 JMP paper is the foundation but more abstract; read it second.
- **Single code file:** `production_model.m` (OSF `7x52q`, `model_code/`; [download](https://osf.io/download/e4nb5/)) — the whole model in ~170 lines: μ, Tvar/Lvar, d′, θ, hits/FAs via erf, for pure/mixed × silent/aloud, plus the RoR plot. Read `overlap_nm.m` ([download](https://osf.io/download/4cpht/)) alongside it — it's ~30 lines and is the conceptual heart (expected feature overlap drives everything). If the convolution paper clicks more, start instead with `Benchmark1a.m` in OSF `r3ywf`.

**Unverified / flagged:** exact body of `overlap_nm.m` past line 28 (formula inferred, see top); individual file lists of the `Benchmark1b/`, `Benchmark2/`, `DirectSearchBenchmark1_ParametricPlotScripts/`, `Supplementary/` folders (existence confirmed, contents not listed); the 2024 JML duration paper was covered via its code + OSF description + the production paper's duration section, not a full-text read.
