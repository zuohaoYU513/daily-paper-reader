---
title: "SeCon-RAG: A Two-Stage Semantic  Filtering and Conflict-Free Framework for Trustworthy RAG"
title_zh: SeCon-RAG：面向可信检索增强生成的两阶段语义过滤与无冲突框架
authors: "Xiaonan si, Meilin Zhu, Simeng Qin, Lijia Yu, Lijun Zhang, Shuaitong Liu, Xinfeng Li, Ranjie Duan, Yang Liu, Xiaojun Jia"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=tTwZhy8JqY"
tags: ["query:hallu-rag"]
score: 6.0
evidence: 面向可信RAG的两阶段语义过滤与无冲突方法，降低污染和冲突证据对生成的影响。
tldr: 针对RAG系统易受语料投毒和污染攻击、同时过滤过强会丢失有用信息的问题，提出SeCon-RAG两阶段语义过滤与无冲突框架。第一阶段利用实体-意图-关系抽取器引导语义与聚类联合过滤，保留关键信息并剔除有害内容，后续阶段确保生成不依赖冲突证据。该方法在提升对抗鲁棒性的同时减少信息损失，为可信RAG提供了一种平衡安全性与相关性的方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: RAG易受语料投毒和污染攻击威胁，现有防御过度过滤导致有价值信息损失和可靠性下降。
method: 提出两阶段语义过滤与无冲突框架，先用实体-意图-关系抽取器联合语义和聚类过滤，再在生成阶段排除冲突证据。
result: 在增强对抗鲁棒性的同时减少信息丢失，提升生成输出的整体可靠性。
conclusion: 为可信检索增强生成提供兼顾攻击防御与信息保留的通用过滤方案。
---

## Abstract
Retrieval-augmented generation (RAG) systems enhance large language models (LLMs) with external knowledge but are vulnerable to corpus poisoning and contamination attacks, which can compromise output integrity. Existing defenses often apply aggressive filtering, leading to unnecessary loss of valuable information and reduced reliability in generation.
To address this problem, we propose a two-stage semantic filtering and conflict-free framework for trustworthy RAG. 
In the first stage, we perform a joint filter with semantic and cluster-based filtering  which is guided by the Entity-intent-relation extractor (EIRE). EIRE extracts entities, latent objectives, and entity relations from both the user query and filtered documents, scores their semantic relevance, and selectively adds valuable documents into the clean retrieval database. 
In the second stage, we proposed an EIRE-guided conflict-aware filtering module, which analyzes semantic consistency between the query, candidate answers, and retrieved knowledge before final answer generation, filtering out internal and external contradictions that could mislead the model.
Through this two-stage process, SeCon-RAG effectively preserves useful knowledge while mitigating conflict contamination, achieving significant improvements in both generation robustness and output trustworthiness.
Extensive experiments across various LLMs and datasets demonstrate that the proposed SeCon-RAG markedly outperforms state-of-the-art defense methods.

---

## 论文详细总结（自动生成）

# SeCon-RAG：面向可信RAG的两阶段语义过滤与无冲突框架——中文总结

> ⚠️ **重要说明**：本次所获取的“论文 PDF 提取文本”实为 OpenReview 的浏览器验证（CAPTCHA）拦截页面，仅包含论文标题、元数据与摘要（Abstract）文字，不包含论文正文、实验章节、公式及参考文献等完整内容。因此，以下总结中凡涉及论文正文方法论细节、实验设置、算力资源配置等信息，均以“原文未提供”进行明确标注，不做虚构性推测。

## 1. 论文的核心问题与整体含义

