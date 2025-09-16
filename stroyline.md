# Theme

Evaluating Large Language Models as Generators of AI Research Ideas

# Summary

We study whether large language models (LLMs) can propose publishable AI research ideas. We generate **700** ideas across seven models and match them to the nearest human-authored research papers (in ICLR'2025) using a standardized semantic-similarity pipeline. After deduplication, **650** unique ideas remain; all **650** yield valid similarity scores (mean ≈ **0.826**, median ≈ **0.839**, σ ≈ **0.113**, 10–90th ≈ **0.800–0.879**). Aggregating across models, **583/650** ideas (≈**89.7%**) meet our high-similarity criterion, **56/650** (≈**8.6%**) are medium, and **11/650** (≈**1.7%**) are low. The top-performing model is **gemini-2.5-flash-preview-05-20** (mean similarity **0.854**, high-quality rate **99%**), while **gpt-4o** lags (mean **0.779**); the best-to-worst gap is ≈**9.6%** relative improvement over the worst. Comparing AI–paper similarity to human outcomes, we observe a weak negative correlation with review quality (Pearson **r ≈ −0.097**, Spearman **r ≈ −0.083**), yet human papers most similar to AI ideas have an acceptance rate of ≈**57.7%** (n = **636**). We release a reproducible protocol and provide guidance on combining cost, speed, and quality when using LLMs for research ideation.

# 1. Introduction

LLMs increasingly assist researchers in brainstorming hypotheses, tasks, and methodologies. However, we lack rigorous, reproducible measurements of how close LLM-generated ideas are to the frontier of human research. This paper introduces a **backtesting** protocol that: (i) elicits research ideas from multiple LLMs under controlled prompts and seeds; (ii) matches each idea to published or submitted human papers; and (iii) analyzes similarity, stability, domain coverage, and alignment with human review outcomes.

**Contributions.**

1. A standardized, documented pipeline for LLM research-idea generation and literature matching.
2. A head-to-head evaluation of seven contemporary models on **700** generated ideas.
3. Evidence that high-similarity ideas are common (≈**89.7%**) and that model quality varies but within a modest band.
4. An analysis of human alignment showing weak negative correlation between AI–paper similarity and human review score, alongside a relatively high acceptance rate among the closest matches.
5. Practical guidance for deploying LLMs as ideation partners (cost/efficiency trade-offs, stability, and domain coverage).

# 2. Related Work

We build on three areas: (a) automated scientific hypothesis generation; (b) evaluation of LLMs for creative ideation; and (c) semantic matching and retrieval for literature review. Our protocol complements prior work by emphasizing a **multi-model**, **reproducible** comparison against human research outputs at scale.

# 3. Evaluation Protocol

**Idea generation.** We query seven LLMs with fixed prompts and seeds, documenting all model versions, prompts, seeds, and parameters. We collect **700** ideas and deduplicate them prior to analysis, retaining **650** unique ideas.

**Matching.** Each idea is embedded and matched to the nearest human-authored paper; all **650** unique ideas yield valid similarity scores. Unless otherwise noted, statistics are computed over this matched set (n = 650).

**Quality bands.** We bin ideas by similarity into **high**, **medium**, and **low** categories. Aggregating across models yields: high **583/650** (≈**89.7%**), medium **56/650** (≈**8.6%**), low **11/650** (≈**1.7%**).

**Human alignment.** For ideas whose nearest human papers have review outcomes, we analyze acceptance rates by similarity band and compute rank/linear correlations between similarity and human scores (Pearson **r ≈ −0.097**, *p* ≈ **0.015**; Spearman **r ≈ −0.083**, *p* ≈ **0.036**).

# 4. Results

## 4.1 Overall distribution and stability

Similarity scores concentrate around the median **0.839** with an interquartile range (IQR) ≈ **0.039** (0.821–0.860). High-similarity ideas are common and fairly stable across prompts/seeds.

*Suggested figures:*

* **Figure 1:** `quality_distribution_heatmap.pdf` — density of ideas across similarity bands.
* **Figure 2:** `similarity_evolution_analysis.pdf` — evolution of similarity under prompt/seed changes (stability).
* **Figure 3:** `model_dynamic_range.pdf` — within-model spread across topics.

## 4.2 Model comparison

**Best:** **gemini-2.5-flash-preview-05-20** (mean **0.854**, high-quality rate **99%**).
**Lowest:** **gpt-4o** (mean **0.779**).
The best model shows ≈**9.6%** improvement over the worst (relative to the worst).

*Suggested figures:*

* **Figure 4:** `model_performance_ranking.pdf` — mean/median similarities by model.
* **Figure 5:** `model_performance_comparison.pdf` & `model_similarity_performance.pdf` — side-by-side comparison across metrics.
* **Figure 6:** `model_quartile_analysis.pdf` — quartile spread per model.
* **Figure 7:** `model_success_rate.pdf` & `model_failure_rate.pdf` — fraction of ideas in each quality band.

## 4.3 Consistency and variance

We examine per-model variance across prompts/seeds; lower variance indicates more predictable ideation quality.

*Suggested figures:*

* **Figure 8:** `model_consistency.pdf` — per-model dispersion.
* **Figure 9:** `model_consistency_variance.pdf` — variance comparison.

## 4.4 Domain analysis

We group ideas by domain (e.g., neural architectures, representation learning, optimization) and study model×domain interactions and domain difficulty.

*Suggested figures:*

* **Figure 10:** `model_domain_performance_heatmap.pdf` — model × domain performance.
* **Figure 11:** `domain_difficulty_ranking.pdf` — relative difficulty by domain.
* **Figure 12:** `domain_model_preference.pdf` — which models excel in which domains.

## 4.5 Alignment with human research outcomes

Across the subset with review outcomes, similarity is **weakly negatively correlated** with human review score (Pearson **r ≈ −0.097**, Spearman **r ≈ −0.083**). However, the human papers most similar to AI ideas show an acceptance rate of ≈**57.7%** (n = **636**); medium and low bands are rare in this subset (n = **2** and **0**, respectively).

*Suggested figure:*

* **Figure 13:** `ai_model_human_quality_matching.pdf` — acceptance/score vs. similarity band.

## 4.6 Efficiency considerations

We qualitatively compare **cost/speed vs. quality**. When performance is within \~10%, cost and latency may dominate model choice.

*Suggested figure:*

* **Figure 14:** `model_efficiency_analysis.pdf` — quality vs. cost/latency trade-offs.

# 5. Discussion

Our results suggest that LLMs routinely generate ideas close to existing human research, with modest but meaningful differences among models. The weak negative correlation between similarity and human review quality hints that **pushing for novelty** (rather than maximizing similarity) may yield better outcomes. Practitioners should balance **exploitation** (retrieve close prior art) with **exploration** (encourage novelty during ideation).

# 6. Limitations

We rely on semantic similarity as a proxy for topical closeness; it does not directly measure **publishability**, **feasibility**, or **novelty**. Our review-alignment subset is limited (n ≈ **638** total across bands), and acceptance is an imperfect quality signal. Figures reflect the provided analysis configuration; different prompts, seeds, or matching systems could shift outcomes.

# 7. Conclusion

LLMs already provide valuable scaffolding for research ideation. In our backtest across **700** ideas, models deliver high-similarity ideas at a high rate, with **gemini-2.5-flash-preview-05-20** leading and a ≈**9.6%** gap to the weakest model. Similarity alone is not a guarantee of human-judged quality; combining similarity with explicit novelty constraints is a promising next step.

# Figures to consider (file names)

* model\_performance\_ranking.pdf
* model\_performance\_comparison.pdf
* model\_similarity\_performance.pdf
* model\_consistency.pdf
* model\_consistency\_variance.pdf
* model\_quartile\_analysis.pdf
* quality\_distribution\_heatmap.pdf
* ai\_model\_human\_quality\_matching.pdf
* model\_success\_rate.pdf
* model\_failure\_rate.pdf
* model\_efficiency\_analysis.pdf
* model\_dynamic\_range.pdf
* model\_domain\_performance\_heatmap.pdf
* domain\_difficulty\_ranking.pdf
* domain\_model\_preference.pdf
* similarity\_evolution\_analysis.pdf
