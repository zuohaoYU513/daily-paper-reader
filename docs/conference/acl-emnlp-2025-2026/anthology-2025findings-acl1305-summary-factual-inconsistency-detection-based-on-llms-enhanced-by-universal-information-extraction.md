---
title: Summary Factual Inconsistency Detection Based on LLMs Enhanced by Universal Information Extraction
title_zh: 基于通用信息抽取增强的大型语言模型摘要事实不一致检测
authors: "Anguo Li, Lei Yu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1305.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 检测摘要中的事实不一致，即生成文本中的幻觉
tldr: 自动文本摘要存在影响事实性的潜在缺陷。现有基于大语言模型的检测方法依赖推理能力，效率和可解释性不足。本文提出UIEFID框架，通过自适应的结构化模式引导微调LLM从文档和摘要中抽取统一结构化信息，解耦抽取与推理，从而高效准确地检测摘要事实不一致。实验表明该方法在保持性能的同时提升了可解释性，为摘要幻觉检测提供了新思路。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1662, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1161, \"height\": 670, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1636, \"height\": 950, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1305/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1654, \"height\": 544, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1305/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 1495, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1305/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 694, \"height\": 229, \"label\": \"Table\"}]"
motivation: 摘要生成存在事实不一致问题，现有LLM检测方法效率低且缺乏可解释性。
method: 提出UIEFID框架，用自适应的结构化模式引导微调LLM抽取文档与摘要的统一结构化信息，解耦抽取与推理。
result: 实验验证了UIEFID在不依赖复杂推理的情况下实现高效且可解释的事实不一致检测。
conclusion: 该方法为LLM摘要事实性检测提供了效率与可解释性兼顾的新框架。
---

## Abstract
Automatic text summarization has a potential flaw that affects the factuality of summaries. Recently, Large Language Models (LLMs) have been introduced as detectors for factual inconsistencies in summaries. However, LLM-based methods rely on reasoning capabilities and face challenges in terms of efficiency and explainability. We focus on decoupling LLMs’ information extraction and reasoning capabilities to address prominent challenges, and propose a novel framework, UIEFID (Universal Information Extraction-enhanced Factual Inconsistency Detection). Our idea is to define a self-adaptive structured schema to guide fine-tuned LLMs in extracting unified structured information from documents and summaries, ultimately detecting the origins of inconsistencies in extraction information. The evaluation on 5 open-source models shows that UIEFID not only enhances the detection accuracy on the AGGREFACT benchmark but also significantly reduces redundant reasoning.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

自动文本摘要技术（特别是抽象式摘要）在生成自然流畅内容的同时，存在事实不一致（factual inconsistency）的固有风险——即摘要可能包含与源文档不符的虚假或扭曲信息。近年来，大语言模型（LLMs）被广泛用作事实不一致检测器，但现有基于 LLM 的方法存在两大核心痛点：

- **效率问题**：现有方法过度依赖 LLM 的推理能力，即使面对显式的不一致，也需要大量冗长的推理过程来分析摘要与文档的差异，特别是在长文档场景下，模型难以简洁地输出检测结果。
- **可解释性问题**：LLM 的推理可能包含错误，产生不稳定的输出（即“幻觉”），使得检测结果缺乏可靠性，且难以向用户解释检测依据。

论文指出，已有研究（如 Wang et al., 2024; Rettenberger et al., 2024）证明 LLM 擅长处理结构化信息。因此，本文的核心思路是**将 LLM 的信息抽取能力与推理能力“解耦”**，利用通用信息抽取（Universal Information Extraction, UIE）将非结构化文本转化为结构化数据，再进行精准的事实一致性比对与验证。

## 2. 论文提出的方法论

### 2.1 核心思想

- 受无损文本压缩算法启发，论文提出一个假设：对文档 D 和摘要 S 应用无损的结构化信息抽取器，将其语义与逻辑转化为**统一结构化信息（USI）**，即：
  - `IE(D, S) → (Id, Is)`，其中 Id 和 Is 分别是文档和摘要的结构化信息。
- 结构化信息采用**以主体（subject）为中心的三元组形式**表示：
  - `{Sub_i : (k_j, v_j)}`，其中 Sub_i 为第 i 个主体，k_j / v_j 为键值对（表达属性或关系）。
- 核心判定逻辑：**如果摘要是事实一致的，则文档的结构化信息应当在逻辑上蕴含摘要的结构化信息**；不一致之处即事实错误的来源。

### 2.2 UIEFID 框架（三阶段流程）

