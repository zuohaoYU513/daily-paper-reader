---
title: "Explicit, Implicit, and Scattered: Revisiting Event Extraction to Capture Complex Arguments"
title_zh: 显式、隐式与分散式：重新审视事件抽取以捕获复杂论元
authors: "Omar Sharif, Joseph Gatto, Madhusudan Basak, Sarah Masud Preum"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.673.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 把事件论元抽取扩展到隐式与散落论元，以捕获完整参与者与属性信息
tldr: 已有事件抽取通常把论元当作文档中连续文本片段，难以处理未在文中出现但可通过上下文推断的隐式论元，以及分散在全文多处需要拼合的散落论元。本文重新定义事件抽取，将这两类复杂论元纳入考虑，并为抽取显式、隐式和分散论元提供新的任务框架。分析表明原有span抽取框架不能覆盖完整事件信息，需要结合跨句或跨段信息来建模参与者与属性。该研究为复杂场景下的事件论元抽取奠定基础。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main673/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main673/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1567, \"height\": 747, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main673/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1528, \"height\": 661, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main673/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 720, \"height\": 610, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main673/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1504, \"height\": 838, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main673/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 729, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main673/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 747, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main673/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 811, \"height\": 758, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 784, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 829, \"height\": 421, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1626, \"height\": 777, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 648, \"height\": 637, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 785, \"height\": 805, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 807, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 739, \"height\": 945, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 785, \"height\": 804, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1594, \"height\": 810, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1632, \"height\": 2076, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main673/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1690, \"height\": 2325, \"label\": \"Table\"}]"
motivation: 传统事件抽取假设论元是连续文本跨度，无法建模可从上下文推断出的隐式论元和分散在全文各处的论元。
method: 扩展事件抽取定义，将隐式论元和散落论元作为重点，并研究如何从上下文中推断或聚合分散信息形成论元。
result: 显示原有的跨度抽取难以完整建模事件，必须借助上下文推断与跨片段聚合才能捕获复杂论元。
conclusion: 推动事件抽取从连续片段抽取走向更通用的复杂论元建模，适用于叙述多样化的长文本事件理解。
---

## Abstract
Prior works formulate the extraction of event-specific arguments as a span extraction problem, where event arguments are explicit — i.e. assumed to be contiguous spans of text in a document. In this study, we revisit this definition of Event Extraction (EE) by introducing two key argument types that cannot be modeled by existing EE frameworks. First, implicit arguments are event arguments which are not explicitly mentioned in the text, but can be inferred through context. Second, scattered arguments are event arguments that are composed of information scattered throughout the text. These two argument types are crucial to elicit the full breadth of information required for proper event modeling.To support the extraction of explicit, implicit, and scattered arguments, we develop a novel dataset, DiscourseEE, which includes 7,464 argument annotations from online health discourse. Notably, 51.2% of the arguments are implicit, and 17.4% are scattered, making DiscourseEE a unique corpus for complex event extraction. Additionally, we formulate argument extraction as a text generation problem to facilitate the extraction of complex argument types. We provide a comprehensive evaluation of state-of-the-art models and highlight critical open challenges in generative event extraction. Our data and codebase are available at https://omar-sharif03.github.io/DiscourseEE.

---

## 论文详细总结（自动生成）

# 论文总结：显式、隐式与分散式论元的事件抽取（EMNLP 2024）

## 1. 核心问题与研究动机
- **背景矛盾**：传统 Event Extraction 将论元定义为“文档中连续的文本片段”（span extraction），只支持**显式论元**。
- **数据现实**：真实在线健康话语中，大量关键事件信息并不是某个连续片段：
  - **隐式论元（implicit）**：未在文中直接提及，但可从上下文推断，例如文中提到 “da vinci route” 实际是指“考虑前列腺切除手术（Da Vinci 机器人手术）”；
  - **分散式论元（scattered）**：信息散落在多句/多段中，需要拼接才能构成完整论元。
- **领域缺陷**：大多数 EE 工作以新闻/维基为主，缺乏对社交媒体/在线健康社区的建模；这限制了 EE 在公共健康、谣言检测、错误信息识别等下游任务上的应用价值。
- **核心问题**：如何把 EE 从“只抽连续片段”扩展为能够抽取显式、隐式和分散在全文各处的复杂论元。

