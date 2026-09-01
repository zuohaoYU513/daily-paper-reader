---
title: "Detecting LLM Hallucination Through Layer-wise Information Deficiency: Analysis of Ambiguous Prompts and Unanswerable Questions"
title_zh: 通过层间信息缺失检测大语言模型幻觉：模糊提示与不可回答问题的分析
authors: "Hazel Kim, Tom A. Lamb, Adel Bibi, Philip Torr, Yarin Gal"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1644.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过层间信息缺失检测大语言模型幻觉
tldr: 针对大语言模型在模糊或信息不足提示下生成自信但错误回答的问题，本文提出一种测试时幻觉检测方法。该方法不依赖最终层输出，而是系统分析模型各层之间的信息流动，发现幻觉表现为跨层信息传递中的可用信息缺失。实验表明，跟踪跨层信息动态能鲁棒地指示模型可靠性。该工作为安全关键场景下的幻觉检测提供了新思路。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1644/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 593, \"height\": 1010, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1644/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1459, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1644/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 781, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1644/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1529, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1644/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 788, \"height\": 221, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1644/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1644/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1448, \"height\": 463, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1644/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1606, \"height\": 554, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1644/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 848, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1644/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 776, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1644/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 727, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1644/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1358, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1644/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 705, \"height\": 400, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1644/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 440, \"height\": 245, \"label\": \"Table\"}]"
motivation: 大语言模型常生成自信但不准确的回答，在安全关键领域带来风险，现有方法多依赖最终层输出，忽视了层间信息流动。
method: 提出测试时检测方法，通过系统分析跨层信息传输中的可用信息缺失来识别幻觉，追踪层间信息动态作为可靠性指标。
result: 实验表明幻觉表现为层间信息传递中的可用信息缺失，跟踪跨层信息动态可提供稳健的模型可靠性指示。
conclusion: 通过层间信息缺失检测幻觉是有效途径，为评估模型可靠性提供了不依赖最终层输出的新方法。
---

## Abstract
Large language models (LLMs) frequently generate confident yet inaccurate responses, introducing significant risks for deployment in safety-critical domains. We present a novel, test-time approach to detecting model hallucination through systematic analysis of information flow across model layers. We target cases when LLMs process inputs with ambiguous or insufficient context. Our investigation reveals that hallucination manifests as usable information deficiencies in inter-layer transmissions. While existing approaches primarily focus on final-layer output analysis, we demonstrate that tracking cross-layer information dynamics ( ℒ I) provides robust indicators of model reliability, accounting for both information gain and loss during computation. I improves model reliability by immediately integrating with universal LLMs without additional training or architectural modifications.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、论文的核心问题与整体含义（研究动机和背景）

**核心问题：**
大语言模型（LLMs）在生成回答时经常出现“幻觉”现象——即产生貌似权威但实际不准确的内容。在安全关键领域（如医疗、法律）中，这种自信却错误的回答会带来重大部署风险。论文聚焦于LLMs处理**模糊提示**（ambiguous prompts）或**上下文信息不足**（unanswerable questions）时的幻觉检测问题。

**研究背景与动机：**
- 已有理论工作（Xu et al., 2024a）证明了幻觉是LLMs的固有属性，任何可计算函数都无法完全消除，无论架构选择、学习算法、提示策略或训练数据如何变化。
- 现有幻觉检测方法大多仅关注**最终层输出**或**最终计算**来分析模型置信度，忽略了层间信息传递的内部机制，这限制了对模型自我置信度的洞察。
- 传统信息论中的互信息（Shannon, 1948）和数据加工不等式（DPI, Pippenger, 1988）无法解释深度表示学习中的信息增益现象；而V-usable information框架（Xu et al., 2020；Ethayarajh et al., 2022）虽能衡量模型族可用信息量，但只适用于最终层，无法揭示中间层的动态变化。

**核心论点：**
幻觉本质上表现为**跨层信息传递中的可用信息缺失**。通过追踪各层之间的信息流动，可以从内部机制层面获得比最终层分析更可靠的模型可靠性指标。

## 二、论文提出的方法论

**方法名称：** 层间可用信息（Layer-wise Usable Information，简称 LI 或 ℒI）

