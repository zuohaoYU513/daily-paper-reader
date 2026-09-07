---
title: "Understanding New-Knowledge-Induced Factual Hallucinations in LLMs: Analysis and Interpretation"
title_zh: 理解新知识诱发的大模型事实性幻觉：分析与解释
authors: "Renfei Dang, Peng Hu, Zhejian Lai, Changjiang Gao (长江 高), Min Zhang, Shujian Huang (书剑 黄)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.358.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 研究微调新知识如何诱发大模型事实性幻觉及其传播机制
tldr: 已有工作发现微调新知识会诱发大模型事实性幻觉，但具体表现与内在机制尚不清楚。该工作设计 Biography-Reasoning 控制数据集，按知识类型与任务类型进行细粒度分析，发现幻觉不仅影响新知识任务，还会迁移到其他评估任务，并且与微调数据形式有关。研究揭示了新知识微调导致幻觉的传播规律，为缓解领域微调带来的忠实度下降提供实证基础。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1384, \"height\": 345, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 822, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 835, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 801, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 795, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 798, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 828, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 834, \"height\": 605, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 828, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 740, \"height\": 1090, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 793, \"height\": 813, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 792, \"height\": 810, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 792, \"height\": 814, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 799, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 798, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 741, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 740, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 744, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 801, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 802, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 798, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 800, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 803, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 798, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 800, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 801, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 798, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 797, \"height\": 571, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 800, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 792, \"height\": 810, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 802, \"height\": 549, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-035.webp\", \"caption\": \"\", \"page\": 0, \"index\": 35, \"width\": 802, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-036.webp\", \"caption\": \"\", \"page\": 0, \"index\": 36, \"width\": 801, \"height\": 577, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-037.webp\", \"caption\": \"\", \"page\": 0, \"index\": 37, \"width\": 797, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-038.webp\", \"caption\": \"\", \"page\": 0, \"index\": 38, \"width\": 799, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-039.webp\", \"caption\": \"\", \"page\": 0, \"index\": 39, \"width\": 801, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-040.webp\", \"caption\": \"\", \"page\": 0, \"index\": 40, \"width\": 795, \"height\": 816, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-041.webp\", \"caption\": \"\", \"page\": 0, \"index\": 41, \"width\": 806, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-042.webp\", \"caption\": \"\", \"page\": 0, \"index\": 42, \"width\": 804, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-043.webp\", \"caption\": \"\", \"page\": 0, \"index\": 43, \"width\": 802, \"height\": 584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-044.webp\", \"caption\": \"\", \"page\": 0, \"index\": 44, \"width\": 797, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-045.webp\", \"caption\": \"\", \"page\": 0, \"index\": 45, \"width\": 797, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-046.webp\", \"caption\": \"\", \"page\": 0, \"index\": 46, \"width\": 800, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-047.webp\", \"caption\": \"\", \"page\": 0, \"index\": 47, \"width\": 793, \"height\": 817, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-048.webp\", \"caption\": \"\", \"page\": 0, \"index\": 48, \"width\": 805, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-049.webp\", \"caption\": \"\", \"page\": 0, \"index\": 49, \"width\": 804, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-050.webp\", \"caption\": \"\", \"page\": 0, \"index\": 50, \"width\": 805, \"height\": 584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl358/fig-051.webp\", \"caption\": \"\", \"page\": 0, \"index\": 51, \"width\": 799, \"height\": 483, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 812, \"height\": 1064, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 770, \"height\": 140, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 754, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1656, \"height\": 2330, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1659, \"height\": 1814, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1878, \"height\": 790, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1662, \"height\": 1330, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1797, \"height\": 817, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 958, \"height\": 749, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 790, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 799, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 775, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 771, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 767, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 772, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 833, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 804, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 786, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 800, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 815, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl358/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 798, \"height\": 167, \"label\": \"Table\"}]"
motivation: 微调新知识会使大模型产生事实性幻觉，但其具体表现和内在机制缺乏深入理解。
method: 构造 Biography-Reasoning 控制数据集，区分多种知识类型与问答/推理任务，进行细粒度分析并解释幻觉传播规律。
result: 幻觉不仅影响新知识相关任务，还会传播到已知知识任务；不同微调条件和知识类型下影响不同。
conclusion: 揭示了新知识微调致幻的机制，提出对微调过程造成幻觉迁移的理解，为安全微调提供参考。
---

