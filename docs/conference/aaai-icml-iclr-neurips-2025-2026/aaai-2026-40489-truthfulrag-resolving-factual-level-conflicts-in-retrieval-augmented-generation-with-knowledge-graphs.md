---
title: "TruthfulRAG: Resolving Factual-level Conflicts in Retrieval-Augmented Generation with Knowledge Graphs"
title_zh: TruthfulRAG：用知识图谱解决检索增强生成中的事实级冲突
authors: "Shuyi Liu, Yu-Ming Shang, Xi Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40489/44450"
tags: ["query:faithfulness"]
score: 8.0
evidence: 用知识图谱解决检索知识与内部知识的事实级冲突以提升生成的事实可靠性
tldr: 针对检索增强生成中外部检索知识与模型内部参数知识冲突导致生成不准确的问题，论文指出现有方法在词元或语义层面消解冲突易造成片面理解，提出TruthfulRAG，用知识图谱把冲突上升到事实级进行结构化表示与消解。通过整体把握相关事实关系而非孤立判断，该方法能更清晰地区分外部证据与内部先验，从而提升生成内容的准确性与可靠性。该工作为证据约束生成中的事实冲突处理提供了新框架。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 检索知识库与模型内部知识可能相矛盾，现有冲突消解多局限在词元或语义粒度，难以全面理解事实差异，影响内容可信度。
method: 利用知识图谱在事实层级表示外部检索知识与内部参数化知识之间的冲突，从而进行整体性的冲突发现与消解。
result: 该方法能够结构化解耦外部证据与内部先验，在冲突存在时提升生成内容的准确性与事实一致性。
conclusion: 事实级知识图谱表示有助于更精确地化解检索信息与模型先验之间的冲突，是提升证据约束生成可信度的有效路径。
---

## Abstract
Retrieval-Augmented Generation (RAG) has emerged as a powerful framework for enhancing the capabilities of Large Language Models (LLMs) by integrating retrieval-based methods with generative models. As external knowledge repositories continue to expand and the parametric knowledge within models becomes outdated, a critical challenge for RAG systems is resolving conflicts between retrieved external information and LLMs' internal knowledge, which can significantly compromise the accuracy and reliability of generated content. However, existing approaches to conflict resolution typically operate at the token or semantic level, often leading to fragmented and partial understanding of factual discrepancies between LLMs' knowledge and context, particularly in knowledge-intensive tasks. To address this limitation, we propose TruthfulRAG, the first framework that leverages Knowledge Graphs (KGs) to resolve factual-level knowledge conflicts in RAG systems. Specifically, TruthfulRAG constructs KGs by systematically extracting triples from retrieved content, utilizes query-based graph retrieval to identify relevant knowledge, and employs entropy-based filtering mechanisms to precisely locate conflicting elements and mitigate factual inconsistencies, thereby enabling LLMs to generate faithful and accurate responses. Extensive experiments reveal that TruthfulRAG outperforms existing methods, effectively alleviating knowledge conflicts and improving the robustness and trustworthiness of RAG systems.

---

## 论文详细总结（自动生成）

## 论文总结：TruthfulRAG——用知识图谱解决检索增强生成中的事实级冲突

### 1. 核心问题与研究动机

- **问题背景**：检索增强生成（Retrieval-Augmented Generation，RAG）将外部知识检索与大型语言模型（LLM）的生成能力结合，已被广泛用于改善生成内容的知识密度与时效性。但现实系统中，外部知识库持续更新，而模型内部参数化知识往往陈旧不变，两者之间很容易出现**知识冲突**（knowledge conflict）——即检索到的外部信息与模型记忆中的内部先验产生事实性矛盾，导致模型输出不可靠或不准确。
- **现有方法的粒度缺陷**：论文指出现有冲突消解方法大体可分为两类——词元级（token-level）方法（如通过调节输出分布来抑制或鼓励参数记忆）和语义级（semantic-level）方法（如通过语义对齐将两方知识融合）。但这些方法的共性问题是：粒度不够，无法充分捕捉细粒度的事实关联（factual-level），只看到零散片段，造成对冲突的片面理解，尤其难以应对需要多跳推理的知识密集型场景。
- **论文主张**：知识冲突的解决不应停留在概率分布或语义相似度层面，而应上升到**事实级（factual-level）表示**——即把知识结构化地组织为三元组与知识图谱，并在该层次上定位、分析、消解冲突。

**一句话概括**：TruthfulRAG通过知识图谱将RAG中的知识冲突处理提升到结构化事实层面，有效区分外部证据与内部先验，让LLM更可靠地生成事实正确的回答。

### 2. 方法论：TruthfulRAG框架

TruthfulRAG由三个模块组成，其整体思路是“结构化抽取→图检索→熵过滤”。

#### (1) 模块一：知识图谱构建（Graph Construction）

把检索到的非结构化上下文转化为结构化三元组 KG：

