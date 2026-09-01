---
title: "HopRAG: Multi-Hop Reasoning for Logic-Aware Retrieval-Augmented Generation"
title_zh: HopRAG：面向逻辑感知检索增强生成的多跳推理方法
authors: "Hao Liu, Zhengren Wang, Xi Chen, Zhiyu Li, Feiyu Xiong, Qinhan Yu, Wentao Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.97.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 通过多跳逻辑推理改进RAG检索，增强知识接地
tldr: 针对传统检索器只关注词法或语义相似度而忽略逻辑相关性的问题，提出HopRAG。该方法在索引阶段构建文本块为节点的段落图，并通过LLM生成伪查询建立逻辑连接；检索阶段采用检索-推理-剪枝机制，沿多跳邻居寻找真正相关的段落。在多个数据集上验证了检索与生成质量的提升。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl97/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 743, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl97/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1594, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl97/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1624, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl97/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1243, \"height\": 1227, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl97/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1245, \"height\": 1242, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl97/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1255, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl97/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1153, \"height\": 296, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 726, \"height\": 1043, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1153, \"height\": 545, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1156, \"height\": 544, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1483, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1487, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1485, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1319, \"height\": 886, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1523, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1630, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl97/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1607, \"height\": 2314, \"label\": \"Table\"}]"
motivation: 传统RAG检索器依赖浅层相似度，难以应对逻辑相关的复杂检索需求。
method: 构建段落图并用LLM生成伪查询作为边，检索时通过多跳推理和剪枝选择逻辑相关段落。
result: 实验表明HopRAG在多个基准上显著提升检索相关性和RAG生成质量。
conclusion: 为逻辑感知检索提供了新型图增强RAG框架。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems often struggle with imperfect retrieval, as traditional retrievers focus on lexical or semantic similarity rather than logical relevance. To address this, we propose HopRAG , a novel RAG framework that augments retrieval with logical reasoning through graph-structured knowledge exploration. During indexing, HopRAG constructs a passage graph, with text chunks as vertices and logical connections established via LLM-generated pseudo-queries as edges. During retrieval, it employs a retrieve-reason-prune mechanism: starting with lexically or semantically similar passages, the system explores multi-hop neighbors guided by pseudo-queries and LLM reasoning to identify truly relevant ones. Experiments on multiple multi-hop benchmarks demonstrate that HopRAG’s retrieve-reason-prune mechanism can expand the retrieval scope based on logical connections and improve final answer quality.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 传统 RAG 系统的检索模块主要依赖**词法相似度**（如 BM25）或**语义相似度**（如 dense retriever），而忽略了**逻辑相关性**。
- 这种“不完美检索”（imperfect retrieval）问题在多跳问答（multi-hop QA）中尤为突出：
  - **精确性方面**：可能返回词法和语义相似但逻辑上不相关的段落；
  - **召回率方面**：可能遗漏回答用户问题所必需的关键段落。
- 论文实证发现（Figure 1）：即便使用较强的 BGE dense retriever，在 MuSiQue、2WikiMultiHopQA、HotpotQA 上召回率最高仅约 0.45；且超过 60% 的检索结果属于“间接相关”或“不相关”段落。
- 受“六度分隔理论”/小世界网络启发，作者提出：**间接相关的段落可作为“垫脚石”，通过逻辑关系跳转到真正相关的段落**。
- 核心研究问题：**能否将 LLM 的推理能力引入检索模块，实现逻辑感知的 RAG？**

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 2.1 核心思想

- 提出 **HopRAG**，一个图结构化的 RAG 框架，将段落组织为图，用**逻辑关系边**连接段落，并在检索时通过**多跳推理**在图中跳转，寻找真正相关的段落。
- 整体流程为 **Retrieve-Reason-Prune（检索-推理-剪枝）** 三步范式。

### 2.2 图结构索引构建（Graph-Structured Index）

- 顶点：每个段落 \( p_i \) 作为一个顶点 \( v_i \)。
- 边：基于**LLM 生成的伪查询（pseudo-queries）** 建立有向逻辑边。

#### （1）查询模拟（Query Simulation）

- 对每个段落 \( p_i \)，用 LLM 生成两组伪查询：
  - **出向问题** \( Q_i^+ \)：从该段落出发、但段落自身无法回答的问题（m 个）；
  - **入向问题** \( Q_i^- \)：答案包含在该段落中的问题（n 个）。
- 对每个问题执行：
  - 用 NER 提取关键词（稀疏表示 \( K \)）；
  - 用 embedding 模型编码为向量（稠密表示 \( V \)）。
