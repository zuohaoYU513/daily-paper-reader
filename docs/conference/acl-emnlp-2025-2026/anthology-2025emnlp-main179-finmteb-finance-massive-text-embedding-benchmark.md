---
title: "FinMTEB: Finance Massive Text Embedding Benchmark"
title_zh: FinMTEB：金融大规模文本嵌入基准测试
authors: "Yixuan Tang, Yi Yang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.179.pdf"
tags: ["query:hallu-rag"]
score: 4.0
evidence: 面向金融的嵌入基准，包含分类与检索任务，可为金融情感分析提供支撑
tldr: 通用文本嵌入基准难以满足金融领域的细粒度需求，而金融情感分析、检索等任务都依赖域内嵌入质量。本文提出 FinMTEB，一个专门针对金融领域的大规模文本嵌入基准，包含 64 个数据集、7 种任务类型，覆盖分类、聚类、检索、重排序、摘要和语义相似度等，并支持中英文。该基准可为金融场景下的嵌入模型提供更全面的评测指标，有助于选择和改进面向金融情感分析、金融问答等应用的表示模型，填补了金融专用嵌入评测的空白。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main179/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1625, \"height\": 871, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main179/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1517, \"height\": 1096, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 810, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1641, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1613, \"height\": 1938, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1628, \"height\": 1192, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1635, \"height\": 816, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1641, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1635, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1337, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1644, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1647, \"height\": 460, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1456, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1154, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1488, \"height\": 1164, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main179/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1622, \"height\": 530, \"label\": \"Table\"}]"
motivation: 通用嵌入基准未覆盖金融领域差异，难以为金融情感分析等任务提供评测依据。
method: 构建含64个金融数据集、7类任务的嵌入基准，覆盖分类、检索、重排序、摘要等。
result: 提出了金融专用评测基准并附带基线模型，为金融嵌入研究提供统一参照。
conclusion: 促进金融NLP中嵌入模型的评测与发展，间接支持金融情感分析等任务。
---

## Abstract
The efficacy of text embedding models in representing and retrieving information is crucial for many NLP applications, with performance significantly advanced by Large Language Models (LLMs). Despite this progress, existing benchmarks predominantly use general-purpose datasets, inadequately addressing the nuanced requirements of specialized domains like finance. To bridge this gap, we introduce the Finance Massive Text Embedding Benchmark (FinMTEB), a comprehensive evaluation suite specifically designed for the financial domain. FinMTEB encompasses 64 datasets across 7 task types, including classification, clustering, retrieval, pair classification, reranking, summarization, and semantic textual similarity (STS) in English and Chinese. Alongside this benchmark, we introduce Fin-E5, a state-of-the-art finance-adapted embedding model, ranking first on FinMTEB. Fin-E5 is developed by fine-tuning e5-Mistral-7B-Instruct on a novel persona-based synthetic dataset tailored for diverse financial embedding tasks. Evaluating 15 prominent embedding models on FinMTEB, we derive three key findings: (1) domain-specific models, including our Fin-E5, significantly outperform general-purpose models; (2) performance on general benchmarks is a poor predictor of success on financial tasks; and (3) surprisingly, traditional Bag-of-Words (BoW) models surpass dense embedding models on financial STS tasks. This work provides a robust benchmark for financial NLP and offers actionable insights for developing future domain-adapted embedding solutions. Both FinMTEB and Fin-E5 will be open-sourced for the research community.

---

## 论文详细总结（自动生成）

# FinMTEB：金融大规模文本嵌入基准测试 — 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：通用文本嵌入模型及其评测基准无法充分满足金融领域对文本表示和语义检索的细粒度需求。金融文本存在**领域特有术语**（如 "liability" 在金融语境中的负面含义）、**时间敏感性**、**复杂数值关系**以及大量**样板化合规语言**（boilerplate language），这些特征使得通用模型的表现不能代表金融场景下的真实性能。
- **总体目标**：构建一个专为金融领域设计的大规模文本嵌入评测基准（FinMTEB），并在此基础上开发一个金融适配的嵌入模型（Fin-E5），为金融 NLP 研究提供标准化评估平台。
- **背景缺口**：现有金融评测（如 FinanceBench、FinQA）多侧重文本生成与推理能力，缺乏对嵌入质量的系统评估；已有的嵌入式评测（如 FiQA）覆盖面窄，仅聚焦单一任务或单一文本类型；商业模型（如 voyage-finance-2）存在，但**缺乏开源、基于大语言模型的金融嵌入模型**。

## 2. 论文提出的方法论

