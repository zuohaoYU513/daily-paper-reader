---
title: Transferable and Efficient Non-Factual Content Detection via Probe Training with Offline Consistency Checking
title_zh: 通过离线一致性检查的探针训练实现可迁移且高效的非事实内容检测
authors: "Xiaokang Zhang, Zijun Yao, Jing Zhang, Kaifeng Yun, Jifan Yu, Juanzi Li, Jie Tang"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.668.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 基于离线一致性检查训练探针模型检测非事实内容
tldr: 已有非事实内容检测常需在线生成多份回答做一致性验证，计算开销大且依赖人工标注。作者提出PiNose，利用离线自洽性检查结果训练探针模型，从而无需额外标注并能在不同数据分布间迁移。它还在回答解码之前检视模型内部状态，更早识别事实性错误。在事实性检测和问答基准上，PiNose超越了已有事实性检测方法，兼具高效性与可迁移性。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long668/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1602, \"height\": 750, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long668/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1490, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long668/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 509, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long668/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1634, \"height\": 514, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long668/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 758, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long668/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long668/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 632, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long668/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long668/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 504, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long668/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long668/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 809, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long668/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1581, \"height\": 705, \"label\": \"Table\"}]"
motivation: 减少非事实内容检测对人工标注的依赖，并降低在线一致性验证带来的推理开销。
method: 用离线自洽性检查结果训练探针，并利用解码前内部状态判断事实正确性。
result: 在事实性检测与问答基准上超越现有方法，无需人工标注且迁移成本低。
conclusion: 离线一致性探针训练提供了一种轻量、可迁移的事实性检测途径。
---

## Abstract
This paper proposes PiNose, which trains a probing model on offline self-consistency checking results, thereby circumventing the need for human-annotated data and achieving transferability across diverse data distributions. As the consistency check process is offline, PiNose reduces the computational burden of generating multiple responses by online consistency verification. Additionally, it examines various aspects of internal states prior to response decoding, contributing to more effective detection of factual inaccuracies. Experiment results on both factuality detection and question answering benchmarks show that PiNose achieves surpassing results than existing factuality detection methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

**研究背景**

- 大语言模型在预训练后展现出较强的知识生成能力，但仍频繁产生与事实不符的内容，即"非事实内容"或幻觉。
- 检测生成内容的真实性是提升其可信度的核心问题，也是长线研究目标。

**已有方法的不足**

- **基于探针（Probing）的检测**：依赖人工标注的问答标注集训练，如 SAPLMA、RepE。这些标注使得模型难以迁移到分布外（Out-of-Distribution）的数据上，在新领域/新问法下性能大幅下降。
- **在线自洽性检查（Online Self-Consistency Checking）**：如 SelfCheckGPT，尽管不需要标注，但需在推理时为每个问题即时多次采样模型输出，引入很高的计算负担；同时它没有利用训练过程，泛化稳健性有限。

**PiNose 解决的矛盾**

- 如何*同时*实现：免人工标注、跨分布迁移、高检测精度、低推理开销。核心诉求是把自洽性检查的强大能力从在线环节转移到离线训练阶段，再通过探针在单次前向中完成检测。

## 2. 论文提出的方法论

### 2.1 核心思想

> PiNose 将"生成多个响应 + 一致性检查"这一原本在推理期执行的耗时过程，离线地构建成带伪标签的训练数据集，并用该数据集训练轻量级探针模型。在线推理时只需一次前向，提取 LLM 内部隐藏表示即可输出事实性判断。

关键假设：LLM 的内部表示中含有关于其输出是否事实的线索，该线索可以从中间层表示中通过探针解码；而一致性检查结果可以近似作为事实的监督信号（符合自洽性原理）。

### 2.2 三阶段流程

**阶段一：数据准备**

- **问题自举（Question Bootstrapping）**：人工标注少量种子问题（Seed Questions），通过上下文学习让 LLM 自动生成大规模多样问题，并不断引入已生成问题来扩大种子池。
- **多样化响应生成**：使用较高采样温度（t = 1）并搭配 5 种不同的提示模板，为同一问题采样多个回答，得到数据集 {(q, {r_i})}。

