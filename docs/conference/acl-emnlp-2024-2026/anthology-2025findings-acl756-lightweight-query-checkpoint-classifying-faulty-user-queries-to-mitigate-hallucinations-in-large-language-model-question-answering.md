---
title: "Lightweight Query Checkpoint: Classifying Faulty User Queries to Mitigate Hallucinations in Large Language Model Question Answering"
title_zh: 轻量查询检查点：为大语言模型问答中的错误查询分类以缓解幻觉
authors: "Minjoo Son, Jonghak Jang, Misuk Kim"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.756.pdf"
tags: ["query:metacognitio"]
score: 6.0
evidence: 用中间层隐状态的小分类器在生成前识别需要验证的错误查询，作为避免不可靠输出的选择性检查点。
tldr: 问答中带有错误前提、上下文不足或歧义的用户提问容易诱发大模型幻觉。论文提出轻量查询检查点，即一个基于小模型中间层隐状态的小分类器，在模型生成前先把需要外部验证的查询与清晰查询分开，从源头约束可能有害的生成。该方法虽不直接评估模型自身回答，但提供了一种轻量、可部署的选择性防错机制，可迁移至自我判断前的质量门槛。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl756/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 632, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl756/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1522, \"height\": 723, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl756/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl756/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl756/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl756/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 719, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl756/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 803, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl756/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 634, \"height\": 549, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl756/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1662, \"height\": 1002, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl756/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 737, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl756/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1660, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl756/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1661, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl756/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1660, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl756/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1500, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl756/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1499, \"height\": 411, \"label\": \"Table\"}]"
motivation: 当用户查询含错误前提、信息不足或歧义时，问答系统仍可能产生幻觉回答。
method: 使用小型非指令调优模型中间层隐藏状态训练分类器，生成前判断查询是否需要验证。
result: 实验表明该检查点能够有效区分需验证与清晰的查询，从而减少随后生成的幻觉答案。
conclusion: 在生成之前加入轻量查询门控能够缓解由输入缺陷引发的幻觉，并可与下游自评估步骤衔接。
---

## Abstract
Question Answering (QA) with large language models has shown impressive performance, yet hallucinations still persist, particularly when user queries carry incorrect premises, insufficient context, or linguistic ambiguity. To address this issue, we propose Lightweight Query Checkpoint (LQC), a small classification model that detects verification-required queries before the LLM generates a potentially faulty answer. LQC leverages hidden states extracted from intermediate layers of a smaller-scale, non-instruct-tuned LLM to effectively distinguish queries requiring verification from clear queries. We first systematically define categories of queries that need verification, construct a dataset comprising both defective and clear queries, and train a binary contrastive learning model. Through extensive experiments on various QA datasets, we demonstrate that incorporating LQC into QA pipelines reduces hallucinations while preserving strong answer quality.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 核心问题与整体含义

- **研究动机**：尽管大语言模型（LLM）在问答任务上表现优异，但当用户查询包含以下缺陷时，幻觉仍在频发：
  - 不正确的前提（false premises），使查询无从作答；
  - 上下文信息不足（如时空条件缺失），迫使模型臆测；
  - 语言歧义，使查询可被多种解读。
- **核心主张**：与其让 LLM 在生成后自行纠正幻觉，不如**在生成前**就识别出这些需要验证的查询，阻断"向用户提供错误答案"这一路径。
- **整体贡献**：提出了 **Lightweight Query Checkpoint (LQC)** 这一轻量级二分类模型，通过在 LLM 生成答案之前介入，将查询分流到"要求澄清"或"直接作答"两条流程中，从而缓解由有缺陷查询引发的幻觉。

### 2. 方法论

- **核心思想**：LQC 利用**小规模、非指令调优 LLM 的中间层隐藏状态**作为查询表征，训练轻量二分类器判断查询是否为"需要验证"（verification needed）。
- **"需要验证的查询"分类学**：
  - **上下文不完整**（Contextual Incompleteness）：缺少回答所需的时间、地点等关键背景；
  - **语言歧义**（Linguistic Ambiguity）：因多义词或句法歧义导致多种合理理解；
  - **不可回答**（Unanswerable）：基于错误前提或要求不存在/不可验证的信息。
- **隐藏状态提取**：
  - 查询经对话模板格式化、token 化后输入 LLM；
  - 从**中间层**（而非首层或末层）提取隐藏状态；
  - 提出**混合池化（Hybrid Pooling）**策略，综合平均池化和末 token 池化：
    - $h_{\text{hybrid}} = \alpha h_{\text{last}} + (1-\alpha) h_{\text{mean}}$
- **对比学习训练**：
  - 将需要验证的查询与清晰查询视为两类，训练 MLP 分类器；
  - 使用监督对比损失拉近同类、推开异类，并叠加交叉熵损失：
    - $\mathcal{L} = \mathcal{L}_{\text{ce}} + \mathcal{L}_{\text{cont}}$
- **推理流程**：
  - LQC 判断查询是否需要验证；
  - 若"需要验证"，将查询导向"要求澄清"的提示模板；
  - 若"清晰"，则直接使用标准 QA 提示模板作答。

