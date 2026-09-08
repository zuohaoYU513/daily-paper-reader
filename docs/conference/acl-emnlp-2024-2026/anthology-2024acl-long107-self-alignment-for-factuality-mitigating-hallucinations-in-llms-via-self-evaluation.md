---
title: "Self-Alignment for Factuality: Mitigating Hallucinations in LLMs via Self-Evaluation"
title_zh: 面向事实性的自我对齐：通过自我评估缓解大语言模型幻觉
authors: "Xiaoying Zhang, Baolin Peng, Ye Tian, Jingyan Zhou, Lifeng Jin, Linfeng Song, Haitao Mi, Helen Meng"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.107.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 利用大模型自评估组件对自身生成回答只依赖内部知识进行真实性验证，并用该信号改善事实性。
tldr: 面向大模型即使掌握相关知识仍可能产生幻觉的问题，论文提出面向事实性的自我对齐方法。通过在生成回答后引入Self-Eval自评估组件，让模型仅基于自身内部知识判断生成结果是否属实，并以该自评信号训练模型，再配合Self-Knowledge Tuning增强模型自我评估能力。该方法减少了对人工事实标注的依赖，用自我评估帮助生成更可信的事实性回答。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long107/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 766, \"height\": 688, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long107/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1575, \"height\": 934, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long107/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1526, \"height\": 695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long107/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 750, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long107/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 765, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long107/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 766, \"height\": 577, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long107/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 751, \"height\": 572, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 787, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1605, \"height\": 645, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1649, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1622, \"height\": 686, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1632, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1629, \"height\": 673, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1624, \"height\": 905, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1640, \"height\": 584, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1620, \"height\": 1315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long107/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1632, \"height\": 2137, \"label\": \"Table\"}]"
motivation: 语言模型在已有相关知识时仍可能编造不实信息，而常用缓解手段需要昂贵的人工事实性标注。
method: 利用自评估组件要求模型用内部知识判断自己生成回答的事实性，并将自评信号与自我知识调优结合训练。
result: 实验显示，自评估信号能够指导模型利用已编码知识并提高回答事实性，降低幻觉倾向。
conclusion: 模型自我评估可作为一种无需人工标注的训练信号来提升事实性，增强模型对自身知识的运用。
---

## Abstract
Despite showing impressive abilities, large language models (LLMs) often struggle with factual inaccuracies, i.e., ”hallucinations”, even when they hold relevant knowledge. To mitigate these hallucinations, current approaches typically necessitate high-quality human factuality annotations. In this work, we explore Self-Alignment for Factuality, where we leverage the self-evaluation capability of an LLM to provide training signals that steer the model towards factuality. Specifically, we incorporate Self-Eval, a self-evaluation component, to prompt an LLM to validate the factuality of its own generated responses solely based on its internal knowledge. Additionally, we design Self-Knowledge Tuning (SK-Tuning) to augment the LLM’s self-evaluation ability by improving the model’s confidence estimation and calibration. We then utilize these self-annotated responses to fine-tune the model via Direct Preference Optimization algorithm. We show that the proposed self-alignment approach substantially enhances factual accuracy over Llama family models across three key knowledge-intensive tasks on TruthfulQA and BioGEN.

---

## 论文详细总结（自动生成）

# 《Self-Alignment for Factuality：通过自我评估缓解大语言模型幻觉》论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

### 背景与观察

- 大语言模型（LLMs）虽在多种 NLP 任务中表现出色，但一个显著痛点在于：**即使模型内部已编码了相关知识，在生成回答时仍可能输出与事实不符的内容，即"幻觉"（Hallucination）**。
- 论文聚焦于"knows yet fails to tell"这种特定类型的幻觉：模型存在"知"与"说"之间的鸿沟——同一问题，模型不同时刻采样可能产生正确和错误两种回答。
- 已有缓解方法通常依赖**高质量人工事实性标注**（例如 RLHF、针对事实性方向的表示编辑等），成本高昂且难以规模化。

### 核心问题

- **能否仅凭模型自身的内部知识与自评估能力，产生训练信号来引导模型走向事实性输出？** 即：不需要外部知识库、不需要人工标注，仅靠模型"自我评判"生成的内容是否真实，来构造偏好信号并微调模型。

