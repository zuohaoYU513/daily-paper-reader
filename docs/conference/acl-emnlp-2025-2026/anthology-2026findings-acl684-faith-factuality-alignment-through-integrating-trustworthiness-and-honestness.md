---
title: "FAITH: Factuality Alignment through Integrating Trustworthiness and Honestness"
title_zh: FAITH：通过整合可信度与诚实性实现事实性对齐
authors: "Xiaoning Dong, Chengyan Wu, Yajie Wen, Yu Chen, Yun Xue (薛云), Zhang Jing, Wei Xu, Bolei Ma"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.684.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: FAITH训练后对齐框架，结合自然语言不确定性与外部知识提升事实准确性
tldr: 大模型即便具备相关知识也可能生成不准确内容，现有方法在提示中加入数值不确定性分数，但语义不足。本工作提出FAITH训练后对齐框架，将自然语言形式的不确定性信号与外部知识整合进训练数据，使模型更好地理解自身的可信与诚实状态。实验表明其对齐效果优于数值置信度基线，显著提升事实正确性。该工作为事实性对齐提供了更语义化的训练范式。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl684/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1637, \"height\": 717, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl684/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 783, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl684/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 320, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl684/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 644, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl684/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 1332, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl684/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1653, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl684/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1649, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl684/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1654, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl684/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1506, \"height\": 1633, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl684/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1514, \"height\": 1347, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl684/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1508, \"height\": 1599, \"label\": \"Table\"}]"
motivation: 数值不确定性分数缺乏语义信息，难以让模型充分理解自身的可信与诚实状态。
method: 构建融合自然语言不确定性信号和外部知识的训练数据，进行后训练事实性对齐。
result: 实验验证FAITH在不同任务上提升了大模型输出的事实准确性。
conclusion: FAITH为事实性对齐提供了一种更具语义性的后训练框架。
---

## Abstract
Large Language Models (LLMs) can generate factually inaccurate content even if they have corresponding knowledge, which critically undermines their reliability. Existing approaches attempt to mitigate this by incorporating uncertainty in QA prompt during training, but these numerical scores lack the semantic richness for LLM to properly understand its internal states of trustworthiness and honestness, leading to insufficient factuality alignment. We introduce FAITH (Factuality Alignment through Integrating Trustworthiness and Honestness), a post-training framework for factuality alignment that integrates natural-language uncertainty signals with external knowledge. Specifically, we augment training datasets by computing confidence scores and semantic entropy from LLM outputs and mapping them into a knowledge state quadrant that describes the model’s internal knowledge possession (trustworthiness) and answering behaviors (honestness) in natural language. Based on this enhanced data, we design a reward function that considers both correctness and uncertainty signals, and fine-tune the LLM using the Proximal Policy Optimization (PPO) algorithm. To further mitigate weakly grounded responses, we design a retrieval-augmented module that retrieves relevant external passages, improving the consistency between internal and external knowledge representations. Extensive experiments on four knowledge-intensive benchmarks demonstrate that FAITH enhances the factual accuracy and truthfulness of LLMs.

---

## 论文详细总结（自动生成）

# FAITH：通过整合可信度与诚实性实现事实性对齐

## 一、核心问题与整体含义（研究动机与背景）

大型语言模型（LLMs）即使在其内部知识库中已经包含了回答问题所需的正确事实，仍然可能生成事实性错误的内容。这种"知道但说不出来"或"知道但答错"的现象，被称为"知-说鸿沟"（know–tell gap），严重损害了模型在高风险领域（如法律、教育、临床）中的可靠性。

现有的事实事后对齐方法（如 UAlign）虽然已尝试将不确定性纳入问答提示中进行训练，但存在三个关键缺陷：

- **数值不确定性缺乏语义丰富性**：直接在提示中注入诸如 `Conf: 0.833` 或 `Entro: -0.5` 之类的原始数字，模型难以充分理解和利用这些抽象信号。
- **二元奖励函数过于粗糙**：只关注回答是否正确，忽视了模型内部的置信度/不确定性，可能间接鼓励模型"猜测"。
- **忽视外部知识的作用**：单纯依赖模型内部参数化知识，未利用外部语料来纠正潜在的错误回答。

## 二、方法论：FAITH 框架

### 核心思想

FAITH 是一个事后训练（post-training）框架，通过整合自然语言形式的不确定性信号与外部检索知识，实现大模型的事实性对齐（factuality alignment）。其核心创新在于将不可解释的数值不确定性映射为可解释的、自然语言描述的"知识状态"（knowledge state），并以此指导策略模型的行为。

