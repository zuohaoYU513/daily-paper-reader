---
title: "DocEE-zh: A Fine-grained Benchmark for Chinese Document-level Event Extraction"
title_zh: DocEE-zh：面向中文文档级事件抽取的细粒度基准数据集
authors: "Minghui Liu, Meihan Tong, Yangda Peng, Lei Hou, Juanzi Li, Bin Xu"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.35.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 中文文档级事件抽取细粒度基准，覆盖事件与论元
tldr: 中文文档级事件抽取因缺少细粒度、领域覆盖广的数据集而研究进展缓慢。本文发布DocEE-zh，包含超过3.6万事件和21万论元，作为DocEE数据集的扩展，并提供中文场景下文档级事件的训练与评测基准。该数据集面向跨句、篇章级的事件论元抽取，降低了中文该方向数据构建成本，可支撑事件抽取模型在中文长文档中的评测和后续迁移研究。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp35/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1622, \"height\": 961, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp35/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1631, \"height\": 914, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp35/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1603, \"height\": 668, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-findings/anthology-2024findings-emnlp35/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 820, \"height\": 609, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp35/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1636, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp35/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 726, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp35/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 566, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp35/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1723, \"height\": 1223, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp35/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1742, \"height\": 577, \"label\": \"Table\"}]"
motivation: 中文文档级事件抽取长期缺乏细粒度且覆盖面广的基准数据集，难以训练与评测模型。
method: 构建DocEE-zh中文文档级事件抽取数据集，含大量带论元标注的事件，并设计可迁移的标注框架。
result: 数据集规模超过三万六千事件、二十一万论元，提供了支持训练、评测的中文文档级基准。
conclusion: 填补了中文文档级事件抽取数据空白，为跨句事件论元识别与关系研究提供基础。
---

## Abstract
Event extraction aims to identify events and then extract the arguments involved in those events. In recent years, there has been a gradual shift from sentence-level event extraction to document-level event extraction research. Despite the significant success achieved in English domain event extraction research, event extraction in Chinese still remains largely unexplored. However, a major obstacle to promoting Chinese document-level event extraction is the lack of fine-grained, wide domain coverage datasets for model training and evaluation. In this paper, we propose DocEE-zh, a new Chinese document-level event extraction dataset comprising over 36,000 events and more than 210,000 arguments. DocEE-zh is an extension of the DocEE dataset, utilizing the same event schema, and all data has been meticulously annotated by human experts. We highlight two features: focus on high-interest event types and fine-grained argument types. Experimental results indicate that state-of-the-art models still fail to achieve satisfactory performance, with an F1 score of 45.88% on the event argument extraction task, revealing that Chinese document-level event extraction (DocEE) remains an unresolved challenge. DocEE-zh is now available at https://github.com/tongmeihan1995/DocEE.git.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文核心问题与整体含义（研究动机与背景）

- **研究背景**：
  - 事件抽取（Event Extraction, EE）旨在从文本中识别事件并抽取其论元（Arguments），是 NLP 信息抽取的重要任务。
  - 近年来，事件抽取研究已从**句子级**转向**文档级**，因为实际事件往往跨多个句子表达，需要模型具备多句推理和长距离依赖建模能力。
  - 英文领域已有丰富数据集（如 ACE2005、TAC KBP、Rich ERE、DocEE 等），但**中文文档级事件抽取仍发展不足**。

- **核心问题**：
  - 中文文档级事件抽取面临的主要障碍是**缺乏细粒度（fine-grained）、领域覆盖广（wide coverage）的训练与评测数据集**。
  - 现有中文数据集存在两方面缺陷：
    1. **领域覆盖有限**：多为金融领域（如 ChFinAnn、DuEE-fin），难以覆盖多样化新闻场景。
    2. **论元类型不够细化**：大量通用论元（ChFinAnn 中 60%、DuEE-fin 中 51%）削弱了模型对不同事件类型特有特征的捕捉能力。

- **论文贡献**：
  - 提出 **DocEE-zh**，一个大规模、细粒度、多领域的中文文档级事件抽取数据集，作为 DocEE 数据集的扩展。
  - 包含 **36,729 个事件**和 **216,496 个论元实例**，覆盖 59 个事件类型与 344 个论元类型。
  - 实验结果揭示中文文档级事件抽取仍是一项未解决的挑战。

### 2. 论文提出的方法论（核心思想与技术细节）

- **核心思想**：
  - 构建高质量中文文档级事件抽取数据集，具备两大特征：**高关注度事件类型**和**细粒度事件特有论元**。
  - 采用**一文档一核心事件**（one-event-per-document）的标注策略，聚焦新闻中的核心事件，提升实际应用价值。

