---
title: Mitigating Multimodal Hallucinations via Gradient-based Self-Reflection
title_zh: 基于梯度自我反思缓解多模态大语言模型幻觉
authors: "Shan Wang, Maying Shen, Nadine Chang, Chuong Nguyen, Hongdong Li, Jose M. Alvarez"
date: 2024-09-26
pdf: "https://openreview.net/pdf?id=zgXGNXkC0F"
tags: ["query:faithfulness"]
score: 7.0
evidence: 利用梯度自我反思与对比解码缓解文本-视觉幻觉，对事实幻觉的约束解码缓解具有可迁移性
tldr: 多模态幻觉源于文本-视觉偏差、共现偏差和长序列偏差，已有缓解通常依赖外部视觉接地或额外评分模型。论文提出基于梯度的自我反思与影响感知对比解码，利用模型内部梯度定位幻觉来源并干预解码过程。实验表明无需额外视觉资源即可降低三类偏差导致的幻觉，尤其改善共现偏差，为约束解码抑制事实幻觉提供借鉴。
source: ICLR-2025-Public
selection_source: conference_retrieval
motivation: MLLM幻觉由文本-视觉、共现和长序列三类偏差引起，现有点状缓解依赖外部视觉接地且难以覆盖全部偏差。
method: 提出基于梯度的影响感知对比解码与自我反思，利用内部梯度指导解码并抑制易导致幻觉的标记。
result: 在无需额外视觉接地条件下降低多类偏差所致幻觉，对共现偏差的缓解尤为明显。
conclusion: 基于梯度的自我反思与对比解码是无外部视觉资源的有效幻觉缓解路径。
---

