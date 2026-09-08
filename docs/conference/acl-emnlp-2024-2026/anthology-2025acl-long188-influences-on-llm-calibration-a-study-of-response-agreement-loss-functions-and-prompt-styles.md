---
title: "Influences on LLM Calibration: A Study of Response Agreement, Loss Functions, and Prompt Styles"
title_zh: 大语言模型校准的影响因素：响应一致性、损失函数与提示风格研究
authors: "Yuxi Xia, Pedro Henrique Luz De Araujo, Klim Zaporojets, Benjamin Roth"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.188.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 跨提示风格与模型规模研究LLM校准时引入响应一致性的作用
tldr: 以往LLM校准研究很少检验方法在不同提示风格和不同规模模型上的泛化能力。作者搭建覆盖12种LLM和四种提示风格的可控实验，并研究引入多个LLM响应一致性以及合适损失函数对置信度估计的改善。据此提出Calib-n框架，训练辅助模型融合多模型响应来估计置信度，优化校准效果。结果为跨模型、跨提示可靠置信度估计器的构建提供了系统性依据。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1625, \"height\": 589, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 784, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 707, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1648, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1643, \"height\": 773, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1631, \"height\": 1014, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1636, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1634, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1644, \"height\": 665, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1645, \"height\": 668, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long188/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1642, \"height\": 668, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1625, \"height\": 1708, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1564, \"height\": 776, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1631, \"height\": 2434, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1624, \"height\": 1802, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1617, \"height\": 2444, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1623, \"height\": 1802, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1616, \"height\": 2441, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1624, \"height\": 1801, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long188/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1617, \"height\": 2413, \"label\": \"Table\"}]"
motivation: 现有LLM校准方法很少检验其在不同提示风格和不同规模模型上的泛化能力。
method: 搭建12种LLM与四种提示风格的可控实验，提出Calib-n框架，训练辅助模型聚合多个LLM响应一致性进行置信度估计。
result: 发现响应一致性与适当损失函数可提升校准性能，且方法对提示与模型规模更为鲁棒。
conclusion: 为构建跨模型、跨提示风格的可靠LLM置信度估计器提供了系统性依据。
---

## Abstract
Calibration, the alignment between model confidence and prediction accuracy, is critical for the reliable deployment of large language models (LLMs). Existing works neglect to measure the generalization of their methods to other prompt styles and different sizes of LLMs. To address this, we define a controlled experimental setting covering 12 LLMs and four prompt styles. We additionally investigate if incorporating the response agreement of multiple LLMs and an appropriate loss function can improve calibration performance. Concretely, we build Calib-n, a novel framework that trains an auxiliary model for confidence estimation that aggregates responses from multiple LLMs to capture inter-model agreement. To optimize calibration, we integrate focal and AUC surrogate losses alongside binary cross-entropy. Experiments across four datasets demonstrate that both response agreement and focal loss improve calibration from baselines. We find that few-shot prompts are the most effective for auxiliary model-based methods, and auxiliary models demonstrate robust calibration performance across accuracy variations, outperforming LLMs’ internal probabilities and verbalized confidences. These insights deepen the understanding of influence factors in LLM calibration, supporting their reliable deployment in diverse applications.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLM）的校准问题——即模型对其预测的置信度与预测真实准确率之间的一致性问题。校准不良会导致模型在医疗、法律、教育等高风险领域中传播错误信息、放大偏见并引发用户的过度依赖。
- **现有研究的不足**：
  - 许多已有方法（如 Liu et al., 2024 的线性层调整方法）只能用于权重可访问的 LLM，实用性受限；
  - Ulmer et al. (2024) 提出的 APRICOT 辅助模型方法仅基于单个目标 LLM 的生成结果，且只在 2 个 LLM 和 2 种提示风格上评估，泛化性证据不足；
  - LLM 自身难以在自然语言中准确表达内部置信度（尤其是 verbalized confidence）。
- **本文的研究意义**：填补了以往研究未系统考察"方法在不同模型规模与不同提示风格下的泛化能力"这一空白，并首次在 LLM 校准中探索响应一致性（response agreement）、损失函数（loss functions）和提示风格（prompt styles）三者的综合影响。

### 2. 论文提出的方法论