- **方法论主要包括三个环节**：

  - **① 事件模式（Event Schema）构建**：
    - 基于 DocEE（Tong et al., 2022）的构建方法，依据硬新闻/软新闻理论定义 59 个事件类型（31 个硬新闻类型 + 28 个软新闻类型），覆盖政治、军事、娱乐、体育、财经、自然灾害等领域。
    - 论元定义分三步：
      1. **维基百科 Infobox 抽取**：每类事件收集 20 个维基百科页面，自动解析 key-value 信息确定初始论元（如地震事件的"震级"、"日期"、"深度"）。
      2. **权威新闻来源补充**：从新华社等来源每类分析 20 篇报道，邀请 5 名新闻学学生补充维基百科未覆盖的重要论元（如海啸的"涌浪高度"）。
      3. **合并去重**：最终获得 344 个论元类型，平均每类事件约 5.8 个论元。

  - **② 候选数据收集**：
    - 数据来源两个渠道：
      - **中文维基百科**：聚焦有中文词条的历史事件（如唐山大地震）。
      - **NewsMiner 系统**：2019-2023 年间来自六家主流新闻网站（腾讯、人民网、新华社、新浪、环球网、搜狐）的新闻报告。
    - 采用基于类别名称与 TF-IDF 的高频关键词检索策略，收集约 60,000 篇中文文章，经筛选后最终标注 36,729 篇。

  - **③ 众包标注流程**：
    - **阶段一：事件分类**：
      - 预标注 100 篇文章建立标准；剔除准确率低于 70% 的标注员（最终保留 48 人）；每篇文章由两位标注员双标注，不一致时由第三人仲裁；不属于任何类别则归为"Other"。
    - **阶段二：事件论元抽取**：
      - 90 名标注员参与，采用初标注 + 多轮迭代修订策略，每篇文章至少经三轮、由不同标注员交叉评审，标注准确率从初始 56.24% 提升至 85.96%。
      - 若同一论元在文中多次出现，所有提及均被记录以保证完整性。
    - **质量验证**：事件分类阶段 Cohen's kappa 达 93%，论元抽取阶段为 82%，表明标注一致性良好，成本约为每条 2 元人民币。

### 3. 实验设计

- **数据集与场景划分**：
  - 将 DocEE-zh 按 80%/10%/10% 划分为训练集、验证集和测试集。
  - 涉及两类子任务：
    1. **事件分类**：为给定文档分配一个预定义事件类型标签。
    2. **事件论元抽取**：给定文档与事件类型及对应的论元类型列表，输出从文档中抽取的论元集合。

- **Benchmark 概览**：
  - 与多个已有数据集进行了对比（表 1），包括句子级的 ACE2005-zh、KBP2017，以及文档级的 ChFinAnn、DuEE-fin、DEIE。DocEE-zh 在文档数（36,729）、论元类型数（344）、句子数（817,085）等方面均具优势。

- **事件分类任务对比方法**：
  - TextCNN（Kim, 2014）
  - BERT（Devlin et al., 2019）
  - RoBERTa（Liu et al., 2019）
  - ERNIE 3.0（Sun et al., 2021）
  - GPT-4（OpenAI, 2023，零样本）
  - 评估指标：Precision、Recall、Macro-F1

- **事件论元抽取任务对比方法**：
  - BERT_Seq（Du & Cardie, 2020a）
  - MG-Reader（Du & Cardie, 2020a）
  - BERT_QA（Du & Cardie, 2020b）
  - Doc2EDAG（Zheng et al., 2019）
  - PTPCG（Zhu et al., 2021）
  - ProcNet（Wang et al., 2023b）
  - ReDEE（Liang et al., 2022）
  - PAIE（Ma et al., 2022）
  - GPT-4（零样本，另有基于语义等价的人工评测变体 GPT-4 (Human)）
  - 评估指标：Precision、Recall、F1

- **GPT-4 评测设置细节**：
  - 零样本学习，从每类事件中随机采样 10 个样本（共 590 个事件）构成独立测试集。
  - 自动评估采用精确匹配；由于 GPT-4 生成结果存在表达形式不同但语义正确的情况，额外引入人工语义等价评估。

### 4. 资源与算力

- **论文未明确说明具体使用的 GPU 型号、数量及训练时长**。
- 仅提供了一些超参数信息：Transformer 基线采用 base 版预训练模型（hidden size 768 级别的 base 模型），学习率 2e-5、batch size 32、最大文档长度 512。
- GPT-4 部分为 API 零样本调用，未说明具体调用规模。
- 人工标注方面提到成本约每条 2 元人民币。

### 5. 实验数量与充分性

- **实验数量**：
  - 事件分类任务：5 个基线模型（TextCNN、BERT、RoBERTa、ERNIE 3.0、GPT-4）。
  - 事件论元抽取任务：9 个基线系统（含 GPT-4 自动评测与人工评测两种设置）。
  - 数据集包含 59 种不同事件类型，表 2、表 3 提供了完整对比。