- 形成三元组：出向三元组 \( r_{i,j}^+ := (q^+, k^+, v^+) \)，入向三元组 \( r_{i,j}^- := (q^-, k^-, v^-) \)。

#### （2）边合并（Edge Merging）

- 对每个出向三元组 \( r_{s,i}^+ \)，用**混合检索**（稀疏+稠密）匹配最相似的入向三元组 \( r_{t^*,j^*}^- \)，在两个段落之间建立有向边。

- 相似度公式：

\[
SIM(r_{s,i}^+, r_{t,j}^-) = \frac{ \frac{|k_{s,i}^+ \cap k_{t,j}^-|}{|k_{s,i}^+ \cup k_{t,j}^-|} + \frac{v_{s,i}^+ \cdot v_{t,j}^-}{\|v_{s,i}^+\| \cdot \|v_{t,j}^-\|} }{2}
\]

- 边特征聚合为：\( e_{s,t^*} := (q_{t^*,j^*}^-, k_{t^*,j^*}^- \cup k_{s,i}^+, v_{t^*,j^*}^-) \)。

### 2.3 推理增强的图遍历（Reasoning-Augmented Graph Traversal）

- 检索阶段：对用户查询 q 做 NER + embedding，通过混合检索匹配 top-k 条边，将对应顶点放入队列 \( C_{queue} \)。
- 推理阶段：对队列中的每个顶点，LLM 阅读其所有出向边上的问题，**选择对回答 q 最有帮助的一个边**并跳转到目标顶点，用计数器 \( C_{count} \) 记录顶点访问次数。进行 \( n_{hop} \) 轮跳转。
- 剪枝阶段：定义 **Helpfulness 指标**，综合考虑文本相似度和逻辑重要性，保留 top-k 顶点：

\[
H_i = \frac{SIM(v_i, q) + IMP(v_i, C_{count})}{2}
\]

其中：

\[
IMP(v_i, C_{count}) = \frac{C_{count}[v_i]}{\sum_{v_j \in C_{count}} C_{count}[v_j]}
\]

- 算法流程：初始化 → 检索 → 每轮对队列中每个顶点做 LLM 推理选边跳转 → 更新访问计数 → 剪枝 → 输出上下文。

## 3. 实验设计

### 3.1 数据集 / Benchmark

- **MuSiQue**（1000 个问题）
- **2WikiMultiHopQA**（1000 个问题）
- **HotpotQA**（1000 个问题）

三个均为多跳问答数据集，每个查询需要多篇支持段落才能回答。

### 3.2 对比方法（Baselines）

| 类别 | 方法 |
|---|---|
| 非结构化 RAG | BM25（稀疏检索） |
| 非结构化 RAG | BGE（稠密检索） |
| 非结构化 RAG | BGE + Query Decomposition |
| 非结构化 RAG | BGE + Reranking |
| 树结构 RAG | RAPTOR |
| 树结构 RAG | SiReRAG |
| 图结构 RAG | GraphRAG（local search） |
| 图结构 RAG | HippoRAG |

### 3.3 评估指标

- **回答质量**：Exact Match (EM)、F1 score
- **检索质量**：Retrieval F1（在消融/讨论部分使用）

### 3.4 设置

- 嵌入模型：BGE（768 维）
- 图生成与遍历推理模型：GPT-4o-mini
- 回答生成模型：GPT-4o 和 GPT-3.5-turbo
- 上下文候选数 top k = 20，跳数 \( n_{hop} \) = 4

## 4. 资源与算力

- 论文**未明确报告**使用的 GPU 型号、数量或训练/推理的具体算力开销。
- 仅在附录 A.7 中提供了**检索延迟估算**：
  - 使用 Qwen2.5-1.5B-Instruct 作为遍历模型时，每个问题约需调用 LLM 38.53 次；
  - 每次调用输入约 500 tokens、输出约 20 tokens；
  - BF16 + Transformer 推理约需额外 18.86 秒/问题；
  - 使用 vLLM + GPTQ-Int4 优化后可降至约 4.43 秒/问题；
  - 提出可用多线程并行进一步加速。

## 5. 实验数量与充分性

### 5.1 实验组数

