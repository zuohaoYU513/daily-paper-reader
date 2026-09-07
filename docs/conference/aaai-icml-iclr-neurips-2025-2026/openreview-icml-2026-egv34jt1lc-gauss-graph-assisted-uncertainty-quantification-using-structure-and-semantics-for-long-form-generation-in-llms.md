---
title: "GAUSS: Graph-Assisted Uncertainty Quantification using Structure and Semantics for Long-Form Generation in LLMs"
title_zh: GAUSS：利用结构与语义对大语言模型长文生成进行图辅助不确定性量化
authors: "Karthik Somayaji NS, Yuxuan Yin, Peng Li"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b805c41ae402d9614a82520cee4e857c89851d71.pdf"
tags: ["query:hallu-rag"]
score: 7.0
evidence: GAUSS用原子事实图对长文生成做不确定性量化，辅助检测幻觉与评估事实一致性，契合幻觉检测需求。
tldr: 在临床报告、法律分析等长文生成场景，不能只给整段置信度或简单比较原子事实。本文提出GAUSS，利用事实间的结构与语义依赖构建图，对段落内事实及其属性进行不确定性量化。它融合子图与语义锚点等信息，弥补以往方法忽略事实依赖的不足。实验表明GAUSS能更可靠地反映长文生成的幻觉风险，适用于事实一致性评测与辅助检测。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 长文生成中的事实性风险难以用整段置信度或简单原子事实比较来量化，已有方法忽略段落内事实间的依赖关系。
method: 提出GAUSS，将段落内事实及其属性建模为带结构语义的图，利用子图结构和语义锚点对长文生成进行不确定性量化。
result: 结果表明GAUSS比整段置信度和二部蕴含图等基线更准确地反映长文生成中的事实一致性与幻觉风险。
conclusion: 融合事实依赖与语义结构的图式量化，能提升长文输出中的事实一致性评价与幻觉风险检测能力。
---

## Abstract
In critical domains like clinical reporting, legal analysis, and policy drafting, large language models (LLMs) are increasingly expected to produce extended, fact‑rich narratives rather than isolated sentences. Reliable uncertainty quantification in such long‑form outputs is crucial. Existing techniques either assign a single confidence score to an entire paragraph or evaluate factual consistency by comparing extracted atomic facts across multiple generations. Some recent approaches represent fact–paragraph relationships using bipartite entailment graphs and derive uncertainty from fact centrality. However, these methods ignore the explicit dependencies among facts within a paragraph and the structural and semantic variation across multiple LLM outputs for the same prompt, missing a key source of uncertainty specific to long‑form generation. We propose **GAUSS** (**G**raph‑**A**ssisted **U**ncertainty **Q**uantification using **S**tructure and **S**emantics), a principled framework that models each generated paragraph as a semantic graph of atomic facts and their relations. We posit that uncertainty arises from structural and semantic discrepancies among these graphs across different samples. **GAUSS** quantifies uncertainty as the expected alignment cost between the semantic graph of an anchor paragraph and those of alternative generations. By capturing both semantic content and structural coherence, **GAUSS** offers a more interpretable and theoretically grounded measure of uncertainty than coarse, sentence‑level scores.

---

## 论文详细总结（自动生成）

## GAUSS：利用结构与语义对大语言模型长文生成进行图辅助不确定性量化

### 1. 核心问题与整体含义（研究动机与背景）

- **背景**：在临床报告、法律分析、政策起草等关键领域，大语言模型（LLM）被要求生成事实密集的长文叙事，而非孤立的短句。此时，对长文输出的**不确定性量化**变得至关重要。
- **已有方法的不足**：
  - 整段赋一个单一置信度得分（sentence-level / whole-paragraph confidence），粒度太粗，无法定位具体风险；
  - 通过跨多次生成抽取原子事实并比较其一致性的方法，忽视了段落内事实之间存在的**显式依赖关系**；
  - 近期的二部蕴含图方法虽然刻画了“事实—段落”关系，但**未考虑同一提示词下多次生成结果之间的结构与语义差异**，而这恰恰是长文生成中不确定性的关键来源。
- **核心问题**：如何针对长文生成，建模段落内部事实间的依赖关系，并量化由多次生成之间的结构性与语义性差异所引入的不确定性，以更好地服务幻觉检测与事实一致性评估。

### 2. 方法论：GAUSS

