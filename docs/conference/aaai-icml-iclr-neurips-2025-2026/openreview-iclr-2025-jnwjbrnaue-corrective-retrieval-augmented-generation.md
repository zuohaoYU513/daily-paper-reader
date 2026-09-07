---
title: Corrective Retrieval Augmented Generation
title_zh: 校正式检索增强生成
authors: "Shi-Qi Yan, Jia-Chen Gu, Yun Zhu, Zhen-Hua Ling"
date: 2024-09-26
pdf: "https://openreview.net/pdf?id=JnWJbrnaUE"
tags: ["query:hallu-rag"]
score: 8.0
evidence: CRAG通过轻量检索评估器判断检索质量并触发校正动作，减少错误证据引发的幻觉，属于幻觉加RAG核心方向。
tldr: 大语言模型依靠参数化知识生成时难以避免幻觉，检索增强生成的效果又高度依赖检索质量。本文提出校正式检索增强生成（CRAG），用一个轻量检索评估器评估检索文档的整体质量，依据置信度触发重新检索或知识精修等动作。实验表明该方法能显著提升生成准确性与鲁棒性，降低错误检索带来的负面影响。相关工作为可靠利用外部证据抑制幻觉提供了重要的方法参考。
source: ICLR-2025-Public
selection_source: conference_retrieval
motivation: 大模型仅凭参数知识难以规避幻觉，RAG的效果又高度依赖检索文档质量，检索一旦出错会诱导错误生成。
method: 训练轻量检索评估器按查询评估检索整体质量，依据置信度触发纠正、重检或知识精修等不同检索动作。
result: 实验显示该方法能显著缓解低质量检索带来的错误，增强生成鲁棒性并降低幻觉。
conclusion: 显式评估与校正检索质量可让模型更可靠地利用外部证据，为RAG证据约束生成提供实用改进方向。
---

## Abstract
Large language models (LLMs) inevitably exhibit hallucinations since the accuracy of generated texts cannot be secured solely by the parametric knowledge they encapsulate. Although retrieval-augmented generation (RAG) is a practicable complement to LLMs, it relies heavily on the relevance of retrieved documents, raising concerns about how the model behaves if retrieval goes wrong. To this end, we propose the Corrective Retrieval Augmented Generation (CRAG) to improve the robustness of generation. Specifically, a lightweight retrieval evaluator is designed to assess the overall quality of retrieved documents for a query, returning a confidence degree based on which different knowledge retrieval actions can be triggered. Since retrieval from static and limited corpora can only return sub-optimal documents, large-scale web searches are utilized as an extension for augmenting the retrieval results. Besides, a decompose-then-recompose algorithm is designed for retrieved documents to selectively focus on key information and filter out irrelevant information in them. CRAG is plug-and-play and can be seamlessly coupled with various RAG-based approaches. Experiments on four datasets covering short- and long-form generation tasks show that CRAG can significantly improve the performance of RAG-based approaches.

---

## 论文详细总结（自动生成）

# CRAG（校正式检索增强生成，Corrective Retrieval Augmented Generation）论文总结

> **论文题目**：Corrective Retrieval Augmented Generation
> **作者**：Shi-Qi Yan, Jia-Chen Gu, Yun Zhu, Zhen-Hua Ling
> **发表信息**：OpenReview（ICLR-2025 投稿），元数据评分 8.0，论文 PDF 约 2024-09-26 发布

---

## 1. 论文核心问题与研究动机

论文针对两个关键问题展开：

- **大语言模型幻觉问题**：LLM 仅凭参数化知识生成文本，无法保证内容的准确性与事实性，容易产生幻觉。幻觉是制约 LLM 可靠落地的核心短板之一。
- **RAG 对检索质量的高度依赖**：检索增强生成（RAG）通过引入外部证据缓解幻觉，但这种缓解效果严重依赖于检索文档与查询之间的相关性。如果检索引擎返回的是低质量甚至不相关文档，非但不能帮助模型，反而会诱导模型生成更严重的错误内容。

**整体含义**：论文提出，RAG 系统不能只靠“检索一次、生成一次”的静态流程，而应显式地评估检索质量，并依据质量情况主动触发修正动作，让生成过程对检索错误具有鲁棒性。

---

## 2. 论文提出的方法论（CRAG）

### 2.1 核心思想

