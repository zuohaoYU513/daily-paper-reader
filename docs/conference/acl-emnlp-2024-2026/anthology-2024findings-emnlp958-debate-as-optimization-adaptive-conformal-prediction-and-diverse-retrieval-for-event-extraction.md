---
title: "Debate as Optimization: Adaptive Conformal Prediction and Diverse Retrieval for Event Extraction"
title_zh: 辩论即优化：事件抽取的自适应共形预测与多样检索
authors: "Sijia Wang, Lifu Huang"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.958.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 面向事件抽取的多智能体辩论与多样检索作为证据支撑，并用自适应共形预测拒绝低置信答案
tldr: 免调参的LLM事件抽取与监督方法仍有明显差距，且输出可靠性不足。本文提出多智能体辩论优化系统DAO，其中Diverse-RAG模块系统检索适合讨论的支持信息，自适应共形预测模块拒绝低可行答案。在ACE05等基准上，该方法显著缩小了免调参方法同监督方法的差距，为证据支撑下的可靠事件抽取提供了可用方案。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp958/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1611, \"height\": 901, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp958/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 448, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp958/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1326, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp958/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 656, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp958/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1637, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp958/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1638, \"height\": 465, \"label\": \"Table\"}]"
motivation: 免调参LLM事件抽取与监督方法差距较大，需要更可靠的证据支撑和输出选择。
method: 以多智能体辩论迭代优化抽取输出，加入多样检索模块提供支撑信息，并引入自适应共形预测拒绝不可靠答案。
result: 在ACE05等基准上大幅缩小了与监督方法的性能差距。
conclusion: 无需参数训练的检索增强辩论能够提升事件抽取准确性与可靠性。
---

## Abstract
We propose a multi-agent debate as optimization (DAO) system for event extraction, where the primary objective is to iteratively refine the large language models (LLMs) outputs through debating without parameter tuning. In DAO, we introduce two novel modules: the Diverse-RAG (DRAG) module and the Adaptive Conformal Prediction (AdaCP) module. DRAG systematically retrieves supporting information that best fits the debate discussion, while AdaCP enhances the accuracy and reliability of event extraction by effectively rejecting less promising answers. Experimental results demonstrate a significant reduction in the performance gap between supervised approaches and tuning-free LLM-based methods by 18.1% and 17.8% on ACE05 and 17.9% and 15.2% on CASIE for event detection and argument extraction respectively.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究背景**：事件抽取（EE）旨在识别文本中的事件提及（触发词）和事件论元（参与者等）。该任务传统上由监督学习方法占据优势，但这些方法需要大规模标注数据；而大型语言模型（LLM）虽具备通用语言理解能力，在无需微调的设置下，其事件抽取性能与监督方法之间存在显著差距。
- **核心问题**：论文聚焦于三个关键挑战：
  - 事件提及本身具有歧义性和多变性（如"pay the fines"既是Transfer-Money也可能是Fine事件，触发词是"pay"还是"fines"存在歧义）。
  - 现有方法未能有效利用领域知识（如复杂的事件模式/本体定义），简单将模式列举进prompt并不能让LLM充分理解。
  - LLM难以利用已标注数据（尤其是在无法获取模型checkpoint的情况下）进行参数微调。
- **整体含义**：论文提出**DAO（Debate as Optimization，辩论即优化）系统**，核心观点是：通过多智能体之间的对抗性辩论，可以在**无需参数微调**的前提下，将事件抽取的答案逐步优化，从而大幅缩小与监督方法之间的性能差距。

## 2. 论文提出的方法论

### 核心思想
将LLM-based事件抽取视为一个迭代优化的过程：多个LLM智能体通过有结构的多轮辩论，结合动态检索的领域知识和自适应拒绝阈值，不断修正初始答案——**辩论即一种对"答案"进行逐步优化的过程**。

### 技术细节

**（1）多智能体辩论框架（四类角色）**
其框架包括四类角色，每轮辩论由四个阶段组成：初始意见形成、事件信息检索、交叉质询、判断。流程中每轮需要通过法官判定是否已达成一致或达到最大轮数（本文上限为3轮）才能结束。若检测到事件，则进入论元抽取辩论；否则跳过。详细描述：
- **Debaters（辩手）**：针对给定句子生成初始观点，并在看到检索信息后为自己的答案辩护或调整。
- **Critic（评论家）**：专门负责发现辩手潜在错误（其prompt中融入了常见EE错误提示）。
- **Judge（法官）**：判定各辩手是否达成共识，若无共识则要求继续辩论。
- **Summarizer（摘要器）**：汇总被共同认可的方案，形成最终答案。
- 角色间的对抗/合作交互构成了一个"质疑-辩护-修正"的循环。