## Abstract
Prior works have shown that fine-tuning on new knowledge can induce factual hallucinations in large language models (LLMs), leading to incorrect outputs when evaluated on previously known information. However, the specific manifestations of such hallucination and its underlying mechanisms remain insufficiently understood. Our work addresses this gap by designing a controlled dataset Biography-Reasoning, and conducting a fine-grained analysis across multiple knowledge types and two task types, including knowledge question answering (QA) and knowledge reasoning tasks. We find that hallucinations not only severely affect tasks involving newly introduced knowledge, but also propagate to other evaluation tasks. Moreover, when fine-tuning on a dataset in which a specific knowledge type consists entirely of new knowledge, LLMs exhibit elevated hallucination tendencies. This suggests that the degree of unfamiliarity within a particular knowledge type, rather than the overall proportion of new knowledge, is a stronger driver of hallucinations. Through interpretability analysis, we show that learning new knowledge weakens the model’s attention to key entities in the input question, leading to an over-reliance on surrounding context and a higher risk of hallucination. Conversely, reintroducing a small amount of known knowledge during the later stages of training restores attention to key entities and substantially mitigates hallucination behavior. Finally, we demonstrate that disrupted attention patterns can propagate across lexically similar contexts, facilitating the spread of hallucinations beyond the original task.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：已有研究表明，在大语言模型（LLM）上进行新知识的微调（如领域适配）会导致模型产生事实性幻觉，即在回答原本已掌握的知识时也出现错误输出。
- **核心问题**：这种新知识诱发幻觉的**具体表现形态**及其**内在机制**尚不清晰。具体包括：
  - 幻觉是否只影响新知识相关的任务，还是会**迁移扩散**到其他评估任务？
  - 新知识的数量比例与知识类型内部的陌生程度，哪一个才是幻觉的主驱动因素？
  - 微调新知识在模型内部造成了什么样的**注意力或表征变化**，从而引发幻觉？
- **研究意义**：理解上述问题对于构建安全、可控的领域微调流程具有重要的实证价值和指导意义。

### 2. 论文提出的方法论

- **核心思想**：通过设计**可控的虚构人物传记数据集**，将“新知识”与“已有知识”在知识类型级别（knowledge-type level）进行严格隔离，从而在微观层面上分离并剖析新知识学习引起的幻觉。
- **控制数据集 Biography-Reasoning**：
  - 针对虚构实体构造包含**多种知识类型**（如出生地、教育背景、职业经历等）的人物传记数据。
  - 将任务划分为**知识问答（knowledge QA）**和**知识推理（knowledge reasoning）**两大类，以考察幻觉在不同任务类型中的表现差异。
  - 通过在训练集中将**某一个特定知识类型的全部数据替换为新知识**，控制“整体新知识比例”与“某一类型内部全部为陌生知识”两个变量之间的对比。
- **核心分析流程**：
  1. 在受控数据上进行微调，比较不同训练数据构成下的幻觉程度；
  2. 对微调后的模型进行**可解释性分析（interpretability analysis）**，使用注意力模式/注意力权重的变化来解释幻觉的成因；
  3. 设计实验验证幻觉的**上下文间传播**（即注意力缺失是否会扩散到词汇上相似的其他上下文）。
- **一套缓解思路**：在训练后期重新引入少量已知知识，检查是否能恢复模型对关键实体的注意并缓解幻觉（**说明论文也包含一个初步的干预/修复实验**）。

> 注：论文本身是分析和解释类工作（Findings），不涉及新的模型架构或损失函数公式；其“方法”主要体现为数据构造策略与分析框架。

### 3. 实验设计

- **主要数据集/场景**：
  - 自行构建的 **Biography-Reasoning** 控制数据集，包含虚构人物实体及其多类型知识。
  - 任务类型：**知识问答**与**知识推理**。
- **Benchmark 设置**：
  - 对同一模型在多种数据构成下进行微调后，在统一构造的评估集上比较幻觉率（幻觉倾向）。
  - 对比条件包括不同新知识比例、不同被替换的知识类型等。
- **对比方法**：论文**不涉及与其他模型的基准对比**，更像是在同一模型内进行不同微调条件的**因果性对比与控制实验**。
- **其他实验维度**：
  - 测试幻觉在不同知识类型（如家族史 vs. 职业生涯 vs. 个人属性等）之间的传播差异；
  - 词汇相似上下文中注意力模式的传播行为检验；
  - 用“重新引入已知知识”作为一种干预措施，比较其前后幻觉率变化。

