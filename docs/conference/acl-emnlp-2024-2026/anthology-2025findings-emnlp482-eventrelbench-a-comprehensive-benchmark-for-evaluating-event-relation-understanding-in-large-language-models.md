---
title: "EventRelBench: A Comprehensive Benchmark for Evaluating Event Relation Understanding in Large Language Models"
title_zh: EventRelBench：大语言模型事件关系理解的综合基准
authors: "Jie Gong, Biaoshuai Zheng, Qiwang Hu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.482.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 面向LLM的事件关系理解基准，含时序/因果等文档级关系评测
tldr: 现有研究尚未系统评估大语言模型理解事件关系的能力。本文设计EventRelBench，包含3.5万个事件关系问题，覆盖共指、时序、因果与隶属四类关系，并同时提供句级和文档级两种粒度的评测。该基准可揭示模型在跨句事件关系理解上的薄弱环节，为事件关系抽取、篇章理解与时序感知模型的改进提供可复用的评估资源。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp482/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp482/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1496, \"height\": 516, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1493, \"height\": 916, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1247, \"height\": 925, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 698, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 833, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 834, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1481, \"height\": 1599, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp482/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 552, \"height\": 362, \"label\": \"Table\"}]"
motivation: 大语言模型虽在多种任务表现优异，但缺少系统评估其对事件关系尤其是文档级关系理解能力的基准。
method: 构建含35K问题的事件关系基准，覆盖四类核心事件关系并为之设计句级和文档级两种粒度评测。
result: 在多种大语言模型上评测后，揭示了文档级事件关系理解上的不足，为后续方法提供基准。
conclusion: 为事件关系抽取与理解提供标准化评估套件，支持时序、因果等方向的系统研究。
---

## Abstract
Understanding event relationships is critical for tasks such as narrative comprehension, information extraction, and reasoning in natural language processing. Despite the remarkable advancements of large language models (LLMs) across diverse NLP tasks, current studies have not systematically evaluated their ability to capture the complex of event relations. To this end, we aim to assess LLMs on event relationship extraction (ERE) by designing the benchmark EventRelBench. EventRelBench comprises 35K diverse event relation questions covering four key categories—coreference, temporal, causal, and supersub relations. These questions are provided at two levels of granularity: document-level and sentence-level. Extensive experiments on different sizes and types of LLMs show that existing LLMs still fall short in accurately extracting and understanding event relationships. To address this gap, we introduce EventRelInst, a 48K instruction fine‐tuning dataset in the event relation extraction domain. Experimental results not only highlight the shortcomings of current general-purpose LLMs in extracting event relationships but also demonstrate the effectiveness of EventRelInst. Both EventRelBench and EventRelBench will be publicly available.

---

## 论文详细总结（自动生成）

## 论文总结：EventRelBench——大语言模型事件关系理解的综合基准

### 1. 核心问题与整体含义

- **研究动机**：事件关系理解是篇章理解、信息抽取与常识推理等下游任务的基础。尽管大语言模型（LLM）已在各类自然语言处理任务上表现出色，其理解与提取复杂事件关系的能力尚未被系统性评估。
- **存在的问题**：现有评测基准通常只关注单一关系类型，或在单一粒度上评估。例如，许多工作只针对时间关系或只关注句子级抽取，缺乏统一的多类型、多粒度事件关系基准。这使人们难以定位通用型 LLM 在事件理解上的具体短板。

---

### 2. 方法论

- **核心思路**：构建一个统一的、多任务事件关系评测框架，并通过指令微调提升模型对事件关系的理解能力。
- **EventRelBench 基准构建**：
  - 以 **35K 道多选题** 为评测载体，覆盖四类核心事件关系：
    - **共指关系**（Coreference）：不同表述是否指向同一事件。
    - **时间关系**（Temporal）：事件发生的时间先后（BEFORE/AFTER/EQUAL/VAGUE）。
    - **因果关系**（Causal）：事件之间的因果影响（CAUSE/CAUSED_BY）。
    - **隶属关系**（Supersub）：某一事件是否为另一事件的具体组成部分（Super-Sub/Sub-Super）。
  - 支持 **两种粒度**：句子级（单句内）和文档级（跨句、跨段落）。
- **EventRelInst 指令微调数据集**：
  - 构建了约 **48K 条指令-答案对**，利用 Sentence-BERT 做语义去重，与 EventRelBench 无重叠。
  - 使用 **LoRA（Low-Rank Adaptation）** 低秩适配对 Llama-3-8B、Qwen-2.5 系列（0.5B–7B）进行微调，并按照 DeepSpeed Zero-2 完成统一配置。

---

### 3. 实验设计

