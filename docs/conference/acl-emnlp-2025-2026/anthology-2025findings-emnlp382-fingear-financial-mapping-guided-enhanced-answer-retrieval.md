---
title: "FinGEAR: Financial Mapping-Guided Enhanced Answer Retrieval"
title_zh: FinGEAR：金融映射引导的增强答案检索框架
authors: "Ying Li, Mengyu Wang, Miguel de Carvalho, Sotirios Sabanis, Tiejun Ma"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.382.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 面向10-K文件的金融检索框架，改进RAG以支持事实性
tldr: 针对金融披露文件（如10-K）长度大、层次复杂且RAG模型利用不充分的问题，提出FinGEAR检索框架。它结合金融词典指导词项级引导、双层分层索引（摘要树和问题树）以及两阶段交叉编码器重排序，使检索与披露结构和术语对齐。在FinQA数据集上，该方法在精确率、召回率和F1上均取得一致提升。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp382/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1596, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp382/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1580, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp382/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 622, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp382/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 770, \"height\": 336, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1648, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1649, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 800, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1624, \"height\": 903, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 679, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1653, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1648, \"height\": 304, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp382/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1554, \"height\": 856, \"label\": \"Table\"}]"
motivation: 标准RAG模型未充分利用金融披露文件的结构和术语，检索性能受限。
method: 融合金融词典、双层分层索引和两阶段重排序，实现细粒度、查询感知的上下文选择。
result: 在FinQA数据集上显著提升精确率、召回率和F1。
conclusion: 为金融文档检索提供领域定制化RAG方案，有助于金融信息的事实性获取。
---

## Abstract
Financial disclosures such as 10-K filings pose challenging retrieval problems because of their length, regulatory section hierarchy, and domain-specific language, which standard retrieval-augmented generation (RAG) models underuse. We present Financial Mapping-Guided Enhanced Answer Retrieval, a retrieval framework tailored to financial documents. FinGEAR combines a finance lexicon for Item-level guidance (FLAM), dual hierarchical indices for within-Item search (Summary Tree and Question Tree), and a two-stage cross-encoder reranker. This design aligns retrieval with disclosure structure and terminology, enabling fine-grained, query-aware context selection. Evaluated on full 10-Ks with the FinQA dataset, FinGEAR delivers consistent gains in precision, recall, F1, and relevancy, improving F1 by up to 56.7% over flat RAG, 12.5% over graph-based RAGs, and 217.6% over prior tree-based systems, while also increasing downstream answer accuracy with a fixed reader. By jointly modeling section hierarchy and domain lexicon signals, FinGEAR improves retrieval fidelity and provides a practical foundation for high-stakes financial analysis.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 金融披露文件（如 SEC 10-K 年报）是投资分析、监管监测和风险评估的关键来源，但它们篇幅长（常超 100 页）、按 SEC 强制规定的 Item（如 Item 1、1A、7、8）组织，且混合叙述文本、表格和脚注。
- 现有 RAG 系统在金融领域检索面临三大核心限制：
  1. **缺乏结构感知**：固定大小分块割裂了披露的逻辑层次，导致上下文错位。
  2. **缺乏金融领域特定性**：通用检索器难以区分细粒度但关键的概念（如“净收入” vs.“营业收入”）。
  3. **纯稠密检索难控制和解释**：向量相似度在需要证据支撑的高风险场景中可解释性不足。
- 论文提出 FinGEAR（Financial Mapping-Guided Enhanced Answer Retrieval），一个面向金融文档的“检索优先”框架，将检索视为一流目标，专门适配监管文件的结构和术语，从而为金融 NLP 任务提供更忠实、可解释的证据选择。

## 2. 论文提出的方法论

FinGEAR 是一个模块化检索框架，核心思想是**用文档结构与领域词汇共同引导检索**。主要技术组件如下：

