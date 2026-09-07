---
title: "On the Limits of LLM Adaptability: Impact of Model-Internalized Priors on Annotation Task Performance"
title_zh: 论大语言模型适应性的边界：模型内化先验对标注任务性能的影响
authors: "Etienne Casanova, Rafal Kocielnik, R. Michael Alvarez"
date: 2026-04-30
pdf: "https://openreview.net/pdf/791a3d53d1a5ef473c83966e4025be4de38cada7.pdf"
tags: ["query:faithfulness"]
score: 4.0
evidence: 实证研究模型内化先验、决策粘性和任务定义误配导致零样本错误持续；与语言先验压制输入信号造成的不忠实输出弱相关
tldr: 论文考察大模型作为零样本标注器时，模型内化的先验如何与任务指令交互并限制其适应性。实验覆盖社交、游戏、新闻等多领域毒性检测，发现约三分之二的零样本错误难以靠任务提示纠正，即决策粘性现象，任务定义误配时模型倾向沿用先验。该结果提示先验可能压制输入证据和指令信号，对理解标注与判断任务中的不忠实输出具有参考意义。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型零样本标注可靠性受内化先验与指令交互影响，模型可能在任务提示下仍重复先验错误。
method: 设计三维度实验，在多个毒性检测数据集上测试先验熟悉度、提示纠错能力与任务定义误配的影响。
result: 约三分之二的零样本错误无法被提示信息纠正，显示决策粘性强、先验主导任务表现。
conclusion: 必须关注模型内化先验的固化作用，任务信息和外部证据难以完全扭转其零样本判断偏差。
---

## Abstract
Large Language Models (LLMs) are increasingly used for zero-shot annotation and LLM-as-a-judge tasks, yet their reliability hinges on how model-internalized priors interact with user-provided instructions. We investigate three dimensions of this interaction: (1) how an LLM's familiarity with data and task definitions affects performance, (2) the extent to which additional information in prompts can correct zero-shot errors (``decision stickiness''), and (3) model susceptibility to misaligned task definitions. Through experiments on toxicity detection across diverse datasets (spanning social media, gaming, news, and forums) using both dense and mixture-of-experts models, we find that nearly two-thirds of zero-shot errors are resistant to correction, with an overall rescue rate (fraction of initial errors corrected by prompting) of only 34.8\%. High-confidence errors prove especially resistant to correction. When given misaligned definitions, LLMs follow them while maintaining confidence levels unchanged from the aligned condition. Crucially, we introduce Definition-Specific Familiarity (DSF), which measures alignment between a model's internal concept and the task definition. After controlling for dataset-level confounds, DSF shows a positive association with model performance (partial $r=+0.41$), while three distinct memorization metrics (ROUGE-L, BERTScore, and embedding cosine similarity) all fail to show a positive association. These findings show the limitations of prompt-based correction in annotation tasks, highlighting the importance of definition alignment over text-level memorization.

---

## 论文详细总结（自动生成）

说明：所提供的“论文 PDF 提取文本”实际为 OpenReview 的浏览器验证页，因此无法获得完整正文。以下总结严格依据随附的论文元数据与 Abstract 内容撰写；凡原文未给出信息的部分，均会明确标注“原文未说明”。

## 1. 核心问题与整体含义

- **研究背景**：大语言模型（LLM）被越来越多地用于零样本（zero-shot）标注以及“LLM-as-a-judge”类任务，但其可靠性取决于**模型内化先验（model-internalized priors）**与**用户提供指令**之间的复杂交互。
- **核心问题**：模型内在的、事先固化的“常识性偏好”是否会在任务提示存在的情况下依然主导模型行为，从而限制 LLM 在标注与判断任务上的适应能力？
- **论文整体含义**：论文从三个维度切入——(1) 模型对数据与任务定义的熟悉程度如何影响表现；(2) 在提示中追加额外信息能否纠正零样本错误（即“决策粘性”）；(3) 模型对“错位/有偏差的任务定义”是否易受影响。整体研究指向一个警示性结论：**提示层面的纠错作用存在明确边界**，定义对齐比文本层面的记忆更重要。

## 2. 提出的方法论

- **核心思想**：通过量化“模型内化概念”与“任务定义”之间的对齐程度，来解释零样本标注中难以被提示纠正的错误来源。
- **关键概念——“定义特定熟悉度”（Definition-Specific Familiarity，DSF）**：
  - 用于衡量模型内部关于某类目标的概念与其拿到的任务定义之间的匹配程度。
  - 论文假设：DSF 越高，模型越可能正确执行任务；DSF 越低，模型更容易沿用自身先验而产生系统性错误。
- **实验性对比指标**：与 DSF 相对照，作者使用了三类**记忆/表层相似度指标**——ROUGE-L、BERTScore、嵌入向量余弦相似度——用于检验“文本级记忆”是否能解释性能，并与 DSF 做区分。
- **“救援率”（rescue rate）**：定义为“被提示信息成功纠正的初始错误的比例”，用于量化决策粘性强弱。
- **论文的 Abstract 中未给出具体公式或算法伪代码**，但从描述来看，其流程大致是：
  - 让模型在多种毒性检测数据上进行零样本标注；
  - 对错误样本增加额外提示信息，看能否纠正；
  - 分别在有/无错位任务定义下观察模型行为与置信度；
  - 对数据集层面混淆因素进行控制后，计算 DSF、记忆指标与模型表现的相关关系。

