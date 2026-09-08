---
title: Confidence Improves Self-Consistency in LLMs
title_zh: 置信度提升大语言模型的自一致性
authors: "Amir Taubenfeld, Tom Sheffer, Eran Ofek, Amir Feder, Ariel Goldstein, Zorik Gekhman, Gal Yona"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1030.pdf"
tags: ["query:metacognitio"]
score: 4.0
evidence: 利用模型自身置信度加权自一致性解码路径，与自我评估回答质量有关联但非核心
tldr: "本文针对自一致性解码需采样大量推理路径而计算开销过高的问题，提出置信度引导的自一致性（CISC）。CISC利用模型给出的置信度对各采样路径进行加权投票，优先采纳高置信度路径。在九个模型和四个数据集上，CISC几乎全部优于标准自一致性，所需推理路径减少超过40%。这显示了模型置信度对改善自一致决策的价值。"
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1030/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 754, \"height\": 723, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1030/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1636, \"height\": 565, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1030/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1030/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 793, \"height\": 152, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1030/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1030/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1637, \"height\": 1627, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1030/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1638, \"height\": 1626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl1030/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 719, \"height\": 923, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1207, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 758, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1558, \"height\": 328, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1606, \"height\": 1366, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 966, \"height\": 440, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1419, \"height\": 973, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1503, \"height\": 693, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1217, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 881, \"height\": 605, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1610, \"height\": 1471, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl1030/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1533, \"height\": 874, \"label\": \"Table\"}]"
motivation: 自一致性解码采样多条长推理路径开销巨大，需要减少样本量同时保持准确率。
method: 将模型置信度作为权重对多条推理路径进行加权多数投票，形成CISC算法。
result: "在九个模型和四个数据集上，CISC所需路径数减少40%以上且性能更优。"
conclusion: 模型置信度可以有效提升自一致性解码的效率与答案选择可靠性。
---

## Abstract
Self-consistency decoding enhances LLMs’ performance on reasoning tasks by sampling diverse reasoning paths and selecting the most frequent answer. However, it is computationally expensive, as sampling many of these (lengthy) paths is required to increase the chances that the correct answer emerges as the most frequent one. To address this, we introduce Confidence-Informed Self-Consistency (CISC). CISC performs a weighted majority vote based on confidence scores obtained directly from the model. By prioritizing high-confidence paths, it can identify the correct answer with a significantly smaller sample size. When tested on nine models and four datasets, CISC outperforms self-consistency in nearly all configurations, reducing the required number of reasoning paths by over 40% on average. In addition, we introduce the notion of within-question confidence evaluation, after showing that standard evaluation methods are poor predictors of success in distinguishing correct and incorrect answers to the same question. In fact, the most calibrated confidence method proved to be the least effective for CISC. Lastly, beyond these practical implications, our results and analyses show that LLMs can effectively judge the correctness of their own outputs, contributing to the ongoing debate on this topic.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：自一致性（Self-Consistency, SC）解码通过采样多条推理路径并选取出现频率最高的答案，能显著提升大语言模型（LLM）在推理任务上的表现。但其主要瓶颈是计算成本高昂——为了增加正确答案成为多数答案的概率，必须采样大量（长）推理路径。
- **核心问题**：能否在不显著牺牲准确率的前提下，减少自一致性解码所需的采样数量，从而降低计算开销？
- **整体含义**：论文提出利用LLM对自身推理路径的置信度评估（self-assessment）来加权投票，使高置信度路径在最终答案选择中占据更大权重；这不仅提升了解码效率，也为“LLM能否判断自身输出正确性”这一争议性话题提供了实证支持。

## 2. 论文提出的方法论：核心思想、关键技术细节与算法流程

- **方法名称**：Confidence-Informed Self-Consistency（CISC，置信度引导的自一致性）。
- **核心思想**：标准自一致性只统计答案的频次（多数投票）；CISC在投票前先为每条采样路径生成一个模型自评置信度分数，然后用该分数进行加权多数投票。高置信度路径的权重更大，低置信度路径的贡献被抑制，从而在更少样本下收敛到正确答案。

