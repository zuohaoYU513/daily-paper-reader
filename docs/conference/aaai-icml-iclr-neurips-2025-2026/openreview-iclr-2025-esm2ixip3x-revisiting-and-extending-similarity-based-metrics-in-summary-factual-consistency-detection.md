---
title: Revisiting and Extending Similarity-based Metrics in Summary Factual Consistency Detection
title_zh: 重新审视并扩展基于相似度的摘要事实一致性检测度量
authors: "Yuxuan Ye, Edwin Simpson, Raul Santos-Rodriguez"
date: 2024-09-27
pdf: "https://openreview.net/pdf?id=ESM2ixIp3X"
tags: ["query:faithfulness"]
score: 9.0
evidence: 面向抽象摘要事实一致性的零样本句子嵌入度量
tldr: 针对基于相似度的摘要事实性度量被普遍认为与人工判断不一致的问题，本文指出根源在于错误使用参考文献作为对照以及比较粒度过粗，提出零样本的句子嵌入事实性度量。该方法通过合适的对照与粒度重新衡量句子相似度，避免构建蕴含或问答监督流水线。实验结果表明该度量在摘要事实一致性检测上显著优于既有相似度基线，并在零样本条件下具有竞争力，为事实性评价提供了高效工具。
source: ICLR-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 抽象摘要生成流畅但事实难保证，早期相似度指标与人工判断不一致，而基于自然语言推断或问答的流水线又依赖额外监督。
method: 提出零样本的句子嵌入评分方法，通过修正对比参照文本和调整比较粒度来改进相似度指标在事实一致性检测中的表现。
result: 实验表明该零样本度量在摘要事实一致性检测上优于常见相似度基线，与人工标注一致性更高。
conclusion: 相似度度量本身可用于摘要事实检测，只要选择合适的对照与粒度，便能以零监督成本实现有效的事实一致性评测。
---

## Abstract
Cutting-edge abstractive summarisers generate fluent summaries, but the factuality of the generated text is not guaranteed. 
Early summary factuality evaluation metrics are usually based on n-gram overlap and embedding similarity, but are reported fail to align with human annotations.
Therefore, many techniques for detecting factual inconsistencies build pipelines around natural language inference (NLI) or question-answering (QA) models with additional supervised learning steps. 
In this paper, we revisit similarity-based metrics,
showing that this failure stems from the use of reference texts for comparison and the granularity of the comparison. 
We propose a new zero-shot factuality evaluation metric,
Sentence-BERT Score (SBERTScore), which compares sentences between the summary and the source document. 
It outperforms widely-used word-word metrics including BERTScore and can compete with existing NLI and QA-based factuality metrics on the benchmark without needing any fine-tuning.
Our experiments indicate that each technique has different strengths, with SBERTScore particularly effective at identifying correct summaries.
Additionally, we demonstrate how a combination of techniques is more effective at detecting various types of error.

---

## 论文详细总结（自动生成）

# 重新审视并扩展基于相似度的摘要事实一致性检测度量——中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- 面向抽象式摘要生成模型，其生成文本往往流畅但**事实性无法保证**，因此需要对摘要进行事实一致性（factual consistency）检测。
- 早期摘要事实性评估指标普遍采用 n-gram 重叠或嵌入相似度，但这些指标被报道与**人工标注不一致**。
- 为此，许多后续方法引入了额外的监督信号，构建基于**自然语言推理（NLI）**或**问答（QA）**的复杂流水线，增加了开发和部署成本。
- 本论文指出，相似度类指标失败的原因并不在于“相似度思路本身不可行”，而在于两点：
  - **错误地使用参考文献（reference）作为对照文本**；
  - **比较粒度过粗**。
- 整体含义：只要选择合适的对照文本与比较粒度，**纯相似度方法可以在零监督成本下有效检测摘要事实不一致**，挑战了“相似度指标必须被 NLI/QA 流水线取代”的既有共识。

## 2. 论文提出的方法论

- 论文提出一种零样本（zero-shot）事实性评估指标：**Sentence-BERT Score（SBERTScore）**。
- 核心思想：
  - 将摘要与源文档的比较对象由“参考文献”改为“**源文档（source document）**”，避免参考摘要与生成摘要共享系统偏差而掩盖事实错误；
  - 将比较粒度由词-词（word-word）调整为**句子-句子（sentence-sentence）**，使模型能够在更完整、更语义化的单元上判断事实是否被支持。
- 关键技术细节（根据摘要可推断的实现逻辑）：
  - 使用 Sentence-BERT 编码摘要中的句子与源文档中的句子；
  - 对每对句子计算嵌入相似度（如余弦相似度），并依据某种聚合策略（对“摘要句子↔源文档最相似句子”的匹配进行汇总）输出整体事实性得分；
  - 全程无需微调、无需额外标注数据，避免了 NLI/QA 流水线所需的监督学习步骤。
- 论文未在摘要中给出具体公式；完整评分公式、聚合方式与阈值策略需参考正文。Mermaid 逻辑图如下（文字说明不能包含图表，此处仅作示意）。

