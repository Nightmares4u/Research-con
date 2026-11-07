# Complete Map of the Computational Memory Lab (CML) — Jeremy B. Caplan, UAlberta Psychology

**Purpose:** so Yashal can walk into the Caplan thread prepared, not empty-handed. Research/report only. No email drafted, no contact made.
**Sources verified for this map:** CML publications page (https://www.psych.ualberta.ca/~cml/publications.html, fetched in full, 1999–2025), CML lab homepage (https://www.psych.ualberta.ca/~cml/), Caplan CV dated July 15, 2026 (http://www.psych.ualberta.ca/~cml/JBC/CV_Jeremy_Caplan.pdf), OSF API inventories for nodes 7x52q, 39cz8, b3hce, r3ywf, fsc8r, and publisher/PubMed/APA abstracts for the model papers. Prior report built on, not redone: `~/workspace/ra-outreach/caplan-research-report.md`.
**Verification flags used below:** † = mechanism verified from an abstract, full text, or code inventory. Unflagged one-liners are faithful to the paper title/topic but their mechanism was NOT individually verified — treat as topic-level, not mechanism-level.

## 1. The lab at a glance

- **PI:** Jeremy B. Caplan, Professor of Psychology, UAlberta (since July 2021; Associate 2012–2021; Assistant 2006–2012). PhD Neuroscience, Brandeis 2002 (advisor Michael Kahana, dissertation on serial/navigational learning and theta oscillations). **ScB Physics, Brown 1995** (thesis: a holographic star chart) — he entered memory science from physics, which is a genuine human resonance point (see §6).
- **Lab:** Computational Memory Lab, Psychology, Biological Sciences Building, UAlberta. Email jcaplan@ualberta.ca, lab phone 780.492.0023.
- **Self-description (lab homepage):** formal mathematical modelling of mental processes, plus behavioural measures in the cognitive-psychology tradition, EEG (ERPs and oscillations), and fMRI. Core debates the lab works on: associative chaining vs positional coding of serial order; mnemonic strategies (Method of Loci, Peg List ≈ positional coding; Link method ≈ chaining); oscillations/rhythmic brain activity, including the BOSC detection method.
- **Funding (CV, July 2026):** NSERC Discovery $255,000, 2023/04/01–2028/03/31 ("Basic mechanisms of directionality and association in relational memory") — covers all of Winter 2027; Alberta Innovates/NSERC Alliance supplement $40,000 ends 2027/02/01. See `caplan-funding-report.md` for the pay mechanics.
- **Current members, as publicly visible (CV, July 15, 2026 — Fall 2026 roster may differ):**
  - Postdoc: Tamari Shalamberidze (co-supervised with Pan Liu), June 2026–present.
  - Undergraduates, current: Avery Rudelich (Psychology, 2026–), Aditi Roy (Psychology, 2024–), Ziad Kadoura (Computing Science, 2023–), Devon Yanitski (Psychology, 2025–).
  - No current graduate student is listed: the last MSc (Sergio Barra Rodríguez) ended Oct 2024; Shalamberidze's PhD ended Apr 2026. The lab is currently small and undergrad-heavy — a CS undergrad with modelling skills is not an unusual profile here (precedent: Kaiyuan Xu, CS BSc, 2nd author on a 2020 modelling paper; Faisal Anquour, CS, 2024–2025; Ayaan Jutt, CS side-project, 2023–2025).
  - Recent alumni in the 2023–2025 window: Gaurav Bansal (Psych), Kieran Pawluk (Psych, BOSC paper first author), Madhvi Sharma (Psych), Avigna Jena (Psych).

## 2. Methods toolkit (the lab's actual machinery)

- **Matched-filter / summed-similarity models:** memory = a summed feature vector m = Σᵢ wᵢ,꜀ ⊗ fᵢ; a probe's matching strength sₓ = fₓ · m; "old" if sₓ > θ, with the analytic criterion θᵢ,꜀ = (1/2)·νᵢ,꜀/n. Hits/false alarms computed analytically via the error function (erf) from means/variances — no simulation needed for the core predictions. †
- **Attentional subsetting:** only a subset of features is attended at study/test; subspaces n_σ ≫ n_ω ≃ n_π. Sparse regime ν ≪ n → cross-talk (overlap between memory traces) vanishes → near-null list-strength effects; compact subspaces → large effects. Ratio-of-ratios (RoR) as a dimensionless diagnostic of overlap. †
- **Convolution / correlation models:** association stored as circular convolution m = a ∗ b of item vectors; retrieval by correlation (approximate deconvolution). Matrix/outer-product models (m = Σ a bᵀ) as the rival family that stores order unambiguously. †
- **Chaining models:** item→item associations; retrieval cue = previously retrieved item; variants add a start-signal item, non-cleared memory across lists, and full non-redintegrated retrieved output as the next cue. †
- **Signal-detection theory:** d′, hits/FAs, criteria; applied to recognition, associative recognition, and mask-model simulations. †
- **Fitting discipline:** grid search / direct search over few parameters, BIC model comparison (ΔBIC > 2 = substantial), analytic moment-matching, and pre-stated decision rules. Falsification is the house style: models are built to be killed by data (e.g. protrusions were supposed to kill chaining; the lab showed they don't). †
- **Oscillation analysis (BOSC):** Better OSCillation detection — fit the 1/f^α background spectrum (α typically 1–2), set power thresholds from that background plus a duration threshold scaling with period; detects rhythmic episodes vs coloured noise, more selective across sites/tasks/species than band-power. 2025 optimization: drop high-power values across frequencies, use median (not mean) power, robust regression — better at short windows and lopsided spectra. †
- **Neural measures:** EEG/ERPs, resting-state and task EEG, fMRI with PLS (partial least squares) network analysis, intracranial recordings (early career, with Kahana).
- **Behavioural paradigms:** immediate serial recall (forward/backward, grouped/ungrouped), judgments of relative order (JOR), cued recall, associative recognition, order recognition (AB vs BA), production-effect recognition, mnemonic-strategy training (Method of Loci, peg, link, interactive imagery).
- **Code language:** MATLAB/Octave, posted on OSF. No Python in the lab's posted code — that is a gap Yashal could fill (see §6).

## 3. Every paper on the publications page, grouped by theme

The publications page lists 73 papers (1999–2025). One more recent paper, Pawluk et al. (2025), is on the CV but NOT on the publications page — included below and flagged. Total mapped: 74.

### Theme A — Feature-space / matched-filter models of recognition (the lab's current core)

| Paper | One-line model/method summary |
|---|---|
| Caplan & Guitard (2024), feature-space theory of the production effect, Exp. Psych. 71(1), 64–82 † | Attentionally masked matched filter: produced (aloud) items get more attended features, so their probe vector matches the memory trace more strongly; predicts the production advantage and its list-composition interactions. Model code: OSF 7x52q. |
| Caplan & Guitard (2024), stimulus duration and recognition, J. Memory & Language 139, 104556 † | Same subsetting machinery, but features accrue over time: shallow features early, deep features later; masking in pure-strong lists explains duration × list-composition effects. Code: OSF 39cz8. |
| Caplan (2023), sparse attentional subsetting, J. Math. Psych. 116, 102802 † | The general theory: sparse attended subsets (ν ≪ n) kill cross-talk and produce null list-strength effects; compact subsets produce large ones; RoR diagnostic. Analytic, no simulation. |
| Caplan, Chakravarty & Dittmann (2022), associative recognition without hippocampal associations, Psych. Review 129(6), 1249–1280 † | Summed-similarity matched filter WITHOUT stored associations: one item's features can activate another item's features, so feature-strength patterns per probe diagnose pairing; six mask models (left-dominant, left-random, combined × vector/matrix) reproduce intact-vs-recombined matching-strength distributions and d′. Code: OSF b3hce. |
| Caplan, Xu, Chakravarty & Jones (2020), bias in vector models gives item memory for free, J. Math. Psych. 97, 102358 † | Anderson (1970) heteroassociative model (sum of outer products) with a non-zero element mean (bias, as firing rates require): bias creates interference and intrusions, but a constant-vector probe retrieves a weighted sum of studied items — formally Anderson's item-memory model, for free; works when bias > 0 but not too large vs element SD; demonstrated in a two-layer spiking-neuron network. |
| Caplan (2005), associative isolation, J. Math. Psych. 49(5), 383–402 † | Isolation Principle: pairs vs lists are ends of a continuum of item isolation; varying item–item strengths (chaining) or position-similarity structure (positional coding) explains why forward/backward probe correlations are near-perfect for pairs but only moderate for lists. |

### Theme B — Serial order: chaining vs positional coding (the lab's long-running debate)

| Paper | One-line model/method summary |
|---|---|
| Caplan, Shafaghat Ardebili & Liu (2022), chaining models can produce positional errors, J. Math. Psych. 109, 102677 † | Chaining CAN produce protrusions (prior-list errors at their correct position) given three ingredients: a start-signal item associated with all first items, memory not cleared between lists, and the full non-redintegrated retrieved output as the next cue — the model covertly recalls all lists in parallel, weighted by recency; plus two new data sets questioning protrusion-dominance. |
| Thomas & Caplan (2023), constituent order despite symmetric associations, J. Math. Psych. 115, 102774 † | Four convolution extensions tested against order-recognition data: Model A (item–position associations), Model Σ (position vectors added before convolving), Model φ (position features concatenated), Model Π (position-specific partial permutation); fits by direct search, BIC comparison. Code: OSF r3ywf. |
| Kato & Caplan (2017), order of items within associations, J. Memory & Language 97, 81–102 † | Order recognition (AB vs BA) is above chance but only moderately coupled to association memory — killing strict convolution models (which predict no order) and strict matrix models (which predict perfect coupling); a wrongly-encoded-order simulation decouples them but wrongly predicts persistent incorrect judgments on retest. |
| Liu & Caplan (2020), temporal grouping and direction of serial recall, Memory & Cognition 48(7), 1295–1315 † | Grouping effects track OUTPUT position, not serial position: participants cue with within-chunk position during recall, combined with response suppression; fits of temporal-distinctiveness model variants. |
| Shafaghat Ardebili, Liu & Caplan (2024), all-or-none retrieval of chunks, Memory & Cognition 52(2), 352–372 † | Transitional-error-probability test of hierarchical chunk retrieval: single-study subdivided lists show NO all-or-none retrieval; it emerges only for pre-trained chunks, and reverses under post-cued backward recall — i.e. a continuous transition during chunk formation, driven at retrieval, not encoding. |
| Liu & Caplan (2022), alphabetical order and congruity effects, Can. J. Exp. Psych. 76(4), 283–301 † | N=340: congruity effect (earlier/later wording × position) extends to the alphabet, a long semantic list; best of four mechanisms = categorical response bias toward discrete "early" vs "late" letter sets; reference-point and positional-distinctiveness models fit worse. Code: OSF fsc8r. |
| Liu, Chan & Caplan (2014), generality of a congruity effect in relative-order judgments, Memory & Cognition 42(7), 1086–1105 † | Congruity effect generalizes across list lengths (4–10) and to error rate, not just RT; Hacker's self-terminating search model (direction switch) explains short lists but not longer ones — pointing to direct-access or mixed mechanisms. |
| Chan, Ross, Earle & Caplan (2009), precise instructions determine memory search strategy in JOR, Psychon. Bull. & Rev. 16(5), 945–951 | Instruction wording flips search direction in short-list relative-order judgments (self-terminating search account). |
| Rehani & Caplan (2011), interference and representation of order within associations, Q. J. Exp. Psych. 64(7), 1409–1429 | Double-function lists show direction-specific cued recall, constraining how order is represented inside associations. |
| Caplan, Madan & Bedwell (2015), item properties may influence item–item associations in serial recall, Psychon. Bull. & Rev. 22(2), 483–489 | Word frequency/imageability effects in serial recall are consistent with item properties feeding item–item associations (a chaining-friendly result), not just late redintegration. |
| Caplan (2015), order-memory and association-memory, Can. J. Exp. Psych. 69(3), 221–232 | Review/synthesis: order and association memory are related but dissociable systems, framing the lab's program. |
| Caplan (2004), unifying paired associates and serial learning via chaining simulation, NeuroComputing 58–60, 739–743 | Early simulation showing one chaining model spanning pair and list paradigms. |
| Caplan, Glaholt & McIntosh (2006), pairs versus triples, J. Exp. Psych.: LM&C 32(6), 1244–1265 | Pairs vs triples dissociate associative and list memory, supporting the isolation continuum. |
| Caplan, Boulton & Gagné (2014), associative asymmetry of compound words, J. Exp. Psych.: LM&C 40(4), 1163–1171 | Compound words show forward/backward asymmetry patterns that constrain symmetric-association accounts. |
| Kahana & Caplan (2002), associative asymmetry in probed recall of serial lists, Memory & Cognition 30(6), 841–849 | Forward/backward probed recall of serial lists is asymmetric — the empirical anchor for the symmetry debate. |

### Theme C — Associative competition, interference, strategies, and applied memory

| Paper | One-line model/method summary |
|---|---|
| Caplan, Hennies & Sommer (2022), competition between associations in memory, J. Cogn. Neurosci. 34(11), 2144–2167 † | fMRI of AB/BC interference: precuneus tracks competitive retrieval of the earlier pair during study of the later pair (diverting study resources); vmPFC + anterior hippocampus activity at earlier-pair study reverses interference; angular gyrus + mid-frontal activity mark resolution after both pairs seen. |
| Caplan, Rehani & Andrews (2014), associations compete directly in memory, Q. J. Exp. Psych. 67(5), 955–978 | Behavioural evidence that overlapping associations compete at retrieval, not merely at encoding. |
| Burton, Lek & Caplan (2017), associative independence revisited, Q. J. Exp. Psych. 70(4), 832–857 | Conflicting associations can be resolved — even reversed — in a single trial, against strict independence accounts. |
| Burton, Lek, Dixon & Caplan (2019), associative interference in older vs younger adults, Psych. & Aging 34(4), 558–571 | Aging increases associative interference and changes its resolution profile. |
| Caplan, Bottomley, Kang & Dixon (2015), rhythmic vs non-rhythmic activity in aging rest, NeuroImage 112, 341–352 | Resting-state BOSC separation of rhythmic from 1/f activity in healthy neurocognitive aging. |
| Kluger, Oladimeji, Tan, Brown & Caplan (2022), mnemonic scaffolds vary in effectiveness, Memory 30(7), 869–894 | Method of Loci vs peg vs other scaffolds differ in serial-recall effectiveness (scaffold ≠ scaffold). |
| Thomas, Ayuno, Kluger & Caplan (2023), interactive-imagery instructions and association memory, Memory & Cognition 51, 371–390 | Interactive imagery instructions improve association memory, with boundary conditions. |
| Sahadevan, Chen & Caplan (2021), imagery-based strategies for associations, Memory 29(10), 1275–1295 | Imagery strategies for pair learning: which variants help, and for what. |
| Caplan, Legge, Cheng & Madan (2019), method of loci minimally related to imagined navigation, Q. J. Exp. Psych. 72(10), 2541–2553 | Method-of-Loci effectiveness does NOT depend much on navigation factors — against a strong spatial-navigation account of the mnemonic. |
| Legge, Madan, Ng & Caplan (2012), memory palace in minutes: virtual vs conventional environments, Acta Psychologica 141(3), 380–390 | Virtual-environment loci work as well as real ones, and fast. |
| Chakravarty, Fujiwara, Madan, Tomlinson, Ober & Caplan (2019), value bias of verbal memory, J. Memory & Language 107, 25–39 | Reward value biases verbal memory, analysed as utility rather than raw value in follow-up work. |
| Madan, Fujiwara, Gerson & Caplan (2012), high reward aids items but hurts new temporal binding, Frontiers in Integrative Neuroscience 6, 61 | Reward enhances item memory while impairing binding to a new temporal context — a dissociation. |
| Madan, Caplan, Lau & Fujiwara (2012), emotional arousal does not enhance association-memory, J. Memory & Language 66, 695–716 | Arousal ≠ association enhancement: emotional arousal fails to boost pair memory. |
| Fujiwara, Madan, Caplan & Sommer (2021), emotional arousal impairs association-memory: prefrontal roles, Learning & Memory 28(3), 76–81 | Prefrontal mechanisms of arousal-impaired association memory. |
| Madan, Fujiwara, Caplan & Sommer (2017), emotional arousal impairs association-memory: amygdala/hippocampus, NeuroImage 156, 14–28 | fMRI version: amygdala/hippocampal roles in the arousal impairment. |
| Caplan, Sommer, Madan & Fujiwara (2019), reduced association-memory for negative information, Cognition & Emotion 33(8), 1745–1753 | Negative valence reduces association memory; confidence and interactive imagery modulate it. |
| Madan, Glaholt & Caplan (2010), item properties and association-memory, J. Memory & Language 63, 46–63 | Word frequency/imageability effects on pair memory constrain association models. |
| Caplan & Madan (2016), word-imageability enhances association-memory via hippocampal engagement, J. Cogn. Neurosci. 28(10), 1522–1538 | Imageability boost to association memory is hippocampally mediated (fMRI). |
| Caplan, McIntosh & De Rosa (2007), two networks for proactive interference resolution, Cerebral Cortex 17(7), 1650–1663 | PLS/fMRI: two distinct functional networks resolve proactive interference. |
| Caplan, Luks, Simpson, Glaholt & McIntosh (2006), parallel networks across attention and motion, NeuroImage 29(4), 1192–1202 | Multi-seed PLS fMRI of attentional/motion networks (methods paper, memory-adjacent). |
| Talmi, Caplan, Richards & Moscovitch (2015), long-term recency in anterograde amnesia, PLoS ONE 10(6), e0124084 | Long-term recency survives anterograde amnesia — constraining context-drift accounts. |
| Talmi, Anderson, Riggs, Caplan & Moscovitch (2008), emotion and attention effects on immediate memory, Learning & Memory 15(3), 172–182 | Emotion's immediate memory consequences run through attention to pictures. |
| Klingmüller, Caplan & Sommer (2017), intrusions: reconsolidation or interference?, Learning & Memory 24(5), 216–224 | Episodic intrusions are better explained as interference than reconsolidation. |
| Pahwa, Miller, Caplan & Collins (2020), associative memory test 8 hours after cardiovascular exercise, J. Sport & Exercise Psych. 42(3), 219–226 | Acute cardio exercise depresses associative test performance at 8 hours. |
| Crawford, Caplan & Loprinzi (2021), acute exercise timing and memory interference, Perceptual & Motor Skills 128(3), 1215–1234 | Exercise timing modulates memory interference. |
| Loprinzi & Caplan (2024), acute exercise intensity and mnemonic discrimination, Q. J. Exp. Psych. 78(3), 534–545 | Null result: acute exercise intensity does not move mnemonic discrimination (listed as 2024 on the publications page; journal volume is 2025). |
| Madan, Ludvig & Spetch (2017), memory in risky decisions from experience vs description, Q. J. Exp. Psych. 70(10), 2048–2059 | Memory processes distinguish experience-based from description-based risky choice. |
| Chakravarty, Chen & Caplan (2020), predicting memory from study-related brain activity, J. Neurophysiology 124(6), 2060–2075 | Study-phase brain activity predicts later memory (subsequent-memory effect, EEG). |

### Theme D — Oscillations, EEG/ERP, and BOSC (the rhythms program)

| Paper | One-line model/method summary |
|---|---|
| Whitten, Hughes, Dickson & Caplan (2011), better oscillation detection method, NeuroImage 54(2), 860–874 † | BOSC introduced: model the background spectrum's functional form at each site, derive power + duration thresholds from it, yielding frequency/region/task-unbiased rhythm detection, robust to alpha presence/absence and applicable to independent components. BOSC scripts posted as supplementary materials. |
| Hughes, Whitten, Caplan & Dickson (2012), BOSC extracts sustained and transient rhythms from rat hippocampus, Hippocampus 22(6), 1417–1428 | BOSC validated in rat hippocampal recordings: separates sustained from transient rhythms. |
| Pawluk, Shalamberidze & Caplan (2025), making oscillation detection more robust, J. Neuroscience Methods 422, 110510 † | Optimized BOSC: remove high-power values across frequencies, median (not mean) power, robust regression — better at short windows and lopsided spectra; standard BOSC still fine in typical cases. NOTE: on the CV, NOT on the publications page. |
| Shalamberidze, Nash & Caplan (2025), rhythmic activity in resting-state EEG predicts trait anxiety, Imaging Neuroscience 3, IMAG.a.44 | Resting-state rhythmic (BOSC-derived) activity predicts trait anxiety — the lab's newest applied-oscillation result. |
| Chen & Caplan (2017), rhythmic activity and individual variability in recognition, J. Cogn. Neurosci. 29(1), 183–202 | Theta oscillations track recognition performance; alpha tracks ERPs — a double dissociation of rhythm vs evoked activity. |
| Caplan & Glaholt (2007), roles of EEG oscillations in learning relational information, NeuroImage 38(3), 604–616 | Oscillatory correlates of learning associations vs order. |
| Caplan, Glaholt & McIntosh (2009), EEG activity underlying successful study of associative and order information, J. Cogn. Neurosci. 21(7), 1346–1364 | Study-phase EEG signatures dissociate associative from order encoding success. |
| Chen, Lithgow, Hemmerich & Caplan (2014), encoding and retrieval ERPs together determine memory outcome, Exp. Brain Research 232(1), 3175–3190 | Memory outcome is jointly determined by encoding- and retrieval-phase ERPs. |
| Caplan, Bottomley, Kang & Dixon (2015) — see Theme C (aging rest; BOSC application). | |
| Cruikshank, Caplan & Singhal (2014), perception-based ERP and delay in memory-guided reaching, Exp. Brain Research 232(7), 2087–2094 | Delay magnitude modulates a perception-based ERP in memory-guided action. |
| Cruikshank, Caplan & Singhal (2012), electrophysiological reflections of perceptual recruitment in memory actions, J. Vision 12(6), 1–13 | Perceptual processing is recruited during memory-guided actions (ERP). |
| Cruikshank, Singhal, Hueppelsheuser & Caplan (2012), theta oscillations and sensorimotor integration, J. Neurophysiology 107(1), 65–77 | Theta as a putative mechanism for human sensorimotor integration. |
| Masuda, Russell, Chen, Hioki & Caplan (2014), N400 incongruity in episodic memory across cultures, Cognitive Neuroscience 5(1), 17–25 | Japanese vs European Canadians differ in handling relevant contextual information (N400 episodic task). |
| Howard, Rizzuto, Caplan et al. (2003), gamma oscillations correlate with working-memory load, Cerebral Cortex 13(12), 1369–1374 | Human gamma power scales with WM load. |
| Ekstrom, Caplan, Shattuck, Fried & Kahana (2005), human hippocampal theta during virtual navigation, Hippocampus 15(7), 881–889 | Hippocampal theta during virtual navigation in humans. |
| Caplan, Madsen, Schulze-Bonhage et al. (2003), human theta and sensorimotor integration/spatial learning, J. Neuroscience 23(11), 4726–4736 | Theta relates to sensorimotor integration and spatial learning. |
| Caplan, Kahana, Raghavachari & Madsen (2001), distinct brain-oscillation patterns underlie two maze-learning parameters, J. Neurophysiology 86(1), 368–380 | Different oscillation patterns track different parameters of maze learning. |
| Raghavachari, Kahana, Rizzuto, Caplan et al. (2001), gating of human theta by a working-memory task, J. Neuroscience 21(9), 3175–3183 | WM task gates human theta oscillations. |
| Caplan, Kahana, Sekuler, Kirschen & Madsen (2000), task dependence of human theta, NeuroComputing 32–33, 659–665 | Human theta is task-dependent — the case for multiple cognitive functions of theta. |
| Kahana, Sekuler, Caplan, Kirschen & Madsen (1999), human theta during virtual maze navigation, Nature 399(6738), 781–784 | Landmark human-theta navigation paper. |
| Kahana, Caplan, Sekuler & Madsen (1999), reply on intracranial theta, Trends in Cognitive Sciences 3(11), 406–407 | Response to O'Keefe & Burgess on theta interpretation. |

### Theme E — Spatial navigation and grid cells

| Paper | One-line model/method summary |
|---|---|
| Rodríguez Domínguez & Caplan (2019), hexagonal Fourier model of grid cells, Hippocampus 29, 37–45 † | Grid-cell population = a 2-D Fourier basis set in hexagonal coordinates with restricted basis-function availability; explains benchmark findings, is implementable by simple MEC mechanisms, and implies grid cells support lossy compression of contextual information (not just space). Supplementary materials posted. Featured cover. |
| Ekstrom, Kahana, Caplan et al. (2003), cellular networks underlying human spatial navigation, Nature 425(6954), 184–188 | Human single-unit spatial navigation networks (place-like cells). |
| Jacobs, Korolev, Caplan et al. (2010), right-lateralized brain oscillations in human spatial navigation, J. Cogn. Neurosci. 22(5), 824–836 | Spatial navigation oscillations are right-lateralized. |
| Newman, Caplan, Kirschen et al. (2007), virtual taxicab drivers learn layout and landmark information, Cognition 104(2), 231–253 | Navigation learning uses both layout and landmark information. |

### Theme F — Methods, reviews, and early foundations (for completeness)

| Paper | One-line summary |
|---|---|
| Kato & Caplan (2017), brain representations may be compatible with convolution models, Can. J. Exp. Psych. 71(4), 299–312 | Neural-representation evidence assessed against convolution-model compatibility. |
| Caplan (2015) order/association review — see Theme B. | |
| Caplan (2005) isolation — see Theme A. | |
| Caplan (2004) chaining simulation — see Theme B. | |

## 4. All posted code, inventoried

| Location | Contents (verified via OSF API) | Belongs to | What to know |
|---|---|---|---|
| OSF 7x52q, `model_code/` (7 files) | `overlap_nm.m` (535 B), `duration_model.m`, `homophones_fit.m`, `production_lse_fit.m`, `production_model.m` (~170 lines), `production_by_duration_model.m`, `README.txt` | Caplan & Guitard (2024) production effect | `production_model.m` is the matched-filter implementation; `overlap_nm.m` (~30 lines) is the conceptual heart — it computes feature overlap between memory traces. FLAG (carried from prior report): the exact body of `overlap_nm.m` past line 28 was inferred from its docstring/usage/hypergeometric expectation, not read directly. `production_lse_fit.m` contains a triple loop that is a concrete vectorization candidate. |
| OSF 39cz8, `MODEL_CODE/` (5 files) + `DATA/`, `STIMULI/`, `EXPERIMENT_CODE/`, `ANALYSIS_CODE/` | `preliminary_models_hits_fas.m`, `README.txt`, `overlap_nm.m` (MD5 d242dd6f490d01e733ebb6d4ac88268c — byte-identical to the 7x52q copy), `duration_hits_fas.m`, `duration_dprime.m` | Caplan & Guitard (2024) duration paper | The duration paper reuses the same overlap core; `duration_hits_fas.m` / `duration_dprime.m` produce hits/FAs and d′ under the duration account. |
| OSF b3hce (8 files) | `left_dominant_mask_model.m`, `left_dominant_mask_matrix_model.m`, `left_random_mask_model.m`, `left_random_mask_matrix_model.m`, `combined_mask_model.m`, `combined_mask_matrix_model.m`, `running_script.m` (24,892 B), `README` | Caplan, Chakravarty & Dittmann (2022) Psych Review | README confirms: "Use running_script.m to generate simulation figures 5 to 7." Parameters: N = 1000 features, K = 50% activated features, L = 8 list length, rho = 1 forgetting rate, nL = 1 lists, repair = 0, out_en = 0; 500 runs per condition. Sweeps: feature size N = 100:100:1000, activated proportion K = 10:10:100, list length L = 8:2:30, forgetting rate rho. Outputs: intact vs recombined matching-strength distributions and d′. This is the lab's most complete simulation pipeline. |
| OSF r3ywf (folders + ReadMe.rtf) | `Benchmark1a/` contains only `Benchmark1a.m` (17,627 B); also `Benchmark1b/`, `Benchmark2/`, `DirectSearchBenchmark1_ParametricPlotScripts/`, `Supplementary/`, `DataFiles/` | Thomas & Caplan (2023) constituent order | Benchmark scripts for the four convolution extensions (A, Σ, φ, Π) with direct-search fits. FLAG: contents of Benchmark1b/, Benchmark2/, and the parametric-plot scripts folder were not individually inventoried. |
| OSF fsc8r, `model_code/` + `Dataset/` | `congruity_anchor.m` (976 B), `congruity_simple.m` (2,456 B), `congruity_positional_distinctiveness.m` (985 B), `congruity_categorical_variable_cut.m` (991 B), `plot_CE_model.m` (4,173 B), `README.txt`, `LICENSE.txt`, `data_to_fit/` | Liu & Caplan (2022) alphabet congruity (paper states MATLAB/Octave code for all models + plotting script are on this node) | The four mechanism files map onto the paper's four congruity mechanisms (anchor/reference-point, positional distinctiveness, categorical early/late cut — the winner — plus a simple model). FLAG: file-to-mechanism mapping is inferred from filenames + paper text, not from reading each file body. |
| Whitten et al. (2011) supplementary materials | BOSC scripts | BOSC method | Per the publications page "[BOSC scripts]"; the scripts themselves were not inventoried here. |
| Rodríguez & Caplan (2019) supplementary materials | Grid-cell model supplements | Hexagonal Fourier model | Per the publications page; not inventoried here. |
| Publications-page "[Model Code]" links (chaining 2022; Liu & Caplan 2020 temporal grouping) | Destination not inventoried | Respective papers | FLAG: these links exist on the publications page but their OSF nodes were not resolved in this pass — check before assuming they are the nodes above. |

**What is NOT posted:** no Python anywhere in the lab's posted code; no code for the EEG/fMRI papers beyond BOSC; no lab GitHub found on the publications page. MATLAB is free to Yashal via the university (per Caplan's email), and Octave runs the .m files free.

## 5. Lab structure as a system (how the pieces fit)

- **One question, three levels.** Everything in the lab is the same question — how are associations and order represented? — attacked at three levels: (1) closed-form math (matched filter, subsetting, convolution), (2) simulation (mask models, chaining, benchmark fits), (3) brain data (EEG/BOSC, fMRI/PLS) that constrains the math. A new RA can enter at any level.
- **The house style is falsificationist, not fit-maximalist.** Papers repeatedly set up a clean kill-test: protrusions vs chaining, order recognition vs convolution/matrix, congruity mechanisms vs each other, BOSC vs band-power. Parameters are few, decision rules are stated before fitting, and BIC punishes complexity. This is the closest thing in psychology to Yashal's preregistered Experiment 001 discipline.
- **The current frontier (2022–2025) is Theme A + Theme D:** the feature-space matched filter (production, duration, sparse subsetting) and the optimized BOSC/anxiety work. The chaining/positional debate (Theme B) is the lab's identity but its most-cited recent word is the 2022–2023 trio. The grid-cell Fourier paper (2019) is a one-off — no follow-up grid-cell program is visible.
- **Who does what (visible):** Caplan is the modeller; Shalamberidze (postdoc) carries the EEG/anxiety line; undergrads historically split between experiments (Psych majors) and modelling/code (CS majors — Xu, Anquour, Jutt, Kadoura). A CS undergrad offering modelling + code is filling a known slot, not inventing one.

## 6. Tie-ins per theme — background, research goals, and honest gaps

### Theme A — Feature-space / matched-filter recognition
- **(a) Background fit — STRONGEST.** Overlap between memory traces is a stability analysis: how much does one trace perturb another? That is Yashal's persistence-under-interference question in a new domain. The sparse regime (ν ≪ n → cross-talk vanishes) is a clean phase-transition-style result — the kind of regime thinking dynamical-systems work trains. Analytic moment-matching (means/variances → erf → hits/FAs) is the same "derive before you simulate" discipline as preregistration, and the pre-stated criterion θ = μ/2 rhymes with his pre-stated 100-seed supermajority rule. The honest-null parallel is direct: Caplan's program has repeatedly published results that kill a favoured model (see Theme B), and his own Experiment 001 verdict was "no interesting signal."
- **(b) Research-goal fit — REAL but NARROW.** The Raza theory's "persistence of structure under perturbation" maps onto overlap/cross-talk and onto the subsetting idea (a structure persists if its attended features survive interference). The "dynamic stability = change that recursively reproduces itself" thread maps weakly onto the matched filter's iterative retrieval idea — but the lab's filter is a single-shot match, not a recurrent dynamical system. No entropy, no thermodynamics here.
- **(c) Gaps.** No entropy/negentropy measure anywhere; no thermodynamics; no claim that matching strength relates to consciousness; no dynamics over time (the model is static: encode → probe → decide).

### Theme B — Serial order: chaining vs positional coding
- **(a) Background fit — STRONG.** Chaining IS a discrete dynamical system: state (retrieved item) → next state via learned associations, with feedback (the retrieved output becomes the next cue). The 2022 protrusion result — parallel recall of all lists weighted by recency — is a superposition/recurrence phenomenon a dynamical-systems person can immediately formalize. Temporal grouping + response suppression is feedback control in behavioural clothing. The convolution models are linear algebra (circular convolution, correlation as deconvolution) — directly in Yashal's wheelhouse, and the four-model BIC shootout in Thomas & Caplan is exactly the "compare mechanisms, don't just fit one" practice his experiment lacked (he compared systems, not models, and noted that gap himself).
- **(b) Research-goal fit — MODERATE.** Recurrence, iteration, and "order from iteration" are the lab's native language, and the lab's central insight — that order can emerge from symmetric associations plus retrieval dynamics rather than being stored explicitly — is philosophically adjacent to "structure emerging from recurrence." But the lab's order is list order (which word came 3rd), not cosmic order; its recursion is one retrieval step, not nested recurrences across scale.
- **(c) Gaps.** No oscillation-as-geometry here (that's Theme D/E, and even there it's measurement, not metaphysics); no zero–infinity duality; no cyclic cosmology; no quantum anything; no consciousness theory. The lab would treat "I-ness" as outside its explanandum.

### Theme C — Competition, strategies, applied memory
- **(a) Background fit — MODERATE.** The competition results (precuneus/vmPFC/hippocampus) are empirical neuroscience, not modelling — Yashal's contribution here would be data analysis or experiment-running, not theory. The strategy work (loci, imagery, scaffolds) is the lab's most applied line and the furthest from his skills.
- **(b) Research-goal fit — WEAK.** Nothing in this theme touches the Raza threads except the generic "interference as perturbation" idea. The exercise/aging/emotion papers are collaborations, not the lab's core.
- **(c) Gaps.** Same as above, plus: this theme is where a newcomer is most likely to be assigned participant-running rather than modelling — worth knowing before accepting any role.

### Theme D — Oscillations, EEG, BOSC
- **(a) Background fit — STRONGEST for the oscillation thread.** BOSC is signal processing: fit a 1/f^α background, threshold power + duration, detect episodes. That is Fourier/spectral analysis plus robust statistics (median, robust regression) — directly transferable Python/NumPy work, and the 2025 optimization paper is a methods paper a CS undergrad can genuinely extend (e.g. port BOSC to Python, test it on synthetic signals with known ground truth, as the paper itself does).
- **(b) Research-goal fit — THE CLOSEST REAL BRIDGE, and the one to handle most carefully.** Yashal's theory leans hard on "circles/oscillation as the geometry of stability" and nested recurrences across scale. The lab DOES study brain rhythms, theta/gamma, and rhythmic vs arrhythmic activity — and the grid-cell Fourier paper treats a neural population as a Fourier basis. That is a legitimate conversation opener: "you treat rhythms as structure-bearing, not epiphenomenal; my question is what makes a rhythmic structure persist." BUT: the lab's oscillations are measurement targets (does theta predict memory? can we detect rhythms cleanly?), not a theory of consciousness, and BOSC's whole point is to avoid mistaking background noise for rhythm — the opposite of reading cosmic significance into every oscillation. If Yashal frames his theory as "oscillations = consciousness," he will lose the room; if he frames it as "I care about what makes a rhythmic/persistent structure stable under noise, and BOSC is the cleanest version of that question I've seen," he is speaking their language.
- **(c) Gaps.** No claim that oscillations constitute consciousness; no entropy; no quantum; no cosmology; no zero–infinity; no panpsychism. Theta is a 4–8 Hz rhythm, not a metaphysical principle.

### Theme E — Grid cells / spatial navigation
- **(a) Background fit — MODERATE–STRONG.** The hexagonal Fourier model is the lab's most mathematical single paper and the most physics-adjacent: a population as a Fourier basis set, lossy compression of context, hexagonal coordinates. A physics-background CS student can read it cold.
- **(b) Research-goal fit — INTRIGUING but DORMANT.** "Representation as a periodic basis set" and "lossy compression of context" rhyme with the Raza theory's compression/recurrence motifs — but this is a 2019 one-off with no visible follow-up program, and its author (Rodríguez Domínguez) has moved on (now at CIMAT, Mexico, working on dictionary learning). Do not walk in expecting a grid-cell project to exist.
- **(c) Gaps.** Navigation is spatial, not cosmological; Fourier basis ≠ zero–infinity duality; compression here is information-theoretic bookkeeping, not a consciousness measure.

### Cross-cutting honest gaps (say these to yourself before any meeting)
1. **No consciousness theory.** The lab models memory mechanisms. It has no position on consciousness, I-ness, or panpsychism, and its methods cannot test them.
2. **No entropy/negentropy program.** The word "entropy" does not appear as a lab quantity; information is measured as feature overlap, d′, or bits only implicitly. Schrödinger's negentropy, the entropy pillar, and the global-entropy/local-order duality have no lab counterpart.
3. **No quantum foundations, no cosmology, no zero–infinity work, no ER=EPR, no black holes.** None. The lab's "physics" is linear algebra, signal detection, and spectral analysis.
4. **No dynamical-systems chaos program.** Lorenz-style chaos, attractors, and stability analysis in the dynamical-systems sense are not lab tools; the lab's "dynamics" is one retrieval step or one study–test cycle.
5. **What the lab DOES offer that maps onto the theory's testable core:** a discipline of turning a vague persistence question into a falsifiable model with few parameters, analytic predictions, and a kill-test — plus a concrete skill (formal modelling + fitting + oscillation analysis) that transfers to any future AI-evaluation work. That is the real prize, and it is worth more than a lab that merely agreed with the theory.

## 7. Suggested reading/playing order

**Papers (in order):**
1. **Caplan & Guitard (2024), feature-space theory of the production effect (PMC11296319)** — the lab's current flagship model in one paper, open access, analytic math you can follow line by line. Reason: this is almost certainly what Caplan means by "model-content papers," and it is the paper a reply should cite first.
2. **Caplan (2023), sparse attentional subsetting (J. Math. Psych. 116, 102802)** — the general theory behind paper 1, and the cleanest statement of the lab's worldview (sparsity → stability of memory). Reason: it gives you the vocabulary (subspaces, cross-talk, RoR) that unlocks every other model paper.
3. **Caplan, Shafaghat Ardebili & Liu (2022), chaining models can produce positional errors (J. Math. Psych. 109, 102677)** — the falsificationist showpiece. Reason: it demonstrates the lab's intellectual character (a beloved model killed, then rescued by three precise ingredients) and gives you the chaining machinery for any serial-order conversation.

**Code (in order):**
1. **`overlap_nm.m` (OSF 7x52q)** — ~30 lines, the conceptual heart: feature overlap between memory traces. Reason: you can read it in minutes, reimplement it in Python in an hour, and it is the single file that lets you say "I played with the code" truthfully. (Carry the flag: body past line 28 inferred, not directly read — verify when you open it.)
2. **`running_script.m` (OSF b3hce)** — the full simulation pipeline: parameters, 500-run Monte Carlo, four parameter sweeps, intact-vs-recombined distributions and d′. Reason: it shows how the lab actually tests a model end-to-end, and it is the file whose Python port would be a credible first contribution (vectorizing its loops, reproducing Figures 5–7).

**After those five:** Thomas & Caplan (2023) + Benchmark1a.m for the convolution shootout; Pawluk et al. (2025) if the oscillation thread pulls you; Rodríguez & Caplan (2019) if you want the physics-adjacent conversation piece.

## 8. What to verify on first contact (unknowns, not assumptions)
- Fall 2026 lab roster (CV is July 2026): who is actually in the lab now, and whether Kadoura/Rudelich/Roy/Yanitski are still active.
- Whether the chaining-2022 and temporal-grouping-2020 "[Model Code]" links resolve to OSF nodes not inventoried here.
- The exact body of `overlap_nm.m` past line 28, and the contents of r3ywf's Benchmark1b/, Benchmark2/, and parametric-plot folders.
- Whether Caplan has a Winter 2027 project in mind already (his reply says "there might be something here IF you connect" — the project is conditional, not posted).
- Office/location and meeting norms: none of this changes the map, but the lab sits in Biological Sciences, Psychology — and Caplan's own instruction was to read + play first, then re-engage with a specific math resonance. This map is the preparation for that step, not a substitute for it.