**阶段二：离线一致性检查**

- **评审收集（Review Gathering）**：将同一问题的多个回答进行*两两对比*，让 LLM 以"Consistent / Neutral / Non-Consistent"的三分类形式做评审。
- **评审富化（Review Enrichment）**：同一次两两比较使用多组（文中 N 组）不同上下文示例的 ICL 提示反复征求评审意见，对齐"多评委"设定。
- **集成与过滤**：
  - Neutral 视为弃权；
  - 在 `N` 轮评审间做多数投票，再在 `k-1` 个两两对比对上做多数投票；
  - 若无任何类别得票过半，则视为争议样本并剔除，保证数据质量；
  - 最后得到带伪标签数据集 {(q, r_i, f_i)}。

**阶段三：探针构建**

- 探针结构：双层前馈网络（公式 1），Sigmoid + 非线性函数组合，以隐藏表示为输入，输出 `P(True)`，公式如下：

```
Probe(H^{(l)}[i]) = σ₂( W₂ σ₁( W₁ H^{(l)}[i] + b₁ ) + b₂ )
```

- 输入构造：将问题与回答拼接成模板输入 LLM；
- 特征提取：取*中间层*（层数为总层数一半处）LLM 的 FFN 输出的隐藏表示中*最后一个标记*的表示 `H^{(l)}[i]`；
- 训练方式：冻结 LLM 全部参数，只训练探针，优化交叉熵损失；
- 推理时，LLM 只生成/解码一次回答，探针即时判断，无需采样多个响应。

## 3. 实验设计

### 3.1 数据集与评测场景

| 测试集 | 类型 | 说明 |
|---|---|---|
| True-False | 事实性检测基准 | LLM 生成陈述句 + 人工事实性标注，q=∅（纯断言型），含训练集与测试集 |
| NQ（Natural Questions） | QA 变体 | 从原问答数据集抽样 1,000 问，用 Llama2-7B 生成回答，人工对照标准答案标注 |
| TriviaQA | QA 变体 | 同上，1,000 问 |
| WebQ | QA 变体 | 同上，1,000 问 |

**训练数据规模**：PiNose 训练集 20,000 条三元组；True-False 中基于监督的基线用 5,000 条人工标注训练数据。

### 3.2 对比方法

- **探针类基线**：SAPLMA（监督探针）、RepE（PCA 表示方向法）；
- **一致性检查基线**：SelfCheckGPT-NLI（BERT NLI 做语义一致性）、SelfCheckGPT-Prompt（LLM 提示做一致性检查）；
- **基于置信度基线**：Perplexity-AVE、Perplexity-MAX、It-is-True 概率比较法。

### 3.3 评测指标

- AUC（受试者工作特征曲线下面积）为主指标；
- ACC（准确率）为辅助指标。

### 3.4 主要实验内容

1. **主实验**（在所有四个测试集上与全部基线做对比）
2. **跨模型评估**（实验组 1–5：组合 Llama2-7B/13B 与 Mistral-7B 在数据制备、一致性检查、事实检测三阶段）
3. **数据分布消融**（同分布自问、跨数据集外部问题、自举生成问题三种训练数据来源的比较）
4. **一致性检查消融**（评审轮数 N ∈ {1,3,5,7} 与回答数量 k 的交叉影响）
5. **探针构建消融**（不同层表示、平均 token vs 最后 token）

## 4. 资源与算力（文中说明情况）

- 论文对各阶段的 GPU 型号、数量、具体训练时长等**均未给出明确量化信息**；
- 文中提供了推理效率对比数据：**每个实例的平均检测时间**
  - PiNose：约 0.024 秒
  - SelfCheckGPT-NLI：2.05–2.53 秒
  - 即 PiNose 在在线推理阶段有约百倍的耗时优势；
- 论文同时承认*离线管线*需要大量 LLM 推断（生成问题、生成响应、执行多次评审），构建成本较高，但可通过多次线上使用摊薄。

## 5. 实验数量与充分性

**实验规模与变体覆盖**

