---
title: Timeline-based Sentence Decomposition with In Context Learning for Temporal Fact Extraction
title_zh: 基于时间线的句子分解与上下文学习用于时间事实抽取
authors: "Jianhao Chen, Haoyuan Ouyang, Junyang Ren, Wentao Ding, Wei Hu, Yuzhong Qu"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.187.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 通过时间线分解建立事实与时间的对应关系，支持跨句时间信息提取
tldr: 复杂句中的事实与时间对齐是时间事实抽取的一大难点。作者提出基于时间线的句子分解策略，利用大语言模型和上下文学习，把复杂句按引用时间线拆解为更细的子句后再进行事实抽取，从而建立精细的时间-事实对应关系。实验表明直接让LLM抽取时间事实的效果不佳，而时间线句子分解策略能够有效提升时间事实抽取的准确性，为知识图谱中动态事实的补充提供了高效方法。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long187/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long187/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 866, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long187/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 238, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long187/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long187/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long187/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long187/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1661, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long187/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 617, \"height\": 181, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long187/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 729, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long187/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1274, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long187/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1658, \"height\": 243, \"label\": \"Table\"}]"
motivation: 复杂句中事实与时间的对应关系难以确定，直接抽取时间事实的效果不佳。
method: 利用LLM与上下文学习，将复杂句按时间线分解为子句，再抽取各子句对应的时间事实。
result: 验证了直接LLM抽取效果差，而时间线分解策略可有效提升时间事实抽取精度。
conclusion: 时间线句子分解能应对复杂句的时间事实抽取挑战，支持结构化和动态知识图谱构建。
---

## Abstract
Facts extraction is pivotal for constructing knowledge graphs. Recently, the increasing demand for temporal facts in downstream tasks has led to the emergence of the task of temporal fact extraction. In this paper, we specifically address the extraction of temporal facts from natural language text. Previous studies fail to handle the challenge of establishing time-to-fact correspondences in complex sentences. To overcome this hurdle, we propose a timeline-based sentence decomposition strategy using large language models (LLMs) with in-context learning, ensuring a fine-grained understanding of the timeline associated with various facts. In addition, we evaluate the performance of LLMs for direct temporal fact extraction and get unsatisfactory results. To this end, we introduce TSDRE, a method that incorporates the decomposition capabilities of LLMs into the traditional fine-tuning of smaller pre-trained language models (PLMs). To support the evaluation, we construct ComplexTRED, a complex temporal fact extraction dataset. Our experiments show that TSDRE achieves state-of-the-art results on both HyperRED-Temporal and ComplexTRED datasets.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- 时间事实抽取（Temporal Fact Extraction）旨在从自然语言文本中抽取带有时间维度的事实，形式化为五元组 `(head entity, relation, tail entity, qualifier, time value)`，用以支撑知识图谱中的时间敏感查询。
- 已有方法在处理**复杂句子**时面临关键挑战：一个句子中通常包含多个时间表达式和多个事实，如何准确建立“时间—事实”的对应关系非常困难。
- 典型困难示例：一个句子中通过“the other players”隐含了其他球员也在同年获奖；“Michael Jordan in 1996 and 1998”一句话实际表达了 6 个时间事实。现有方法难以处理此类隐含、交织的时间线叙述。
- 作者首次系统探索大语言模型（LLMs）在时间事实抽取任务上的应用，发现直接使用 LLM 抽取效果不佳；进而提出将 LLM 的强分解能力与小型预训练语言模型（PLM）的精细微调能力相结合的方法。

## 2. 方法论

### 核心思想
- 提出**基于时间线的句子分解（Timeline-based Sentence Decomposition, TSD）**：先识别句子中的时间表达式，再利用 LLM 的上下文学习能力将复杂句子按时间点拆分为若干描述该时刻事件的简单子句，从而显式建立“事件—时间”的对应关系，降低后续事实抽取的难度。

### 技术细节与流程
- **时间识别**：使用专用工具 SUTime 识别文本中的时间表达式（而非直接依赖 LLM）。
- **分解提示构造**：
  - 首先仅给 ChatGPT3.5 任务描述和测试句，观察其输出格式偏好；
  - 根据偏好精心构造高质量示范示例，经多次迭代得到上下文学习所用的 few-shot 提示。
- **人类反馈增强**：
  - 在提示中加入负面示例和人工反馈，指出模型常见错误（如事件主体混淆、隐含结束时间漏报等），并提供修正后的正确分解，以提升分解精度和召回。
- **训练阶段融合分解结果**：
  - 将原始文本与 LLM 生成的“时间点 + 事件描述”分解结果拼接为新的输入，用于微调生成式 PLM（如 Flan-T5）。
  - 提出方法 **TSDRE**，即以 Flan-T5 为基座模型、采用 TSD 增强输入的方法。
- 对比方法还包括：
  - 直接使用 ChatGPT3.5 进行上下文学习抽取；
  - 对 Llama2 (7B) 做 LoRA 微调，以及在其训练时同样加入 TSD 增强（Llama2 + TSD）。

## 3. 实验设计

### 数据集
- **HyperRED-Temporal**：由公开基准 HyperRED 筛选出带时间标签的样本构成。
- **ComplexTRED**：作者新构建的复杂时间事实抽取数据集，主要来源：
  - 远距离监督：将 DBpedia、Wikipedia 文章文本与 Wikidata 时间事实对齐，并用 ChatGPT3.5 + 人工校对补充缺失事实，得到约 17,000 句；
  - 从 HyperRED 中人工修正超过两个时间表达式的复杂句子，得到 2,589 句；
  - 总计 19,148 句复杂句子，开发集与测试集经过人工全部校验。
