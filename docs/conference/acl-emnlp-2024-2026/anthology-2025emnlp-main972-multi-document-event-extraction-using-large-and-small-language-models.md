---
title: Multi-Document Event Extraction Using Large and Small Language Models
title_zh: 利用大型与小型语言模型进行多文档事件抽取
authors: "Qingkai Min, Zitian Qu, Qipeng Guo, Xiangkun Hu, Zheng Zhang, Yue Zhang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.972.pdf"
tags: ["query:evidence-qa"]
score: 7.0
evidence: 多文档事件抽取需要处理长上下文和复杂事件结构，并提供新基准与聚合评测指标
tldr: 多文档事件抽取能从不同来源聚合事件信息，但现有研究很少，且需处理长上下文和复杂事件结构。论文提出大模型与小模型协作的框架：大模型负责多步推理，微调小模型承担关键子任务，共同引导抽取过程；同时构建新基准与聚合事件评测指标。实验表明该框架在长程多文档事件聚合上具有优势，为该方向提供了基础设施。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main972/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main972/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main972/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1660, \"height\": 617, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main972/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 790, \"height\": 401, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main972/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main972/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1621, \"height\": 674, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main972/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1618, \"height\": 752, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main972/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1398, \"height\": 1283, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 813, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 817, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 659, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 814, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 765, \"height\": 1281, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1665, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 801, \"height\": 847, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 814, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 506, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 504, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 464, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1663, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main972/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1661, \"height\": 432, \"label\": \"Table\"}]"
motivation: 多文档事件抽取可聚合多源事件，但长上下文与复杂事件结构使其研究不足。
method: 提出大模型多步推理和小模型关键子任务协作的抽取框架，并建立新基准和聚合评价指标。
result: 实验验证该协作框架在长上下文多文档事件聚合场景下效果良好。
conclusion: 大小模型分工加定制评测可推动多文档事件抽取研究。
---

## Abstract
Multi-document event extraction aims to aggregate event information from diverse sources for a comprehensive understanding of complex events. Despite its practical significance, this task has received limited attention in existing research. The inherent challenges include handling complex reasoning over long contexts and intricate event structures. In this paper, we propose a novel collaborative framework that integrates large language models for multi-step reasoning and fine-tuned small language models to handle key subtasks, guiding the overall reasoning process. We introduce a new benchmark for multi-document event extraction and propose an evaluation metric designed for comprehensive assessment of multiple aggregated events. Experimental results demonstrate that our approach significantly outperforms existing methods, providing new insights into collaborative reasoning to tackle the complexities of multi-document event extraction.

---

## 论文详细总结（自动生成）

## 一、论文核心问题与整体含义

### 研究动机

- 多文档事件抽取旨在从多个信息来源中聚合和融合事件知识，形成关于复杂事件全局性、完整性的结构化表示。
- 随着事件抽取从句子级、文档级向跨文档/多文档级演进，如何将不同来源之间相互补充的信息（如精确时间、伤亡人数、位置细节等）整合为一个规范且一致的“多文档事件”（Multi-Document Event），成为关键问题。
- 现有研究对此关注不足，主要挑战在于：
  - **长上下文**下的复杂推理；
  - 多文档间**表达不一致**（术语/措辞/细节冗余）；
  - 事件数量庞大，**跨文档事件与参数共指**聚合困难；
  - 对模型推理能力要求高，难以通过单一序列生成完整事件链。

### 整体含义

- 本文首次正式面向“多文档事件抽取”构建了新型基准数据集 ECB++，提出配套的聚合评测指标 CEAF-MEE，并提出一套**大语言模型（LLM）与小型语言模型（SLM）协作的抽取框架**，在长上下文、多事件聚合场景中验证了有效性。

---

## 二、方法论

### 核心思想

- 将任务分解为关键子任务，由 **fine-tuned SLM** 负责处理局部高效、可微调的子任务（提取候选结构）；由 **LLM agent** 在全局层面进行**多步启发式推理**，通过整合 SLM 提供的结构化中间结果和原始文本上下文，实现事件组合、参数对齐与最终规范化——即“大小模型分工协作”。

### 流水线子任务分解（SLM 部分）

1. **Event Trigger Detection**：识别文档中的事件触发词；
2. **Cross-Document Event Coreference Resolution**：对跨文档的事件触发词进行聚类，形成初始事件簇；
3. **Document-Level Event Argument Extraction**：针对单文档内每个触发词，提取其参数（如时间、地点、人物对象等）；
4. **Cross-Document Argument Coreference Resolution**：对参数提及进行跨文档的共指消解聚类；
5. **Event Canonicalization**：为每个事件簇选择规范触发词并聚合规范参数，得到最终的多文档事件表。

