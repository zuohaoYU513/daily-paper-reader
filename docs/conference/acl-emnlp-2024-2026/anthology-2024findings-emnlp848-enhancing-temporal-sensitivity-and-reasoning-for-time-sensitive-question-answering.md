---
title: Enhancing Temporal Sensitivity and Reasoning for Time-Sensitive Question Answering
title_zh: 增强时间敏感问答中的时间敏感性与推理能力
authors: "Wanqi Yang, Yanda Li, Meng Fang, Ling Chen"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.848.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 面向需要随时间演进事实和多时间语境的时间敏感问答
tldr: 传统模型对问答中的时间信息不敏感，也难以推理随时间变化的多条事实。本文提出时间信息感知嵌入与粒度对比强化学习框架，使模型在表示层捕获时间线索，并在推理层对齐不同粒度的时间事实。在四个时间敏感问答数据集上的实验表明，该方法显著提升答案准确率，为需跟踪长或跨句文档内事实变化的任务提供了有效技术支撑。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp848/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1576, \"height\": 913, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp848/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1326, \"height\": 730, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp848/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp848/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1644, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp848/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 644, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp848/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp848/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp848/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 398, \"height\": 573, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp848/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1645, \"height\": 2006, \"label\": \"Table\"}]"
motivation: 大语言模型对时间变化事实感知不足，难以回答依赖时间演进语境的问题。
method: 提出时间信息感知嵌入与粒度对比强化学习，联合增强时间感知和时间推理。
result: 在四个TSQA数据集上的实验显示效果显著提升，验证了时间感知增强的有效性。
conclusion: 该方法能有效利用文档中随时间演进的多条事实来回答时间敏感问题。
---

## Abstract
Time-Sensitive Question Answering (TSQA) demands the effective utilization of specific temporal contexts, encompassing multiple time-evolving facts, to address time-sensitive questions. This necessitates not only the parsing of temporal information within questions but also the identification and understanding of time-evolving facts to generate accurate answers. However, current large language models still have limited sensitivity to temporal information and their inadequate temporal reasoning capabilities. In this paper, we propose a novel framework that enhances temporal awareness and reasoning through Temporal Information-Aware Embedding and Granular Contrastive Reinforcement Learning. Experimental results on four TSQA datasets demonstrate that our framework significantly outperforms existing LLMs in TSQA tasks, marking a step forward in bridging the performance gap between machine and human temporal understanding and reasoning.

---

## 论文详细总结（自动生成）

# 论文总结：Enhancing Temporal Sensitivity and Reasoning for Time-Sensitive Question Answering

## 1. 核心问题与整体含义（研究动机与背景）

- 任务背景：时间敏感问答（Time-Sensitive Question Answering, TSQA）要求模型利用问题中显式或隐式的时间信息，对包含多个随时间演进事实的上下文进行理解，进而推理出正确答案。例如，“奥巴马的职位在2006年和2016年并不相同”，这类问题要求模型按时间定位事实。
- 核心挑战有两方面：
  1. 时间信息敏感度不足：LLM 对问题与上下文中的时间表达缺乏关注，容易被长上下文中无关信息干扰，难以通过时间线索定位相关文本片段。
  2. 时间推理能力薄弱：模型容易受到同一实体/关系在不同时间段上的干扰答案影响，也容易受到同时间段内其他不相关事件的影响。
- 论文的整体动机是：尽管 TSQA 数据集被引入并用于评测多个 LLM（如 FiD、BigBird、T5），但这些模型表现远低于人类水平，且缺乏一种系统性的方法增强模型对时间信息的感知与推理。
- 该论文提出一个通用训练框架，从“时间信息感知嵌入”和“粒度对比强化学习”两端入手，旨在显著提升 LLM 在 TSQA 上的表现，缩小人类与机器在时间理解和推理上的性能差距。

## 2. 论文提出的方法论

### 2.1 总体框架

- 框架以预训练语言模型（T5-base）为骨干，针对输入的自由文本问题 \( Q \) 和上下文 \( C \) 生成答案 \( \tilde{A} \)。
- 框架包含两个核心模块：
  1. Temporal Information-Aware Embedding（TIAE，时间信息感知嵌入）——提升模型对时间信息的敏感性；
  2. Granular Contrastive Reinforcement Learning（GCRL，粒度对比强化学习）——增强模型的时间推理能力。

### 2.2 Temporal Information-Aware Embedding（TIAE）

