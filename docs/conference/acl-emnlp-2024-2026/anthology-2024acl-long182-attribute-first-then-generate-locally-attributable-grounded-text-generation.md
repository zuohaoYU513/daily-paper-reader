---
title: "Attribute First, then Generate: Locally-attributable Grounded Text Generation"
title_zh: 先归因后生成：局部可归因的基于证据文本生成
authors: "Aviv Slobodkin, Eran Hirsch, Arie Cattan, Tal Schuster, Ido Dagan"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.182.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 先生成源证据归因再逐句生成的本地归因方法，提升文本对证据的忠实度
tldr: 该文针对现有归因生成中引用粒度过粗的问题，提出先归因后生成的生成方式。模型先选择相关源片段，再做句子规划，最后逐句生成并附带局部归因。实验证明方法在保持文本质量的同时提高了可归因性和忠实度，减少用户核查负担。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1561, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1325, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 646, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1611, \"height\": 1709, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1566, \"height\": 2394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1579, \"height\": 2058, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1606, \"height\": 1789, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1614, \"height\": 1313, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1607, \"height\": 1315, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1547, \"height\": 1880, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1577, \"height\": 1697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1589, \"height\": 623, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long182/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1564, \"height\": 794, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1390, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1392, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 159, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 135, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 794, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 796, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1618, \"height\": 1852, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1626, \"height\": 767, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1626, \"height\": 1053, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 806, \"height\": 118, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1657, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long182/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1339, \"height\": 244, \"label\": \"Table\"}]"
motivation: 现有归因模型常引用整篇文档或段落，导致验证成本高、证据与生成关联弱。
method: 将生成分解为内容选择、句子规划和顺序生成三步，实现细颗粒度的源片段归因。
result: 在降低用户核查负担的同时提升了生成内容的事实忠实度与可归因性。
conclusion: 为证据约束下的可靠文本生成提供了一种端到端可归因范式。
---

## Abstract
Recent efforts to address hallucinations in Large Language Models (LLMs) have focused on attributed text generation, which supplements generated texts with citations of supporting sources for post-generation fact-checking and corrections. Yet, these citations often point to entire documents or paragraphs, burdening users with extensive verification work. In this paper, we introduce a locally-attributable text generation approach, prioritizing concise attributions. Our method, named “Attribute First, then Generate“, breaks down the conventional end-to-end generation process into three intuitive steps: content selection, sentence planning, and sequential sentence generation. By initially identifying relevant source segments (“select first“) and then conditioning the generation process on them (“then generate“), we ensure these segments also act as the output’s fine-grained attributions (“select“ becomes “attribute“). Tested on Multi-document Summarization and Long-form Question-answering, our method not only yields more concise citations than the baselines but also maintains - and in some cases enhances - both generation quality and attribution accuracy. Furthermore, it significantly reduces the time required for fact verification by human assessors.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **研究背景**：在文本生成用于多文档摘要（MDS）和长文本问答（LFQA）的今天，大语言模型（LLM）在开放性生成任务中会出现“幻觉”（hallucinations），即输出与输入证据不符。近年来，诸多研究转向“归因文本生成”（attributed text generation），在生成的句子旁附带引用证据，帮助事后进行事实核查和纠错。然而：
  - 已有系统往往引用整个文档或整个段落，粒度过粗；
  - 阅读和核验引用内容本身的时间成本高，削弱了归因的实用价值；
  - 生成与归因在流程上是分离的，证据选择无法真正约束生成过程。

- **核心问题**：能否让模型在生成时**自动提供细粒度的、精确的“局部化归因”**——即让生成文本中的每个句子都直接对应源文中最相关的片段（一句话甚至子句级的连续文本），显著缩短核查负担，同时不损失文本质量与归因准确性。

- **整体含义**：论文将上述问题形式化为**“局部可归因的有根据文本生成”任务**，并提出了“先选定内容、后据此生成”的范式，使得归因不再是后置的“检查标签”，而成为整个生成过程的底层驱动机制——**“选择即归因”**。从技术、评估、人工核验成本等方面验证了细粒度归因生成的可实践性。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式与流程

### 核心思想

论文提出“Attribute First, then Generate”（先归因，再生成）方法。其核心是把传统“端到端生成”拆解为三个子步骤，用“先选、再排、后写”的方式天然地获得句子级、片段级的归因：