- 给定用户查询 q 与检索内容 C，先把 C 按语义切分为多个连贯文本段 S = {s₁, s₂, …, sₘ}。
- 对每个片段，用同一个生成模型 M 抽取知识三元组 T = {(h, r, t)}，其中 h 是头实体、r 是关系、t 是尾实体；每个实体还可以附带属性描述。
- 汇总得到图 G = (E, R, T_all)，E 是实体集，R 是关系集，T_all 是三元组全集。

该模块的意义：结构化表示能滤除噪声，保留细粒度事实关联，为后续检索与冲突定位奠定基础。

#### (2) 模块二：图检索（Graph Retrieval）

从知识图中找出与查询强相关的推理路径，主要有三步：

- **关键元素抽取**：从查询 q 中提取核心实体、关系与意图类别。
- **语义匹配**：通过稠密嵌入（如 all-MiniLM-L6-v2）计算语义相似度，选出 Top-k 相关实体集 E_imp 和关系集 R_imp。
- **路径遍历与打分**：从每个关键实体出发做两跳遍历，得候选路径集合 P_init，再按事实关联度打分：

  **Ref(p) = α·(路径中关键实体覆盖率) + β·(路径中关键关系覆盖率)**，其中 α、β 控制实体与关系的权重，取 Top-K 路径为 P_super。

每条最终保留的路径会综合三类信息作为上下文：完整顺序推理路径 C_path、重要实体及其属性 C_entities、重要关系及其属性 C_relations。这一步在保持结构连贯的同时丰富语义信息。

#### (3) 模块三：熵驱动冲突消解模块（Conflict Resolution）

通过与纯参数化生成的模型置信度对比来识别冲突路径，核心流程为：

- **基线输出**：模型中无外部上下文时对查询 q 的响应分布：P_param(ans|q) = M(q)。
- **增强输出**：分别加入每条推理路径 p，得到 Paug(ans|q,p) = M(q⊕p)。
- **熵量化**：按输出 token 概率分布计算熵值 H(P)，熵值大小反映不确定程度。
- **冲突信号**：对每条路径计算熵差：
  **ΔHp = H(Paug) − H(Pparam)**
  - ΔHp > 0：外部知识加剧了模型的不确定性 → 说明外部知识与内部先验存在冲突；
  - ΔHp < 0：外部知识降低了不确定性 → 说明知识间大体一致。
- **过滤决策**：留取 ΔHp 超过设定阈值 τ 的路径作为纠偏路径集合 P_corrective，最终用这些路径作为上下文生成最终回应：Response = M(q ⊕ P_corrective)。

该模块的效果是让模型在保留内部合理知识的同时，重点采用外部更具时效性的事实来纠正内部错误记忆——即论文所称的把“冲突知识”变成“纠偏知识”。

### 3. 实验设计：数据集 / 场景 / 基准 / 对比方法

- **数据集（四类知识密集型冲突场景）**：
  1. **FaithEval**：评测在反事实/不一致上下文中模型是否忠实上下文，包括超越实体层的逻辑级复杂冲突。
  2. **MuSiQue**：来自 KRE 研究，含事实级冲突，需多跳组合推理。
  3. **RealtimeQA**：面向时间敏感问题的时效性冲突——旧参数知识 vs. 新外部事实。
  4. **SQuAD**：抽取式问答，构造事实性冲突，用于广泛测试。
  5. 另在 MuSiQue-golden 和 SQuAD-golden 上额外测试非冲突场景。
- **骨干模型（三个LLM）**：GPT-4o-mini（闭源）；Qwen2.5-7B-Instruct、Mistral-7B-Instruct（开源7B级）。体现出对不同架构与规模的一定普适性。
- **对比基线（5类）**：
  - w/o RAG（直接生成，只靠参数记忆）
  - w/ RAG（标准检索增强生成，直接拼接检索文本）
  - KRE：提示优化方法
  - COIECD：解码控制方法
  - FaithfulRAG：语义级冲突建模结合自反思机制
- **评估指标**：ACC 为主指标，附加 CPR（Context Precision Ratio）来衡量处理后上下文对正确答案的密度。实验设置中，温度设为 0，Top-K=10。

### 4. 资源与算力

- 论文明确提到使用 **NVIDIA V100 GPU（32GB 显存）** 完成实验。
- 但**未说明具体使用的 GPU 数量、训练时长、总共运行的计算量**，也未报告推理的经济开销或评价改进方法引入的额外计算负担。
- 隐含的问题是：方法论的整体计算成本（三元组抽取 + 图谱检索 + 多次生成前向与熵计算）实际上并不低，但论文未给出定量分析（如延迟、FLOPs、性能-成本权衡曲线）。

### 5. 实验数量与充分性评估

- **实验类型覆盖**：
  1. 主实验：3个模型 × 4个数据集 × 6种方法（含自身），规模较完整；
  2. 非冲突场景验证实验（golden 上下文）；
  3. 结构化路径对模型置信度影响的分析实验；
  4. 消融实验（去掉知识图谱/去掉冲突消解，报告 ACC 与 CPR）。