- **充分性与公平性分析**：
  - **充分之处**：
    - 对比方法覆盖了传统分类模型、监督微调的 Transformer、文档级事件抽取专用框架、基于提示学习的生成式模型，以及大规模语言模型的零样本能力。
    - 同时报告精确匹配和人工语义评估，探索了生成模型评估方式的差异。
    - 数据规模大（36k+ 文档），实验结果为未来研究提供了有价值的参考基准。
  - **不足与潜在偏差**：
    - **无消融实验**：未进行针对论元类型设计、标注策略等构建决策的消融研究。
    - **总体性能偏低**：最先进模型在论元抽取任务中 F1 仅约 46%（ProcNet），说明实验揭示的是能力上限不足而非充分探索了模型的优化空间。
    - **评测不一致性风险**：GPT-4 在自动评估（F1 24.88%）与人工评估（F1 68.86%）间存在极大差距，精确匹配可能低估生成式模型，而人工语义判定则可能引入主观偏差且难以复现，两组数字间的巨大差异也缺乏进一步分析。
    - **基线公平性**：部分基线（如 Doc2EDAG、PTPCG 等）最初是针对金融文档设计的，未经调整就在 DocEE-zh 上评估，可能未能充分发挥其能力。

### 6. 主要结论与发现

- **DocEE-zh 填补了中文文档级事件抽取数据集的空白**，提供了最丰富的事件类型-论元映射关系（每事件类型平均 5.8 个细粒论元，344 个独特论元类型，86% 为特定事件独有）。
- **事件分类任务**相对较为可解：最佳模型 RoBERTa 取得 Macro-F1 89.16%，ERNIE 3.0（88.71%）接近，GPT-4 仅 66.39%，说明专业化微调仍具优势。
- **事件论元抽取任务依然困难**：所有监督模型 F1 均低于 46%，最高为 ProcNet 的 45.88%。模型普遍面临精度与召回难以平衡的问题（如 Doc2EDAG 精度 49.45% 但召回仅 31.06%），多句推理与长距离依赖构成主要技术瓶颈。
- **GPT-4 的能力在抽取类任务中被自动评估严重低估**：即便采取了更宽松的语义匹配，自动精确匹配下 F1 仅为 24.88%；人工语义评估下达 68.86%，但依然说明生成式模型在需要严格抽取的场景中并不可靠。
- **中文文档级事件抽取仍然是开放问题**，需要更加适应细粒度论元定义与跨句推理的新模型架构与评估策略。

### 7. 优点

- **数据集规模与细粒度程度领先**：36,729 篇文档、344 种论元类型、86% 的事件特有论元设计，明显优于 ChFinAnn、DuEE-fin 等既有中文数据集。
- **多领域覆盖性**：59 种事件类型横跨硬新闻（灾害、政治、冲突、科技）与软新闻（体育、娱乐、公众人物生活等），有助于推进通用事件抽取。
- **严谨的人工标注流程**：
  - 双标注 + 第三方仲裁机制有效降低主观性；
  - 多轮迭代修订使标注准确率从 56.24% 提升到 85.96%；
  - kappa 系数（分类达 93%，论元达 82%）提供了可靠性证据。
- **合理的构建方法论**：融合维基百科结构化信息与权威新闻报道，并引入新闻专业学生参与论元设计，保证论元体系的科学性与实用性。
- **实验覆盖面广**：同时纳入传统监督模型、专用文档级抽取架构、生成式模型和 GPT-4，既给出了各自能力的初步刻画，也揭示了现有评测范式与生成模型之间的适配问题。

### 8. 不足与局限

- **单事件标注限制**：仅标注每个文档的核心主事件，无法处理多事件共现的复杂文档，限制了数据的通用性和模型在多事件场景中的迁移能力。
- **抽取式论元标注忽略了模型推理能力**：
  - 当前论元标注仅采用文档中显式出现的文本片段，覆盖不了需要推理才能获得的隐含信息。
  - 如表 4 所示，当 GPT-4 基于上下文正确推断出完整日期（"April 24"）时，数据集标注仅为不完整的显式文本（"24th"），导致模型被误判为错误。这一设计偏差会模糊模型真实的抽取与推理能力。
- **事件类型分布不均**：数据呈典型长尾分布，头部 15 类事件占据较大比例（出现超过 500 次的事件类型仅占 36.2%），尾部事件训练样本不足可能影响对少数事件类型的抽取效果。
- **实验缺乏消融与进一步分析**：未检验标注策略、论元类型覆盖度、不同分词等设计选择对模型效果的具体影响。
- **资源细节不透明**：未报告 GPU 型号、数量等关键复现信息，难以准确评估算力成本和复现门槛。

（完）
