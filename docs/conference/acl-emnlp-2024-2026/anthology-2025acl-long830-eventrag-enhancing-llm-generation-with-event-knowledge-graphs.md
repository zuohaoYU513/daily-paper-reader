---
title: "EventRAG: Enhancing LLM Generation with Event Knowledge Graphs"
title_zh: EventRAG：利用事件知识图谱增强大语言模型生成
authors: "Zairun Yang, Yilin Wang, Zhengyan Shi, Yuan Yao, Lei Liang, Keyan Ding, Emine Yilmaz, Huajun Chen, Qiang Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.830.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 用跨文档事件抽取构建事件知识图谱，在RAG中显式利用事件的时间与逻辑关系
tldr: RAG在叙事丰富的文档和跨源事件推理上往往缺乏结构化的事件关系与时间逻辑。EventRAG先从多个文档中抽取事件，合并语义等价的事件节点并扩充弱连接关系，形成事件知识图谱；随后使用迭代检索与推理策略，显式建模事件间的时间依赖和逻辑关系。在UltraDomain与MultiHopRAG等基准上，该方法较基线RAG系统取得了显著生成性能提升。这为事件密集场景下的可靠跨文档生成提供了一种结构化增强方案。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long830/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1615, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long830/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1611, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long830/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1574, \"height\": 1406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long830/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 681, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long830/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 763, \"height\": 1103, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long830/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1329, \"height\": 920, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long830/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1501, \"height\": 885, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long830/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 816, \"height\": 366, \"label\": \"Table\"}]"
motivation: RAG面对叙事密集文档和事件中心推理时，难以综合多个来源中的结构化事件关系与时间逻辑。
method: 抽取事件并跨文档合并等价事件节点以构建事件知识图谱，再用迭代检索和推理显式捕获时间依赖与逻辑关系。
result: 在UltraDomain和MultiHopRAG基准上显著优于RAG基线，证明事件知识图谱能提升事件驱动的生成质量。
conclusion: 为RAG引入事件结构知识，增强跨文档事件感知和时序逻辑推理能力。
---

## Abstract
Retrieval-augmented generation (RAG) systems often struggle with narrative-rich documents and event-centric reasoning, particularly when synthesizing information across multiple sources. We present EventRAG, a novel framework that enhances text generation through structured event representations. We first construct an Event Knowledge Graph by extracting events and merging semantically equivalent nodes across documents, while expanding under-connected relationships. We then employ an iterative retrieval and inference strategy that explicitly captures temporal dependencies and logical relationships across events. Experiments on UltraDomain and MultiHopRAG benchmarks show EventRAG’s superiority over baseline RAG systems, with substantial gains in generation effectiveness, logical consistency, and multi-hop reasoning accuracy. Our work advances RAG systems by integrating structured event semantics with iterative inference, particularly benefiting scenarios requiring temporal and logical reasoning across documents.

---

## 论文详细总结（自动生成）

# EventRAG：利用事件知识图谱增强大语言模型生成——论文详细中文总结

## 1. 核心问题与整体含义（研究动机）

- 传统 RAG（检索增强生成）在叙事密集文档、跨文档综合与事件中心推理场景中表现不佳：
  - 多以文档、段落或句子为处理单元，忽略了事件之间的结构关系。
  - 难以捕获时间动态（事件顺序、持续时间、时间迁移），导致生成内容缺乏连贯时间线。
  - 单次检索或浅层拼接无法支撑多事件链式推理，容易造成叙事碎片化和逻辑不一致。
  - 多源信息混用时，难以分辨哪些是真实、最新信息，容易产生幻觉。
- 论文的整体目标：将文本组织为结构化的事件知识图谱（Event Knowledge Graph, EKG），并配合智能体式迭代检索与推理，从而提升生成的事实性、逻辑一致性和多跳推理能力。

## 2. 提出的方法论

### 2.1 总体架构

- 包含两个主要阶段：
  1. 事件知识图谱构建（Event Knowledge Graph Construction）；
  2. 多事件检索与生成（Multi-event Reasoning）。
- 与普通 RAG 不同，EventRAG 把“事件”作为知识组织的基本单元，显式建模事件、参与实体及其时间和逻辑关系。