**阶段一：主体对齐（Subject Alignment）**

- 利用命名实体识别（NER）比较文档与摘要之间的主体差异，识别三类错误：不存在（non-existent）、拼写错误（spelling errors）、错位（misplacement）。
- 通过文本相似度计算和共指消解，从文档中选取合适的主体来替换摘要中的不一致内容。
- 目的：及时纠正主体的基础性语义错误，防止后续推理过度发散或引入偏差。

**阶段二：键值分析（Key-value Analysis）**

- 首先在 IEPile 语料库上对 LLM 进行微调，增强其 NER、关系抽取（RE）和事件抽取（EE）等信息抽取能力。
- 让微调后的 LLM 从摘要中抽取结构化信息（主体：键值对）；然后将键值对中的**值掩码**（替换为 "[?]"）构建抽取模式（schema）。
- 以该 schema 引导 LLM 从文档中检索相关内容并填写被掩码的值。
- 直接比较摘要与文档提取出的键值对差异，确定不一致的来源。
- 创新点：与传统“以文档为参照检测摘要”不同，UIEFID **以更简洁的摘要为基础进行验证**，显著降低对文档长度的敏感性。

**阶段三：事实性评估（Factuality Evaluation）**

- 量化累积的一致性程度，计算摘要的事实性分数（FS）：
  - `FS = (|ents_fc| / |ents|) × (1/|Sub|) × Σ (|p_fc_i| / |p_i|)`
  - 其中 `ents_fc` 为事实一致的实体数，`p_fc_i` 为第 i 个主体的事实一致键值对数。
- 只有实体和键值对都与文档高度一致时，摘要才能获得高事实性分数，从而保证评估的全面性。

## 3. 实验设计

### 3.1 数据集 / Benchmark

- **AGGREFACT**：评估摘要事实性指标的公认基准，聚合了 9 个已标注的新闻文章摘要事实性数据集。
- 包含两个子集：
  - **AGGREFACT-CNN/DM** 子集（源自 CNN/DailyMail）
  - **AGGREFACT-XSum** 子集（源自 XSum）
- 根据底层摘要模型的发展时间线，进一步划分为 FTSOTA（如 BART、PEGASUS、T5）、EXFORMER（如 BERT-Sum、GPT-2）和 OLD（如 Pointer-Generator、BottomUp）三类。

### 3.2 评估指标

- 使用**平衡准确率（balanced accuracy）**，以应对 AGGREFACT 数据集中事实一致与不一致摘要的不平衡问题。

### 3.3 对比基线（12 种）

- **NLI 类指标**：DAE、SummaC-ZS、SummaC-Conv、MENLI、AlignScore
- **QA 类指标**：QuestEval、QAFactEval
- **LLM 类指标**：TrueTeacher-11B、ChatGPT-ZS、ChatGPT-CoT、ChatGPT-DA、ChatGPT-Star
- 另有其他 LLM 零样本基线（Llama3-8B、Llama3.1-8B、Qwen2.5-7B、Qwen2.5-14B、DeepSeek-R1）在不同策略下进行对比。

### 3.4 实验场景

- 三种策略对比：零样本（zero-shot）、微调后零样本（+fine-tuning）、微调 + UIEFID 框架（+fine-tuning+UIEFID）。
- 消融实验：ZS（零样本）、KVA（仅键值分析，无主体对齐）、SA+KVA（完整 UIEFID 框架），每组实验重复 10 次记录波动范围。
- 鲁棒性测试：将 AGGREFACT 按文档-摘要压缩比分为 5 个区间（[0,10×], (10×,20×], (20×,30×], (30×,40×], (40×,∞)），考察不同压缩率下的检测准确性。
- 效率评估：构造效用度量 U = 输入 token 数 / 输出 token 数，比较各模型策略下的冗余推理程度。

## 4. 资源与算力

- 论文**未明确说明具体 GPU 型号、数量或训练时长**。
- 已知信息：
  - 使用 IEPile 语料库（约 0.32B tokens）对 Llama 3-8B、Llama 3.1-8B、Qwen2.5-7B、Qwen2.5-14B 进行微调。
  - 由于硬件资源限制，DeepSeek-R1 **无法本地部署和微调**，仅通过 API 调用进行实验。
- 这暗示实验使用的 GPU 资源并非大规模集群配置，但具体规格缺失。

## 5. 实验数量与充分性

### 实验覆盖面

