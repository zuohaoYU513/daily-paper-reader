---
title: "CofCA: A STEP-WISE Counterfactual Multi-hop QA benchmark"
title_zh: CofCA：一个逐步反事实多跳问答基准
authors: "Jian Wu, Linyi Yang, Zhen Wang, Manabu Okumura, Yue Zhang"
date: 2025-01-22
pdf: "https://openreview.net/pdf?id=q2DmkZ1wVe"
tags: ["query:faithfulness"]
score: 6.0
evidence: 通过逐步反事实改写检查模型是否依赖内部记忆而非给定证据，服务证据一致性评测。
tldr: 在复杂多跳问答中，LLM常依靠内部记忆而非检索到的证据作答，而现有反事实基准仅看最终答案，无法暴露推理过程中的证据依赖问题。论文提出CofCA逐步反事实基准，在子问题层面对上下文进行反事实改写，引导模型展示每一步的证据检索和推理。该基准可更准确地区分模型是否真正使用给定材料，为评估与引导忠实推理提供检测手段。
source: ICLR-2025-Accepted
selection_source: conference_retrieval
motivation: 多跳问答中LLM可能靠内部记忆作答，已有反事实基准只看最终答案，无法评估推理过程中的证据使用。
method: 构建CofCA基准，在子问题层面进行反事实替换，引导模型一步步显示证据检索与推理过程。
result: 能够更细粒度地区分基于内部记忆与基于证据推理的表现，暴露模型真实推理能力。
conclusion: 为多跳证据问答中的忠实性评估提供了逐步、细粒度的评测工具。
---

## Abstract
While Large Language Models (LLMs) excel in question-answering (QA) tasks, their real reasoning abilities on multiple evidence retrieval and integration on Multi-hop QA tasks remain less explored. Firstly, LLMs sometimes generate answers that rely on internal memory rather than retrieving evidence and reasoning in the given context, which brings concerns about the evaluation quality of real reasoning abilities. Although previous counterfactual QA benchmarks can separate the internal memory of LLMs, they focus solely on final QA performance, which is insufficient for reporting LLMs' real reasoning abilities. Because LLMs are expected to engage in intricate reasoning processes that involve evidence retrieval and answering a series of sub-questions from given passages. Moreover, current factual Multi-hop QA (MHQA) benchmarks are annotated on open-source corpora such as Wikipedia, although useful for multi-step reasoning evaluation, they show limitations due to the potential data contamination in LLMs' pre-training stage. To address these issues, we introduce the Step-wise and Counterfactual benchmark (CofCA), a novel evaluation benchmark consisting of factual data and counterfactual data that reveals LLMs' real reasoning abilities on multi-step reasoning and reasoning chain evaluation. Our experimental results reveal a significant performance gap of several LLMs between Wikipedia-based factual data and counterfactual data, deeming data contamination issues in existing benchmarks. Moreover, we observe that LLMs usually bypass the correct reasoning chain, showing an inflated multi-step reasoning performance. We believe that our CofCA benchmark will enhance and facilitate the evaluations of trustworthy LLMs.

---

## 论文详细总结（自动生成）

> 说明：本次抓取到的实际内容为 OpenReview 的访问验证页，而非论文全文；以下内容主要基于所附的论文元数据与摘要文字进行总结，因此部分实验细节、具体数值和算法流程无法完整还原，已在相应位置注明。

## 1. 核心问题与研究动机

- 大语言模型（LLM）在多跳问答（Multi-hop QA）任务上表现出色，但其“真正”的多证据检索与推理能力仍缺乏可靠评测。
- 已有工作发现：LLM 有时依赖内部记忆或预训练知识作答，而非真正依据给定上下文中的证据进行逐步推理，这会夸大模型的实际推理水平。
- 已有反事实问答基准虽然能在一定程度上区分“记忆”与“推理”，但它们大多只看最终答案是否准确，无法检查模型在推理过程中是否忠实于每个阶段的证据。
- 现有事实性多跳问答基准多基于维基百科等公开语料构建，而这类语料很可能出现在 LLM 预训练阶段，带来数据污染问题，使评测结果不可信。
- 因此，论文提出 CofCA（Step-wise and Counterfactual Multi-hop QA benchmark），希望从“逐步推理”和“反事实改写”两个角度揭露 LLM 是否真正使用了给定证据。