### 2.2 事件知识图谱构建

- 使用 LLM 从文本中抽取事件、实体和关系。
- 抽取结果走两条处理流：
  1. 嵌入为稠密向量存入向量数据库，用于相似度检索；
  2. 进行相似度合并（实体融合）与知识扩展，再构建事件知识图谱。

#### 实体融合（Fuse Entities）

- 解决跨文档中同一实体表达不同、或事件重复出现的问题。
- 用向量相似度合并语义或时间上等价的条目，公式为：

  ```text
  Vi ∪ Vj → Vf，当 similarity(Vi, Vj) > θ
  ```

- 采用余弦相似度；超过阈值的最相似候选作为合并目标。
- 并非直接丢弃原信息，而是建立“相似”关系，保留出处，维持知识图谱语义一致性。

#### 知识扩展（Expand Knowledge）

- 识别知识图谱中连接不足、信息孤立的节点或关系，用文档线索或 LLM 自身知识补全。
- 例如对共享相同参与实体、时间上下文的孤立事件建立链接。
- 本质是把分析性推理前置到图谱构建阶段，降低后续检索与推理的计算负担。

### 2.3 事件级检索与生成

- 查询到来后，智能体将查询拆解为事件要素（实体、时间、逻辑关系），并在 EKG 中检索与查询向量最相关的事件：

  ```text
  ej = argmax_{ek∈E} similarity(q, ek)
  ```

- **时间感知推理**：
  - 若事件 ej 早于事件 ek，则 T(ej) ⪯ T(ek)。
  - 时间标记作为事件节点属性，时间关系作为图边，由 LLM 解释这些信息以还原事件演进过程。
- **多事件推理**：
  - 智能体采用迭代式检索与多跳推理，不依赖单次检索。
  - 逐步链接逻辑上或时间上相关的事件，构建中间推理路径，并对照图结构进行一致性校验。
- **反思与自校正**：
  - 推理中定期检查结论的连贯性，发现矛盾或歧义时重新访问相关事件节点、修正推理方向。
  - 可减少错误推理与幻觉，尤其在需要多事件链式推理时。

## 3. 实验设计

### 3.1 数据集与任务场景

- **生成有效性评测**：使用 UltraDomain 中的 agriculture、cooking、history 数据集，以及真实的实验室协议场景数据集 bioprotocol。
  - 这些数据集包含多文档输入，要求事件理解与时间感知能力。
  - 在实验中为每个数据集用 LLM 生成 125 个问题（见附录）。
- **推理能力评测**：使用 MultiHopRAG 数据集，包含四类查询：
  - Inference Query（逻辑推断）；
  - Comparison Query（事件属性比较）；
  - Null Query（判断无答案/证据不足）；
  - Temporal Query（事件时间关系理解）。
  - 实验时选取前 100 个问题作为评测集。

### 3.2 对比方法

- NaiveRAG（朴素向量检索 + LLM 生成）。
- GraphRAG（基于图结构的 RAG）。
- LightRAG（轻量图 RAG）。
- 所有方法使用相同底层 LLM 与检索设置（GPT-4o、milvus 向量库等）以保证公平性。

### 3.3 评测指标

- 生成有效性：六个维度的两两胜率：Comprehensiveness、Diversity、Empowerment、Logic、Directness、Overall Winner，使用 LLM 进行答案配对评测。
- 推理能力：RAGAS 框架中的 Answer Relevancy、Answer Correctness、Semantic Similarity。

### 3.4 实验类别

- **实验一：生成有效性**，对比四类基线，报告六维度胜率。
- **实验二：推理能力**，在 MultiHopRAG 上按四类查询分别测试。
- **实验三：消融分析**：
  - 去掉 Expand Knowledge（w/o EK）；
  - 去掉 Multi-event Reasoning（w/o MB）；
  - 均与 NaiveRAG 对比胜率。
- **案例研究**：展示 EventRAG 与 GraphRAG 在同一历史问题上的回答差异。

## 4. 资源与算力