### 2.1 FinMTEB 基准构建
- **任务覆盖**：包含 7 种嵌入任务，模仿 MTEB 结构但完全使用金融领域数据集：
  - **语义文本相似度（STS）**：评估金融文本对的语义相似度，使用 Spearman 相关系数。
  - **检索（Retrieval）**：测试模型从金融语料中检索相关信息的能力，使用 NDCG@10。
  - **聚类（Clustering）**：评估金融文本自动分组的质量，使用 V-measure。
  - **分类（Classification）**：测试金融文本分类能力（如情绪分析、鹰派/鸽派分类、ESG 分类等），使用 MAP。
  - **重排序（Reranking）**：评估模型对检索结果进行相关性排序的能力，使用 MAP。
  - **对分类（Pair Classification）**：判断金融文本对之间的语义关系，使用平均精度（AP）。
  - **摘要（Summarization）**：评估嵌入对原文-摘要语义一致性的捕捉能力。
- **数据规模**：共 **64 个数据集**（英文 35 个、中文 29 个），涵盖多种金融文本类型（新闻、10-K 年报、财报电话会议记录、消费者投诉、金融词典等）。

### 2.2 Fin-E5 模型训练方法
- **基础模型**：e5-Mistral-7B-Instruct，进行金融领域微调。
- **训练数据构建**（核心创新）：
  - **种子数据**：使用 InvestLM 提供的金融 QA 数据（经专家验证），并严格检查与 FinMTEB 基准无重叠。
  - **Persona-based 数据增强**（三阶段流程）：
    - **阶段一（人设与任务识别）**：用 Qwen2.5-14B-Instruct 分析每个问答对，生成详细的人设描述（如 "金融机构合规官，负责追踪经济指标及其监管影响"）。
    - **阶段二（上下文查询生成）**：基于人设描述，用 Qwen2.5-72B-Instruct 生成该人设可能提出的新查询，并过滤出需要外部文档才能回答的"上下文型"查询。
    - **阶段三（合成正文档生成）**：对每个查询，用 Qwen2.5-72B-Instruct 合成一个与查询直接相关的正文档 d+。
- **训练流程**：
  - 使用三元组结构 **（q, d+, D−）**，其中 q 为金融查询，d+ 为合成正文档，D− 为使用 all-MiniLM-L12-v2 挖掘的**困难负样本**。
  - 采用 **InfoNCE 对比学习损失**，结合批内负样本。
  - 使用最后 token 池化（与 e5-mistral 训练方案一致）。
  - 使用指令模板：`q_inst = Instruct: {task_definition}\n{q}`。
  - 训练数据规模：19,467 条；100 个训练步；批次大小 128；AdamW 优化器；学习率 1e-5；线性 warmup。

## 3. 实验设计

- **评测基准**：FinMTEB（64 个数据集，7 个任务，中英文）。主评测聚焦英文，中文结果在附录 C。
- **对比模型（15 个）**，分四类：
  - **BOW（词袋）**：传统稀疏向量基线。
  - **编码器模型**：BERT、FinBERT（金融领域专用）、instructor-base、bge-large-en-v1.5、AnglE-BERT、all-MiniLM-L12-v2 等。
  - **LLM 基础模型**：e5-mistral-7b-instruct、bge-en-icl、Echo、NV-Embed v2、gte-Qwen1.5-7B-instruct。
  - **商业模型**：OpenAI text-embedding-3-large/small、voyage-3-large。
- **统计分析**：
  - 使用**单因素 ANOVA** 检验各任务上模型间差异的显著性。
  - 使用**配对 t 检验**比较 Fin-E5 vs. e5-mistral、FinBERT vs. BERT 的逐任务表现。
  - 通过**自助法（bootstrapping）**生成 500 个样本进行 MTEB 与 FinMTEB 的跨域 ANOVA 对比（模型因子 × 领域因子）。
- **新增数据集构建**：WikiCompany2Industry（聚类）、FinanceArxiv（聚类）、TheGoldman（检索，基于高盛金融词典），并详述了三阶段过滤/构建流程。

## 4. 资源与算力

- **评测环境**：NVIDIA H800 GPU，批次大小 512。
- **各模型评测耗时**：Echo 最长（约 12 小时），BeLLM 约 11.98 小时，AnglE-BERT 约 8 小时，NV-Embed v2 最高效（约 5.6 小时）。
- **Fin-E5 训练**：论文仅说明训练 100 步、批次大小 128、数据量 19,467 条，并使用 Qwen2.5-14B/72B 做数据合成；但**未明确报告训练所用的 GPU 数量、总训练时长及算力成本**。