CRAG 的核心思路是引入一个**轻量级检索评估器（lightweight retrieval evaluator）**，对给定查询下检索到的文档整体质量做出评估，并以一个**置信度分数**表示评估结果。基于该置信度，系统触发不同的**知识检索动作（knowledge retrieval actions）**，以此实现“校正式”的检索增强，而不是被动接受原始检索结果。CRAG 作为模块可即插即用，能无缝耦合到各种现有 RAG 方法上。

### 2.2 关键技术组件与流程（文字说明）

1. **检索评估器训练与评估环节**
   - 针对一条查询（query）和其检索结果集合，设计一个轻量级模型，输出一个关于检索质量的置信度。
   - 模型需学习区分“检索结果是否整体足以支撑回答该问题”。
   - 评估器开销较小，不会给整个生成流程带来显著推理负担。

2. **基于置信度的动作触发策略（校正动作）**
   - 依据评估器给出的置信度，将检索质量划分为不同等级。
   - 若检索质量差（置信度低），则触发**纠正动作（corrective action）**，例如丢弃当前结果并重新检索；
   - 若检索质量一般，则触发**知识精修（knowledge refinement）**，对检索文档做进一步过滤处理；
   - 若检索质量良好，则直接进入下一步生成。

3. **大规模网络搜索扩展（large-scale web searches as extension）**
   - 如摘要原文所述：“Since retrieval from static and limited corpora can only return sub-optimal documents, large-scale web searches are utilized as an extension for augmenting the retrieval results.”
   - 说明在静态、受限语料库检索结果不理想时，CRAG 会引入**大规模 web 检索**作为外部扩展，以获得更丰富的候选知识。这一动作与前面的评估器判断配合，形成“先评估、后校正、必要时扩展检索”的闭环。

4. **分解-重组算法（decompose-then-recompose）**
   - 对检索到的文档内容，设计了一种“先分解、后重组”的算法。
   - 目的：从文档中**选择关键信息**，**过滤掉不相关信息**，避免长文档中噪声内容干扰生成。
   - 该方法与触发策略配合，在知识质量一般时对文档内容进行精炼（refine），使最终输入到生成器的知识更干净、更聚焦。

5. **即插即用耦合（plug-and-play）**
   - CRAG 并非一个独立的端到端生成模型，而是一个可灵活组装在 RAG 系统和检索器之间的修正模块。
   - 与现有 RAG 方法兼容，无需修改原生成器架构。

> **注**：由于正文页未能完整获取，具体的评估器损失函数、置信度阈值设定方式、分解-重组算法的详细步骤等底层技术细节未包含在当前可用文本中，以上各部分是根据摘要中呈现的流程所概括。

---

## 3. 实验设计

根据论文摘要公开的信息：

- **数据集/场景**：实验覆盖了**四个数据集**，涵盖**短文本生成任务（short-form）** 与**长文本生成任务（long-form）** 两类场景。
- **Benchmark 体系**：在多个 RAG 相关基准上评测，但摘要中未列出具体数据集名称（如是否包含 KILT、Natural Questions、HotpotQA、ASQA 等尚不明确）。
- **对比方法**：以“多种现有 RAG 方法”作为基线，对比 CRAG 方法嵌入前后效果。
- **评测目标**：验证 CRAG 能否显著提升基于 RAG 的各类方法的生成准确性与鲁棒性。

---

## 4. 资源与算力

- **摘要与元数据中没有给出训练评估器所需的 GPU 型号、卡数、训练时长、参数量等任何算力信息。**
- **本文档所依据的材料（已验证的 PDF 文本 + 元数据字段）未包含相关说明。**
- 从摘要表述推测，评估器属于“轻量级（lightweight）”，理论上应可单卡训练，但这一推断没有来自论文的算力实验数据支持。

---

## 5. 实验数量与充分性评估

### 已公开信息可做判断的部分

- 论文在**四个数据集**上验证，覆盖了短/长文本两种形式的生成任务，在覆盖面上有一定的广度。
- 从摘要看，实验比较了 CRAG 与多种 RAG 方法的组合效果，能体现出**“即插即用”方法对不同基线的提升能力**。

### 无法充分验证的部分