- **充分性总体评价**：实验设计在对比范围上做到了合理覆盖，主实验与消融打通了“性能—组件→作用机制”链条，结论证据层层递进，整体较系统。
- **不足之处**：
  - 消融实验只在 GPT-4o-mini 上完成，缺少对开源模型（Qwen、Mistral）的消融验证；
  - 未做参数敏感度分析（如 α、β、τ 对不同数据集的敏感程度）；
  - 未实验不同检索器与不同三元组抽取方式对结果的影响；
  - 使用“平均准确率”作聚合性指标时，没有披露方差/显著性检验结果；无法判断差异是否显著。

### 6. 主要结论

- **优越性能**：TruthfulRAG 在四个数据集与三个LLM上总体达到最优或次优的 ACC，在全部骨干模型上取得了最高的平均准确率和最大的相对提升（较无检索基线的改善最高达 66.1%）。相比标准 RAG 提升幅度为 3.6%~29.2%。
- **在非冲突场景下也具有稳健收益**：在 MuSiQue-golden（比标准RAG +3.3%）与 SQuAD-golden（+0.4%）上都取得了最好的效果，说明它不只是“冲突矫正器”，其知识图谱结构本身增强了对知识的精细理解。
- **结构化推理路径提升模型置信度**：图3显示，以结构化推理路径为上下文时，模型对正确答案的负对数概率（越低越自信）普遍低于自然语言文本检索上下文，表明结构化路径有效提高模型对外部知识的采纳意愿。
- **组件协同效应明显**：消融研究表明，知识图谱单独使用已有明显收益（能提高CPR），熵过滤单独使用也能改善一些方向（有些数据集API有下降），两者组合效果最佳，证明框架设计是相互配套、互为补充的有机整体。

### 7. 方法亮点

- **把冲突消解的粒度提升到“事实级”**：图（实体-关系-属性）的表达比词元级/语篇级更精细，也更贴近人类对“fact”的理解，对矛盾场景的解释力更强。
- **结构先行的思路**：通过知识图谱构建发现相关“路径”而不是零散片段，天然适合多跳逻辑推理类 QA，这是前序方法的弱项。
- **熵差引导冲突识别**：用“有无检索上下文时的信息不确定性差”作为信号，隐含假设来自内部知识与外部证据的双重证据冲突会造成不确定性上升，这个思路简洁、无需监督数据，对整个 RAG 自动纠偏管线更具可实现性。
- **与一般 RAG 框架可插拔**：设计上不干扰底层检索和模型，对外部检索系统具有一定的即插即用能力。
- **可解释性好**：把模型“信什么”“纠了什么”外化为可被检验的路径与熵信号，比黑盒概率操控更好理解。

### 8. 不足与局限

#### 实验层面的局限
- 只验证了三种LLM、两个开源均为7B规模，缺更大规模模型的验证；也难以确知在超出论文阈值设定时对大模型（例如 GPT-4 级别或 70B+ 开源模型）是否具有相同优势。
- 只在英文数据集上实验，未讨论多语言冲突场景。
- 没有给出运行开销的量化预估（图谱构建时间、额外推理成本等）。
- 没有对 τ、α/β、保留路径数K的敏感度做网格分析，导致可复现性受到一定削弱。
- ACC 在很多数据集上本就偏饱和（在 SQuAD-golden 已经 98.3%），用来区分方法之间的精度差异的敏感性有限。

#### 方法层面的局限与隐患
- **依赖三元组抽提质量与模型能力**：对整个图谱的构建由大模型本体完成，若模型对文本理解不够而导致三元组抽取不完整或错误，图检索和后续判断都会被带偏。
- **只保留“熵差较大”路径可能会丢失本应该被信任的检索内容**：对外部知识信心不充分时（尤其针对模型在未知领域上本身很自信时）会导致错误纠偏或错误的路由策略。
- **忽略多文档冲突的场景**：目前的框架设计基本以“上下文路径整体为单位”，并未在逻辑模型层面区分“证据之间互相冲突”的情况。
- **基于语义聚类的图检索会遗漏非语义相关的实体推理链**：本质关联需要通过数值、空间或逻辑约束串联，而相似嵌入可能把它漏掉。
- **阈值依赖不同模型设置不同的 τ**，在实践中对不同域/不同模型都需要重新调参，不够自适应性。

#### 潜在验证偏差
- “结构化路径提高 LLM 置信度”实验主要基于模型对自己输出的 logprob，而 logprob 高不完全等同于事实正确；测试集中于该模型有能力回答的已知范围，对完全开放领域结论的适用性有待更广验证。

### 结论简评

TruthfulRAG 在“面对检索知识与内部先验冲突时，LLM 该如何决定信什么”这一实际困境中提出了清晰且有一定原创性的路线——借助知识图谱把冲突上升到结构化的“事实关系”层面，再通过熵的升降让模型自我暴露并过滤出纠偏知识。主实验中的一致改进验证了路线本身的价值。但工程上是否完全优越，除了精度，还需更多考虑计算成本与抽取模型的鲁棒性。

（完）
