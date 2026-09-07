---
title: "FactLens: Benchmarking Fine-Grained Fact Verification"
title_zh: FactLens：细粒度事实验证基准
authors: "Kushan Mitra, Dan Zhang, Sajjadur Rahman, Estevam Hruschka"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.929.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 构建细粒度事实验证基准FactLens，将复杂声明拆分为子声明并逐条验证，可精确检测无依据内容
tldr: 传统事实验证对复杂声明给出单一真伪标签，容易掩盖局部错误。论文主张细粒度验证：把复杂声明拆分成子声明，并为每个子声明检索证据以独立验证。基于这一思路构建了FactLens基准去系统评测大模型，结果显示细粒度验证能提高错误定位精度、增强透明性并减少证据检索歧义，为自动检验无依据内容提供新的基准支持。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl929/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 706, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl929/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 790, \"height\": 589, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl929/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 701, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl929/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 701, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl929/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 739, \"height\": 965, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl929/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 779, \"height\": 568, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl929/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1372, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl929/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1635, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl929/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl929/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 570, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl929/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 589, \"height\": 425, \"label\": \"Table\"}]"
motivation: 整体式声明级事实核查容易掩盖细粒度错误，证据检索也因此存在歧义。
method: 将复杂声明拆为子声明，逐一检索证据验证并构建FactLens基准进行系统评测。
result: FactLens显示细粒度验证可提高错误定位精度、透明性和证据利用效果。
conclusion: 细粒度子声明验证是构建可解释、高精度自动事实核查的重要研究范式。
---

## Abstract
Large Language Models (LLMs) have shown impressive capability in language generation and understanding, but their tendency to hallucinate and produce factually incorrect information remains a key limitation. To verify LLM-generated contents and claims from other sources, traditional verification approaches often rely on holistic models that assign a single factuality label to complex claims, potentially obscuring nuanced errors. In this paper, we advocate for a shift towards fine-grained verification, where complex claims are broken down into smaller sub-claims for individual verification, allowing for more precise identification of inaccuracies, improved transparency, and reduced ambiguity in evidence retrieval. However, generating sub-claims poses challenges, such as maintaining context and ensuring semantic equivalence with respect to the original claim. We introduce **FactLens**, a benchmark for evaluating fine-grained fact verification, with metrics and automated evaluators of sub-claim quality. The benchmark data is manually curated to ensure high-quality ground truth. Our results show alignment between automated FactLens evaluators and human judgments, and we discuss the impact of sub-claim characteristics on the overall verification performance.

---

## 论文详细总结（自动生成）

# FactLens：细粒度事实验证基准（中文总结）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）在文本生成和理解上表现优异，但仍有严重的“幻觉”问题，会生成与事实不符或缺乏证据支撑的内容。
- **现有问题**：传统事实验证通常采用“整体式（holistic）”模型，给一段复杂声明分配一个真/假标签。这种做法容易掩盖声明中的局部错误，无法明确指出是哪一部分信息不准确；同时，整体式检索证据也容易产生歧义。
- **核心主张**：论文倡导转向“细粒度验证（fine-grained verification）”——将复杂声明拆解为更小的子声明（sub-claims），分别检索证据、逐一验证。这种方式能精确定位错误、提高可解释性，并缩小证据检索范围。
- **整体意义**：论文提出 **FactLens** 基准，用于系统评估细粒度事实验证中的子声明质量，并提供自动化评估指标和工具，为构建更可靠、可解释的自动事实核查系统提供基础支撑。

## 2. 方法论

### 2.1 核心思想
- 将复杂声明分解为一组原子化但保持上下文完整的子声明，再对每个子声明独立进行事实验证。
- 子声明的质量直接决定后续验证的准确性；因此需要专门的指标来评估拆解质量。

### 2.2 子声明的质量评价指标
FactLens 定义了六个指标，每个指标按低/中/高（或原子性专用标签）评分：

- **Atomicity（原子性）**：每个子声明应只包含一个主-谓-宾事实单元，不能同时断言多个时间、地点或多个对象。
- **Sufficiency（充分性）**：子声明应自带必要上下文，可独立验证，不含歧义（例如不能出现“该校的昵称是……”但缺少“该校”指代）。
- **Fabrication（捏造性）**：拆解过程中不得添加原声明没有的新信息，也不能把条件当作事实。
- **Coverage（覆盖率）**：所有拆解出的子声明必须覆盖原始声明的全部事实断言。
- **Redundancy（冗余性）**：子声明之间不应存在语义重复，避免信息重复带来的偏差与额外验证成本。
- **Readability（可读性）**：子声明应自然、易读，满足最终用户阅读需求。