- **背景（研究动机）**：检索增强生成（RAG）系统通过引入外部知识来增强大语言模型（LLM）的能力，但同时也面临**语料投毒（corpus poisoning）与污染攻击（contamination attacks）** 的威胁，这类攻击可能损害模型输出的完整性与可信度。
- **现存主要问题**：已有防御手段往往采用**过度激进的过滤（aggressive filtering）** 策略，这虽然能够剔除有害内容，但同时也造成**有价值信息的丢失**，进而削弱生成结果的可靠性。
- **整体研究目标**：提出一套能够**同时兼顾“过滤有害/冲突内容”与“保留有用知识”** 的信任RAG方案，在提升对抗鲁棒性的同时，不牺牲生成质量。
- **核心定位**：发表于 NeurIPS-2025（Accepted）的方法类论文，题目为“SeCon-RAG: A Two-Stage Semantic Filtering and Conflict-Free Framework for Trustworthy RAG”。

## 2. 论文提出的方法论

根据摘要内容，方法论的整体框架可归纳为**“两阶段语义过滤与无冲突框架（SeCon-RAG）”**，其核心思想与技术要点如下：

- **核心思路**：将防御从“一刀切式强过滤”调整为**“细粒度语义筛选 + 冲突剔除”**，在保证对抗安全性的前提下最大化信息保留。
- **第一阶段：语义-聚类联合过滤（Semantic and Cluster-based Joint Filter）**
  - 引入 **Entity-intent-relation extractor（EIRE）** 组件，即“实体-意图-关系抽取器”。
  - EIRE 依次从**用户查询（user query）** 和**候选文档（filtered documents）** 中抽取三类语义要素：
    - **实体（entities）**；
    - **隐含目标 / 潜在意图（latent objectives / intentions）**；
    - **实体间关系（entity relations）**。
  - 基于抽取结果计算语义相关性得分，以引导过滤过程，实现**同时进行语义过滤（semantic filtering）与基于聚类的过滤（cluster-based filtering）**。
  - 过滤后的高质量文档会被**选择性地添加回“干净检索库”（clean retrieval database）**，以弥补传统激进过滤带来的信息损失。
- **第二阶段：EIRE 引导的冲突感知过滤模块（EIRE-guided Conflict-aware Filtering Module）**
  - 在**最终答案生成前**，对以下三者做**语义一致性分析（semantic consistency）** ：
    - 查询（query）；
    - 候选答案（candidate answers）；
    - 检索到的知识/证据（retrieved knowledge）。
  - 过滤掉**内部矛盾与外部矛盾（internal and external contradictions）**，防止误导模型的信息进入最终生成环节。
- **效果机制**：两阶段处理使得 SeCon-RAG 能够有效避免因冲突证据（conflict contamination）导致的输出错误，同时通过选择性回填机制保留有用知识。
- **原文公式与算法流程**：鉴于仅获得摘要信息，论文正文中是否给出目标函数、算法伪代码等细节，**原文未提供，无法说明**。

## 3. 实验设计

- **使用的数据集/场景**：摘要中仅提到“across various LLMs and datasets”（跨越多种大语言模型与数据集），具体数据集名称（如自然问答类、事实验证类等）**原文未提供**。
- **Benchmark**：采用的基准测试集与评价指标体系**原文未提供**。
- **对比方法**：摘要仅提及“与最先进的防御方法相比（outperforms state-of-the-art defense methods）”，具体对比基线方法名称（如诚实RAG、对抗训练、提示扰动防御等）**原文未提供**。
- **测评的模型**：未列出具体的 LLM 类别（如 Llama、GPT、Qwen 等）与模型规模。

## 4. 资源与算力

- 鉴于本次获得的文本仅为 OpenReview 验证拦截页面与摘要字段，关于：
  - GPU 型号（如 A100/H100）；
  - GPU 数量；
  - 训练时长 / 推理开销；
  - 参数量级；
  - 微调策略与计算成本等与算力相关的所有信息，**原文未提供，无法总结**。

## 5. 实验数量与充分性