### 4. 资源与算力

- **说明**：从现有论文内容中**没有获取到训练所使用的 GPU 型号、数量或训练时长等硬件与算力信息**。
- 因此，该项信息目前**未明确公开**（通常此类分析性实验使用 LLaMA 等开源基座模型进行小规模微调，但本次总结中不能据此作确认性表述）。

### 5. 实验数量与充分性

- **实验体量**：
  - 从论文附图可见图表非常丰富（提取到约 51 张图、21 张表格），涉及不同微调条件、知识类型、注意力分析分布、传播检验、干预效果等。
  - 可以推断至少在**模型层面（≥1个基座模型的多设置微调）具有覆盖多种微调数据组合的系统性实验**。
- **充分性与客观性**：
  - **亮点**：由于采用完全虚构的受控数据，排除了预训练语料中知识污染的干扰，因此实验归因相对干净，变量控制科学。
  - **客观性**：评测指标为幻觉率/事实性指标，属于可客观衡量的范畴；多次重复设置下的对比过程逻辑清晰，结论建立在直接证据（注意力）和反事实（重新加回已知知识）之上。
  - **可质疑之处**：有效实验数量最终取决于基座模型的选择。从文本无法判断是否做了**跨多个主流开源基座模型或不同规模**的实验，因此在“单一模型上结论是否具有普遍性”层面存在局限。

### 6. 主要结论与发现

- **幻觉具有强蔓延性**：微调新知识造成的幻觉不仅严重损害新知识相关任务的正确性，还**向其他任务（包括既有知识问答和推理）蔓延**。
- **驱动因素并非整体比例**：当一个知识类型内部的数据**完全由新知识构成**时，模型幻觉倾向明显上升。说明与“整体新知识占比”相比，**某一知识类型内部的陌生程度**才是更强的幻觉驱动器。
- **机制根因：注意力弱化**：学习新知识会使模型在回答问题时**弱化对输入中关键命名实体的注意力**，转而过拟合到周边上下文模式，由此增大幻觉风险。
- **注意力缺失具有上下文传播性**：模型对关键实体注意力的减弱会从原始任务**传播到词法相似的其他情境**中，解释了幻觉为何不只局限于新知识任务。
- **后续数据能缓解**：在后期重新引入少量已覆盖的知识，能**有效修复模型的部分注意力**，并显著抑制幻觉行为——这为实践中复杂训练数据的配比策略提供了可操作的缓解思路。

### 7. 优点

- **控制变量设计严谨**：通过虚构实体数据集，成功隔离了内外知识的干扰，使“新知识效应”这一研究对象清晰化。
- **多维细粒度分析**：对知识类型维度与任务类型维度进行了交叉分析（如问答 vs. 推理），能定位幻觉的精确生成条件。
- **因果归因逻辑完整**：既用注意力数据进行机制层面的解释，又使用“减少幻觉的手段（重新引入已知知识）”进行了反向验证，使因果链条扎实。
- **关注幻觉的跨任务传播**：提出并验证了幻觉“溢出”效应，为将来研究新知识的副作用提供了新视角。

### 8. 不足与局限

- **依赖单一受控设置的可推广性有限**：虚构人物是一个偏理想化的场景，真实世界的领域知识以混合、交叠和复杂关联的方式存在，难以将结论一一复制到自然更新的知识库场景。
- **可能过度强调“知识类型内的全陌生”驱动**：该结论是否受人类概念中的知识类型边界所局限尚需验证；现实中的知识类型并非均有清晰分隔。
- **注意力机制的解释只是必要性而非充分性**：作者通过可解释性揭示了注意力弱化的关联，但并未做完整的因果扰动实验（如直接操纵注意力），是否需要模型内部状态之外的其它解释仍存问号。
- **算力与多模型对比信息缺失**：无法确认规律是否在多种规模或架构的模型稳定复现。
- **缓解方法简单**：重新引入已知知识的方法可操作性有限，实际流程中难以人工确定“何时重新引入”“比例多大”的效果边界。
- **评测以幻觉率为主，未深刻讨论输出保真度等其他质量维度**（如对已有知识是否发生完全“遗忘” vs. “遮蔽”）。

（完）
