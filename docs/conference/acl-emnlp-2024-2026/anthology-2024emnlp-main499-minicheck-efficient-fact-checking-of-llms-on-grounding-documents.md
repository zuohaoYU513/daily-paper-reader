---
title: "MiniCheck: Efficient Fact-Checking of LLMs on Grounding Documents"
title_zh: MiniCheck：基于证据文档对LLM输出进行高效事实核查
authors: "Liyan Tang, Philippe Laban, Greg Durrett"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.499.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 用轻量模型对LLM输出进行证据文档事实核查，达到GPT-4性能并大幅降本，属事实一致性评测工具
tldr: 针对基于大模型逐项事实核查成本高的问题，使用GPT-4构造兼具真实与困难错误实例的合成数据，训练小型模型MiniCheck。该方法使轻量模型在文档接地判定上达到GPT-4级别效果，而成本约降低400倍。在摘要与RAG等任务上证明小型专用模型足以支撑高效的事实一致性检测，便于大规模评估LLM输出。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main499/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main499/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 103, \"height\": 101, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main499/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main499/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 453, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 776, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 801, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 817, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1662, \"height\": 900, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 630, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 815, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1663, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1663, \"height\": 556, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1662, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1661, \"height\": 544, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 581, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 806, \"height\": 1037, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 821, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 783, \"height\": 510, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 816, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1659, \"height\": 1347, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main499/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1648, \"height\": 2396, \"label\": \"Table\"}]"
motivation: 基于LLM的逐步事实核查需要大量模型调用，成本高，难以大规模部署到摘要与RAG评测中。
method: 用GPT-4按结构化程序生成真实且具挑战性的错误样本作为训练集，训练一个小型分类器检查是否被证据支持。
result: 小模型达到GPT-4的事实核查水平，成本仅为约四百分之一，适合大规模幻觉检测。
conclusion: 高质量合成数据与小模型结合可实现经济和可扩展的证据归因判定。
---

## Abstract
Recognizing if LLM output can be grounded in evidence is central to many tasks in NLP: retrieval-augmented generation, summarization, document-grounded dialogue, and more. Current approaches to this kind of fact-checking are based on verifying each piece of a model generation against potential evidence using an LLM. However, this process can be very computationally expensive, requiring many calls to a model to check a single response. In this work, we show how to build small fact-checking models that have GPT-4-level performance but for 400x lower cost. We do this by constructing synthetic training data with GPT-4, which involves creating realistic yet challenging instances of factual errors via a structured generation procedure. Training on this data teaches models to check each fact in the claim and recognize synthesis of information across sentences. For evaluation, we unify datasets from recent work on fact-checking and grounding LLM generations into a new benchmark, LLM-AggreFact. Our best system MiniCheck-FT5 (770M parameters) outperforms all systems of comparable size and reaches GPT-4 accuracy. We release LLM-AggreFact, code for data synthesis, and models.

---

## 论文详细总结（自动生成）

# 《MiniCheck:基于证据文档对LLM输出进行高效事实核查》详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 判断LLM输出是否能够被证据（grounding documents）所支持，是许多NLP任务的核心：检索增强生成（RAG）、摘要生成、文档接地对话等。
- 现有方法通常依赖LLM逐句、逐事实地对照证据进行核查，虽然准确率高，但计算成本高昂——一篇110–150词的传记可能包含26–41个原子事实，需进行130–205次蕴含判定。
- 该论文的动机正是这种矛盾：**准确性 vs. 效率**。作者希望构建小型、高效、廉价的事实核查模型，使其在准确率上接近GPT-4，同时在成本上降低约400倍。
- 整体定位：作者将多个设定下的“文档接地事实核查”（fact-checking on grounding documents）统一为共享的基础原语操作，试图以一个小型专用模型覆盖所有场景。


## 2. 论文提出的方法论：核心思想、关键技术细节、流程