### LLM 多步推理的两个阶段

- **阶段一：事件组合（Event Composition）**
  - 将多文档事件组成问题建模为**组合空间上的启发式搜索**；
  - 步骤1.1（**Event-to-cluster assignment**）：对候选文档级事件与已有事件簇“逐事件比对”，LLM 按*上下文、触发词同义性、参数重叠*进行 1~5 的离散相关打分；超过阈值并入对应簇，否则新建簇；
  - 步骤1.2（**Argument alignment**）：事件加入簇后，逐参数与簇内已有参数簇比对语义等价性与共指线索，合并或新建参数簇；
  - 利用 SLM 预测结果做**候选簇缩减**（核心事件种子初始化、触发词近似分组），提升搜索效率。
- **阶段二：事件归一化/巩固（Event Consolidation）**
  - 对阶段一形成的簇，由独立 LLM agent 进行簇级推理：
    - **trigger selection**：从多个候选触发词中选取一个规范触发词；
    - **argument consolidation**：逐簇判断参数的语义相关性与去冗余性，保留且仅保留相关、互不冗余的参数，并为每个参数簇选出规范提及。

### 评测指标 CEAF-MEE

- 扩展自 CEAF-REE；用**两级二分图匹配**来对齐预测事件与参考事件：
  - 第一级：事件级最优匹配（基于触发词与参数的综合相似度）；
  - 第二级：事件内参数级匹配（基于跨度重叠）；
  - 支持精确匹配（exact）和头部词匹配（head match）两种评测粒度，综合给出 Precision/Recall/F1。

---

## 三、实验设计

### 基准数据集

- **ECB++**：在 ECB+（Event Coreference Bank Plus）基础上扩展文档级事件参数标注（参照 FrameNet 框架），保留原有事件/实体跨文档共指链。
- 规模：982 篇新闻文章 / 43 个主题；每主题 20–25 篇文档；事件分为仅单文档提及和跨文档多篇提及两类；
- 划分：25 个训练主题、8 个开发主题、10 个测试主题；
- 标注一致性 IAA = 83.4%。

### 对比方法

1. **Pipeline + SLM SFT**（BERT/RoBERTa/BART 微调，各子任务模块化）
2. **Pipeline + LLM ICL**（每个子任务用专门 prompt 驱动 LLM）
3. **Seq2seq + LLM SFT**（直接端到端生成最终事件表，基于 Qwen3-14B 微调）
4. **Seq2seq + LLM ICL**（DeepSeek-V3，几示例引导直接输出）
5. **本文协作框架（Our Collaborative）**
   - SLM 流水线 + 两个 LLM 推理阶段（DeepSeek-V3）

### 评价方式

- 主评测：CEAF-MEE（exact match 与 head match）
- 附加分析：**解耦评测**（仅评测事件共指 / 仅评测参数合并）、**逐模块消融**（去掉 stage1.1 / 1.2 / stage2 等）、**自洽性分析**、**Chat vs Reasoning 模型对比**、**模型规模对比**（Qwen3-8B vs 14B）。

---

## 四、资源与算力

- **SLM管线**：单张 NVIDIA V100 可运行，各模块训练数小时，整条流水线可在十几小时内完成。
- **协作框架（本文方法）**：在 SLM 基础上增加 LLM 多步推理；总耗时约 12 小时内（取决于 DeepSeek API 性能）。
- **Seq2seq LLM SFT**：在 **8 张 NVIDIA 80GB A100 GPU** 上训练 14B 模型，时长数小时。
- **LLM ICL 型方法**：使用 DeepSeek API，耗时从数小时到约十几小时不等。
- 运行细节：ICL 实验均运行三次取平均，temperature = 0。
- 局限说明：因 GPU 显存限制，未微调更大模型（如 Qwen3-32B）。

---

## 五、实验数量与充分性

### 实验组数概览

- 主实验（表2）：4 类基线 vs 本文方法，分别报告 exact match 与 head match 下的 P/R/F1；
- 消融实验（表3）：完整模型 vs 去除 stage1.1 / 去除 stage1.2 / 去除 stage2 / 同时去除 stage1.2 & stage2 多个变体；
- 解耦评测（图4）：区分“事件共指”与“参数合并”两个维度，验证错误来源；
- 扩展实验（表4、图5）：
  - 自一致性投票策略对比；
  - DeepSeek-V3（chat） vs DeepSeek-R1（reasoning）作为推理骨干；
  - Qwen3-8B vs Qwen3-14B 作为 seq2seq SFT 骨干；