### 整体含义

- 论文提出一种 **"Self-Alignment for Factuality"** 框架，用模型的**自评估能力**替代人类反馈作为奖励信号。
- 核心直觉：LLM 直接"生成"正确回答可能有困难，但在被问及"这个回答是否正确"时，它有能力基于自身内部知识**评估/识别出错误**（正如图 1 所示，模型能指出自己生成内容中的错误事实）。这种"评估比生成更容易"的现象，为训练信号提供了依据。

---

## 2. 方法论：核心思想、关键技术细节与算法流程

### 2.1 整体框架（三步流程）

以长文本生成（如写传记）为例，整体流程如图 2 所示：

#### Step 1：生成候选回答（Response Sampling）

- 对于给定 prompt x，从基础 LLM（policy π_ref）中采样 M 个候选回答 {y₁, …, y_M}（论文中 M = 30），使用 few-shot prompting 保证回答连贯相关。
- 温度分别取 T = 1、0.9、0.8。

#### Step 2：通过 Self-Eval 估计回答事实性（事实性标注/偏好标注）

- **针对长文本生成任务**，回答常混杂正确与错误信息。为精细评估：
  1. 用 GPT-3.5-turbo 将回答抽取为若干**原子声明（atomic claims）**，每条声明是独立的事实信息；
  2. 再用 GPT-3.5-turbo 将每条原子声明转化为对应的**原子问题（atomic question）**；
  3. 用 Self-Eval 评估每个（问题 q，声明 c）对的事实性得分 p(True | q, c)；
  4. 对所有声明的得分取平均，得到回答的最终事实性分数 Avg-p(True)。

- **针对短文本生成/MCQA 任务**：直接对回答/选项计算 p(True) 置信度。

#### Step 3：构造偏好数据并通过 DPO 对齐

- 根据事实性分数对所有候选回答排序，选择 top α 作为偏好回答（y_w），其余作为非偏好回答（y_l），构成偏好对集合 D = {(x, y_w, y_l)}。
- 用 **Direct Preference Optimization（DPO）** 算法微调模型，优化目标：

  L_θ = −E_{(x,y_w,y_l)∼D} [ log σ( β log(π_θ(y_w|x)/π_ref(y_w|x)) − β log(π_θ(y_l|x)/π_ref(y_l|x)) ) ]

- 其中 σ 是 logistic 函数，β 控制偏离参考策略的程度。

### 2.2 核心组件一：Self-Eval（事实性自我评估）

- 给定问题 q 和模型生成的回答 a，Self-Eval 的任务是基于模型内部知识评估回答的真伪，即估计概率 p(True | q, a) = f_M(q, a)。
- **Self-Eval-P(True)**：用 True/False QA 提示词实现。示例格式为：
  ```
  Instruction: Please evaluate the truthfulness of the proposed answer based on the given question and internal knowledge.
  <Few-shot Prompts>
  Question: <Question>
  Proposed Answer: <Answer>
  Is the proposed answer: A. True B. False
  The proposed answer is:
  ```
- 初步实验显示 Self-Eval-P(True) 存在**过度自信**问题（与 Tian et al., 2023b 的发现一致），据此设计 SK-Tuning 加以改进。

### 2.3 核心组件二：SK-Tuning（Self-Knowledge Tuning）

- 目的：增强 LLM 的**置信度估计与校准能力**，从而提高自我评估准确度。
- 训练数据构建（图 3）分两步：
  1. **采样候选答案并验证事实性**：对每个问题 q，用 few-shot prompting 采样 K 个候选答案；用 **Deberta-Large-MNLI** 做双向蕴含判断，与标准答案语义等价的标为"正确"（a_c），否则为"错误"（a_i）。
  2. **构建 True/False 训练样本**：将每个正确回答配正预测 R⁺（"A"），配负预测 R⁻（"B"）；错误回答则反之。保留重复项以近似模型对该问题的知识覆盖，改善置信度校准（附录 H 证实这一设计的必要性）。