- **总体框架名称**：Calib-n（n 表示提供响应的目标 LLM 数量）
- **核心思想**：训练一个独立的辅助模型（auxiliary model）来估计目标 LLM 的置信度。辅助模型不仅看到单个模型的问题-答案对，还能同时看到多个 LLM 对同一问题的回答，从而捕捉**模型间的一致性（inter-model agreement）**——当多个模型回答不一致时，辅助模型可推断出更高的不确定性，从而抑制单个模型固有的过度自信。
- **核心技术细节**：
  - **辅助模型结构**：由 transformer 骨干（bert-base-uncased, 110M 参数）、分类头（n×768 → n）和 sigmoid 激活函数组成；
  - **输入构造**：将 n 个"问题+回答"对分别以 `q[SEP]ai` 的形式拼接（如 `What is the capital of France?[SEP]Paris`），每个回答独立经过编码后再在模型中聚合；
  - **答案正确性的标注**：使用开源裁判模型 Prometheus-8x7b-v2.0 对每个 LLM 生成的答案与标准答案进行语义等价判断，输出二元正确性标签 ci；
  - **三种损失函数**：
    1. **BCE（二元交叉熵）**：最小化预测概率与答案正确性之间的平均交叉熵；
    2. **Focal Loss (FL)**：降低易分类样本的权重，使模型聚焦于"置信度与正确性差距大"的困难样本（默认 α=0.25, γ=2.0）；
    3. **AUC Surrogate Loss**：通过 logistic loss 最大化正样本与负样本 logit 得分之差，直接优化 AUC。
- **方法变体**：
  - `(BCE)/(FL)/(AUC)Calib-1`：仅使用单个目标 LLM 的响应训练辅助模型；
  - `(BCE)/(FL)/(AUC)Calib-n`：使用同组多个 LLM 的响应训练辅助模型；
  - `(BCE)/(FL)/(AUC)Calib-n+PS`：在辅助模型输出的概率基础上，进一步进行 Platt Scaling 后处理校准。

### 3. 实验设计

- **数据集（4 个开放域问答数据集）**：
  - TriviaQA、Sciq、WikiQA、NQ（Natural Questions）
  - 训练/测试样本划分：TriviaQA、Sciq、NQ 各约 2k/1k；WikiQA 为 1040/293。
- **被校准的目标 LLM（12 个，来自 5 个模型家族）**：
  - **小模型（2–9B 参数，7 个）**：Llama2-7b、Llama3-8b、Llama3.1-8b、Phi3-4b、Phi3-7b、Gemma2-2b、Gemma2-9b；
  - **大模型（27–72B 参数，5 个）**：Qwen2-72b、Llama3-70b（文中也称 Llama3-72b）、Llama3.1-70b、Mixtral-8x7b、Gemma2-27b。
- **提示风格（4 种）**：Verbalized（要求给出概率）、Zero-shot、Chain-of-Thought (CoT)、Few-shot。
- **评价指标（4 种）**：ECE、ECE-t、Brier Score、AUC。
- **对比的基线方法**：
  - LLM 内部条件概率（LLM Prob.）；
  - LLM 概率 + Platt Scaling (LLM Prob.+PS)；
  - Verbalized confidences（模型用自然语言明确表述的置信度百分比）；
  - APRICOT（Ulmer et al., 2024，基于聚类的辅助模型校准方法）。

### 4. 资源与算力

- **辅助模型训练**：BERT-base（1.1 亿参数），学习率 1e-5，batch size 16，共训练 5 个 epoch；
- **训练耗时**：2k 条样本每轮约 200 秒（单 GPU），总时长随数据集大小和参与训练的 LLM 数量而变化；
- **硬件**：全部实验（含 LLM 推理）在最多 2 张 NVIDIA H100 GPU 上完成；
- 论文未额外披露更细粒度的总 GPU 小时数或能耗数据。

### 5. 实验数量与充分性

- **实验规模较大**：12 个 LLM × 4 个数据集 × 4 种提示风格 ×（10 种方法左右），生成了大量细粒度结果（正文和附录共报告 9 张完整表格，含每个模型-数据集-提示配置的 4 指标结果）；
- **统计聚合分析**：通过"获胜次数"（wins）统计对所有配置下的方法表现进行汇总对比，并分别从提示风格、模型规模、数据集三个维度给出分组聚合结果，增强了结论的客观性；
- **辅助分析**：包含可靠性图（reliability diagrams）、准确率-ECE 相关性分析、域外（out-of-domain）泛化实验，多个角度互为印证；
- **总体评价**：实验覆盖维度广、数量充足、对比公平（提示风格在各方法间保持一致）。不过，论文也明确指出不存在一个在所有设置下都一致最优的方法，因此结论主要以"多数胜场"的形式给出——这是对真实复杂性的客观呈现。

