---
title: Query Optimization for Parametric Knowledge Refinement in Retrieval-Augmented Large Language Models
title_zh: 面向参数化知识精炼的检索增强大模型查询优化
authors: "Youan Cong, Pritom Saha Akash, Cheng Wang, Kevin Chen-Chuan Chang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.193.pdf"
tags: ["query:hallu-rag"]
score: 7.0
evidence: 提出抽取-精化-检索-阅读的RAG查询优化框架，利用参数化知识精化检索以提升知识支撑与事实准确性
tldr: 为弥补检索增强生成系统中检索前信息不足的问题，论文提出ERRR框架，先从大语言模型中抽取参数化知识，再通过专门的查询优化器精化检索式，使系统只检索对生成答案最必要的信息。该方法还提供可训练管道以增强灵活性和降低计算成本。实验结果显示它能提升RAG的知识支撑质量和生成准确性，是缓解模型幻觉的一种有效途径。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp193/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1502, \"height\": 1142, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp193/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 843, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp193/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1236, \"height\": 531, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp193/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1194, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp193/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1116, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp193/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1666, \"height\": 1080, \"label\": \"Table\"}]"
motivation: 检索增强生成存在预检索信息缺口，常规查询优化未考虑模型自身的参数化知识需求。
method: 先抽取大模型的参数化知识，再对查询进行精化，并用可训练管道优化检索与生成。
result: 系统可聚焦检索关键信息以支持准确生成，同时降低计算成本并更灵活。
conclusion: 将参数知识抽取用于查询优化可增强RAG的知识锚定和事实准确性。
---

## Abstract
We introduce the Extract-Refine-Retrieve-Read (ERRR) framework, a novel approach designed to bridge the pre-retrieval information gap in Retrieval-Augmented Generation (RAG) systems through query optimization tailored to meet the specific knowledge requirements of Large Language Models (LLMs). Unlike conventional query optimization techniques used in RAG, the ERRR framework begins by extracting parametric knowledge from LLMs, followed by using a specialized query optimizer for refining these queries. This process ensures the retrieval of only the most pertinent information essential for generating accurate responses. Moreover, to enhance flexibility and reduce computational costs, we propose a trainable scheme for our pipeline that utilizes a smaller, tunable model as the query optimizer, which is refined through knowledge distillation from a larger teacher model. Our evaluations on various question-answering (QA) datasets and with different retrieval systems show that ERRR consistently outperforms existing baselines, proving to be a versatile and cost-effective module for improving the utility and accuracy of RAG systems.

---

## 论文详细总结（自动生成）

# 《面向参数化知识精炼的检索增强大模型查询优化》论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大型语言模型（LLM）在检索增强生成（RAG）系统中存在**“预检索信息差距”（pre-retrieval gap）**——即使用原始用户查询所检索到的文档，与生成最优回答所需的关键知识之间存在失配，导致检索结果不精准、回答质量受限。
- **研究动机**：现有 RAG 查询优化方法（如 RRR）虽能改写/扩展用户查询，但**未能考虑 LLM 读者自身的参数化知识需求**（即模型已经知道什么、还需要什么外部信息来补足或验证），因此无法有针对性地消除预检索差距，检索到的内容仍然可能不够精准，影响知识支撑质量和最终生成准确性。
- **整体意义**：论文从“对齐外部检索与模型内部知识缺口”的角度切入，引入先抽取 LLM 参数化知识再据此优化查询的流程，为提升 RAG 系统的事实准确性和知识利用效率提供了新思路，有助于缓解LLM在开放域问答中因知识不足或检索干扰产生的**事实性偏差与幻觉**问题。

## 2. 论文提出的方法论

### 2.1 总体框架：ERRR（Extract-Refine-Retrieve-Read）

- **核心思想**：先让 LLM 输出它已经具备的“参数化知识”（伪上下文文档），再基于这些已知信息生成针对性的优化查询，去外部检索**验证或补充**内部知识，避免检索到大量无关信息，从而提高生成质量。
- **关键公式阐述**：论文将原始 RAG 定义为 `LLM(R(q), q | θ)`，但由于 `R(q)` 与理想文档集 D 之间存在差距，因此引入一个针对特定查询的优化函数 f′(C, q)，使得 `LLM(R(f′(C, q)), q | θ)` 能更好地逼近“理想检索结果”，其中 `C = E(q | θ)` 即参数化知识抽取结果。

### 2.2 四个核心步骤

1. **参数化知识抽取（Extract / Parametric Knowledge Extraction）**
   - 直接向 LLM 提问，使其生成一段包含相关背景信息的伪上下文文档。
   - 该文档被视作 LLM 参数化知识的一种抽象表征，即为后续查询优化提供上下文素材。