- **已知声称**：摘要明确说“Extensive experiments across various LLMs and datasets”表明进行了**跨多种模型、多种数据集的充分实验**，且取得了显著的性能提升。
- 然而，由于未获取完整正文：
  - **具体实验组数**（在多少个数据集上有多少组对比）——无法核实；
  - **是否包含消融实验**（如 EIRE 组件有效性、两阶段各自贡献等）——无法确认；
  - **统计显著性检验、误差线设置、多次运行均值方差报告** —无法确认；
  - **公平性**（如基线是否调整到最优、计算预算是否对齐）——无法评估。
- 因此实验数量与充分性的判断，**需要以论文正式发表版中实验章节为准**，本总结无法擅自给出验证性结论。

## 6. 论文的主要结论与发现

- SeCon-RAG 在**多种大语言模型与数据集**上显著优于现有的 SOTA 防御方法。
- **两阶段过滤机制**能够在增强模型对抗鲁棒性（鲁棒性提升）的同时保留更多有价值信息（信息损失降低），最终提升生成输出的整体可信度（trustworthiness）。
- 这表明“语义层级筛选 + 冲突检测”比“广谱强过滤”更有优势，为可信 RAG 提供了一个更平衡安全性、有用性之间矛盾的通用方案。

## 7. 优点

以下是基于可获取的摘要与论文题目，可以合理归纳的亮点：

- **问题定位贴心**：指出“防御过滤过度”造成的副作用，所提出的方法切中了安全防御与信息可用性之间的权衡痛点。
- **“过滤后回填”的机制设计巧妙**：通过选择性将高价值文档加入干净检索库，避免传统过滤的不可逆信息损失。
- **两阶段并行防御思路**：第一阶段管“文档级污染”，第二阶段管“答案级矛盾”，覆盖了从检索到生成的完整链路，防御逻辑严密。
- **EIRE 抽取器设计具备一定新意**：将查询和文档统一映射到实体-意图-关系维度进行语义比对，既有信息粒度又有语义深度。
- **适用性广**：实验跨不同 LLM 与数据集，方法被设计为通用型过滤框架，不依赖于某一特定底座模型。

## 8. 不足与局限

- **本次获取信息严重不完整**：
  - 论文 PDF 实际上并未被成功获取，有效文本仅包含标题与摘要。
  - 因此无法验证其完整方法表述是否足够清晰、伪代码或算法流程是否完整。
  - 无法判断实验是否包含消融、鲁棒性边界测试、失败案例分析等。
- **已知潜在局限（基于摘要推测）**：
  - 两阶段流程引入了额外的语义抽取与一致性分析模块，**可能带来额外计算延迟**与推理成本，摘要中未见效率对比数据（原文未提供）；
  - 方案高度依赖“实体-意图-关系”的抽取质量，若查询本身模糊或文档语义复杂，EIRE 组件的误差可能逐级放大（需看原文是否有讨论）；
  - 摘要只谈及“过滤”与“冲突检测”，对**后门攻击、越狱类攻击**是否有效不明；
  - 是否覆盖多跳检索知识或长文档检测未见具体说明。
- **开放性风险**：综述性评估其“公平性”（即 SOTA 基线是否充分调整）无法完成，因为正文实验细节未在本次提取内容中出现。

## 简要总结（一页速览）

| 维度 | 要点 |
|---|---|
| 论文定位 | NeurIPS-2025：可信 RAG 的对抗防御方法 |
| 核心问题 | 防御投毒攻击时，过度过滤造成信息丢失 |
| 方法 | 两阶段：EIRE引导的语义+聚类联合过滤 → 冲突感知一致性过滤 |
| 最大特色 | 从“粗暴删”变成“聪明留”，过滤后选择性回填 |
| 实验结论声明 | 多种LLM/数据集下优于 SOTA 防御方法（摘要声称） |
| 本次评估限制 | 仅有摘要，完整方法、实验、效率等信息缺失 |
| 主要不足 | 框架复杂度可能高、换发额外推理开销，尚未见到证据（待原文证实） |

（完）
