---
title: "Relink: Constructing Query-Driven Evidence Graph On-the-Fly for GraphRAG"
title_zh: Relink：为图检索增强生成即时构建查询驱动的证据图
authors: "Manzong Huang, Chenyang Bu, Yi He, Xingrui Zhuo, Xindong Wu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40382/44343"
tags: ["query:hallu-rag"]
score: 7.0
evidence: 按查询动态构建证据图的GraphRAG方法，用结构化知识支撑生成以减少幻觉，处于RAG与忠实性交叉点。
tldr: 当前GraphRAG通常采用先建图后推理的静态知识图谱方式，存在图谱不完整和噪声导致推理链断裂或误导模型的问题。为此提出Relink，其采用先推理后构建的范式，按查询即时构建查询相关的证据图，弥补缺失关系并抑制无关事实。通过动态证据重组，模型可以获得更贴合问题的结构化支撑，从而减少推理错误与幻觉。该工作为基于图检索增强的忠实生成提供了新的思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 静态知识图固有的不完整性和低信噪比会破坏推理或引入误导事实，阻碍GraphRAG减少幻觉。
method: 提出先推理后构建范式的Relink框架，按查询即时构建查询相关证据图，弥补缺失关系并过滤无关事实。
result: 动态证据图能够提供更连贯且相关的支撑结构，减少推理链断裂和干扰信息导致的生成错误。
conclusion: 为基于图证据的检索增强生成提供了一种动态证据组织方法，可提升LLM输出的忠实性。
---

## Abstract
Graph-based Retrieval-Augmented Generation (GraphRAG) mitigates hallucinations in Large Language Models (LLMs) by grounding them in structured knowledge. However, current GraphRAG methods are constrained by a prevailing build-then-reason paradigm, which relies on a static, pre-constructed Knowledge Graph (KG). This paradigm faces two critical challenges. First, the KG's inherent incompleteness often breaks reasoning paths. Second, the graph’s low signal-to-noise ratio introduces distractor facts, presenting query-relevant but misleading knowledge that disrupts the reasoning process.
To address these challenges, we argue for a reason-and-construct paradigm and propose Relink, a framework that dynamically builds a query-specific evidence graph. To tackle incompleteness, Relink instantiates required facts from a latent relation pool derived from the original text corpus, repairing broken paths on the fly. To handle misleading or distractor facts, Relink employs a unified, query-aware evaluation strategy that jointly considers candidates from both the KG and latent relations, selecting those most useful for answering the query rather than relying on their pre-existence. This empowers Relink to actively discard distractor facts and construct the most faithful and precise evidence path for each query.
Extensive experiments on five Open-Domain Question Answering benchmarks show that Relink achieves significant average improvements of 5.4% in EM and 5.2% in F1 over leading GraphRAG baselines, demonstrating the superiority of our proposed framework.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：GraphRAG 通过将大型语言模型（LLM）的推理过程锚定在结构化知识图谱（KG）之上，以缓解 LLM 生成中常见的幻觉问题，尤其适用于复杂的多跳问答任务。
- **核心问题**：现有 GraphRAG 方法普遍遵循 **"先建图、后推理"（build-then-reason）** 范式——依赖一个预先构建的静态知识图谱。这种范式面临两个关键挑战：
    1. **知识图谱固有的不完整性（KG incompleteness）**：静态图谱由于知识演进和抽取误差，往往存在缺失链接，导致推理路径断裂、无法完成多跳推理。
    2. **知识图谱的低信噪比（low signal-to-noise ratio）**：图谱中充斥着大量与查询主题相关但会误导推理的干扰事实（distractor facts），例如图 1 中 `died in` 与 `buried in` 的例子——高度相关但目标错位，会扰乱推理过程。
- **整体含义**：作者认为静态范式采用的 **"one-graph-fits-all"（一图通用）** 策略本质上有缺陷——模型被静态图束缚，而非按需服务具体的用户查询。为此，论文倡导 **reason-and-construct（先推理、后构建）** 的范式转变，提出按查询动态构建"证据图"的新方法。

## 2. 论文提出的方法论

- **核心思想**：提出名为 **Relink** 的框架，基于 reason-and-construct 范式，为每个查询动态构建一个紧凑、与查询对齐的证据图，而非在静态 KG 上做推理。方法包含两个互补的机制：
  - 针对 **KG 不完备性**：从原始文本语料中挖掘"潜在关系池"，按需补全缺失路径。
  - 针对 **干扰噪声**：引入统一的查询感知评估策略，根据候选知识对回答当前查询的"有用性"（而非其是否预先存在于图中）来选边，从而主动丢弃干扰事实。