- 训练目标采用**成对排序损失**：

  L_ϕ = −E_{(q,a,r⁺,r⁻)∼D_ψ}[ log σ( log π_ϕ(r⁺|q,a) − log π_ϕ(r⁻|q,a) ) ]

- 训练数据来自 **Wikipedia（49,862 个 prompt）+ BIG-bench 17 个 MCQA 任务（32,500 个 prompt）**，共 2,470,860 个训练样本。经 SK-Tuning 的 Self-Eval 记为 **Self-Eval-SKT**。

### 2.4 方法论要点总结

| 设计要素 | 说明 |
|---|---|
| 自评估信号 | 模型对自己生成内容给出 p(True)，作为奖励信号 |
| 无需人类标注 | 用模型内部知识 + Self-Eval 生成偏好标签 |
| 置信度校准 | SK-Tuning 通过异构任务训练提升评估能力 |
| 对齐算法 | DPO，直接优化偏好目标 |
| 长文本处理 | Claims 抽取 → 问题转化 → 逐条评估 → 取平均 |

---

## 3. 实验设计：数据集、基准与对比方法

### 3.1 数据集与评估场景

| 任务类型 | 数据集 | 评估指标 |
|---|---|---|
| 多选题问答（MCQA） | TruthfulQA | Accuracy |
| 短文本开放式生成 | TruthfulQA（生成版） | True（真实性）、Info（信息量）、True × Info |
| 长文本开放式生成 | BioGEN | FActScore、Respond Ratio、#Cor / #Incor（每回答准确/不准事实数） |

- BioGEN 测试集：100 个人物传记（训练 50、验证 33），prompt 由 GPT-4 生成（格式："Write a biography of <Entity>"）。

### 3.2 对比方法（Baselines）

- **SFT**：在人工标注的高质量训练集上监督微调。
- **ITI**（Inference-Time Intervention）：沿事实性方向编辑模型内部表示。
- **DoLA**（Decoding by Contrasting Layers）：对比不同层的输出分布来解码。
- **FACT-TUNE-MC**（Tian et al., 2023a）：用基于一致性的置信度标注偏好数据，再用 DPO 微调。
- **Self-Alignment 的消融/变体**：w/ Self-Eval-P(True) vs w/ Self-Eval-SKT；另外还引入 w/ SE（语义等价聚类）和 w/ USC（通用自一致性）两个变体来对比不同置信度估计方法的效果。

### 3.3 基座模型

- LLAMA-7B、LLAMA 2-7B（小规模、公开模型）。

### 3.4 辅助实验（用于深入分析 Self-Eval）

- 5 个 MCQA 数据集：TruthfulQA、CommonSenseQA、OpenBookQA（Closed）、MedQA（USMLE）、MMLU。
- 两个指标：**Accuracy**（正确答案在所有选项中取得最高置信度的概率）和 **AUROC**（正确 vs 随机错误答案的区分能力）。
- 对比对象：LLAMA 2-7B 基座直接生成 vs Self-Eval-P(True) vs Self-Eval-SKT。

---

## 4. 资源与算力

### 论文中明确提到的信息：

- **GPU**：8 × 32G Tesla V100。
- **SK-Tuning 微调**：1 个 epoch，batch size = 8，learning rate = 5 × 10⁻⁷。
- **DPO 对齐微调**：5 个 epochs，batch size = 8，learning rate = 5 × 10⁻⁶，β = 0.1。
- 训练数据规模：2,470,860 个 True/False 样本（SK-Tuning）；偏好数据由 30 个采样回答构造。

### 论文未明确说明的部分：

- 每阶段具体训练时长/小时数未透露；
- 推理阶段（GPT-3.5 抽取 claims、GPT-4 评估）的 API 调用总量未说明；
- 未提供端到端的整体算力开销估算。

---

## 5. 实验数量与充分性评估

### 实验组数量与维度

