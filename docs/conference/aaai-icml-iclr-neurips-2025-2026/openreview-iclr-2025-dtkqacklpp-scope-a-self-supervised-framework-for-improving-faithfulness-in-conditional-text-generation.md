---
title: "SCOPE: A Self-supervised Framework for Improving Faithfulness in Conditional Text Generation"
title_zh: SCOPE：提升条件文本生成忠实性的自监督框架
authors: "Song Duong, Florian Le Bronnec, Alexandre Allauzen, Vincent Guigue, Alberto Lumbreras, Laure Soulier, Patrick Gallinari"
date: 2025-01-22
pdf: "https://openreview.net/pdf?id=dTkqaCKLPp"
tags: ["query:faithfulness"]
score: 9.0
evidence: 针对条件文本生成对上下文的忠实性提升并抑制幻觉，覆盖摘要与数据到文本任务
tldr: 大型语言模型在摘要和数据到文本生成中常引入与输入上下文不一致的幻觉内容，这源于对训练数据统计模式的依赖。SCOPE通过自监督方式强化模型对给定上下文的忠实性，抑制额外信息的生成。实验证明该方法能显著提升条件生成内容与上下文的一致性，为缓解条件生成幻觉提供了一种低成本的通用途径。
source: ICLR-2025-Accepted
selection_source: conference_retrieval
motivation: 条件生成中模型受训练统计先验干扰，容易产生未基于输入证据的幻觉内容，需提升生成忠实性。
method: SCOPE设计自监督任务，以模型对给定上下文的复述与还原为监督信号，促使生成尽量忠实于输入证据。
result: 在摘要与数据到文本等任务中，SCOPE可明显降低幻觉和不忠实内容，提升与上下文的一致性。
conclusion: 自监督的忠实性强化能通用地改善条件文本生成，为缺少标注场景下的幻觉缓解提供了有效手段。
---

## Abstract
Large Language Models (LLMs), when used for conditional text generation, often produce hallucinations, i.e., information that is unfaithful or not grounded in the input context. This issue arises in typical conditional text generation tasks, such as text summarization and data-to-text generation, where the goal is to produce fluent text based on contextual input. When fine-tuned on specific domains, LLMs struggle to provide faithful answers to a given context, often adding information or generating errors. One underlying cause of this issue is that LLMs rely on statistical patterns learned from their training data. This reliance can interfere with the model's ability to stay faithful to a provided context, leading to the generation of ungrounded information. We build upon this observation and introduce a novel self-supervised method for generating a training set of unfaithful samples. We then refine the model using a training process that encourages the generation of grounded outputs over unfaithful ones, drawing on preference-based training. Our approach leads to significantly more grounded text generation, outperforming existing self-supervised techniques in faithfulness, as evaluated through automatic metrics, LLM-based assessments, and human evaluations.

---

## 论文详细总结（自动生成）

# SCOPE 论文总结

## 1. 论文的核心问题与整体含义

- 大型语言模型（LLMs）在**条件文本生成**任务中容易产生“幻觉”内容，即生成与给定输入上下文不一致或缺乏证据支撑的信息。
- 典型场景包括**文本摘要**和**数据到文本生成**（data-to-text），这类任务的目标是基于上下文输入，生成流畅且忠实于上下文的文本。
- 论文指出了一个关键成因：LLMs 在预训练阶段习得了大量**训练语料中的统计模式**；在领域微调或条件生成时，这些统计先验会干扰模型对当前上下文的忠实性，使其“自发补全”或加入不实信息。
- 整体研究含义是：提高条件生成对上下文的忠实性，是抑制幻觉、提升模型可信度的关键；论文希望提供一种**不需要昂贵人工标注**的通用改进方案。

## 2. 论文提出的方法论

- **核心思想**：不依赖额外人工标注，而是通过**自监督方式构造“不忠实的样本”**，再用**偏好式训练**让模型学会优先生成忠实于上下文的输出，抑制与上下文无关的额外信息。
- **主要技术流程（据摘要与元数据推断）**：
  1. 利用模型本身或自监督机制，基于给定上下文生成/构造一组**不忠实（unfaithful）输出**，作为负面样本。
  2. 同时保留或构造对应的**忠实输出**作为正面样本。
  3. 借助**偏好式训练**（preference-based training），更新模型参数，使模型对忠实输出的得分/概率高于不忠实输出。
  4. 训练后的模型在条件生成时，会更强地依赖给定上下文，而非训练数据中的统计先验。