- **关键技术细节**：
    1. **异构知识源构建（Heterogeneous Knowledge Source Construction）**：
       - **高精度事实图谱 Gb**：由 LLM 从语料库中抽取的三元组构成，作为可靠的骨架，但覆盖有限。
       - **高召回潜在关系池 Rc**：基于文本中的实体共现，用 PMI（互信息）过滤，再用预训练语言模型（Encoder L）对带有 `[MASK]` 标记的上下文编码，以得到潜在关系的稠密向量表示。
    2. **查询驱动的动态路径探索（Query-Driven Dynamic Path Exploration）**：
       - **统一语义空间**：用 Encoder F 将显式 KG 三元组（如 `(h, r, t)`）编码为向量，潜在关系则使用预计算向量。通过对比对齐损失将二者映射到同一语义空间，以使单一排序器可以直接横向比较两类来源的知识。
       - **迭代路径扩展与排序**：使用 beam search 从查询中的主题实体出发**分三步扩展路径**：
         - **候选扩展**：同时在显式图和潜在池中寻找一跳邻居；
         - **查询感知排序（粗排 + 细排）**：先用轻量级 Ranker 筛选噪声候选，再由 LLM 对高潜候选进行细粒度打分（通过结构化 prompt 判断某条边对回答问题语义上的贡献），并按递归算式做路径平均分更新；
         - **动态实例化**：当选择到潜在关系时，用 LLM 结合源上下文与原始查询，将潜在关系实例化为符合查询意图的事实三元组。此步骤既修复了断层，又充当精确的干扰过滤机制。
    3. **联合训练目标**：包括两个损失函数与一个分阶段优化策略：
       - **排序损失 Lrank**：用（q, P+, P−）偏好三元组训练 Ranker，确保它能为正确路径给出更高分；
       - **对比对齐损失 Lcontra**：利用 InfoNCE 损失拉近显式事实与其对应潜在关系在嵌入空间中的距离，实现异构源的可比性；
       - **分阶段训练策略**：先冻结编码器训一层 Ranker，再冻结 Ranker 对齐编码器，如此交替直至验证集收敛，避免两个目标互相干扰。
    4. **证据可溯源的答案生成**：最终生成的证据图谱中，每条边都关联至少一个源文本句子。生成器 LLM 会同时基于查询和附带溯源的结构化证据作答，以增强可验证性和忠实性。

## 3. 实验设计

- **数据集（Benchmark 场景）**：5 个标准多跳问答基准：
  - **2WikiMultiHopQA**
  - **HotpotQA**
  - **ConcurrentQA**
  - **MuSiQue-Ans**
  - **MuSiQue-Full**
- **评价指标**：EM（精确匹配）和 F1，并采用统一的 LLM 抽取答案后处理方式。
- **对比方法（Baselines）**：覆盖多个主要技术路线，统一使用 4 组基线：
  - **LLM-only**：Deepseek-v3、GPT-4o；
  - **Text-based RAG**：Vanilla RAG（LangChain）、RAPTOR（树状结构的文本检索）；
  - **Graph-based RAG**：TOG、G-Retriever；
  - **Hybrid RAG（图+文本混合检索）**：GraphRAG、LightRAG、HippoRAG。
- **统一配置**：所有 RAG 变体（含 Relink）统一使用 **deepseek-v3-0324** 作为骨干 LLM 以保证可比性；每个数据集上随机抽取 **500** 个问题测试以控制成本。
- **实验类型**包括主实验（全数据集对全部基线）、消融实验（删除 4 个组件）、鲁棒性/稀疏性实验（逐次删除显式图的边）和案例分析。各类实验细节见第 5 节。

## 4. 资源与算力

- 论文未明确说明使用的 GPU 型号、数量、训练时长等算力相关信息，也未报告推理时的具体耗时与成本。
- 仅提及在合肥工业大学 HPC 平台上的计算是在该平台完成的（见致谢部分），并指出所有 RAG 方法均统一使用 Deepseek-v3-0324 作为骨干大模型以保证可比性。

## 5. 实验数量与充分性

- **实验数量（组数/广度）**：
  - **主性能对比实验**：5 个数据集 × 10 个基线 = 全面横向比较；
  - **消融实验**：在 2WikiMultiHopQA 和 HotpotQA 两个数据集上，共 4 组消融（去掉显式图 Gb 的变体、去掉动态修复 Rc 的变体、去掉查询感知 Ranker 并将其替换为 OpenAI text-embedding-3-small 词嵌入余弦相似度的方法、去掉对比对齐损失 Lcontra 的变体）；
  - **知识稀疏性实验**：逐步删除显式 KG 边（可最多删至 90%），对比 Relink 完整版与其不含动态修复的变体，在 2WikiMultiHopQA 上评测；
  - **案例分析**（图 4）：具体展示 Relink 面对缺失 composer of 链接和干扰事实时如何动态修复和选边。
- **实验充分性**：
  - **优点方面**：基准覆盖面宽，既有纯 LLM、纯文本 RAG，也有基于图的和混合架构；消融研究任务拆解清晰，能逐项证明各组件（隐式池、显式图骨架、查询感知 Ranker、统一语义对齐）的独立贡献。稀疏性实验模拟了图谱不完整场景，直接检验新范式对静态范式的关键优势。案例研究直观剖析了失效场景和工作机理。这也是本文亮点。
  - **可在更广层面再补充之处**：对于统计显著性检验（例如多次重复运行/方差报告）未给出，不同随机抽样问题的批次差异未作说明。在 500 个随机问题上的一次性评测的稳定性虽在相关工作中较常见，但仍有可能受抽样噪声影响，未做多轮验证。此外，消融实验仅覆盖了其中两个数据集，未探讨在 ConcurrentQA、MuSiQue 等更复杂基准上的消融情况。

