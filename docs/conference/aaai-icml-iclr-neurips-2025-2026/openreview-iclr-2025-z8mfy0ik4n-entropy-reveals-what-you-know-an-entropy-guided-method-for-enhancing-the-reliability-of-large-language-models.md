---
title: "Entropy Reveals What You Know: An Entropy-Guided Method for Enhancing the Reliability of Large Language Models"
title_zh: 熵揭示所知：熵引导增强大语言模型可靠性的方法
authors: "XiaoQi Han, Ru Li, Zhichao Yan, Jeff Z. Pan"
date: 2024-09-27
pdf: "https://openreview.net/pdf?id=Z8Mfy0iK4n"
tags: ["query:faithfulness"]
score: 7.0
evidence: SREF依据熵估计不确定性并鼓励拒答，借助自我引用增强已知事实回答一致性，属拒答机制缓解幻觉的路线。
tldr: 大模型虽参数中蕴含大量知识，但仍会出现事实不一致和不可靠回答。本文提出熵引导的SREF方法，将模型对问题改写后的自我引用理解输入模型，依据熵判断其是否真正知道答案，并对不确定问题鼓励拒答。分析显示SREF能增强已知事实回答的一致性，同时降低不确定问题上的幻觉。该方法为提高LLM可靠性提供了轻量的推理期干预手段。
source: ICLR-2025-Public
selection_source: conference_retrieval
motivation: 大模型虽存储大量知识，仍会出现事实不一致与不可靠回答，给实际应用带来风险；不确定问题尤其危险。
method: 提出熵引导的SREF方法，把模型对问题改写的理解作为自我引用加入输入，并结合熵估计判断是否该拒答或作答。
result: 实验表明SREF能增强已知事实的回答一致性，并在不确定问题上有效鼓励拒答，提升整体可靠性。
conclusion: 通过熵信号和自引用显式建模模型知道什么，为提升LLM可靠性提供了不依赖额外外部证据的轻量途径。
---

## Abstract
While large language models (LLMs) encode vast amounts of knowledge within their parameters for some mainstream entities, factual inconsistencies and untruthfulness in LLMs often lead to unreliable responses and cause significant risks in practical applications.
This paper aims to improve model reliability by enhancing consistency in answers to known facts and encouraging refusal to answer for uncertain questions.
Specifically, we introduce \textbf{SREF}, an entropy-guided approach designed to enhance the reliability of language models by incorporating \textbf{S}elf-\textbf{REF}erences, models' understanding of rephrasing questions, with inputs.
We analyze and reveal the effectiveness of SREF in enhancing model reliability from the perspectives of entropy and KL divergence.
Extensive experiments on 12 LLMs demonstrate that outputs generated with SREF yield more reliable results, including an average improvement of 16.01\% over the baselines and a 15.10\% average improvement in consistency, while also adapting to identify and acknowledge uncertain facts.

---

## 论文详细总结（自动生成）

# 论文详细中文总结：《熵揭示所知：熵引导增强大语言模型可靠性的方法》

## 1. 核心问题与整体含义（研究动机与背景）

- **研究焦点**：大语言模型（LLMs）虽然在参数中内化了大量世界知识，但在回答时仍普遍存在**事实不一致**和**不真实陈述**（untruthfulness）的问题，导致输出不可靠，并在实际应用中带来显著风险。
- **核心动机**：模型内化的知识与它实际“知道并能够稳定输出”的知识之间存在鸿沟。已有方法多依赖外部证据或额外训练，论文希望找到一种**轻量、无需外部证据**的推理期干预方案。
- **解决思路**：通过显式建模模型对自身“知晓状态”的判断，提升对**已知事实**回答的一致性，同时鼓励对**不确定问题**直接拒答，而不是生成幻觉内容。

## 2. 方法论：核心思想、关键技术细节

- **方法名称**：**SREF（Self-REFerences，熵引导的自我引用方法）**。
- **核心思想**：
  - 将模型的**自我引用（self-reference）**——即模型自身对问题改写的理解——与原始输入共同作为模型输入，促使模型更稳定地调用参数内知识。
  - 用**熵（entropy）** 来估计模型对某一问题的“不确定性”，据此判断模型是否**真正知道**答案：熵低代表已知事实，熵高代表不确定。
  - 对熵高（不确定）的问题，**鼓励模型拒答（refusal）**，对熵低的问题则正常作答，从而将“不知道”显式路由为“拒答”，而非幻觉。
- **算法/流程描述（以文字说明代替公式）**：
  1. 让模型对原始问题进行改写（rephrasing）生成若干个改写版本；
  2. 将改写后的理解（self-reference）作为辅助输入与原问题拼接；
  3. 将拼接后的输入送入模型，获得答案生成；
  4. 通过模型的输出分布计算**熵**或**KL 散度**，以衡量模型对该问题回答的不确定性；
  5. 根据熵阈值判断：低熵 → 给出答案；高熵 → 拒答或输出“不知道”。
