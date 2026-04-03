We deeply appreciate your constructive feedback. We have addressed all your concerns and conducted extensive new experiments. Due to space constraints, we present the core results here. **All comprehensive data tables are provided in our anonymous GitHub repository: [Anonymous Table URL](https://anonymous.4open.science/r/ICML-2026-Table-9F0D/Reviewer%20cGj2-table.md).**

**Q1: Test Leakage (Crucial Clarification)**
TimeVQGAN acts strictly as an **unsupervised tokenizer**, akin to BPE in LLMs or VQGAN in CV, which are routinely pretrained on full datasets without leakage concerns. It learns morphological primitives via self-reconstruction, never accessing downstream task targets. Furthermore, the overlapping datasets constitute a negligible **0.089%** of the 48M sample 300B corpus, which is overwhelmingly dominated by synthetic and weather data. 

To definitively prove our SOTA results do not stem from leakage, we retrained TimeVQGAN entirely from scratch on a strictly **decontaminated Leak-Free corpus**. Downstream MoVE performance remained identical:
*   **ECL MSE/MAE:** Orig 0.175/0.268 vs. Leak-Free 0.175/0.269
*   **Traffic MSE/MAE:** Orig 0.412/0.279 vs. Leak-Free 0.412/0.279
*   **M4 Avg sMAPE:** Orig 13.54 vs. Leak-Free 13.53
This empirically guarantees our evaluation is completely fair and robust.

**Q2: Expanded SOTA Baselines & Benchmarks**
*   **VQ Baselines (TOTEM):** Results highlight an architectural trade-off. TOTEM optimized by pure MSE acts as a low-pass filter, favoring smooth data like ECL and Weather. Conversely, MoVE's adversarial training captures complex high-frequency volatility, dominating dynamic data. For example, MoVE achieves **0.027** vs TOTEM's 0.054 on ETTm1 Imputation Avg MSE, and **96.99** vs 95.87 on PSM Anomaly Detection F1.
*   **LLM Baselines (Time-LLM, GPT4TS):** In forecasting, MoVE matches or beats GPT4TS and closely trails Time-LLM. Crucially, Time-LLM relies on continuous patching and a massive **7B LLaMA**, whereas MoVE uses a standard **100M GPT-2**, operating at **~1/70th the size**. Furthermore, because MoVE outputs true discrete tokens, it bridges time series to standard categorical vocabularies, unlocking step-by-step autoregressive generation that continuous-patching LLMs cannot natively perform.
*   **Forecasting & Imputation:** MoVE significantly outperforms TimeMixer++ in Imputation, achieving **0.042** vs 0.055 Avg ETT MSE. In Forecasting, MoVE matches or beats both TimeMixer++ and pre-trained TinyTimeMixers, winning all ETTm1 and Traffic horizons.
*   **Classification:** We expanded our evaluation to all 30 UEA datasets to eliminate selection bias, comparing against TS2Vec, TimesNet, PatchTST, TSPulse, and VQShape. MoVE achieves SOTA average performance across the full suite.
*   **Anomaly Detection:** On the rigorous TSB-AD benchmark, MoVE strongly outperforms TimesNet and AutoEncoder across metrics, achieving **0.253** vs 0.190 in Univariate AUC-PR, and **0.297** vs 0.250 in Standard-F1 against AutoEncoder.

**Q3: Limited Criteria in Ablations**
We agree that MSE alone does not perfectly reflect generative token quality. We expanded our 128-dataset ablations to include **FID and Inception Score (IS)**. Results confirm our adversarial setup perfectly aligns reconstruction fidelity with generative quality, as optimal configurations maximize all metrics jointly. For Quantization Block Size, size 4 is the sweet spot with 0.089 MSE and 35.6 FID. Expanding to 16 sharply degrades semantic quality to 0.129 MSE and 65.1 FID. Additionally, a 3-layer discriminator yields the best joint performance, proving a balanced discriminator is essential for capturing the true data distribution.

**Q4: TimeMoE Backbone Version**
We utilize **TimeMoE-Base**. Its MoE architecture perfectly balances high capacity with efficiency. While total parameters are ~100M, the active parameters per token are only **~50M**.

**Q5: High-Dim VQ Stability & Intuition**
High dimensionality ($d=768$) prevents severe information bottlenecks, preserving the rich, multi-domain semantics extracted from the massive 300B corpus. Low-dim bottlenecks like $d=64$ caused "spectral bias" in early tests, failing to capture high-frequency transients. To prevent codebook collapse and ensure stability in high-dim space, we apply **$\ell_2$ normalization** to both encoder outputs and embeddings. This projects features to a unit hypersphere for stable cosine similarity lookup. We also utilize standard **EMA** for robust codebook updates.

We hope these comprehensive SOTA comparisons, rigorous decontamination proofs, and expanded multi-metric ablations thoroughly address your concerns. If our rebuttal and additional experiments have resolved your doubts, we respectfully request you to consider raising the score.