| 实验类型 | 数量/范围 | 目的 |
|---|---|---|
| 主实验（3 类任务 × 2 个基座模型） | TruthfulQA-MC、TruthfulQA-Gen、BioGEN | 验证整体方法有效性 |
| 变体对比实验 | Self-Eval-P(True) vs Self-Eval-SKT vs SE vs USC | 验证 SK-Tuning 与不同置信度估计方法的优劣 |
| 置信度估计分析 | 5 个 MCQA 数据集上 Accuracy + AUROC | 剖析 Self-Eval 有效性的内在原因 |
| 成对评估（人类/AI 评判） | BioGEN 100 个传记 × 4 维度（GPT-4 评判） | 验证生成质量的综合提升 |
| 校准曲线分析 | CommonSenseQA 上 ECE 风格的 calibration curve | 检验置信度校准效果 |
| 定性/个案分析 | TruthfulQA 错误类型分类、BioGEN 示例 | 分析残余错误类型 |
| 消融实验（附录 H） | 移除重复样本前后校准对比 | 验证训练样本设计合理性 |

### 充分性评价

- **优点**：任务覆盖较全面（选择、短文本、长文本三种范式），在两个模型上均验证；每个结果报告三次运行均值，增加稳定性。
- **不足/可提升空间**：
  - 仅用 7B 规模 LLAMA 模型，未在更大模型（13B、70B）或 RLHF 模型上验证；
  - 数据集类型有限（TruthfulQA 偏"误导性常识"，BioGEN 偏传记生成），未涉及医疗、法律、金融等真实应用场景；
  - 对比方法中，ITI 等是基于域内标注数据的方法，在这种任务设定下并不完全公平（不过论文在表注中说明部分结果直接引用原文），且标注数据量小，跨方法比较仍有基准不一致风险；
  - 表 1 中 ITI 和 DoLA 的部分结果引用自原论文而非同条件复现，存在实验环境不可比的可能；
  - 长文本生成中用 GPT-3.5 抽取 claims、用 GPT-4 做评估，这些辅助模型的错误会向评估结果传播。

---

## 6. 主要结论与发现

### 6.1 方法有效性的核心指标提升

| 模型 | 任务/指标 | 基座模型原值 | Self-Alignment（Self-Eval-SKT） |
|---|---|---|---|
| LLAMA-7B | TruthfulQA MC Accuracy | 25.60 | **45.48**（↑约 20 个点） |
| LLAMA-7B | True × Info | 26.90 | **45.75** |
| LLAMA 2-7B | TruthfulQA MC Accuracy | 28.90 | **44.10** |
| LLAMA 2-7B | True × Info | 39.04 | **53.42** |
| LLAMA 2-7B | BioGEN FActScore | 40.54 | **46.50** |
| LLAMA-7B | BioGEN FActScore | 30.72 | **38.28** |

### 6.2 具体发现

1. **自我对齐可显著缓解幻觉**：仅用模型内部知识作为训练信号，三任务上事实性均大幅提升。
2. **SK-Tuning 是关键**：w/ Self-Eval-SKT 在 True×Info 上超过 w/ Self-Eval-P(True) 约 12%，在 BioGEN FActScore 上超过约 4%。原因在于 SK-Tuning 改善了置信度校准，显著抑制了过度自信。
3. **Self-Eval-SKT 优于一致性置信度**：Self-Eval-SKT 显著超越 FACT-TUNE-MC（基于采样一致性估计置信度，依赖生成能力），表明"评估"比"多次重新生成后聚类"更贴近内部知识。
4. **自我对齐优于表示编辑方法**：如 ITI 和 DoLA 需要域内标注数据且泛化有限，自我对齐在综合指标（True×Info）上表现更佳。
5. **事实性评估比事实性生成容易且更可靠**：在 5 个 MCQA 数据集上，Self-Eval-SKT 的评估准确率显著高于模型直接

生成高质量回答更有优势；同时自我评估的置信度与真实正确性之间的一致性（AUROC）也显著更高，验证了“知识内化但表达不可靠”假设下自评估信号的有效性。

---

## 7. 进一步讨论与内部分析

### 7.1 幻觉削减的动力来源

- 通过 DPO 的偏好优化，模型被正向强化于“基于内部知识生成的、能被自评估确认为正确的回答”，同时被负向抑制于“自评估认定为事实错误但模型仍可能输出的回答”。
- 该方法本质上是**将评估能力“反向传播”到生成策略**，构造了一个无需外部知识库的闭环自我修正机制，使模型在解码阶段更倾向于选择与内部知识一致的输出。