### 2.1 核心思想
- 高效专用模型 + 高质量合成训练数据：
  - 不依赖市面上已有的任务实例通过LLM蒸馏标签（如ExpertQA的专家问题在设定上无法适用于蒸馏）。
  - 通过**可扩展的合成数据生成管线**从零开始构造有挑战性的事实核查样本，教会模型验证句子中的每个事实，并学会跨句综合信息。

### 2.2 问题形式化（判别器定义）
- 定义判别器 M(Dᵢ,ⱼ, cᵢ) ∈ {0,1}
- 对句子级声明 cᵢ（claim）配对文档 Dᵢ,ⱼ，判定该声明为该文档所支持(1)或不支持(0)。
- 判断句子是否被支持：取 maxⱼ M(Dᵢ,ⱼ, cᵢ)（存在任一文档支持即视为支持）。
- 另外两条简化假设：
  - 假设每个句子“足够原子化”，可以由单个文档独立验证（若需多文档支持，可拼接文档）；
  - 将每条句子单独进行蕴含判断（不依赖上下文；可通过“去上下文化”（decontextualization）步骤补足）。

### 2.3 合成数据生成的两种方法

#### 方法一：C2D（Claim-to-Doc）
核心：**从一个真实的已有声明出发，反向生成文档**，使声明的验证需要跨句综合。

流程：
1. **Step 1——声明分解**：用GPT-3.5将原始声明 c 分解为原子事实 a = {a₁, …, aₗ}。
2. **Step 2——原子事实扩展**：针对每个原子事实 aᵢ，用GPT-4（4-shot）生成两个句子 (sᵢ,₁, sᵢ,₂)，使得存在一个约束：该事实只有在两句话信息合并时才能被支持。
3. **Step 3——支持文档生成**：用GPT-4生成一个文档 D，要求将所有成对信息用自己的话整合在文档内（且不得写出推导出的结论）。
4. **Step 4——非支持文档生成**：通过删掉每个原子事实句对中的一句话，生成文档 D′ₐᵢ\ⱼ = PassageGen(s \ sᵢ,ⱼ)。用GPT-4做ENT检查，确保删除后该原子事实不再被支持。
5. **Step 5——子声明-文档配对扩充**：对原声明的幂集生成子声明（Aug(c) = {Merge(a′): ∀a′ ∈ Power(a)}），根据缺失的事实标签生成更多的正负样本。

#### 方法二：D2C（Doc-to-Claim）
核心：**从真实人类文档出发，生成声明**，提高文档的分布真实感（减少合成文档和真实文档间的分布偏移）。

流程：
1. **Step 1——分块摘要**：将人类撰写的长文档切为三个长度相近的块(D₁, D₂, D₃)，用GPT-4为每块生成一句摘要（视为正样本）。
2. **Step 2——声明分解与子声明扩充**：与C2D类似，将摘要句拆分成原子事实、并生成子声明的幂集。
3. **Step 3——文档-声明增强**：对每块文档Dᵢ=Concat(s)，依次删除每个句子 sᵢ,ⱼ，生成文档 D′ᵢ\ⱼ；再用GPT-4对每个原子事实逐一判断蕴含标签；若全部支持则子声明为支持，否则为不支持。
4. **Step 4——跨文档-声明增强**：将文档块 Dⱼ（ⱼ≠i）与摘要句 cᵢ 配对，通过GPT-4逐原子事实做蕴含判断，进而生成正负样本。

### 2.4 模型架构（MiniCheck系）
三种骨干：
- **MiniCheck-RBTA**：在AlignScore的RoBERTa-large检查点上二分类微调（使用14K合成数据）。
- **MiniCheck-DBTA**：在DeBERTa-v3-large上进行微调（使用21K ANLI + 14K合成数据，合并35K点）。
- **MiniCheck-FT5**（最强）：在Flan-T5-large（770M）上进行微调（同样35K点）。

训练数据的整合：将21K的ANLI难例（原始训练过程中模型预测错误的部分）与约14K的合成数据（C2D约7K + D2C约7K）结合。

