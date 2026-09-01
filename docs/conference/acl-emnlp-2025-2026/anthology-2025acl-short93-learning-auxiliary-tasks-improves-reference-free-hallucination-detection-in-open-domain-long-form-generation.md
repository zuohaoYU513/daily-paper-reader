---
title: Learning Auxiliary Tasks Improves Reference-Free Hallucination Detection in Open-Domain Long-Form Generation
title_zh: 学习辅助任务可改进开放域长文本生成中的无参考幻觉检测
authors: "Chengwei Qin, Wenxuan Zhou, Karthik Abinav Sankararaman, Nanshu Wang, Tengyu Xu, Alexander Radovic, Eryk Helenowski, Arya Talebzadeh, Aditya Tayade, Sinong Wang, Shafiq Joty, Han Fang, Hao Ma"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-short.93.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 基于辅助任务学习的无参考幻觉检测
tldr: 针对开放域长文本生成中幻觉检测依赖外部工具或领域受限的问题，系统研究无参考幻觉检测。发现仅靠内部状态（如概率和熵）难以可靠区分事实与幻觉。提出通过辅助任务学习增强检测能力，实验证明该方法能显著提升检测性能，同时减少对外部事实核查工具的依赖。
source: ACL-2025-Short
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 781, \"height\": 488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 769, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 763, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 763, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 770, \"height\": 129, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 773, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-short/anthology-2025acl-short93/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 777, \"height\": 527, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 765, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 600, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 760, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 124, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 365, \"height\": 126, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 366, \"height\": 126, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-short/anthology-2025acl-short93/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 670, \"height\": 130, \"label\": \"Table\"}]"
motivation: 现有长文本幻觉检测依赖外部工具或领域受限，内部状态单独使用效果不佳。
method: 基于内部特征与辅助任务学习建立无参考幻觉检测方法。
result: 实验表明辅助任务学习显著提升开放域长文本幻觉检测准确性。
conclusion: 为无外部工具条件下的幻觉检测提供了有效增强手段。
---

## Abstract
Hallucination, the generation of factually incorrect information, remains a significant challenge for large language models (LLMs), especially in open-domain long-form generation. Existing approaches for detecting hallucination in long-form tasks either focus on limited domains or rely heavily on external fact-checking tools, which may not always be available.In this work, we systematically investigate reference-free hallucination detection in open-domain long-form responses. Our findings reveal that internal states (e.g., model’s output probability and entropy) alone are insufficient for reliably (i.e., better than random guessing) distinguishing between factual and hallucinated content. To enhance detection, we explore various existing approaches, including prompting-based methods, probing, and fine-tuning, with fine-tuning proving the most effective. To further improve the accuracy, we introduce a new paradigm, named RATE-FT, that augments fine-tuning with an auxiliary task for the model to jointly learn with the main task of hallucination detection. With extensive experiments and analysis using a variety of model families & datasets, we demonstrate the effectiveness and generalizability of our method, e.g., +3% over general fine-tuning methods on LongFact.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：大语言模型（LLM）在开放域长文本生成中容易产生“幻觉”（hallucination），即生成与真实世界事实相冲突的内容。这一问题在需要跨领域综合信息的长篇回答中尤为严重，例如回答“琥珀宫的意义”等开放式问题时，模型可能混入虚构细节。
- **现有方法的不足**：
  - 已有幻觉检测研究大多聚焦于短文本任务（一至几个 token 的输出），难以直接迁移到数百至数千 token 的长文本场景。
  - 针对长文本的少数工作要么限于特定领域（如人物传记生成），要么高度依赖外部事实核查工具（如 Google Search），但外部工具并非总是可用或可扩展。
- **核心研究问题**：能否仅依靠模型自身机制（reference-free，即无外部事实核查资源）在开放域长文本生成中有效检测幻觉？
- **论文含义**：系统探索了无参考条件下长文本幻觉检测的可行性，发现模型内部状态（概率、熵）单独使用并不可靠，并提出了一种通过辅助任务学习增强微调效果的新范式 RATE-FT，显著提升了检测性能。

## 2. 论文提出的方法论

