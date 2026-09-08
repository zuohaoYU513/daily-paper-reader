---
title: "Beyond Single-Event Extraction: Towards Efficient Document-Level Multi-Event Argument Extraction"
title_zh: 超越单事件抽取：迈向高效的文档级多事件论元抽取
authors: "Wanlong Liu, Li Zhou, DingYi Zeng, Yichen Xiao, Shaohuan Cheng, Chen Zhang, Grandee Lee, Malu Zhang, Wenyu Chen"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.564.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 文档级多事件论元并行抽取，建模跨事件关联
tldr: 主流事件论元抽取把每个事件孤立处理，既慢又忽略多事件间联系。作者提出多事件提取模型DEEIA，采用多事件提示机制，通过DE依赖引导编码增强提示与对应事件上下文的相关性，用EIA事件特定信息聚合补充语境理解，支持在文档中同时抽取所有事件的论元。实验表明DEEIA能够利用跨事件依赖提升文档级抽取效率和准确性。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl564/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 716, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl564/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl564/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1644, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl564/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 796, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl564/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 1169, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl564/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl564/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 805, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl564/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1603, \"height\": 454, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1526, \"height\": 681, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1604, \"height\": 427, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 731, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 666, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 777, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 795, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1639, \"height\": 877, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 803, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl564/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1455, \"height\": 1489, \"label\": \"Table\"}]"
motivation: 事件论元抽取逐事件处理导致推理低效且无法利用文档内事件间的关联信息。
method: 提出DEEIA，将多头提示与依赖编码、事件信息聚合结合，在多事件文档中同时抽取论元。
result: 实验显示该模型可在一个文档中并行提取多个事件的论元，提升效率和提取效果。
conclusion: 文档级多事件建模能有效捕捉事件关联，比孤立抽取更适合真实文档。
---

## Abstract
Recent mainstream event argument extraction methods process each event in isolation, resulting in inefficient inference and ignoring the correlations among multiple events. To address these limitations, here we propose a multiple-event argument extraction model DEEIA (Dependency-guided Encoding and Event-specific Information Aggregation), capable of extracting arguments from all events within a document simultaneously. The proposed DEEIA model employs a multi-event prompt mechanism, comprising DE and EIA modules. The DE module is designed to improve the correlation between prompts and their corresponding event contexts, whereas the EIA module provides event-specific information to improve contextual understanding. Extensive experiments show that our method achieves new state-of-the-art performance on four public datasets (RAMS, WikiEvents, MLEE, and ACE05), while significantly saving the inference time compared to the baselines. Further analyses demonstrate the effectiveness of the proposed modules.

---

## 论文详细总结（自动生成）

## 论文中文详细总结

### 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：文档级事件论元抽取（Document-level Event Argument Extraction, EAE）是信息抽取中的关键任务，旨在从文档中识别事件相关论元及其角色。
- **现有方法的局限**：主流EAE方法大多为“单事件抽取”（Single-EAE），即每次只处理一个事件。这类方法存在两个显著问题：
  - **推理效率低下**：面对包含多个事件的文档，必须反复迭代处理同一文本，计算开销大。
  - **忽视事件间关联**：无法利用同一文档中多个事件之间的语义相关性（如论元重叠、事件共现等现象）。
- **本文目标**：提出一种**多事件论元抽取（Multi-EAE）**模型，能够在一次前向传播中同时抽取文档内所有事件的论元，以提高效率，并通过建模事件间关联提升抽取性能。

### 2. 方法论

#### 2.1 核心思想
作者提出DEEIA模型（Dependency-guided Encoding and Event-specific Information Aggregation），基于SOTA提示式单事件模型PAIE，引入**多事件提示机制**，并设计两个核心模块应对多事件并行抽取带来的信息复杂性：
- **依赖引导编码模块（Dependency-guided Encoding, DE）**：通过预先定义的事件依赖关系，引导模型将各事件的提示（prompt）与其对应的事件上下文关联起来。
- **事件特定信息聚合模块（Event-specific Information Aggregation, EIA）**：为目标论元自适应聚合与其相关的上下文与提示信息，增强上下文理解。

