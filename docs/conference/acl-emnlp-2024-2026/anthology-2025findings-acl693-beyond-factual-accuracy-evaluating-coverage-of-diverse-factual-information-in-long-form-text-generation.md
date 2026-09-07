---
title: "Beyond Factual Accuracy: Evaluating Coverage of Diverse Factual Information in Long-form Text Generation"
title_zh: 超越事实准确性：评估长文生成中多样事实信息的覆盖度
authors: "Chris Samarinas, Alexander Krubner, Alireza Salemi, Youngwoo Kim, Hamed Zamani"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.693.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: ICAT将长文拆为原子主张并经检索验证，衡量多样事实覆盖度，属事实一致性评测方法
tldr: 传统事实评估多聚焦单句或整体准确性，忽略长文输出中的事实覆盖度。论文提出ICAT评测框架：把长文本切成原子事实主张，经可靠知识源检索逐条验证，并计算这些主张与外部期望方面的对齐程度，从而同时度量事实准确性与多样性覆盖。研究在TREC Web Track和ClueWeb数据上验证，显示其与人类判断有强相关性。该框架能更全面地表征长文生成的事实质量。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl693/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1367, \"height\": 748, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl693/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 816, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl693/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 747, \"height\": 560, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl693/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1492, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl693/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1228, \"height\": 604, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl693/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1225, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl693/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1219, \"height\": 274, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1437, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1153, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1132, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1226, \"height\": 510, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 440, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 464, \"height\": 152, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 375, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 345, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl693/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1229, \"height\": 470, \"label\": \"Table\"}]"
motivation: 长文生成评测不能只看事实准确性，还应衡量多样化事实信息是否被覆盖。
method: 将长文输出拆成原子主张，通过检索验证每条主张，并计算其与预期方面的对齐情况。
result: 在TREC与ClueWeb评测中与人类判断强相关，支持不同方面可得性与对齐假设。
conclusion: 原子事实验证加方面对齐可同时衡量事实准确性和覆盖度，适于长文评估。
---

## Abstract
This paper presents ICAT, an evaluation framework for measuring coverage of diverse factual information in long-form text generation. ICAT breaks down a long output text into a list of atomic claims and not only verifies each claim through retrieval from a (reliable) knowledge source, but also computes the alignment between the atomic factual claims and various aspects expected to be presented in the output. We study three implementations of the ICAT framework, each with a different assumption on the availability of aspects and alignment method. By adopting data from the diversification task in the TREC Web Track and the ClueWeb corpus, we evaluate the ICAT framework. We demonstrate strong correlation with human judgments and provide comprehensive evaluation across multiple state-of-the-art LLMs. Our framework further offers interpretable and fine-grained analysis of diversity and coverage. Its modular design allows for easy adaptation to different domains and datasets, making it a valuable tool for evaluating the qualitative aspects of long-form responses produced by LLMs.

---

## 论文详细总结（自动生成）

# 《超越事实准确性：评估长文生成中多样事实信息的覆盖度》论文总结

## 1. 核心问题与研究动机

- **背景问题**：大语言模型（LLM）在长文生成任务中发展迅速，但现有评测体系存在关键缺口——大多数评测只关注事实准确性（factual accuracy），而忽略了回答是否**全面覆盖了多样化的相关事实信息**。
- **核心差距**：一个回答可能在所有陈述上都事实准确，但如果遗漏了某些重要方面（如只讨论咖啡益处、忽略健康风险），会给出不完整甚至误导性的信息。这在医疗、政策分析、教育等需要平衡信息的场景尤为关键。
- **现有方法不足**：
  - 传统词面重叠指标（BLEU、ROUGE、METEOR）只能衡量表层文本相似度，无法评估语义等价但表述不同的内容；
  - BERTScore、G-Eval 等语义相似方法依然无法验证事实准确性，也不能判断主题覆盖是否全面；
  - FActScore、VERISCORE 等方法虽然能评估原子主张的事实性，但"事实准确 ≠ 覆盖充分"，两者需要统一评测框架。
- **论文目标**：提出一个能**同时衡量事实准确性与多样化信息覆盖度**的模块化评测框架——ICAT。

## 2. 方法论：ICAT 评测框架

### 2.1 核心思想

ICAT 将长文本输出（LLM 的回答）拆解为**原子事实主张（atomic claims）**，对每一条主张逐一通过知识源检索进行事实核实；再将**已验证的事实主张**与一组期望出现的**多样化方面（aspects/subtopics）** 进行对齐，以此同时计算出事实性分数与覆盖度分数，并最终融合为一个综合分数。

### 2.2 核心组成与符号定义

**（1）事实性分数（Factuality Score）**

- 将输出文本 y 经原子主张生成函数 $AC(y)$ 拆分为一组原子主张 C；
- 通过检索验证函数 $CG(C; K)$（K 为知识源）筛选出可被支持的主张子集 $C_T$；
- 事实性分数定义为：**$S_{fact} = |C_T| / |C|$**，即所有主张中被验证为真实的比例。