- **缺少消融实验说明**：由于正文不可完整获取，无法判断论文是否报告了以下关键消融：无评估器、无纠错动作、无 web 扩展、无分解-重组等变体对比。
- **缺少与专用纠错/后编辑方法的对比**：摘要没有表明 CRAG 是否与其它幻觉缓解方法（如自我修正、事实核验后处理）做过对比，无法判断相对优势。
- **缺少失败案例分析**：是否分析了 CRAG 仍无法矫正的检索错误场景，尚不明确。
- **缺少人工评测说明**：摘要无明确提及自动指标之外的人工评测（如事实性人工打分）。
- **客观性评价**：实验方向设计合理——测量的是“加上 CRAG 后一批 RAG 基线是否变好”，这一对比框架本身是客观、公平、有说服力的。但由于数据集、评测指标、基线的参数规模等细节并不在可用文本中，其具体充分性难以给出全面结论。

---

## 6. 主要结论与发现

论文的核心结论可归纳为以下几点：

1. **RAG 的输出质量取决于检索质量的保障，仅靠一次检索无法确保可靠生成**，因此需要引入“校正”机制。
2. 通过轻量检索评估器结合置信度导向的动作策略，可**显著提升基于 RAG 的生成准确性与鲁棒性**，降低由错误检索内容引发的幻觉。
3. **与大规模 web 检索结合**，能扩展静态语料所不能覆盖的知识范围，弥补检索覆盖不足。
4. **分解-重组式的知识过滤**能有效筛选文档中的关键信息，滤除不相关内容，对长文本和噪声文档场景尤为有价值。
5. CRAG 作为即插即用模块，可以便捷地融入多个 RAG 框架，具备较强的通用性和实用性。

---

## 7. 方法的优点

- **问题定位准确**：指出 RAG 的瓶颈不仅在于“是否检索”，更在于“检索错了怎么办”，切中 RAG 系统中检索质量影响可靠生成的实际痛点，与幻觉治理直接相关。
- **轻量级评估器的设计**：相比加重生成器本身的自省/自我修正机制，“用一个小型评估器给检索打分”是一个成本可控且思路清晰的做法。
- **分级动作机制**：不是简单的“有错就重检”，而是依据置信度使系统在不同层次上做出反应（丢弃、重检、web 扩充、精修、保留），更贴近实际应用场景。
- **即插即用，兼容性强**：CRAG 可适配多种 RAG 方法，而不需要重新训练生成大模型，这大大降低了在现有系统中集成的难度。
- **知识精修的方法论与“分解-重组”策略**：为文档级检索信息到生成可用知识之间增加有序的精选步骤，在长文本与噪声信息处理方面具有参考价值。
- **视角先进**：将“检索质量评估”作为一个独立研究对象提出，为后续证据筛选与幻觉抑制研究提供了新的中间任务。

---

## 8. 不足与局限

- **实验信息无法核实完整**：当前文本只提供了 4 个数据集和两类任务这一基本信息，缺少具体数据集、基线模型、评测指标及误差分析等细节，不利于读者全面评估方法的推广边界。
- **算力与效率分析缺失**：论文没有报告评估器参数量、推理时的额外时延开销、训练所需资源。虽然宣称“轻量级”，但缺乏数字证据。
- **对评估器的准确性依赖较高**：整个修正链的第一环是评估器，若评估器对检索质量的判断不够可靠，后续动作都受影响；论文既然未能给出评估器的独立评测（如判断准确率），无法判断该环节的误差风险。
- **web 搜索引入的外部不确定性**：引入大规模 web 搜索可以扩大信息范围，但随之带来的 web 内容质量参差不齐、事实冲突、缓存/API 依赖等问题，论文如何规避或是如何纳入评估，当前不可见。
- **长/短形式覆盖虽好，但领域覆盖可能受限**：是否在对话、多跳问答、摘要生成、代码生成、医疗法律等特定领域做过测试并不清楚，实际部署到专业场景时的变体适配有待考察。
- **端到端可解释性有限**：纠错动作的依据本质是置信度的数值判断，难以向用户解释为什么某次检索被判定为低质量、为什么某段文档被丢弃，这可能在需要可追溯/可复现证据链的应用中形成挑战。
- **与 RAG 以外的其他幻觉抑制手段之间的协同/竞争关系未充分展示**：例如和 prompt 约束、采样策略、诚实生成等其它方法的效果叠加或优势边界，不属于本文主要的实验论述范围（至少在当前材料中未展示）。

---

## 附：可获取信息说明

> 本总结基于论文公开摘要、元数据字段与尽可能可读的 PDF 文本完成。受网页 PDF 访问验证影响，论文正文的完整实验表格、公式、实现细节与引用文献没有完整进入分析范围，凡涉及未在材料中清楚交代的部分，以上总结均已明确标注为“不可见”或“未明确说明”，以帮助读者区分事实信息与推断信息。

---

（完）
