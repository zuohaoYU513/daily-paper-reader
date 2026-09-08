---
title: "CondAmbigQA: A Benchmark and Dataset for Conditional Ambiguous Question Answering"
title_zh: CondAmbigQA：关于条件模糊问答的基准与数据集
authors: "Zongxi Li, Yang Li, Haoran Xie, S. Joe Qin"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.115.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 将条件作为显式上下文约束引入问答，识别隐含条件并评测适用性
tldr: 问答中用户常省略关键条件，导致模型基于错误假设作答并产生幻觉。本文构建CondAmbigQA基准，包含2000条条件歧义查询和条件感知评测指标，借助检索维基百科片段来标注并揭示可能的隐式条件。该基准首次将“条件”作为显式上下文约束引入问答评测，有助于衡量模型对条件限制与应用范围的判别，为规范性文本中的条件和例外理解提供了方法论借鉴。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main115/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1593, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main115/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 636, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main115/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 764, \"height\": 1081, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main115/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1480, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main115/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 751, \"height\": 601, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1349, \"height\": 481, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1339, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1336, \"height\": 540, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1599, \"height\": 1013, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1668, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1663, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1635, \"height\": 1047, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1664, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1635, \"height\": 1399, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main115/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1674, \"height\": 353, \"label\": \"Table\"}]"
motivation: 问答用户常省略重要条件，模型因错误假设而输出看似幻觉的回答，需识别隐式条件。
method: 构建2000条条件歧义查询，通过检索维基百科进行条件标注，并提出条件感知评测指标。
result: 提供了首个条件模糊问答基准，使模型对隐含假设和适用条件的评测更精确。
conclusion: 显式建模条件可减少误解带来的幻觉，并为条件约束理解任务提供资源与方法。
---

## Abstract
Users often assume that large language models (LLMs) share their cognitive alignment of context and intent, leading them to omit critical information in question-answering (QA) and produce ambiguous queries. Responses based on misaligned assumptions may be perceived as hallucinations. Therefore, identifying possible implicit assumptions is crucial in QA. To address this fundamental challenge, we propose Conditional Ambiguous Question-Answering (CondAmbigQA), a benchmark comprising 2,000 ambiguous queries and condition-aware evaluation metrics. Our study pioneers “conditions” as explicit contextual constraints that resolve ambiguities in QA tasks through retrieval-based annotation, where retrieved Wikipedia fragments help identify possible interpretations for a given query and annotate answers accordingly. Experiments demonstrate that models considering conditions before answering improve answer accuracy by 11.75%, with an additional 7.15% gain when conditions are explicitly provided. These results highlight that apparent hallucinations may stem from inherent query ambiguity rather than model failure, and demonstrate the effectiveness of condition reasoning in QA, providing researchers with tools for rigorous evaluation.

---

## 论文详细总结（自动生成）

# CondAmbigQA：条件模糊问答的基准与数据集——详细总结

## 1. 核心问题与整体含义

- **动机**：用户在向大语言模型（LLM）提问时，常默认模型与自身拥有相同的背景常识和意图认知，因此倾向于省略关键上下文信息，导致查询出现歧义。模型若基于错位的假设作答，即便逻辑自洽，也可能被用户视为“幻觉”。
- **核心问题**：现有 QA 研究虽在推理、检索增强（RAG）等方面取得进展，但**并未直接解决由用户隐含假设引发的查询歧义**；模型需要一种机制来显式识别"条件"，并据此区分同一问题的多种合法答案。
- **核心含义**：论文主张将“条件”（conditions）作为显式上下文约束引入问答：检索到的片段用于揭示可能的解释，并据此给出条件-答案对。作者认为，**绕过歧义处理直接评估模型"幻觉"是不公平的**，因为许多看似错误的回答其实是问题本身缺少条件所致。

## 2. 方法论

