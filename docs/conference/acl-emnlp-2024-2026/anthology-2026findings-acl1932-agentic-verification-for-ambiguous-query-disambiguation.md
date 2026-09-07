---
title: Agentic Verification for Ambiguous Query Disambiguation
title_zh: 面向歧义查询消解的智能体验证方法
authors: "Youngwon Lee, Seung-Won Hwang, Ruofan Wu, Feng Yan, Danmei Xu, Moutasem Akkad, Zhewei Yao, Yuxiong He"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1932.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 通过检索相关性与答案可回答性反馈来验证证据，减少RAG产生的无依据查询与幻觉
tldr: "在RAG中处理歧义查询时，先多样化再验证的流程常生成语料无法回答的无依据查询，并产生级联错误。论文提出VerDICT，将多样化与验证统一起来，及早整合检索器相关性与生成器可回答性反馈。这样既减少无依据问题，又支持并行处理。在ASQA数据集上，它在多个LLM骨干下比最强基线平均提升grounding-aware F1约23%，展示了更强的证据接地能力。"
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1932/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1532, \"height\": 840, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1932/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1636, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1932/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 800, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1932/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1413, \"height\": 994, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 733, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1405, \"height\": 834, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 778, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 778, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 488, \"height\": 164, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 808, \"height\": 119, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 778, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 702, \"height\": 553, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 807, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 646, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1932/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 764, \"height\": 116, \"label\": \"Table\"}]"
motivation: RAG歧义查询消解中，先生成解释再检索容易引入无法由语料回答的无依据查询与级联误差。
method: 提出统一多样化与验证的框架，把检索器相关性和生成器可回答性反馈提前纳入流程。
result: "在ASQA基准上，相比多种强基线将grounding-aware F1平均提升23%。"
conclusion: 通过早期融合可回答性验证，可显著提高RAG对证据的依赖、减少无依据内容。
---

## Abstract
We study ambiguous-query disambiguation in retrieval-augmented generation (RAG). Prior Diversify-then-Verify (DtV) pipelines first generate interpretations and then retrieve evidence, often introducing ungrounded queries that cannot be answered from the corpus and requiring costly post-hoc pruning and verification. We propose VerDICT, a novel approach that unifies diversification with verification by integrating retriever relevance and generator answerability feedback early. This not only reduces cascading errors but also enables parallelism. On ASQA, VerDICT improves grounding-aware F1 by an average of 23% over the strongest baselines across multiple LLM backbones.

---

## 论文详细总结（自动生成）

# 论文详细总结：Agentic Verification for Ambiguous Query Disambiguation

## 1. 核心问题与整体含义

- 研究背景：检索增强生成（RAG）在处理现实中常见的**歧义查询**时，需要先对查询进行消歧，才能检索到有效证据并生成可靠答案。
- 已有范式：**Diversify-then-Verify（DtV，先多样化后验证）** 通常先生成对歧义查询的多种解释或子查询，再检索证据，最后进行验证与筛选。
- 核心问题：这种顺序化方法容易产生**“无依据/不可回答的中间查询”**——即生成出的解释或子问题无法在给定语料库中找到支持证据。这不仅带来昂贵的后处理验证成本，还可能引发**级联误差和幻觉**，损害RAG输出的真实性与可依据性。
- 研究意义：需要一种更高效的机制，在生成多样化假设的同时就融入可验证性约束，从源头减少不可回答的中间查询，提升最终答案的证据接地能力。

## 2. 方法论

- 核心思想：将“多样化”和“验证”从**顺序的两阶段**统一为**一体化流程**，提出的方法名为 **VerDICT**。
- 关键技术：在早期阶段同时整合两类反馈信号：
  - **检索器相关性反馈**：用于评估生成的中间查询是否能检索到足够相关的支持证据；
  - **生成器可回答性反馈**：用于判断检索到的证据能否真正回答当前查询。