## 3. 实验设计

- **任务场景**：以“毒性检测（toxicity detection）”为零样本标注任务；该任务同时具有实际应用意义与可量化真值。
- **数据集覆盖**：
  - 覆盖多种话语类型的多个数据集：社交媒体、游戏、新闻、论坛。
  - 原文未列出具体数据集名称，但摘要表明其跨域多样性是设计核心之一。
- **模型类型**：
  - 使用了 **dense models（密集模型）** 与 **mixture-of-experts models（MoE 模型）**。
  - 具体模型名称与参数量在 Abstract 中未说明。
- **Benchmark/对比方法**：
  - 并非典型的“模型间对比”，而是**条件对比**：
    - 对齐任务定义 vs. 错位任务定义；
    - 高置信错误 vs. 低置信错误的可纠正性；
    - DSF 的预测能力 vs. ROUGE-L/BERTScore/嵌入余弦三种记忆指标。
  - 主要统计结果为：总 rescue rate 34.8%；DSF 偏相关系数 +0.41；三种记忆指标均未呈现正向关联。

## 4. 资源与算力

- **原文未说明**：在所提供的 Abstract 与元数据中，没有提及任何 GPU 型号、数量、训练时长、推理预算或总的计算资源消耗。
- 只能推测其实验规模属于“提示/推理级”评测，而非大规模预训练或微调，但这一点是合理推断，论文正文中并无明确信息。

## 5. 实验数量与充分性

- **实验内容覆盖**：
  - 从摘要可确定至少包含以下实验组：
    1. 零样本毒性检测基线；
    2. “提示附加信息试图纠正错误”的决策粘性测试；
    3. 错位任务定义下的行为与置信度测试；
    4. DSF 与三种记忆指标对性能的预测力比较。
- **关于数量**：原文未披露精确的数据集数量、样本量、试验轮次或消融实验数量，因此无法严格评估统计功效。
- **充分性评述**：
  - 从设计上看，跨多个话语域、同时覆盖 dense 与 MoE 模型、并控制数据集层面混淆，具有一定说服力。
  - 但仅局限于毒性检测一种任务类型；若推广到更广泛的“LLM-as-a-judge”任务，证据强度仍然偏弱。
  - 由于缺乏正文细节（如公式、prompt 原文、模型列表），无法判断其实验设计是否完全客观、公平；例如“错位定义”的具体构造方式对结果影响很大，而 Abstract 中没有给出。

## 6. 主要结论与发现

- **决策粘性明显**：约三分之二的零样本初始错误无法通过向提示中追加信息来纠正。
- **救援率低**：整体救援率仅为 **34.8%**，说明提示纠错效果有限。
- **高置信错误尤其顽固**：模型对自身高置信度的错误判断表现出更强的抵抗纠正倾向。
- **错位定义会被接受但不改变置信度**：当任务定义本身存在偏差或与真实意图不符时，LLM 会选择跟随该定义，却**维持与对齐定义条件相当的置信度**——这表明模型在方向被带偏时并不会“感知”到风险。
- **DSF 能正向预测表现**：在对数据集层面的混淆因素进行控制后，DSF 与模型性能呈正相关（偏相关 **r = +0.41**）。
- **记忆类指标不能解释表现**：ROUGE-L、BERTScore 与嵌入余弦相似度三种文本级记忆指标均未显示出与模型性能的正向关联。
- **总体判断**：模型不适应任务往往不是“记不记得住文本”的问题，而是“内部先验与任务定义是否匹配”的问题；提示工程能提供的纠正能力存在结构性上限。

## 7. 优点

- **问题分解清晰**：把“模型内化先验的干扰”拆为熟悉度、决策粘性、定义敏感性三个可操作维度，便于实验与归因。
- **提出有区分度的新指标 DSF**：把分析焦点从“文本记忆”转移到“概念对齐”，并直接与三类常见记忆指标作对比，有助于澄清文献中关于“模型是否为记忆驱动”的争论。
- **统计控制较严格**：特别提到“控制数据集层面混淆因素”后才计算偏相关，降低了跨数据集差异造成伪相关的风险。
- **实验材料具有生态效度**：使用社交、游戏、新闻、论坛等多个实际毒性检测场景，比单一语料更具外部推广潜力。
- **直面应用痛点**：针对 LLM-as-judge 的实际部署场景，给出了“提示纠错并不可靠、需重视任务定义设计”的可操作启示。

## 8. 不足与局限

- **任务域局限**：只基于“毒性检测”一类任务得出结论，能否外推到事实核查、情感标注、法律判断或医疗标注等高风险场景尚不确定。
- **纠错手段单一**：论文中的“纠正”仅指通过提示附加信息；没有覆盖思维链、few-shot 示范、拒绝重试、外部证据检索等更强或更实际的对策，因此 34.8% 的救援率可能低估了现实中的总体可纠正程度。
- **对“错位定义”只报告了行为结果**：Abstract 显示模型会跟随错位定义且置信度不变，但没有给出该现象背后的机制解释（例如注意力分配、token 概率分布变化）。
- **信息不完整难以评价**：由于原文 PDF 只有验证页，本文无从确定其数据集规模、prompt 设计细节、模型版本、统计显著性区间等；论文评审得分 4.0 也表明其在完整审稿语境下可能存在争议点（如新颖性或实验充分性）。

（完）
