---
title: "From Loops to Oops: Fallback Behaviors of Language Models Under Uncertainty"
title_zh: 从循环到失误：不确定性下语言模型的回退行为
authors: "Maor Ivgi, Ori Yoran, Jonathan Berant, Mor Geva"
date: 2024-09-23
pdf: "https://openreview.net/pdf?id=tFwEsrx1hm"
tags: ["query:faithfulness"]
score: 8.0
evidence: 分类并分析预训练规模与指令微调如何改变重复和幻觉等回退行为，与训练如何影响幻觉倾向直接相关。
tldr: 本文认为大模型在不确定性下会表现出序列重复、退化文本与幻觉等回退行为，并考察了预训练数据量、参数规模与指令微调对这类行为的影响。作者在同一模型族内系统分类并比较这些回退现象，发现模型训练规模越大或经过指令调优，其回退行为会发生清晰而一致的变化。这一结果表明重复与幻觉并非孤立缺陷，而是模型不确定性下的不同回退层级。对理解训练如何改变幻觉倾向具有参考价值。
source: ICLR-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 大模型常出现幻觉和序列重复等不良行为，本文将这类现象统一视为不确定性下的回退行为，并探查其与训练状态的关系。
method: 在模型家族中按预训练数据量、参数规模和是否指令微调分组，系统分类并比较重复、退化文本与幻觉三类回退行为。
result: 实验发现模型越先进，回退行为类型呈现清晰而一致的变化：重复等退化行为减少，幻觉特征发生转移。
conclusion: 重复与幻觉应被理解为模型不确定性的不同回退表现，训练过程会系统性改变回退层级。
---

## Abstract
Large language models (LLMs) often exhibit undesirable behaviors, such as hallucinations and sequence repetitions.
We propose to view these behaviors as fallbacks that models exhibit under epistemic uncertainty, and investigate the connection between them.
We categorize fallback behaviors — sequence repetitions, degenerate text, and hallucinations — and extensively analyze them in models from the same family that differ by the amount of pretraining tokens, parameter count, or the inclusion of instruction-following training.
Our experiments reveal a clear and consistent ordering of fallback behaviors, across all these axes: 
the more advanced an LLM is (i.e., trained on more tokens, has more parameters, or instruction-tuned), 
its fallback behavior shifts from sequence repetitions, to degenerate text, and then to hallucinations.
Moreover, the same ordering is observed during the generation of a single sequence, even for the best-performing models; as uncertainty increases, models shift from generating hallucinations to producing degenerate text and finally sequence repetitions. 
Lastly, we demonstrate that while common decoding techniques, such as random sampling, alleviate unwanted behaviors like sequence repetitions, they increase harder-to-detect hallucinations.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- 大型语言模型（LLMs）在实际应用中经常表现出不受欢迎的行为，最典型的两类是**幻觉（hallucinations）**和**序列重复（sequence repetitions）**。
- 以往研究通常将这两类现象视为彼此独立的缺陷，分别加以研究和治理。
- 本文提出一个新的统一视角：**将幻觉、序列重复和退化文本（degenerate text）都视为模型在“认知不确定性”（epistemic uncertainty）下表现出的“回退行为”（fallback behaviors）**。
- 在此框架下，作者系统探究这些看似不同的失败模式之间的内在关联，以及它们如何随模型训练状态（如预训练数据量、参数量、是否经过指令微调）而系统性演化。
- 整体含义：重复与幻觉并非孤立缺陷，而是一个连续的回退层级（fallback hierarchy）中的不同表现。这为理解 LLM 失败机制、改进解码策略与训练方法提供了新视角。

## 2. 方法论

- **核心思想**：将三类不良输出行为——序列重复（sequence repetitions）、退化文本（degenerate text）、幻觉（hallucinations）——统一归类为模型在不确定性下的**回退行为**类别，并研究这些类别之间的排序（ordering）与转换关系。
- **技术关键点**：作者认为模型的回退层级会沿着“训练先进程度”的梯度发生变化——模型越先进（预训练 token 越多、参数越多、经过指令微调），回退行为的类型会从低层形式（重复）向高层形式（幻觉）转移。
- **论文未提供具体公式或算法流程图**；其方法论的核心是**行为分类框架 + 跨模型维度的系统比较**，属于实证分析方法，而非提出新的训练算法或解码算法（注：由于现有材料为基础，具体判定标准和量化指标无法获取）。

## 3. 实验设计