2. **查询优化（Refine / Query Optimization）**
   - 使用一个专门的 LLM“查询优化器”，依据抽取出的参数化知识，生成一条或多条优化查询语句；
   - 这些查询旨在验证或补充模型已有知识，尤其关注时间敏感信息等容易过时或缺失的内容。
   - 查询之间用分号分隔，以“**”结尾作为输出结束符。

3. **检索（Retrieve）**
   - 适配两种检索场景：黑盒网页搜索工具（Brave Search API）和本地稠密检索系统（WikiDPR + DPR）。
   - 每条查询取 top-5 结果，与原始问题拼接后交给 LLM 读者处理。

4. **生成（Read / Generation）**
   - 使用 LLM 读者基于拼接过原始问题的检索文档生成最终答案。

### 2.3 可训练方案（Trainable Scheme）

- 使用**知识蒸馏**训练一个小型可调模型（T5-Large，7.7 亿参数）充当查询优化器；
- 由 GPT-3.5-Turbo 在统一设置下生成蒸馏数据，T5 通过在 QA 数据集上微调（每数据集 3 epoch）学会查询优化任务；
- 优点是降低成本（省去推理时调用 GPT-3.5-Turbo 进行查询优化的开销）、增加定制灵活性，且在实际实验中性能反超了教师模型（GPT-3.5-Turbo）。

## 3. 实验设计

### 3.1 数据集

- **AmbigQA（AmbigNQ）**：测试集前 1000 条样本，考察对天然歧义问题（多答案）的处理能力；
- **PopQA**：测试集前 997 条样本，考察长尾（冷门）知识问题；
- **HotpotQA**：评估全量测试集，考察多跳推理能力。
- **指标**：Exact Match（EM）和 F1 分数。

### 3.2 基线方法

| 基线 | 说明 |
|------|------|
| Direct | 无检索，直接调用 GPT-3.5-Turbo 回答 |
| RAG | 经典检索增强生成，原查询直接检索 |
| ReAct | 推理与行动交错进行的迭代式 RAG |
| Frozen RRR | GPT-3.5-Turbo 训练的查询重写器（RRR 原始设定） |
| Trainable RRR | 用监督微调 + PPO 强化学习的 T5-large 重写器 |
| Self-RAG | 用于代价/延迟对比的迭代反思框架 |
| Frozen ERRR | 论文提出的冻结版方法（查询优化器用 GPT-3.5-Turbo） |
| Trainable ERRR | 论文提出的可训练版方法（查询优化器用微调 T5） |

### 3.3 检索环境

- 网页检索：Brave Search API（实际模拟真实检索场景）；
- 本地检索：WikiDPR 静态语料库（2018 年 12 月的 2100 万段落，DPR 向量检索）；
- 两套环境中均取 top-5 段落。

## 4. 资源与算力情况

- 论文**未明确说明完整实验所用的 GPU 型号、数量和端到端训练时长**；
- 仅提及的可参考成本与训练信息包括：
  - Trainable ERRR 的 T5-Large 微调参数：每个数据集训练 3 epochs，学习率 1e-4，batch size 4；
  - Trainable RRR 复现训练参数：学习率 2e-5，3 epochs，batch size 8；
  - 蒸馏数据集由 GPT-3.5-Turbo 针对各数据集训练集产生；
  - 部分实验因资源有限仅做了 500 条（HotpotQA 上评估 ReAct）或 200 条（成本测试）随机样本；
  - 论文在 Limits 中明确承认由于计算资源限制，未训练基于 PPO 的强化学习方案。

## 5. 实验数量与充分性评估

### 5.1 实验规模

- 主实验覆盖 **3 个开放域 QA 数据集 × 2 种检索系统**；
- 分别测试了 **7 类方法**（在网页检索下为 Direct、RAG、ReAct、Frozen RRR、Trainable RRR、Frozen ERRR、Trainable ERRR；在本地检索下为 Direct、Frozen RRR、Trainable RRR、Frozen ERRR、Trainable ERRR）；
- 额外提供成本与延迟对比实验（HotpotQA 200 条样本，对比 ReAct 与 Self-RAG）；
- 提供附录中的**案例分析**（两组样例对比 RRR 与 ERRR）。

### 5.2 充分性分析