- **核心思想**：用“条件”刻画歧义问题的隐式假设——一个条件是一组决定了“在什么范围内答案才成立”的上下文约束；不同条件对应不同答案，从而实现对歧义查询的系统性消解。
- **数据构建流程（CondAmbigQA 数据集）**：
  - **来源**：从 ALCE-ASQA（源自 AmbigNQ）中筛选 2,000 条真正具有“歧义导致不同答案”的查询；每个实例包含查询、维基百科检索片段以及结构化的条件-答案-引文三元组集合。
  - **检索式标注**：使用 FAISS 从 Wikipedia 向量库检索相关片段，再由标注流程从片段中提炼限定条件与答案，保证注释有据可依。
  - **人类-LLM 三轮交互标注**：
    1. 第一轮：GPT-4o 依据定制 prompt（RAG 问答、歧义分析、证据评估、结构化回答、校准、合并）生成初始条件-答案-引文候选；
    2. 第二轮：人工结合提示词，让 LLM 对歧义和证据进行再分析与修正；
    3. 第三轮：引入额外判断反馈，由人工审核逻辑一致性并校准标注。
  - 结果：40% 无需修改即可通过，经两轮反馈后该比例升至 85%。
- **评测指标**：
  - **Condition Score**（条件正确性/完整性）、**Answer Score**（答案准确性与相关性）、**Citation Score**（引用召回率）。
  - **Answer Count / Count Difference**：衡量模型生成答案数量的匹配程度（用于诊断过生成或欠生成）。
  - **Combined Score**：三个核心指标的加权组合，加入对答案数量偏差和"只给出单一答案（未识别歧义）"的管理惩罚。
  - 所用指标均采用与人类判断相关性较高的 G-Eval 形式自动打分。

## 3. 实验设计

- **数据集 / Benchmark**：CondAmbigQA-2K 包含 2,000 条歧义查询，收窄自 ALCE-ASQA / AmbigNQ，含检索片段、真实条件、标准答案和引文标注；评估中另用 ALCE-ASQA 的 948 道问题做跨数据集泛化验证。
- **对比的基线 / 模型**：
  - 通用数据集中对比 AmbigNQ、ASQA、ALCE、Multihop-RAG、NQ、TriviaQA、ELI5、TruthfulQA 等特性差异。
  - 评测模型包括商用 API 模型：GPT-4o、GLM4-plus；本地开源模型：LLaMA3.1 (8B)、Mistral (7B)、Gemma2 (9B)、GLM4 (9B)、DeepSeek-R1 (7B)、Qwen2.5 (7B)。
- **实验协议（对照场景）**：
  1. 主实验：仅提供查询与检索片段，模型先自行识别条件，再生成带引文答案；
  2. 提供真实条件：将地面真值条件作为额外输入，测试显式条件对答案质量的加成；
  3. 无条件的标准 RAG（仅用片段直接作答）；
  4. 封闭书（closed-book）消融：移除外部检索片段，对比零样本直接回答、自假设条件推理和给定真实条件推理三类设置；
  5. 泛化验证：将条件识别框架迁移至 ALCE-ASQA；

## 4. 资源与算力

- **作者未明确说明**任务所需的 GPU 型号、数量、训练时长、显存或训练参数量细节。
- 文中说明的开销信息集中在**数据集标注成本**：采用 LLM 辅助（human-LLM 交互式标注）后总计 API 标注成本约 $1000（约每实例 $0.3–0.5），共约 150 小时；若完全人工标注则预计每查询至少 30 分钟，整体成本显著低于全人工方案。
- 本地模型部署基于 Ollama，默认采样参数、8K 上下文窗口，但未列明算力集群配置。

## 5. 实验数量与充分性

- **组数**：实验覆盖三个主要场景（无条件、模型自生成条件、地面真值条件） × 多类模型（8 种），并提供封闭书消融、跨数据泛化和案例研究；附录中还包含 20 条人工评估与 G-Eval 的相关性检验。
- **是否充分**：总体设计较完整，特别是“条件有无与否”的递进式对照（无检索 → 无条件 RAG → 模型条件 → 真实条件）能较有力支撑核心论点；且泛化到 ALCE-ASQA 增加外部有效性。
- **客观性的潜在问题**：
  - 自动评估（G-Eval）依赖 GPT-4o 等 LLM 作为裁判，可能自带偏见；
  - 本地模型仅在 7B–9B 规模间对比，缺少更大规模开源模型的参照，不能据此推断“所有开源模型系统性弱于 API 模型”；
  - 主观歧义本身无金标准，人工标注易受个人经验影响，跨语言的验证不足；
  - 规模只有 2,000 条，可能无法覆盖所有歧义类型和领域。

