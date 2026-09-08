---
title: "When to Trust LLMs: Aligning Confidence with Response Quality"
title_zh: 何时信任大语言模型：使置信度与回复质量对齐
authors: "Shuchang Tao, Liuyi Yao, Hanxing Ding, Yuexiang Xie, Qi Cao, Fei Sun, Jinyang Gao, Huawei Shen (沈华伟), Bolin Ding"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.357.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: CONQORD通过强化学习与保序奖励将模型置信度与回复质量对齐，直接校准模型可信度
tldr: 本文针对大语言模型置信度与回复质量不一致、难以判断何时可信的问题，提出CONQORD方法。它利用强化学习，结合质量奖励和保序对齐奖励，训练模型让口头表达的置信度高低与回复质量的好坏顺序一致。实验表明，该方法显著改进置信度与质量的排序一致性，有助于更可靠地决定何时信任模型输出。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl357/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 643, \"height\": 812, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl357/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl357/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 496, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl357/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 807, \"height\": 504, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl357/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1621, \"height\": 820, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl357/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1621, \"height\": 819, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl357/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1475, \"height\": 796, \"label\": \"Table\"}]"
motivation: LLM的置信度不能可靠反映回复质量，限制高风险场景下的可信使用。
method: 使用基于质量奖励和保序对齐奖励的强化学习，训练模型按质量顺序表达置信度。
result: CONQORD改善了置信度与回复质量的排序一致性，明显增强对LLM可靠性的判断。
conclusion: 通过与质量对齐的置信度训练，可让模型更可信地表示何时被信任。
---

## Abstract
Despite the success of large language models (LLMs) in natural language generation, much evidence shows that LLMs may produce incorrect or nonsensical text. This limitation highlights the importance of discerning when to trust LLMs, especially in safety-critical domains. Existing methods often express reliability by confidence level, however, their effectiveness is limited by the lack of objective guidance. To address this, we propose CONfidence-Quality-ORDer-preserving alignment approach (CONQORD), which leverages reinforcement learning guided by a tailored dual-component reward function. This function integrates quality reward and order-preserving alignment reward functions. Specifically, the order-preserving reward incentivizes the model to verbalize greater confidence for responses of higher quality to align the order of confidence and quality. Experiments demonstrate that CONQORD significantly improves the alignment performance between confidence and response accuracy, without causing over-cautious. Furthermore, the aligned confidence provided by CONQORD informs when to trust LLMs, and acts as a determinant for initiating the retrieval process of external knowledge. Aligning confidence with response quality ensures more transparent and reliable responses, providing better trustworthiness.

---

## 论文详细总结（自动生成）

好的，我理解您的要求。下面是对论文《When to Trust LLMs: Aligning Confidence with Response Quality》的结构化中文总结。

---

# 论文详细总结

## 🎯 1. 核心问题与研究动机

- **核心痛点**：LLM 虽然能生成流畅文本，但经常产生事实性错误或荒谬内容，尤其在安全敏感领域（如医疗、引用真实性）存在风险，因此**如何判断模型何时值得被信任**成为一个关键问题。
- **现有方案缺陷**：现有置信度校准方法（如利用多次生成的一致性、Top-k 召回概率等）多基于启发式假设，**缺乏能够直接反映回复质量的"置信度金标准"**，导致置信度与真实回复质量之间存在系统性错位——模型可能对低质量回复给出过度自信的判断。
- **影响**：这种错位破坏了模型输出的透明性与可信赖性，并阻碍了在"依赖模型自身推理 vs 触发外部知识检索"之间做正确决策。
- **文章的核心回答**：通过强化学习，用显式的双组件奖励函数，使模型输出的口头化置信度**在顺序层面与回复质量保持一致**——即质量越好的回复被赋予更高的置信度，从而回答"何时可以信任 LLM"的问题。

## ⚙️ 2. 方法论

### 2.1 总体框架

- 文本生成被建模为**马尔可夫决策过程（MDP）**，采用 **强化学习（RL）** 框架对模型策略进行优化。与依赖于标注数据的 SFT 不同，RL 的核心优势在于**任意指标都可以作为奖励**——这为规避缺少置信度金标准问题提供了可能。
- 采用 **PPO（Proximal Policy Optimization）** 作为策略优化算法，并加入了 KL 散度惩罚项以控制策略偏离原始语言模型的程度。
- 提出方法：**CONQORD（CONfidence-Quality-ORDer-preserving alignment）**，即置信度-质量-保序对齐方法。

### 2.2 双组件奖励函数（Dual-Component Reward Strategy）

**① 质量奖励（Quality Reward）**