- 流程效果：
  - 通过早期反馈及时过滤、修正或淘汰低质量/无依据的查询，从而**减少级联错误**；
  - 由于验证被前移并融入生成过程，避免了事后逐个验证的顺序瓶颈，因此**支持并行处理**，有利于提升效率。
- 需要注意的是：提供的摘要与元数据中没有给出具体的神经网络结构、公式推导或算法伪代码，以上技术描述基于文本信息的概括。

## 3. 实验设计

- 数据集与基准：使用**ASQA**（歧义查询消解基准）进行评测。
- 对比方法：主要是“先多样化后验证”类基线（DtV），以及论文所称的“最强基线”（具体基线名称在摘要中未列出）。
- 评估指标：**grounding-aware F1**，即能够衡量答案是否真正由检索到的证据支撑的F1分数，比普通F1更能反映“有据可依”程度。
- 主干模型：实验在**多个LLM骨干**（multiple LLM backbones）下进行，用以验证方法的泛化性。

## 4. 资源与算力

- 提供的论文文本与元数据中**未明确说明**使用了多少GPU、GPU型号、训练/推理时长等硬件资源信息。
- 无法据此估算复现成本或能耗规模；这是当前信息下的一个明确留白。

## 5. 实验数量与充分性

- 从元数据中的图表编号看，论文包含约 **4 个图和 12 个表**，推测可能覆盖了主要结果（多个LLM骨干上的对比）、消融研究、案例分析以及超参数敏感性等。
- 从摘要可直接观察到的定量结论是：**在ASQA上，相比最强基线平均提升grounding-aware F1约23%**，这一结果在多个LLM骨干上一致。
- 充分性评估：
  - 目前可见的实验仅在 **一个公开基准（ASQA）** 上验证，缺少跨数据集、跨领域、跨语料的泛化证据；
  - 具体对比基线的名单、消融项的设置、统计显著性检验等细节尚无法从摘要中获知，因此难以完全评估实验的公平性和覆盖度。

## 6. 主要结论与发现

- 在多个LLM骨干下，**VerDICT比最强基线平均提升grounding-aware F1约23%**。
- 将“可回答性验证”反馈前移到中间查询的生成过程中，能够显著提高RAG系统输出的**证据接地能力（grounding）**。
- 统一多样化与验证后，减少了由“无法回答的中间查询”导致的幻觉和级联错误，同时允许并行处理，兼顾效果与效率。

## 7. 优点

- **问题切中要害**：不同于传统先扩写再事后验证的做法，VerDICT在生成阶段就嵌入验证信号，从源头上降低无依据查询的出现概率。
- **流程简化与错误抑制**：将多样化与验证统一，减少了“先污染再治理”的级联风险。
- **支持并行化**：由于验证被整合进早期判断，避免了串行后处理瓶颈，具有一定工程实用性。
- **多骨干验证**：在多种LLM骨干上报告一致提升，增强结论的稳定性。
- **指标合理**：使用grounding-aware F1，比普通精确匹配或F1更贴近事实性与可验证性的核心诉求。

## 8. 不足与局限

- **资源与算力信息缺失**：文本中没有报告训练/推理的硬件配置与时间成本，不便于复现或部署评估。
- **数据集范围单一**：仅见ASQA一个基准，未覆盖其他歧义问答、多跳推理或不同领域/语料库的RAG场景，泛化性证据不足。
- **基线不透明**：摘要只笼统称“最强基线”，未给出具体方法，比较设置和实现细节未知。
- **方法细节欠缺**：没有给出检索器/生成器反馈的具体融合策略、损失设计或迭代终止条件，技术可复现性受限。
- **敏感性分析未知**：例如对“相关性判断”和“可回答性判断”质量的好坏如何影响最终性能，未见相应讨论。
- **潜在偏差风险**：可能过于依赖LLM的自我验证能力；真实场景中的歧义查询与基准分布可能不同，agentic交互带来的额外延迟和查询成本也未量化。

（完）
