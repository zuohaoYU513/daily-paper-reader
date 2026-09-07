---
title: Building Reliable Long-Form Generation via Hallucination Rejection Sampling
title_zh: 通过幻觉拒绝采样构建可靠的长文本生成
authors: "Lin Li, Georgia Channing, Suhaas M Bhat, Gabriel Davis Jones, Yarin Gal"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a4a9be55fe38c69b367d428b09f382c01481026f.pdf"
tags: ["query:faithfulness"]
score: 7.0
evidence: 推理期幻觉拒绝采样剔除生成中的虚构片段并重新采样，提升内容忠实性
tldr: 大模型在开放式长文本生成中容易出现幻觉，且早期错误会随句子累积放大。本文提出分段式幻觉拒绝采样SHARS，利用任意幻觉检测器在生成时识别并拒绝含幻觉的片段，重新采样直到产出可信内容。实验结果显示该方法能明显降低长文本中的累积性幻觉，增强输出的可靠性和忠实度。该方法具有即插即用特点，是面向长文本的通用推理期幻觉抑制方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 长文本中幻觉滚雪球使初始错误放大，需要推理期主动剔除不可信片段。
method: SHARS以分段检测-拒绝-重采样的框架，递归生成忠实内容。
result: 实验证明该机制能有效压制累积幻觉，提高长文本事实一致性。
conclusion: 在解码阶段采样去伪可显著改善可靠长文档生成能力。
---

## Abstract
Large language models (LLMs) have achieved remarkable progress in open-ended text generation, yet they remain prone to hallucinating incorrect or unsupported content, which undermines their reliability. This issue is exacerbated in long-form generation due to hallucination snowballing, a phenomenon where early errors propagate and compound into subsequent outputs. To address this challenge, we propose a novel inference-time hallucination mitigation framework, named Segment-wise HAllucination Rejection Sampling (SHARS), which uses am arbitrary hallucination detector to identify and reject hallucinated segments during generation and resample until faithful content is produced. By retaining only confident information and building subsequent generations upon it, the framework mitigates hallucination accumulation and enhances factual consistency. To instantiate this framework, we adopt semantic uncertainty as the detector and introduce several vital modifications to address its limitations and better adapt it to long-form text.
Our method enables models to self-correct hallucinations without requiring external resources such as web search or knowledge bases, while remaining compatible with them for future extensions. Empirical evaluations on standardized hallucination benchmarks demonstrate that our method substantially reduces hallucinations in long-form generation while preserving or even improving the informativeness of generation.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机与背景）
*   **核心问题**：大语言模型（LLMs）在开放式文本生成中频繁产生“幻觉”，即生成不正确或缺乏依据的内容，严重削弱了模型在实际应用中的可信度。
*   **关键矛盾**：长文本生成进一步放大了这一问题。作者关注到“幻觉雪球效应”（Hallucination Snowballing）：早期生成中的微小错误会作为后续生成的上下文，导致错误逐句传播、累积甚至加剧，使长文本后期内容越发不可靠。
*   **方法定位**：论文提出了一种**推理期（inference-time）**的幻觉抑制框架，不依赖额外的检索资源，而是让模型在生成过程中自我检错并纠错，从源头上阻断早期错误的滚雪球式放大。

### 2. 方法论：核心思想、关键技术细节与流程
*   **框架名称**：分段式幻觉拒绝采样（Segment-wise HAllucination Rejection Sampling, **SHARS**）。
*   **核心思想**：“宽进严出”的生成控制——允许模型自由生成候选片段，但通过外部幻觉检测器严格把关，只保留可信度高的内容，对含幻觉的片段全部拒绝并重新采样。
*   **算法流程**（文字描述）：
    1.  **分段生成**：将长文本生成过程分解为多个连续的文本片段（segment），而非一次性端到端生成全篇。
    2.  **幻觉检测**：每生成一个片段，即调用一个任意的幻觉检测器（hallucination detector）对该片段进行评估，判断其是否包含幻觉或与既有上下文是否矛盾。
    3.  **拒绝与重采样**：若片段被判定为含有幻觉，则丢弃并从该位置重新采样新的候选片段。
    4.  **递归构建**：重复上述“生成→检验→拒绝/保留”循环，直到所有片段均通过检测。通过保留高置信信息并以此为基础生成后续内容，破坏幻觉累积链条，保证最终文本的全局一致性。