- 主实验：4 个测试集 × 9 组方法，覆盖概率型、探针型、一致性型、置信度型四类范式，对比充分；
- 跨模型实验：3 个不同检测目标（Llama2-7B、Llama2-13B、Mistral-7B）在两两组合下的 5 组设置，且在 NQ、TriviaQA、WebQ 上均重复验证；
- 数据分布消融：3 种问题分布来源对 3 个 QA 集的影响；
- 一致性检查消融：4 × 4 组参数组合的研究；
- 层选择实验：逐层扫描 32 层隐藏表示的 AUC 曲线。

**充分性评价**

- 不同模块（数据制备、一致性检查、探针结构）都有独立的消融实验，归因清晰，覆盖面较完整；
- 客观上**较为充分**：对方法的每一设计决策均有相应实验支撑；
- 公平性尚可：与探针类基线采取了相同的层选择/训练方式下的"训练集来自 True-False"，与一致性检查基线使用了相同的 9 个响应采样数；但**未给出多次运行的统计显著性检验**（如方差）是瑕疵；
- 实验模型以开源模型为主，没有验证 GPT-4/Claude 级别的大规模 API 模型上的表现。

## 6. 论文的主要结论与发现

1. **主导性能**：PiNose 在三个 QA 测试集上相较监督探针基线（RepE、SAPLMA）提升显著（AUC 约 7.7–14.6 个点），尽管零人工标注；
2. **超过在线一致性检测**：相较 SelfCheckGPT-NLI/Prompt，PiNose 在 NQ、TriviaQA、WebQ 上约提高 3–7 个 AUC 点，同时推理时间从秒级降到 0.024 秒量级；
3. **自洽性与事实性正相关**：无监督的一致性基线超越监督探针，验证了自洽性原则的可靠性，而 PiNose 通过训练探针进一步继承了该优势；
4. **跨模型的迁移能力**：由 Llama2-7B 产生的自动标注训练数据可直接用来训练其他 LLM（更大规模或不同架构）的事实性探针，检测目标从 7B 换到 13B / Mistral-7B 时几乎不掉点；
5. **生成问题优于同分布外部问题之外的"外部题"来源**：即使外部题数量是生成题的 5 倍，用少量生成题训练就能达到可比甚至更优的效果——说明问题的**多样性**比分布一致性对探针迁移更重要；
6. **中间层 + 最后一个标记是最优探针配置**：性能随层递增先升后降，中点层最优。

## 7. 优点与亮点

- **无需人工标注的真实性探针**：借助自举数据 + 离线一致性检查，把成本从"在线多次生成"转移到"离线一次性构建"，有效平衡了准确率与推理开销；
- **良好的迁移性**：训练数据完全自动化，且不绑定特定分布；跨数据集、跨模型均有出色的迁移表现；
- **从生成文本前内部状态获取信号**：用中间隐藏表示而非离散 token 做预测，信息量更丰富、检测更准；
- **方法简洁、成本低、易复现**：探针是轻量双层网络，LLM 冻结，在线检测仅需单次前向；代码与数据公开；
- **实验逻辑完整**：三个阶段均有逐一对应消融，结论在多个维度上相互印证。

## 8. 不足与局限

- **离线构造开销较大**：数据制备阶段需大量 LLM 推断生成问题、响应及多轮评审，成本集中在训练前阶段；
- **仅适用于开源 LLM**：探针依赖从 LLM 内部层隐藏表示提取特征，不适用于只暴露输出的闭源 API 模型，限制了实用性覆盖范围；
- **事实性错误的定义偏窄**：目前只检测"对问题/断言的事实性错误"，未涉及逻辑谬误、推理漏洞、有害内容等其他错误类型；
- **同模型实施策略可能引入偏差**：数据生成、一致性评审、最终检测由同一 LLM 完成，虽然论文将其解释为增强迁移性的一致设计，但也可能存在系统性偏差的隐患；
- **实验规模局限**：评测集中于 Llama2-7B、13B 和 Mistral-7B 三个 open-sourced 中等规模模型，最大的检测目标只有 13B，缺乏更大规模模型的验证；
- **对抗性问题**：论文自身承认方法可能被用于对抗学习——LLM 若能感知探针特征，可能优化出更隐蔽的非事实内容，逃避检测。

（完）
