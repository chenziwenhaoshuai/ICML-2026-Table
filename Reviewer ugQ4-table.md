
### Table R1: Step-wise Component Ablation Study (Causal Link of Adversarial Training)
*Demonstrating the direct causal impact of each architectural component on both reconstruction fidelity and downstream forecasting performance. Removing the GAN loss causes catastrophic failure, proving its necessity.*

| Configuration (Incremental)     | Rec. MSE ↓ | $\Delta_{Rec}$ | ETT-h1 MSE ↓ | $\Delta_{Pred}$ | Qualitative Behavior                    |
| :------------------------------ | :--------: | :------------: | :----------: | :-------------: | :-------------------------------------- |
| **Full Model** (TimeVQGAN+MoVE) | **0.0896** |       -        |  **0.421**   |        -        | Balanced fidelity and generalizability. |
| w/o Adversarial Loss (GAN)      |   0.8732   |    +0.7836     |    1.037     |     +0.616      | Loss of volatility and structure.       |
| w/o Time-SWAG                   |   0.1017   |    +0.0121     |    0.427     |     +0.006      | Suffers from feature collapse.          |
| w/o MoVE (Single Scale)         |     -      |       -        |    0.432     |     +0.011      | Inability to adapt to local complexity. |

---

### Table R2: Tokenizer Strategy Comparison (Efficiency and Fidelity)
*A controlled experiment comparing TimeVQGAN against Uniform Binning (used in Chronos) with an identical downstream GPT-2 backbone. TimeVQGAN acts as a temporal compressor, drastically reducing VRAM and training time while achieving better forecasting accuracy.*

| Tokenizer Strategy   | Seq Length (L) | Token Length (N) | Downstream Training Time | GPU VRAM (Inference) | ETTh1 MSE ↓ |
| :------------------- | :------------: | :--------------: | :----------------------: | :------------------: | :---------: |
| Uniform Binning      |      512       |       512        |       3.46$\times$       |       0.66 GB        |    0.428    |
| **TimeVQGAN (Ours)** |    **512**     |     **128**      |     **1.00$\times$**     |     **0.51 GB**      |  **0.421**  |

---

### Table R3: Computational Cost and Scalability Benchmark
*Comparing the training and inference efficiency of MoVE against SOTA continuous models scaled to a comparable ~100M parameter budget. MoVE avoids the $O(N^2)$ explosion of PatchTST, proving its high accessibility.*

| Model           | Trainable Params | Training Time / Step (s) ↓ | Inference Time / Step (s) ↓ |
| :-------------- | :--------------: | :------------------------: | :-------------------------: |
| iTransformer    |       100M       |           0.109            |            0.024            |
| PatchTST        |       99M        |           2.160            |            0.701            |
| TimeMoE-B       |       113M       |           0.840            |            0.095            |
| **MoVE (Ours)** |     **100M**     |         **0.262**          |          **0.152**          |