判别方式：输出分数 z ∈ [v_min, v_max]，当 M(D,c) > t = 0.5 时预测支持。


## 3. 实验设计：数据集、基准与对比方法

### 3.1 新基准：LLM-AggreFact
- 汇集了10个近期公开的、含人类标注事实一致性评测的数据集，横跨两大类生成场景：
  1. **固定文档生成**（Fixed-Doc Generation）：如摘要、对话摘要。
    - AGGRE FACT（CNN / XSum）、TOFU EVAL（MediaSum / MeetingBank）
  2. **事后接地**（Post-Hoc Grounding）与**检索-生成**（Retrieve-then-Generate）：
    - WICE、REVEAL、CLAIMVERIFY、FACTCHECK-GPT、EXPERTQA、LFQA
- 评估指标：**平衡精度（BAcc）** = ½(TP/(TP+FN) + TN/(TN+FP))，避免类别不平衡干扰。
- 默认不进行每数据集的阈值调整（用0.5中点阈值），以模拟真实零样本部署；附录中也报告了带阈值调整的结果。

### 3.2 对比方法
**专用小模型基线**：T5-NLI-Mixed、DAE、QAFactEval、SummaC-ZS、SummaC-CV、AlignScore、FT5-ANLI-L（微调Flan-T5-large于完整ANLI）。

**LLM型事实核查器**：Gemini-Pro、PaLM2-Bison、Mistral-8x7B、Mistral-Large、Claude 2.1、Claude 3 Opus、GPT-3.5、GPT-4。


## 4. 资源与算力

- GPU：作者未给出详细的训练时长或GPU总数量的说明。
- 但在成本核算上提供了以下信息（换算方式见论文附录）：
  - 以**单张NVIDIA RTX A6000 GPU 0.8美元/小时**作为云价换算基准；
  - MiniCheck-FT5在13K条LLM-AggreFact测试集上的推理成本为**0.24美元**；
  - 对比GPT-4同样测试集推理约107美元，MiniCheck-FT5约**400倍更便宜**；
  - 参数量770M（Flan-T5-Large），与GPT-4的万亿级规模相比差异巨大。
- 训练数据规模极小：仅35K条（14K合成 + 21K ANLI难例），远低于AlignScore的4.7M条训练数据。


## 5. 实验数量与充分性

论文实验量大且覆盖全面，包括：
- **主实验**：在LLM-AggreFact的10个数据集上对比约7个专用小模型 + 8个LLM模型，并报告聚合性能和逐数据集成绩。
- **两档阈值设置对照**（零样本阈值 vs 每数据集阈值调优）。
- **消融实验**（Ablation）：
  - 分别移除C2D、D2C、两者全部移除；
  - 在两个保出集（held-out C2D / D2C）上对多种模型进行内部评估；
  - 在简化合成数据（C2D-SIMP、D2C-SIMP）上的性能对比。
- **流程分析**：
  - 声明分解（Decomposition）对正确率的影响；
  - 声明的去上下文化（Decontextualization）实验（对适用数据集的评估）；
  - “整段文档全部错误判定”模式的实验（GPT-4-Full）。
- **数据质量**：小规模人工评估（40×2样本抽样）报告了标注者一致性和标注准确率。
- **附加说明**：还给出了完整的每数据集细粒度结果（附表8—9等）。

**总体判断：** 实验覆盖了训练分布内外、单文档与多文档、各AI模型来源的声明以及多种骨干模型，整体设计较为客观；其中“无阈值调优”设定比以往论文更贴近真实部署。对照公平性方面，既对齐了传统的专用事实核查SOTA（AlignScore），也对齐了前沿通用LLM（GPT-4等），证据是较充分的。


## 6. 论文的主要结论与发现

1. 合成数据高度有效：
   - 在三个不同骨干模型（RoBERTa、DeBERTa、Flan-T5）上的表现显著提升。
   - MiniCheck-FT5在LLM-AggreFact上平均BAcc达到**74.7**，较AlignScore提升约**4.3%**，相比此前最好的专用模型有了质的跨越。