- **第一步：内容选择（Content Selection）**  
  从给定的若干文档中，抽取出对输出最有价值、且与任务要求最相关的连续文本片段。论文将这些片段称为“highlights”，它们在后续流程中既作为生成的事实依据，也直接成为最终输出引用中的归因片段。  
  - 对于 MDS，选择标准是“显著性”（salience）；  
  - 对于 LFQA，选择标准是“与查询的相关性”。
  - 为了保证片段可被精确映射，模型被要求逐字复制源文片段，并采用字符串匹配定位；无法匹配的片段会被丢弃。

- **第二步：句子规划（Sentence Planning）**  
  将第一步选出的片段组织为“有序的高亮簇”（clusters）。每个簇内的若干片段是后续被融合进同一个目标句子中的内容。该步骤引入了句子级归因结构：最终某个簇对应生成中的一个句子，因而每个生成句子的归因集合即该句对应的原文片段集合。

- **第三步：逐句生成（Sentence-by-sentence Generation）**  
  按第二步的簇顺序，每次生成一个句子。第 \(i+1\) 句的生成调用了“当前簇的片段内容 \(C_{i+1}\)”以及“此前生成的句子 \(s_{1:i}\)”：
  \[
  p(s_{i+1} \mid s_{1:i}, C_{i+1})
  \]
  这样既保证句子内容紧密对应预先选定的源片段，也能通过先前句子的前缀提升文本连贯性。

### 两种实现策略

1. **上下文学习（In-context Learning, ICL）**：
   - 使用 Gemini-Pro 模型；
   - 内容选择→句子聚类→逐句融合分别给定任务提示和少样本示例；
   - 探索了“Chain-of-Thought”（CoT）变体，将规划与生成合并为一次推理调用，先隐式决定哪些高亮进入哪个句子，再生成输出。

2. **微调（Fine-tuning）**：
   - 使用 PRIMERA（一个以多文档摘要为目标的 Longformer 编码器-解码器模型，447M 参数）；
   - 同样划分为“内容选择”“聚类规划”和“融合生成”三个可微调子系统；
   - 在内容选择和规划阶段引入“受约束解码”技术，迫使模型只输出原文中真实存在的片段，同时给最小片段长度与数量施加约束；
   - 同时测试“联合选择与规划”压缩流水线。

### 辅助处理

- 源文档中选中的片段会被包裹上 `<highlight_start>` 与 `<highlight_end>` 特殊标记，作为后续步骤的输入特征；
- 不同任务步骤的提示、标记、解析策略在附录中有完整示例。

## 3. 实验设计：数据集、场景和对比方法

### 任务场景与数据集

- **任务一：多文档摘要（MDS）**
  - 训练集：DUC、TAC 摘要任务；
  - 验证/测试集：Multi-News 数据集；
  - 关键标注资源：使用 Ernst 等的“摘要-原文命题级对齐”数据，将源片段与参考摘要句子对齐，用于构造三步流程的训练和验证目标。

- **任务二：长文本问答（LFQA）**
  - 使用 Liu 等（2023）请人类标注的大型语言模型回复引用数据；
  - 仅保留高质量样本：过滤掉不支持（unsupported）的回复，只保留被认为有帮助（评分 4/5）且证据可定位的样本。

### 对比方法（Baselines）

- **端到端生成**：
  - ICL 版本：直接让 Gemini 输出摘要/答案；
  - 微调版本：直接微调 PRIMERA。
- **归因基线（ALCE）**：
  - 采用 Gao 等的 ALCE 提示方法，让模型在文本内联生成引用（如 [1]），引用指向整篇源文档；
  - ICL 与人工都做了评估。
- **自研框架的多个变体**：
  - ICL 三步法（Attr.First）；
  - ICL+CoT 变体（Attr.First CoT）；
  - 微调三步法（Attr.First）；
  - 微调联合选择+规划变体（Attr.First joint）；
  - 对比“后置归因”路径：先用端到端方法生成内容，再使用类 RARR 方法回溯查询并捆绑证据片段。

### 评测指标

- **涵盖度/生成质量**：ROUGE-L、BERTScore；
- **归因质量**：AutoAIS（基于 NLI 模型 TRUE 对“句子是否被引用内容支持”的自动判定）；人工进行 AIS（Attributable to Identified Sources）打分；
- **归因粒度**：引用文本长度（token 数）；
- **核验成本**：人工标注者确认归因的耗时；
- **文本流畅度与有益性**：人工 5 点 Likert 量表。