- 根据现有材料，实验主要是在 **同一模型家族（same model family）内** 进行。
- 设置了三组独立比较维度，每次仅变化一个轴：
  1. **预训练 token 数量不同**的模型；
  2. **参数规模不同**的模型；
  3. **是否经过指令微调（instruction-following training）** 的模型。
- 实验任务是分类并比较三类回退行为（重复、退化文本、幻觉）在上述维度下的表现差异。
- 论文未提供具体数据集名称和 benchmark 细节，也未报告与外部基准方法的对比结果——材料中没有说明是否存在基线方法对比。

## 4. 资源与算力

- **论文中没有明确报告所消耗的算力资源**，如 GPU 型号、数量或训练 / 评估时长等信息在现有文本中均未出现。
- 由于本文是开放性研究，使用的模型可能来自公开的预训练模型家族，但即便如此，论文材料中未给出任何资源相关信息。

## 5. 实验数量与充分性

- 根据现有材料可确认至少开展了以下系统性比较实验（同一模型族内）：
  1. 不同预训练 token 量的对比实验；
  2. 不同参数规模的对比实验；
  3. 有无指令微调的对比实验；
  4. 单序列生成过程中的动态回退行为分析；
  5. 对解码技术（随机采样）影响的验证。
- **充分性与客观性评估**：由于材料仅为摘要和元数据，无法判断实验数量是否充分、对比是否公平。从已揭示信息看，其横向系统比较设计合理，但尚不清楚是否覆盖多样化模型架构、多种语言或不同任务类型。公开发表的元数据中有明确的客观性风险（如幻觉的检测方法可能有一定偏差），需结合全文确认。

## 6. 主要结论与发现

- 作者在多个模型维度上观察到**清晰且一致的回退行为排序规律**：
  > 模型越先进（预训练 token 越丰富、参数越多、或经过指令微调），其回退行为*从序列重复 → 退化文本 → 幻觉*方向转移。
- 同样的排序规律**也在单条序列的生成过程中动态出现**：即便对性能最好的模型，其生成的每一步不确定性升高时，回退行为会从幻觉退回退化文本，最终退回序列重复，形成一个稳健的回退层级表。
- 研究还揭示了**解码策略与回退行为的权衡**：常用解码技术如随机采样（random sampling）虽然能减少序列重复等表面明显的退化行为，但同时会**增加更难以检测的幻觉输出**。

## 7. 优点

- **统一性视角有理论价值**：首次将重复、退化文本和幻觉纳入统一的不确定性模型的框架内分析，强调整体失败层级的迁移而非孤立缺陷的叠加，为“忠实性”讨论提供一个分类基准。
- **多维度的交叉验证设计**：在同一模型族内同时改变三轴（数据量、参数量、指令微调），可以把单一轴上的变化归因于普通成长效应还是架构共性，结论的可推广性更高。
- **动态微观视角**：不仅比较最终输出，也探测生成过程每一步的回退动态（从幻觉逐步“退回”到重复），对开放生成诊断有借鉴意义。
- **提示出解码算法的隐蔽副作用**：随机采样在消除重复的同时会增大难以察觉的幻觉概率，暗示仅仅追求流畅性解码并不能缓解不确定性问题，这一结论有实践参考意义。

## 8. 不足与局限

- **实验范围不全面**：材料中未提及所测试的任务类型（如问答、摘要、常识推理？）、模型架构和语言多样性，也未见与主流的幻觉消减方法（如 fact-guided decoding、对照解码等）的比较。
- **分类体系存在主观性**：三类回退行为（如幻觉）的界定与自动度量方式不确定，在开放生成任务中，幻觉的定义本身就高度依赖于评估方法与事实来源。
- **数据缺失风险**：由于缺少具体的数据集及 benchmark 细节，难以评估其实验结果的外部效度，这是论文上下文不可回避的局限性。
- **无法判别公平化指标**：本材料不足以判断其是否控制了生成温度、prompt模板、训练批次等混杂因素，该评判只能依赖全文。
- **不同计算规模的可延展性**：作者也承认 回退层级在多语言、超大规模 RLHF 等新的训练范式下是否仍然成立，仍属于未证议题（元数据中的 rejected 注释提示，这一点或成为评审重点关注的范围）。

## 总结一句话

> 本文将重复、退化文本和幻觉统一为“不确定性下的回退行为”体系，并在同一模型族内沿预训练数据量、模型参数和指令微调三条轴线比较，确认 LLM 能力增强时回退行为层级会系统地由“重复”迁移到“幻觉”，同时发现常用的随机解码在缓解重复时反而会加剧更隐蔽的幻觉风险——这一条可为 LLM 不确定性理论、忠实性评估与解码策略设计提供参考框架。

（完）