- **优点**：跨越了不同数据集类型（歧义/冷门/多跳）、不同检索后端（实时网络检索与历史静态语料库）、不同 LLM 配置（冻结 vs 可训练）；探究了成本/延迟维度，并给出了直观性案例，证明 ERRR 框架的普适性较强。
- **不足**：
  - 缺少消融实验（例如：去掉参数化知识抽取步骤、或直接用原始查询当上下文、或对生成阶段不同提示法做对比）；
  - 未与更多先进的 RAG 变体（Self-RAG、CRAG 等）在同一评估协议中全量对比，仅做了成本/延迟对比；
  - 部分源语言模型的开放式回答受限于 EM/F1 指标的覆盖度，难以全面反映知识支撑的质量；
  - 将全部计算资源限制归因于训练成本和 API 限制，没有报告统一的 retriever 与 reranker 提示等扰动控制；
  - 公平性上：虽然声称使用与原论文一致的实施细节，但小模型训练数据仅是各数据集训练集，原始 RRR 是否用同一子集并不清楚，且 ReAct 等基线未全量测试，容易低估或高估相对效果。

## 6. 论文的主要结论与发现

- ERRR 框架在 **AmbigQA、PopQA、HotpotQA** 上，同时使用网页检索和本地稠密检索时，都稳定优于 Direct、RAG、ReAct、Frozen RRR、Trainable RRR 等基线方法；
- “可训练版 ERRR”（T5 蒸馏）在三个数据集上都超越了自身教师模型（GPT-3.5-Turbo），说明从大模型中提炼知识、专用化地注入小模型的训练方案有助于泛化简化和任务适配；
- ERRR 相比传统 RRR 的优势在于：不是机械地重写问题，而是找出“模型已知什么 / 需要补充或验证什么”，从而在检索前就有了明确的信息需求导向；
- ERRR 在**低质量检索语料**（过时、窄域的 WikiDPR）下仍保持较强的鲁棒性，而普通 RAG/RRR 因检索到低质量无关结果反而可能拉低 Direct 的性能——说明 ERRR 能有效避免检索噪声的误导；
- 网页检索环境中 ERRR 的性能提升比本地稠密检索更明显，提示其对高质量、多样化知识来源的适应能力更强；
- 成本衡量显示：Frozen ERRR 在费用（$0.62）和延迟（148s）上远低于 ReAct（$1.05 / 202s）和 Self-RAG（$1.65 / 270s），Trainable ERRR 还能进一步减少对大规模 LLM 的重复调用（成本更低、延迟约 140s）。

## 7. 优点

- **方法思路新颖、流程简洁**：第一步抽取参数化知识这一点切中肯綮，直接对齐了 LLM 的信息需求而非单纯“改写查询”，有效缩小了预检索信息差距。
- **通用性强**：框架不绑定特定检索器或模型，网页检索与稠密检索都能适配，灵活度高，可以直接插入现有 RAG 系统作为改进模块。
- **可训练版本有实践价值**：用一个小模型去蒸馏大模型的查询优化能力，使该模块轻量化，同时提升鲁棒性，落地更便利；
- **考虑成本与延迟**：将模型的工程可用性纳入评估维度，比纯追求效果的论文更具现实参考意义。
- **案例展示直观**：用正反例说明了“即使参数化知识包含错误，只要生成的细化查询击中关键验证需求，仍可能纠错并得到正确答案”。

## 8. 不足与局限

### 8.1 实验覆盖方面

- **没有消融**：未分解各模块（尤参数化知识抽取、查询优化指令设计、蒸馏学生模型规模等）的相对贡献，说服力稍微受限。
- **基线覆盖不全面**：ReAct 在 HotpotQA 上只用了 500 条随机样本；Self-RAG 与 CRAG 等更强或自省式基线未在完整评估协议下参与对比；
- **两个检索系统只用了固定的 top-5 通道**：未探索不同 top-k、不同检索器（如 BM25、混合检索等）的影响，泛化性能到其它检索配置还需验证。

### 8.2 偏差风险

- 使用了单一骨干模型 GPT-3.5-Turbo，未验证方法在其他 LLM 上的适用性，结论可能存在模型偏差；
- 训练和测试来源相同（从同一数据集的 train 部分构造蒸馏集、再从 test 部分评测），跨域泛化能力未检验；
- 使用了 2018 年的固定 WikiDPR 语料库替代实时网页搜索，可能造成对模型对实时数据或动态知识的适应力估计不足。

### 8.3 方法自身的局限

- ERRR 依赖基座模型内部已有的知识质量，若内部参数化知识严重错误或不存在，生成的细化查询可能同样偏移不准确；
- 检索结果中若含错误信息，仍有可能误导最终答案（论文虽用案例说明有时能纠正，但并不能保证普遍适用）；
- 蒸馏小模型优化器只在当前数据集上训练，可迁移性和跨领域使用能力仍待评估；
- 使用多查询模式虽然有效，但增加了召回率和上下文阅读负担，对于上下文窗口受限的模型可能不利。


（完）