**（2）覆盖度分数（Coverage Score）**

- $T_Q(x)$：输入查询 x 的所有相关方面集合；
- $T_O(c, K)$：识别某条已验证主张 c 关联的子主题；
- 覆盖度分数定义为：**$S_{coverage} = |\{T_O(c,K): c ∈ C_T\} ∩ T_Q(x)| / |T_Q(x)|$**；
- 关键设计：**只有通过事实验证的主张才能计入覆盖度**，避免错误信息"污染"覆盖评分。

**（3）ICAT-β综合分数**

- 借鉴 F-measure 思想，计算加权调和平均值：**$ICAT_\beta = (1+\beta^2)·S_{fact}·S_{coverage} / (\beta^2·S_{fact} + S_{coverage})$**；
- β 控制事实性与覆盖度之间的权重；默认 β=1（两者等权）；β<1 偏向事实性，β>1 偏向覆盖度。

### 2.3 三种实现变体（按自动化程度区分）

| 变体 | 方面获取方式 | 主张-方面对齐方式 |
|------|------------|-----------------|
| **ICAT-M** | 人工标注的真实方面（ground-truth aspects） | 基于检索 + 文档级人工相关性标注（文档标注了其覆盖的方面） |
| **ICAT-S** | 人工标注的真实方面 | 基于检索 + LLM 伪标注（LLM 分析每条主张覆盖哪些方面） |
| **ICAT-A** | LLM 自动生成方面 | 基于检索 + LLM 伪标注（全自动，无需任何人工标注） |

### 2.4 关键模块实现

1. **原子主张生成（AC）**：利用特定提示词（见图 6）引导 LLM 将文本拆分为自包含、去语境化（decontextualized）的单事实句子；论文对比了 8B 微调模型与 70B 零样本模型的差异（详见第五节实验部分）。
2. **主张检索验证（CG）**：两阶段方法——先使用稠密检索（Snowflake-Arctic-Embed + FAISS 索引）或 Brave Search API（网络搜索）检索 top-k 文档片段；再用 DeBERTa-v3 微调的 NLI 模型判断主张能否被检索到的片段支持。
3. **主题生成（$T_Q$）**：直接零样本提示 LLM 生成最多 10 个主题，8B 模型即可胜任。
4. **主张-方面对齐（$T_O$）**：将查询、方面集合和已验证主张列表呈现给 LLM，按结构化 jsonl 格式输出"哪些主张支持哪些主题"。

## 3. 实验设计

### 3.1 数据集与基准（Benchmark）

- **检索语料**：ClueWeb09 Category B（超过 5000 万英文网页文档），使用 Waterloo spam scorer 过滤垃圾文档（阈值 70%）；
- **查询数据**：TREC Web Track 2009–2012 的 200 个主题（包含人工标注的子主题——即"多样方面"）；过滤掉 21 个不适合长文生成评测的查询后剩 **179 个有效查询**；从中随机采样 **50 个查询**用于人工评估与 LLM 比较。

### 3.2 评估方式

- **人工评估**：Amazon Mechanical Turk（AMT），每个查询-回答对由 3 名独立标注者评估覆盖度，需标注文本证据；Fleiss's κ = 0.829（高度一致）。
- **比较方法**：
  - **传统指标**：BLEU、ROUGE-1/2/L/Lsum、METEOR、BERTScore（precision/recall/F1）；
  - **4 个被评测 LLM**：GPT-4、Llama-3-70B-Instruct、Mixtral-8x22B-Instruct-v0.1、Openchat 3.5（7B）。
- **相关性指标**：Pearson's ρ、Spearman's ρ、Kendall's τ，衡量 ICAT 各变体与传统指标与人类判断的相关程度。

### 3.3 消融与组件评估

- 对比了 8B 与 70B 覆盖模型、不同稠密检索模型（BM25 vs Arctic-Embed-M vs Arctic-Embed-L）、语料检索 vs 网络检索（Brave Search API）、三种 ICAT 变体对比等。

## 4. 资源与算力

论文仅在实现细节部分明确提到：使用 **QLoRA 微调 Llama-3.1-8B**，批次大小 16、学习率 2e-4、LoRA α=16、rank=64、训练 1 个 epoch，训练数据为 1000 个合成示例；推理使用 vLLM 库加速，8B 模型相比 70B 节省约 **8.75 倍内存**。文中**未明确说明**具体使用的 GPU 型号、数量、训练时长或总计算成本等信息，也未报告完整的碳排放或能耗数据。

## 5. 实验数量与充分性评估

**实验类型概览：**
- 三种 ICAT 变体 × 两种检索源 × 四种 LLM 的覆盖度评测；
- 与 9 类传统指标的整体相关性对比；
- 人工评估（50 查询×3 标注者）；
- 三组组件级评测（原子主张质量、主题生成质量、覆盖预测精度）；
- 检索模型消融（BM25 vs Snowflake-Arctic-Embed-M/L）；
- 语料检索 vs Web 检索对比。