- 设计灵感：人类阅读时间敏感问题时，会先定位问题中的时间线索，再到上下文中寻找对应时间附近的答案；该方法模拟这一行为，在嵌入层显式强化时间表达及其邻近信息。
- 算法步骤：
  1. 构造问题时间矩阵 \( A_q \) 和上下文时间矩阵 \( A_c \)，初始化为全 0 向量，长度分别对应 token 长度。
  2. 使用 SpaCy 识别问题和上下文中的时间表达式，将这些位置在矩阵中标记为 1。
  3. 对每个标记位置，采用中心滑动窗口 \( W_{a_i} = \{a_{i-L}, ..., a_i, ..., a_{i+L}\} \)（窗口大小 \( L \)）将窗口内所有位置也置为 1，从而突出时间词临近的信息。
  4. 将扩展后的两个矩阵拼接，通过时间嵌入层 \( W_{\text{time}} \) 得到 temporal information-aware embedding \( e_{\text{time}} \)。
  5. 问题的文本嵌入 \( e_{\text{text}} \) 与 \( e_{\text{time}} \) 相加，作为模型输入，使模型更关注时间线索及其附近具体内容。

### 2.3 Granular Contrastive Reinforcement Learning（GCRL）

- 核心思想：通过引入不同“粒度”的负答案，并用对比式奖励函数进行强化学习，让模型学会区分时间维度上的正确与错误事实。

#### 负答案的构造（两种粒度）

- 远程负答案（Remote Negative Answers）：与正确事实属于同一实体和关系，但发生在不同时间段。例如奥巴马的“芝加哥大学教授（1993-2005）”对“2009年奥巴马职位”的问题而言就是远程负例；这类答案虽然在语义上相关，但时间距离较远。
- 近端负答案（Proximal Negative Answers）：与正确事实处于同一时间段，但属于不同实体或关系。例如奥巴马 2008-2017 期间发生的“国务卿”“最高法院”“诺贝尔和平奖”等，虽时间相近但与职位问题不直接对应。
- 二者的数量比例在实验中设为 1:1。

#### 对比强化学习奖励函数

- 论文指出传统 EM（Exact Match）奖励机制过于刚性，例如预测是“the capital of France”、真实答案是“Paris”时 EM 得分为 0，忽略了语义等价性。
- 新方法采用向量化表示，对真实答案 \( GT \)、模型预测 \( P \)、负答案集合 \( N \) 计算三元组损失：
  \[
  T = \max\{d(GT, P) - d(P, N) + \text{margin}, 0\}
  \]
  其中 \( d(x, y) = \|x - y\|_2 \)。
- 将 \( T \) 归一化并映射为奖励函数 \( R \)：
  \[
  R = \alpha \cdot \left( \frac{2}{1 + e^{T} + \delta} \right) - \beta
  \]
  实验中使用 \( \alpha=4, \beta=2, \delta=1e-6 \)。
- 优化目标使用 Proximal Policy Optimization（PPO）进行策略训练。

## 3. 实验设计

### 3.1 数据集

- 论文使用四个 TSQA 测试集合，覆盖不同难度和上下文类型：
  - TempReason L2（Time-Event QA）：问题含显式时间点（如 in YEAR）；时间点可能无法在上下文中直接匹配；提供 Wikidata 自由文本上下文（OBQA）和结构化上下文（ReasonQA）。
  - TempReason L3（Event-Event QA）：问题不含显式时间，时间信息用事件表达（如“二战期间”），涉及 before/after/during/simultaneous 等关系；同样包含 OBQA 和 ReasonQA 两种上下文。
  - TimeQA Easy：问题含显式时间，时间能在上下文中直接匹配，只提供 OBQA 自由文本上下文。
  - TimeQA Hard：问题时间表达更复杂（如 before/after/first/last），时间不能直接匹配，只提供 OBQA 上下文。
- 最终形成六种“数据集×设置”的评测组合：(L2-ReasonQA, L2-OBQA, L3-ReasonQA, L3-OBQA, TimeQA-Easy, TimeQA-Hard)。

### 3.2 基准方法

- FLAN-T5-Large；
- ChatGPT（gpt-3.5-turbo）；
- T5-SFT（在训练集上做监督微调的 T5-base）；
- 另外还对比了专为 TempReason 设计的 TempT5 框架。

### 3.3 评估指标

- Exact Match（EM）和 F1 分数。

### 3.4 消融实验设计

- T5-SFT vs T5-SFT with TIAE vs T5-SFT with GCRL vs Ours（完整框架）：用于验证两个模块各自的贡献。
- 奖励函数对比：T5-SFT with EM-RL（EM 作为奖励） vs T5-SFT with Contrastive-RL（对比三元组分数作为奖励）。
- 负答案粒度对比：Remote only、Proximal only、Remote & Proximal，彼此数量一致。
- 与专门方法的对比：Ours vs TempT5。

## 4. 资源与算力

- 论文在训练部分给出的算力相关信息有限，明确提到的内容如下：
  - 硬件：NVIDIA Tesla V100 GPU。
  - 第一阶段（监督微调 T5-base）：6 epochs，batch size 8，优化器 AdamW，学习率 5e-6。
  - 第二阶段（基于框架的强化学习微调）：10 epochs，batch size 16，PPO 优化。
  - TIAE 参数：滑动窗口大小 \( L=10 \)；GCRL 中远程与近端负答案比例为 1:1。