- 论文未明确说明使用的 GPU 型号、数量或训练/推理时长。
- 实现中使用了 OpenAI GPT-4o API (`gpt-4o-2024-08-06`) 作为所有 LLM 相关操作（抽取、构建、生成、评测）的默认模型，并使用 `text-embedding-3-small` 作为嵌入模型、milvus 作为向量数据库。
- 由于主要依赖外部 API，算力成本更多体现为大量 LLM 调用次数，而非本地 GPU 显式算力消耗。

## 5. 实验数量与充分性

- **实验数量**：
  - 在四个域（agriculture、cooking、history、bioprotocol）上各进行生成效果对比；
  - 在 MultiHopRAG 上覆盖四类推理查询；
  - 执行了两组消融（去掉知识扩展、去掉多事件推理），并配有案例研究。
  - 单独从表看，共形成三张主要结果表与一张案例表，实验规模较充分。
- **充分性与公平性**：
  - 数据集覆盖不同领域与文档规模，基准选择主流 RAG 方法，实验较为全面。
  - 所有对比方法统一使用同一 LLM、相同 chunk 大小和 gleaning 参数，具有相对公平的设定。
  - 但是，评测本身也使用 GPT-4o 进行两两“胜率”判断，可能存在大模型评审者的偏好偏差；同时 MultiHopRAG 只取前 100 个问题，采样规模不够大，可能影响统计显著性。
  - 未与其他基于事件结构的 RAG 系统进行比较，baseline 仅限三段式 RAG 与图式 RAG。

## 6. 主要结论与发现

- EventRAG 在几乎所有数据集和大部分指标上优于 NaiveRAG、GraphRAG 与 LightRAG。
- 尤其在 **Comprehensiveness（信息完整性）** 与 **Logic（逻辑一致性）** 上提升最明显，说明事件知识图谱有助于跨文档的事件聚合与连贯叙述。
- 在 MultiHopRAG 推理任务中：
  - Average Answer Correctness 达到 0.7158，较最强基线 LightRAG（0.5713）提升约 14.5 个百分点；
  - Temporal Query 的 Answer Correctness 达到 0.8786，显著高于其他基线；
  - Null Query 上错误/过度自信的回答减少，体现出反思与自校正机制的作用。
- 消融实验表明：
  - 实体融合与知识扩展能显著增强知识图谱的完整性和覆盖度；
  - 多事件推理对长程依赖捕获与逻辑一致性至关重要；
  - 即使移除某些组件，EventRAG 变体仍优于 NaiveRAG，说明事件中心表示本身是有效的。

## 7. 优点

- **事件中心的表示方式**：相较“扁平化文本片段”，EKG 显式呈现事件间时间与逻辑关系，能更好地支持叙事理解和跨文档推理。
- **实体融合 + 知识扩展**：在保留原始出处的基础上合并等价信息，补全弱连接，提升知识图谱的完整性与鲁棒性。
- **时间感知推理**：把时间顺序纳入事件边建模，使模型能回答“事件先后、因果演进”等时间敏感问题。
- **智能体式多事件推理与自校正**：通过迭代查询、逻辑链构建、检查一致性和修正结论，显著降低幻觉与碎片化输出。
- **实验验证充分**：结合多领域生成任务和多种推理查询类型，并通过消融分析证明各组件贡献，案例分析直观展示效果提升。

## 8. 不足与局限

- **计算开销大**：论文自己指出，知识图谱构建依赖多次 LLM 调用（事件抽取、关系识别、实体融合、知识扩展等），文档量大时效率低，不适合实时或计算资源受限的场景。
- **应用风险**：在实时新闻、社会运动等动态变化场景中，用户可能过度依赖系统对事件时间线的推理，甚至用以预测未来事件，容易得出过于简化的结论；系统更适合作为辅助工具而非决策主体。
- **评测依赖与表征偏差**：
  - 所有方案的生成和评估都基于同一 LLM，评测胜率可能带有模型偏好；
  - 事件抽取和知识扩展质量高度依赖底层 LLM 能力，且无法完全避免漏抽或错抽。
- **事件类型和领域覆盖有限**：实验主要集中于农业、烹饪、历史、生物协议等文本，对更多样化的开放领域、对话场景和流式新闻的适用性尚未验证。
- **未提供端到端系统性对比**：将 EKG 构建作为离线阶段，与在线 RAG 查询之间的协同效率、时间成本等缺少更细粒度的量化分析。

（完）