### 关键技术细节

**（1）训练数据增强（Uncertainty Estimation & Mapping）**

- 对每个问题 $x_i$，使用 $K$ 个不同的 one-shot 示例采样得到 $K$ 个响应 $Y_i = \{y_i^k\}_{k=1}^K$（主要实验中 $K=6$）。
- 估计两个不确定指标：
  - **一致性（Consistency）**：基于正确匹配（PREM）的比例，反映知识占有（knowledge possession）。
  - **语义熵（Semantic Entropy, SE）**：基于语义聚类而非表面形式的熵，反映回答行为的诚实性/确定性。
- 将二者映射到**知识状态象限**，得到四种自然语言状态：
  - **KH（有知识且诚实）**：Consistency > 0 且 SE = 0
  - **K¬H（有知识但不诚实）**：Consistency > 0 且 SE ≠ 0
  - **¬KH（无知识但诚实）**：Consistency = 0 且 SE = 0
  - **¬K¬H（无知识且不诚实）**：其他情况

**（2）策略优化（PPO + 细粒度奖励）**

- 定义奖励函数：$R_{FAITH}(x_i, y_i^k, \hat{y}_i, s_i) = R_{correctness}(y_i^k, \hat{y}_i) + R_{uncertainty}(s_i)$
- 其中 $R_{uncertainty}$ 根据知识状态映射：KH→+2，K¬H→+1，¬KH→−1，¬K¬H→−2
- 使用 PPO 算法优化策略模型，目标函数包含奖励期望和 KL 散度惩罚项。

**（3）RAG 修正模块**

- 基于 Wikipedia 语料库构建向量数据库（使用 BGE-base-en-v1.5 嵌入模型和 FAISS 索引）。
- 通过 RAFT 训练一个 RAG 模型作为"纠正器"，输入策略模型的输出和检索到的 top-3 上下文，输出修正后的答案。

**（4）知识状态估计器**

- 训练一个轻量级四分类模型直接预测问题的知识状态，避免推理时多次采样的开销。

### 推理流程

给定问题 → 估计器预测知识状态 → 策略模型生成回答 → RAG 模型用外部知识修正 → 最终答案。

## 三、实验设计

### 数据集

| 用途 | 数据集 | 类型 |
|---|---|---|
| 训练 + 域内评估 | TriviaQA（TVQA）、SciQ、NQ-Open | 知识密集型问答 |
| 域外评估 | WebQuestions（WebQ-QA） | 泛化性能测试 |

### 对比方法

- **Prompt-based**：ICL-CoT（链式思维提示）
- **SFT**：标准监督微调
- **RL**：RL-DPO（偏好优化）、UAlign（不确定性对齐）
- **RAG-based**：DTA（知识边界对齐）、Context-DPO、InFact，以及 SFT_rag 和 UAlign_rag 等增强变体

### 评估指标

- **Precision**：已知问题中正确回答的比例
- **Truthfulness**：正确回答已知问题 + 正确拒绝未知问题占总问题的比例

### 评估协议

在 Llama3-8B 和 Mistral-7B-v0.1 两个模型上实施，使用 LoRA 进行参数高效微调。

## 四、资源与算力

文中在附录 C 中说明了训练配置：

- **硬件**：4 × NVIDIA A40 GPUs
- **SFT 阶段**：3 epochs，LoRA rank=32，alpha=16，总 batch size 256
- **RM/PPO 阶段**：2 epochs，LoRA rank=8，alpha=16，总 batch size 128
- **未说明具体训练时长**（例如需要多少 GPU 小时），也未对比各方法的训练开销细节。

## 五、实验数量与充分性

### 实验组数与覆盖

- **主实验**：两种模型 × 4 个数据集 × 多方法（约 10+ 种对比），形成系统的性能对比矩阵。
- **消融实验**：
  - 知识状态形式对比（FAITH_sft vs. UAlign_sft，验证自然语言优于数值）
  - 奖励函数对比（FAITH_sft+ppo vs. UAlign，验证细粒度奖励优于二元奖励）
  - RAG 模块消融（FAITH vs. FAITH_sft+ppo）
- **专门分析**：
  - RAG 修正效果统计（正确修正 vs. 错误修正比例）
  - 模型化估计 vs. 采样化估计的对比
  - 训练时采样数量 $K \in \{6, 8, 10, 12\}$ 的扩展实验