- 论文并没有说明具体使用了多少张 GPU 卡、单卡型号细节、总训练时长或显存占用；因此无法从文本中估算完整算力成本。也就是说，该论文没有提供可复现的算力开销细节。

## 5. 实验数量与充分性

- 实验数量较充实：
  - 全部主结果覆盖四个数据集、六种子设置，对比 3 个基线；
  - 额外提供与 TempT5 的对比；

- 消融实验方面：
  - 验证 TIAE 和 GCRL 两个模块的贡献；
  - 验证不同奖励函数（EM vs 对比式）的差异；
  - 验证远程/近端负答案单独及联合的效果；
  - 每个消融均使用固定测试集，并同时报告 EM 与 F1。
- 充分性评估：
  - 优点：实验设计较系统，能够说明方法各组成部分的有效性；覆盖了显式/隐式时间、结构化/自由文本、不同难度等多类情况，结论有一定泛化性；与专门框架 TempT5 的对比强化了说服力。
  - 不足：① 骨干模型仅为 T5-base，缺少在更大模型（如 T5-large、FLAN-T5-Large、LLaMA 等）上的扩展结果，无法证明框架对模型规模的迁移性；② 自由文本 OBQA 上的绝对分数仍然较低（EM 19.3~48.1），说明长文本干扰仍是挑战；③ 在 TimeQA 数据集上，Ours 虽提升 EM，但 F1 相比 T5-SFT 有所下降（Easy 从 53.7 降到 52.1，Hard 从 45.5 降到 44.3），论文解释为模型倾向于生成空字符串导致 recall 下降，该现象说明评测稳定性存在隐患；④ 没有与“人类表现”在同一实验条件下直接量化比较，因此“缩小人类差距”的结论只能间接体现。

## 6. 论文的主要结论与发现

- 所提出的整个框架在所有评测的 TSQA 设置上均显著优于 FLAN-T5-Large、ChatGPT、T5-SFT 和 TempT5。
- 具体提升示例（以 EM 为主）：
  - 相对于各自最强基线，L2-ReasonQA EM 提升 12.2%，L2-OBQA 提升 30.4%，L3-ReasonQA 提升 19.7%，L3-OBQA 提升 26.4%，TimeQA-Easy 提升 6.7%，TimeQA-Hard 提升 7.4%。
- 单独消融证明：
  - 仅使用 TIAE 即可在 L2-OBQA 上带来 23.6% EM 相对提升；
  - 仅使用 GCRL 即可带来 29.7% EM 提升；
  - 两个模块叠加获得最佳性能（30.4% EM 提升）。
- 负答案粒度实验表明，远程和近端负答案各自均有贡献，同时使用两种负答案效果最好。
- 对比式三元组奖励比基于 EM 的奖励更适合 TSQA，能减轻“语义相同但文本不同”导致的零分问题。

## 7. 优点

- 方法设计贴近人类认知：TIAE 模拟人类先定位时间线索再阅读周围文本的流程，直观且有效。
- 将嵌入层与强化学习结合，不是简单增加模型容量，而是针对“时间敏感”和“时间推理”两个能力缺口分别建模，具备较强的可解释性。
- GCRL 中负答案的双粒度设计同时覆盖“时间距离干扰”和“同时间事件干扰”，较完整地刻画了 TSQA 中的常见混淆来源。
- 引入对比奖励函数解决了以往 EM 奖励无法处理语义等价预测的问题，是奖励设计上的合理改进。
- 实验验证较系统：含多数据集、多上下文类型、多难度，并给出多个维度的消融，证据链较完整。

## 8. 不足与局限

- 算力与训练细节披露不充分，缺少 GPU 数量、训练时长等信息，不利于复现和成本评估。
- 模型基座选择有限，仅在 T5-base 上验证；未说明方法是否稳定适用于更大规模的 LLM 或结构不同的模型。
- 依赖 SpaCy 识别时间表达，识别错误或漏检可能直接削弱 TIAE 的效果；对包含大量隐式时间、相对时间或复杂事件指代的场景，敏感性可能不足。
- TimeQA 上出现“通过牺牲少量 F1 换取 EM 提升”的副作用，说明奖励机制可能还未完全平衡精准率与召回率，存在过度倾向输出空字符串的风险。
- OBQA 自由文本设置下的绝对性能仍然偏低（多数 EM 低于 50%），框架对长文本、高度噪音上下文的处理能力依然有限。
- 论文自述模型与人类水平仍有显著差距，且缺少更细粒度的跨数据集泛化测试；对“未来工作”也只作简要陈述，没有提出后续优化方向。
- 总体而言，该工作提出了一套新颖且有效的 TSQA 训练框架，实验证据支持其相对现有方法的领先性，但在模型规模扩展、细节披露和评估稳定性方面仍有明显不足。

（完）
