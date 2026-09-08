---
title: Consistent Discourse-level Temporal Relation Extraction Using Large Language Models
title_zh: 使用大语言模型进行一致的话语级时序关系抽取
authors: "Yi Fan, Michael Strube"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1010.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 篇章级跨句时序关系抽取及一致性建模
tldr: 大语言模型在如何抽取话语级时序关系上仍缺乏系统研究，零样本和少样本设置下甚至弱于小型微调模型。本文深入分析输入上下文、推理过程与一致性约束对模型能力的影响，并提出一个三步式LLM抽取框架，从时序关系结构和推理一致性两方面改善抽取效果。实验验证了该框架在篇章级文本上的有效性，为跨句时间信息和文档时间结构的抽取提供了可复用的技术路线。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 493, \"height\": 222, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 479, \"height\": 207, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1514, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 663, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 771, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 763, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 787, \"height\": 642, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 788, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 784, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp1010/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 790, \"height\": 425, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1062, \"height\": 615, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 818, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 817, \"height\": 469, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 590, \"height\": 511, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 811, \"height\": 509, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 890, \"height\": 448, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1661, \"height\": 970, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 633, \"height\": 511, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp1010/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 779, \"height\": 315, \"label\": \"Table\"}]"
motivation: 现有大语言模型在零样本和少样本下对篇章级时序关系抽取表现不佳，一致性因素未被充分研究。
method: 剖析上下文、推理过程与一致性三类影响因素，并据此设计三步式LLM抽取框架。
result: 所提框架提升了大模型在话语级时序关系抽取中的表现，说明一致性引导是关键。
conclusion: 为篇章级时间结构抽取提供了一种强调推理一致性的LLM使用策略。
---

## Abstract
Understanding temporal relations between events in a text is essential for determining its temporal structure. Recent advancements in large language models (LLMs) have spurred research on temporal relation extraction. However, LLMs perform poorly in zero-shot and few-shot settings, often underperforming smaller fine-tuned models. Despite these limitations, little attention has been given to improving LLMs in temporal structure extraction tasks. This study systematically examines LLMs’ ability to extract and infer discourse-level temporal relations, identifying factors influencing their reasoning and extraction capabilities, including input context, reasoning process and ensuring consistency. We propose a three-step framework to improve LLMs’ temporal relation extraction capabilities: context selection, prompts inspired by Allen’s interval algebra (Allen, 1983), and reflection-based consistency learning (Shinn et al., 2024). Our results show the effectiveness of our method in guiding LLMs towards structured processing of temporal structure in discourse.

---

## 论文详细总结（自动生成）

## 论文总结

### 一、核心问题与整体含义（研究动机与背景）

- **任务定义**：时序关系抽取（Temporal Relation Extraction）旨在判断文本中事件之间的时间先后或包含关系，是构建文本时间结构、支持文档摘要、叙事线构建、阅读理解等下游任务的基础能力。
- **核心矛盾**：篇章级（discourse-level）时序关系抽取要求模型在跨句甚至跨段落的长距离事件之间推理时间关系，这对 LLM 是一个突出难点。已有研究表明：
  - LLM 在零样本/少样本设置下在该任务上表现不佳，往往不如小规模微调模型；
  - 即便进行微调，LLM 与基于 BERT/RoBERTa 的专门模型仍有性能差距；
  - 现有研究多聚焦 F1 分数，鲜少关注预测结果的时间一致性（consistency），即同一文档内预测出的多个三元事件关系是否满足传递性等逻辑约束。
- **关键挑战**：论文提炼出篇章级时序关系抽取中三个未被充分研究的问题：
  1. **上下文选择**：全文档输入或滑窗策略均会引入大量噪声，且 LLM 存在“Lost in the Middle”现象（文档中间位置的信息被忽视）；
  2. **性能**：LLM 即使微调，仍与基于小规模预训练模型的方法存在明显差距；
  3. **一致性**：多数方法不检查输出是否构成逻辑自洽的时间图，违反传递规则的情况普遍存在。
- **论文含义**：作者主张通过系统分析影响 LLM 时序推理的因素（输入上下文、推理过程、一致性约束），提出一套显式引导 LLM 进行结构化时间推理的框架，使 LLM 在该任务上既能达到较高 F1，又具备全局一致性。

### 二、方法论：核心思想、关键技术细节与流程

论文提出一个**三步式框架**，其整体结构如图 2 所示，具体如下：

