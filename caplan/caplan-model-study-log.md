# Caplan model study log

Personal learning notes for understanding the Computational Memory Lab's model-content work. These notes record my own explanations and questions; they are not claims of new results.

## 2026-11-07 — Matched-filter recognition: first pass

### What the model is doing

This is computational psychology: a formal model of how recognition memory could distinguish a studied item from an unstudied item. It is programmable, but it is not a machine-learning system that trains embeddings or predicts the next word.

At study, the model combines representations of the studied items into a shared memory vector:

\[
m = \sum_i w_i \odot f_i
\]

At test, a presented item is the **probe**. Its recognition strength is computed with a dot product:

\[
s_x = f_x^\top m
\]

The model compares this strength with a criterion to predict an \"old\" or \"new\" response.

- **Studied item:** has a self-match contribution plus cross-talk from the other stored items.
- **Lure:** an unstudied probe; it has no self-match contribution, only cross-talk.
- **Cross-talk:** unwanted overlap between a probe and representations of other studied items.

The memory vector is a vector sum, not a dot product. The dot product occurs later, when a probe is compared with the shared memory.

### Vector example

If CAT and DOG are studied,

\[
m = f_{CAT} + f_{DOG}
\]

Testing CAT gives:

\[
f_{CAT}^\top m =
f_{CAT}^\top f_{CAT} +
f_{CAT}^\top f_{DOG}
\]

The first term is self-signal. The second is cross-talk from DOG. The word labels themselves are arbitrary; the model operates on assumed feature vectors.

### Feature-space terms

- \(L\): number of studied items in the list.
- \(n\): number of available feature coordinates in the shared feature space.
- \(\nu\): number of attended features per item.

A studied item is a pattern across multiple feature coordinates, not a single slot. If there are 80 studied items, a feature-space size of 1,000, and 37 attended features per item, then each of the 80 word patterns uses 37 coordinates from the same pool of 1,000 possible coordinates.

## My feature-space collision reframing

Hold the number of attended features per item fixed. Each item's active features are assigned within a shared feature universe.

If Universe A has few available feature slots, then many items are forced to reuse the same coordinates more often. If Universe B has many available slots, the same number of feature activations can spread out across more coordinates.

Therefore, under random assignment, the compact universe has a higher probability of feature collisions, so it produces greater expected overlap and cross-talk. The sparse universe lowers those collision probabilities because its representational space is less confined.

This is my way of visualizing why expected overlap scales as:

\[
\frac{\nu^2}{n}
\]

where \(\nu\) is the attended-feature count and \(n\) is the size of the shared feature space.

Important qualification: this is a personal explanatory reframing of the model's established result, not a claim that the mathematical result is new.

### Sparse versus compact

- **Sparse:** \(\nu \ll n\). Each item occupies a small fraction of a large shared feature space. Accidental overlap is reduced.
- **Compact:** each item occupies a substantial fraction of the relevant feature space. Overlap becomes more likely.

The RAM analogy is helpful if it is treated as a shared address space: holding a pattern size fixed, a larger available address space lowers the probability that two patterns reuse the same addresses. Unlike ordinary RAM allocation, multiple item traces can contribute to the same feature coordinate; that shared activation is what creates cross-talk.

## Next questions

