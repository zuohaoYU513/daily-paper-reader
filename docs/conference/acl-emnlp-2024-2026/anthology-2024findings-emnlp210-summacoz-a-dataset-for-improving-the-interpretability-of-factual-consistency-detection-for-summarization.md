---
title: "SummaCoz: A Dataset for Improving the Interpretability of Factual Consistency Detection for Summarization"
title_zh: SummaCoz：提升摘要事实一致性检测可解释性的数据集
authors: "Ge Luo, Weisi Fan, Miaoran Li, Guoruizhe Sun, Runlong Zhang, Chenyu Xu, Forrest Bao"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.210.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 带解释增强数据的摘要事实一致性检测与可解释性改进
tldr: 该文聚焦摘要事实一致性检测的可解释性不足问题。在SummaC基准上构建SummaCoz数据集，加入了人工与模型生成的不一致自然语言解释，说明摘要偏离源文的原因。同时训练结合解释的检测器，一方面保持一致性判断能力，另一方面输出可读证据。该工作增强了检测结果的可信度和诊断价值。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp210/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1621, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp210/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 626, \"height\": 617, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp210/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1682, \"height\": 271, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp210/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp210/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp210/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1649, \"height\": 1084, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp210/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp210/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 736, \"height\": 545, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp210/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 662, \"height\": 544, \"label\": \"Table\"}]"
motivation: 摘要事实一致性检测已有很多模型，但缺少解释性，用户难以理解判定原因。
method: 在SummaC基础上构建带人工和模型解释的SummaCoz数据集，并联合训练附带解释的检测器。
result: 检测器能够在保持一致性判断性能的同时生成自然语言解释。
conclusion: 提升事实一致性检测的透明性，有助于错误分析和模型改进。
---

## Abstract
Summarization is an important application of Large Language Models (LLMs). When judging the quality of a summary, factual consistency holds a significant weight. Despite numerous efforts dedicated to building factual inconsistency detectors, the exploration of explanability remains limited among existing effort. In this study, we incorporate both human-annotated and model-generated natural language explanations elucidating how a summary deviates and thus becomes inconsistent with its source article. We build our explanation-augmented dataset on top of the widely used SummaC summarization consistency benchmark. Additionally, we develop an inconsistency detector that is jointly trained with the collected explanations. Our findings demonstrate that integrating explanations during training not only enables the model to provide rationales for its judgments but also enhances its accuracy significantly.

---

## 论文详细总结（自动生成）

# SummaCoz：提升摘要事实一致性检测可解释性的数据集

## 1. 核心问题与研究动机

- **任务背景**：摘要质量评估中，事实一致性（factual consistency）是关键维度，即摘要信息是否被源文支持。现有检测方法（如 MFMA、FalseSumm、NonFactS 等）大多将事实一致性检测视为**二分类问题**，仅输出"一致/不一致"标签。
- **核心痛点**：单纯二分类标签无法揭示不一致的**具体成因**——摘要哪个部分有误？源文中哪段信息与之矛盾？二者差异何在？这种缺乏解释性的判断限制了用户对检测结果的信任度，也难以指导人工或自动后编辑（post-editing）修正摘要。
- **现有数据的缺口**：虽有少数数据集（如 Maynez et al., 2020; Wu et al., 2023）标注了摘要中的不一致 span，但**缺乏源文中对应证据信息**的标注。
- **本文目标**：构建包含自然语言解释的数据集 SummaCoz，说明摘要为何与源文不一致；并训练一个**能同时输出判断与解释**的检测器，提升可解释性与准确性。

## 2. 方法论

### 2.1 SummaCoz 数据集构建流程

采用半自动方式，流程如下：

