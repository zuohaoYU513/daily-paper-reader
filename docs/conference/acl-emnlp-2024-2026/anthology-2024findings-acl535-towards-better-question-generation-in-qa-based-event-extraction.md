---
title: Towards Better Question Generation in QA-based Event Extraction
title_zh: 基于问答的事件抽取中的更好问题生成研究
authors: "Zijin Hong, Jian Liu"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.535.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 针对基于问答的事件抽取优化问题生成
tldr: 针对基于问答的事件抽取中问题质量不高、影响抽取精度的问题，作者提出四个问题质量评估准则，并设计强化学习方法RLQG，自动生成可泛化且依赖上下文的高质量问句。这些问句可为QA模型提供更清晰的事件信息定位指引，从而改善事件抽取准确率。研究显示问题生成质量是QA式事件抽取的关键瓶颈之一，为事件抽取提供了一种轻量有效的改进思路。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl535/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 762, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl535/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 769, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl535/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 731, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 768, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1570, \"height\": 1079, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 796, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 785, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 742, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 792, \"height\": 1027, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 778, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 731, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 805, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 753, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 729, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 738, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 784, \"height\": 2218, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl535/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 787, \"height\": 2353, \"label\": \"Table\"}]"
motivation: 基于问答的事件抽取中问题质量直接影响抽取准确率，但高质量、上下文相关的问题生成仍具挑战。
method: 提出四个问题质量准则，用RLQG强化学习生成可泛化、上下文相关的问题来训练QA模型完成事件抽取。
result: 验证所提规则与强化学习可生成更高质量问题，明显提升问答式事件抽取精度。
conclusion: 问题生成策略决定QA式事件抽取的上限，是提升事件论元与属性抽取效果的重要方向。
---

## Abstract
Event Extraction (EE) is an essential information extraction task that aims to extract event-related information from unstructured texts.The paradigm of this task has shifted from conventional classification-based methods to more contemporary question-answering-based (QA-based) approaches. However, in QA-based EE, the quality of the questions dramatically affects the extraction accuracy, and how to generate high-quality questions for QA-based EE remains a challenge. In this work, to tackle this challenge, we suggest four criteria to evaluate the quality of a question and propose a reinforcement learning method, RLQG, for QA-based EE that can generate generalizable, high-quality, and context-dependent questions and provides clear guidance to QA models. The extensive experiments conducted on ACE and RAMS datasets have strongly validated our approach’s effectiveness, which also demonstrates its robustness in scenarios with limited training data. The corresponding code of RLQG is released for further research.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与研究动机

**研究背景与问题**
- 事件抽取（Event Extraction, EE）旨在从非结构化文本中提取事件相关信息，是信息抽取的核心任务之一。
- 该任务范式已从传统的**基于分类的方法**转向**基于问答（QA-based）的方法**——即针对目标语义角色生成问题，再用问答模型从上下文中抽取答案作为事件论元。
- 然而，**问题质量直接影响抽取准确率**：低质量、模板化的问题会导致QA模型给出错误答案。作者通过预实验发现，即使使用GPT-4这样强大的商用模型，模板化问题仍会导致约60%的错误。

**核心研究问题**
- 什么是"好的问题"？
- 如何自动生成高质量、上下文相关、可泛化的问题，以有效引导QA模型完成事件抽取？

## 2. 方法论

### 2.1 提出四个问题质量评估准则

| 准则 | 含义 |
|------|------|
| **流畅性（Fluency）** | 问题应符合自然语言表达习惯，便于QA模型理解 |
| **可泛化性（Generalizability）** | 提问方法应适用于未见过的上下文和新角色，而非局限于训练数据 |
| **上下文依赖性（Context Dependence）** | 问题应与具体上下文一致，包含必要信息以便QA模型准确定位答案 |
| **对QA模型的指示性（Indicative Guidance）** | 问题应为QA模型提供清晰的定位指引，使其能够有效找到答案 |

### 2.2 核心框架：RLQG（Reinforcement Learning-based Question Generation）

整体方法包含三个模块，训练流程分为两阶段：

**阶段一：监督微调（SFT）生成初始问题**
- 使用序列到序列生成模型（以LLaMA-2-7b为基座）学习从"（角色，触发词，上下文）"到模板问题的映射。
- 输入格式：`role: [r'] ⊕ trigger: [t'] ⊕ context: [c']`，目标是模板问题如"WH is the [r'] in the [t'] event?"
- 训练损失为交叉熵损失。
- 使用**束搜索增强**为每个实例生成Top-N个候选问题，增加问题多样性。

**阶段二：强化学习（RL）精炼问题**

该阶段包含两个关键奖励机制：

