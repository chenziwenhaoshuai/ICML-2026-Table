### Table R1: Step-wise Component Ablation Study
*Demonstrating the modular-sequential design logic of TimeVQGAN and MoVE.*

| Configuration (Incremental) | Rec. MSE ↓ | $\Delta_{Rec}$ | ETT-h1 MSE ↓ | $\Delta_{Pred}$ |
| :-------------------------- | :--------- | :------------- | :----------- | :-------------- |
| **Full Model** (TimeVQGAN+MoVE) | **0.0896** | - | **0.421** | - |
| w/o Adversarial Loss (GAN)  | 0.8732     | +0.7836        | 1.037        | +0.616          |
| w/o Time-SWAG               | 0.1017     | +0.0121        | 0.427        | +0.006          |
| w/o MoVE (Single Scale)     | -          | -              | 0.432        | +0.011          |

---

### Table R2: Codebook Utilization and Downstream Performance
*Quantifying the intrinsic quality of the learned discrete representations. TimeVQGAN achieves near-perfect utilization, preventing index collapse.*

| Model Configuration      | Training Objectives | **Codebook Utilization (%)** ↑ | **ETT-h1 MSE** ↓ |
| :----------------------- | :------------------ | :----------------------------- | :--------------- |
| **TimeVQVAE** (Baseline) | MSE                 | 48.7%                          | 0.427            |
| **TimeVQGAN** (Ours)     | MSE + Adv + Perc    | **99.3%**                      | **0.421**        |

---

### Table R3: Emergent Frequency Decoupling (IoU of Active Indices)
*Intersection over Union (IoU) of the Top-50 active codebook indices across different frequency bands (B1-Low to B4-High). The near-zero overlap between B1 and B4 proves the shared codebook spontaneously partitions its latent space.*

| Dataset   | B1 (Low) vs B2 | B1 vs B3 | B1 (Low) vs B4 (High) | B2 vs B3 | B2 vs B4 | B3 vs B4 |
| :-------- | :------------- | :------- | :-------------------- | :------- | :------- | :------- |
| **ETTh1** | 0.0000         | 0.0000   | **0.0000**            | 0.1364   | 0.0870   | 0.2987   |
| **ETTh2** | 0.0526         | 0.0204   | **0.0204**            | 0.0204   | 0.0204   | 0.1765   |
| **ETTm1** | 0.0000         | 0.0000   | **0.0000**            | 0.1905   | 0.1111   | 0.2987   |
| **ETTm2** | 0.1628         | 0.0417   | **0.0417**            | 0.1236   | 0.0870   | 0.2987   |
| **Mean**  | 0.0539         | 0.0155   | **0.0155**            | 0.1177   | 0.0764   | 0.2681   |

---

### Table R4: Impact of Curriculum Learning Strategy
*Ablation showing that the "Structural Initialization" phase is a necessary condition to prevent catastrophic index collapse during large-scale pre-training.*

| Training Strategy          | Rec. MSE ↓ | **Codebook Utilization (%)** ↑ | **Downstream (ETT-h1 MSE)** ↓ |
| :------------------------- | :--------- | :----------------------------- | :---------------------------- |
| **W/O Curriculum**         | 0.9412     | **1.3%**                       | N/A                           |
| **With Curriculum (Ours)** | **0.0896** | **99.3%**                      | **0.421**                     |

---

### Table R5: Expert Pair Co-occurrence Frequencies in MoVE Routing
*Statistics of dynamic routing behavior using Top-k=2. Expert 1 represents the finest granularity (smallest stride), and Expert 4 represents the coarsest granularity (largest stride).*

| Expert Pair | ETTm2 (Co-occurrence %) | Traffic (Co-occurrence %) |
| :---: | :---: | :---: |
| **(1, 2)** | 6.2% | **42.5%** |
| **(3, 4)** | **40.1%** | 5.8% |
| **(1, 4)** | 11.5% | 13.2% |
| **(2, 3)** | 15.2% | 16.4% |
| **(2, 4)** | 19.8% | 8.6% |
| **(1, 3)** | 7.2% | 13.5% |