## 2. 方法论

- **核心思想**：构建一个同时包含“事实数据”和“反事实数据”的评测基准，并通过逐步拆解问题链的方式，让模型在每一步都显式展示其证据检索与推理过程，而不是只给出最终答案。
- **逐步（Step-wise）设计**：将多跳复杂问题拆分为一连串子问题，模型需要按顺序处理每个子问题并利用对应证据。这样可使证据使用过程“可视化”，更容易追踪模型在哪一步跳出了正确推理链。
- **反事实（Counterfactual）设计**：对子问题对应的上下文进行反事实改写，使原有事实记忆与上下文内容发生冲突。如果模型仍按内部记忆作答，就会在中间步骤上暴露问题，从而区分模型是“记忆驱动”还是“证据驱动”。
- **评估方式**：不只比较最终答案，而是结合推理链和逐步推理表现进行判断，从而识别模型是否真正遵守给定材料。
- **需要说明的是**：由于可见材料只有摘要，正文中关于反事实改写如何构造、子问题如何自动生成、是否有公式化实现等细节，目前无法具体展开。

## 3. 实验设计

- **核心基准**：CofCA，由事实数据与反事实数据构成；事实数据对应维基百科来源，反事实数据则是在其基础上进行逐步改写。
- **对比场景**：将多个 LLM 放在“基于维基百科的事实数据”与“反事实数据”上进行对比。
- **实验目标**：观察模型在两类数据上的表现差异，以判断其是否存在预训练数据污染和“绕过正确推理链”的行为。
- **可见材料中未提供**：具体测试了哪些 LLM 模型、参数量大小、对比基线模型、子问题数量、测试集条目数、评测指标公式及数值结果等细节。

## 4. 资源与算力

- 在所给摘要和元数据中，**没有提及任何算力信息**，例如 GPU 型号、GPU 数量、训练时间、推理成本或人工标注投入等。
- 由于无法访问正文，暂时不能判断论文是否在完整版本中报告了计算资源；但至少在可见摘要范围内没有相关说明。

## 5. 实验数量与充分性

- 从摘要可见的实验内容主要是：多个 LLM 在事实数据与反事实数据上的性能对比，并观察其性能差距。
- 这类实验能直接支撑“已有事实基准可能受到数据污染”的核心判断，也可以展示当前 LLM 在多跳推理中存在“绕开正确推理链”的问题。
- 但是，仅凭摘要无法判断实验的充分性：例如是否包含消融实验、不同提示策略的影响、推理链评估的人工验证、基准质量问题、误差分析或统计显著性检验等。
- 因此，从当前可见信息看，实验方向清晰，但**证据链的完整性和公平性仍需查阅全文后才能评价**。

## 6. 主要结论与发现

- 多个 LLM 在维基百科事实数据与反事实数据之间存在显著性能落差，说明已有基于公开语料的评测可能受到预训练数据污染影响，存在高估模型能力的风险。
- LLM 经常“绕过正确的推理链”（bypass the correct reasoning chain），在没有完整执行逐步推理的情况下得出看似合理的答案，导致多跳推理表现被夸大。
- CofCA 的逐步、反事实设计可以更细粒度地区分“记忆调用

鉴于摘要可见内容在此句结束，下面继续补全论点归纳、潜在局限以及面向后续研究的启示；不重复第 1–5 节已述内容。

## 6. 主要结论与发现（续）