## 4. 资源与算力

- 论文在正文和实验部分**未给出全局性的总计算量**描述。
- 但附录 C 中提供了关键信息：
  - 所有微调实验在单张 **Nvidia A100 80GB** GPU 上完成；
  - 每个子模型训练约 **10 个 epoch**，时长约 **1 小时**；
  - 实验使用的微调模型是 PRIMERA，参数规模 447M；
  - 主 ICL 实验则通过 Google API 调用 Gemini-Pro 完成。
- 在附录 J 的部署/延迟统计中，框架分步带来的单实例总耗时从数秒到数十秒不等（具体步骤的 token 数和时间如附录表 H.3/H.4 所示）；作者承认该框架相比“端到端生成”有较高推理延迟，需要多次模型调用。
- 综上所述，该文对训练资源做了基本披露，但未整合给出“总 GPU 时数”或全部超参搜索开销。

## 5. 实验数量与充分性

- **实验总量可观**：
  - 在两个任务上进行了跨 ICL、微调、联合规划、CoT 等 6～8 种方法变体的自动评测；
  - 在 MDS 和 LFQA 两个数据集上分别做了自动评测（主页结果表 1、表 2）；
  - 对最优配置（Attr.First ICL-CoT）与 ALCE 基线做了人工评测（表 3、表 4）；
  - 额外做了“有前缀 vs 无前缀”的消融实验；
  - 附录中还报告了全句级 AutoAIS 变体、后置归因、NLI 模型与人工判断的相关性测试等附加分析。

- **实验设计较为充分且规范**：
  - 同时覆盖自动指标与人工判断；
  - 人工评估包括流畅度、有益性、句子级 AIS、核验时间，并报告了标注者间一致性（Kappa=0.37）；
  - 自动评测使用已有的 NLI 评估范式和人工标注数据做辅助验证。

- **客观性与代表性需注意的方面**：
  - ICL 人工评估只对最优“Attr.First ICL-CoT”配置实施，未对微调版法进行全面人工评估；
  - 主实验只用一个 ICL 模型（Gemini-Pro）和一个微调骨干（PRIMERA），没有覆盖多模型泛化性；
  - 由于自动评测存在对基础 LLM 或 NLI

### 5. 实验数量与充分性（续）

……模型本身的依赖，以及自动阈值选择可能影响结果等，实验充分性仍有一定局限：

- 自动评测中的“归因支持度”完全依赖 NLI 模型（TRUE）的判断，而 NLI 模型对长文本、复杂推理的鲁棒性有限，可能将部分真实但不蕴含的内容误判为“不支持”；
- 细粒度归因的匹配依赖精确字符串匹配，对于改写或指代消解后的合法文本，可能造成漏检；
- 人工评测仅涉及英语数据集，且标注者数量不多（文中未报告具体人数），Kappa=0.37 仅属中等一致性，说明 AIS 判断本身存在主观性；
- 由于每种方法变体只运行在单一种子/单一配置下，实验报告未提供方差或显著性检验，难以判断某些小差距是否具有统计意义。

总体而言，该文的实验设计覆盖面较广，自动与人工评估相互补充，能够支撑其核心结论；但在模型多样性和统计严谨性方面仍留有提升空间。

## 6. 主要结果与发现

### 6.1 细粒度归因显著降低核验成本

- 在 MDS 和 LFQA 上，Attr.First 框架产生的归因引用长度远短于 ALCE 的整文档引用（MDS 中约减少 80% 以上的 token 数；LFQA 中也有明显压缩）。
- 人工核验时间相应降低：标注者阅读引用并判断句子是否被支持的耗时为 ALCE 的一半左右，说明“片段级引用”确实能让读者更快完成事实核查。

### 6.2 归因质量（AIS）与基线相当或更好

- 在 MDS 的 AutoAIS 上，Attr.First ICL-CoT 与端到端 ICL 持平，并显著优于 ALCE 基线；
- 在 LFQA 中，Attr.First 变体的归因质量优于直接生成+后置引用（ALCE）方法，且不牺牲答案有用性；
- 人工 AIS 评估表明：Attr.First ICL-CoT 生成句子的可归因比例与 ALCE 相当（差距在统计误差范围内），但在引用粒度和可读性上明显获胜。