## 2. 方法论
### 总体思路：将 EAE 重构为文本生成问题而不是 span 抽取
- 用自然语言描述论元值，而不是给出起始/结束位置。
- 允许论元值为“null”；多个取值用逗号分隔。
- 每个样本同时从 post 和 comment 中分别标注，再在评估阶段合并（解决标签稀疏）。

### 论元类型与本体框架
- 三类事件：**Taking MOUD (TM)**、**Return to Usage (RU，即“Relapse”)**、**Tapering (TP)**。
- 四组论元角色：**core**（事件概要）、**type-specific**（事件类型细节）、**subject-specific**（病人特征）、**effect-specific**（身心影响/副作用细节）；合计 41 个具体论元。
- 论元被标记为 explicit / implicit / scattered 三类（三类互斥）。

### 评估方法（核心贡献之一）
- 生成式输出不能单纯用 exact match。
- 提出 **relaxed-match F1（RM_F1）**：用 SBERT 语义相似度判断输出是否与金标准相似；相似度 >0.75 判为命中。
- 同时保留 **exact-match F1（EM_F1）**（相似度=1.0）以与已有工作比较。
- 事件检测采用无触发词（trigger-free）的形式，被定义为多标签分类（一个样本可以既是 tapering 又是 …）。

### 数据构建流程
1. 扩展现有 TREAT-ISE 语料：收集 5,412 条与 MOUD 相关的 Reddit 帖子（信息寻求）及 39,300 条评论；
2. 过滤出目标事件相关帖子，再依次做“至少 4 条评论的讨论”过滤和“长度≥10 词”过滤；
3. 用 GPT-4 以零样本方式从 post-comment 对中筛选含“建议/advice”的评论输出（advice precision=0.94，人工复核 50 条约 98% 准确）；
4. 随机选 396 对，由 8 名训练过的标注者完成论元标注；每个样本至少 2 人标注，第 3 人复核；
5. 因为有整句或散布信息，论文**不使用 Cohen's kappa**，而是用 RM_F1 计算 IAA，最终平均 IAA=0.811。

## 3. 实验设计
### 数据集与基准
- **DiscourseEE**：376 对 post-comment + 共 7,464 条论元标注。
  - 51.2% 隐式论元，17.4% 分散论元，合计 68.6% 无法用单一片段表达。
  - 每样本平均约 10.27–11.4 条论元（不含 null）；文本平均长度约 115 词。
- 划分：train=246，dev=50，test=100。

### 事件检测（多标签分类）对比模型
- Transformer：BERT、RoBERTa、MPNet（均为微调）；
- Instruction-tuned：FLAN-T5-base、FLAN-T5-large（微调）；
- LLM（零样本，统一 prompt）：Gemma-7B、Mixtral-8x7B、Llama3-8B、Llama3-70B、GPT-4。

### 论元抽取对比的三大设定
1. **Extractive-QA**：BERT + SQuAD 式 span 抽取；
2. **Generative-QA**：FLAN-T5-base/large 经过指令微调，逐个角色抽取；
3. **LLM zero-shot 生成**：5 个 LLM × 2 种提示：
   - **description-guided**：给角色描述；
   - **question-guided**：给角色对应的问题。
- 为了控制推理成本，采用 divide-and-conquer：一次推理抽较多同类论元（core/type-specific/subject-effect），而不是为每个角色单独做一次。
- 由于 subject-specific 论元稀疏，实验中把 subject-specific 与 effect-specific 合并为“subject-effect”进行评价。

## 4. 资源与算力
- 论文明确说明所有训练/微调实验在 **Google Colab GPU 平台**上完成，其中 FLAN 微调提到使用 **A100** GPU。
- **未报告**：GPU 数量、总训练 GPU 时长、能耗等定量资源信息。因此无法精确估算算力成本；推理侧使用 API 的 GPT-4，也未报告费用/调用量。

## 5. 实验数量与充分性
### 实验数量
- ED：10 个模型（3 个 Transformer + 2 个 FLAN + 5 个 LLM），平均 3 次运行取均值；
- EAE：Extractive-QA + FLAN-T5(base/large) + 5 个 LLM × 2 种提示；
- 除总体 RM_F1/EM_F1 外，还报告了“explicit/implicit/scattered”分组下的 recall，并做了人类定性评估子集。

