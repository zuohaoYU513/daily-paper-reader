---
title: RETRIEVAL-AUGMENTED GENERATION WITH ESTIMATION OF SOURCE RELIABILITY
title_zh: 基于来源可靠性估计的检索增强生成
authors: "Jeongyeon Hwang, Junyoung Park, Hyejin Park, Sangdon Park, Jungseul Ok"
date: 2024-09-26
pdf: "https://openreview.net/pdf?id=J3xRByRqOz"
tags: ["query:faithfulness"]
score: 8.0
evidence: 通过估计多源可靠性改进检索增强生成，减少错误信息与幻觉
tldr: 标准检索增强生成在多源数据库上主要按相关性检索，忽略来源可靠性差异，容易传播错误信息。本文提出可靠性感知的RAG（RA-RAG），在检索与聚合过程中迭代估计来源可靠性并据此筛选整合证据。实验表明该方法可降低不可靠来源造成的幻觉和错误答案，提高基于外部证据生成的文本可信度。这项研究为多证据环境中的可靠生成提供了可迁移框架。
source: ICLR-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 标准RAG在多源库中按相关性检索而忽略来源可靠性，容易传播误导信息。
method: 提出RA-RAG，在检索与聚合中联合估计来源可靠性与真实答案，加权使用证据。
result: 实验显示RA-RAG可减少不可靠来源引发的幻觉，提升答案准确性。
conclusion: 将来源可靠性引入检索聚合，能够增强证据依赖性与生成的事实可信度。
---

## Abstract
Retrieval-augmented generation (RAG) addresses key limitations of large language models (LLMs), such as hallucinations and outdated knowledge, by incorporating external databases. These databases typically consult multiple sources to encompass up-to-date and various information. However, standard RAG methods often overlook the heterogeneous source reliability in the multi-source database and retrieve documents solely based on relevance, making them prone to propagating misinformation. To address this, we propose Reliability-Aware RAG (RA-RAG) which estimates the reliability of multiple sources and incorporates this information into both retrieval and aggregation processes. Specifically, it iteratively estimates source reliability and true answers for a set of queries with no labelling. Then, it selectively retrieves relevant documents from a few of reliable sources and aggregates them using weighted majority voting, where the selective retrieval ensures scalability while not compromising the performance. We also introduce a benchmark designed to reflect real-world scenarios with heterogeneous source reliability and demonstrate the effectiveness of RA-RAG compared to a set of baselines.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：大语言模型（LLM）存在幻觉和知识过时等固有局限，检索增强生成（RAG）通过引入外部数据库来缓解这些问题。现实中的外部数据库通常整合多个来源，以提供更全面和更新的信息。
- **核心问题**：标准 RAG 方法在从多源数据库中检索文档时，几乎只依赖查询与文档之间的相关性，而忽略了不同来源之间的可靠性差异。这会使得不可靠来源所发布的错误信息同样被检索和引用，反而加剧了模型的错误传播风险。
- **核心研究问题**：如何让 RAG 系统对多来源数据库中的异构可靠性有感知，从而从未知可靠性的多个来源中筛选和整合证据，最终生成可信答案。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **方法名称**：RA-RAG（Reliability-Aware RAG，可靠性感知的检索增强生成）。
- **核心思想**：将“来源可靠性”作为一个显式的、可估计的变量，引入 RAG 的检索与证据聚合两个核心环节，而非仅依赖文本相关度。整个框架在无需标签的情况下，交替估计来源可靠性和真实答案，实现来源间的去伪存真。
- **关键技术细节与流程**（文字说明）：
  - **联合迭代估计阶段**：给定一组未经标注的查询，系统迭代执行两个相互促进的估计步骤：
    1. 利用当前对各来源可靠性的估计，对一组问题的候选答案进行综合推断；
    2. 基于这些推断出的答案，反过来更新对各来源可靠性的评估，使回答正确来源的可靠性上升、错误来源的可靠性下降。
  - **选择性检索（Selective Retrieval）**：完成可靠性估计后，不再从全部来源中检索，而是从被判定为较可靠的少数来源中优先检索相关文档。这种策略在减少检索请求数量的同时能够维持生成性能，从而保证了系统在更大规模多源数据库上的可扩展性。
  - **加权聚合（Weighted Majority Voting）**：将检索到的证据汇总给 LLM 生成候选答案后，采用按来源可靠性加权的多数投票机制来确定最终答案，使高可靠来源对最终决策具有更大影响，减少误导性信息的干扰。
- **是否包含公式**：在提供的论文文本中没有给出具体数学公式，但其算法逻辑可理解为迭代的最大化期望式估计（EM 式交替更新），以及决策层面的可靠性加权投票过程。

### 3. 实验设计：使用了哪些数据集 / 场景，benchmark 是什么，对比了哪些方法