- 目标：准确评估回复质量，这是置信度对齐的前提。
- 实现：基于 RLHF（Helpful & Harmless）数据集（含 chosen/rejected 回复对）训练一个奖励模型 \(R_Q\)，用**二进制排序损失**（binary ranking loss）：
  - \(L_Q = -\log(\sigma(R_Q(x, y_h) - R_Q(x, y_l)))\)
  - 其中 \(y_h\) 为高质量（chosen）回复，\(y_l\) 为低质量（rejected）回复。

- 解决的问题：避免单个奖励模型同时评估"质量"与"对齐"时出现模型走捷径、选择退化行为——即生成低质量低置信度的回复来满足对齐要求。

**② 保序对齐奖励（Order-Preserving Alignment Reward）**

- 核心准则：对任意两个样本 \((x_i, y_i, c_i)\) 与 \((x_j, y_j, c_j)\)，理想的置信度与质量关系应该保持如下顺序关系（"黄金准则"）：
  - \(c_i \le c_j \iff R_Q(x_i, y_i) \le R_Q(x_j, y_j)\)
  - 即**质量越高的回复，其置信度水平也应该越高**。
- 奖励函数形式：
  - \(R_A(x_i, y_i, c_i) = \sum_{j \neq i} (c_i - c_j) \cdot (R_Q(x_i, y_i) - R_Q(x_j, y_j))\)
  - 该函数在置信度与质量排序一致时呈正反馈；当出现排序不一致（质量低但置信度高）的样本时，乘积为负，即被惩罚。
- 优势：（a）**只关注相对顺序而非绝对值**，对绝对的置信度尺度不敏感；（b）对异常高群点/离散点具有**鲁棒性**；（c）推动模型进行**细粒度自我评估**并适应不同上下文。

**③ 总奖励**

- \(R_O(x_i, y_i, c_i) = R_Q(x_i, y_i) + \alpha \cdot R_A(x_i, y_i, c_i)\)
- \(\alpha\) 为平衡两个目标的超参数（默认取 0.4）。

**④ 与朴素的 PreApproach 的差异**

- PreApproach 通过人工构造带固定极端置信度（0.1/0.9）的样本训练奖励模型来同时评价质量和对齐，实验结果发现虽然 ECE 降低，但模型**回复准确率明显退化**——模型学会了走捷径（降质量+降置信度）。
- CONQORD 解耦了两类评估，且不要求人工预定义置信度等级，避免二元化偏差，更鲁棒与泛化。

## 🧪 3. 实验设计

### 3.1 数据集与应用场景

- 两个 benchmark 数据集覆盖两种任务场景：
  - **TruthfulQA**（幻觉评估）：含 817 个问题，覆盖 38 个类别，测试模型模仿人类错误观念的倾向。
  - **Natural Questions / NQ**（开放域问答）：从 NQ 验证集中随机采样 500 条真实用户查询，以控制实验成本。
- 另外在**自适应检索（adaptive retrieval）**场景中验证了校准置信度对是否触发 RAG 的指导价值。

### 3.2 基座模型与基线方法

- **基座模型（4 个）**：LLAMA-2 7B、LLAMA-2 13B、Zephyr 7B、Mistral 7B。
- **基线方法（3 个）**：
  - **Vanilla**：直接提示模型输出 0~1 的置信度分数。
  - **Top-k**（Tian et al., 2023）：让模型生成 Top-K 个可能答案，并各自附带概率。
  - **CoT+Agg**（Xiong et al., 2023）：用思维链提示（Chain-of-Thought）引导推理后输出置信度。
- **评价指标（4 个）**：ECE（期望校准误差）、Pearson 相关系数、Spearman 秩相关系数、以及由 GPT-4 判断 Semantic Equivalence 得到的 Accuracy。

## 💻 4. 算力与训练配置

- 文中报告了硬件资源：**8 块 80G A100 GPU**。
- 优化器：AdamW；学习率恒定 \(10^{-6}\)；weight decay = 0.1。
- KL 惩罚系数 \(\beta = 0.005\)；\(\alpha = 0.4\)。
- 每轮 PPO batch size 为 32，每个 mini-batch 只做一次梯度更新。
- ⚠️ **说明**：论文**未明确报告具体训练时长**（小时数）或 PPO 迭代总轮数。

## 📊 5. 实验数量与充分性评估

### 实验矩阵概览

- 两大主实验表：Table 1（TruthfulQA）和 Table 2（NQ），覆盖 **4 个基础模型 × 4 种方法**，共 **32 组核心对比**，每组报告 ECE、PCC、SRCC、p 值和 Accuracy。
- 附加实验包括：
  1. **PreApproach 对比（图 2）**：验证朴素方法导致准确率下降。
  2. **自适应检索（图 3）**：验证置信度在 RAG 触发场景的指导作用（两个数据集各设一个阈值）。
  3. **超参数 \(\alpha\) 敏感性分析（图 4）**：在 0.0~1.0 范围内取 6 个值，对比 CONQORD 与 PreApproach。
  4. **案例研究（表 3）**：展示不同方法下具体问题的置信度-质量对齐情况。