### 充分性评估
- **优点**：覆盖抽取式、生成式、大中小规模模型，统一 prompt 并低温度设置（LLM temperature=0.01/0.0），整体对比公平。
- **不足/缺口**：
  - 没有做**消融实验**（例如 RM 阈值敏感性、不同事件论的标签整合影响等）；
  - 仅给定 zero-shot 设置，未比较 few-shot/CoT/system prompt 优化；
  - 没有跨领域/跨平台验证，也缺少多语言或跨数据集迁移实验；
  - RM 阈值 0.75 是人工观察设定的，存在主观性；
  - 数据只有 396 对样本；未充分讨论测试集重复 3 次测试的标准误或置信区间。

## 6. 主要结论与发现
- **现有 Extract-QA 严重失效**：span 抽取式方法 RM_F1 只有 17.13（而隐式/分散论元 recall 仅 9.40%/13.44%），证明“连续片段”假设确实无法覆盖复杂论元。
- **生成式方法明显优于抽取式**：FLAN-T5-large 35.53，Gemma(large)/Llama3/GPT-4 可到 35–42 RM_F1。
- **GPT-4 + question-guided prompt 为最优单模型**：RM_F1 41.98，EM_F1 16.84——说明生成式 EE 仍有巨大空间。
- **隐式论元最难**：即使 GPT-4，隐式论元 correct recall 也只有 36.53%；显式 > 散落 > 隐式（相对而言）。
- **EM_F1 显著低估性能**：GPT-4 从 RM 的 41.98 掉到 EM 的 16.84；人类评估表明很多“语义正确但措辞不同”的输出会被 EM 判错。
- **模型规模与 ED 性能近似线性相关**：LLM 越大越好，但小于 1B 参数的 FLAN-T5 可通过指令微调贴近甚至超过部分 7–8B 模型。

## 7. 优点
- **任务扩展具有开创性**：第一个把隐式与分散式论元引入事件论元抽取的大规模标注语料（DiscourseEE），具有明显社会价值（MOUD/成瘾治疗）。
- **标注质量控管严谨**：4 周培训、双人标注+第三方复核，并给出了适用于生成式标注的 IAA 度量（RM_F1=0.811），而非简单套用有局限性的 kappa。
- **方法论迁移合理**：将 EAE 转换为 text generation，与 LLM 的能力对齐，并专门提出 relaxed-match 语义评估，缓解“句义等价却文本不同”的评价误差。
- **评测覆盖广**：从 encoder-only 小模型到 70B 级开源 LLM 再到 GPT-4，跨 explicit/implicit/scattered 分层的分析提供了清晰的诊断结论。
- **开放与可复现**：公开数据集与代码，明确使用提示模板、数据划分、采样方式与模型超参（batch size、lr、epoch、temperature），同时给出伦理与隐私声明。

## 8. 不足与局限
- **规模与通用性有限**：仅 396 对、7,464 条论元；单领域（Reddit 上 MOUD/阿片类治疗）、单语言、只有 3 类事件，学科外推受限制。是否适用于其他健康社区（癌症、精神健康、怀孕）尚缺少验证。
- **零样本评估存在偏置风险**：没有为每个 LLM 单独调优 prompt，也未测试 few-shot/CoT；因此“模型间差距”与“模型内潜力”不能完全解释。
- **评估指标仍不稳定**：RM_F1 依赖人工设定的 0.75 相似度阈值，用户不易复现该阈值决策；EM_F1 又过度苛刻，两种指标的分歧为未来统一评测留下问题。
- **消融不足**：未量化“post+comment”合并、分而治之的论元是否对结果有因果贡献，也没有系统评估 label 分布不均衡（null 比例高）对模型预测的偏见影响。
- **显式/隐式标注含主观判断**：隐式论元本质依赖标注者推理，即使 IAA=0.811，仍可能引入系统性解释偏差；没有公开矛盾标注样本的误差分析。
- **预算/成本信息缺失**：如第 4 点所述，论文未提供准确的推理/训练算力成本，可复现时的资源评估较难。
- **下游验证不足**：论文强调了公共健康、谣言检测等应用价值，但并未提供任何下游任务验证来度量 DiscourseEE 的实证益处。

（完）