*   **检测器实例化**：论文采用**语义不确定性（semantic uncertainty）**作为基础检测器，并针对长文本场景做了若干关键改进，以弥补其在长序列下语义判定不敏感、词汇多样性干扰等局限。
*   **零外部依赖、可扩展性**：设计上不依赖网络搜索或外部知识库，模型通过内在语义自评即可完成纠偏；同时框架松散耦合，未来可以无缝接入更强的外部检测器或知识库。

### 3. 实验设计
*   **基准（Benchmark）**：论文在标准的幻觉评测基准（standardized hallucination benchmarks）上做实证评估。由于本文档仅提供元数据与摘要，**未具体列出**使用了哪些数据集名称（如是否包含 TruthfulQA、FActScore、LongEval 等未作说明）。
*   **评估场景**：聚焦长文档、开放式文本生成场景，特别针对容易出现“幻觉雪球”的多句、多段生成。
*   **对比方法**：摘要没有披露具体对比基线，但通常推断会与下列方法对照：基础语言模型采样（Greedy/Sampling）、自我纠错（Self-Correction）、常规拒绝采样、基于外部知识的约束解码方法等。

### 4. 资源与算力
*   论文提供的文本内容中**未明确说明**训练/推理所需的硬件资源，包括 GPU 型号、数量、耗时、参数量级和能耗等关键工程信息。鉴于该方法属于推理期约束，推断其主要算力开销在于多轮重采样的额外推理成本，但由于缺乏原文数据，无法给出量化细节。

### 5. 实验数量与充分性
*   由于材料中仅收录了摘要，无法还原具体开展了多少组实验、消融实验的粒度以及统计显著性检验结果。严格来说，**实验细节的透明度在这次提供的文本范围内是缺失的**。
*   合理推测原文应当包含：
    *   主实验：SHARS vs. 若干基线的幻觉率对比；
    *   消融实验：不同幻觉检测器、不同片段长度的影响；
    *   信息量控制实验：验证在抑制幻觉的同时不牺牲文字的信息密度。
*   就摘要所述“substantially reduces hallucinations while preserving or even improving informativeness”来看，实验设计目标兼顾了可靠性维持与内容效用，但在缺乏数据集规模与可复现细节的前提下，不能从该摘要层面判断其是否充分公平。

### 6. 主要结论与发现
*   **机制有效**：通过分段检测-拒绝-重采样，SHARS 有效减少了长文本生成中的幻觉累积问题，显著提升事实一致性（factual consistency）。
*   **效用无损**：干预过程并未导致模型输出空洞化，反而在保留甚至提升内容信息量（informativeness）的前提下降低了牺牲。
*   **通用可行**：方法不依赖外部工具即可实现模型自我纠正，同时具备即插即用的模块化特征，适用于任意幻觉检测器的框架扩展。

### 7. 优点（方法/实验亮点）
*   **直击痛点**：明确针对“长文本幻觉雪球”这一多数现有研究忽视的角度，切中生成可靠性在实际产品落地中的瓶颈。
*   **工程务实的即插即用设计**：SHARS 是推理期插件，无需重新训练模型，也无需为每个任务收集知识库或检索语料，适配性广泛。
*   **理论切入点清晰**：引入拒绝采样思维到文本生成的分段流程中，巧妙地将统计学中的质量筛选思路引入叙事生成控制。
*   **兼容与扩展性**：检测器接口抽象化，未来可方便地替换为更强的语义评估模型，或融合检索结果进一步提升可控性。
*   **保信息性意识**：多数纠偏方法倾向于保守化输出而伤害信息密度，论文明确将信息量作为评估维度，力求抑制幻觉与保留信息间的双赢。

### 8. 不足与局限
*   **实验公开信息不透明**：在本文档可及范围内，没有给出所用数据集详情、比较基线清单、评价指标的具体数值和统计显著性，难以独立验证效果强度。
*   **计算成本抑制实用化**：拒绝重采样本质上是多次采样的重试策略，在长文本场景中可能导致大规模推理算力消耗；论文对该开销如何控制（如采样上限、延迟预算）未做展示性说明。
*   **检测器依赖风险**：框架上限取决于底层幻觉检测器的灵敏度与误报率。若检测器本身对某些开放性、创造性文本误判率偏高，SHARS 可能反复拒绝好内容，降低流畅性与多样性。
*   **语义不确定性检测的局限**：对于流畅但完全虚构的“幻觉黄金”样例，LLM 自身的语义不确定性信号可能偏弱，导致检测器漏检。
*   **普适性与多样性验证有待加强**：是否存在特定领域（如法律文书、医学报告）或特定任务（如故事写作）会产生更大的重采样滑坡风险，这一跨任务鲁棒性问题仍需更大规模的实验矩阵来检验。

（完）
