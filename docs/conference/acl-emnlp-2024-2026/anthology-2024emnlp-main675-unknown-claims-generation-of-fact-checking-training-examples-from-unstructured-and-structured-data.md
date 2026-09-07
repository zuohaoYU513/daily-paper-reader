---
title: "Unknown Claims: Generation of Fact-Checking Training Examples from Unstructured and Structured Data"
title_zh: 未知声明：从非结构化与结构化数据生成事实核查训练样例
authors: "Jean-Flavien Bussotti, Luca Ragazzi, Giacomo Frisoni, Gianluca Moro, Paolo Papotti"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.675.pdf"
tags: ["query:faithfulness"]
score: 4.0
evidence: 从文本与表格证据自动生成支持/反驳的事实核查训练样本，可服务于无依据内容检测
tldr: 计算事实核查依赖大量人工标注训练数据，成本高昂。论文提出Unown框架，可自动从文本与表格数据中选择证据，并生成带否定伪影的支持性与反驳性声明，从而构建事实核查训练集。该框架在Feverous、SciFact及新多模态基准MMFC上得到验证，显示其生成训练样例的灵活性与可用性。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 794, \"height\": 608, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1650, \"height\": 1083, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1600, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 818, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 780, \"height\": 201, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 700, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 727, \"height\": 329, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 808, \"height\": 287, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 781, \"height\": 198, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 769, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 707, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main675/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 693, \"height\": 1245, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 817, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 813, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 690, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 816, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 816, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 765, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 779, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1660, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1661, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1661, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main675/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1657, \"height\": 504, \"label\": \"Table\"}]"
motivation: 事实核查模型训练需要大量人工标注，成本高且难以扩展。
method: 设计Unown框架，依据文本/表格证据选择相关语句并生成支持与反驳声明及否定变体。
result: 在Feverous、SciFact与MMFC上验证了自动生成训练样例的效果。
conclusion: 自动化生成核查训练样例能够降低事实核查数据标注依赖。
---

## Abstract
Computational fact-checking (FC) relies on supervised models to verify claims based on given evidence, requiring a resource-intensive process to annotate large volumes of training data. We introduce Unown, a novel framework that generates training instances for FC systems automatically using both textual and tabular content. Unown selects relevant evidence and generates supporting and refuting claims with advanced negation artifacts. Designed to be flexible, Unown accommodates various strategies for evidence selection and claim generation, offering unparalleled adaptability. We comprehensively evaluate Unown on both text-only and table+text benchmarks, including Feverous, SciFact, and MMFC, a new multi-modal FC dataset. Our results prove that Unown examples are of comparable quality to expert-labeled data, even enabling models to achieve up to 5% higher accuracy. The code, data, and models are available at https://github.com/disi-unibo-nlp/unown

---

## 论文详细总结（自动生成）

# 论文总结：UNOWN：从非结构化与结构化数据生成事实核查训练样例

## 1. 核心问题与整体含义（研究动机和背景）
- **问题背景**：计算事实核查（Fact-Checking, FC）依赖监督学习模型验证声明，需要大量人工标注的训练数据。人工标注需专家逐条编写证据‑声明对并构造反驳样本，成本高、耗时且难以扩展。
- **现有自动合成训练数据方法的局限**：
  1. 未将**结构化表格数据**与**非结构化文本**有机结合（真实世界声明往往需要联合验证两者）。
  2. 仅针对**特定领域**（如生物医学），依赖领域知识库（KB），无法跨域泛化。
- **核心含义**：论文提出 **UNOWN** 框架，能够从任意给定的半结构化文档（句子 + 表格）中自动生成带标注（Supports/Refutes）的 FC 训练样本，以降低对人工标注的依赖，并适应不同资源条件（从冷启动到少量标注、从 SLM 到 LLM）。

## 2. 方法论
- **总体流程**：输入文档 \(d\) → **证据选择**（构建文本锚点并完成证据上下文）→ **声明生成**（生成支持性/反驳性声明）→ 输出训练三元组 <证据, 声明, 标签>。
- **证据选择**：
  1. **锚点创建（Anchor）**
     - 纯文本场景：从 \(d\) 中随机选择一个句子作为锚点。
     - 文本 + 表格场景：将 T5-large 在 ToTTo 数据集上微调得到表格‑到‑文本的 verbalizer，先随机抽取若干表格单元格（数量分布模仿 FEVEROUS 训练集），再根据表格头、单元格值和文档标题生成一段文本锚点，实现两种模态的统一。
  2. **证据完成（Evidence Completion）**
     - **随机策略**：从文档中随机抽取 k 个句子拼接进证据。
     - **语义一致性策略**：用 T5 编码后计算锚点与各句子的余弦相似度，选取最相关的 k 个句子，保持主题连贯。
     - k 也从与 FEVEROUS 训练集证据规模匹配的分布中采样。最终证据以 `<title> <evidence> ...` 格式组织，使模型能对标题、表格、句子进行跨注意力。