1. **逆向提示奖励（Inverse Prompting Reward）**
   - 思路：好的问题应包含足够的上下文信息，使模型仅凭问题和触发词就能部分"恢复"原上下文。
   - 实现：训练一个逆向提示模型，输入 `trigger + question`，输出恢复后的简化上下文；再用语义相似度（SemSim）评估恢复上下文与原上下文的接近程度。

2. **问答奖励（Question Answering Reward）**
   - 思路：好的问题应能引导QA模型给出正确答案。
   - 实现：将候选问题输入QA模型获取预测答案，用上下文重叠率（COR，Context Overlap Ratio）计算预测答案与标准答案的匹配程度：
   - 公式：`COR(a, â) = |a ∩ â| / max(|a|, |â|)`

3. **奖励建模与PPO优化**
   - 综合得分：`Sq = λ1·SemSim(c, ĉ) + λ2·COR(a, â)`（λ1=0.3, λ2=0.7）。
   - 通过阈值条件筛选正/负问题对，构建偏好数据集。
   - 奖励模型损失：`LRM = -E[log(σ(r(p, q+) - r(p, q-)))]`。
   - 最终用PPO算法优化目标：`LRL = E[r(p, q)] - μ·E_KL(fRL | fSFT)`，即最大化奖励的同时，以KL散度正则化防止与初始模型偏离过远。

**最终测试阶段**
- 使用精炼后的问题生成模型为每个角色生成问题，然后使用现成的问答模型（LLaMA-2-13b-chat或GPT-4）生成答案，得到最终的事件论元抽取结果。

## 3. 实验设计

### 数据集与场景
- **ACE 2005**：33种事件类型、22种论元角色，599篇文档。评估分为两种设置：
  - *实用评估*：仅评估目标角色确有对应论元的可回答问题。
  - *完整评估*：评估ACE本体中所有可能角色对应的问题（包含不可回答问题）。
- **RAMS**：文档级事件论元抽取数据集，9,124个标注事件，139种事件类型、65种论元角色。
- **低资源（数据稀缺）场景**：在ACE上使用20%~100%不同比例的训练数据（仅20%~100%动态模板），验证模型在数据有限场景的性能。

### 评估指标
- **EM（精确匹配准确率）**：要求预测答案与标准答案完全一致。
- **COR（上下文覆盖率）**：基于词级重叠的比例。
- **SemSim（语义相似度）**：评估语义层级的响应质量。

### 对比基线（三组）
1. **模板方法**：Simple-Q（RCEE）、Standard-Q（EEQA）、Guideline-Q、Back-Trans-Q、Dynamic-Q（QGA-EE）。
2. **监督微调**：用上述模板为训练目标训练QGen模型，记为SFT(Template)。
3. **上下文学习**：LLaMA-2-13b-Chat和GPT-4的0-shot和5-shot设置。

## 4. 资源与算力

论文中**未明确说明GPU型号、数量与训练时长**，但提供了以下相关信息：
- 基座模型：QG模型用LLaMA-2-7b，QA模型用LLaMA-2-13b-Chat。
- 使用LoRA参数高效微调（可训练参数仅为全参数的0.0622%）。
- 超参数：SFT阶段学习率5e-5、3个epoch、batch size 16、梯度累积4步；RL阶段学习率1e-5、1个epoch、batch size 8。
- 附录验证了不同基座模型（ChatGLM-3-6b、Qwen-7b）和LLaMA-2不同规格（7b/13b、基座/Chat变体）上的表现。
- 以上信息表明测试了多种备选架构，说明作者对资源匹配有系统验证。

## 5. 实验数量与充分性评估

论文进行了**较为充分且成体系的实验**，主要包括：

| 实验类型 | 说明 | 结论 |
|---------|------|------|
| **主要结果（表2）** | ACE全量数据上的15+种方法对比 | 在EM/COR/SemSim上全面领先 |
| **主要结果（表3）** | RAMS上的5种方法对比 | 全面超过基线 |
| **低资源实验（图3）** | 数据量20%~100%变化 | 40%数据即达到此前方法全量数据的水平 |
| **起始模板消融（表4）** | 在Standard-Q基础上应用RLQG | 即使简单模板作为起点也明显优于SFT基线 |
| **奖励机制消融（表5）** | 移除IP/QA奖励 | 两个奖励均重要；QA奖励影响更大 |
| **QA架构消融（图4）** | 不同QA模型（LLaMA-13b-0shot/5shot、GPT-4-0shot/5shot） | RLQG方法泛化到不同QA模型 |
| **案例研究（表6）** | 定性展示不同问题生成的效果 | RLQG生成的问句与人工写作的最接近 |
| **逆向提示模型变体消融（附录A.2）** | 无SFT直接用LLM、5-shot代替SFT的IPM | SFT的IPM仍保持最佳 |
| **基座模型泛化（附录C）** | 在ChatGLM-3/6b、Qwen-7b上验证 | 均一致有效 |