### 2.1 整体框架

论文首先系统评估三类现有方法的检测效果：

| 方法类别 | 核心思路 |
|---------|---------|
| **Prompting** | 直接提示 LLM 判断 claim 正确性，包括 Prompt TF（输出 True/False）、Prompt Prob（输出概率数值）、SelfCheckGPT（采样多条响应并衡量一致性） |
| **Probing** | 在 LLM 冻结的上下文嵌入上训练多层感知机（MLP）进行二分类 |
| **Fine-Tuning** | 使用 LoRA 微调基座 LLM，使其输出 True/False |

实验发现 Fine-Tuning 效果最佳，但仍有提升空间。

### 2.2 RATE-FT（Rationale and Auxiliary Task Enhanced Fine-Tuning）

RATE-FT 是在 Fine-Tuning 基础上的改进框架，包含两个核心增强组件：

**(1) Rationale 增强（理由/推理链增强）**
- 在数据构建阶段，生成解释判断依据的推理路径（rationale）。
- 采用“标签-理由”格式（如 "True. {explanation}"），保证推理成本与基线 Fine-Tuning 一致——直接从第一个输出 token 提取 Pfactual，无需生成完整的推理路径。
- 受 Chain-of-Thought（CoT）启发，系统性引导模型拆解判断依据。

**(2) 辅助问答任务增强（Auxiliary QA Task）**
- 对每个 claim，提示模型生成关于其关键信息的问题：
  - 事实性 claim：直接从 claim 中提取正确答案并给出解释。
  - 幻觉 claim：利用已增强的 rationale 引导模型生成正确的答案和解释。
- 将构造的 QA 样例与原始数据合并进行微调，通过多样性情境下的重复学习强化模型对事实性的理解。
- 动机类比：医学生通过图表、模拟、解剖等不同视角加深对同一知识的理解。

### 2.3 关键设计细节

- **分类指标**：Pfactual（预测为“事实”的概率）作为分类指示器，超过预定义阈值即分类为“事实”，否则为“幻觉”；阈值在验证集上搜索选定。
- **评估指标**：平衡准确率（Balanced Accuracy, BAcc）= 1/2 × (TP/(TP+FN) + TN/(TN+FP))。
- **数据构造**：基于 LongFact 的 200 个 prompt 采样，用模型将长文响应分解为原子化 claim，借助 Google Search 标注事实/幻觉标签及理由。

### 2.4 混合不确定性管道（附录 A.8）

- 设置双阈值（αlow 和 αhigh）：Pfactual > αhigh 判定为事实，< αlow 判定为幻觉，介于两者之间的标记为“未知”并交由外部工具处理。
- 使用 BAcc-unknown 指标评估，在验证集上保证 BAcc 超过 70% 的同时最大化 BAcc-unknown。

## 3. 实验设计

### 3.1 数据集与 Benchmark

| 数据集 | 说明 | 规模 |
|-------|------|------|
| **LongFact** | 开放域长文本生成数据集，覆盖 38 个不同领域 | 采样 200 个 prompt 进行实验；构造出 2,394 条事实性 claim 和 223 条幻觉 claim，平衡后各取 223 条用于实验 |
| **Biography** | 人物传记生成数据集（Min et al., 2023） | 用于验证跨数据集的泛化性 |

- 数据切分：训练集 70%、验证集 20%、测试集 10%。
- 标注方式：使用模型生成多步 Google Search 查询词并推理搜索结果是否支持 claim（遵循 Wei et al., 2024 的方法）。

### 3.2 对比方法

- **基线方法**：内部状态（概率/熵的多种变体）、Prompt TF、Prompt Prob、SelfCheckGPT（采样 20 条响应）、Probing、Fine-Tuning。
- **RATE-FT 变体**：仅 Fine-Tuning、不含辅助任务的 RATE-FT（w.o. aux）、RATE-FT half（训练数据减半）、Fine-Tuning para（用 GPT-4 改写做数据增强的对照）。

### 3.3 模型与实验场景