- **声明生成**：
  - **支持性声明**：将证据作为输入，由生成模型（BART-large 400M 或 LLaMA-2-7B）直接生成声明，训练目标是 \(e \rightarrow c\)。
  - **反驳性声明**：
     - **直接拒绝（Direct Refusal）**：让模型直接根据证据生成矛盾声明。
     - **两步法（Two-Step）**：先由生成模型生成支持性声明，再对其执行“直接拒绝”或“实体替换（ER，Entity Replacement）”。
  - 实体替换基线：使用 FLAN-T5-large 找反义词、GenSim+WordNet 找相似词、ConceptNet 找相关知识并替换关键实体，以构建更自然的矛盾表达。
  - **冷/热启动**：warm-start 时先使用外部任务数据（FEVER 的 10K+/10K− 样本）对生成模型微调；随后可根据目标数据集中的少量样本（10、100）做 few-shot。
- **与典型自动化方法的区别**：不仅依赖问答/实体替换，而是统一支持“纯文本”和“文本 + 表格”输入，无领域知识库需求。

## 3. 实验设计
- **数据集 / Benchmarks**：
  - **FEVER**：作为 warm-start 的外部样例集（10K 正 / 10K 负）。
  - **FEVEROUS**：验证集代替私有测试集使用，并分离为 **文本-only** 与 **文本 + 表格** 两个场景子集。
  - **SciFact**：科学论文摘要相关的专业声明，仅文本证据。
  - **MMFC（New）**：从 MultiModalQA 抽样 2000 例，过滤视觉依赖后，用 GPT-4-Turbo 结合少样本将问答对转换成 claims，再经人工核查，构建出含文本与表格证据的多领域多模态 FC 测试集。
- **对比方法**：
  1. 人工标注训练数据 vs. UNOWN 生成数据；
  2. 多种证据选择方式：人类证据、随机+gold 句子数、随机无 gold、语义一致性；
  3. 多种反驳声明生成策略：BART-large、BARTNeg、LLaMA-2、实体替换（FLAN-T5、WordNet、ConceptNet 等变体）；
  4. 不同训练样本数量（0、10、100、10K）和冷/热启动设置。
- **下游 FC 验证模型**：
  - FEVEROUS/MMFC：RoBERTa；
  - SciFact：MultiVerS。
- **评估**：Accuracy、F1（按 Supports/Refutes 区分）、NLI 一致性（用 DeBERTa cross-encoder 判断证据与声明的关系）、人工评估（清晰度与连贯性盲比对）、否定伪影标注分析。

## 4. 资源与算力
- 文中附录提到：所有实验在 Linux 集群上进行，每项实验使用 **单块 Nvidia RTX3090 Turbo GPU（24 GB VRAM）** 运行；但论文**未明确**总共使用的 GPU 数量、整体训练耗时或单次完整实验的总天数。
- 提供了生成阶段的部分时间测量（每生成一条声明）：BART 训练 1.92s、推断 0.12s；BARTNeg 1.01s / 0.08s；LLaMA-2 1.98s / 2.10s；表格 verbalization（T5-ToTTo）推断 0.75s；语义一致性证据选择（T5 tokenize+距离计算）5.43s。因此每条样本的总生成时间约在数秒级，明显低于人工构造所需时间。
- 实验规模层面，warm-start 需要基于 FEVER 的 2 万条样本对生成模型进行微调，这会消耗一定 GPU 算力，但在低资源部署层面作者称模型仍较为轻量。

