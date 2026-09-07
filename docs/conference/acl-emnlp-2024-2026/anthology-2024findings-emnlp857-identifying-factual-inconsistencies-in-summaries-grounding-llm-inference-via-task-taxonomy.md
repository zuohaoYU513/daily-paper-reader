---
title: "Identifying Factual Inconsistencies in Summaries: Grounding LLM Inference via Task Taxonomy"
title_zh: 识别摘要中的事实不一致：通过任务分类法为LLM推理提供基础
authors: "Liyan Xu, Zhenlin Su, Mo Yu, Jin Xu, Jinho D. Choi, Jie Zhou, Fei Liu"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.857.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 基于任务分类法进行LLM推理以识别摘要事实不一致
tldr: 摘要生成模型常产生与原文不一致的事实，阻碍了忠实摘要的使用。本文认为除构建更强的NLI模型外，把摘要不一致错误类型纳入推理也很关键。作者整理关键错误类型并形成任务分类法，用于零样本和有监督的大模型推理，在十个数据集五个领域上取得当前最优性能。这项工作为基于LLM的事实一致性检测提供了可扩展的推理空间。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp857/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1572, \"height\": 493, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp857/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 537, \"height\": 292, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp857/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1656, \"height\": 701, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp857/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 512, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp857/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp857/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp857/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1610, \"height\": 520, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp857/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp857/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 699, \"height\": 406, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp857/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 690, \"height\": 191, \"label\": \"Table\"}]"
motivation: 摘要生成模型常与原文不一致，阻碍忠实摘要应用，检测手段仍需改进。
method: 整理摘要不一致的错误类型为任务分类法，用其指导零样本与有监督LLM推理。
result: 在十个数据集、五个领域上取得最先进性能，零样本推理亦明显受益。
conclusion: 任务分类法可显著增强LLM对摘要事实不一致的检测，并支持跨域迁移。
---

## Abstract
Factual inconsistencies pose a significant hurdle for the faithful summarization by generative models. While a major direction to enhance inconsistency detection is to derive stronger Natural Language Inference (NLI) models, we propose an orthogonal aspect that underscores the importance of incorporating task-specific taxonomy into the inference. To this end, we consolidate key error types of inconsistent facts in summaries, and incorporate them to facilitate both the zero-shot and supervised paradigms of LLMs. Extensive experiments on ten datasets of five distinct domains suggest that, zero-shot LLM inference could benefit from the explicit solution space depicted by the error type taxonomy, and achieves state-of-the-art performance overall, surpassing specialized non-LLM baselines, as well as recent LLM baselines. We further distill models that fuse the taxonomy into parameters through our designed prompt completions and supervised training strategies, efficiently substituting state-of-the-art zero-shot inference with much larger LLMs.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义

- **研究动机与背景**：生成式摘要模型（如 BART、LLM）在生成摘要时容易出现事实不一致问题，即摘要中的某些事实与原始文档不符。这类问题严重影响摘要系统的可靠性与可用性。传统主流做法是将事实一致性检测建模为自然语言推理（NLI）问题，通过加强 NLI 模型来提升检测效果；但本文从另一个正交角度切入：显式地利用任务特有的错误类型分类法来给推理过程注入结构化知识和可解释的“解空间”。

- **整体含义**：研究提出，**除了要建更强的 NLI 模型，更应考虑将语篇摘要不一致特有的错误类型融入 LLM 推理中**，让推理在明确的错误类型指导下进行，从而提高零样本推理和有监督蒸馏模型的准确性、鲁棒性与可解释性。

---

### 2. 论文提出的方法论

#### 核心思想
- 将摘要事实不一致的关键错误归纳为一个**简洁的、面向任务的分类法**，供大模型推理时使用。
- 错误类型分类法包括五类错误：
  - **Predicate Error**（谓词错误）：摘要中谓词表达的语义与原文不符。
  - **Entity Error**（实体错误）：语义框架核心论元或属性与原文不符。
  - **Circumstantial Error**（环境错误）：事件发生的时间、时长或地点等环境信息错误。
  - **Coreference Error**（指代错误）：摘要中代称或指代无法正确对应原文档实体。
  - **Addition Error**（新增错误）：摘要表达的事实无法在原文中找到依据。