- **算法流程（分为四步）**：
  1. **采样多条推理路径**：给定问题 \(q\) ，从模型中采样 \(m\) 组响应 \((r_i, a_i)\)，其中 \(r_i\) 为推理链，\(a_i\) 为最终答案。
  2. **置信度提取**：为每条路径计算一个置信度 \(c_i\)。论文比较了三种置信度方法：
     - **Response Probability**：使用整条响应（推理链+答案）的长度归一化生成概率作为置信度。
     - **Verbal Confidence**：在生成答案后，拼接一个提示（如“请用0-100评分”），让模型用文本输出置信度；有“二值（0/1）”和“0-100”两个变体。
     - **P(True)**：使用二值提示，取模型分配给token“1”的概率作为置信度。这是最终表现最好的方法。
  3. **置信度归一化**：用带温度 \(T\) 的 softmax 将置信度归一化为权重：
     \[
     \tilde{c}_i = \frac{\exp(c_i / T)}{\sum_{j=1}^m \exp(c_j / T)}
     \]
     温度 \(T\to\infty\) 时权重趋于均匀，CISC退化为标准自一致性；\(T\to 0\) 时趋于只选择最高置信度的路径。
  4. **加权多数投票**：最终答案选择为：
     \[
     \hat{a}_{\text{CISC}}=\arg\max_a \sum_{i=1}^m \mathbb{1}[a_i=a]\cdot \tilde{c}_i
     \]

- **高效的置信度提示设计**：采用两步提示机制——先用原问题生成推理链和答案，再拼接一个极短的置信度提取提示（约20个token）并继续生成。由于前缀（问题+推理链+答案）不变，可通过KV缓存复用避免重算，因此置信度提取的额外计算开销可忽略（仅需编码20个token并生成1个token）。

## 3. 实验设计：数据集、基准与对比方法

- **数据集**（四个广泛使用的推理基准）：
  - **GSM8K**：小学数学应用题，完整验证集1320题。
  - **MATH**：更具挑战性的数学题，完整测试集5K题。
  - **MMLU-Pro**：MMLU的加强版，覆盖科学、历史等多领域知识与推理，随机采样5K题。
  - **Big-Bench-Hard**：从23个子任务中选取20个（排除需要特殊答案提取方法的3个），共5761个例子。

- **模型**（三个家族共9个指令微调的开源模型）：
  - **Gemma2**：2B、9B、27B。
  - **Qwen2.5**：3B、14B、72B。
  - **Mistral系列**：Ministral-8B、Mistral-Small-22B、Mistral-Large-123B。

- **对比方法**：
  - 标准自一致性（Self-Consistency, SC）：等权多数投票。
  - CISC的三种置信度变体：Verbal Binary、Verbal 0-100、Response Probability、P(True)。
  - 消融实验中还对比了：
    - 无归一化的CISC；
    - Softmax T=1（不调温度）的CISC；
    - Max方法（直接选择最高置信度的答案）；
    - Tie方法（仅在SC平局时用置信度破局）。

- **评估指标**：
  - **Cost Reduction（成本降低百分比）**：固定CISC预算（5或10条路径），计算标准SC需要多少条路径才能达到同等精度。
  - **Accuracy Improvement（准确率相对提升）**：两者采用相同路径数量时，CISC相对SC的准确率提升比例。

## 4. 资源与算力

- 论文未提供精确的GPU型号数量、总训练/推理时长等明细，仅粗略说明：
  - 每个模型约生成50万条响应（17,000个问题，每问30条采样）。
  - 作为参考，使用Gemma2-2B（1K token上下文）推理时，约需“100 Nvidia H100 GPU小时”的数量级（原文为“an order of 100 Nvidia H100 GPU hours”），这是一个粗略量级而非精确数字。
  - 温度调参在10%留出集上进行网格搜索（80个值），只需几分钟桌面计算，无需重新运行LLM。

- 整体而言，论文对算力花费的描述是粗略的，没有给出端到端总成本或各模型的具体资源清单。

## 5. 实验数量与充分性

- **实验规模较大**：9个模型 × 4个数据集 × 5~6种置信度/变体方法构成矩阵式实验；每种配置下对每道题采样最多30条路径，并通过bootstrap（n=500次重采样）估计不同预算下的性能，降低了随机性影响。
- **统计显著性**：提供了micro-averaged的置信区间（95%），表明各置信度方法的准确率提升均具有较强统计显著性。
- **消融实验丰富**：
  - 去掉置信度归一化 vs Softmax归一化（固定温度 vs 调温）；
  - Max和Tie的简化替代方案；
  - 温度缩放对不同置信度方法的影响；
- **人类评估**：对90条采样路径进行人工标注，检查模型低置信度回答与人类识别出的低质量推理模式之间的一致性。

- **充分性评价**：
  - **优点**：覆盖面广（模型家族、规模、任务类型均有代表性），指标设计能直接体现“效率+精度”的双重目标，bootstrap与置信区间使结果更可靠。
  - **不足**：所有模型均为开源的指令微调模型（未含闭源前沿模型如GPT-4级别）；实验聚焦于数学与常识推理，未覆盖代码、开放生成或规划任务；置信度提取使用的是零样本提示，没有探索少样本或训练式置信度方法；人类评估仅基于MMLU-Pro单一数据集且样本量较小。

