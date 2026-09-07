---
title: Logit Space Constrained Fine-Tuning for Mitigating Hallucinations in LLM-Based Recommender Systems
title_zh: 基于Logit空间约束微调的LLM推荐系统幻觉缓解
authors: "Jianfeng Deng, Qingfeng Chen, Debo Cheng, Jiuyong Li, Lin Liu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1491.pdf"
tags: ["query:faithfulness"]
score: 4.0
evidence: 利用正负指令对及KL散度在logit空间进行约束微调以缓解LLM幻觉，属于幻觉抑制的微调技术
tldr: 推荐系统引入大语言模型后面临严重幻觉，标准微调常常忽略此问题。作者提出LCFT，输入语义正负指令对并把KL散度纳入训练目标，在微调时对logit空间施加显式约束，缓解推荐内容的幻觉。该框架为LLM推荐提供更可靠的微调范式，其对输出概率分布的约束思想也适用于其他生成任务。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1491/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 772, \"height\": 254, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1491/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1612, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1491/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 761, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1491/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 762, \"height\": 471, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1491/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 816, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1491/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1491/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1407, \"height\": 470, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1491/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1660, \"height\": 1068, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1491/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 742, \"height\": 498, \"label\": \"Table\"}]"
motivation: LLM推荐系统易产生幻觉，常规微调未针对性抑制，导致推荐结果准确性下降。
method: 以语义正反指令对为训练样本，引入KL散度约束logit空间，使模型输出尽量靠近正确语义分布。
result: 相较于标准微调，LCFT能缓解生成内容幻觉，提升推荐结果的可靠性与准确性。
conclusion: 约束微调可有效治理推荐场景的幻觉，为生成式模型的忠实输出提供参考。
---

## Abstract
Large language models (LLMs) have gained increasing attention in recommender systems, but their inherent hallucination issues significantly compromise the accuracy and reliability of recommendation results. Existing LLM-based recommender systems predominantly rely on standard fine-tuning methodologies, often ignoring hallucination issues during the fine-tuning process. To address this challenge, we propose Logit Space Constraints Fine-Tuning (LCFT), a novel fine-tuning framework designed to mitigate hallucination in LLM-based recommenders. Specifically, LCFT takes as input semantically positive and negative instruction pairs and incorporates Kullback–Leibler (KL) divergence into the training objective to explicitly maximise their distributional disparity in the logit space. By conducting such logit space-constrained fine-tuning, LCFT encourages more distinguishable and semantically grounded representations, thereby reducing the model’s susceptibility to hallucination. Extensive experiments on two recommendation models with distinct LLM backbones and four real-world datasets demonstrate that LCFT consistently reduces hallucination and enhances recommendation performance.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- 大型语言模型（LLM）在推荐系统中应用日益广泛，但模型固有的**幻觉问题**会严重损害推荐结果的准确性和可靠性。

- 现有的LLM推荐系统大多依赖标准微调方法（如LoRA），但这些**微调过程往往忽略了幻觉问题**，导致模型在面对语义相反的指令时可能产生相同或逻辑矛盾的输出，其行为更像“猜测”而非真正的“理解”，削弱了推荐系统的可信度和实用价值。

## 2. 方法论

- **核心思想**：提出Logit Space Constrained Fine-Tuning（LCFT），一种融合对比指令微调（contrastive instruction tuning）与logit空间约束的幻觉缓解方法。

- **关键技术细节**：构造语义相反的正/负指令对。例如，“用户会喜欢这个物品吗？”为正指令；“用户会不喜欢这个物品吗？”为负指令。负指令由正指令语义反转而来，输入上下文保持不变；基于正负指令对，将**KL散度项纳入训练目标**，在微调中最大化正负指令间logit分布的差异；在微调时使用**参数高效微调技术LoRA**进行，以降低显存占用和计算成本。

- **核心公式与算法**：训练目标函数由两部分组成：
  - 原生的LoRA微调目标：`LLoRA = min Θ − Σ (X,Y)∈Z Σ_t log PΦ+Θ(Yt | X, Y<t)`（标准交叉熵/语言建模损失）
  - KL散度约束目标：`LKL = min Θ − Σ (Xpos, Xneg, Y)∈Z Σ_t DKL(PΦ+Θ(Yt | Xpos, Y<t) ‖ PΦ+Θ(Yt | Xneg, Y<t))`（帮助模型在logit层面区分语义相反的指令）
  - 最终目标：`LCFT = LLoRA + λ · LKL`，通过权重λ平衡两个目标。模型通过`λ`控制KL约束权重，使得logit空间中正负指令分布保持分离，输出概率分布可分辨，增强模型对指令语义的敏感度，从而降低幻觉。

## 3. 实验设计