## 5. 实验数量与充分性

- **实验数量**：在 FinMTEB 上评估 15 个来源多样的模型（覆盖传统基线、中小型编码器、7B 级 LLM 嵌入模型、商业 API），在 7 个任务的 64 个数据集上进行系统评测；此外进行了跨基准（MTEB vs. FinMTEB）的 7 模型 × 2 领域 × 500 次自助抽样 ANOVA 分析。
- **充分性分析**：
  - **优点**：模型覆盖类型全面，涵盖不同规模、架构和领域适配程度；统计检验（ANOVA、配对 t 检验、Spearman 相关）增强了结论的可靠性；新增了多个此前缺失的金融数据集；中英双语覆盖。
  - **不足**：主实验仅聚焦英文（中文评估在附录且模型覆盖较少）；未做消融实验（如不同数据增强策略、不同训练步数、不同负样本数量的影响未被单独验证）；部分基线模型（如 BOW）的优越性缺乏深入机制分析；训练数据与基准数据的重叠风险虽有排查但未能完全杜绝。

## 6. 论文的主要结论与发现

1. **领域适配显著提升表现**：FinBERT 比 BERT 平均提升 15.6%；Fin-E5 比通用版 e5-mistral-7b-instruct 平均提升 4.5%，在分类任务（0.7565 vs. 0.6449，p = 0.0206）和检索任务（0.7105 vs. 0.6749，p = 0.0489）上达到统计学显著。
2. **Fin-E5 在 FinMTEB 上达到 SOTA**（平均分 0.6767，超越所有开源和商业模型），且仅需 100 步微调即可获得。
3. **通用基准无法预测金融任务表现**：模型在 MTEB 与 FinMTEB 上的排名相关性在统计上不显著（p > 0.05）；ANOVA 显示领域因子在所有任务上显著（p < 0.001），且解释了比模型因子更大的方差。
4. **反直觉发现**：传统 BoW 模型（0.4845）在金融 STS 任务上**超过了所有稠密嵌入模型**，推测原因是金融年报文本中存在大量标准化披露用语，BoW 通过精确词匹配获益，而稠密模型因未针对该领域词汇微调而表现不佳。
5. **金融文本的独特性得到量化验证**：FinMTEB 文本在句长、依赖距离等语言特征上显著不同于通用 MTEB 文本。

## 7. 优点

- **首个综合性金融嵌入基准**：FinMTEB 涵盖 64 个数据集、7 类任务、中英双语，是目前覆盖面最广的金融嵌入评测体系，填补了该领域空白。
- **模型开源贡献**：同时开源基准和 Fin-E5 模型，为社区提供了可复用的基础资源。
- **创新的数据增强方法**：Persona-based 数据合成框架能够系统地生成多样化、任务相关且上下文一致的金融训练三元组，是一种可推广的领域适配范式。
- **严格的数据完整性控制**：训练数据与基准数据进行了重叠检查，避免评估泄漏。
- **严谨的统计方法**：使用 ANOVA、配对 t 检验、自助法等多种统计手段支撑结论，特别是使用跨基准 ANOVA 验证了领域专用基准的必要性。
- **发现具有实践指导价值**：BoW 在 STS 上反超稠密模型的现象提醒研究者关注稠密嵌入在金融领域（尤其是标准化文本）中的核心局限。

## 8. 不足与局限

- **数据污染风险**：基准中部分数据集来自公开来源，可能已出现在某些商业或开源模型的训练集中，影响比较的公平性。
- **评估范围受限**：Fin-E5 与当前评估管线仅覆盖英文，中文评估仅验证少量多语言模型，未能体现 Fin-E5 在中文上的表现（其 Avg. 0.6364 低于 text-embedding-3-large 的 0.6067 部分任务评估，但缺少 Fin-E5 中文适配的训练细节）。
- **消融实验缺失**：未系统地验证各组件（persona 数据生成、困难负样本挖掘、指令模板、训练步数）的独立贡献。
- **合成数据局限性**：训练文档由 LLM 生成，可能存在事实性错误或与真实金融文档的分布偏差，模型学到的是"类金融"文本而非真实金融文本语义。
- **任务覆盖不均衡**：部分任务数据集数量偏少（如 STS 2 个英文数据集、Summ. 3 个），统计功效受限；p 值在 Clustering 和 Summarization 上不显著也印证了这一点。
- **分析深度有限**：对 BoW 在 STS 上反超的现象给出了推测性解释，未设计进一步实验验证该假设（如分析词汇重叠度与性能的关系等）。

（完）