**步骤 1：上下文选择（Context Selection）**
- 核心思想：避免全文档输入造成的噪声和注意力分散，仅为每个目标事件对选取最相关的最小上下文。
- 方法 A（实体话语分段，Entity-Based Discourse Segmentation）：
  - 利用 neuralcoref 对文档进行共指消解；
  - 提取每个句子的主语、直接/间接宾语以及所有名词/名词短语，形成实体列表 SE_i；
  - 对相邻句子的实体列表两两计算余弦相似度，取最大值 Sim_ij，若 Sim_ij ≥ 阈值 γ（通过网格搜索选取最优值），则将两句归入同一话语段，否则开启新段；γ 最优取 0.7；
  - 若目标事件 e1、e2 分别位于 ds_i、ds_j 话语段，则拼接两个段作为输入（段内则直接取该段），将输入长度限制在约 20 句以内。
- 方法 B（LLM 引导的上下文选择，作为对比/消融）：给文档每句话编号并交由 LLM 自行选择与事件对相关的句子——实验表明其效果不如实体分段方法。
- 附加策略（目标事件高亮）：在输入文本中用 `<e1>...</e1>`、`<e2>...</e2>` 标记目标事件，避免同名或无关事件干扰模型判断。

**步骤 2：指令与提示设计（Instruction and Prompt Engineering based on Allen's Interval Algebra）**
- 受 Allen 区间代数启发，将事件建模为具有起点和终点的时间区间，引导模型先比较两个事件的 start 时间与 end 时间，再推断二者时序关系，而非直接判断标签。
- 例如对于 `before` 关系，期望模型的推理输出为：“Event 1 starts before Event 2 starts, and Event 1 ends before Event 2 starts, so the temporal relation ... is before”。
- 该 CoT 结构将推理分解为“起点比较 → 终点比较 → 关系判断”三个子步骤，促使模型显式锚定事件在时间轴上的位置。文中图 5 给出了八种标签在时间轴上起点/终点的完整定义（Table 6 展示标签与期望输出的对应表），指令示例见附录（Figure 9）。

**步骤 3：基于反思的一致性学习（Reflection-based Consistency Learning）**
- 动机：ILP 等方法依赖模型对各标签输出的概率才能施加全局约束，而 LLM 以文本生成方式进行预测，无法直接套用 ILP。为此借鉴 Reflexion（Shinn et al., 2024）与 Chen et al.（2024）的思路，提出**两阶段微调**：
  - 第一阶段：以标准指令对模型进行时序关系分类微调；
  - 在训练集预测结果中检测违反传递性的不一致事件三元组（如 e1→e2 为 before、e2→e3 为 before、但模型判定 e1→e3 为 after）；
  - 第二阶段：将这些不一致三元组作为新一轮训练数据（输入不含真实标签，只指出不一致并解释——该步骤也称为自反思第一遍），对模型再进行一轮微调，从而教会模型识别并修正逻辑矛盾；
  - 推理时，先让模型对所有事件对生成初始预测，再检测不一致三元组，仅对不一致部分用上述“重评估输入”二次查询模型（最多查询两次，不迭代）。
- 每一个阶段均使用该研究的学习率、LoRA 超参等进行 LLaMA 微调（LoRA alpha ∈ [8,16]，rank ∈ [16,32] 或更大；学习率 3e-5/5e-5；最多训练 3 epochs，第二阶段仅训练 1 epoch）。

### 三、实验设计与基准

- **数据集**（均以新闻语篇为主）：
  1. **TDD-Man**：专家标注的篇章级全部时间结构语料；
  2. **MAVEN-ERE**：大规模事件语料（含时间、因果、子事件、共指）；时间关系分类仅考虑 temporal；训练/测试分割遵循 Hu et al.（2025），由于测试集未公开，将原始训练集按 80/20 切分 5 次并取平均结果，用原始验证集作为测试集；
  3. **TimeBank**：经典时序标注语料；因无官方切分，采用 TimeBank-Dense 的划分策略，并对标签体系做简化。

- **对比基线**：
  - BERT、BERT+ILP、UCGraph、SCS-EERE、CPTRE（Yuan et al., 2024，论文自行复现）等小规模预训练模型方法；
  - 基于 ChatGPT / LLM 的零样本、少样本方法（Yuan et al., 2023；Chan et al., 2024；Zhang et al., 2024）；
  - 自建的 Llama-3.1-8B-Instruct、Llama-3.3-70B-Instruct 零样本和直接微调基线（用简单指令、全文档输入）。
- **评估指标**：micro F1-Score，以及一致性率（Consistency Rate）——通过检查任意三事件元组的预测是否满足传递规则得到（按 Naik et al., 2019 的方法）；显著性检验用 Wilcoxon signed-rank test（p=0.05）；全部结果取 5 轮运行平均。