- **分析视角**：论文从**熵**和**KL 散度**两种信息论指标出发，解释了 SREF 为什么能增强可靠性——自我引用可以让模型在已知事实上形成更集中、低熵的分布，而在未知事实上暴露出高熵、分散的不确定性信号，从而作为拒答依据。

## 3. 实验设计

- **模型覆盖**：在 **12 个大语言模型**上进行了大规模实验，涵盖不同规模与系列，以验证方法的通用性。
- **评估维度**：
  - **可靠性（reliability）**：输出是否更可靠、事实性更强；
  - **一致性（consistency）**：对已知事实多次作答能否保持一致；
  - **不确定性识别**：能否识别并承认不确定的事实（即“知道自己不知道”）。
- **Benchmark 与具体数据集**：
  - 原文文本和元数据中**未给出具体的 benchmark 名称**（如 TruthfulQA、NQ、HotpotQA 等）及数据集细节，仅概括性地描述了实验结论。
- **对比基线**：提出平均提升 16.01% 的“baselines”概念，但**基线的具体方法名称在可获取文本中未列出**。

## 4. 资源与算力（GPU 型号、数量、训练时长等）

- 论文可获取的文本（包括元数据与摘要）中**没有报告任何算力资源信息**，如 GPU 型号与数量（A100/H100 等）、训练或推理时长、总计算成本。
- 根据方法描述，SREF 属于**推理期干预（inference-time intervention）**，无需微调训练，因此预计算力消耗以额外推理次数（改写、多次采样计算熵）为主，但具体数值**文中未说明**。

## 5. 实验数量与充分性：是否充分、客观、公平？

- **实验数量**：
  - 关于实验的主要描述为“在 12 个 LLM 上进行实验”，覆盖模型数量较多（12 个）；
  - 报告了两个关键数字：相对基线平均提升 **16.01%**，一致性平均提升 **15.10%**；
  - 是否包含消融实验（如去掉熵门控、去掉自我引用）在现有文本中无法确认。
- **充分性评估（结合可获取信息）**：
  - **模型覆盖广度较好**：12 个模型的横跨度是本研究的重要优势；
  - 但**缺失细节较多**：具体数据集名称、任务类别（开放式问答？多选？对话？）、不同模型的分项结果均未出现在所给文本中；
  - **公平性判断受限**：无法确认基线的强度、是否有同参数量对比、是否进行了多次独立采样等实验控制信息。

## 6. 主要结论与发现

- **可靠性提升**：使用 SREF 生成的输出更可靠，12 个模型上平均改进 **16.01%**（相对基线）。
- **一致性提升**：已知事实的回答一致性平均提升 **15.10%**。
- **拒答能力改善**：模型能更好地识别不确定的事实，并适应性地选择承认不确定或拒答，而非强行作答产生幻觉。
- **方法论的价值**：熵与自我引用的组合提供了一种**不依赖额外外部知识证据**的轻量途径，可增强模型区别“已知识”和“未知识”的能力，从机制上缓解幻觉。

## 7. 优点与亮点

- **轻量、通用**：不依赖外部知识库或重训练，仅通过输入重构和推理期信息量计算即可实现，适用面广。
- **创新视角**：将模型的“自我引用”与信息论中的“熵”结合，显式建模“模型知道自己是否知道”，角度新颖，直接针对幻觉的根源问题。
- **机制可解释**：从熵和 KL 散度两个角度给出理论解释，不仅展示了效果，还说明了为何有效。
- **模型覆盖广**：在 12 个 LLM 上的验证使结论具有较强的泛化意义。

## 8. 不足与局限

- **信息不完整限制评估**：给定文本缺少数据集明细、任务类型、基线名称、具体数值表格、消融实验等信息，难以全面审视实验设计的完备性与公平性。
- **算力消耗可能被低估**：虽然无需训练，但需模型对每个问题多次改写、多次采样以估计熵，实际推理成本是普通解码的数倍，论文未进行成本-收益分析。
- **潜在偏差风险**：
  1. 熵阈值的选择是否对模型/数据集敏感、是否泛化到新领域未知；
  2. “改写”本身可能引入新的语义漂移，对于涉及复杂推理或多跳知识的问题是否依然有效未见讨论；
  3. 拒答策略对高风险场景虽有安全价值，但可能损害可用性（过度拒答），论文未报告精确率/召回率的权衡。
- **应用限制**：依赖模型自身分布输出的方法，对于校准性差（miscalibrated）的模型，熵信号可能失真，作用可能受限。

---

（完）