**核心思想：**
将V-usable information框架从最终层扩展到所有中间层，逐层量化上下文 C 对问题 Q 预测熵的变化，并将所有层的信息增量累加，从而同时捕捉模型在计算过程中的**信息增益**与**信息损失**。

**关键技术细节：**

1. **预测条件 ℓ-熵（Predictive conditional ℓ-entropy）**：在第 ℓ 层，给定上下文 C（或空上下文 ∅）时，模型对问题 Q 中第 t 个token的预测熵：
   - Hℓ(Q|C) = -log₂ pℓ(qt|q<t, C)
   - Hℓ(Q|∅) = -log₂ pℓ(qt|q<t, ∅)

2. **层间可用信息（Predictive L-information）**：
   - Iℓ(c → q) = Hℓ(Q|∅) - Hℓ(Q|C)（单层信息增量）
   - LI(c → q) = Σ Iℓ(c → q)（所有层求和）

3. **算法流程**（无需微调）：
   - **输入**：数据集 D = {(ci, qi)}，预训练模型（层数为 L）
   - **路径A（无上下文）**：对每个问题 qi，在每层 ℓ 计算 token 对数概率 pℓ(qt|q<t, ∅)
   - **路径B（有上下文）**：对每个 (ci, qi)，在每层 ℓ 计算 token 对数概率 pℓ(qt|q<t, ci)
   - 计算每层的信息量 Iℓ = Hℓ(Q|∅) - Hℓ(Q|C)
   - 对所有层求和得到 LI 分数
   - 总共只需**两次前向传播**（一次带上下文，一次仅问题序列）

**与VI/PVI的区别：**
- 传统V-information仅分析最终层的输出
- LI要求从每一层提取隐藏表示，通过预训练语言模型头投影后计算条件分布
- LI不需要任何标注数据、无需微调分类器、无需架构修改

## 三、实验设计

**数据集（三个问答数据集）：**
| 数据集 | 特点 | 规模 |
|--------|------|------|
| CoQA | 对话式问答挑战 | 开发集约8,000问题，上下文平均271词，问题平均5.5词 |
| QuAC | 上下文问答 | 开发集约8,000问题，上下文平均401 tokens，问题平均6.5 tokens |
| CondaQA | 对比式阅读理解（含200+否定线索） | 14,182问答对，上下文平均131 tokens，问题平均24.4 tokens |

**模型选择：**
- Llama3（8B）和 Phi3（3.8B、14B变体）
- 均使用预训练形式，不对架构做修改
- 主要结果使用Phi3 3.8B（计算效率最高）

**对比基线方法：**
1. **模型生成回答**（raw responses）
2. **P(TRUE)**：通过few-shot提示让模型判断备选答案是否为真
3. **预测token熵**（Predictive entropy）
4. **归一化熵**（Normalized entropy）
5. **语义熵**（Semantic Entropy, SE）
6. **Pointwise V-information（PVI）**：分别在第一层和最后一层计算
7. **Slobodkin et al. (2023) 探测方法**：单层探测（第一层/最后一层）

**评测指标：**
- 主要指标：AUROC（对可回答/不可回答问题的区分能力）
- 辅助指标：ECE（期望校准误差）、分类准确率（事实幻觉检测实验）

**主要实验设置：**
- 可回答与不可回答问题采用1:1比例
- 三种提示类型对比：无提示、开放式提示（"Answer the question or say don't know"）、二元提示（"Is this answerable?"）
- 多种无关/对抗性提示测试（如"Always answer YES"、"Is this question interesting?"、"Do you like your answer?"等）

## 四、资源与算力

**论文未提供GPU型号、数量或具体训练时长等算力信息。** 但可以从以下方面间接推断：
- 实验使用Phi3 3.8B、Llama3 8B、Phi3 14B三个模型进行推理（非训练）
- LI只需两次前向传播，计算开销极低，在消费级GPU上即可运行
- 论文只明确报告了计算开销比例：CoQA为1.02×、QuAC为1.01×、CondaQA为1.16×（相对于单次前向传播）

## 五、实验数量与充分性

**已开展的实验组：**