- 附录附加案例分析（D1/D2/D3 等），并提供了人工可见的推理轨迹说明。

### 充分性与客观性评估

- **优点**：评测维度较全面，同时使用 exact 与 head match，能够同时衡量事件共指与参数合并，考虑了 recall/precision 的分解；自一致性和骨干模型对比等能揭示模型行为；
- **不足**：
  - 仅在单一数据集（ECB++/ECB+）上进行完整实验，跨数据集泛化性未验证；
  - 未与最新大规模事件抽取模型或更大参数模型的 seq2seq 结果进行对比（如未微调 Qwen3-32B/更大模型）；
  - 模型推理输出由 API 驱动，实验中 DeepSeek API 性能会带来环境噪音；
  - 实验任务中部分“单文档事件”与“多文档事件”并存，评估指标和统计检验的细节可以更透明。

---

## 六、论文主要结论与发现

1. **Pipeline 优于 Seq2seq**：在 SFT 下 pipeline 的 exact F1 比 seq2seq 高 10%，ICL 下高 4.3%，表明将多文档事件任务显式分解为子步骤更符合其复杂结构。
2. **SFT 远优于 ICL**：SFT 相比 ICL 在 pipeline 设置下 exact F1 高 23.1%，在 seq2seq 设置下高 18.4%，说明仅有少量示例不足以刻画任务的复杂约束。
3. **协作框架效果显著**：本文方法在 exact/head F1 上分别是 41.2%/47.6%，超越所有基线（SLM pipeline 35.6/41.6；LLM seq2seq SFT 26.6/32.7）。
4. 消融显示：**事件至簇分配（stage1.1）贡献最大**，而去除后 head F1 下降约 5%；参数跨文档对齐（1.2）与簇级参数归一化（stage2）也有独立贡献。
5. 解耦分析显示：任务整体分数远低于单独“共指”和单独“参数合并”得分，说明联合多事件对齐是真正难点，而该方法在共指与参数合并两端均有提升。
6. **自一致性策略收益很小**；使用 DeepSeek-R1（reasoning 模型）反而略差于 DeepSeek-V3（chat 模型），可能是任务内部逻辑与模型推理风格不匹配。
7. 单纯增大模型规模（8B→14B）并未带来等比例提升，说明任务难点更多在于**结构化与跨文档推理**而非模型参数量。

---

## 七、优点

- **任务设定新颖且实用**：多文档事件抽取相较于文档级事件抽取更接近真实新闻信息整合场景，研究价值高。
- **数据贡献扎实**：ECB++ 在广泛使用的 ECB+ 上进行细粒度文档级参数标注，并保留跨文档事件/实体共指链，可直接复用对比；
- **评测指标设计有针对性**：CEAF-MEE 通过两级最优匹配同时评价事件匹配和参数匹配，避免单纯依赖触发器匹配导致的评价失真；
- **方法设计合理且模块化**：SLM 捕捉局部语义、LLM 进行全局多步推理的混合架构，在子任务精确度和全局上下文推理之间取得较好平衡；
- **具备可解释性**：LLM 在每个推理步骤中输出显式 rationale，便于错误分析和结果审查；
- **报告了详尽消融与案例分析**，对组件贡献的剖析较细腻；
- 代码与数据开源，可复现性强。

---

## 八、不足与局限

- **依赖 SLM 中间结果**：SLM 错误（例如参数抽取 F1<70%，事件共指 F1<80%）会在后续阶段传播，限制整体上限。
- **角色分工相对固定**：SLM 负责局部、LLM 负责全局的逻辑，缺少 LLM 介入局部纠错或反向指导 SLM 微调的动态协同机制。
- **仅有一个评估数据集**：ECB++ 基于新闻英文语料，若推广到中文、低资源领域或更多风格文档，效果尚未验证。
- **评测指标局限**：主要基于跨度的匹配，未引入语义等价/指称是否跨句可推断等维度；gold 事件表的完整度对标注重叠度敏感。
- **计算资源未完全交代**：仅提及 SLM 在 V100、seq2seq SFT 在 8×A100 80GB 上完成；未给出 LLM API 调用次数、token 用量或各环节详细时间。
- **外部 API 的公平性**：LLM 相关实验依赖 Close-source 服务（DeepSeek API），随机性和模型更新可能导致结果难以完全复现；
- **模型规模上限**：由于显存限制未训练/评估 32B 级模型，无法验证更大规模模型在 seq2seq SFT 上的表现趋势；
- **自一致性提升有限**，说明现有投票 prompt 不够对抗本任务中的细粒度歧义，仍需改进。

（完）