## 5. 实验数量与充分性
- **实验数量较多、设置较系统**：
  1. FEVEROUS 上对不同训练样本量（0/10/100/10K）和冷启/热启的横断对比（图 5、图 6）；
  2. SLM（BART 系列）与 LLM（LLaMA-2）的对比；
  3. 证据选择的 4 种策略 × 文本/表格式场景对比（表 5）；
  4. 反驳声明生成的多模型与实体替换基线对比（表 6、图 12）；
  5. NLI 质量分析（表 3）；
  6. FEVEROUS 挑战类别（Combining Tables and Texts、Multi-hop Reasoning、Numerical Reasoning 等）上的细粒度分析（表 4）；
  7. 两轮人工评估（50 claims 文本-only + 60/100 claims 多模态，以及 30 例否定伪影分类）；
  8. SciFact（跨域验证）和 MMFC（新数据基准）上的额外实验；
  9. 模态消融（表 7，去除表格/去除句子的影响）等。
- **充分性评判**：总体上覆盖面广，兼顾自动指标与人工判断，并考虑了不同标注预算、热启动来源、证据类型和领域，实验较**客观且公平**。但存在几个偏差风险：
  - FEVEROUS 原测试集并未公开，使用验证集作为测试集会降低与官方报告结果的直接可比性；
  - SciFact 人类训练数据本身数量很少（0.3K/0.2K），易于引起波动；
  - MMFC 的人工核查仅保证 claims 正确性，但证据采样与生成链路中仍可能引入隐式偏差；
  - “文本-only”部分结论与“文本+表格”部分结论张力较大（如在纯文本场景合成数据仍低于人工数据 8%），并非在所有设置下都能超过人工标注。
- **总体**：实验数量足以支持主要结论，但在跨域泛化（只有科学 + 通用领域）和多语言（不含低资源语言）上覆盖还不全面。

## 6. 主要结论与发现
- **合成数据接近人类数据质量**：在 FEVEROUS 文本-only 场景中，纯冷启动最好的 UNOWN 训练结果约为 86.7%（人类数据为 94.5%）；warm-start 后加入 100 条目标域人类样本可到 92.3%，由 LLaMA-2 生成可在 93.3%，逐步逼近全人类标注的上界。
- **文本 + 表格场景优势突出**：使用 UNOWN 合成数据训练的模型，在 FEVEROUS 文本+表格子集上取得**比人工标注数据高最多 5%** 的准确率；并且“语义一致性”证据选择比直接使用人类证据效果更好，说明自动证据选择能在表格场景中缓解人工标注的不一致性。
- **SLM 和 LLM 差别不大**：SLM（BART 系列）与 LLM（LLaMA-2-7B）生成的数据在下游准确率上相差约 1%，而 SLM 的计算成本更低，具有更好的“效率‑效果”权衡。
- **反驳声明生成**：
  - BARTNeg（针对事实核查训练过的专用小模型）比直接实体替换更有效，尤其在科学领域（SciFact 上 F1 明显优于 ER）；
  - 实体替换法倾向产生浅层/不合理改动，且强依赖词汇资源覆盖范围；
  - UNOWN 生成的反驳声明在否定类型（Verbal/NP、Lexical/Morphological/Replacement）的分布和多样性上表现出与人类编写数据相似的趋势。
- **冷/热启动作用**：外部数据（FEVER）对生成模型进行 warm-start 可显著提升合成样本质量，但目标数据集内部样本越多，外部启动带来的额外增益逐渐减小（图 9），说明外部数据只是引导性知识来源。
- **MMFC 上的短板**：UNOWN 生成数据用于训练 RoBERTa 后在 MMFC 上效果低于人类证据引导的结果；作者认为是因为 warm-start 所用 FEVER 与 MMFC 领域差异带来的负面迁移，强调了数据生成器与下游目标域的对齐重要性。

## 7. 优点
- **问题新颖且实用**：第一个系统地将“文本 + 表格”两类事实核实证据纳入自动 FC 训练数据生成框架，能够覆盖更多实际声明验证场景。
- **方法灵活性高**：支持多种证据选择策略和声明生成手段（直接生成/两步改写/实体替换）、支持冷启动/热启动、兼容 SLM 与 LLM，可部署于不同硬件环境。
- **减少对领域 KB 的依赖**：相对 Wright et al. 的工作（仅在生物医学 KB 上工作），UNOWN 是领域无关的，可以从小型通用语料

（接上文）

……从小型通用语料中抽取证据，而无需为每个新领域重新搭建知识库，显著提升了数据生成管线的可移植性。