#### 2.2 关键技术细节

**（1）多事件提示机制（Multi-event Prompt Mechanism）**
- 对文本中的每个事件触发词添加唯一标记（如`<ti> trigger </ti>`）。
- 将每个事件的提示（基于PAIE的schema prompt）与事件类型拼接，并在事件类型前后添加唯一标记，形成整体输入。

**（2）事件依赖定义**
形式化为D = {dp_ij}，其中dp_ij ∈ {Intra-event, Inter-event, NA}，含义如下：
- **Intra-Event Dependency（事件内依赖）**：同一事件内，触发词与提示词之间、提示词内部之间的联系。
- **Inter-Event Dependency（事件间依赖）**：不同事件之间，触发词与提示词之间的联系。
- **NA**：表示无依赖关系。

**（3）依赖引导编码器（DE模块）**
- 在vanilla self-attention中引入可学习的注意力偏置项：
  - `a_ij = (q_i * k_j^T) / sqrt(d_k) + γ · bias_ij`
  - 当有依赖关系时，`bias_ij`由依赖类型对应的可学习参数计算；无依赖时为0。
- 每个Transformer编码器层都施加该依赖信息；解码器不施加（消融实验表明编码器纳入依赖信息即可，解码器过度引导反而有害）。

**（4）事件特定信息聚合（EIA模块）**
- 利用编码器多头注意力中**论元槽位**与**对应触发词**的注意力向量，计算点积得到软权重p_k：
  - `p_k = softmax(A_ti · A_s_k,i)`
- 用该权重对编码器隐藏状态进行加权求和，得到“上下文增强向量”c_k,i。
- 将c_k,i与解码器输出拼接后经tanh层融合，得到最终论元表示。

**（5）跨度选择与训练损失**
- 采用PAIE中的span selector方式，结合双向匹配损失（Bipartite Matching Loss）训练，利用匈牙利算法为各槽位匹配最优gold论元。

**（6）长文本处理**
- 使用动态滑动窗口算法（Dynamic Window），对超长序列切分后分别编码、平均池化融合。

### 3. 实验设计

- **数据集**：使用了三个文档级公开数据集——RAMS、WikiEvents、MLEE；此外还扩展到句子级数据集ACE05。
- **Benchmark对比方法**：
  - **Span-based**：TSAR、SCPRG；
  - **Generation-based**：DocMRC、EEQA、FEAE、BART-Gen、HRA；
  - **Prompt-based单事件**：RKDE、PAIE、SPEAE、TabEAE；
  - **Prompt-based多事件baseline**：PAIE-multi、TabEAE-multi（作者改造）。
  - 附录中还与基于大语言模型的方法HD-LoA（text-davinci-003、gpt-3.5-turbo、GPT-4）进行了对比。
- **评价指标**：
  - Arg-I（严格论元识别F1）；
  - Arg-C（严格论元分类F1，需边界和角色都正确）；
  - 结果取5次不同随机种子平均值。

### 4. 资源与算力

- 论文实验说明使用**一张Tesla A100 GPU**进行推理时间测试；模型训练配置描述为PyTorch实现，未明确报告GPU数量。
- **训练步数**：三个数据集均为10,000步。
- **模型结构**：采用RoBERTa-large前17层作为编码器，后7层作为解码器；解码器交叉注意力随机初始化，学习率为其他参数的1.5倍。
- 未提及模型训练总时长或能源消耗。

### 5. 实验数量与充分性评估

论文的**实验组数相当丰富**，整体具有较强的充分性：