- **案例研究**：三种类型的 RAG 修正模式（隐式支持、显式支持、误导性覆盖）

### 充分性与公平性评估

- **优点**：对比基线覆盖了 prompt-based、SFT、RL、RAG 等多个类别；在两种基座模型上验证泛化性；消融设计清晰，逐一验证了每个核心设计的贡献；域外数据集验证了泛化能力。
- **待改进之处**：DTA 方法在 SciQ 上因数据未发布而缺失结果（标记为"–"）；未报告多种子实验的标准差；训练/推理计算成本对比不够透明。

## 六、主要结论与发现

1. FAITH 在所有基线方法中取得了最优性能。例如在 Llama3-8B 上，FAITH 在域内数据集上达到 74.26% 的精度和 45.73% 的真实性，在域外 WebQ 上达到 67.99% 精度和 34.03% 真实性，均优于 UAlign、Context-DPO、InFact 等强基线。
2. **自然语言知识状态显著优于数值不确定性**：FAITH_sft 相比 UAlign_sft 在 Llama3-8B 上平均精度提升 2.05%、真实性提升 1.27%；在 Mistral 上提升更大。
3. **细粒度奖励函数有效**：使用 FAITH 奖励的 PPO 带来的提升（精度 +1.52%、真实性 +1.15%）大于 UAlign 的二元奖励（精度 +0.7%、真实性 +0.44%）。
4. **RAG 修正整体有效但并非总是正确**：在 TriviaQA 上 87% 的修正成功，但 SciQ 上正确修正比例低于错误修正（40.3%），表明外部知识质量与检索相关性会影响修正效果。
5. **K=6 已足够**：增大采样数量 K 未带来显著的性能提升，表明少量采样即可较准确刻画模型的知识状态分布。
6. **估计器能高效替代采样**：模型化估计在精度/真实性上与采样化估计仅相差约 1%，但推理效率大幅提升。

## 七、优点与亮点

- **语义化不确定性建模**：将冰冷的数值不确定性转换为"有知识/无知识"、"诚实/不诚实"的自然语言状态，更符合 LLM 的语义理解偏好，是一个简洁而有效的设计。
- **多维度的奖励设计**：同时考虑正确性和不确定性来源，比单纯二值化反馈提供更细粒度的训练信号，有效抑制模型的盲目猜测。
- **内外部知识的融合**：在利用模型内部不确定性信号的同时，引入 RAG 外部知识修正通道，弥补了纯参数化知识的局限。
- **推理效率优化**：训练知识状态估计器使推理时无需多次采样，仅需一次前向传播即可获得知识状态，兼顾效果与效率。
- **系统而透明的消融**：通过 SFT-only、SFT+PPO、完整框架的分层消融，清晰展示了每个组件（自然语言状态、奖励函数、RAG）的独立贡献。
- **实验严谨性**：在两个不同架构的基座模型（Llama3-8B、Mistral-7B-v0.1）以及域内/域外四个数据集上验证，提高了结论的可靠性；对 RAG 修正失败案例进行了细致的错误分析，未回避方法缺陷。

## 八、不足与局限

- **奖励函数缺乏理论保障**：作者承认奖励函数基于启发式规则设计，虽然经验上有效，但缺乏严格的理论证明，其最优性或适用范围未经形式化分析。
- **计算开销较高**：训练阶段需采样 $K$ 个响应、构建向量数据库；推理阶段至少需要两次模型前向（估计器 + 策略模型），如需要修正则增加第三次（RAG 模型）。相比单次端到端推理，延迟和资源成本明显更高。
- **RAG 修正存在反效果**：在 SciQ + Mistral-7B 组合上，RAG 修正的正确率低于错误率（40.3% 纠正成功 vs. 59.7% 导致错误），说明检索质量不佳时外部知识可能反而误导模型。
- **未深入探索检索质量的影响**：论文未系统分析不同的向量数据库构建质量、检索器参数（如 top-k）对修正效果的影响。
- **对"知道但拒绝回答"的处理不彻底**：研究目标将 UR（未知且拒绝）视为正确行为，但实际训练中"拒绝"机制的触发条件和行为边界未做细粒度分析，可能造成过度保守或虚假拒绝。
- **适用场景有限**：实验集中在英文短格式问答任务上，未验证长文本生成、多轮对话、非英语场景下的有效性。

（完）