### 四、资源与算力说明

- 论文在**附录 G** 仅说明：“本研究所用的 GPU 是 NVIDIA H200”，**未给出 GPU 数量、每卡显存、训练总时长、卡时开销或碳排放等详细算力信息**。
- 可以推断训练大体规模较大：在两个 LLaMA 模型（8B 与 70B）上进行多轮 LoRA 微调，涉及 3 个数据集、5 次重复实验以及消融试验，但具体算力消耗无法从文中量化。

### 五、实验数量与充分性

- 实验轮次/变体比较充分，广度和深度兼顾：
  1. **主实验**：在 TDD-Man、MAVEN-ERE、TimeBank 三个语料上分别对比了多个 BERT/RoBERTa 基线、不同规模的 LLM 零样本/微调基线与完整方法；
  2. **消融实验**（TDD-Man 上以 Llama-3.1-8B 为例，表 4）：共 8 行配置，分别检验：
     - 实体上下文选择 vs. LLM 自选上下文 vs. BERTopic 选上下文；
     - 去掉 CoT 提示的影响；
     - 去掉自反思（仅普通微调）的影响；
     - 去掉微调后自反思、仅对不一致预测重新提示（PA）的影响。
  3. **额外分析**：
     - 混淆矩阵分析标签类别混淆情况（图 4）；
     - 句子距离与精度的关系（表 5、表 7）；
     - 附带 MAVEN-ERE 多数类基线（84.8 F1）以反映数据标签极不平衡的问题。
- **客观性与公平性判断**：
  - 与 BERT 类基线进行比较时存在天然的模型代差，但在同一 LLM 基础上对比零样本/直接微调/完整框架，能较公平地论证各组件增益；
  - 每个结果平均 5 次运行，并使用统计显著性检验与 Wilcoxon 配对检验，具有一定稳健性；
  - 复现 CPTRE 以评估可比性，显示作者的做法较为严谨；
  - MAVEN-ERE 上的多数类基线达到 84.8 F1，充分披露了该数据集上指标容易被标签不平衡“推高”的事实，这对公平解读结果有积极意义。

### 六、主要结论与发现

- **三步框架有效指引 LLM 进行篇章级时序关系抽取**：
  - 基于 Llama-3.3-70B-Instruct 的完整模型在 TDD-Man 上达到 57.9 F1、一致性 93.6%，均优于现有最优（CPTRE 56.5 F1 / 65.9 一致性），且统计显著；基于 8B 的版本也具备竞争力（55.3 F1 / 91.3 一致性）。
  - MAVEN-ERE 上，本文方法（91.9 F1）胜过同模型的零样本与直接微调基线（76.3 / 89.2 F1 等）。
  - TimeBank 上，本文方法取得 66.0 F1（70B 版）并与 87.8 的一致性，明显优于 CPTRE 复现结果（61.1 F1 / 51.7 一致性）以及 Llama-3.3-70B 直接微调（62.2 F1 / 46.6 一致性）。
- **一致性大幅提升**：自反思学习将一致性从约 82.6–84.5% 提升到 91.3–93.6%，远超此前 ILP 方案仅提升 2 个百分点左右的水平。
- **上下文选择至关重要**：相较全文档、模型自选上下文或 BERTopic，实体话语分段方法能有效减小噪音输入、保持语篇连贯且截取更贴近事件的上下文。
- **更深层的判断**：即使使用 70B 量级模型，LLM 在捕捉文本时间结构上仍相对薄弱，单纯扩大参数规模并不能带来大幅性能提升；需要进一步的策略性引导。

### 七、论文优点

1. **首次将自反思（self-reflection）用于篇章级时序关系抽取的一致性优化**，为 LLM 方案中无法直接套用 ILP 提供了可替代的微调式一致性学习路径。
2. **框架组件可解释、模块化**：三步法分别指向输入质量、推理结构与输出一致性三个关键因素，并逐一开展消融验证。
3. **在提升 F1 的同时显著提高了逻辑一致性**，较此前仅关注局部精度、一致性微弱改善的工作有质的进步。
4. **多角度分析丰富**：混淆矩阵揭示标签混淆真实来源（如 “includes” vs. “before”），句子距离归因分析说明短距离关系在全文输入下并不一定比长距离更容易，纠正了一种“短距更简单”的直觉假设。
5. 提供开箱可用的指令设计（Allen 区间代数式的 CoT 模型、事件高亮、一致性反思指令），可迁移性强；对 MAVEN-ERE 标签极不平衡情况亦提供了多数类基线与多次 80/20 切分的稳健报告，体现出实验设计的透明度。
6. 该方法可扩展为基于 LLM 的语料标注辅助工具，节约人工标注成本。