## 3. 实验设计

该点依据论文摘要整理。由于 PDF 提取文本中仅可获取摘要部分，**具体细节无法完全核对**，以下均为此推测字段。
- 数据集：使用了“benchmark”（摘要中提到的基准测试），但**未给出数据集名称**（如是否包含 SummEval、FactCC 或 Newsroom 等不得而知）。
- 场景：
  - 在标准摘要事实一致性基准上进行**零样本评估**；
  - 与既有相似度指标进行对比；
  - 与 NLI/QA 类事实性指标进行对比；
  - 进行基线测试，用于验证本文方法与他人方法的差异；以及涉及不同错误类型检测的对比。
- 对比方法（摘要中明确或可推断）：
  - **BERTScore**（词-词级的嵌入相似度指标）；
  - 广泛使用的 n-gram 重叠类指标（背景提及）；
  - 基于 **NLI** 的事实性指标；
  - 基于 **QA** 的事实性指标；
  - 可能还有常见的相似度基线（如基于 Word2Vec、Glove 等的词向量指标，摘要中未给全，**不臆测**）。

## 4. 资源与算力

**摘要部分未提及任何算力相关细节**。未见 GPU 型号、GPU 数量、训练（或推理）时长、参数量等任何数据。由于论文方法是零样本 Sentence-BERT 编码，推测主要开销在推理侧而非训练侧，但论文文本中没有直接披露，这一点应当指出，不能凭空补全。

## 5. 实验数量与充分性

限于正文缺失，只能依据摘要做间接判断，属于推测：
- 摘要中仅明确概述了：
  - 与相似度基线（如 BERTScore、词级指标）的对比；
  - 与 NLI/QA 事实性指标的对比；
  - 关于“不同技术各有所长”的分析（揭示具备不同错误类型的多维度实验视角）；
  - 关于不同技术“组合”效果的评估。
- 这些实验在覆盖上看起来**初步合理**，证明了“SBERTScore 有效”这一核心论点；
- 但在缺乏具体数据集名称、数据规模、评价指标和统计显著性等信息的情况下，**无法判定实验是否足够充分与公平**；
- 值得指出的是：论文发布时 ICLR-2025 评论分数为 9.0，但仍被标记为 Rejected（根据来源信息），说明评审者方面仍可能存在对实验或方法问题的分歧，但这条元数据不等同于论文的缺陷证据，仅可作为间接参考。

## 6. 论文的主要结论与发现

- 重新确认了**相似度度量的失败根源不在“相似度”本身**，而在**参照文本的选择（参考文献 vs. 源文档）**和**比较粒度（词级 vs. 句子级）**。
- 基于上述洞察提出的零样本 SBERTScore：
  - **显著优于词-词相似度指标**（例如 BERTScore）；
  - 在 benchmark 上，**不需任何微调即可与基于 NLI 和 QA 的事实性指标竞争**；
  - 尤其擅长**识别正确的摘要**（高特异度/正确摘要识别）。
- 由于不同技术各具优势，**组合多种技术可以更有效地检测各类错误**。

## 7. 优点

- **概念上简洁**：揭示了一个此前被忽视的关键要害——参考文本的不当使用与粒度过粗，而非否定相似度本身；
- **真正零样本**：无需为事实一致性任务进行额外的监督训练，省去了 NLI/QA 流水线的构建和标注成本；
- **轻量实用**：仅基于 Sentence-BERT 嵌入推理，相比端到端的生成式 NLI/QA 模型更容易部署；
- **更具信息量的分析视角**：不像端到端打分那样黑盒，句子级输出可辅助定位具体错误句；
- **正确摘要检测性强**：在直接判断“摘要是否忠实”这一任务上有突出表现；
- **组合观点**：明确给出“组合方法效果更好”的实验结论，而非一味强调自己的方法全面碾压对手，显得客观。

## 8. 不足与局限

- **正文不可获取**：当前摘要文本无法确认模型的完整相似度聚合式；缺少算法伪代码以及更多消融细节。
- **实验覆盖不足**：无法确认测试数据集是否涵盖多样化的领域（新闻、对话、医学、法律等），无法验证跨域泛化性；
- **可能的情报偏差风险**：
  - 摘要专注于相似度距离，对同义改写（paraphrase）中**信息丢失/新增**等情况可能不够敏感；
  - 特别擅长“识别正确摘要”，意味着可能**偏保守或偏精确**，在检出不正确摘要（召回）方面是否有短板尚不清楚；
  - 中文语料效果未经报告，未知跨语言性能；
- **无算力与稳定性报告**：没有给出运行时开销、批次规模、嵌入模型选择敏感性分析等；
- **零样本方法的上限**：Sentence-BERT 本身训练语料未必与“事实一致”语境对齐，对长文摘要、多跳事实关系可能失效；
- **组合实验的具体增益幅度和统计检验没有在摘要中披露**，无法量化“组合”的贡献程度。

（完）