2. 小模型可达到GPT-4水平：
   - MiniCheck-FT5（770M参数）在整体精度上接近GPT-4，成本仅为约1/400。
   - 在同级模型中全面领先，并超过了GPT-3.5、Mistral-8x7B、Claude-2.1等更大规模的LLM。
3. 声明分解不必要：
   - 在LLM-AggreFact测试集中，将声明分解为原子事实后在整体上基本无提升（GPT-4 +0.3%，也有指标下降的情况），无需额外做这一步。
4. 去上下文化不一定提升：
   - 在已有训练设定中，去上下文化对模型效果几乎没有正增益，但仍认为其在真实检索/回答管线中对检索和链接的构建是有意义的。
5. 训练数据选择和构造比模型容量更重要：
   - 单纯增加模型大小（T5-XXL）但训练数据选用一般（如T5-NLI-Mixed）并不能解决事实核查的实际困难；数据质量/构造方式才是决定性因素。
6. 无阈值调优下鲁棒性更强：
   - 其他专用模型在无阈值调优时表现明显下降；MiniCheck-FT5几乎没有多少变化，显示其对不同数据集域分布更稳健。


## 7. 优点

1. **成本控制具有显著工程价值**：将基于文档的事实核查成本从“数美元/千条”级降到“亚美分级”，且不牺牲精度——对RAG评测、摘要过滤等高频场景非常友好。
2. **方法可复现、开源完备**：作者公开了合成数据生成代码、模型和数据集，整个库可供研究社区直接使用。
3. **全面的评测基准（LLM-AggreFact）** ：整合了此前分散在摘要评测、RAG评论、Wikipedia引用核查等子任务上的数据集，并做了类别统一，有助于从统一视角研究不同幻觉问题。
4. **合成数据构造富有创新性**：
   - 通过“将原子事实拆成两句信息对应”的方式，在源头上保证训练样本必须有跨句推理；自动剔除低质量数据，避免了直接人工标注大规模数据的高成本。
5. **结论具有反直觉性**，挑战了既有实践：通过充分对比证明“声明分解”并非必要环节，具有实践上的简化价值。
6. 实验设计细致：同时报告了阈值调优和无阈值调优两种设置；并有消融、内部评估以及误差讨论。


## 8. 不足与局限

1. **可解释性缺失**：模型只输出二分类分数，不易定位错误具体在文档中的哪个跨句关系上；若要做到局部归因，仍需事后分解。
2. **多文档推理未被真正覆盖**：
   - LLM-AggreFact中各数据集只要求对单个文档的跨句推理，不要求跨多个独立的证据文档进行推理；
   - 尚未验证对“证据分散在多篇文档中”的场景效果。
3. **合成数据的边界**：
   - 数据构造的哲学是“把事实拆分为句对后进行合并”，这种模式虽有效，但也可能带来特定的偏置，不一定涵盖所有真实错误的分布；
   - 内部自动质检有小规模人工验证（准确率约80%），但数据中存在标注噪声和主观判定差异（如NLI经典的主观性）。
4. **语言限制**：只训练与验证英文，未评估跨语言推广情况；尽管骨干模型（Flan-T5）支持多语言，但基准数据没有覆盖其他语种。
5. **未提及训练总时长**：论文未说明在GPU上训练各型号的具体时长，只能通过页数推断为小规模微调。
6. **基准本身的局限**：基准中未吸纳FActScore、HaluEval等数据集，原因是这些是合成错误类型或存在“检索-引用不一致”问题；但这也意味着结论尚无法直接平移至需真实检索步骤的复杂闭环系统。
7. **检索与核查分离的假设**：论文所聚焦的是“已知提及的文档和句子配对后的纯判定子任务”，未处理由检索带来的上下文不一致（如检索片段本身描述模糊或存在冲突叙述的困难情况）。


（完）