- 在四个数据集上的**主实验对比**（RAMS、WikiEvents、MLEE、ACE05）；
- **多组对照消融**（去除DE、w/o intra、w/o inter、w/o PE、w/o EIA、w/o DE & EIA），并按单事件/多事件实例分别报告；
- **推理效率对比**（在三个数据集上对比PAIE、PAIE-multi、TabEAE-multi的推理时间）；
- **事件数量分组分析**（MLEE和WikiEvents上按#E分组展示性能变化）；
- **依赖引导可视化分析**（三层数据集上按层展示注意力偏置）；
- **EIA注意力权重可视化**（具体案例分析）；
- **错误分析**（WikiEvents测试集上分5类错误统计）；
- **架构变体分析**（DE是否引入解码器、重复prompt是否拼接）；
- **LLM对比实验**（RAM数据集上的性能对比）；
- **案例研究**（包含多事件示例，直观展示模块效果）。

整体实验设计**客观公正**：多事件baseline做了公平化改造，消融和分组分析能从多个维度验证模块有效性，错误分析和可视化也增加了结论的可靠性。但错误分析仅基于一个数据集，涉及一定偏差风险。

### 6. 主要结论与发现

- DEEIA在四个数据集上均取得了最优或接近最优的结果：
  - RAMS：Arg-C 53.4；
  - WikiEvents：Arg-C 67.0；
  - MLEE：Arg-C 74.3；
  - ACE05：Arg-C 74.1。
- 相比单事件PAIE，DEEIA在RAMS、WikiEvents、MLEE上分别节省了约8.76%、32.96%、35.20%的推理时间；相比TabEAE-multi节省55%~69%推理时间，且参数几乎未增加。
- DE和EIA模块均能显著提升多事件抽取性能；两者联合使用效果更好。其中DE主要改善“过度抽取”和“漏抽取”错误；EIA主要改善“漏抽取”和“部分匹配”错误。
- 多事件文档中，事件间依赖的作用更加显著；EIA模块能有效捕捉论元重叠等跨事件关联现象。
- 在EAE任务上，有监督方法仍显著优于基于大语言模型的方法，且成本更低。

### 7. 优点

- **任务视角新颖**：厘清“单事件”与“多事件”抽取的差异，提出更贴近真实文档场景的多事件抽取范式。
- **方法设计合理**：在提示框架下引入依赖引导编码，直接解决多事件并行抽取中“提示与上下文对应关系不清”这一核心问题。
- **模块互补性好**：DE负责结构信息引导，EIA负责内容级信息聚合；二者可联合作用，消融证明设计有效。
- **效率与效果双优**：在性能提升的同时显著降低推理时间，实用价值高（参数总数几乎不增加）。
- **分析较全面**：包括事件数量效应分析、依赖偏置可视化、注意力权重可视化、错误分类分析、案例研究等，能深入揭示各模块内部机制。
- **多事件基线改造比较公平**（PAIE-multi、TabEAE-multi），对结论可靠性有益。

### 8. 不足与局限

- **输入长度限制**：拼接文本与多事件提示后更容易超出模型最大长度。当前采用滑动窗口方案可能导致信息丢失，模型处理过长文档的效果仍不理想。
- **数据集与任务多样性有限**：虽然覆盖了多个数据集，但多为新闻和生物医学领域；在剧本对话等更多领域文本上的泛化能力尚待验证。
- **事件类型分布偏差**：RAMS数据集中单事件样本占主导，导致实验中多事件改进空间的明显差异；错误分析和部分深入分析只在WikiEvents进行，结论存在一定的偏差风险。
- **LLM对比深度不足**：与LLM的对比仅在RAMS上进行，未覆盖其他数据集，也没有充分讨论prompt策略或成本差异。
- **架构复杂度较高**：依赖偏置在编码器各层加入，引入额外超参数（γ），需要针对不同数据集单独调参，实验实现成本比较高。
- **未充分讨论实际情况中的复杂文档**：如事件触发词重叠、事件嵌套等场景未进行处理或讨论。

（完）