- 与 HyperRED-Temporal 相比，ComplexTRED 的句子更长、每句时间表达式和事实数更多，难度更高。

### 对比方法
- CubeRE（已有 SOTA 抽取方法）
- Flan-T5（直接微调）
- Flan-T5 + Explanation（借鉴 Wadhwa et al. 2023，用 LLM 生成解释辅助训练，这里用 ChatGPT3.5 生成）
- TSDRE w Flan-T5（本文方法）
- Llama2 w LoRA（直接微调）
- Llama2 w LoRA + TSD（本文增强变体）
- ChatGPT3.5（上下文学习）
- 另外在附录中补充了 BART Large 作为基座的 TSDRE 变体实验。

### 评估指标
- 精确率（Precision）、召回率（Recall）、F1，采用字符串级别精确匹配（严格匹配）。

## 4. 资源与算力

- 论文中提及的环境条件：
  - TSDRE 实验：Intel Xeon Gold 5222 CPU @ 3.80GHz、376GB RAM、3 张 NVIDIA RTX3090 显卡；
  - Llama2 实验：Intel Xeon Gold 6248 CPU @ 2.50GHz、472GB RAM、8 张 NVIDIA Tesla V100 显卡。
- 超参数方面：Flan-T5/TSDRE 与 BART 的 batch size 约为 20.12、学习率 2e-5、最多 4 epochs；Llama2 LoRA 使用 rank=8、alpha=32、学习率 1e-4、3 epochs；CubeRE 为 batch size 32、学习率 5e-5、30 epochs。
- 论文未明确给出每个实验的具体训练时长或 GPU 总耗时时长，因此详细计算开销无法直接获知。

## 5. 实验数量与充分性

- 主要实验覆盖两个数据集（HyperRED-Temporal 和 ComplexTRED），并对比了多种范式（LLM 直接抽取、LLM 微调、PLM 微调、PLM+生成式辅助、TSD 增强等），方法数量较全面。
- 专门开展**分解质量人工评估**：随机抽取 100 句，由 3 位专家打分，比较了带与不带人工反馈的提示下分解的精确率和召回率。
- 进行了**错误分析**：从两个数据集各取 50 个 F1<1 的句子，统计 NER、关系抽取、缺漏事实等错误类型。
- 提供了**案例研究**，展示 TSD 对 Flan-T5 抽取结果的提升。
- 附录补充了 BART 作为基座的实验、与时间关系抽取任务的区分、删除的关系类别、完整的 prompt 等。
- 综合来看，实验设计较系统、对比合理，但缺少不同分解模型或不同示例数量的消融实验；此外，严格精确匹配可能在数值上低估模型的部分正确输出，但作者在错误分析中对此进行了解释。

## 6. 主要结论与发现

- 直接使用 LLM（ChatGPT3.5 上下文学习、LoRA 微调 Llama2）进行时间事实抽取的效果不理想，F1 明显低于已有的小模型方法 CubeRE。
- Llama2 在训练中加入 TSD 后，F1 在 HyperRED-Temporal 上提升约 11 个点，在 ComplexTRED 上提升约 9 个点，说明分解信息有助于大模型训练。
- Flan-T5（Large）本身在微调后优于 LLM 直用方法；但使用 LLM 生成的“解释”辅助训练反而造成轻微下降（作者认为解释生成方法在严格匹配下不适合该任务）。
- **TSDRE 在两个数据集上均达到 SOTA**：在 HyperRED-Temporal 上 F1 为 66.71，在 ComplexTRED 上 F1 为 42.55。
- 分解质量控制实验表明，TSD 结果在人工评估中 Precision/Recall 均超过 90%，加入人类反馈后进一步提高了分解质量（Precision 94.65，Recall 95.57）。
- 时间选择与限定符分类的错误率极低，表明 TSD 确实有效解决了时间—事实对应问题。

## 7. 优点

- 首次系统探索并对比了多种 LLM 在时间事实抽取任务中的应用方式，填补了该方向的空白。
- 提出了一种新颖、无需训练样本的**时间线分解策略**，利用 LLM 上下文学习 + 人类反馈迭代构造提示，不依赖大规模标注分解数据。
- 将 LLM 分解能力与较小 PLM 的微调能力结合，形成互补框架，思路清晰且通用（不限定特定基座模型）。
- 构建了面向复杂句子的新基准 ComplexTRED，补充了现有数据集中复杂时间场景不足的问题，数据集统计完善，并经过人工校检。
- 实验分析细致：除主结果外，还进行了分解质量人工评估、错误分析、案例研究，并有附录补充说明，具有较好的可复现性。

## 8. 不足与局限

- 分解结果依赖 ChatGPT3.5 生成，未验证开源 LLM 是否能达到同样质量；商用 API 成本较高且可能有稳定性风险。
- 仅测试了 GPT-3.5-turbo，未评估 GPT-4 / GPT-4-turbo 等更强模型（原文承认受限于成本）。
- 对于文档级时间事实抽取，将长文本与分解结果拼接后可能超出生成模型的最大输入长度，应用范围受限。
- 数据构建使用了远距离监督，不可避免存在噪声；且受限于资源，ComplexTRED 训练集未完全人工校验，可能遗留部分错误标签。
- 对“需要基于现有时间表达进行推理”的时间表达（如“three days later”）尚未覆盖，是未来方向。
- 严格精确匹配的评价方式可能低估模型部分正确输出（如实体重叠情况），但作者在错误分析中说明在放宽标准下实际性能会更高。

（完）