- 元数据提示其设计还涉及“模型对给定上下文的复述与还原”作为监督信号，用于促使生成内容尽量忠实于输入证据。
- 摘要中未给出具体公式或算法伪代码，但整体可归类为：**自监督负样本构造 + 偏好优化/对齐式训练**。

## 3. 实验设计

- **任务场景**：
  - 文本摘要（text summarization）
  - 数据到文本生成（data-to-text）
- **评估方式**：
  - 自动评估指标（automatic metrics）
  - 基于 LLM 的评估（LLM-based assessments）
  - 人工评估（human evaluations）
- **对比方法**：
  - 摘要中明确提到 “优于现有的自监督技术（existing self-supervised techniques）”，但**没有列出具体基准方法名称**。
  - 论文元数据仅给出“条件文本生成对上下文的忠实性提升”这一主题，未给出特定数据集名称，如 CNN/DailyMail、XSum、WebNLG、E2E 等。
- **说明**：当前提取文本中缺乏具体的 benchmark、对比模型和消融设置细节，需查看论文正文才能获得完整实验图谱。

## 4. 资源与算力

- 在当前提供的摘要和元数据中，**没有说明**使用了什么 GPU 型号、GPU 数量、训练时长、参数量、显存占用等信息。
- 这一点属于信息缺失，需要查阅论文“实验设置”部分才能补充。

## 5. 实验数量与充分性

- 从摘要看，实验覆盖了**至少两个任务类型**，并采用了**三类评估方式**，包括人工评估，这在一定程度上增强了结论的可信度。
- 元数据提到方法能“降低幻觉和不忠实内容，提升与上下文的一致性”，说明实验在主要任务上取得了正面效果。
- 但仅凭当前内容，**无法判断实验组数、消融实验是否充分、基线与统计检验是否公平客观**。
- 潜在公平性风险包括：基线选择是否覆盖足够多的强方法、自监督负样本构造方式是否会导致评估偏向、人工评估的规模和一致性检验等，均需原文确认。

## 6. 论文的主要结论与发现

- LLMs 在条件生成中的幻觉问题，与其过度依赖训练语料统计模式有关。
- 通过自监督生成不忠实样本并进行偏好式训练，可以明显提升生成文本对输入上下文的忠实性。
- 该方法在文本摘要和数据到文本生成上，均优于现有自监督忠实性提升方法。
- 该训练策略可以作为一种**低成本、通用性强**的手段，用于缓解条件生成中的幻觉问题。

## 7. 优点

- **自监督机制**：不需要人工标注不忠实样本，降低了数据成本。
- **问题切入清晰**：将幻觉归因于“训练统计先验干扰上下文服从”，动机明确。
- **偏好式训练**：能够直接优化模型“选择忠实输出而非不忠实输出”的排序能力，与生成质量目标匹配。
- **多维度评估**：同时使用自动指标、LLM 评估和人工评估，提高了结论的可信度。
- **适用面广**：面向摘要和数据到文本两类代表性条件生成任务，方法可能具有较好的通用性。

## 8. 不足与局限

- **信息局限**：本次仅提供摘要与元数据，缺少数据集名称、基线列表、超参数、训练细节等，无法全面判断实验充分性。
- **负样本构造依赖设计质量**：自监督生成“不忠实样本”的方式如果覆盖不全，可能无法触发模型潜在的所有幻觉模式。
- **幻觉成因单一化风险**：论文强调统计先验的干扰，但幻觉还可能来自解码策略、知识冲突、上下文过长等，本文方法未必能覆盖所有成因。
- **适用范围有限**：实验仅提及摘要和数据到文本，对开放域对话、问答、长文档生成等任务上的表现未知。
- **偏好式训练的潜在偏差**：偏好训练可能使模型变得过于保守，影响生成信息的丰富性或流畅性。
- **代码/数据/复现性**：当前摘要未说明是否开源模型或代码。

（完）