1. **数据来源**：选取 SummaC 基准（Laban et al., 2022）验证集中 1,323 个"不一致"摘要-源文样本对（仅含不一致样本，原因是判断"一致"较易，模型可达 >95% 准确率，解释一致性成因更有价值）。
2. **初始解释生成**：使用 Llama-2-13b-chat 生成初步解释。采用**标签引导提示**（label-elicited prompt），明确告知 LLM 摘要与源文不一致，要求其逐步推理并解释原因。
3. **人工后编辑**：6 位具有 NLP 背景的标注者依据 FRANK 错误类型学（8 类事实错误），对 LLM 生成的解释进行修正，要求按编号列表格式输出，注明不一致文本段、引用源文对应信息、指出差异。
4. **质量交叉验证与过滤**：使用 GPT-4（gpt-4-1106-preview）为相同数据独立生成解释；再以 GPT-3.5 为评判者，逐条比对人编辑后的解释与 GPT-4 解释的一致性（Bullet-level 评分）。仅保留**完全一致**的样本；1,323 个人工标注样本中最终保留 755 个样本（每个样本含 2 个解释：人工后编辑的 Llama-2 解释 + GPT-4 解释）。

### 2.2 训练框架

- **范式转换**：将传统分类任务重构为**纯文本到文本生成**任务，使模型同时输出标签文本与解释文本。
- **训练提示模板**（NLI 风格）：
  > Is the hypothesis true based on the premise? Premise: {article} Hypothesis: {summary}
- **目标输出**：
  > Yes, the hypothesis is true.（一致时）或 No, the hypothesis is not true. {explanation}（不一致时）
- **数据平衡**：由于 SummaCoz 仅含不一致样本，从 SummaC 验证集随机采样等量一致样本构成平衡训练集，其余样本作验证集。
- **微调策略**：采用 LoRA 参数高效微调。
- **训练设置对比**：
  - **LabelOnly**：仅训练输出标签；
  - **w/Explain**：训练先输出标签，若预测为不一致则输出解释。

## 3. 实验设计

### 3.1 Benchmarks 与数据集

- **SummaC test set**：包含 CoGenSum、FactCC、Frank、SummEval、XSumFaith（排除 Polytope，因其标注可靠性问题在先前研究中已有报告）。
- **RAGTruth test set（摘要任务）**：更具挑战性的基准，包含由更近期 LLMs 生成的长摘要。

### 3.2 基础模型

涵盖 5 个不同规模的模型：

| 模型 | 参数量 | 架构 |
|---|---|---|
| Flan-T5-0.8B | 0.8B | Encoder-Decoder |
| Flan-T5-3B | 3B | Encoder-Decoder |
| Flan-T5-11B | 11B | Encoder-Decoder |
| Mistral-7B-Instruct-v0.2 | 7B | Decoder-only |

### 3.3 评估指标

- SummaC 基准：平衡准确率（Balanced Accuracy, BA）
- RAGTruth：精确率/召回率/F1（不一致样本为命中）、平衡准确率
- 附带人类评分评估解释质量（0/0.25/0.5/0.75/1 五级量表）

### 3.4 对照方法

- 主要是本文两种训练模式（LabelOnly vs. w/Explain）内部对比，无外部基准方法直接对比。
- 附录还补充了 zero-shot 结果（Mistral-7B、Flan-T5-11B、GPT-4、GPT-3.5-turbo），与微调模型对比。

## 4. 资源与算力

- **GPU 资源**：单张 NVIDIA A100 80GB GPU 完成全部训练。
- **训练时长**：论文未明确说明各模型的训练耗时。
- **关键超参数**：epochs 10；学习率 1e-4；warmup ratio 0.1；batch size 1 + 梯度累积 8；优化器 paged_adamw_8bit；LoRA rank 16 / alpha 32 / dropout 0.05。
- 算力披露程度一般，未报告训练时长、GPU 总时数等细节。

## 5. 实验数量与充分性

- **主要实验维度**：
  1. **两个训练设置对比**（LabelOnly vs. w/Explain）：覆盖 4 个基础模型 × 两个 benchmark（SummaC 5 个子集 + RAGTruth）。
  2. **SummaC 基准**：5 个测试集上的平衡准确率（Table 1）。
  3. **RAGTruth 基准**：P/R/F1/BA 多元指标（Table 2）。
  4. **附录补充**：Zero-shot 对比结果（Table 4）。
  5. **解释质量人工评估**：97 个样本三档评分。
  6. **错误分析**：3 个典型误判案例的定性分析。