- CofCA 的逐步、反事实设计可以更细粒度地区分“记忆调用”与“证据推理”：当模型在反事实数据上仍沿用预训练知识、未依据改写后的证据调整中间答案时，即可明确判定其并未真正遵循给定上下文。
- 与仅看最终答案的评测相比，逐步评估能够在推理链的某一环节捕获失败信号，避免“一步错、最终答案却碰巧正确”带来的误判。
- 从摘要措辞看，论文作者认为现有“事实性多跳问答评测高分”并不等于“多跳推理能力强大”，其更可能是模型利用预训练语料中的相关事实进行捷径推断的结果。
- 由此引出的总体主张是：多跳问答评测若不引入反事实机制并检查中间步骤，就难以将“检索增强式推理”与“参数化记忆召回”干净地区分开。

## 7. 潜在局限与值得推敲之处

- **可推广性有限的风险**：反事实改写是否只作用于文本层面的“名词替换”，还是对逻辑关系、时空约束、数值条件等核心要素也做了系统扰动，仅凭摘要无法确认；若改写深度不足，模型仍可能通过表面线索绕过测试意图。
- **改写质量对公平性的影响**：反事实问题可能存在违反常识或引入表达歧义的情况。若改写后的句子不通顺或语义含糊，那么模型表现下降未必反映记忆依赖，而可能仅仅是语言理解负担增加——这是该基准须通过质量控制与人工校验来回答的问题。
- **无法排除评测过程中的提示偏差**：摘要没有说明是否对所有模型采用完全一致的提示模板、是否对推理链格式做了统一约束，而这些因素在多跳问答中极易引入额外方差。
- **反事实本身可能难以为强模型提供足够约束**：如果模型判断出语境属于反事实模拟（如“假设 Wiki 页面改成……你会怎么回答”），较强的模型也可能主动抑制内部记忆并临时切换参照系，这使得“反事实落差”在模型能力增强后未必能持续反映记忆依赖。
- **数据污染检验的间接性**：事实—反事实性能差只能为预训练数据污染提供间接证据；要更有力地证明污染，还需比对模型对事实语料中独有实体、非常见组合及不同改写强度下的敏感性。仅从基线差的广度无法完全锁定污染来源。

## 8. 对评测研究与模型开发的启示

- 对于评测基准设计者而言，CofCA 提示一个方向：将“渐进式证据链”与“语义冲突注入”结合，可以作为通用多跳工具属性评测的组件，而不仅是另一个静态 QA 数据集。
- 对需要发布基准的团队而言，论文在公开材料中蕴含的一个可借鉴之处是：围绕同一套问题构建“事实/反事实”平行视图，利用差异分数形成诊断指标，而非单点准确率。
- 对模型开发者而言，该工作提醒：仅靠“可解释的提示词”让模型输出思考过程，并不保证推理忠实；更关键的是评测能否在某步给出“错误知识诱饵”，迫使模型选择拒绝内部记忆、转向文本证据。
- 未来的重要延伸方向包括：将 CofCA 扩展到多语言与跨域知识场景、对不同推理拓扑（如链式、树式、比较式）进行更细粒度的诊断，以及把反事实干扰动态嵌入训练过程，从而改善模型对证据变化的敏感性。

## 9. 总体评价

- 从可见材料来看，CofCA 在问题定义上是清晰且有价值的：它精准打中了“记忆掩蔽推理”这一多跳问答评测中的核心痛点，并把评估粒度从“末位答案”推进到“过程性证据使用”，具备较高的方法驱动意义。
- 由于正文信息缺失，当前能确认的主要是基准的设计理念与实验结果方向；涉及构建细节、基准质量控制、比较模型集合和完整指标的部分，建议在获取全文后进一步核对。
- 总体判断：该工作的原创贡献集中在评测思路与诊断机制，而不是提出新的推理模型架构；作为“评测型”研究，其说服力最终取决于定量指标能否覆盖足够多样的反事实扰动类型，并配合透明可复现的样本示例进行叙述验证。

（完）