## 6. 论文的主要结论与发现

- **CISC在几乎所有配置下优于标准自一致性**：无论使用哪种置信度提取方法，CISC都能在相同或更少的采样数量下获得更高准确率。
- **P(True) 是最优置信度方法**：在5和10条路径的预算下，P(True)平均能减少约41%和46%的计算成本（即SC平均需要8.4条和18.6条路径才能达到CISC仅用5条和10条路径的准确率）。部分场景节省超过67%。
- **置信度归一化很重要**：带调温softmax的归一化能显著提升性能；若不调温（T=1）甚至可能出现负收益。
- **传统置信度评估指标不适用于CISC**：最“校准”（ECE/Brier最优）的Verbal方法在CISC中表现最差；论文据此提出**Within-Question Discrimination（WQD）**指标，衡量同一问题内部正确/错误回答的区分能力。WQD能完美预测CISC的性能排序，而传统跨问题指标不能。
- **模型置信度与推理路径质量高度相关**：WQD随置信度差距单调增长，表明模型对同一问题的不同答案存在精细的自评估能力。
- **人类评估佐证**：67%的模型低置信度回答被人为判断存在低质量推理模式，而高置信度回答中该比例仅33%。其中“最终答案不在选项中”和“计算不完整”两类低质量模式与模型低置信度强相关。
- **对LLM自我评估能力的争论做出贡献**：作者从效率收益、WQD和人类一致性三方面提供证据，支持“LLM能较好判断自身回答正确性”的正面观点。

## 7. 优点：方法或实验设计上的亮点

- **方法简单且即插即用**：CISC是对标准自一致性的最小改动——只需多一个极短的置信度提示和加权投票，无需重新生成推理链，利用KV缓存可以忽略额外开销，完全保留并行采样的优势（吞吐量和延迟不变）。
- **计算成本度量清晰**：通过“成本降低百分比”指标直观说明了使用CISC的收益，并将效率和精度统一考量，避免只报精度的片面性。
- **归一化与温度控制设计合理**：将置信度归一化与温度参数结合，使CISC包含标准SC（T→∞）为特例，有明确的公式化行为解释；调温只需一份10%留出集，过程轻量。
- **提出“题内置信度评估”的视角**：区分了跨问题校准能力与同问题区分能力，指出传统指标（ECE/Brier）的误导性，并给出可计算的新指标WQD，这是方法论上的重要贡献。
- **实验验证充分**：9模型×4数据集×多种置信度方法的大规模对比，加上bootstrap置信区间、多个消融和人类评估，证据层次丰富。
- **对争论点的实证贡献**：通过多种路径（效率红利、WQD单调性、人类一致性）系统论证LLM具有自评能力，为学术争议提供新证据。

## 8. 不足与局限

- **算力信息不完整**：全文只给出Gemma2-2B的粗略GPU小时数量级，没有列出所有模型的总推理成本、具体GPU数量或时长，不利于复现成本估算。
- **模型覆盖局限**：仅测试9个开源指令微调模型，且多为中低参数规模（2B-123B），未覆盖典型闭源商业模型（如GPT-4、Claude等）；也未验证非指令微调或RL后训练（如DeepSeek-R1）的模型上是否适用。
- **数据集范围有限**：集中于数学（GSM8K、MATH）与单选题知识推理（MMLU-Pro、BBH），未涉及开放问答、摘要、代码生成或规划任务，结论的外推性有限。
- **置信度提取方法的范围较窄**：
  - Verbal方法只用了0/1和0-100简单提示，未尝试类似“列出多个猜测并给概率”等更细粒度的方法；
  - P(True)是最佳方法，但需要访问token级概率，并非所有LLM API都支持；论文在局限性中也承认了这一点。
  - 所有实验均基于零样本提示，未分析少样本提示的影响。
- **置信度提示的两步设计依赖KV缓存支持**：作者指出并非所有框架都能方便地复用前缀缓存；虽然提供了单步替代方案，但在主实验未采用该方案。
- **人类评估规模与覆盖面有限**：仅90条样本、两个知识背景为NLP博士的标注者，且集中在MMLU-Pro；由于MMLU-Pro本身难度很大，标注者缺乏领域知识，只能依赖“推理模式”判断，可能引入主观偏差。
- **温度调参依赖留出集**：虽然调参成本很低，但CISC的性能仍依赖一个额外的超参数T，而标准SC无需调参；论文未深入分析T在不同分布/难度问题下的稳定性。
- **简化分析忽略多答案分布情形**：在§3的动机示例中仅对二值情形做了闭式分析；对任意答案集合的一般情形，作者承认需要额外分布假设才能解析。

（完）
