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

- \(N\): number of studied items in the list.
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