- **评测模型**：10 个开闭源 LLM，包括 Bloomz-7B、ChatGLM2-6B-32k、AquilaChat-7B、Gemma-7B-IT、ERNIE-3.5-8K、DeepSeek-V3、Claude-3-Haiku、GPT-3.5-Turbo、GPT-4o/GPT-4o-mini、Llama-3-8B 与 Qwen-2.5（0.5B/1.5B/3B/7B）。
- **评测策略**：对比四种提示方式：零样本（Zero-shot）、思维链零样本（Zero-shot with CoT）、少样本（Few-shot）、思维链少样本（Few-shot with CoT）。
- **基准数据集来源**：
  - 共指：ECB+、EventStoryLine
  - 时间关系：MATRES、TCR、Causal-TimeBank
  - 因果：MAVEN-ERE、EventStoryLine
  - 隶属：HiEve、MAVEN-ERE
- **评估指标**：Accuracy 与 Macro F1。

---

### 4. 资源与算力

- 论文没有明确给出 GPU 型号、训练设备数量或训练总时长等具体算力配置。
- 文中仅提及统一采用 DeepSpeed Zero-2 框架，设置合理的 LoRA 条目大小、批次等超参数，说明作者对训练条件的控制是存在的，但未做设备层面的详细披露。

---

### 5. 实验数量与充分性

- **实验覆盖量较大**：整体评测涉及多个不同规模、不同训练范式的模型和多种提示方案，并包含 LoRA 微调前后对比。
- **四类事件关系分别报告**：除总体结果外，还分别给出四类事件关系和文档级/句级的表现与发现。
- 进行了三轮独立运行以避免随机性影响。
- **评估充分性分析**：
  - **亮点**：对于目前通用型 LLM 在多任务、多层级关系抽取上的侧写相对较全面。
  - **不够充分之处**：没有覆盖跨语言场景（仅英文），也缺少对非选择题形式（生成式、抽取式）的扩展评测；时间关系的复杂推理问题（如多跳时间线）在现有测试中暴露有限。对消融测试（如不同指令微调数据量对结果的影响）没有给出专门的对照组。

---

### 6. 主要结论与发现

- 现有 LLM 在 **EventRelBench 上整体表现不足**，少部分模型甚至接近或低于随机猜测水平。
- **文档级表现优于句子级**，和过去传统抽取模型相反；这说明 LLM 对长跨度的上下文线索可能比短句隔离更能进行有效捕捉。
- **时间关系是最难的子任务**：所有模型的 F1 基本低于 30%，即便微调后提升也非常有限。
- **共指关系**与**因果关系**相对容易，尤其在微调后有明显进步。
- **CoT 提示不一定带来稳定收益**，部分模型甚至出现掉点，需要更精细的推理引导。
- EventRelInst 指令微调可带来显著性能提升，**Qwen2.5-7B-FT** 在 EventRelBench 上取得了 Acc 60.0%、F1 54.5% 的成绩，为该模型的基座版本带来了 6.9–10.4 个百分点的进步。

---

### 7. 优点

- **统一多类型基准设计**：同时评估共指、时间、因果、隶属四类关系，模型评估不再集中于单一能力。
- **双粒度设计**：提供句子与文档两个层次，切合真实自然语言推理场景。
- **质量控制严谨**：引入人工复核、标注一致性检查和干扰项筛选方案，确保数据标签可靠。
- **开源数据与真实来源结合**：大量基于公开的权威语料构建，可复现性强。
- **给出针对性解决方案**：不仅做了问题揭示，还提供了可用的 48K 指令微调数据，能直接用于后续模型优化。

---

### 8. 不足与局限

- **实验范围限制**：
  - 事件关系种类有限，未涵盖所有语义交互类型（例如复杂事件逻辑、否定、模态等）。
  - 评估依赖的多选题形式，无法全面呈现模型在开放式抽取任务中的表现。
- **语言与领域限制**：
  - 全部集中于英文数据，对非英语环境的表现无法提供支持。
- **时间关系数据不足**：
  - 时间戳标注不丰富、长期时态依赖训练样例较少，导致基于指令微调的提升空间有限。
- **标注一致性的问题**：
  - 文档中提及的 91.7% 标签准确率和 75.6 的 Kappa 值已能说明整体质量较高，但仍存在边界模糊问题，可能对模型评测结果有潜在影响。
- **微调泛化风险**：
  - 有可能会出现对特定格式或题型（A/B/C/D 版）的过拟合，降低对未见指令类型的适应能力。
- **算力开销与评测覆盖局限**：
  - 资源调度未说明细节，也缺少更大的模型参数量等多样化体系实验。

---

（完）