### 3. 实验设计

- **数据集与 benchmark**：
  - **SituatedQA-Geo / SituatedQA-Temp**：依赖地理位置/时间上下文的查询；
  - **CLAMBER-Linguistic Ambiguity**：多义词及句法歧义查询；
  - **CoCoNot-False Presuppositions**：含错误前提的查询；
  - 另使用 **KUQ** 作为域外（out-of-distribution）测试数据。
- **评估方式**：将回答分为五类：正确验证（A）、漏验（B）、正确回答（C）、错误回答（D）、过度验证（E），在此基础上计算 Accuracy、F1、F1c（清晰查询处理质量）与 F1v（验证需求检测能力）。
- **对比基线**：
  - **INSTANT**：无任何检查步骤，直接问答；
  - **REFLECT**：用提示指令让 LLM 自行判断是否需要验证。
- **答案生成模型**：Llama-3.1-8B-Instruct、Qwen2.5-7B-Instruct、Qwen2.5-14B-Instruct，各用两个随机种子取均值。

### 4. 资源与算力

- 论文**未明确说明**总训练时长、GPU 数量等详细算力配置。
- 仅提及：LQC 采用 Llama-3.2-1B 或 Qwen2.5-0.5B（共 13 个模型配置左右的小型 LLM）来提取隐藏状态，**可在单张 24GB RTX3090 GPU 上顺利运行**。
- 推理开销极小：LQC 引入的额外延迟不足 **0.02 秒**。
- 分类器本身仅为一个简单的 MLP，训练成本很低。

### 5. 实验数量与充分性

- **主实验**：4 个数据集 × 3 种答案生成模型 × 2 种 LQC 嵌入模型 × 3 种方法对比，构成 16 个实验条件的完整矩阵（如表 1 所示），覆盖了 Accuracy、F1、F1c、F1v 四个指标。
- **消融与分析**：
  - 对比学习有无的效果对比；
  - 不同 LLM 层级的特征提取效果对比；
  - 不同混合池化权重 α 的敏感性分析；
  - 指令调优 vs. vanilla 模型的对比；
  - 模型参数量大小的影响分析；
  - PCA 嵌入可视化。
- **可靠性验证**：对 5% 的回答进行人工标注复核，人机一致率 88.3%，Fleiss' Kappa=0.78，证明 GPT-4o 自动评估是可靠的。
- **域外测试**：使用 KUQ 数据集测试模型的分布外鲁棒性。
- **总体评价**：实验设计较为充分，具有多维度消融检验，能支撑论文的核心主张。但在数据的真实多样性方面仍有覆盖不足。

### 6. 主要结论与发现

- LQC 在 16 个实验条件中的 14 个场景下，各项指标**显著优于 INSTANT 和 REFLECT**，既有效拦截了需要验证的查询，又避免了过度验证干扰清晰查询。
- **中间层表征更有利于缺陷检测**：中间层特征兼具语义与语法信息，初层和末层效果均不及中间层。
- **混合池化优于单一池化**：综合全局信息与关键 token 信息可提升分类性能。
- **Vanilla 模型优于指令调优模型**：指令调优（尤其是 helpfulness 取向）会削弱模型对查询缺陷的识别能力（即 "alignment tax"）。
- **参数量并非越大越好**：更小的 LLM 反而能更清晰地凸显查询缺陷信号，分类性能更高，且资源消耗更低。
- **对比学习能显著改善分类效果**（+1-3 个点的 F1）。

### 7. 优点

- **轻量级、即插即用**：无需修改 LLM 权重或调整提示，直接以 LF 检查点方式插入 QA 流水线，额外延迟极低（<0.02s），适合在真实系统部署。
- **思路新颖且具可解释性**：利用 LLM 内部状态检测输入缺陷，而非"一头雾水"地依赖生成结果来推断。LQC 在生成前拦截，与常见的"生成后修正"形成互补。
- **系统性构建了缺陷查询的分类学**：三大类别定义清晰，数据集通过对公开资源的整合构建，是后续可复用的资源。
- **分析深入**：对层级选择、池化方式、指令调优与否、参数量大小等均做了消融，结论对实践有较强的指导意义（如如何取舍基础模型）。

### 8. 不足与局限

- **未修改 LLM 本身的幻觉机制**：LQC 只是"防御性过滤器"，无法完全杜绝模型在其自身能力不足时的错误回答，必须配合下游模型其他机制使用。
- **查询数据相对简单**：现有数据集多为短查询、结构化较强的问句；面对真实世界的复杂、嵌套、多领域查询时鲁棒性有待验证。
- **域外性能下降明显**：在 KUQ 数据集上 F1 从约 91% 降至 74%/73%，表明方法在分布漂移时鲁棒性受限，难以直接泛化到 Web 环境。
- **评估依赖自动化标注**：虽然报告了高一致性，但使用 LLM 标注存在系统性偏差风险，五分类评估对"正确"与"错误"的判定仍较粗糙。
- **答案质量缺乏细粒度评估**：仅通过 F1 指标判定"回答是否正确"，未考虑事实性、流畅度、对话体验等维度。

（完）