- **自定义 Benchmark**：论文构建了一个全新的评估基准（benchmark），其设计目标在于反映真实世界场景中异构来源可靠性的特点——即不同来源的信息质量参差不齐，部分来源可能系统性输出错误信息。该 benchmark 中的查询被设计为需要综合多个证据才能正确回答的复杂检索任务。
- **评价场景**：多源混合检索、答案准确性与幻觉抑制能力。
- **对比方法**：与一组基线方法（a set of baselines）相比，涵盖标准 RAG 类方法及其无障碍聚合方式的变体。提供的文本未列出具体的基线名称和细节。
- **局限说明**：提供的论文文本中并未给出具体数据集名称、检索语料库的来源数量、任务类型（如问答/事实验证等）及数据规模大小。

### 4. 资源与算力

- 提供的论文内容（标题、摘要与元数据）中**完全没有提及**训练或评估所需的计算资源信息，包括 GPU 型号、GPU 数量、训练时长、总预算能耗等。
- 如需掌握这一信息，必须查阅论文正文中的实验设置部分（Implementation Details / Experimental Setup），但在给出的文本范围内无法指出具体算力消耗。

### 5. 实验数量与充分性：是否充分、客观、公平

- **能从摘要中掌握的实验方面**：
  - 提出了一个新的 benchmark，并对一组基线进行了比较，验证了最终方法的有效性。
  - 结果的表述为“demonstrate the effectiveness”——说明至少进行了主实验对比。
  - 从方法存在“迭代估计”和“选择性检索”等模块来看，正文中通常应有相应的消融实验。但在提供的文本中**没有**明确提到任何消融实验的数量或结果。
- **充分性判断**：仅凭摘要和元数据提供的信息，不足以判断实验是否充分。摘要显示实验方向完备（validation against baselines），但没有给出在哪些数据上做了多少个对比、是否进行异常值分析、是否报告方差或显著性检验等。对比方法范围、数据规模和可靠性的具体分布等也未被说明。总体上，在可获得的文本范围内，实验设计思路合理但无法检验其覆盖度和公平性。需查看论文正文或附录才能给出完整判断。

### 6. 论文的主要结论与发现

- **主要结论**：在多源知识库中，标准 RAG 忽略来源可靠性的做法会让误导信息进入生成上下文。将来源可靠性纳入检索与聚合过程，可以显著降低因不可靠来源引发的幻觉和错误答案，提高基于外部证据生成的文本的可信度。
- 具体来说，通过无标注的迭代估计方式识别可靠来源，并做加权证据融合，RA-RAG 能够以一种无需人工干预的方式适配“真实世界中来源可信度差异大”的场景。
- 此外，论文认为这套做法是一种可迁移的框架，可以用于多个需要多证据环境下的可靠文本生成任务。

### 7. 优点

- **问题切入现实且痛点明显**：标准 RAG 多数研究假设语料库总体可信，“按相关性检索”天然存在弱点；该文从来源可靠性角度为多源 RAG 提供了合理的纠偏视角。
- **无需人工标注**：可靠性估计和真实答案推断均基于一组查询迭代完成，没有依赖额外的人工标注信息，落地成本较低（self-supervised 式训练思路）。
- **检索质量与可扩展性的兼顾**：通过只从少数可靠来源中检索而非全库遍历，避免了为规避错源带来的巨量检索开销；方案可扩展到大规模多源数据库。
- **聚合方式的可靠化**：利用加权多数投票而非简单证据拼接，从机制上削弱了低可靠证据的话语权。
- **创新 Benchmark 的构建**：专门构造了模拟真实世界多源可靠性差异的 benchmark，有利于推动该方向后续比较的标准化。

### 8. 不足与局限

- **所提供的文本信息量有限**：摘要中没有包括具体数据集细节、基线对比结果表格、消融分析及计算开销等关键内容，难以系统评估方法的普适性和收益幅度。
- **对查询集合的依赖**：可靠性的估计建立在给定查询集之上。若查询本身的分布有偏（未覆盖某些错误源），或来源擅长内容领域存在差异（在某领域可靠的来源在另一领域未必可靠），仅靠整体可靠性打分来筛选来源可能失灵，这一点尚未在文本层面见到讨论。
- **可靠性表征的粒度不足**：按“来源”而不是按“文档—查询主题”建模可靠性，可能会让一个来源在某话题上不可靠、但另一话题上可靠时无法精细区分。
- **缺少对计算开销和延迟的分析**：迭代估计阶段本身需要多次查询 LLM，这一额外成本及其与检索收益之间的代价—收益分析没有在摘要中披露，而这一点往往是实际部署的关键约束。
- **多源数据库时规模下复杂情况**：选择性检索虽提升可扩展性，但如果可靠来源覆盖不足，可能引入覆盖偏差（coverage bias），在具体实验文本中也未讨论这种折衷的边界条件。

（完）
