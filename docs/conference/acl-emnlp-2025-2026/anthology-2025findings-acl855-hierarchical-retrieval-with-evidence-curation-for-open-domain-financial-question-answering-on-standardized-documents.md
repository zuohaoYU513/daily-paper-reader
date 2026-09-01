---
title: Hierarchical Retrieval with Evidence Curation for Open-Domain Financial Question Answering on Standardized Documents
title_zh: 面向标准化文档的开放域金融问答中的分层检索与证据整理
authors: "Jaeyoung Choe, Jihoon Kim, Woohwan Jung"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.855.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 面向金融文档的分层检索与证据整理RAG框架，改善事实性
tldr: 金融领域的标准化文档（如 SEC 文件）包含大量相似格式和表格，容易让传统 RAG 检索到近重复片段，导致检索冗余和答案不完整。针对这一问题，本文提出 HiREC 框架，先进行分层检索以减少相似文本之间的混淆，再从选定的文档中筛选最合适的证据。在开放域金融问答任务上，HiREC 显著提升了答案的准确性和完整性，表明层次化检索与证据整理是提升金融 RAG 系统知识和事实性的有效途径。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl855/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 737, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl855/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl855/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 776, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl855/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 757, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl855/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 620, \"height\": 418, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 617, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 789, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 835, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 801, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1655, \"height\": 842, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 781, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 796, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 776, \"height\": 1084, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 796, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 797, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1643, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1644, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1645, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1655, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1656, \"height\": 615, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl855/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1539, \"height\": 1371, \"label\": \"Table\"}]"
motivation: 标准化金融文档中的近重复文本导致RAG检索冗余，影响问答准确性和完整性。
method: 提出 HiREC，先分层检索相关文档，再从文档中精选证据以支撑最终回答。
result: 在开放域金融问答实验中，HiREC 显著提高了检索相关性和答案质量。
conclusion: 为金融领域 RAG 提供了层次化证据选取方案，有助于提升模型的事实性表现。
---

## Abstract
Retrieval-augmented generation (RAG) based large language models (LLMs) are widely used in finance for their excellent performance on knowledge-intensive tasks. However, standardized documents (e.g., SEC filing) share similar formats such as repetitive boilerplate texts,and similar table structures. This similarity forces traditional RAG methods to misidentify near-duplicate text, leading to duplicate retrieval that undermines accuracy and completeness. To address these issues, we propose the Hierarchical Retrieval with Evidence Curation (HiREC) framework. Our approach first performs hierarchical retrieval to reduce confusion among similar texts. It first retrieve related documents and then selects the most relevant passages from the documents. The evidence curation process removes irrelevant passages. When necessary, it automatically generates complementary queries to collect missing information. To evaluate our approach, we construct and release a Large-scale Open-domain Financial (LOFin) question answering benchmark that includes 145,897 SEC documents and 1,595 question-answer pairs. Our code and data are available at https://github.com/deep-over/LOFin-bench-HiREC.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

论文题目：**Hierarchical Retrieval with Evidence Curation for Open-Domain Financial Question Answering on Standardized Documents**（面向标准化文档的开放域金融问答中的分层检索与证据整理）

作者：Jaeyoung Choe, Jihoon Kim, Woohwan Jung（汉阳大学）

---

## 1. 核心问题与研究动机

- **金融文档的高度标准化**：SEC 文件（如 10-K、10-Q、8-K）在公司和年份之间遵循统一模板，包含大量重复的样板文本（boilerplate）和结构相似的表格，如 Amazon、Meta、Walmart 的 10-K 表格标题和指标几乎一致，仅数值不同。
- **传统 RAG 的缺陷**：标准检索会将语义相似的近重复文本混淆，导致检索到冗余或不相关的段落，难以区分不同公司/年份的同一指标，从而影响答案的准确性和完整性。
- **现有金融 QA 基准的不足**：已有开放域金融 QA 数据集（如 Financebench、SEC-QA）规模小（至多约 1,300 篇文档），测试集有限，无法反映真实金融场景中的大规模检索挑战。
- **目标**：提出一种能应对标准化文档近重复问题的检索增强框架，并构建大规模开放域金融 QA 基准。

## 2. 方法论：HiREC（Hierarchical Retrieval with Evidence Curation）

HiREC 由两个核心组件构成：**分层检索（Hierarchical Retrieval）** 和 **证据整理（Evidence Curation）**。

### 2.1 分层检索

先检索相关文档，再在文档内检索相关段落，以缩小候选范围、减少近重复文本造成的混淆。