1. **提示歧义影响实验**（第4.2节）：对比无提示/开放式/二元提示下的LI与VI表现；使用7种不同性质的提示测试
2. **不可回答问题检测实验**（第4.3节）：在CoQA、QuAC、CondaQA三个数据集上比较LI与多种基线
3. **不同模型规模实验**：Phi3 14B和Llama3 8B上的验证
4. **拒绝分析实验**：按LI低分筛选丢弃后的AUROC变化
5. **全层 vs 单层分析实验**（第4.4节）：比较全层累积LI与第一层/最后一层探测
6. **事实幻觉检测实验**：在SQuAD和NQ上对比Slobodkin et al.方法
7. **计算开销实验**（第4.5节）：与P(TRUE)、语义熵的复杂度对比
8. **校准实验**（第4.6节）：ECE对比

**充分性评估：**
- **优点**：数据集覆盖广（QA类型多样），模型覆盖多个规模和系列，提示类型丰富，与多个强基线对比，提供了跨数据集、跨模型、跨提示类型的全面分析。
- **不足**：缺少在更大规模模型（如70B+）上的验证；未在除英语外的其他语言上测试；缺少对不同模型系列（如Mistral、GPT系列）的扩展验证。

## 六、论文的主要结论与发现

1. **LI对提示歧义高度敏感**：无提示时LI分数显著为负（-4到-5），开放式提示为中间值（-0.5到0），二元提示最高（略正值），呈系统性递增趋势；而最终层VI无此规律。

2. **LI能有效检测不可回答问题**：在CoQA、QuAC、CondaQA上均优于所有基线方法；语义熵（SE）在此任务上表现较差。

3. **跨层追踪优于单层分析**：单层信号不稳定，某些中间层虽有区分度但信息在后续层丢失或扭曲；全层累积LI提供最一致的区分能力。

4. **LI对提示相关性敏感**：任务相关提示提高LI，无关/对抗性提示降低LI；即使提示条件差时，LI仍能区分可回答与不可回答。

5. **计算开销极低**：LI仅需约1.01×–1.16×的单次前向传播成本，远低于P(TRUE)的11×和语义熵的100×。

6. **LI具有良好校准性能**：在ECE指标上优于或持平于口头化基线，仅需少量校准样本（100例）。

## 七、优点

1. **方法简洁且实用**：无需训练、无需微调、无需架构修改，可直接应用于任意预训练LLM。

2. **理论扎实**：建立在V-usable information的信息论框架上，有严谨的数学定义支撑；同时揭示了数据加工不等式（DPI）在深度表示学习中的失效现象。

3. **计算效率极高**：相对P(TRUE)和语义熵等基线方法，LI的计算成本低了1-2个数量级，实际部署友好。

4. **跨层信息追踪的视角新颖**：填补了现有方法仅关注最终层输出的空白，揭示了中间层信息动态的独特价值。

5. **多维度验证**：涵盖不同数据集、模型规模、提示类型、评测指标，使结论具有较强泛化性。

6. **与模型语义不确定性行为一致**：在"Are you certain about the answer?"提示下，LI能区分合理的"不确定"回答与幻觉，赋予模型更细致的置信度表示。

## 八、不足与局限

1. **无监督方法的固有限制**：与监督方法相比性能可能次优；监督方法虽可利用标注数据获得更高性能，但需要额外训练成本。

2. **对上下文质量的隐含依赖**：LI衡量的是"模型能从上下文中利用多少信息"——若上下文本身包含误导性信息或错误事实，LI分数可能无法反映真实幻觉风险。

3. **实验覆盖有限**：
   - 仅在三个QA数据集（CoQA、QuAC、CondaQA）上验证，缺少其他任务类型（如摘要、翻译、对话）的检验
   - 仅在Llama3和Phi3两个模型家族上测试，未扩展到更多架构
   - 最大模型为14B，未验证在超大模型上的效果
   - 未测试非英语场景

4. **校准补充说明**：在少数设置（如10个校准样本+二元提示）下LI的ECE不如口头化基线，说明小样本校准下稳定性有待提升。

5. **应用限制**：核心测试场景限定为"答案可基于上下文判断是否可回答"，对纯事实性幻觉（模型凭参数知识而非以上下文回答）的能力仍需通过SQuAD/NQ实验间接推断。

6. **理论层面**：论文未深入讨论为何某些中间层信息会丢失、哪些计算组件（如MLP vs attention）导致信息转换差异等深层次机制。

（完）