- 若不存在上述任何错误，则视为“事实正确”（Factually Correct）。

#### 零样本范式（Zero-Shot Paradigm）
- **FACTAX**（Factuality with Taxonomy）：
  - 构造标准零样本提示，要求 LLM 对文档-摘要对进行逐类错误判断。
  - 每个错误类型附带手工撰写的解释（可选少量示例），并引导 LLM 以 **Chain-of-Thought（CoT）** 形式先推理再输出错误标签，而不是直接给出二元一致/不一致判断。
  - 只有当 LLM 判定摘要中不存在任何规定错误类型时，才认定摘要事实正确。
- **FACTAX-WD**（FACTAX by Windows）：
  - 考虑到长的摘要会降低 LLM 推理精度，将摘要拆分为**约 30 个词长的窗口**，逐一按 FACTAX 框架推理。
  - 汇总每个窗口的结果：只有所有窗口均无错误时，才认定摘要整体事实正确。

#### 有监督范式（Supervised Paradigm）
- 目标：将任务分类法**蒸馏进较小模型（Llama3-8B）参数中**，从而取代对大模型的低效零样本推理。
- 将历史数据集按统一分类法进行标签转化；
- 设计了“错误类型 completion”与“二元判定 completion”两类训练格式；
  - **Error Type Completion**：若样例带有错误类型标注，则让模型输出具体错误类型；
  - **Binary Completion**：让模型直接输出事实正确或不正确。
- 数据来源包括人工标注数据（Training Set I）和合成数据（Training Set II）。

#### 关键设计细节
- 对于超长文档（GovReport、SQuALITY），用 ROUGE 指标挑选高相关信息作为上下文压缩窗口。
- 零样本时 GPT-3.5-turbo、GPT-4o、Llama3 系列、Mistral 都作为底座模型进行了比较。
- 有监督训练采用完整微调，loss 仅作用在 completion 上。

---

### 3. 实验设计

- **覆盖范围**：总共 **10 个数据集、5 个领域**的摘要事实一致性评测：
  - **新闻摘要**：CNN/DM（Polytope、SummEval、FRANK、BUMP、CLIFF）与 XSum（XsumFaith、Wang’20、Goyal’21、Cao’22）；
  - **对话摘要**：DiaSumFact；
  - **官方报告**：GovReport；
  - **叙事故事**：SQuALITY。

- **评估形式**：二分类使用 Balanced Accuracy；GovReport 和 SQuALITY 使用 Pearson Correlation；最终使用 MACRO（各领域均分）作为总体指标。

- **对比方法**：
  - 非 LLM 基线：QuestEval、QAFactEval、SummaC、ALIGNSCORE、ALIGN（另有引用 FalseSum、AMRFACT 的公开结果）；
  - LLM 基线：ChatGPT-ZS、ChatGPT-CoT、ChatGPT-Star、G-Eval；
  - 有监督基线：自训练模型的三组配置（I-Binary、I-Taxonomy、I&II-Taxonomy）。

- **重复实验**：所有 LLM 方法均重复 3 次取均值，以削弱输出随机性。

---

### 4. 资源与算力

- **零样本阶段**：未指定训练所需算力，主要依赖 API 服务或开源 LLM 推理。
- **有监督蒸馏阶段**：
  - 使用 **8 张 NVIDIA A100（40GB 显存）GPU** 进行完整微调；
  - 开启了 Flash Attention；
  - 训练 8 个 epoch；
    - I-Binary 与 I-Taxonomy 各耗时约 **6 小时**；
    - I&II-Taxonomy 耗时约 **24 小时**；
  - 每张 GPU 批大小为 1，学习率 1×10⁻⁵，采用余弦学习率调度（warm-up ratio 0.05）。

---

### 5. 实验数量与充分性