## 6. 主要结论与发现

- **引入条件显著提升问答质量**：模型先识别条件再作答，Answer Score 平均提高 11.75%；若显式给定地面真值条件，还可再提升 7.15%。
- **显式条件对引文可靠性作用更大**：以传统 RAG（无明确条件）为基线，加入真实条件后 Citation Score 普遍提高超过 100%；例如 GPT-4o 的引文得分可从 0.38 升至 0.96。
- **模型规模的层级差异明显**：
  - API 模型（GPT-4o、GLM4-plus）在条件生成、答案准确率和引用准确性上均远超本地开源模型（如 GPT-4o 综合得分 0.662，本地最佳 Qwen2.5 为 0.360）；本地模型中，即使带有推理增强训练的 DeepSeek-R1 也远不能消除与 GPT-4o 的差距。
  - GPT-4o 倾向于少而精的答案（欠生成约 −0.17 组）；本地模型更倾向于多而全的答案（如 Mistral 平均超生成 +1.09 组），这可能是其分数较低的部分原因。
- **“幻觉”部分源于查询歧义而非纯模型缺陷**：在封闭书设置下给出条件相比直接作答能使 Answer Score 平均提升约 135%（范围 93%–400%），说明只要补充恰当的语境约束，局部模型的回答能力可被显著打开。
- **跨数据集验证有效**：把条件化问答框架搬到 ALCE-ASQA（948 题）后，无条件下直接回答得分 0.374，条件化回答得 0.471（+约 10%）。条件质量与答案表现显著正相关（Pearson: 0.598，Spearman: 0.637，p<0.001）。

## 7. 优点（亮点）

- **问题视角新颖且实用**：首次系统地提出“条件”作为解决歧义 QA 的一等公民，将“识别问题中隐藏的约束条件”与“给出答案”解耦，直击 RAG/QA 实践的真实痛点。
- **数据架构设计合理**：实例格式 `(条件, 答案, 引用集合)` 同时支持条件识别、条件化回答和来源归因三类评估，可在同一基准上同时考察多个层面能力。
- 提出**兼顾完备性与精确性的综合指标**（Combined Score + Answer Count 惩罚），避免模型一味多答来刷指标。
- 使用**人工参与和 LLM 三轮协同的标注管线**，大幅降低构建成本，并提供明确的 prompt 与质量控制协议，方法具可复现性和扩展性。
- 用**多种互补对照实验**强化因果论证（无检索/无条件/自生成条件/真值条件），让“显式条件有用”的结论更具说服力。

## 8. 不足与局限

- **覆盖面不足**：仅英文维基来源、2,000 条规模，对特定领域（如医学、法律）或更多复杂交错歧义的覆盖有待扩充。
- **评估指标存在启发式风险**：论文自己也承认 Citation Score 采用偏“回忆优先/召回型”的算法可能忽视冗余引用问题；对冲突片段/对抗证据也缺少显式鲁棒性检测。
- **针对主观性问题适用有限**：当问题本身不存在客观的“条件-答案”关系时，框架难以给出有意义区分（例如观点类、审美类查询）。
- **训练成本与推理成本**：两阶段（先识别条件、再给出回答）会增加响应延迟，不适合实时性要求高的生产场景。
- **小模型能力受限**：7B–9B 量级模型的 Condition/Answer 得分普遍在 0.2–0.3 之间，说明条件化消歧目前对模型容量要求较高，在资源受限场景中难以直接落地。
- **外部泛化验证仍偏单薄**：仅附 ALCE-ASQA 一个外部数据集，且主要借助 GPT-4o 单模型完成，不足以推断到更多领域与不同模型架构。

（完）