**客观性评估**：
- 评估体系较完备：两组数据集、多种评估指标、多种QA模型、多种基座模型、数据稀缺实验齐全。
- 缺点/不足：验证实验基于test集而非dev集，且未报告多次运行的方差或统计显著性检验，可能有略微偏向方法的评测风险。
- 公平性关切：作者声称与"GPT-4 (5shot)"对比时，其中ChatGPT版本未明示于主文（附录补充GPT-3.5-turbo-1106和GPT-4-1106-preview），比较细节相对完整但有进一步提升透明度的空间。
- 整体判断：实验数量丰富、覆盖维度广泛，对提出的方法做了较充分的多角度验证。

## 6. 主要结论与发现

1. **问题质量决定QA式事件抽取的上限**：模板化问题即使配合GPT-4，仍产生大量错误，说明问题本身是重要瓶颈。
2. **RLQG框架显著提升抽取精度**：在ACE全量数据上，EM比最佳基线高2.08%，比模板方法高2.69%；在RAMS上比最佳基线高1.32%，比最佳模板高1.96%。
3. **低资源场景优势突出**：RLQG仅使用40%训练数据，就能达到此前基于模板方法使用100%数据的效果；这是因为强化学习机制能对候选问题排序，利用合成偏好信号提供额外监督，能够有效克服数据不足。
4. **问题生成的改进对QA模型无关**：不同QA模型下均一致提升，说明RLQG产生的是更通用的"好的问题"。
5. **两个奖励机制互补**：QA奖励贡献略大于逆向提示，说明指示性略有优先于上下文依赖性。

## 7. 主要优点

1. **问题导向清晰、定义明确**：提出四个可操作性强的质量指标，为QA式事件抽取中的研究提供了系统性分析框架。
2. **方法新颖且设计合理**：将"逆向提示"（通过问题找回上下文）用于衡量问题的上下文依赖度，这一思路设计巧妙——好的问题应当让模型仅凭问题即可大致还原出原始事件的场景信息。
3. **无需人工编写大量模板**：只需现有的简单模板为起点，通过强化学习即可自动精炼问题，减少人工干预和工作量。
4. **保证训练效率**：用现成的冻结QA模型（LLaMA-2-13b-Chat / GPT-4）做"评审"，避免训练额外QA模型带来的成本开销。
5. **有效性验证多维充分**：不同数据集、不同QA模型、不同基座、不同模板起点、低资源设置等多角度一致验证，并有代码开源。
6. **与LLM提示工程前沿接轨**：该方法可以理解为面向事件抽取场景的"自动提示词工程"，有一定跨任务启发价值——放之EE之外也有参考意义。
7. **在数据稀缺时使用合成信号（候选排序+偏好对构造）+PPO 融合，而非在原始监督数据上直接训练**，这种自监督/自举式的思路对低资源NLP场景具有参考意义。

## 8. 不足与局限

1. **对触发词已知的强假设**：本文沿用了先前工作的假设——触发词已知，忽略了触发词识别问题对整体性能的制约。作者在Limitations中承认这一点，但实际事件抽取中触发词往往未知，降低了方法的实用性。
2. **未做完整端到端EE评估**：由于需要将触发词作为输入，模型的推理流程需要管线式方法，会累积上游错误，与本领域最先进方法可能不能直接对齐比较。
3. **未见在更大更多样化真实数据上的验证**：仅在ACE 2005和RAMS两个标准数据集上评测，未见更多、更新的EE benchmark（如MAVEN、ERE等）的验证。模型的自举/偏好数据可能由模板或规律化文本驱动，难以反映多文档、高噪声真实业务场景下的性能，如Limitations所承认。
4. **答案长度与匹配度量选择对特征表现的影响**：文中主要使用EM和COR作为主要自动指标；QA模型输出长度变化（如生成长串而不是单个短语）会抬高COR分数，需要更多人工评估。
5. **资源与可重复性**：并未说明具体的GPU型号和资源消耗，也未说明偏好数据挑选比例与训练稳定性的详细敏感性分析，限制复现和部署参考价值。
6. **全面公平性存疑**：当对比GPT-4（5shot）时，不同阶段使用的prompt策略可能不完全一致；强化学习训练的奖励模型也可能存在偏好数据偏差风险，但作者没有提供具体出错模式的分析。
7. **偏好对质量可能影响模型上限**：在RL框架中，偏好数据集的来源是基座模板生成问题+SFT问题的合成信号与QA模型评价，若QA模型能力弱或语义相似度计算误差大，则错误评分可能在PPO中放大。文中未与人类偏好数据标注进行对比校准误差。

---

（完）