- **主实验模型**：Llama-3-8B-Instruct。
- **泛化性实验模型**：Llama-3.1-70B-Instruct、Mistral-7B-Instruct、Qwen2.5-7B-Instruct。
- **OOD（分布外）场景**：在 LongFact 上训练，在 Biography 上评估。
- **不确定性集成场景**：在 LongFact 上评估 BAcc-unknown（附录 A.8）。

### 3.4 关键实验结果

| 方法 | LongFact BAcc (%) | Biography BAcc (%) |
|------|-------------------|-------------------|
| Prompt TF | 69.9 | 72.3 |
| Prompt CoT-TF | 74.9 | 74.8 |
| Prompt Prob | 53.4 | 56.3 |
| SelfCheckGPT | 69.1 | 71.9 |
| Probing | 74.4 | 77.0 |
| Fine-Tuning | 76.1 | 78.2 |
| **RATE-FT** | **79.6** | **80.9** |

多模型结果（LongFact）：

| 模型 | Prompt TF | Prompt CoT-TF | Probing | Fine-Tuning | RATE-FT |
|------|-----------|---------------|---------|-------------|---------|
| Llama-3.1-70B-Instruct | 73.2 | 76.8 | 79.4 | 80.6 | **83.8** |
| Mistral-7B-Instruct | 61.8 | 64.1 | 68.4 | 70.8 | **73.4** |
| Qwen2.5-7B-Instruct | 72.8 | 75.5 | 77.0 | 78.4 | **81.1** |

## 4. 资源与算力

- **论文中未明确说明**：没有提及使用的 GPU 型号、数量、训练时长或具体算力消耗。
- 仅能推断：实验涉及 4 个不同规模的模型（7B~70B），主要使用 LoRA 微调（参数量较小），且推理阶段使用 greedy decoding 或少量采样（SelfCheckGPT 采样 20 条响应），整体算力开销可能适中，但具体细节无从考证。
- 实现细节中仅提到使用 LLaMA-Factory 库（Zheng et al., 2024）进行微调，超参数在验证集上搜索确定。

## 5. 实验数量与充分性

### 实验组数与覆盖范围

论文包含较为丰富的实验体系，主要实验组包括：

1. **内部状态分析实验**：验证概率和熵的多种变体（算术/几何平均、Top-K 最低概率、Top-P% 低概率、最高熵等）在幻觉检测中的表现，结论为均无法有效区分事实与幻觉。
2. **现有方法对比实验**：在 LongFact 上对比 5 类方法，在 Biography 上复现验证。
3. **RATE-FT 主实验**：在 LongFact 和 Biography 上与所有基线对比。
4. **消融实验**：考察 rationale 与辅助任务各自贡献（w.o. aux 变体）。
5. **数据增强对照实验**：Fine-Tuning para（GPT-4 改写增强数据量）vs. RATE-FT、Fine-Tuning vs. RATE-FT half，证明性能提升来自辅助任务设计而非单纯数据量增加。
6. **跨模型泛化实验**：4 种不同架构和规模的模型。
7. **OOD 实验**：跨数据集（LongFact 训练 → Biography 测试）。
8. **不确定性集成实验**（附录）：BAcc-unknown 指标上的混合管道评估。

### 充分性与客观性评估

- **优点**：覆盖面较广，同时验证了跨数据集、跨模型、多类基线的对比；消融和对照实验设计较为严谨，能有效分离辅助任务与数据量增加的效果。
- **不足**：
  - 训练/验证/测试数据总量较小（平衡后仅 446 条 claim），统计效力有限。
  - 标注依赖 Google Search 和模型自身生成，存在噪声，可能引入系统性偏差。
  - 未报告方差（不同随机种子/数据切分的方差），结果稳定性未验证。

## 6. 论文的主要结论与发现

