---
title: "LexTime: A Benchmark for Temporal Ordering of Legal Events"
title_zh: LexTime：法律事件时间排序基准
authors: "Claire Barale, Leslie Barrett, Vikram Sunil Bajaj, Michael Rovatsos"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.280.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 法律事件时间排序基准，标注事件对时序关系
tldr: "案件分析、合规监测和法律摘要都需要准确重建事件时间线，但缺少专业法律语言上的时间排序评测。论文构建LexTime，从美国联邦起诉书中选取512个实例，标注事件对之间的时间关系。结果显示，LLM在法律事件排序上比叙事文本表现更好，最多高10.5%；更长输入与隐式事件对带来提升，隐式-显式事件对的准确率可达80.8%。该基准为法律领域时间理解提供了稀缺评测资源并提示上下文与隐式推理的重要性。"
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 779, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 705, \"height\": 348, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1454, \"height\": 362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 734, \"height\": 244, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 625, \"height\": 247, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1461, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 699, \"height\": 347, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1653, \"height\": 303, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1625, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 774, \"height\": 781, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp280/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 787, \"height\": 302, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp280/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1249, \"height\": 850, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp280/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 650, \"height\": 795, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp280/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1555, \"height\": 671, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp280/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1646, \"height\": 680, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp280/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1656, \"height\": 1148, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp280/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1642, \"height\": 2386, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp280/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1651, \"height\": 1352, \"label\": \"Table\"}]"
motivation: 法律场景中重建事件时间线很重要，但现有基准缺少法律语言的专门时序评测。
method: 从美国联邦起诉书构建512例事件对时序数据集LexTime，比较不同上下文与事件类型下LLM排序能力。
result: LLM法律事件排序优于叙事文本；长上下文和隐式事件显著提高相对排序准确率。
conclusion: LexTime为法律事件时间推理提供了基准，启示应更重视上下文与隐式事件建模。
---

## Abstract
Understanding temporal relationships and accurately reconstructing the event timeline is important for case law analysis, compliance monitoring, and legal summarization. However, existing benchmarks lack specialized language evaluation, leaving a gap in understanding how LLMs handle event ordering in legal contexts. We introduce LexTime, a dataset designed to evaluate LLMs’ event ordering capabilities in legal language, consisting of 512 instances from U.S. Federal Complaints with annotated event pairs and their temporal relations. Our findings show that (1) LLMs are more accurate on legal event ordering than on narrative texts (up to +10.5%); (2) longer input contexts and implicit events boost accuracy, reaching 80.8% for implicit-explicit event pairs; (3) legal linguistic complexities and nested clauses remain a challenge. While performance is promising, specific features of legal texts remain a bottleneck for legal temporal event reasoning, and we propose concrete modeling directions to better address them.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

**题目**：LexTime：法律事件时间排序基准（LexTime: A Benchmark for Temporal Ordering of Legal Events）

**会议**：Findings of EMNLP 2025

---

## 一、核心问题与研究动机

- **问题背景**：在案件分析、合规监测与法律摘要等法律 NLP 任务中，准确理解事件间的时序关系、重建事件时间线至关重要——它直接影响责任认定、义务判断与程序有效性评估。然而，现有时间推理基准均聚焦于通用文本或叙事文本（如 EVENT STORYLINE CORPUS、TRACIE、TimeQA 等），缺少针对法律专业语言的时序排序测评资源。
- **核心研究问题**：大规模语言模型（LLM）在处理法律文本中特有的事件结构时表现如何？它们在法律语境下的事件排序能力与叙事文本相比是否存在差异？哪些法律语言特征构成瓶颈？
- **整体意义**：该工作是首次系统性地针对法律文本中的事件时序排序进行基准测试，填补了法律时间推理评测的空缺，为下游法律 NLP（摘要、问答、起草等）提供基础支撑。

---

## 二、方法论

### 2.1 基准数据集 LexTime