- **主实验**：在 AGGREFACT-CNN 和 AGGREFACT-XSum 两大子集的所有摘要模型类别（FTS、ExF、OLD）上对比了 12 个基线 + 5 个开源 LLM × 3 种策略，评估矩阵较为完整。
- **消融实验**：验证了主体对齐（SA）和键值分析（KVA）的独立及协同贡献。
- **鲁棒性分析**：覆盖 5 个压缩比区间，考察输入长度差异对性能的影响。
- **效率分析**：多模型 × 多策略的效用对比，并分析了文档长度对推理/抽取占比的影响。

### 充分性与客观性评估

- **优点**：实验设计层次清晰，从准确率、效率、消融、鲁棒性多个维度验证框架有效性；重复实验提供了波动范围（±区间），增强了结果可信度。
- **不足**：
  - 消融实验仅在 Qwen2.5-7B 一个模型上进行，结论的普适性有限。
  - 未包含使用最新 LLM 生成的摘要数据集的评测。
  - 部分基线（如 DAE）因训练数据重叠问题在特定子集上被排除，对比的完全公平性存在一定折扣。
  - 某些检测基线因官方代码库维护问题无法运行，限制了对比实验的扩展。

## 6. 论文的主要结论与发现

1. **UIEFID 显著提升检测准确率**：在 AGGREFACT 基准上，所有 5 个开源模型在 UIEFID 框架下均取得明显性能提升（最高提升 14.5%）。其中 DeepSeek-R1 + UIEFID 实现了最优平均平衡准确率（83.7），刷新 SOTA。
2. **效率显著改善**：UIEFID 在各种模型上均带来更高的效用值（输入/输出 token 比），有效抑制冗余推理生成。随着文档长度增加，推理与抽取的占比差距逐渐缩小，证明框架有效抑制了推理发散。
3. **主体对齐具有必要性**：消融实验显示，KVA 单独带来 +10.9 的准确率提升，SA 额外贡献 +3.7，且性能提升未引入明显不稳定性。
4. **模型性能遵循缩放定律**：参数量更大的模型（如 Qwen2.5-14B 优于 Qwen2.5-7B）在检测任务中表现更好。
5. **压缩比对性能影响呈非线性**：准确率在中间压缩比区间波动最大，在极简单或高度压缩的文档-摘要对上表现相对稳定，表明输入复杂度对检测有显著影响。

## 7. 优点

- **方法创新性强**：首次将通用信息抽取（UIE）引入摘要事实性检测领域，成功实现 LLM 信息抽取与推理能力的解耦，开辟了新的方法论方向。
- **兼顾效率与可解释性**：通过结构化信息提取，显著减少推理时间与冗余输出；将不一致来源细化为“主体对齐错误”和“键值对差异”，检测结果具有明确依据，可解释性强。
- **实用价值突出**：将检测重心从长文档转向更简洁的摘要，有效降低长文档场景下的计算复杂度；采用“自我修正”思路，可直接指导摘要修订。
- **实验验证充分**：横跨多种模型规模（7B~14B + R1 API）、多类基线、多个维度的评估；消融和鲁棒性分析设计科学。
- **工程实现借鉴性强**：结合 spaCy 低成本实现主体对齐，仅对关键环节使用 LLM，资源开销可控。

## 8. 不足与局限

- **结构化表示的普适性存疑**：论文未证明以主体为中心的三元组表示是最优方案，其他结构化表示可能更有效地传达文本语义内容。
- **基线模型覆盖面有限**：未包含最新的 LLM 摘要数据集，对 LLM 生成摘要特有错误模式的分析不足。
- **消融实验范围较窄**：仅在单一模型（Qwen2.5-7B）上进行了消融验证，主体对齐在不同规模、不同架构模型上的贡献度尚不清楚。
- **硬件信息缺失**：未报告具体 GPU 规格、训练时长和资源消耗，可复现性和成本评估受限。
- **DeepSeek-R1 对比不完整**：由于硬件限制，DeepSeek-R1 无法进行微调与本地部署，其与微调模型的公平性对比度有所降低；且 R1 因自带冗长推理链，在效率指标上表现不佳，与其准确率优势形成张力。
- **外部验证不足**：仅在 AGGREFACT（新闻领域）上验证，未涉足其他领域（如医学、法律、科学文献）的摘要事实性检测，泛化能力未见展示。
- **部分基线的比较公平性有限**：如 DAE 由于训练重叠被部分排除；多个基线因官方代码库问题未能全部复现，对比的全面性受客观条件限制。

（完）