### 7.2 为什么“评估”比“生成”更容易

- 生成任务需要模型从前瞻性的、开放的词汇空间中规划完整表达；而评估任务仅需在给定答案基础上做验证判断，是局部性、判别式的认知任务，对模型的要求更接近其预训练目标（如下一句预测任务中对合理性的隐式判断）。

### 7.3 候选生成采样的作用

- 高温采样（T = 1、0.9、0.8）引入多样性，能够产生包含正确与错误答案的对比样本，进而暴露模型内部真实的知识分布边界。这种从“自身采样”获得的偏好对比数据，比外部知识库或者人工标注更能反映模型固有的知识盲区与表达偏差。

---

## 8. 局限性与潜在风险

### 8.1 技术层面局限

- 自评估信号并非完全可靠，当模型对某些主题存在系统性知识缺失或错误时，自我评估依然可能“自信地犯错”，此时整个偏好信号会被错误引导，导致错误被进一步固化。
- 长文本生成时需要额外的文本拆解和问题转化流程，其准确性受辅助模型影响，可能引入级联误差。

### 8.2 任务与规模局限

- 论文只在 7B 级别模型上验证，无法判断方法在更大模型上的表现是否同样显著；模型规模增大后，自评估能力与生成能力之间的差距可能缩小，自我对齐的增益或许会减弱。
- 任务类型上侧重于百科常识与传记类事实，对需要实时知识或专业领域知识的场景覆盖有限。

### 8.3 评估体系局限

- 对“真实性”的度量依赖人工设计或 GPT-4 辅助评估，主观性和模型偏见难以完全排除；
- 事实性提升是否以牺牲风格、流畅性或推理能力为代价，论文仅通过少量附加指标（如 Info）做了有限缓解，并未对所有能力维度做系统评测。

---

## 9. 总结性评价与关键启示

### 9.1 学术贡献

- 首次系统地展示了“自评估信号—偏好数据构造—DPO 对齐”的完整闭环可用于缓解幻觉，无需人类标注；
- 引入 Self-Eval 与 SK-Tuning 概念，在置信度校准层面推进了对“LLM 能否自我判断真伪”这一问题的理解，为后续利用模型自省能力提供了可行的训练方案。

### 9.2 实际应用启示

- 该方法适用于无监督/弱监督条件下的大模型事实性优化，具有较强的可迁移性——在垂直领域或新语种场景中，只要能够采样、能够自评，就可以迭代优化，减少对昂贵人工反馈的依赖。

### 9.3 开放性思考

- 如果将自我评估能力扩展到更细粒度（如句子级甚至短语级）并逐步反馈至解码阶段，有可能实现推理时即时的幻觉抑制；
- 自我对齐若与外部检索或工具调用结合，可形成“自知 + 外查”双层事实保障机制，弥补纯内部知识驱动的局限。

---

## 10. 关键术语速查表

| 术语 | 含义 |
|---|---|
| Self-Alignment | 用模型自身评估结果构造对齐信号并微调的过程 |
| Self-Eval | 模型对给定问答对进行真伪判断并输出概率的模块 |
| SK-Tuning | 在异构 QA 与 MCQA 任务上通过成对排序损失微调，提升自评估置信度校准 |
| DPO | Direct Preference Optimization，直接基于偏好对优化策略模型的对齐方法 |
| Atomic Claim / Question | 长文本被拆成的独立事实性断言及其问题化形式 |
| FActScore | 长文本逐句事实性准确率的评估指标 |
| True × Info | 真实性（True）与信息量（Info）的综合指标，防止模型靠“避答”刷真实性 |
| AUROC | 用于衡量自评估区分正确与错误答案能力的指标 |

---

# 结语

该论文的核心价值在于提出了一种完全摆脱人工标注的幻觉缓解路径，用“自我评估”替代“人类反馈”，将评估与生成之间的能力不对称转化为模型自我优化的动力。虽然目前实验规模与任务覆盖仍有限，但其方法论构想——让模型在“自知之明”中自我纠偏——为构建更可靠、可自我进化的大语言模型提供了重要思路。

（完）
