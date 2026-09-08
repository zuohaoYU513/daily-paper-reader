---
title: "Temporal Cognitive Tree: A Hierarchical Modeling Approach for Event Temporal Relation Extraction"
title_zh: 时间认知树：事件时序关系抽取的层次化建模方法
authors: "Wanting Ning, Lishuang Li, Xueyang Qin, Yubo Feng, Jingyao Tang"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.47.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 抽取事件间的时序关系，用层次化认知建模时间联系
tldr: 事件时序关系抽取中，以往方法多只判断事件对在时间线上的相对位置，忽略多维时间信息与层级推理过程。本文将人类逻辑推理引入建模，提出时间认知树TCT的层次化表示方法，把事件间的时序关系组织为树状认知结构。模型在事件时序关系抽取任务上验证了该结构能更好地利用多维信息。实验表明TCT可有效提升时序关系抽取效果，为该任务提供层次推理的新视角。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp47/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 763, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp47/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 758, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp47/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1650, \"height\": 908, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp47/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1658, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp47/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp47/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 801, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp47/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 802, \"height\": 657, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp47/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 812, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp47/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 505, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp47/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1676, \"height\": 733, \"label\": \"Table\"}]"
motivation: 现有事件时序关系抽取只靠逻辑表达式或辅助任务预测事件对的时间先后，忽略了多维时序信息与人类的层级推理机制。
method: 提出时间认知树TCT层次化模型，将事件时序关系组织为模拟人类逻辑推理的树状认知结构。
result: 在事件时序关系抽取上进行实验，验证该层级建模方法能提升事件对时序关系的抽取表现。
conclusion: 表明时间认知树层次建模可弥补仅做时间线定位的不足，为事件时序关系抽取提供更贴近人类推理的建模思路。
---

## Abstract
Understanding and analyzing event temporal relations is a crucial task in Natural Language Processing (NLP). This task, known as Event Temporal Relation Extraction (ETRE), aims to identify and extract temporal connections between events in text. Recent studies focus on locating the relative position of event pairs on the timeline by designing logical expressions or auxiliary tasks to predict their temporal occurrence. Despite these advances, this modeling approach neglects the multidimensional information in temporal relation and the hierarchical process of reasoning. In this study, we propose a novel hierarchical modeling approach for this task by introducing a Temporal Cognitive Tree (TCT) that mimics human logical reasoning. Additionally, we also design a integrated model incorporating prompt optimization and deductive reasoning to exploit multidimensional supervised information. Extensive experiments on TB-Dense and MATRES datasets demonstrate that our approach outperforms existing methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **任务定义**：事件时序关系抽取（Event Temporal Relation Extraction, ETRE）旨在识别和抽取文本中事件之间的时序连接，如 BEFORE、AFTER、INCLUDES、VAGUE 等关系。该任务是自然语言处理中的一项基础且具有挑战性的任务。
- **研究背景**：早期使用传统机器学习方法，近期方法主要分为两类：一类通过引入外部知识来缓解数据稀疏问题；另一类则关注时序关系语义，采用“时间线定位”（timeline positioning）策略，将事件对的时序关系建模为它们在时间轴上相对位置的线性组合。
- **核心问题**：论文指出现有时间线定位模型仅使用事件发生时间的单一维度信息来推断时序关系，忽略了时序关系中的**多维语义信息**（如重叠、先后、包含等）以及人类在推理时序关系时固有的**层级推理过程**。这种线性建模方式导致模型对时序关系的理解有限，尤其对语义模糊的 VAGUE 关系判别不佳，容易将其他关系误分类。
- **整体含义**：本文旨在将人类的逻辑推理过程引入事件时序关系抽取，提出层次化建模方法，使模型能够充分利用多维监督信息以及层级推理的先验知识，从而更深入地理解各类时序关系的内在含义。

### 2. 论文提出的方法论