#### 实验主要类型
- 零样本主实验（10 个数据集、多组 LLM 对比）；
- 有监督微调三组训练设置对比；
- 不同底座 LLM 性能对比（ChatGPT、GPT-4o、Llama3-8B/70B、Mistral-7B）；
- 消融式对比：I-Binary vs I-Taxonomy vs I&II-Taxonomy，以验证分类法在训练中的增益；
- 基于摘要长度的分析（长、短摘要下 FACTAX 与 FACTAX-WD 的表现）；
- 细粒度错误类型 F1 分析（五类错误分别计算）；
- 错误类型预测的四种宽松程度指标分析；
- 失败样例分析（附录）。

#### 充分性与公平性评估
- **优势**：数据集覆盖新闻、对话、报告、故事等多个领域，同时使用了 OpenAI API 与开源 LLM，具备较高多样性与参考意义；统一采用 Balanced Accuracy/Pearson Correlation，并保持与 AGGREFACT-FTSOTA benchmark 的可比配置。
- **潜在问题**：部分基线（如 FalseSum、AMRFACT）结果来自原论文而非统一环境下重跑，存在环境不完全一致的可能性；训练数据划分缺少专门开发集，模型的超参数选择可能存在一定主观倾向。

---

### 6. 论文的主要结论与发现

- **零样本推理受益于任务分类法**：FACTAX-WD 在总体 MACRO 上超越所有 LLM 基线和强非 LLM 基线，验证了“显式解空间指引”在事实一致性检测中的作用。
- **FACTAX 方法可随更强 LLM 同步提升性能**：切换到 GPT-4o 或 Llama3-70B 后，表现进一步提升，说明提出的方法具备良好的可扩展性和面向未来的适用性。
- **基于窗口的推理有利于长摘要**：FACTAX-WD 在长摘要（GovReport、SQuALITY）上提升明显，但在短摘要上未必优于 FACTAX。
- **有监督蒸馏是可行的高效替代方案**：将分类法融入 Llama3-8B 参数后，模型可达与 ChatGPT 级别零样本 FACTAX 相近甚至更好的效果，不需要大模型在线推理的巨大开销。
- **加入错误类型监督信号确有增益**：I-Taxonomy 相比 I-Binary 在 MACRO 上提高 0.5，说明错误类型分类法对训练也是有效的；引入额外合成数据 I&II 又提升约 1.2。
- **细粒度推理优于直接二分类**：I&II-Taxonomy + INF-Taxonomy 在 MACRO 上最高，达到 75.4，与 GPT-4o 持平。

---

### 7. 优点

- **转换视角**：与大量文献专注于提升 NLI 模型不同，本文提出通过任务分类法来“框定”推理空间，思路新颖。
- **简洁的分类法具有落地价值**：五类错误分类足够简单，便于 LLM 理解与统一多数据集的异质标签。
- **可解释性强**：模型输出不只是二元标签，而是先展示推理过程、再指出具体错误类型，便于人工校验。
- **擅长处理“长摘要”场景**：针对长摘要设置基于窗口的推理，在长文档评测上表现突出。
- **跨模型通用性好**：方法在 ChatGPT、GPT-4o、Llama3-8B/70B、Mistral-7B 上均展现出性能提升。
- **开源支持**：数据和代码公开在 GitHub 上，具备可复现性。
- **多方位实验设计**：构造了独立于训练的测试集，并进行了受控训练设置对比，具有一定说服力。

---

### 8. 不足与局限

- **异质数据集标签转换存在噪声**：不同数据集根据各自标准设计的原始标注所转换的统一错误标签不一定是纯净的，可能影响有监督训练效果。
- **零样本方法对复杂摘要的把握有限**：部分失败案例表明 LLM 可能对隐含信息理解不到位，也无法保证与人类推理完全一致。
- **有监督依赖特定数据源**：监督模型的行为受制于已有标注数据或自动生成数据，不排除存在领域偏向。
- **缺少更细粒度的调优策略**：全部微调训练中未设专门开发集，可能带来超参数欠优化风险。
- **少样本示例未带来明显改善**：加入示例并没有稳定的性能正向增益，说明提示中的示例敏感性仍需更深层面的解决。
- **评测范围有限**：故事类数据（SQuALITY 只有 60 条摘要）虽然能看出一定趋势，但在统计显著性上仍然偏弱；实验也主要面向英文场景，尚未讨论跨语言应用。

---

（完）