### 6. 论文的主要结论与发现

- **响应一致性的作用**：利用多 LLM 响应一致性的 Calib-n 方法整体优于现有最优基线；在 BCE 损失下，Calib-n 在多数设置中优于 Calib-1；
- **损失函数的作用**：Focal Loss 相比 BCE 和 AUC 损失能更有效地改善校准，它在 Calib-1 与 Calib-n 上均有效；综合比较下 **(FL)Calib-1 是整体最优的方法**；
- **提示风格的作用**：Few-shot 提示带来的校准效果最好，其次为 CoT；Verbalized 与 Zero-shot 相对较弱。提示风格对辅助模型类方法的校准影响显著；
- **准确率-校准相关性的鲁棒性**：LLM 内部概率、Platt Scaling 后的概率以及 verbalized confidence 的 ECE 随准确率波动明显（准确率越高 ECE 越低，二者高度相关）；而 APRICOT 和 Calib-* 辅助模型在准确率变化时保持稳定的校准表现；
- **最佳方法随准确率区间变化**：(FL)Calib-1 在低准确率（≤50%）区间最优，Calib-n+PS 在中准确率（50–70%）区间最优，LLM Prob.+PS 在高准确率（>70%）区间最优；
- **LLM 自身的置信度表达缺陷**：Verbalized confidence 在所有准确率水平上表现最差，进一步证实了 LLM 在自然语言中表达不确定性方面的困难。

### 7. 优点

- **实验设计上的广度和系统性**：覆盖 12 个 LLM（2B–72B）、4 个数据集、4 种提示风格，是目前 LLM 校准研究中规模较全面的实证分析之一；
- **方法创新性**：首次将多模型响应一致性引入 LLM 置信度校准，训练一个辅助模型即可同时为多个目标 LLM 提供校准置信度，节省了分别训练多个校准模型的算力成本；
- **损失函数的迁移验证**：将 focal loss 与 AUC surrogate loss 从传统神经网络校准场景迁移到 LLM 辅助校准场景并验证其有效性；
- **对比公平性**：在统一提示风格下比较各方法，避免了以往研究中"提示风格不一致导致对比不公"的问题；
- **客观呈现不确定性**：论文坦诚报告"没有单一方法在所有配置下一致最优"，符合实证研究的真实结果，增强了结论的可信度。

### 8. 不足与局限

- **提示覆盖有限**：虽然覆盖了 4 种主流通用提示类型，但未探索更细粒度的提示变体、自动生成的提示或更多任务导向的提示工程，提示与校准之间的深层交互仍有待研究；
- **评价指标范围**：仅使用 ECE、ECE-t、Brier、AUC 等聚合式校准指标，未必能完全刻画校准质量的所有维度（如用户感知的置信度、任务特定的效用）；
- **正确性标注机制的偏差风险**：使用 Prometheus-8x7b-v2.0 作为答案裁判模型，尽管其与人类评判相关性较高，但"LLM 评估 LLM"仍可能存在系统性偏差；论文也承认最优的答案正确性判定方式仍是一个开放问题（其他工作使用 extract match、ROUGE 等方式）；
- **域外泛化表现下降**：附录中的 out-of-domain 实验显示，跨数据集训练（如用其他三个数据集训练再在 TriviaQA 上测试）的辅助模型在多数设置下存在性能下降，尽管未出现灾难性退化；
- **语言和任务覆盖**：仅在英文开放域问答数据集上评测，未覆盖多语言、多任务（如长文本生成、对话、检索等）场景；
- **辅助模型本身的代价**：Calib-n 虽然共享单个辅助模型，但仍需要一个外部可训练的神经网络（BERT-base）和有标注数据集，这在纯黑盒、低资源场景下仍构成部署门槛；
- **PLS 后处理的不一致性**：Platt Scaling 虽能降低 ECE-t，但并未普遍提升整体校准表现（Calib-n+PS 在多数设置中反而劣于未缩放版本），说明后处理与辅助模型的结合仍需要更精细的调适策略。

（完）