- **方法透明、分析与人工评估并重**：不仅报告标准准确率，还引入 NLI 一致性验证、否定极性分布分析、盲评与错误分类，使读者能理解“合成数据为何有效/失效”的内在机制，而不仅仅看到指标提升。
- **实验设计具有示范意义**：系统地将“人工证据”与“自动证据”对比，将“人工声明”与“机器声明”对比，并在不同预算（0/10/100/10K）下考察收益曲线，给出可操作的资源决策参考（如：目标域 100 条样本即可达到接近人工标注的性能上限）。
- **对低资源与多语言场景具有参考价值**：虽然论文没有直接实验多语言，但其“无领域知识库 + 有限人工样本 + 小模型”的设定为低资源事实核查研究提供了可复制的范式。

## 8. 缺点与局限性

- **测试集可比性问题**：FEVEROUS 的官方测试集未公开，论文使用其验证集作为评测基准，使得自动化指标不能直接与该榜单上的其他方法横向比较；相关结论需在官方测试集上复验。
- **证据构建的真实性偏差**：UNOWN 采用的证据选择策略（随机或语义相似）虽然模拟了 FEVEROUS 的证据分布，但本质上仍是在“已知文档内”选取句段，未考虑现实中证据可能缺失、文档可能包含错误信息、或需要跨多个独立来源的情形，因此对更开放的互联网事实核查场景仍然存在理想化假设。
- **对“反驳声明”多样性的控制不够充分**：尽管作者统计了否定类型的分布，但生成的反驳声明仍可能出现“过度否定”或“无意义改写” (如仅替换为反义词但语义并未真正冲突)；其中的实体替换基线还需外部词汇资源，违背了“无需外部知识库”的初衷。
- **LLM 对照使用的模型规模与代表性有限**：仅使用 LLaMA-2-7B 作为大模型代表，未与更强的指令微调模型（如 GPT-4、Mistral-7B-Instruct）做对比；因此“SLM 效果与 LLM 相当”这一结论很可能受生成器训练目标和提示方式的限制，推广时需谨慎。
- **人工评估样本量偏小**：人工评审仅针对 50~100 条声明，且由少数标注者参与，缺乏统计显著性检验；对“自然度/流畅性”的判断主观性强，难以精确度量合成数据与人工数据在语言质量上的真实差距。
- **跨域泛化结论薄弱**：只在 FEVEROUS 与 SciFact 上验证，其中后者是专业学术摘要，前者仍是百科类结构化文本；对新闻、社会媒体、对话内容等事实核查常见场景尚未评估，无法支撑“普遍适用”的论断。
- **冷启动阶段与热启动实验存在任务混淆**：声称支持“冷启动”，但实际冷启动仍使用了 ToTTo 与 FEVER 做预训练/微调，这并不能被视为“零外部数据”的绝对冷启动；事实上，生成模型本身（BART/LLaMA）已经包含大规模预训练知识，所谓冷启动仅指下游 FC 训练集中没有目标域样本。

## 9. 总结与个人思考

**UNOWN** 的主要贡献在于将在传统事实核查数据合成中被分离的“句子”和“表格”统一到一个生成框架中，提出了锚点‑证据‑声明的流水线，使自动构造 FC 训练数据不再依赖领域知识库，并揭示了两个具有实践价值的发现：

1. **当声明需同时消费文本与表格证据时，UNOWN 合成数据甚至优于人工标注数据**——这很可能是因为人工标注员在构造此类样本时容易忽略某些表格单元格或仅依赖单模态线索，而自动流程反而能覆盖更多模态间的矛盾模式。
2. **数据生成器与目标域的对齐比生成器规模更关键**——MMFC 上的性能倒挂清楚地说明，一个在海量通用数据上表现良好的生成器，并不一定适合“领域偏移较大 + 证据类型混合”的下游任务；未来工作应着力于动态选择/构建与目标域更相似的预热数据。

从更宏观的视角看，UNOWN 是一种典型的“数据为中心”的 AI 解决思路：不扩大模型，而是改造训练数据。其方法论可进一步延伸至其他知识密集型任务，如开放域问答、事实验证与对话系统的负采样等。要想真正取代人工标注，仍需在“证据真实性控制（防幻觉）”“否定多样性生成”“跨语言与跨领域迁移”三个方向上做更细粒度的优化；但作为组合了 SLM/LLM、多模态证据、预算感知与无领域资源的统一框架，UNOWN 已为低资源事实核查研究树立了一个清晰可复现的基线。

（完）