- **文档检索器（Document Retriever）**：
  - 索引：对每份文档的封面页用 LLM 生成摘要，再用 Bi-Encoder（E5 模型）生成嵌入向量存入文档库。
  - 检索过程三步：
    1. 用 LLM 将原始问题改写成聚焦的检索查询（去除干扰性金融术语）；
    2. 用 Bi-Encoder 进行稠密检索，取 top-\(k'_D\) 候选文档；
    3. 用 Cross-Encoder（DeBERTa-v3）对候选文档重排，取 top-\(k_D\) 最终文档。

- **段落检索器（Passage Retriever）**：
  - 在最终文档集合内，用 Cross-Encoder 对每个段落打分，取 top-\(k_P\) 段落。
  - 为解决预训练模型不擅长处理财务表格的问题，在 FinQA 训练集上对 Cross-Encoder 进行微调，正例为证据页上的表格段落，负例为其他页面的表格，使用二元交叉熵损失。

### 2.2 证据整理

检索段落可能包含无关信息，也可能缺少关键证据，因此设计证据整理流程：

- **段落过滤器（Passage Filter）**：过滤掉与问题无关的段落，保留最相关的至多 \(k'_P\) 段。
- **可回答性检查器（Answerability Checker）**：判断当前过滤后的段落是否足够回答问题；若足够则进入生成阶段，否则触发补充检索。
- **补充问题生成器（Complementary Question Generator）**：分析缺失信息，生成一个补充查询（\(q_c\)）用于下一轮检索。

### 2.3 迭代与生成

- 算法最多迭代 \(i_{\text{max}}=3\) 轮；若达到上限，则将补充检索的段落与之前过滤的段落合并后生成答案。
- 答案生成：数值计算类问题采用 **Program-of-Thought (PoT)** 生成 Python 代码；文本推理类问题采用 **Chain-of-Thought (CoT)**。
- 框架中 LLM 的职责分配：查询改写、文档摘要、证据整理使用较小的开源模型（Qwen-2.5-7B-Instruct），答案生成使用 GPT-4o。

## 3. 实验设计

### 3.1 数据集与基准

- 构建并发布 **LOFin（Large-scale Open-domain Financial QA）** 基准：
  - 语料：145,897 份 SEC 文件（2001–2025，S&P 500 公司），来源包括 10-K/10-Q/8-K。
  - QA 对：共 1,595 对（初始版 LOFin-1.4k 有 1,389 对，扩展版 LOFin-1.6k 新增 206 对 SEC-QA 多文档问题至 333 对，总计 1,595 对）。
  - 数据来源：FinQA（封闭域转换开放域）、Financebench（直接采用）、SEC-QA（多文档模板 + 人工标注）。
- 问题类型分为三类：**Numeric (Table)**、**Numeric (Text)**、**Textual**。

### 3.2 对比方法

- 基线包括：GPT-4o Zero-shot、Perplexity、Self-RAG、RQ-RAG、IRCoT、HybridSearch、HHR、Dense（DPR + DeBERTa-v3 重排）等。
- 为保证公平，除 Self-RAG 和 RQ-RAG 使用各自生成器外，其余方法与 HiREC 使用相同的 GPT-4o 生成器。
- 额外对比商业系统：Perplexity（llama-3.1-sonar-large-128k-online）和 SearchGPT（GPT-4o）。

### 3.3 评估指标

- 检索性能：页面级别召回率（Page Recall）和精度（Page Precision）。
- 答案准确率（Answer Accuracy）：数值型答案考虑四舍五入和截断；文本型答案使用 GPT-4o 和 FAMMA 提示进行评估。

## 4. 资源与算力

- 文本仅明确说明：段落检索器微调使用 **单张 GeForce RTX 4090 GPU**，训练配置为 3 epochs、batch size 128、学习率 \(2 \times 10^{-7}\)，负样本数 \(n_{\text{neg}}=8\)。
- **未说明**：具体训练时长、总计算量、每个实验的 API 调用量（但给出了 token 成本统计）以及除微调外的算力要求。
- 整体框架使用较小的开源 LLM（Qwen-2.5-7B）执行中间任务，降低了推理成本；生成器使用 GPT-4o 等商业 API。

## 5. 实验数量与充分性

实验较为全面，主要包括：

- **主实验**：在 LOFin-1.4k 上对比 8 种以上 RAG 方法，按三类问题报告检索性能与答案准确率。
- **消融实验**：移除分层检索（w/o HR）、移除证据整理（w/o EC）、移除微调重排器（w/o Fine-tuning）、移除过滤器（w/o Filter），分析各组件贡献。
- **错误类型分析**：按公司级错误对比各方法 top-1 段落的准确性。
- **迭代分析**：展示随着证据整理迭代次数增加，召回率、精度和所需段落数的变化。
- **精度-召回曲线**：比较 HiREC 与基线的 PR 曲线。
- **成本效率比较**：统计检索与生成阶段的输入/输出 token 数和 API 成本。
- **不同生成器实验**：使用 Qwen-2.5-7B、DeepSeek-R1-Distill-Qwen-14B、GPT-4o 作为生成器，验证 HiREC 的鲁棒性。
- **按数据源分析**：分别评估 Financebench、FinQA、SEC-QA 子集上的性能，讨论数据泄漏风险。
- **扩展基准实验**：在 LOFin-1.6k 上报告结果（附录 A），并按答案类型和数据源分别对比 Dense 与 HiREC。
- **跨领域泛化实验**：在 LegalBench-RAG（隐私合同、ContractNLI、MAUD、CUAD）上评估检索性能，验证框架对新领域结构化文档的适用性。

**充分性评价**：实验覆盖了检索质量、答案质量、各组件贡献、成本效率、模型鲁棒性和跨领域泛化，整体较充分、公平。不过，仍有局限：文本类问题各方法答案准确率高于页面召回，说明 LLM 可能借助内在知识作答，存在数据泄漏风险；SEC-QA 多文档子集难度高，所有方法（包括 HiREC）的绝对性能仍较低。

## 6. 主要结论与发现

- HiREC 在 LOFin-1.4k 上比当前最优传统基线 **Dense** 在页面召回率高 10% 以上、答案准确率高 13% 以上（平均 Accuracy 42.36% vs 29.22%）。
- HiREC 平均仅使用 **3.7 个段落**即可生成答案，说明证据整理显著提升了检索效率。
- 分层检索有效减少公司级错误：先锁定正确公司文档，进而保证段落准确性。
- 证据整理的迭代过程能逐步提升召回率和精度，同时减少冗余文档。
- 小型开源 LLM（Qwen-2.5-7B）也能有效执行证据整理，HiREC + DeepSeek-14B 甚至超过 Dense + GPT-4o 超过 9%，说明框架对生成器有较好鲁棒性，且成本更低。
- 在与商业系统（Perplexity、SearchGPT）的对比中，HiREC 在数值表格和数值文本问题上显著领先。

## 7. 优点

- **针对性强**：专门解决标准化金融文档中近重复文本导致的检索混淆问题，具有明确问题意识。
- **方法设计合理**：分层检索缩小候选空间、证据整理过滤噪音并自动补全缺失信息，形成闭环迭代，逻辑清晰。
- **基准贡献大**：构建并开源大规模开放域金融 QA 基准 LOFin（145,897 文档 / 1,595 QA 对），填补现有数据集规模不足和缺乏多文档场景的空白。
- **实验丰富**：不仅看答案准确性，还分析检索质量、组件消融、成本效率、迭代效果、模型泛化、跨领域能力，结论可信度高。
- **效率与性能兼顾**：使用小模型承担中间任务，显著降低 token 成本和计算开销。
- **开源开放**：代码和数据集公开，便于复现和后续研究。

## 8. 不足与局限

- **对 LLM 依赖较强**：查询改写、证据整理、答案生成均依赖 LLM，小模型（如 Qwen-2.5-7B）能力有限，可能影响整体效果。
- **数据泄漏风险**：FinQA 和 Financebench 是公开数据集，预训练 LLM 可能已在训练中见过，导致文本类问题答案准确率虚高（GPT-4o 零样本即表现较好）。
- **多文档问题性能仍偏低**：SEC-QA 子集要求跨文档推理，HiREC 虽优于基线，但绝对准确率仍处于较低水平（14.17% 等），仍有很大提升空间。
- **语料范围有限**：仅覆盖 S&P 500 公司的 SEC 文件，未考虑更广的金融文档类型（如新闻、电话会议记录），跨领域泛化仅测试法律领域。
- **计算资源信息不完整**：未明确报告整体训练时间和推理消耗，难以完整评估方法的重现成本。
- **证据标注存在误差**：使用 BM25 + NLI 自动选择证据页并辅以人工修正，但 OCR/页合并可能引入少量错误，约 1% 自动标注用例有误。
- **数值推理仍是瓶颈**：即使检索正确，生成阶段也可能因算术推理错误而失败（如自由现金流计算错误），表明表格数值理解和代码执行能力有待加强。

（完）
