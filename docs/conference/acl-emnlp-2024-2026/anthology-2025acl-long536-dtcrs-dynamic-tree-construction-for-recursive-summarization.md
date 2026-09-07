---
title: "DTCRS: Dynamic Tree Construction for Recursive Summarization"
title_zh: DTCRS：面向递归摘要的动态树构建
authors: "Guanran Luo, Zhongquan Jian, Wentao Qiu, Meihong Wang, Qingqiang Wu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.536.pdf"
tags: ["query:faithfulness"]
score: 6.0
evidence: 动态构建递归摘要树，为抽象式问答生成提供精简且去冗余的证据
tldr: RAG中的递归摘要构建会生成大量冗余摘要节点，增加构建时间并可能损害问答效果，且并非所有问题都适用。DTCRS根据文档结构和查询语义动态判断是否及如何构建摘要树，避免不必要的递归摘要。该方法能够在多步推理问答中保留必要证据并显著减少冗余节点。实验显示DTCRS提升了RAG抽象式问答的效率与质量，为证据受限生成提供了更自适应的中间证据准备方式。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 699, \"height\": 233, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1660, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 645, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 780, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 735, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1301, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1498, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1374, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1457, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1499, \"height\": 336, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long536/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1501, \"height\": 368, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 478, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 418, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1648, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 806, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 806, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 484, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1643, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1647, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1639, \"height\": 2167, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 800, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 644, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long536/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 494, \"height\": 557, \"label\": \"Table\"}]"
motivation: 递归摘要树存在过多冗余节点，构建耗时且可能对问答产生负面影响，且并非所有问题都需要递归摘要。
method: 提出DTCRS，依据文档结构和查询语义动态生成摘要树，决定是否进行递归摘要以降低冗余并适配问答需求。
result: DTCRS能减少摘要树冗余并提升RAG问答的效率和质量，实证了动态树构建的有效性。
conclusion: 面向文档结构与查询语义的动态摘要树构建可以更有效地为抽象式生成提供证据支撑。
---

## Abstract
Retrieval-Augmented Generation (RAG) mitigates the hallucination problem of Large Language Models (LLMs) by incorporating external knowledge. Recursive summarization constructs a hierarchical summary tree by clustering text chunks, integrating information from multiple parts of a document to provide evidence for abstractive questions involving multi-step reasoning. However, summary trees often contain a large number of redundant summary nodes, which not only increase construction time but may also negatively impact question answering. Moreover, recursive summarization is not suitable for all types of questions. We introduce DTCRS, a method that dynamically generates summary trees based on document structure and query semantics. DTCRS determines whether a summary tree is necessary by analyzing the question type. It then decomposes the question and uses the embeddings of sub-questions as initial cluster centers, reducing redundant summaries while improving the relevance between summaries and the question. Our approach significantly reduces summary tree construction time and achieves substantial improvements across three QA tasks. Additionally, we investigate the applicability of recursive summarization to different question types, providing valuable insights for future research.

---

## 论文详细总结（自动生成）

# DTCRS：面向递归摘要的动态树构建 — 论文总结

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **背景问题**：RAG 通过注入外部知识来缓解大语言模型的幻觉问题，但大多数 RAG 仅检索连续短文本块，难以支持需要整合文档多个部分信息的多步推理问题。
- **已有方法**：递归摘要（如 RAPTOR）通过分层聚类和摘要构建层级摘要树，以在不同粒度整合分散信息，为抽象式问答提供证据。
- **现有缺陷**：
  - 传统摘要树是**静态树**，基于文档本身构建，而忽略查询语义，导致大量的**冗余摘要节点**与查询无关。
  - 冗余节点不仅增加构建时间和计算开销，还可能使最终生成引入无关干扰信息，**降低回答正确率**。
  - **并非所有类型的问题都适用递归摘要**。对提取式、布尔式等简单问题，递归摘要可能并无帮助甚至造成干扰。
- **核心目标**：动态地决定是否以及如何构建摘要树，使摘要与查询相关、减少冗余节点并提高效率，同时探索递归摘要对不同问题类型的适用边界。

## 2. 方法论：DTCRS

### 2.1 总体框架

DTCRS 的整体流程为：

1. 基于文档生成**目录（ToC）**；
2. 利用分类器判断问题是否需要做递归摘要；
3. 若需要，基于 ToC 将原始问题分解为若干子问题；
4. 以子问题 embedding 作为**初始聚类中心**，对文本块进行递归聚类与摘要，构建动态摘要树；
5. 最终采用 collapsed-tree 检索方式将相关节点送入 LLM 回答。

### 2.2 问题类型分类

- 先由 LLM 生成文档目录 `c`，再输入原始问题 `q`，由二分类器输出：

  `y = f_LLM(q, c) ∈ {0, 1}`