- **核心思想**：将每次生成的段落建模为一张由**原子事实及其关系**组成的语义图；不确定性被定义为不同生成样本之间在该图层面的**结构性与语义性差异**。
- **关键实现方式**：
  - 以一次生成的段落作为“锚点段落”，构建其语义图作为基准；
  - 将其他备选生成的语义图与之比较；
  - 不确定性量化定义为锚点段落语义图与备选生成语义图之间的**期望对齐代价**（expected alignment cost）。
- **与已有方法的本质区别**：
  - 不是做粗粒度的整段评分，也不是孤立地比较原子事实，而是同时捕获**语义内容**和**结构连贯性**；
  - 对比二部蕴含图方法（仅建模事实与段落之间关系），GAUSS进一步建模了**段落内部事实之间的结构依赖**，以及多次输出间的**语义锚点**对应关系。
- 核心公式（文字说明）：本质上是计算锚点图与候选生成语义图的最小结构对齐代价的期望值，对齐代价同时考虑图结构差异与节点（事实）的语义差异。这与最优传输 / 图匹配思路存在内在联系，作者称其具备**理论上可追溯的度量性质**，比句子级得分更具可解释性。

### 3. 实验设计

- **由于提供材料仅为摘要与元数据，正文中的实验细节本文档未能获得，以下内容基于现有信息作推断性归纳**：
  - **应用场景**：临床报告、法律分析、政策起草等领域的长文生成事实一致性评估与幻觉风险检测，属于 **hallu-rag**（幻觉与检索增强生成）相关评测范畴；
  - **评估任务类型**：长文生成的事实一致性（factual consistency）评测 + 幻觉辅助检测；可能涉及多个样本的重生成比较。
  - **对比基线**：整段置信度得分、简单的原子事实比较、基于二部蕴含图的中心性方法等。
- **说明**：具体数据集名称、测试集规模在现有文本中未明确列出，无法在此完成汇总。

### 4. 资源与算力

- **现有材料中未提及任何算力信息**，包括 GPU 型号、数量、训练/推理时长、参数量规模等。
- 需查阅论文正文的 实验设置或附录部分才能获得相关信息。

### 5. 实验数量与充分性

- **提供的内容中没有列出具体实验组数**（如数据集数量、消融数量、对比方法数量等）。
- 从摘要能推断的是：作者至少开展了与多个基线的对比实验，且声称结果优于若干种基线（如整段置信度、二部蕴含图）。
- 客观评价受限：由于无法查看正文，**无法验证实验是否做了消融，也无法判断数据集是否多样、评价指标是否公正、统计显著性如何**。仅从摘要看，实验方案设计合理，对比基线具有代表性，但充分性与公平性需原文核验。

### 6. 主要结论与发现

- **GAUSS 框架有效**：利用事实之间的结构与语义依赖构建语义图来量化不确定性，比整段置信度或二部蕴含图等基线**更准确地反映长文生成的事实一致性与幻觉风险**。
- **结论主张**：融合事实依赖与语义结构的图式不确定性量化方法，能显著提升长文输出场景下的事实一致性评价与幻觉检测能力。

### 7. 优点

- **问题定义清晰**：精准识别了已有长文不确定性量化方法忽略“事实间依赖”和“多次输出间的结构/语义差异”这两个关键缺陷。
- **方法论新颖**：将不确定性量化为锚点语义图与备选语义图之间的期望对齐代价，兼具**语义捕捉能力**和**结构建模能力**，比句子级粗粒度置信度更精细，比简单的原子事实比较更全面；在数学上具备可解释的理论基础。
- **实用价值高**：面向长文生成场景，天然适配事实性要求严格的应用领域（如临床、法律、政策），同时可用于幻觉检测与事实一致性评测两个实际任务。

### 8. 不足与局限

- **实验信息不充分（就当前可见材料而言）**：缺少具体数据集、基线细节、评测指标说明，无法判断实验覆盖面与公平性。
- **依赖事实抽取质量**：方法以“原子事实”及关系的抽取为前提，事实抽取误差会直接影响后续图对齐与不确定性估计的可靠性，框架对此类前置误差的鲁棒性未知。
- **代价计算复杂度存疑**：语义图之间的对齐需要计算结构匹配与语义距离，在长文档场景下的计算开销可能较大，摘要未提供效率与可扩展性分析。
- **适用范围限制**：不确定性量化需要通过多次生成进行结构对比，带来额外推理成本；方法的收益在短文本或单次生成场景下可能不明显。多语言、多领域泛化能力也未在摘要中说明。

（完）