- **充分性评价**：实验覆盖面较广，模型规模从 0.8B 至 11B 具备梯度，benchmark 涵盖经典与新基准。但无外部一致性检测器（如 FactCC、QAFactEval 原文模型等）的横向对比；未进行基于解释质量的消融或对解释数量/质量的敏感性分析；每样本仅一人标注，无多标注者一致性验证（解释的人类评分有 2 人并报告 alpha=0.68，但数据集构建中每个样本只有 1 个人工标注）。整体而言**实验设计合理但对比严谨性中等**。

## 6. 主要结论与发现

1. **解释训练提升准确率**：在 SummaC 基准上，w/Explain 设置的平均 BA 全面优于 LabelOnly（如 Flan-T5-11B：81.1 → 82.0；Flan-T5-3B：78.6 → 80.8）。
2. **RAGTruth 上更明显**：w/Explain 在 3B–11B 模型上召回率、F1、BA 显著提升。例如 Flan-T5-11B BA 从 65.3 → 71.0，F1 从 46.6 → 56.9。
3. **召回率提升是关键**：加入解释训练增强了模型发现更多不一致摘要的能力。
4. **规模阈值**：0.8B 的 Flan-T5 未能从解释训练中获益，推测小模型推理能力受限，无法有效利用解释信号。
5. **零样本 vs. 微调**：微调后（尤其 w/Explain）显著超过 zero-shot；Flan-T5-11B w/Explain 的 F1 与 BA 甚至超过 GPT-4（zero-shot）。
6. **解释质量有限但可用**：RAGTruth 真负样本中约 78% 的解释准确或部分准确；但正确预测标签 ≠ 解释正确，二者需分开检验。

## 7. 优点

1. **填补空白**：首个为摘要事实一致性检测提供"标签 + 自然语言解释（人工 & LLM）"配对的数据集，源文证据与摘要错误跨度对应关系明确。
2. **构建流程严谨**：半自动生成配合人工后编辑 + LLM 交叉验证的双重质控机制，显著提升解释质量；解释了 568 个不一致样本被剔除的过程，透明度高。
3. **文本到文本统一框架**：单一模型同时承担分类与解释生成任务，架构简洁、易于部署，避免了多步多 LLM 调用的额外成本（与 FactScore/FacTool 分解式方法相比）。
4. **深入错误分析**：通过生成的解释定位模型误判根源，揭示了三类新挑战（词义细微差别、隐藏推理、常识知识依赖），具有诊断价值。
5. **模型规模梯度覆盖**：评估了 0.8B–11B 多个模型，验证了方法在中等规模模型的适用性边界。

## 8. 不足与局限

1. **仅覆盖不一致样本**：SummaCoz 数据集中没有一致性样本的解释（作者解释为一致性判断较易），导致模型只能学习"不一致"的解释模式；一致性样本在训练中有标签但无解释，影响对误判一致样本的解释能力。
2. **选择性偏差**：仅保留人类与 GPT-4 解释完全一致的 755 个样本（丢弃 568 个），可能偏向简单、明显的错误模式，对复杂不一致的覆盖能力有疑。
3. **单标注者局限**：数据构建中每样本仅一位人工标注者标注，未报告标注者间的信度；人工后编辑后的解释仍可能带有模型生成的偏差（后验解释与实际判断依据可能不一致，即"解释不忠实于推理"问题）。
4. **解释质量不高**：人工评分显示约 22% 的解释错误或无关；模型"预测正确但解释错误"的情形被论文自身的附录实验证实，可能影响用户信任。
5. **评测参照有限**：与外部既有检测器没有直接性能对比；解释质量缺乏与更强基线（如 GPT-4 零样本解释）的系统比较。
6. **自动过滤的模型偏差**：使用 GPT-3.5 作为评判者判断 GPT-4 解释与人解释一致性，可能引入了评判模型的偏好或误判。
7. **参考解释不唯一**：作者自认（Limitation 部分）——一个不一致样本可能存在多种解释原因，单参考解释可能无法覆盖所有合理理由。
8. **可复现性细节**：标注指南中的示例只覆盖了部分错误类型；未披露 6 位标注者的专业背景差异是否造成风格或质量偏差。

（完）