1. How does attentional subsetting determine which \(\nu\) features are retained and re-used at test?
2. How does the model translate expected signal and noise into hits, false alarms, and \(d'\)?
3. Why does the same framework predict near-null list-strength effects in sparse/deep feature spaces but larger effects in compact/phonological spaces?


## Masking as a many-to-one mapping

My linear-algebra connection: masking and forgetting feel like many-to-one mappings.

A mask can be represented as a diagonal matrix. For example:

\[
W = \operatorname{diag}(1,0,1)
\]

maps

\[
(2,3,4) \mapsto (2,0,4).
\]

The middle coordinate has been excluded from the representation used for recognition. Knowing the masked vector and the mask cannot recover whether the original middle coordinate was 3, 99, or some other value. This is a genuinely many-to-one map: many full item vectors produce the same attended trace.

There is a related but narrower analogy to row reduction. Given only a final row-echelon form, without its row-operation history, one generally cannot recover the unique original matrix: many row-equivalent matrices reduce to the same form. However, elementary row operations preserve rank and the relevant solution structure, and are reversible when the operations are retained. Masking is closer to projection or coordinate deletion because it explicitly removes information from the representation.

### Why the model uses a mask

Masking is the model's formal statement of selective attention. It assumes that recognition does not necessarily encode every possible feature of an item. Instead, attention selects a subset at study, and roughly the same subset is available at test.

This does two jobs in the theory:

1. It preserves selected features as signal when the studied item is probed again.
2. It determines cross-talk: excluded features cannot contribute accidental overlap, while the retained subset's size relative to its feature space controls the expected overlap with other traces.

Thus masking is not merely an information-loss operation. It is the mechanism that lets the model ask how different attentional selections can yield either low interference in sparse spaces or substantial interference in compact spaces.


## List length, masking, and a capacity-limited extension

### Safe interpretation of the current model

Adding studied items does not automatically increase the amount of feature information discarded per item. If the attention mask for each item stays fixed, the per-item loss is fixed by that mask.

What list length increases is cross-talk: more stored traces are superposed in the shared memory, so matching features have more possible non-target sources. Thus, in the current model:

- more masking means more per-item feature information is excluded;
- more studied items means more interference among retained traces.

Both can harm recognition, but they are different mechanisms.

### My speculative extension: capacity-limited attention

A possible extension would make the number of attended features per item depend on study-list length. If attention has a fixed total budget, then adding more items could force the system to retain fewer features of each item. In that extended model, larger lists would have two effects:

1. more cross-talk from more superposed traces; and
2. greater per-item information loss because each item's mask becomes narrower.

This is explicitly a speculative hypothesis, not a conclusion of Caplan's current matched-filter model. It would need a stated attention-budget rule and empirical or simulation tests before being presented as a model result.


### My linear-algebra observation about the mask

I recognized the attention mask as a transformation from the full feature space into a lower-dimensional attended subspace. When the mask contains zeros, it is rank-deficient: the excluded coordinates are mapped to zero, so distinct full item vectors can map to the same attended trace.

This creates irreversible information loss for the recognition representation. Once a coordinate has been masked out, the masked trace cannot determine its original value. In that precise sense, attentional masking is a many-to-one transformation and a projection-like reduction of the usable feature representation.

This is my own linear-algebra framing of the model's masking mechanism, not a claim that the transformation itself is a new mathematical discovery.


## My speculative extension: context-sensitive mask selection

### Starting point in the current model

The current account specifies the relevant feature subspace and the number of attended features, while treating the exact selected coordinates as random within that subspace. For example, a condition can increase attended phonological features or make more deep features available.

### Extension idea

Instead of selecting attended coordinates uniformly at random within a subspace, the probability that a feature is retained could depend on properties of the study and test context, such as:

- **salience:** features that are perceptually distinctive or unusually emphasized;
- **task relevance:** features useful for the participant's current goal; and
- **context congruence:** features that match the retrieval context or cue.

The model would still retain a limited subset, but the mask would become structured rather than exchangeable. A feature's selection probability would be a stated function of these variables, rather than a uniform draw.

### Testable predictions

1. Lures sharing task-relevant or context-congruent features with studied items should produce more false alarms than lures matched only on irrelevant features.
2. Changing the retrieval goal should change which lures are confusable, even when the study list is identical.
3. The structured-mask model should be compared against the random-mask model using held-out behavioural data, with complexity penalized rather than assumed to be an improvement.

### Scope and caution

This is my proposed extension of the current account, not an established result and not yet a claim of novelty. Establishing novelty would require reading the relevant attention and recognition-memory literature. Its value is that it adds a concrete mask-selection rule and makes falsifiable predictions.


## My statistical dilution analogy for compact versus sparse spaces

My intuition for compact versus sparse feature spaces comes from statistics. A fixed number of unusually large observations has a larger influence on a sample mean when the sample is small than when the sample is very large. The same perturbation is diluted by a larger denominator.

The matched-filter model has an analogous inverse-denominator structure. Holding the number of attended features fixed, the expected overlap between two traces scales approximately as \(\nu^2/n\). When the feature space \(n\) is smaller, adding attended features to strong items has a more pronounced effect because the added features are more likely to overlap with other traces. When \(n\) is larger, that effect is diluted because the added features can spread through more possible coordinates.

The analogy is structural, not an identity: a statistical sample size and a feature-space dimension are different quantities, and the model changes an interference distribution rather than a population-height mean. Still, both make the same comparative point: a fixed perturbation has a larger relative effect in a smaller available space.


## Sensitivity of expected overlap

For two randomly subsetted item traces, expected pairwise overlap is:

\[
\mathbb{E}[\text{overlap}] \approx \frac{\nu^2}{n}.
\]

My reading of the sensitivity is:

- Increasing feature-space size \(n\) reduces expected overlap inversely.
- Increasing attended features per item \(\nu\) increases expected overlap quadratically, not exponentially.

Thus a doubled \(\nu\) produces approximately four times the expected pairwise overlap, while a doubled \(n\) halves it. This shows why a modest increase in attended features can matter greatly in a compact subspace.

Notation reminder: \(n\) is the total feature-space size, \(\nu\) is the attended-feature count per item, and \(L\) is the number of studied items that contribute competing traces.

## 2026-11-21 — Second pass: the production mechanism, the decision rule, and the fits

Added from the verified research report on the lab (Caplan & Guitard 2024, Caplan 2023, and the OSF code inventory). This is a read-through distillation, not yet worked by hand — to make it mine I need to re-derive the threshold and the ratio-of-ratios, and run `production_model.m`.

### The three subspaces and their sizes

Features split into three subspaces: phonological \(\pi\), orthographic \(\omega\), and semantic/deep \(\sigma\), with \(n_\sigma \gg n_\omega \simeq n_\pi\). The fitted values in the production paper are \(n_s = 128\) (shallow) and \(n_d = 512\) (deep), with \(\nu_\omega = 3\), \(\nu_\sigma = 2\), \(L = 50\). The size ordering is the whole game: the deep subspace is large, so attended subsets there are sparse; the phonological subspace is compact, so attended subsets there cannot be sparse.

### The production mechanism — what the paper is actually about

Reading aloud increases the attended phonological features: \(\nu_{\pi,\mathrm{aloud}} > \nu_{\pi,\mathrm{silent}}\). Because the phonological subspace is compact, its subsets cannot be sparse, so cross-talk \(V_{xy}\) is large — and that is why production shows a large list-strength effect, unlike other "strength" manipulations. The production advantage is bigger in mixed lists than in pure lists: in a pure-aloud list every item carries the same boost, so the advantage washes out in the comparison; in a mixed list the aloud items stand out against silent ones.

This connects directly to my collision reframing: production is a manipulation that pushes \(\nu\) up inside a small \(n\), so \(\nu^2/n\) grows fast. The paper's empirical claim is that strength manipulations only produce list-strength effects when they operate in a compact subspace.

### The decision rule — threshold, hits, false alarms, \(d'\)

The criterion is set from the probe itself, not tuned after the fact:

\[
\theta_{i,c} = \frac{1}{2}\cdot\frac{\nu_{i,c}}{n}
\]

the midpoint between the expected target and lure means. The model derives the mean and variance of the matching-strength distribution in closed form — \(\mu_\mathrm{target}\) from \(\nu/n\) summed over subspaces, \(\sigma^2_\mathrm{lure} = L\cdot V_{xy}\), \(\sigma^2_\mathrm{target} = V_{xx} + (L-1)\cdot V_{xy}\) — then applies the pre-stated rule: an item is judged "old" if \(s_x > \theta\). Hits and false alarms come from the normal CDF via the error function, \(P(\mathrm{hit}) = 1 - (0.5 + 0.5\cdot\mathrm{erf}((\theta-\mu)/\sqrt{2\sigma^2}))\), and \(d' = \mu/\sqrt{0.5\cdot(Tvar+Lvar)}\).

What struck me: the threshold and the \(d'\) computation are derived, not tuned after seeing the numbers. That is the same discipline as my preregistered 100-seed rule — the decision rule is fixed before the results.

### List-strength effects and the ratio-of-ratios

Caplan (2023) puts the sparse and compact regimes on one continuum: in the sparse regime (\(\nu \ll n\), deep features) cross-talk vanishes and the list-strength effect is near-null; when the attended space is compact, cross-talk is non-negligible and list-strength effects are large. One mechanism, not two.

The diagnostic is the ratio-of-ratios:

\[
\mathrm{RoR} = \frac{d'(D\ \mathrm{mixed})/d'(S\ \mathrm{mixed})}{d'(D\ \mathrm{pure})/d'(S\ \mathrm{pure})}
\]

typically \(\approx 1\) for null effects. It is a dimensionless ratio that cancels scale — the same kind of diagnostic as a stability margin. This answers my question 3: the same framework predicts near-null effects in sparse/deep spaces and large effects in compact/phonological spaces because only the ratio of subset size to subspace size changes.

### Duration extension

Shallow features are accessed early, deep features later, so longer stimulus duration means more deep features encoded (\(\nu_\sigma\) grows with duration). Key mechanism: in pure-strong lists the model can mask out (disregard) the noisy shallow features and rely on deep ones; in mixed lists it cannot, because the threshold/mask must serve both item types. This is why duration (deep-feature strength) shows near-null list-strength effects while production (compact-space strength) does not. Same machinery, opposite prediction — which is what makes the framework falsifiable rather than flexible.

### Homophone fit

Fawcett et al. (2022): homophone lures share identical phonological features with a studied item. The technical care here is what I want to remember: when features are identical, a \(V_{xy}\) term becomes a \(V_{xx}\) term (factor 1 → 2), and a `corr_var` correction subtracts the double-counted covariance:

\[
d' = \frac{Tmu - Lmu}{\sqrt{0.5\cdot(Tvar + Lvar - corr\_var)}}
\]

The model handles the edge case by adjusting the variance bookkeeping, not by adding a new mechanism.

### Fitting to data

`production_lse_fit.m` fits the model to Bodner et al. (2014) Exp. 1 by direct search: a triple grid loop over \(\nu_\sigma\) (1…32) × \(\nu_\omega\) (1…64) × \(\nu_\pi\) (1…64), RMSD to 7 data points (hits/false alarms across 4 list conditions), log-likelihood \(\log L = -nn\cdot\log(\mathrm{rmsd}^2)\). Three to four parameters, fit to real data, compared by BIC elsewhere in the lab (Thomas & Caplan 2023: \(\Delta\mathrm{BIC} > 2\) = substantial). The fit earns its keep against the data rather than by adding parameters.

### Code walkthrough — read from the OSF inventory, not yet run

- `overlap_nm.m` (~30 lines): expected number of overlapping features between two randomly subsetted vectors, \(N_M \approx \nu_1\nu_2/n\). The conceptual heart. Flag carried over: the exact body past line 28 was inferred from its docstring and usage, not read directly — verify when opening it.
- `production_model.m` (~170 lines): parameter-sensitivity sweep over amount of production (\(\nu_\pi = 1\ldots16\)) for pure/mixed × silent/aloud; computes \(\mu\), target/lure variances, \(d'\), \(\theta = \mu/2\), hits/FAs via erf. Produces paper Figures 3a,b,c.
- `production_lse_fit.m`: the triple-loop grid fit above. The \(O(\nu_\sigma\cdot\nu_\omega\cdot\nu_\pi)\) loop with erf evaluations is straightforward to vectorize — a concrete first contribution.
- `production_by_duration_model.m` and `duration_model.m`: production as a function of duration, and duration alone.
- `homophones_fit.m`: the homophone fit with the `corr_var` correction.

No MATLAB/Octave run has been done yet. Next step is to run `production_model.m` (Octave runs the .m files free) and reproduce Figures 3a,b,c, then re-derive \(\theta = \mu/2\) and the RoR by hand.

### What this closes

My next questions 2 and 3 from the first pass are now answered in outline: the decision rule (threshold, hits/FAs, \(d'\)) and the list-strength/RoR story. What remains is doing them by hand and running the code — and the two extension questions (capacity-limited attention, context-sensitive masks) are still mine to pose, not results.