### 2.3 FactLens 自动评估器
- **评估方法**：采用“LLM 评分 + 统计计算”的集成方式。
  - **LLM 评估**：使用 GPT-4o-mini 按给定提示词对每个指标打分，温度为 0，保证一致性。
  - **统计计算**：
    - 用 GPT-4o-mini 提取子声明中的三元组（主体/对象）；
    - **原子性**：根据子声明中主语和宾语的数量判断原子性；
    - **覆盖率**：检查所有子声明的实体集合是否包含原始声明中全部主语和宾语；
    - **捏造性**：比较子声明中出现的实体是否在原声明中出现，按新实体数量打低/中/高；
    - **冗余性**：用 BERTScore 计算子声明两两之间的语义相似度，超过阈值视为冗余；
    - **充分性和可读性**因难以统计计算，主要依赖 LLM 评估。
- **集成选择**：根据人类相关性实验，原子性和覆盖率使用统计分数（相关性更好），其余指标使用 LLM 分数。

### 2.4 验证流程
- 使用 CoverBench 提供的真实证据（ground truth evidence），将每个子声明交给验证器（GPT-4o-mini）逐一判断真伪；
- 若任一子声明为假，则整体声明判为假；否则判为真。

## 3. 实验设计

### 3.1 数据集/基准
- **原始声明来源**：CoverBench（733 个实例），包含复杂声明和真实证据。
- **子声明基准构建**：先由 GPT-4o 和 Llama-3.1(405B) 生成候选子声明，再由人类专家修正/生成高质量 ground-truth 子声明。
- **合成数据（用于评估器验证）**：从 FEVEROUS 中取 10 个声明，人工构建 7 种不同质量的分解结果（完美的、LLM 生成的、以及分别针对原子性/充分性/捏造性/覆盖率/冗余性加入扰动的），用于检验 FactLens 评估器与人类判断的一致性。

### 3.2 对比方法/模型
- **子声明生成**：GPT-4o vs Llama-3.1(405B)，使用相同的 few-shot 提示词。
- **子声明质量评估**：人类标注 vs FactLens 评估器（LLM 评分、统计评分）。
- **验证方式**：细粒度验证（逐子声明验证后聚合） vs 整体式验证（直接验证原声明）。

### 3.3 关键结果与指标
- **合成数据上的人机相关性**：
  - LLM 评估与人类评分的 Pearson/Spearman 相关系数中等，其中冗余性约 0.56/0.52，覆盖率约 0.43/0.45，原子性 0.40/0.39；
  - 统计评分在原子性和覆盖率上更高（0.58/0.59 与 0.61/0.58）；
  - 充分性相关系数很低（LLM 约 0.14/0.09），说明该指标主观依赖上下文；
  - Krippendorff's Alpha 显示除充分性外均为中等一致。
- **CoverBench 上的分解质量**：
  - GPT-4o 与 Llama-3.1 表现接近，充分性（2.85）、覆盖率（约 2.89）、可读性（约 2.96）较好，捏造性低（约 1.01）；
  - 原子性得分较低（GPT-4o 1.82，Llama 1.87），是主要瓶颈。
- **端到端验证表现**：
  - 子声明质量越高（如低捏造、高原子性等），细粒度验证的 F1 越高；
  - 当声明复杂度（子声明数量）增加时，细粒度验证相比整体式验证的优势更大；
  - 用原子性、充分性、捏造性、覆盖率做逻辑回归预测最终验证标签，F1 约 0.71，其中捏造性权重绝对值最大（负向影响），其余三者有正向影响。

## 4. 资源与算力

- **论文未明确说明使用的 GPU 型号、数量或训练时长**。
- 文中仅列出模型调用配置：GPT-4o、GPT-4o-mini 和 Llama-3.1(405B)，温度为 0；例如 GPT-4o-mini 作为验证器和 LLM 评估器，GPT-4o 和 Llama-3.1 用于子声明生成。
- 由于主要依赖 API 调用而非本地训练，因此算力开销主要体现在推理评估上，但具体数值无从得知。

## 5. 实验数量与充分性

- **主要实验组**：
  1. 两个分解模型的六维质量评估（CoverBench）；
  2. 合成数据上“人类 vs LLM vs 统计评估器”的相关性/一致性分析；
  3. 端到端细粒度验证与整体式验证的对比（按复杂度分层）；
  4. 指标对验证结果的逻辑回归影响分析。
- **充分性评价**：
  - 实验设计能回应核心问题，即子声称质量如何影响最终验证，以及自动评估器是否可靠；
  - 但覆盖面较窄：仅使用 CoverBench 一个数据源、没有真实证据检索步骤、只用 GPT-4o-mini 一个验证器、未在多类基准上做更广泛的消融；
  - 总体上是“方法论展示”级别的实验，结论方向合理，但泛化性仍有待更多数据集和模型来验证。

## 6. 论文的主要结论与发现

- 细粒度事实核查比整体式核查更精确、透明，在复杂声明场景下优势尤其明显。
- FactLens 的六维指标能有效刻画子声明质量，且自动评估器与人类判断在多数维度达到中等级别一致（冗余、覆盖、原子性较好；充分性较弱）。
- 子声明质量与最终验证性能高度相关：低捏造、高原子性、高充分性和高覆盖率均能带来更好的下游验证效果。
- 当前最强的 LLM（GPT-4o 和 Llama-3.1 405B）在生成高质量的原子性子声明上仍欠佳，说明该任务仍有较大研究改进空间。