### 八、不足与局限

1. **数据代表性与泛化风险**：TDD-Man、MAVEN-ERE、TimeBank 均为新闻文本，标签分布受新闻文体影响；作者也承认难以推广到叙述性、程序性等其他文体的时序关系需求。
2. **资源消耗偏高**：需要对 70B 模型做两轮 LoRA 微调，并在推理时对不一致三元组做二次查询；论文未报告具体 GPU 数量、训练时长与总能耗，算力透明度有限。
3. **性能提升有“天花板”**：虽然一致性明显领先于基线

（接上文）

3. **性能提升有“天花板”**：虽然一致性明显领先于基线，但在 F1 分数上提升幅度有限（TDD-Man 上相较最优基线 CPTRE 仅提高约 1.4 个百分点），说明当前框架更多是在“修正已有预测的逻辑错误”上下工夫，并没有从本质上突破模型对文本时间语义理解的上限。
4. **高资源需求削弱了实际部署的可行性**：框架需先对完整训练集做一遍推理以挖掘不一致三元组，再以人工设计的不一致样本进行二次微调；对于需要持续更新标注的语料场景，pipeline 成本较高。
5. **一致性检查依赖传递规则为主**：时间关系语义远比形式逻辑约束丰富，如 overlap、simultaneous 与 during 之间存在更微妙的时间区间包含关系，文中仅依靠传递性构建一致性校验，未必能完全覆盖所有语义矛盾类型。
6. **长距离跨段关系可能被上下文选择阶段牺牲**：实体话语分段将输入限制到 ~20 句，虽然减少了噪音，但对于需要极长距离全局信息才能判断的关系（例如文档级全局时间锚点），截断策略可能会导致有效证据丢失，文中未对这类情况的失败案例做系统分析。
7. **未讨论事件抽取误差的级联影响**：实验假设事件提及及事件对已正确抽取，而在真实管道中事件识别与共指消解自身的错误会向下游传递，影响框架的有效性评估。

### 九、对后续研究的启示与建议

1. **探索更轻量的一致性学习**：能否将两阶段自反思精简为单阶段，或从少量不一致示例出发，利用上下文学习（in-context learning）在推理时修正，从而避免对每个数据集都做二次微调？
2. **引入更强的逻辑约束形式**：可尝试将输出空间约束（constrained decoding）或形式化验证器（verifier）与 LLM 生成结合，从解码层面上保证输出满足传递闭包，替代二次查询的软约束方式。
3. **将框架迁移至叙事文本与跨文体场景**：论文所提出的实体分段、Allen 区间代数式推理与一致性反思均属于领域无关设计，未来可在小说、剧本、百科类语料中验证其通用性。
4. **关注标注语义的细粒度差异**：不同语料对时序标签的定义并不完全一致（如 TimeBank 与 TDD-Man 的 during/overlap 界定），后续工作可设计更统一的标签映射方案，使框架在跨数据集迁移时更具鲁棒性。

### 十、总体评价

- **定位**：该文属于“LLM 用于结构化 NLP 任务”方向上具有代表性的方法论文。其贡献不在于提出全新的网络架构，而在于将三个直观的模型设计原则（上下文降噪、推理分解、一致性反思）进行系统整合，并以实验证据逐项验证各环节的贡献，令人信服。
- **方法论的价值**：文中对“LLM 与小规模微调模型在时序推理任务上的差距”的归因分析具有较强的启发性——LLM 并非缺乏时序知识，而是需要更合适的上下文组织方式和推理路径引导。这一思路不仅适用于时序关系抽取，也可外推至其他涉及篇章级结构化推理的任务。
- **方法论的风险**：由于所有实验都集中在新闻语料并依赖较大的 GPU 算力，当前优异成绩的普适性与复现成本仍是潜在风险；同时，未披露能耗细节让读者难以评估方法的可持续发展性。
- **结论公允性**：对 MAVEN-ERE 标签不平衡、数据切分策略等进行了充分披露，整体上没有过度宣称方法的优越性，结论尺度把握较为恰当。

---

综上，本文系统性地揭示并缓解了 LLM 在篇章级时序关系抽取中的三个主要瓶颈——上下文冗余、推理碎片化与输出不一致，提出了一个可复现、可消融验证的三步框架，并在三个公开语料上取得一致的性能提升。论文在实验设计、多角度分析与透明度方面均表现出较高水准；但受限于数据范围、算力披露及一致性约束的建模视野，框架的实际泛化能力和工程可采纳性仍有进一步探索的空间。

（完）