#### 核心思想
借鉴人类判断事件时序关系的逻辑思维过程，提出**时间认知树（Temporal Cognitive Tree, TCT）**，将单一的时序关系分类问题分解为多个由抽象到具体、由粗粒度到细粒度的“条件判断”子问题，从而形成层次化的推理路径，并通过多任务学习和演绎推理将层级知识注入模型。

#### 关键组成模块

**（1）时间认知树（TCT）**

- 针对不同数据集，设计不同的树状结构。树的节点为“是/否”类的条件判断提示（conditional prompts），时序关系由这些二值节点组合成唯一的 0/1 向量表示。
- 设计遵循两条原则：
  - **一致性原则**：不同时序类别至少在一个维度上共享相同特征，以帮助模型理解类别间的语义关联和细粒度差异（而非简单地将标签作 one-hot 编码）。
  - **层次性原则**：高层判断更抽象，低层判断更具体；高层判断结果决定所需进行的低层判断内容，且部分关系无需遍历所有判断节点。
- 通过每条时序关系的推理规则（如 TB-Dense 中 BEFORE 的路径被定义为 `P1 ∧ ¬P2 ∧ P3`），将时序关系映射为逻辑表达式，供推断模块使用。

**（2）时间判断模块（Temporal Judgment Module, TJM）——基于多任务提示学习**

- 采用序列到序列的 BART 模型。输入的文本和事件对被编码后，分别与各条件提示及最终关系分类提示交互，得到携带层次信息的表示向量。
- 辅助任务：为每个条件提示训练一个二分类器；主任务：为最终时序关系训练一个多分类器。两者共享编码器参数。
- 不使用线性加权多任务损失，而是将多任务学习视为**多目标优化问题**，采用多梯度下降算法（MGDA）求解 Pareto 最优解，动态更新各任务的权重。

**（3）时间推理模块（Temporal Inference Module, TIM）——基于演绎推理**

- 将任务转化为**多标签二分类**问题，对每个事件对预测树中每个条件节点的真值概率。
- 使用焦点损失（Focal Loss）处理类别不平衡，同时兼顾 Hamming Loss。
- 推理时，根据 TCT 的逻辑表达式（如表 1 中的 `P1 ∧ P3` 等）组合各条件节点的概率，得到最终的时序关系概率分布。具体概率计算规则为：
  - `P ∧ Q = Pr(P) · Pr(Q)`
  - `P ∧ ¬Q = Pr(P) · (1 − Pr(Q))`

**（4）模块融合**

- 将 TJM 主任务得到的概率分布与 TIM 的概率分布进行加权求和，得到最终预测概率：`P_final = α·P_J + β·P_I`（超参数 α、β 在不同数据集上设置不同）。

### 3. 实验设计

- **数据集（Benchmark）**：
  - **TB-Dense**：包含 6 种细粒度时序关系（BEFORE、AFTER、INCLUDES、IS_INCLUDED、SIMULTANEOUS、VAGUE），使用排除 VAGUE 类的微平均 F1 作为评估指标。
  - **MATRES**：包含 4 种粗粒度时序关系（BEFORE、AFTER、EQUAL、VAGUE），同样使用微平均 F1 作为评估指标。
- **对比方法**，分为三类：
  1. **知识增强模型**：Uncertainty-training、HGRU、Bayesian-Trans、OntoEnhance 等（引入外部知识/额外数据）。
  2. **时间线定位模型**：Relative Time、Unified-Framework（即 Huang 等 2023 的方法）。
  3. **其他基准模型**：ECONET、Probabilistic Box、Syntax Transformer 等。
  此外还补充了 T5-large 和 BART-large Vanilla Classifier 两组基线。
- **模型配置**：以 BART-large 为骨干；另以 BART-base 进行消融实验；TJM 和 TIM 并行训练两个 BART 模型。

### 4. 资源与算力

- 论文**未明确提及**所使用的 GPU 型号、数量、训练总时长或硬件规模。仅说明了训练超参数：
  - 优化器：Adafactor，学习率 warm-up 比例为 0.1；
  - Batch size：32；
  - 学习率：TB-Dense 为 3e-5，MATRES 为 2e-5；
  - 训练轮数：50 epochs，依据验证集效果选取模型。