## Abstract
Hallucination in Multimodal Large Language Models (MLLMs) occurs when inaccurate text-visual alignments are generated, posing a major challenge for reliable model output. Previous studies have identified three primary biases as major causes of hallucinations: text-visual bias (over-reliance on text over visual details), co-occurrence bias (misleading object correlations), and long-term bias (increased hallucinations in later stages of long sequences). Existing hallucination mitigation methods often rely on visual grounding, which requires additional resources such as scoring systems using another MLLM, and still fail to fully address all biases, particularly co-occurrence bias in visual inputs. We propose Gradient-based Influence-Aware Contrastive Decoding (GACD) to explicitly and jointly balance these biases, thereby mitigating hallucinations. To quantify these biases at the individual sample level, we introduce `token influence'. Since biases are rooted in the training data and become embedded in pre-trained MLLMs, we derive token influence through self-reflection by calculating the gradients from output predictions to input tokens. Notably, GACD is the first approach capable of fully addressing co-occurrence bias without relying on extra resources or any form of tuning. Extensive experiments demonstrate GACD's effectiveness in reducing hallucinations and improving MLLM performance, achieving new state-of-the-art results while providing insights into the visual perception capabilities of these models.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 核心问题与整体含义

- **研究背景**：多模态大语言模型（MLLM）在生成与图像内容相关的文本时，常产生“幻觉”——即文本与视觉信息不对齐的错误输出，严重影响可靠性。
- **主要诱因**：已有研究归纳为三类偏差：
  - **文本-视觉偏差**：模型过度依赖文本先验而忽视视觉细节；
  - **共现偏差**：利用对象间误导性的统计相关性产生幻觉；
  - **长序列偏差**：在长输出的后期阶段幻觉加剧。
- **现有局限**：已有缓解方法多依赖额外视觉接地资源（如调用另一个 MLLM 做评分系统），且不能全面覆盖所有偏差，尤其难以处理视觉输入导致的共现偏差。
- **研究目标**：提出一种无需额外资源或调参即可缓解幻觉的解码方法，并特别针对共现偏差提供有效解决路径。

## 2. 方法论

- **方法名称**：Gradient-based Influence-Aware Contrastive Decoding（GACD，基于梯度的影响感知对比解码）。
- **核心思想**：不借助外部视觉接地，而是利用模型自身的内部梯度信息，通过自我反思定位幻觉来源，并干预解码过程，以显式平衡三类偏差。
- **关键概念：Token 影响力（Token Influence）**：在单个样本层面量化各偏差的程度。由于偏差根植于训练数据并内嵌于预训练 MLLM 中，可通过计算输出预测对输入 token 的梯度来推导 token 的影响力。
- **技术流程（文字说明）**：
  1. 从模型输出预测出发，计算预测对输入 token（文本与视觉 token）的梯度；
  2. 基于梯度推导各输入 token 的“影响力”分数，用以识别可能加剧幻觉的 token；
  3. 在解码阶段实施“影响感知对比解码”，降低易诱导幻觉的 token 的生成概率；
  4. 将三类偏差的抑制过程联合纳入解码决策，从而在生成阶段同时减轻文本-视觉偏差、共现偏差与长序列偏差。
- **方法定位**：作者称 GACD 是首个在不依赖额外资源、也不需任何形式的调优下，能够完整应对共现偏差的方法。

## 3. 实验设计

- **数据集/场景**：摘要未逐一列出具体数据集名称，但实验针对多模态幻觉的典型 benchmark 展开，覆盖文本-视觉偏差、共现偏差、长序列偏差三类场景。
- **评测任务**：多模态大语言模型的幻觉减少与整体性能提升（包括视觉感知能力的评估）。
- **对比方法**：摘要未详列方法名，但指明与既有依赖视觉接地或额外评分模型的幻觉缓解方法进行比较。
- **评价指标**：以幻觉率下降和 MLLM 性能提升为准，并宣称达到新的 state-of-the-art（SOTA）水平。

## 4. 资源与算力

- 论文摘要中**未明确说明**使用的 GPU 型号、数量、训练/推理时长等算力信息。
- 值得注意的是，该方法属于推理阶段解码策略，**不需要重新训练或调优**，因此算力开销主要来自梯度计算与对比解码过程，但文中未给出具体数值。

## 5. 实验数量与充分性

- **实验规模**：摘要中仅给出概括性结论，未列出表格化的实验组数。从描述可推断至少包含：
  - 三类偏差对应的幻觉缓解实验；
  - 与既有方法的对比实验；
  - 视觉感知能力的分析实验。
- **充分性评估**：
  - 优点：覆盖了三类主要偏差，且对比了外部接地方法，验证了“无额外资源”这一核心主张。
  - 不足：论文摘要层面缺乏消融实验细节、各偏差缓解的定量结果以及不同 MLLM 骨干的可泛化性数据。仅凭摘要难以判断实验完整性与统计显著性。

## 6. 主要结论与发现

- GACD 可**显式且联合地平衡三类偏差**，有效降低多模态幻觉。
- 在不使用外部视觉资源、不进行任何调优的前提下，GACD 是首个能**完全解决共现偏差**的幻觉缓解方法。
- GACD 在幻觉减少与整体性能上均获得提升，达到新的 SOTA 水平。
- 通过梯度自我反思获得的 token 影响力为理解 MLLM 的视觉感知能力提供了新的分析视角。

## 7. 优点

- **自包含性**：不依赖额外视觉接地或外部评分模型，实用性强。
- **机理明确**：从训练数据内嵌偏差出发，用梯度量化 token 影响，解释性强。
- **覆盖全面**：同时针对三类已知偏差，而非只处理某一点状问题。
- **零调优**：无需重新训练或微调，易于部署到已有模型。
- **创新性**：首次在无需额外资源的前提下完整应对共现偏差。

## 8. 不足与局限

- **信息缺失**：摘要中未给出具体数据集名称、基准版本、评测指标数值、消融实验设计等关键细节，可复现性与可验证性需依赖全文。
- **算力报告缺失**：未说明梯度计算带来的额外推理开销，也未报告实验资源，不利于成本评估。
- **通用性存疑**：论文是否只在特定 MLLM 架构上验证？对多语言、多领域、不同视觉编码器的泛化能力尚不清楚。
- **偏差边界定义**：三类偏差的划分与 token 影响力计算是否在复杂真实场景中保持稳健，需要更多压力测试。
- **应用限制**：对比解码可能影响模型原有的生成分布，涉及生成质量与创造性的权衡，文中未讨论潜在副作用。

（完）