- **预检索（Pre-Retrieval）管线**：
  1. **结构提取**：
     - 将每个 10-K Item 切成约 2,000 token 的块（100 token 重叠），用金融微调的句子编码器嵌入。
     - 采用 UMAP（降至 10 维）+ 高斯混合模型（GMM，最多 50 个簇）自底向上构建层次树。
     - 生成两个拓扑相同的索引：**Summary Tree**（内部节点存摘要，叶子为原始文本块）和 **Question Tree**（内部节点存 LLM 生成的子问题嵌入，叶子指向相同块 ID）。
  2. **金融词典感知映射（FLAM）**：
     - 从 FinRAD 词典提取候选金融术语，用金融微调嵌入聚类成潜在主题。
     - 基于相对频率计算每个 Item 的权重 \( w_i = \text{freq}_i / \sum_j \text{freq}_j \)。
     - 将总检索预算 k 按权重分配为每个 Item 的预算 \( k^*_i = \text{round}(k \cdot w_i) \)，用于跨 Item 的全局导航。
- **检索中（In-Retrieval）管线**：
  1. **全局导航**：FLAM 识别查询中的金融关键词并扩展为术语簇，映射到相关 Item 并分配预算，跳过权重为 0 的 Item。
  2. **Item 内搜索（双树遍历）**：
     - Summary Tree：用 BM25 对节点摘要进行稀疏匹配。
     - Question Tree：用余弦相似度对查询嵌入与子问题嵌入进行稠密匹配。
     - 各树独立遍历，每层只扩展得分最高的 b 个子节点（默认 b=3），直到叶子，合并两树候选并去重。
  3. **两阶段重排序**：
     - 第一阶段跨树：用交叉编码器 BAAI/bge-reranker-large 对候选统一重排。
     - 第二阶段跨 Item：对来自不同 Item 的候选池再次重排，选出全局最有信息量的段落。
- 整体流程可概括为：FLAM 决定“去哪儿找”（Which Items），双树决定“怎么搜”（Within-Item），两阶段重排序提升精度与覆盖率。

## 3. 实验设计

- **数据集**：
  - 使用 **FinQA** 数据集（8,281 个问答对，来自 10-K 文件，需数值推理与领域知识），分为训练 6,251、验证 883、测试 1,147。
  - 通过 SEC EDGAR 恢复与每个 FinQA 实例对应的原始完整 10-K 文件，构建了 **720 份完整 10-K 文件**的语料库，覆盖 S&P 500 公司（1999–2019），跨多个行业。
- **评估框架**：
  - 使用 RAGAS 框架的指标：**Precision、Recall、F1、Relevancy**，分别在 **Top-5、Top-10、Top-15** 三个深度下评估。
  - 下游评估：固定 GPT-4o-mini 为 reader，仅变化检索器，报告最终答案准确率。
- **对比方法**：
  - General RAG（平坦检索）、Self-RAG、LightRAG（mix 模式）、GraphRAG（local-global 社区遍历）、RAPTOR（树状递归处理）。
  - 基线使用默认设置，稠密相似度采用 text-embedding-ada-002；FinGEAR 使用 BM25s + 金融微调嵌入（FinLang + FinQA/FinRAD fine-tune）和 bge-reranker-large。
- **消融实验**：
  - 单组件消融：去掉 Summary Tree、Question Tree、FLAM、Reranker。
  - 多组件消融：同时去掉 FLAM+Summary Tree、FLAM+Question Tree。
  - 词典权重策略对比：相对频率、对数加权、Softmax 加权。
  - 问题类型细分：数值 vs. 分类，简单 vs. 复杂（多跳）。

## 4. 资源与算力

- **嵌入微调**：在单个 **NVIDIA A100-SXM4-80GB GPU** 上完成。
  - FinQA 嵌入训练（6,251 train / 1,147 test）约 **1,972 秒**。
  - FinRAD 嵌入训练（17,300 train / 5,190 test）约 **3,607 秒**。
  - 二者均训练 50 epochs，使用 Matryoshka 表示学习和 MultipleNegativesRankingLoss。
- **推断环境**：在 MacBook Pro M3 Max（64GB RAM）上测试，平均检索延迟约 **17.58 秒**（含树遍历、FLAM 打分、重排序）。
- **API 成本**：用 gpt-4o-mini 构建一份 127 页 10-K 的索引约 $0.11，单次查询成本约 $0.00048（Top-5）至 $0.00100（Top-15）。
- 注意：论文未说明 A100 GPU 的具体数量（但提到“单个”），也未报告多卡并行或大规模推理成本细节。

## 5. 实验数量与充分性