- 判断标准：该问题**是否复杂、是否需综合目录中多个段落的信息**。
- `y=1` 时递归构建摘要树；`y=0` 时直接使用 DPR 检索 top-K 文本块。

### 2.3 动态摘要树构建

（1）问题分解

- 输入 ToC 和原始问题，使用 LLM 生成子问题集合 `Q' = {q1, ..., qj}`。
- 引入 ToC 的原因：限制子问题范围，使其贴合文档不同章节的主题；将子问题与文档结构对齐。

（2）文本分块

- 为控制构建开销，不使用复杂语义分割，采用固定 token 长度（500 tokens）切分。
- 跨越边界的不完整句子整体移至下一块，避免块内出现截断句。

（3）聚类

- 第一层聚类中，以子问题数作为聚类数，以子问题 embedding 作为 GMM（高斯混合模型）各簇的初始中心，使聚类结果向查询语义偏移。
- 采用 UMAP 将文本块 embedding 与子问题 embedding 统一降维，保证语义空间一致。
- 后续层（子问题数大等于文本块数等情况）使用 BIC 确定聚类数、随机初始中心。
- 使用**全局聚类**代替 RAPTOR 采用的分层聚类，减少簇数，提升效率。

（4）递归摘要生成

- 对同一簇内的文本块调用 LLM 生成摘要；重复聚类与摘要直至不可再分。

### 2.4 检索方式

- 比较了 tree traversal 与 collapsed tree。由于后者性能更稳定，实验中**采用 collapsed tree**：将所有节点展平，按余弦相似度取 top-k，以最大 token 数（3500）为上限不断补充候选节点。
- 对非抽象类问题，仅使用 DPR top-5 检索。

## 3. 实验设计

### 3.1 数据集与评测指标

| 数据集 | 问题数 | 平均文档字符数 | 主要问题类型 |
|---|---|---|---|
| QASPER | 1451 | 约 2.2 万 | 包含 extractive、abstractive、boolean、unanswerable 四类 |
| QuALITY | 2128 | 约 2.5 万 | 长文档多项选择，含 hard 子集 |
| NarrativeQA | 10558 | 约 33.2 万 | 超长文档，以简单 extractive 问题为主 |

- QASPER：token-level F1；
- NarrativeQA：BLEU-1/4、ROUGE-L、METEOR；
- QuALITY：accuracy（含 SAT-style Score、hard subset）。

### 3.2 使用模型与对比方法

- LLM：GPT-4、GPT-4o-mini、DeepSeek-V2-Lite-Chat（7B）；embedding 为 SBERT；检索为 DPR。
- 核心对比方法：
  - DPR；
  - RAPTOR；
  - 各任务原 SOTA：NarrativeQA（BiDAF、BM25+BERT、Recursively Summarizing Books、Retriever+Reader）；QuALITY（Longformer-base、DPR+DeBERTaV3-large、CoLISA+DeBERTaV3-large）；QASPER（LongT5 XL、CoLT5 XL）。

### 3.3 主实验结果

- **QASPER**：DTCRS+GPT-4 达到 58.5 F1，显著优于 RAPTOR+GPT-4（55.7）、CoLT5 XL（53.9），实现最佳结果。
- **QuALITY**：DTCRS+GPT-4o-mini 在全体与 hard subset 上分别达到 74.7% 与 62.9%，优于 RAPTOR（67.6% / 57%）等 baseline。
- **NarrativeQA**：DTCRS 仅在 METEOR 上最高（14.4%），其余指标与 DPR/RAPTOR 相当但明显低于 Retriever+Reader（非同一 LLM pipeline）。作者把原因归为 NarrativeQA 缺少需要多步综合推理的抽象式问题。
- 作者进一步对比 abstractive vs non-abstractive 问题，显示 DTCRS 在 abstractive 上收益更大。

### 3.4 消融与过程分析

- 在 QASPER 上对 GPT-4o-mini 和 DeepSeek-V2-Lite-Chat 分别做了消融：移除全局聚类（改用层次聚类）、移除分类器、移除 ToC、移除问题分解器。
- 在 NarrativeQA 上也给出不同组件的完整对比。
- 补充分析包括：不同问题类型的分类比例、节点数量/证据覆盖率对比、构建时间与冗余率下降情况、LLM 输出样例对比，以及不同 UMAP 参数（如 n_neighbors 与降维维度）的敏感度实验。

## 4. 资源与算力