- **数据集与场景**：
  - 少样本（few-shot）训练场景：在 movie（MovieLens-100K）和 book（BookCrossing）两个数据集上进行；
  - 全量样本（full-shot）训练场景：在 ML-1M 和 Amazon-Book 两个数据集上进行；
  - 两个场景分别用于验证不同数据稀缺程度下的效果，覆盖不同领域（电影/图书）、不同规模的数据集。

- **Benchmark与基线模型**：
  - 传统推荐模型：GRU4Rec、Caser、SASRec、DROS、GRU-BERT、DROS-BERT；
  - 基于深度学习的经典模型：MF、LightGCN；
  - LLM推荐系统基线：ICL、Prompt4NR-V、TALLRec（LLaMA-7B）、CoLLM-MF（Vicuna-7B）；
  - 评估指标：AUC 与 UAUC 用于进行模型效果对比。

## 4. 资源与算力

- 论文指出，实验使用了 LLaMA-7B 与 Vicuna-7B 两个约7B参数的模型作为LLM底座；
- 训练在配备单张 **NVIDIA GeForce RTX 4090 GPU（24GB VRAM）** 的服务器上完成，操作系统为Ubuntu 22.04；
- 采用LoRA进行参数高效微调，总训练时长**约16个GPU小时**；
- 计算资源整体需求不高，与全参数微调7B模型相比，训练成本相对可控。

## 5. 实验数量与充分性

- 所做的实验包括：
  1. **少样本设置下的性能对比**（movie与book，shots = 16、64、256，对应10个基线模型）；
  2. **全量设置下的性能对比**（ML-1M与Amazon-Book，对应9个基线模型）；
  3. **两种不同LLM底座上的泛化性验证**（LLaMA-7B和Vicuna-7B）；
  4. **定性案例研究**（MovieLens-100K场景下用户输出的对比）；
  5. **消融实验**（移除LCFT约束后，在movie和book上AUC对比）；
  6. **超参数敏感性分析**（不同λ取值在movie和book上对AUC的影响）；
  - 总体上看，实验范围覆盖两代主流推荐模型、多类型基线、多样数据集、少样本/全量两种训练设置，多个维度互相印证。论文未报告每次实验的随机种子具体数值，但说明“每种方法运行5次并汇报平均结果”，并使用固定划分的数据集（TALLRec或CoLLM设置），因此**总体上实验较为客观、公平、充分**。

## 6. 主要结论与发现

- 在少样本和全量训练中，LCFT在多数情况下均优于标准微调的LLM推荐基线，平均相对提升稳定；
- 传统微调难以缓解LLM固有的幻觉问题，加入logit空间约束可以显著提升模型的判别能力，减少对语义相反输入的“无差别处理”；
- 将LCFT整合到不同架构（LLaMA-7B、Vicuna-7B）的LLM推荐系统中都能保持一致的性能增益，说明LCFT具有较好的通用性；
- 定性案例显示，标准微调会对“喜欢”和“不喜欢”同一物品给出相同的回答参考，而LCFT能正确输出可区分的不同结果；
- 超参数λ需要取合适值；过大或过小都会带来性能下降，不同数据集的敏感区间不同。

## 7. 优点

- 提出了一种具有**可解释性、可验证性的推荐幻觉定义**：对语义相反的指令（喜欢/不喜欢）给出相同或逻辑上不一致的回答则视为幻觉；
- 该框架不修改原有任务数据或添加显式负面反馈，可**灵活集成到任意现有LLM推荐微调流程中**，具备较强的泛化性；
- 将对比学习约束从表征层迁移至**logit分布层**，在微调时显式扩大语义差异，训练过程引入了额外的可解释约束；
- 仅采用LoRA，显著降低了参数训练成本，同时保持较好的推荐性能和幻觉缓解效果；
- 在少样本设置下的结果显示，LCFT还能缓解**冷启动、数据稀疏**下的幻觉和推荐退化问题，具有实际应用价值。

## 8. 不足与局限

- **对比性依赖限制**：LCFT依赖正/负指令的可清晰对比性，但是实际推荐中部分物品与用户关系的语义极性可能不是绝对对立，存在“对比性不明”的使用场景局限；
- **过度自信风险**：最大化KL散度虽然增强了分布可区分性，但对某些输入可能造成模型产生过度自信或预测不稳的问题，需要谨慎解释输出置信度；
- **语言与群体覆盖不足**：目前实验全部局限于英语数据集，面向其他语言、领域、以及代表性不足的用户群体，其泛化能力尚未验证；
- **公平性问题未探讨**：在当前实验中没有分析引入LCFT后是否可能放大或引入性别、种族等敏感属性相关的偏见，在模型公平性上仍需进一步分析和验证；
- **未来方向**：与因果推断方法结合只是设想的后续规划，现阶段未给出相应验证。

---

（完）