**（2）Diverse-RAG（DRAG）模块**
DRAG的核心是动态检索最适合当前争论焦点的支撑信息，其设计围绕四个原则：

- **距离（Distance）**：使用语义编码器对句子和参考文本编码，选择Top-K（K=128）语义最相似的数据条目。
- **多样性（Diversity）**：为解决Top-K中信息冗余问题（如过长的相同实体会抬高相似度），引入**聚类**操作（公式为聚类距离约束），确保相似样本被去重，且每个簇只能选一个数据点，最终挑选来自M个不同簇的最接近数据。
- **极性（Polarity）**：同时考虑正例（实际触发事件）和负例（含歧义词但未触发事件），提高判别能力。
- **自适应（Adaption）**：将辩论比作由粗到细的优化过程——检索随辩论进行而从"广泛"转为"精细"。用聚类半径的衰减来实现：`μ_t = λ * μ_{t−1}`（λ为半径衰减因子），即聚类逐渐收紧、检索更加精准。

**（3）Adaptive Conformal Prediction（AdaCP）模块**
- 该模块的定位与实现方式是：利用conformal prediction理论，以校准集计算非一致性风险分数并求得阈值，然后在推理阶段拒绝超过阈值的低置信度答案。与传统”合格预测“不同，AdaCP会随着辩论推进不断动态调整阈值。
- 校准集上计算初始阈值：`q̂_0 = Quantile({r_1, ..., r_n}, ⌈(n+1)(1−δ)⌉ / n)`，初值在ED中设为1、EAE中设为3。
- 动态更新：随着检索信息增多，模型对正确答案更自信，因此阈值按衰减系数`β`逐步收紧，即`q̂_t = β × q̂_{t−1}`（β=0.5）。
- 这样可以**在辩论早期允许广泛的候选答案**，在辩论后期（大量证据出现后）拒绝不合适的答案，提高精度和可靠性。

### 算法流程总结（文字版）
1. 辩手初始输出（设置不同temperature或使用不同LLM，保证观点多样性）。
2. 检索事件定义（仅针对辩手提及的事件类型）以及DRAG检索的示例，分发给除法官外的所有智能体。
3. 所有提交的意见经AdaCP验证，未通过（R(x,y) > q̂）的答案被拒绝；通过者进入交叉质询阶段。
4. 辩手进行相互辩论，Critic给出评论意见。
5. Judge检查是否达成一致，若未达成且轮数未达上限则返回步骤2开始新一轮。
6. 达到条件后由Summarizer整理最终答案（或跳转到论元抽取辩论）。

## 3. 实验设计

### 数据集/Benchmark
- **ACE05-E（ACE05）**：最经典的事件抽取英文数据集，报告了ED（事件检测）、EAE（给定触发词的论元抽取）、EE（联合抽取）三项结果。
- **CASIE**：网络安全领域的事件抽取数据集，同样评估ED、EAE和EE三方面。
- 评估指标采用F1值（ACE05用Exact Match和Argument Head F1，CASIE用types metric），与既有文献保持一致。

### 对比方法
- **监督微调方法（SFT）**：DEGREE、InstructUIE、RexUIE（较小规模的PLM基座）。
- **零次学习（ZS）**：ChatGPT-14、G-PTLM、CODE4STRUCT、ChatIE等。
- **上下文学习（ICL）**：ChatGPT-IE（ICL-5）、Code4UIE（ICL-10）。

### 系统自身配置
- 两种引擎设置对比：(a) Gemini-GPT；(b) Llama3-GPT，分别配置不同的辩手/评论家/法官。
- 全部智能体temperature设为0（保证复现性）；校准模型为Flan-t5-xxl。

## 4. 资源与算力

- 论文明确提到使用了**1块 NVIDIA A40 GPU**运行所有实验。
- 文中称每句话平均推理时间约**10秒**，每句成本不到**$0.01**（视API成本而定），声称成本介于小型微调模型和LLM ICL方法之间，这种增量是对免调参/可适配性的权衡。
- **需要指出**：论文未披露校准模型运行耗时、具体API调用次数、完整的GPU训练时长等细节。因为其所有LLM均免调参，总体算力消耗低于传统SFT方案。

## 5. 实验数量与充分性