- **数据来源**：从美国联邦起诉书（U.S. Federal Complaints，2020–2024）中随机采样劳动法相关案件（Nature of Suit 代码以 7 开头），共构建 **512 个实例**（257 个正例 / 255 个负例）。
- **实例结构**：每个实例包含：
  - 一个上下文段落（平均 172 个 token）
  - 一对事件（可为显式-显式或显式-隐式配对）
  - 一个查询三元组 {事件A, 时间关系, 事件B}
  - 一个二分类标签（yes/no）
- **标注构建流程**：
  1. 使用 Mistral-Large-Instruct-2407 采用 **prompt-chaining** 方法生成预标注（分三步：提取段落→识别隐式事件→构造时序关系句）
  2. 人工审核全部 512 个实例，修正了 23.24% 的错误标签（54.55% 为时序关系错误，37.87% 为事件提取错误，7.58% 为两者兼有）
- **时间关系设计**：简化 Allen 区间关系为三类——**Precedes/Before**、**Simultaneous**、**Follows/After**。选择三类的原因：①法律推理中主要依赖先后顺序与因果关系；②Finer-grained 关系的边界模糊易错；③与 TRACIE 数据集对齐以便对比。

### 2.2 评估方法

- 两种提示策略：**标准提示（Standard prompting）** 和 **思维链提示（CoT prompting）**
- 三种示例设置：**零样本（ZS）**、**一样本（1S）**、**少样本（FS，3 个示例）**
- 评测指标：准确率（accuracy），每组实验三次运行取平均

---

## 三、实验设计

### 3.1 数据集与对比基准

- **目标数据集**：LexTime（法律文本，512 实例）
- **对照数据集**：TRACIE（叙事短文，从中随机选 512 实例），与 LexTime 的任务设计高度相似，将原蕴含任务改为相同的问答格式后对比

### 3.2 评测分组

- 按上下文长度分组：**短上下文**（<150 token，230 段）vs **长上下文**（>150 token，282 段）
- 按事件类型分组：**显式-显式事件对**（288 对）vs **显式-隐式事件对**（210 对）+ 隐式-隐式（14 对）

### 3.3 对比模型

- 专有模型：GPT-4o、GPT-4 Turbo
- 开源/开放模型：Mistral-Large-Instruct-2407（123B）、LLaMA 3.1 70B/8B、LLaMA 3.2 3B/1B（含 instruct 和 base 版本）、Flan-T5-large（780M）

---

## 四、资源与算力

- 论文在附录注明使用了以下 GPU 资源：**Nvidia Tesla V100-SXM2、Tesla K80、A100（40GB/80GB）、RTX A6000（40GB）**。
- 论文利用了**爱丁堡计算与数据设施（ECDF）**和**爱丁堡国际数据设施（EIDF）**。
- **未明确说明**：具体 GPU 数量、模型推理/评估的总时长、以及 API 调用成本等细节并未给出。

---

## 五、实验数量与充分性

### 实验规模
- **大量组合实验**：对 11 个模型 × 5 种提示设置（ZS/1S/FS/CoT-1S/CoT-FS）× 2 个数据集 × 5 个子集（全量/长/短/显式对/显式-隐式对）进行了系统评测，构成较为全面的矩阵。
- **错误分析**：额外对 GPT-4、GPT-4 Turbo、LLaMA 3.1 70B 的 100 个错误预测进行了人工归因分析，并与数据集整体语言特征对比（如 +89% 的释义偏差、+84% 的从句偏差等）。

### 充分性与公正性评估
- **充分维度**：模型覆盖了从 780M 到 123B 的规模梯度，包含专有与开源模型，且对每个模型使用完全相同的提示模板与示例数量；提供 1S/FS 的 CoT 对比，能有效检验不同推理策略的影响。
- **客观欠缺（TRACIE 比较方面）**：LexTime 的上下文段落由**三段原始文本拼接**而成（平均 172 token），而 TRACIE 的段落自带隐式事件相关标注；二者的数据构建过程与难度基线不完全对齐，直接比较时需谨慎归因。作者提出的"LexTime 中有更精确时间线索（如具体日期）"的解释只覆盖部分差异。

---

## 六、主要结论