| 实验类别 | 数量/内容 |
|---|---|
| 主实验（Table 1 & 2） | 3 个数据集 × 8 种方法 × 2 种 reader 模型（GPT-3.5-turbo、GPT-4o） |
| 超参数敏感性（top k） | Table 3：top k 从 2 到 20 共 6 档，在 3 个数据集上评估 |
| 超参数敏感性（n_hop） | Table 4 / Table 8：n_hop 从 1 到 4，在 3 个数据集上评估 |
| 遍历模型消融 | Table 5：非 LLM、Qwen2.5-1.5B-Instruct、GPT-4o-mini 三种遍历模型，3 个数据集 |
| 案例分析 | 附录 A.6：HopRAG vs GraphRAG 的图结构对比 |
| 检索效率分析 | 附录 A.7：延迟估算 |

### 5.2 充分性与公平性评估

- **充分性**：实验覆盖了 3 个主流多跳 QA 数据集、8 种基线方法、多种超参数设置和消融，覆盖面较广。
- **公平性**：
  - 将非结构化基线也放在 Neo4j 图数据库上检索，对齐检索引擎；
  - 树结构方法因引入摘要节点，未参与检索指标对比，避免不公平比较；
  - 使用两种不同 reader 模型（GPT-3.5-turbo、GPT-4o）验证鲁棒性。
- **潜在不足**：检索指标仅用于 HopRAG 自身的消融分析，未与图方法（如 HippoRAG）直接对比检索 F1。

## 6. 论文的主要结论与发现

- HopRAG 在绝大多数设置下取得最优或次优结果：
  - 相比 BGE dense retriever，回答指标平均提升约 **76.78%**；
  - 相比 query decomposition 提升约 **48.62%**；
  - 相比 reranking 提升约 **36.25%**（与摘要中“over 36.25% higher answer metric”一致）；
  - 相比 RAPTOR 提升约 **9.94%**；
  - 相比 HippoRAG 提升约 **3.08%**；
  - 相比 SiReRAG 提升约 **1.11%**。
- 检索 F1 相比传统方法提升约 **20.97%**。
- 即使在 top k = 12 时，HopRAG 的回答质量仍可与 HippoRAG/RAPTOR 在 top k = 20 时相当，说明图遍历能在更小的上下文预算下高效找到相关信息。
- 随着 n_hop 增加，检索性能提升，但 LLM 调用成本也随之增加；第 5 跳时平均队列长度仅 1.23，说明 4 跳已基本覆盖局部图区域。
- 即使**不用 LLM** 做推理（纯相似度匹配跳转），HopRAG 仍比 BM25 高 45.84%、比 BGE 高 25.43%；引入 LLM 推理后可再提升约 45.78%。

## 7. 优点

- **创新性**：首次系统性地将“伪查询作为逻辑边” + “LLM 推理遍历”引入 RAG 检索，填补了相似度检索与逻辑检索之间的空白。
- **索引设计轻量**：相比知识图谱类方法（如 GraphRAG），不依赖预定义 schema、不需要额外文本化三元组、不需要额外实体抽取，避免了信息丢失和幻觉风险。
- **跨文档逻辑建模**：边的构建不受文档边界限制，支持跨文档的多跳推理。
- **检索与推理解耦**：遍历模型可替换（GPT-4o-mini / Qwen2.5 / 甚至非 LLM 的相似度匹配），提供了灵活的成本-性能权衡。
- **可解释性**：访问计数（C_count）和 Helpfulness 指标提供了可解释的剪枝依据。
- **效率优势**：图结构相对稀疏（平均每个顶点 5.87 条边），利于高效遍历；与 HipperRAG 等相比无额外的聚合节点。

## 8. 不足与局限

- **评估范围有限**：仅评估了多跳 QA 场景，未覆盖更多任务类型（如单跳 QA、查询聚焦摘要、开放域问答等），泛化能力未验证。
- **索引构建成本**：需要 LLM 为每个段落生成多组伪查询，对于大规模语料库，索引阶段的 API 成本和延迟可能较高。
- **检索延迟**：遍历过程需要多次 LLM 推理（平均 38.53 次调用/问题），虽然可用小模型或量化加速，但实时性仍受限。
- **图结构度分布**：论文承认段落图的度分布不满足幂律特性，与“小世界网络/六度分隔”的理论类比只是启发式动机，并非严格的理论支撑。
- **边合并策略**：仅保留 O(n·log(n)) 条边，可能丢失一些真实逻辑关系；更复杂的边合并策略可能进一步提升效果。
- **对比公平性**：与 SiReRAG 的优势较小（约 1%），且 SiReRAG 的树结构引入了额外摘要节点；图类方法的检索 F1 未直接横向对比。
- **遍历推理的局限**：每轮只选择一个“最有帮助”的邻居，可能遗漏对回答问题同样重要的其他逻辑路径。

（完）