1. **内部状态不足以可靠检测幻觉**：在开放域长文本生成中，输出概率和熵等内部状态无法以高于随机猜测的水平区分事实性 claim 和幻觉 claim。原因在于长文本 claim 包含大量非关键 token（如停用词），且概率/熵反映的是模型对表达形式的置信度而非 claim 内容正确性。
2. **Fine-Tuning 是最有效的现有方法**：在 prompting、probing 和 fine-tuning 三类方法中，微调通过更新 LLM 内部特征取得最佳检测效果（LongFact BAcc 76.1%）。
3. **引入 CoT 推理有益**：Prompt CoT-TF（69.9% → 74.9%）验证了推理路径对判断正确性的促进作用。
4. **RATE-FT 显著优于所有基线**：在 LongFact 上比一般 Fine-Tuning 提升 +3.5%（76.1% → 79.6%），在 Biography 上提升 +2.7%（78.2% → 80.9%）。
5. **RATE-FT 具有良好泛化性**：在 70B 和 7B 规模的不同模型架构上均一致优于基线。
6. **辅助 QA 任务的效果来自任务设计而非数据量扩充**：RATE-FT 与 Fine-Tuning para、RATE-FT half 的对照表明，性能提升的核心在于辅助任务提供了互补的学习视角。
7. **外部工具可以与模型不确定性协同**：通过设置双阈值将模型“不确定”的样本交由外部工具处理（BAcc-unknown 最高达 85.0%），为混合检测管道提供了可行方案。

## 7. 优点

- **问题新颖性与价值**：首次系统研究开放域长文本生成中的无参考幻觉检测，填补了该方向的研究空白。
- **方法设计巧妙**：RATE-FT 采用“标签-理由”格式保持推理开销不变，同时获得推理链的增强效果；将幻觉检测转化为辅助 QA 任务，从互补视角帮助模型理解事实性，思路具有启发性。
- **实验设计严谨**：通过多种消融和对照实验（去除辅助任务、数据减半、GPT-4 改写数据增强）有效隔离了辅助任务设计和数据量两个因素，因果推断较为扎实。
- **跨模型、跨数据集验证**：涵盖 7B~70B 不同架构的 4 种模型和 2 个数据集（外加 OOD 实验），结论的泛化性得到了较好支持。
- **分析深入**：对内部状态失效的原因给出了清晰解释（概率反映表面形式而非 claim 正确性；长文本含大量无关 token），并与 SelfCheckGPT 的结论进行了详细对比讨论。
- **实际部署友好**：LoRA 微调方式允许模型在保留通用能力的同时加载专用检测适配器，且无需外部工具即可运行。

## 8. 不足与局限

- **数据规模与标注质量**：
  - 实验数据规模较小（平衡后仅 446 条 claim），可能不足以支撑细微的性能差异结论。
  - 数据标注依赖 LLM 自身生成查询和 Google Search 验证，标注过程可能存在噪声和偏差。
  - 实验未报告多次运行的方差或置信区间。
- **评估指标单一**：主要依赖 BAcc，未使用 AUC、Precision-Recall、F1 等指标做多维评估；BAcc 在阈值选择上可能受到验证集波动的影响。
- **外部工具依赖的局限性**：
  - 虽然主打 reference-free，但数据构建和标注过程仍然依赖 Google Search（训练标签来源），本质上未能完全脱离外部资源。
  - 混合不确定性管道（附录 A.8）额外依赖外部工具，应用场景受限于工具可用性。
- **实验覆盖不足**：
  - 只使用了一个主数据集（LongFact）和一个人物传记数据集，领域覆盖有限（论文也在 Limitations 中承认需要更全面的 benchmark）。
  - 未评估在更广泛模型（如 GPT 系列闭源模型）上的有效性。
- **检测粒度**：限于 atomized claim 级别的二分类，未处理 claim 之间的交互、部分正确/部分错误等更复杂的现实场景。
- **训练标签的来源偏差**：用于构造训练数据的 claim 由模型自身分解和标注，模型可能在某些方面系统性地错误标注，导致训练信号含噪。
- **RATE-FT 的额外成本**：虽然推理时与 Fine-Tuning 持平，但数据构建过程需额外生成 QA 示例和 rationale，训练数据准备成本和复杂度有所增加。
- **应用局限**：论文 Limitations 部分指出，研究仅聚焦于提高检测器性能，未探索将检测器反馈作为奖励信号用于引导模型生成更真实的内容。

（完）
