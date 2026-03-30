
## 1 Random vs. Pre-trained Initialization
| Model Configuration              | Encoder Init | Training Steps | ETTh1 (MSE/MAE)   | Weather (MSE/MAE) |
| :------------------------------- | :----------- | :------------- | :---------------- | :---------------- |
| TimeVQGAN (Standard Transformer) | Random       | 1M             | 0.445 / 0.450     | 0.245 / 0.280     |
| TimeVQGAN (TimeMoE backbone)     | Random       | 1M             | 0.435 / 0.442     | 0.238 / 0.275     |
| TimeVQGAN (TimeMoE backbone)     | Random       | 1.5M           | 0.423 / 0.437     | 0.231 / 0.279     |
| TimeVQGAN (TimeMoE backbone)     | Pre-trained  | 1M (Ours)      | **0.421 / 0.432** | **0.227 / 0.267** |

## 2 Efficiency Benchmark
| Model           | Trainable Params | Training Time / Step (s) ↓ | Inference Time / Step (s) ↓ |
| :-------------- | :--------------- | :------------------------- | :-------------------------- |
| iTransformer    | 100M             | 0.109                      | 0.024                       |
| PatchTST        | 99M              | 2.16                       | 0.701                       |
| TimeMoE-B       | 113M             | 0.840                      | 0.095                       |
| **MoVE (Ours)** | **100M**         | **0.262**                  | **0.152**                   |