**充分性与客观性分析**：
- ✅ 实验设计较为周全：人工评估采用多数投票（κ=0.829，高度一致）；与人类相关性比较覆盖多种变体和模型规模；组件独立评测使得每个模块的贡献可追溯；表 10 的检索模型系统消融说明框架鲁棒性；
- ❌ 局限：50 个查询的样本量偏小；人工评估仅涉及英文；在比较不同 LLM 时，仅使用默认设置生成输出（未针对"多样性"做提示优化），可能低估了某些模型的能力——但论文承认这一点，可视为公平性上的稳妥选择；
- ❌ 需注意的偏差风险：ICAT-A 与 ICAT-S 中使用 Llama 模型进行主题生成和对齐，与被评测模型（如 Llama-3-70B）存在同源偏差的可能性，论文在 Limitations 中主动指出此问题，值得肯定。

## 6. 主要结论与发现

1. **ICAT 与人类判断强相关**：ICAT-S（Llama-3.1-70B 作对齐模型）获得最强相关性（Pearson's ρ = 0.422，Spearman's ρ = 0.446，p<0.01），显著优于传统指标。
2. **传统指标无法有效衡量主题覆盖**：BLEU、ROUGE 等 n-gram 指标与人类覆盖度判断几乎零相关甚至负相关；仅 BERTScore-recall 达到统计显著性（ρ=0.291），但仍远低于 ICAT-S。
3. **ICAT-A 的潜力**：虽然 ICAT-A 与人类判断的相关性弱于 ICAT-S，但论文观察到自动生成的主题质量更高、更全面，如果使用更完整的人类标注主题集，ICAT-A 表现应更好。
4. **网络检索显著提升事实性分数**：Web 搜索相比语料检索使事实性分数从约 0.34 提升至约 0.75，但覆盖度提升相对温和——覆盖度更依赖 LLM 自身能力。
5. **模型差异**：各 LLM 在事实性上差异不大，但在覆盖度上存在明显差距，Llama-3-70B 表现突出；β 超参数可灵活调整事实性 vs 覆盖度的侧重需求。
6. **大覆盖模型更准**：Llama-3.1-70B 作为覆盖对齐模型显著优于 8B 版本（见表 2、表 10）。

## 7. 优点与亮点

- **统一双维度评测**：首次在同一框架内同时考虑事实准确性和方面覆盖度，弥补了现有单一维度评测的缺口；
- **高度模块化设计**：各组件（主张生成、主张验证、主题生成、主张-方面对齐）可独立替换和定制，便于适配不同领域；
- **三种自动化层次（M/S/A）** ：从完全人工到全自动渐进过渡，赋予用户在不同标注资源条件下选择合适实现方式的灵活性；
- **细粒度可解释性**：评测不仅能给出分数，还能追溯"哪个具体主张、支持哪条证据、覆盖哪个主题"，便于诊断生成失败的具体原因；
- **可直接用于优化**：ICAT-β可作为强化学习的奖励函数，同时优化事实性和覆盖度（论文在引言中主动提及此应用场景）；
- **检索模型消融**：表 10 系统展示了 BM25 → 小型稠密 → 大型稠密检索模型的性能提升路径，说明了检索质量对评测可靠性的影响；
- **工程效率考虑**：使用 NLI 小模型进行主张验证、QLoRA 微调 8B 模型代替 70B 零样本推理等设计体现了对可扩展性和部署可行性的实际考量。

## 8. 不足与局限性

- **方面-主张对齐仍有精度瓶颈**：论文在 Limitations 承认 70B 模型在做主张-主题对齐时仍会出现错误，还有提升空间；需要对此任务专门微调或优化提示策略；
- **主题生成的系统性验证不足**：当前主题生成使用零样本提示，但未对生成主题的完整性、冗余度、质量进行系统评估或与专家标注主题对比；
- **同源模型偏差风险**：若用于生成主题/对齐的 LLM 与被评测的 LLM 架构相近，可能产生循环依赖导致评估偏差（论文明确承认此风险，但未实测量化）；
- **语言与领域受限**：目前仅支持英文网络文本语料评测，不适用于多语言内容或需要领域专用知识库的场景（如医学、法律）；
- **数据集时效性**：ClueWeb09 是 2009 年的数据，对于当前的实时信息和热门话题评测可能不够充分；
- **实验规模有限**：人工评估仅覆盖 50 条查询，跨模型对比也因此受限；此外被评估模型数量有限（尤其缺少较新的 GPT-4o、Claude、Gemini 等），结论的时效性和泛化性值得留意；
- **"方面"定义对评测质量的影响很敏感**：如果真实主题集不完整（如 TREC 原有主题不够全），会导致对覆盖度的系统性低估——这本身也提示了自动生成主题方案（ICAT-A）的潜在价值，但也说明了该领域在"标准答案完整度"上的挑战。

（完）