### 1. 法律文本的事件排序优于叙事文本
- GPT-4o 在 FS 设置下在 LexTime 上比 TRACIE 高 **+10.5%**；GPT-4 系列与 LLaMA 3.1 70B 同样多数场景在 LexTime 上占优。原因可能在于法律文本含有更明确的时间锚点（如具体日期、法定期限表达）。

### 2. 上下文长度的作用具有模型依赖
- 大模型（GPT-4 Turbo、GPT-4o 等）从**长上下文**中获益最多（GPT-4 Turbo 在 FS 长上下文中达 79.9%，最多提升 3.5%）；
- 中小型模型（Mistral 123B、LLaMA 8B 等）在**短上下文**中表现更好（Mistral 123B 短上下文 FS 达 77.8%，提升 7%）。

### 3. 隐式事件有助于推断
- GPT-4 Turbo 在**显式-隐式事件对**上达到最高准确率 **80.8%**，比全量平均高 3.2%，比显式-显式事件对高 2.6%。原因可能是隐式事件紧邻显式事件的位置约束有助于模型推理。

### 4. CoT 提示无效甚至有害
- CoT prompting 在 LexTime 上导致准确率下降（FS 设置下降 3.4%，1S 设置下降 3.2%），在 TRACIE 上同样无效。作者推测长提示稀释注意力所致。

### 5. 法律语言中的特定语言现象是主要错误来源
- 错误样本高度集中在：**释义表达（+89%）**、**从句内事件（+84%）**、**非一般过去时事件（+63%）**、**被动结构（+24%）**、**否定/将来推测表达（+12%）** 等方面，说明法律文本特有的句法/话语特征仍是时序推理的关键瓶颈。

---

## 七、优点

1. **填补空白**：第一个针对法律事件时间排序的基准数据集，既有理论贡献也有实用价值。
2. **特征驱动分析**：从词汇、句法、话语层面对比法律语言与叙事语言，量化差异（如拼写日期密度比叙事高 10.28 倍、名词化事件高 50.4%、被动语态高 24.76%、事件密度差异等），为后续建模指明了方向。
3. **前瞻性研究框架**：对标准提示 vs CoT 提示、上下文长度、隐式/显式事件等维度做系统消融，提供了可操作的配置指导（如实际部署时：大模型用长上下文、小模型用短上下文）。
4. **规模化的模型评估范围**：覆盖从 780M 到 123B 的开源与专有模型，结论的稳健性有一定保证。
5. **可视化结构清晰**：每类实验均给出三次平均数值，附数据集构建提示与评估提示，方便复现与扩展。

---

## 八、不足与局限

1. **数据规模较小且来源面窄**：只有 512 个实例，且仅覆盖劳动法的联邦起诉书文本；结论在不同法域（如合同、刑法）和不同法律文书类型中的泛化能力尚不明确。
2. **事件注释类型不完整**：事件触发词只限定为动词，忽略了法律文本中高频的名词化事件（nominalized events）；而名词化恰恰是法言法语的典型结构（正文错误分析图也含 noun-events 相关统计），留下重要盲区。
3. **时间关系分类过粗**：只有三种关系（Before/Same/After），无法评估更细粒度的时间重叠、包含、相接等关系，限制了基准的可扩展性。
4. **隐式事件的标注依赖 LLM，存在“伪时序关联”风险**：部分隐式事件由大模型推得并以相邻显式事件为参照标注，可能出现循环注释——即隐式事件与显式事件的紧邻关系导致显式-隐式对更容易预测，但实际模型只是利用了距离，而不是真正推理了时序关系。
5. **评估仅限英文文本**，未呈现多语言的法律文本场景的适用性。
6. **CoT 的提示设计局限**：文章未尝试“让模型先定位事件再比较时间”等更结构化的 CoT 变体，因此“CoT 对时序排序无效”这一强结论的普适性有待进一步验证。
7. **计算资源细节不透明**：未报告各模型的运行时间、API 成本和能耗，可能影响该基准在资源受限环境下的实用性。

---

（完）