### 6.3 生成质量几乎无损

- 在 ROUGE-L 和 BERTScore 上，Attr.First 与端到端生成的自动得分差距很小（多数在 0.5 分以内），人工流畅度评分也接近。
- 这说明“先选内容再生成”的约束并未像预期那样严重限制语言模型的表达能力——只要句子规划合理，融合生成仍能输出流畅且信息密集的文本。

### 6.4 生成即归因优于后置归因

- 论文对比了“先生成、再检索证据”的后置归因路径，发现其句子级 AIS 不如先选后生成的方式，且引用片段往往与生成句子在措辞上不匹配，核验成本反而更高。
- 这支持了核心动机：归因不应是事后的装饰性操作，而应在生成前就锚定证据片段。

### 6.5 消融实验的发现

- 去掉“句子前缀”（即每次生成时不看前面已生成的句子），人工流畅度和连贯性评分显著下降，说明逐句生成时保留上下文是必要的。
- 将内容选择与规划合并为一个步骤（joint 变体）在自动指标上略低于分步式，但在效率上更快；作者认为分步式具有更好的可控性和诊断性。

## 7. 研究贡献与创新点

1. **形式化新任务**：提出“局部可归因的有根据文本生成”，给出了句子级甚至片段级归因的定义和评估方式，将研究焦点从“引用有无”推向“引用粒度和可核查性”。
2. **归因驱动的生成范式**：颠覆了传统“生成-后验引用”的先后顺序，转为“选择-规划-生成”三步流水线，使每个输出句子天然地带有精确的源文片段证据。
3. **统一适用于 ICL 和微调**：证明该范式不局限于特定模型类别，既能用于大型闭源模型的上下文学习，也可搬到中等规模开源模型上进行微调，具备可迁移性。
4. **面向人工核验的评估设计**：引入核验时间、引用长度等实际使用维度，弥补了单纯依赖 AIS 或 NLI 指标的不足。
5. **工程上的约束解码技巧**：在微调的内容选择和规划阶段，利用受约束解码保证模型输出严格来自原文片段，从而保证归因映射的可靠性与可复现性。

## 8. 局限与未来研究方向

### 局限性

- **依赖高质量标注数据**：MDS 训练需要命题级对齐数据（Ernst 等），LFQA 需要人工标注“有用性+可支持性”的大模型回复，数据构建成本高，难以快速推广到新领域。
- **流水线误差累积**：内容选择若漏掉关键信息，后续规划与生成无法弥补；规划阶段的聚类错误会导致句子主题混乱，影响可读性。
- **片段拼接的自然性**：从多个异构文档中选取的片段直接融合，句子内部可能存在冗余或衔接生硬，自动指标难以察觉。
- **中文等其他语言未验证**：所有实验与人工评估均为英文，对于中文等语言的片段匹配、NLI 判断和标注可行性尚不明确。
- **推理延迟较高**：分步调用模型导致端到端延迟上升，在实际交互式系统（如实时问答）中可能构成部署瓶颈。

### 未来方向

- 开发更紧凑的“联合选择-规划-生成”端到端模型，以减少误差传递和推理开销；
- 引入非精确匹配的指代消解与语义对齐机制，放宽“逐字复制”的约束，同时保持可核验性；
- 对片段选择策略做强化学习或可微分近似，使选择过程能够感知下游生成器的需求；
- 探索跨语言、跨领域的归因数据自动构造，如使用弱监督或合成数据替代昂贵的人工标注；
- 将归因粒度与神经符号验证（如形式化事实检测）结合，构建更鲁棒的自动评测指标。

## 9. 总体评价

该论文聚焦于文本生成的可归因性问题，以“先选内容、再逐句生成”的流程有效实现了细粒度的局部归因。其最大亮点在于将归因从“结果标签”转变为“生成约束”，并通过引用长度与人工核验时间的下降证明了实际价值。实验设计兼顾了生成质量、归因质量和用户效率三个层面，证据比较充分。虽然受限于数据集、模型和语言的覆盖面，但作为一篇方法学论文，其核心思路清晰、工程实现完整，对多文档摘要、长文本问答以及未来的可解释文本生成研究具有明确的推动作用。对于任何关心大模型事实性、可信赖文本生成的研究者或工程师而言，本文的方法与结论都具有较强的参考意义。

（完）