### 5. 实验数量与充分性

文中进行的主要实验组包括：

- **主实验**：在 TB-Dense 与 MATRES 两个数据集上与三类共 10 余种现有方法对比，实验覆盖较全面。
- **消融实验**：分别在 BART-large 和 BART-base 两种骨干模型规模上，逐一移除 TJM 和 TIM，共形成多组消融组合，能够说明模块各自的贡献。
- **子类别分析**（TB-Dense）：比较各时序关系类别（含少量类）分类的 F1，分析模型在小样本类别上的表现。
- **误分类分析**：对比被误分类为 VAGUE 的实例数量，验证模型在歧义关系上的判别力。
- **案例研究**：通过具体例子的条件查询输出结果验证模型推断过程合理性。

**充分性与客观性评价**：整体实验设置较全面，主实验、消融、细粒度类别分析及案例覆盖了方法评估的主要维度；消融实验同时使用两种规模的骨干模型，增强了结论的稳健性。但不足在于仅使用两个公开数据集，结论的外推性仍有一定局限；MATRES 上优势幅度较小，且论文未报告显著性检验结果。此外，超参数 α、β 的可调节性也可能引入调参偏差。

### 6. 论文的主要结论与发现

- 论文所提出的基于 TCT 的层次化建模方法在 **TB-Dense** 与 **MATRES** 上均取得最优成绩（不依赖外部知识），在 TB-Dense 上比此前 SOTA 高出 **2.9%**，在 MATRES 上高出 **0.2%**。
- 模型能够有效缓解数据不平衡问题，在样本量稀少的类别上优于基线模型。
- 相较于时间线定位模型，基于 TCT 的层次推理建模包含更多对训练有益的多维信息；层级越多，对模型性能的提升越明显。
- TJM 更倾向于提升召回率，而 TIM 更倾向于提升精确率，融合两者可以结合各自优势，实现模型整体最佳表现。

### 7. 优点

- **方法设计新颖**：将人类逻辑推理中的层级过程显式建模为时间认知树，突破仅基于单一时间线位置进行推断的范式。
- **多维信息利用充分**：通过设计条件提示与逻辑推理规则，模型需要从多个视角（是否重叠、是否先发生、是否同时、是否包含等）判断事件关系，有助于捕捉时序类别的语义结构。
- **理论支撑扎实**：多任务部分使用 MGDA 求解 Pareto 最优，推理部分使用 Focal Loss 缓解不平衡，技术选择具有明确理论依据。
- **无需外部知识**：对比依赖外部知识增强的主流方法，该模型在无外部资源条件下依然取得更优效果，降低了对额外资源的依赖和噪声引入风险。
- **分析角度丰富**：包括子类别性能分析、VAGUE 误分类分析、案例推断过程展示等，从多个角度验证模型有效性。

### 8. 不足与局限

- **方法依赖关系类别与数量的设计**：TCT 的形状与层级数完全依数据集定义而人工设计，若时序类别较少（如 MATRES 仅 4 类），层次不足时性能优势明显变弱（仅比 SOTA 高 0.2%），说明方法在粗粒度场景下的提升潜力有限。
- **计算开销较大**：TJM 和 TIM 需要并行训练两个 BART-large 模型，训练成本较高。
- **人工设计成本高**：认知树的构造依赖人工对时序关系语义的分解和逻辑表达式的手工设计，迁移到新领域或新任务时需重新设计。
- **实验覆盖不足**：仅涉及两个英语公开数据集，未在跨语言、跨领域或文档级关系抽取上验证方法的泛化性；也未报告统计显著性检验结果。
- **算力细节缺失**：未披露 GPU 型号、数量及训练耗时，难以评估复现成本与效率。
- **潜在偏差风险**：虽然加入了多任务优化，但条件判断提示的设计本身存在人工主观性，不同的提问顺序或问法可能对模型产生不可预期的影响。

（完）