### 实验组数概览
- **主实验**：2个数据集（ACE05、CASIE）× 3个子任务（ED/EAE/EE）× 2种引擎配置，外加多个基线系统对比。
- **消融实验**：在ACE05上进行了4组：(1) 无re-clustering；(2) 无完整DRAG检索；(3) 无AdaCP；(4) 无DRAG和AdaCP（退化为基础辩论系统）。
- **案例分析**：随机抽取40个推理样本分析Critic影响（其中15%的trigger答案被Critic修正）；另有表格呈现DRAG和AdaCP的纠错/拒错案例（含失败案例）。

### 充分性与客观性分析
- **优点**：主实验和消融实验结构清晰，能较好反映各模块的独立贡献；多种LLM基座配置（GPT、Gemini、Llama3）提高了结果的可泛化性。
- **不足**：
  - 消融实验仅在一个数据集上进行，未涉及CASIE中的消融，难以判断模块在新领域（如网络安全）中的各自贡献。
  - 随机抽样的案例分析规模较小（仅40条），统计显著性未作检验。
  - 一些基线（如ChatGPT-IE）使用的是ICL-5，而主系统使用ICL-10（带*标记），对比上的sample budget并不完全一致，可能略微影响公平性。
  - 论文也承认，虽然与监督方法差距缩小，但仍未完全超越SFT方法（DEGREE等在多个指标上仍占据优势）。

## 6. 论文的主要结论与发现

- 多智能体辩论+检索增强+自适应拒绝的免调参方法能够显著提升事件抽取性能，与SFT方法之间的性能差距大幅缩小（**在ACE05上差距缩小18.1%和17.8%，在CASIE上缩小17.9%和15.2%**，分别对应ED和EAE）。
- 在CASIE上，相对于Code4UIE基线，ED获得绝对+19.9%的F1提升。
- DRAG模块和AdaCP模块各自都有显著贡献；其中**Critic在交叉质询阶段的作用尤为明显**，能有效纠正辩手的错误输出。
- 风险分布可视化验证了优化过程中模型对正确答案信心逐步提升（风险值分布向低值偏移），为"辩论即优化"论点提供了直接证据。

## 7. 优点

- **概念创新**：将多智能体辩论形式化地看作一个**优化过程**，将多个模块统合起来解决信息抽取中的认知不确定性问题，视角新颖。
- **模块设计精细**：
  - DRAG的四个"检索原则"（距离、多样性、极性、自适应）不是简单堆砌，而是针对辩论过程中"如何利用证据"做了系统建模，尤其是聚类半径随时间衰减的设计颇具启发性——与"粗检索→细检索"的直觉一致。
  - AdaCP利用共形预测理论，实现了动态、可解释的拒绝机制，而不是使用简单固定的阈值，具有统计学意义。
- **适应性强**：无需微调即可适配新领域或新本体，在小数据/零标注条件下有潜在的应用价值。
- **分析细致**：除性能数字外，还提供了风险分布演化、案例研究和长span问题的深入讨论，体现了作者对评估方法本身局限性的自觉。

## 8. 不足与局限

- **成本和效率问题**：每句平均10秒、$0.01的推理成本明显高于单次ICL或小型PLM方法，不适合大规模实时处理场景。论文虽将其视为"适应性"的代价，但仍会在实际应用中构成阻碍。
- **性能局限**：即便大幅缩小差距，整体上仍不及最强SFT基线；在ACE05的某些EAE/EE指标上与SFT方法的差距依然明显（例如ACE05 ED上的50.2 vs. 77.1的InstructUIE）。
- **丢失细节评估**：作者指出现有基于head token的论元评价标准无法充分反映LLM的长参数span能力。这意味着系统在"全span"上的真实性能可能被低估，但也提示相关的评估体系需要进一步改造。
- **生成偏差**：GPT和Llama3倾向于生成比标注更长的span，影响最终提取精度，这在当前的评价标准下客观拉低了系统得分。这既暴露模型本身的行为特性，也暴露标注标准与LLM自然输出间的错位。
- **泛化验证不足**：消融实验覆盖不足（仅单数据集），且只涉及英语数据集，未在ERE、更多领域或非英语数据上验证系统的泛化性。
- **可解释性与控制性**：辩论是开放式的对话过程，虽然设计了Judge和结构化输出，但对中间结果的纳入/更新缺乏严格的可解释机制，结果可能受prompt影响；系统的"收敛"更多依赖最大轮数约束，而非语义层面的真正趋同。

（完）