## 7. 优点

- **基准设计有针对性**：将“声明分解”作为细粒度核查的核心环节，并首次提出系统化质量维度（原子性/充分性/捏造性/覆盖率/冗余性/可读性）。
- **数据集质量高**：结合 LLM 生成与人工专家修正，提供 Ground-truth 子声明和细粒度标签。
- **评估工具实用**：FactLens 自动评估器将 LLM 评估与统计计算结合，兼顾可扩展性与可解释性，为研究社区提供现成工具和开源代码。
- **实验设计合理**：使用固定证据避免检索环节带来的不可控干扰；通过合成数据验证人与自动评估器的一致性，并分析子声明质量对最终结果的因果关系。

## 8. 不足与局限

- **评估指标的局限**：LLM 作为评判者存在偏倚和不稳定性；统计方法依赖自动实体提取的准确性，可能产生误差。充分性指标的人机一致性很低，表明该维度的定义与度量都不够稳定。
- **缺乏证据检索环节**：论文只使用 CoverBench 提供的现成证据，未验证子声明拆解能否实际提升“证据检索”的质量。
- **验证器单一**：实验全部使用 GPT-4o-mini 作为验证模型，未比较不同规模/类型的验证模型，结论可能受单一模型影响。
- **数据集覆盖面有限**：实验只基于 CoverBench，且原始声明类型/领域相对有限，对真实世界中不断

不断变化的声明类型和领域，覆盖度有限，限制了结论的通用性；真实世界中的噪声文本、隐含前提和不完全证据，都会对子声明的拆解与验证带来额外挑战，而基准尚未覆盖这些情形。
- **错误传播与可解释性不足**：论文虽然定性描述了“子声明质量影响最终结果”，但对“错误从哪个环节引入、在哪个环节被放大”缺少误差传播分析。例如，证据检索错误、拆解错误与验证器自身的判断错误之间如何交互，未被单独拆解分析。
- **缺乏对基线方法的系统总结**：论文声称细粒度验证优于整体式验证，但仅在单一数据源、单一验证器、单一一组提示词条件下进行比较，缺少对“不同生成模型、不同拆解提示词、不同验证聚合策略”的系统性对照，未能充分剥离各环节的贡献。
- **成本与效率未量化**：将声明拆分成子声明、逐个检索证据、逐个验证，相比整体式验证会显著增加 API 调用次数和推理延迟，论文在给出优势结论时，没有报告验证成本与复杂度增长的量化指标。

## 9. 未来工作方向

- **更广的数据域与真实证据检索**：可扩展至多领域声明，并引入标准证据检索环节，验证“子声明拆解—检索—验证”的完整流程是否在真实开放域设定下依然有效。
- **更强的分解决策机制**：面向不同任务场景自适应地决定拆解粒度——例如对简单声明不拆或粗拆，对高复杂度多跳声明细化拆解，避免过度拆解导致的成本膨胀。
- **迭代式动态验证**：初步验证后若发现某子声明证据不足或歧义，可触发对子声明本身的再修正与再生成，使子声明拆解由“一次性静态过程”转变为“闭环可优化过程”。
- **更稳健的自动化质量评估器**：针对充分性等维度，可能需要引入外部知识或交互式澄清机制，而非仅靠单模型直接打分；统计评估手段也需要结合更强的语义解析模型（如结构化三元组抽取的精度提升）。
- **多验证器与联合建模**：可引入不同规模的验证器交叉验证，或构建“拆解质量—证据质量—验证标签—解释生成”的联合模型，从证据到解释端到端可追溯。

## 10. 总结性评价（小节）

FactLens 的价值不在于提出了一个更复杂的端到端系统，而在于把“复杂声明如何被拆解、拆得如何、拆后如何影响可信度判定”这几个环节显式地定义出来，并给出了可操作的质量度量与自动评估工具。它为事实验证研究提供了一个清晰的分析框架：将“验证的粒度”与“验证的可靠性”绑定起来，推动事实核查从整体分类走向透明、可解释的细粒度判断。虽然基准在数据覆盖、检索缺失和评估器稳定性的问题上仍留有隐患，但整体上方向清晰、方法可行、资源可复用，是这个领域中一份较扎实、有实际参考价值的工作。

**局限性的建议应对**：读者若将 FactLens 用于自身研究，应避免直接照搬其验证器的绝对性能值作为系统质量的唯一衡量标准，而更应关注其相对性的质量诊断功能——例如，用它来对比不同拆解策略、验证器之间的子声明质量差异与下游误差变化，可能在工程诊断场景中发挥更大价值。

---

**参考文献风格提示**：原文的主数据源为 CoverBench，配套工具使用 GPT-4o-mini 与统计打分，合成评估数据基于 FEVEROUS 构建；以上来源信息有助于读者追查原始实验材料和数据处理细节。

（完）