### 充分性与公平性评价

- ✅ **多基座模型交叉验证**：覆盖了 7B 至 13B 的三种不同架构系列，增强了结论普适性。
- ✅ **全维度基线**：对比了无提示 Vanilla、Top-k 概率式方法和 CoT 提示方法三个主流方向。
- ✅ **多面齐全度量**：同时使用了基于分桶的校准度量（ECE）和基于相关性的度量（Pearson/Spearman），避免单度量偏差。
- ⚠️ **局限性**：实验只局限于 7B~13B 规模，未涉及 70B 级别的大规模模型；在 TruthfulQA 上 LLAMA-2 13B 的 ECE 改善并不显著；准确率提升有限，且部分情况下（如 Zephyr 7B、LLAMA-2 13B 在 NQ 上）精度略有下降。

## 📝 6. 主要结论与发现

1. **校准效果大幅提升**：CONQORD 在绝大多数场景下取得最低 ECE。最典型的是 **Mistral 7B**：在 TruthfulQA 和 NQ 上 ECE 分别从 0.3379/0.2258 降至 **0.0228/0.0276**（近乎完美校准）。在 LLAMA-2 7B 上 TruthfulQA 的 ECE 从 0.6327 降至 0.1856。
2. **避免了"过度谨慎"副作用**：与 PreApproach 相比，CONQORD 在提升校准的**同时没有牺牲回复精度**（accuracy 基本保持基座模型水平），没有诱导模型产生低质量低置信度的走捷径行为。
3. **保序对齐优于绝对对齐**：相对顺序约束比人工指定极端置信度（0.1 vs 0.9）更稳健且减少了偏差。
4. **校准置信度的实用性**：实验证明校准后的置信度可以作为判断**何时触发外部知识检索（RAG）**的有效信号。对于低置信度输出附加 RAG 可显著提高回答正确率；对高置信度输出引入 RAG 可能因检索噪音导致性能下降，因此选用合适阈值可避免多余检索并规避噪音。
5. 相关性地提升：在多数实验组中，CONQORD 的 Pearson/Spearman 相关系数显著为正且 p 值远低于 0.05，例如 Zephyr 7B 在 NQ 上均超过 0.29，表明置信度与质量之间存在统计显著的正相关关系。

## 🌟 7. 优点与创新亮点

- **清晰的动机链条**：从"缺少置信度金标准"这一核心难点切入，自然过渡到"用 RL 灵活奖励来桥接"，逻辑严密。
- **无监督式定义的保序准则**是一个优雅的核心设计：**不需要为每条回复标注一个具体的"完美置信度"数值**，只需要保持质量-置信度的排序一致性。这是一种弱监督/自监督的设计哲学，能有效规避主观打分偏差。
- **解耦质量与对齐的奖励设计**：双组件奖励机制避免了单个奖励模型优化时的"走捷径"问题，确保对齐的同时不降低回答质量。
- **广泛的多基座实验与多样指标**：四种不同源的基础模型、两大数据集、三套指标体系，外加自适应检索下游应用测试，呈现了较全面的效果验证。
- **方法具有应用延伸价值**：校准置信度可用作自适应检索、自我反思等下游任务的决策信号，具有很强的潜在实用面。

## 🚫 8. 不足与主要局限性

- **模型适用范围的限制**：CONQORD 依赖直接对模型权重进行 PPO 微调，**仅适用于开源模型**，对 API 型商业闭源模型（如 GPT-4）无法使用。
- **规模外推尚未验证**：论文仅验证了 7B~13B 参数量模型，**没有在更大规模（如 70B）模型上进行实验**，规模扩大后有效性未知。
- **效果存在模型间的差异**（天花板效应）：Zephyr 和 LLAMA-2 13B 在部分准确率指标上出现回落；LLAMA-2 13B 在 TruthfulQA 上的 ECE 虽优于 Vanilla 但不如 CoT+Agg，提示方法在部分模型上有提升空间。
- **评价者偏差风险**：Accuracy 使用 GPT-4 评判语义等价性，虽方便高效，但存在裁判模型自身引入的潜在系统性偏差，尚未提供人工复核的比例/一致性检查。
- **风险与权衡不完整**：置信度对齐后缺乏对"应拒绝回答"（abstention）机制的引入——文中虽然校准了置信度，但对极度低置信度回复仍没有明确的"不回答"策略（只在 RAG 中触发检索，若检索信息质量差如何规避仍需探讨）。
- **外部检索实验结果较简略**：只报告了单一阈值条件下的结果，没有讨论不同阈值下 RAG 触发率与最终精度的完整权衡曲线。
- **训练代价较高**：RLHF 式 PPO 训练需要大量 reward model 与 actor 计算开销，虽然没有给出精确时长，但可以推测成本不低。

（完）