- 论文主要在 NVIDIA A800 80GB PCIe GPU 与 Intel Xeon Silver 4314 CPU 上完成，但**未报告具体 GPU 数量、训练/推理运行时长及总耗能**。
- 相对于传统监督模型，该方法是“多次 LLM inference + 重聚类”的组合流程，核心开销在聚类与递归摘要上。文中给出摘要层构建时间约 40.82 秒，相比 RAPTOR 的 214.39 秒降低约 80.95%，但这仅是单文档（平均规模场景）的构建耗时，不包含预处理和整体全过程的时间统计。
- 由于任务以 LLM 推理驱动而非训练模型，论文“资源成本”汇报并不像训练类论文那样完整。

## 5. 实验数量与充分性

- **实验总量较丰富**：
  - 3 个主流长文本问答数据集；
  - 跨 3 个不同参数规模的 LLM；
  - 主实验、分类别实验、消融实验、节点结构分析、时间效率分析、样本输出对比、UMAP 参数敏感性等多个角度；
  - 附录还给出完整分类别 F1 表，帮助判断方法的类别异质性。
- **充分但非完全公正的方面**：
  - NarrativeQA 上的对比报告中，Retriever+Reader 并非同一 LLM 框架；与同用 LLM 的 DPR/RAPTOR 相比，DTCRS 提升微弱乃至部分下降。
  - QuALITY 只用 GPT-4o-mini 报告；作者说明计算资源有限，更大 GPT-4 仅用在了 QASPER 上。
  - 消融在多个数据集/模型上分布不均：完整消融集中在 QASPER，NarrativeQA 有补充，QuALITY 未有详细逐类消融结果。
- **总体结论**：对支撑“动态树 + 分类触发递归摘要”有效性的证据比较充分，但对大规模 LLM 和更多任务的泛化验证仍有限。

## 6. 主要结论与发现

- **动态摘要树有效**：基于文档结构和查询语义构建，摘要节点数量大幅下降；在保留必需证据的同时显著减少与查询无关的冗余摘要。
- **构建效率改进**：以子问题为簇中心的全局聚类大幅压缩了聚类数量，使摘要层的节点数平均降低约 92.2%，构建时间降低约 80.95%。
- **对抽象式问题尤其适用**：对需要合成多处信息、多跳推理的 abstractive 问题（如 QASPER 中比例较高的一类），DTCRS 比 DPR/RAPTOR 提升显著。
- **问题类型决定工具适用性**：实验验证假设——递归摘要对 extractive 与 boolean 类问题无明显优势、甚至带来负面影响，因此必须先进行问题分类。
- 总体而言，DTCRS 为“何时做递归摘要、如何让摘要围绕查询动态生长”给出了一个可复用、可扩展的结构化方案。

## 7. 优点

- 提出一个**模块化且可解释的检索-摘要 pipeline**：将 ToC 生成、问题分类、问题分解、子问题引导聚类、递归摘要和 collapsed-tree 检索串成一个清晰的流程。
- 充分利用查询语义指导信息组织方式：把子问题的 embedding 作为聚类中心和簇数，使摘要树更“问有所答”，是新颖且直接的改进。
- 明确回答了一个此前未被系统讨论的问题：递归摘要不能无差别用于所有问题；该结论对未来设计 RAG/长文本问答系统具有指导意义。
- 通过大量消融与分类别结果，指出分类器和 ToC 两个模块的贡献，实验逻辑清晰。
- 提供了人工可读的样例对比（RAPTOR vs DTCRS），直观展示冗余证据减少如何改善答案正确性。

## 8. 不足与局限

- **泛化能力有限**：仅在三类 QA 基准上测试，未验证开放式问答、综述写作或其他长上下文推理任务中的表现。
- **对超长文档的策略不健壮**：NarrativeQA 中文档远超 LLM 输入上限时，ToC 生成可能不完整，进而影响子问题分解和摘要质量。
- **模型规模覆盖不均衡**：大模型 GPT-4 只在 QASPER 上使用，未在其他两个任务中与大模型作全面比较；较小的 DeepSeek-V2-Lite-Chat 只在 QASPER 部分做了深入评估，实验完备性受计算资源限制。
- **依赖额外的串行 LLM 调用**：ToC 生成、问题分类、分解与摘要会引入累积延迟及多次 LLM 调用成本；论文未系统性报告端到端时间或 API 消耗。
- **在 NarrativeQA 上的公平性存疑**：与其最强的 Retriever+Reader 对比不处于同一 LLM 框架；和同框架 DPR/RAPTOR 相比，DTCRS 的增益不明显，作者解释合理但缺乏更细粒度的问题分类实验支撑。
- **聚类参数与误差的影响分析不足**：对 GMM 阈值、文本块大小、UMAP 参数的敏感性分析只做了部分探索；且 GMM 软聚类与递归摘要中可能引入误差传播效应，并未逐层分析。
- **未充分讨论安全性/幻觉问题**：尽管作者指出摘要中的轻微幻觉对答案影响不大，但缺少对递归摘要引入伪证据这一风险的系统性风险量化分析。

（完）