## 6. 论文的主要结论与发现

- **主实验结论**：Relink 在全部 5 个数据集的所有评价指标上一致性地优于现有各类基线，相对最强基线 HippoRAG 亦取得显著提升——尤其在与单跳以外的复杂多跳场景中，如 MuSiQue-Full 上相对提升达 32.6%（EM：0.252 vs. 0.190）。相较纯 LLM 与文本 RAG 的方法更是大幅领先。
- **消融实验结论**：
  - 同时需要显式图骨架和潜在关系池：移除 Rc 会导致 HotpotQA 的 EM 相对下降 5.7%，移除 Gb 则下降高达 12.9%；
  - **查询驱动 Ranker 是最重要的组件**：将其替换为通用文本嵌入相似度后，HotpotQA 的 EM 相对降幅达 19.4%，证明通用的语义相关性匹配无法代替面向推理目标的取舍；
  - **统一的语义空间不可或缺**：移除对比对齐损失使 HotpotQA 的 EM 相对下降 7.2%，显示异构知识源的联合推理需要统一的表示空间作为前提。
- **鲁棒性结论**：随着图谱不完整度增加（最多删去 90% 边），静态方法性能崩塌（F1 降 34.7%），而 Relink 几乎不受影响（F1 仍可达 0.669 的水平），说明 reason-and-construct 范式能依托隐式关系池动态补全路径，对现实世界知识图谱的稀疏性有很强的适应力。
- **总体判断**：基于静态图谱的"检索/遍历式"推理本质上存在天花板；动态按查询构建证据图，在应对知识空缺与干扰事实两个问题上，是面向复杂多跳问答更为鲁棒与有效的设计选择。

## 7. 优点

- **问题诊断准确、犀利**：清晰地把静态 GraphRAG 的两大痛点——不完全性和低信噪比——拆分开来，且用案例分析（如 `died in` 干扰 `buried in`）将其具象化，直击现有范式的核心缺陷。
- **方法设计创新**：提出 reason-and-construct 范式本身及其工程设计（异构知识源 + 查询驱动排名 + LLM 动态实例化）即具备方法示范意义。将显式高精度三元组与基于共现的隐式高召回关系统一在同一语义空间中进行竞争性排序，构思自然且具有启发价值。
- **针对幻觉问题的有效机制设计**：每条所选证据（无论显式或推断）都保留文本溯源；LLM 只有在上下文、实例化提示和最终生成时都面对证据链的约束下才能作答，从机制上为忠实可验证的生成提供了支撑。
- **实验设计目标明确**：主实验之外，特意设置了**模拟知识稀疏（删边）**的实验，能直观暴露静态方法的"脆弱性"并凸显动态范式在真实场景中的亮点。
- **可复现性**：提供了代码仓库（https://github.com/DMiC-Lab-HFUT/Relink），且所有基线使用统一框架实现，显著提升了对比公平性。

## 8. 不足与局限

- **算力与代价信息缺失**：论文未报告训练与推理时的 GPU 资源、时间、API 成本等关键资源消耗指标。实际落地时 Relink 每一步（每层候选扩展、粗排 + LLM 细排、潜在关系实例化）都会调用多次 LLM，计算成本相对静态 RAG 可能显著更高。作者未做成本-收益层面的分析。
- **实验覆盖仍可加深**：消融实验只在 2WikiMultiHopQA 和 HotpotQA 上进行；未在 ConcuurentQA 或 MuSiQue 上验证组件的可迁移性。所有实验集中于英文开放域问答，尚未覆盖垂直领域或其它语言场景。
- **统计显著性未讨论**：在随机抽取 500 条样本的实验设置下，模型间分数差距是否具有统计显著性（如采用多次抽样或配对检验方法）没有讨论，结论稳健性有待进一步检验。
- **LLM 依赖性与误差传导**：Ranker 需要刻意构造偏好数据，显式图谱的抽取、潜在关系的过滤与实例化均依赖 LLM。文中未专门评估"LLM 自身抽取错误"如何影响最终图的质量，也未对 LLM 细排阶段的稳定性做置信度分析。
- **鲁棒性实验的模拟方式**与真实的图残缺仍有差异：删边只是让某些待选三元组缺失，但图上实际仍可能存在未被删去的大量"直观有效"的三元组；真实世界的图谱残缺通常与抽样的系统性偏置耦合，情况更复杂。另外，场景中"干扰事实"的过滤主要依赖训练好的 Ranker + LLM 打分，对分布在长尾的偏差难有完善的保证。
- **结构侧重局限**：Relink 主要面向多跳问答中的链式推理，而更复杂的聚合类（如"数量/最值判断"）或比较型问题时，单链式图结构是否依然充分，尚未直接评估。

（完）