- **实验量丰富**：包括主检索性能对比（5 个基线 × 3 深度 × 4 指标）、下游 QA 准确率、单组件消融、多组件消融、词典权重策略消融、问题类型子分析、错误分析示例、token 统计和延迟报告。
- **充分性**：
  - 主实验覆盖了代表性的平坦型、图型、树型 RAG 基线，对比逻辑合理。
  - 消融实验验证了每个模块的必要性，并揭示了模块间互补关系。
  - 固定 reader 使得检索效果的差异归因于检索器本身，公平性较好。
- **客观性/公平性**：
  - 所有系统使用相同分块策略和 reader，但注意 LightRAG 的检索结果混合了实体、关系和向量文本，可能导致精度虚高且运行时间约为 FinGEAR 的 15 倍（论文指出）。
  - 评估仅基于 FinQA 数据集，且 FinQA 每题只标注一个相关 span，可能低估召回率；榜单覆盖有限。
  - 消融实验在部分深度下呈现性能波动（如 k=10 时某些设置 F1 高于 k=5），说明稳定性仍有提升空间。

## 6. 论文的主要结论与发现

- FinGEAR 在 **Precision、Recall、F1、Relevancy** 上，在各检索深度（k=5,10,15）均全面优于所有基线。
  - F1 相比平坦 RAG 最高提升 **56.7%**，相比图型 RAG 最高提升 **12.5%**，相比树型 RAG 最高提升 **217.6%**（摘要中数据）。
  - 在 k=15 时 Recall 达 **0.65**，F1 稳定在 **0.68**，Relevancy 峰值 **0.64**。
- 下游答案准确率方面，FinGEAR 在 k=5 和 k=15 上最高（**49.1% / 50.0%**），在 k=10 上略逊于 LightRAG 的异常尖峰（58.8%），但总体更稳定并随 k 增加而提升。
- 消融实验显示：
  - 去除 Summary Tree 或 Question Tree 均会大幅降低 F1（k=5 时从 0.69 降至 0.37 左右），说明双树互补。
  - 去除 FLAM 也会造成明显下降，且引入跨深度不稳定性。
  - 多组件同时去除导致性能进一步复合下降，证明模块间协调设计的重要性。
  - 相对频率权重在 FLAM 中优于对数和 Softmax 加权。
- 问题类型分析：分类问题 F1 更高（0.81@k=10），数值问题 Relevancy 更高（0.64@k=10）；复杂多跳问题 F1 略低但在大 k 时 Relevancy 提升，说明双树检索能较好覆盖分散证据。

## 7. 优点

- **结构感知**：利用 SEC Item 层次和文档内部主题聚类，替代平坦分块，检索结果保持逻辑连贯性。
- **领域自适应**：FLAM 将金融术语映射到披露章节，提供全局导航，并能随语料更新词典。
- **混合检索**：BM25 稀疏匹配与金融微调稠密嵌入结合，兼顾可解释性与语义相关性。
- **双树设计**：Summary Tree 提供高层摘要路由，Question Tree 将节点转化为子问题，在查询空间中增强匹配，二者共享拓扑但承载不同信号。
- **两阶段重排序**：先跨树融合再跨 Item 选择，提升全局信息质量。
- **模块化与可解释性**：组件可独立替换，检索路径透明，便于审计和调整（如词典权重、重排序灵敏度）。
- **实证充分**：通过多项消融和问题类型细分，明确归因于各模块贡献，而非黑盒效应。

## 8. 不足与局限

- **领域特定性**：只在美式 10-K 报告上验证，对非结构化金融文档（如财报电话会议）或其他国家/地区报告的可迁移性未测试。
- **词典依赖**：依赖跨文件稳定的金融术语，新兴术语或行业特定表达可能削弱关键词映射和聚类的质量。
- **解析敏感**：假设文档解析准确且结构一致，OCR 错误或 HTML 转文本错位会破坏树构建和检索。
- **缺乏推理能力**：FinGEAR 仅做语义检索，不执行显式财务推理或计算（如比率计算、时序预测），数值理解仍靠下游模型。
- **评估覆盖有限**：基于单个数据集（FinQA），且每题仅一个标注 gold span，可能低估真实召回表现；未在 DocFinQA 或多数据集上系统评估。
- **源偏见**：不引入新偏见，但会继承公司在披露中的选择性陈述（如省略或淡化风险）造成的报告偏差。
- **潜在风险**：检索可能因语义漂移或歧义而漏检最相关披露；下游 LM 可能基于证据产生错误或投机性推理，需人工验证。

（完）
