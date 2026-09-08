---
title: "ET-MIER: Entity Type-guided Key Mention Identification and Evidence Retrieval for Document-level Relation Extraction"
title_zh: ET-MIER：实体类型引导的关键提及识别与证据检索用于文档级关系抽取
authors: "Xin Li, Huangming Xu, Fu Zhang, Jingwei Cheng"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.961.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 文档级关系抽取中联合关键提及识别与证据句检索，提升跨句关系推理
tldr: 文档级关系抽取需要跨句关联同一实体的多个提及，并用证据句推断关系，现有工作未充分区分提及贡献和证据重要性。ET-MIER利用实体类型提供的一致语义约束，识别对关系判定更关键的关键提及并检索证据句子，从而减少无关提及与噪声。实验结果表明实体类型引导能有效提升文档级关系抽取性能，并增强关系证据的可用性。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp961/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 889, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp961/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 644, \"height\": 1104, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1406, \"height\": 1207, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1406, \"height\": 1335, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 686, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 770, \"height\": 568, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 645, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 605, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 717, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 794, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 801, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp961/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1644, \"height\": 986, \"label\": \"Table\"}]"
motivation: 现有文档级关系抽取对提及贡献和证据句内关键提及的区分不足。
method: 利用实体类型先验联合识别关键提及与证据句，抑制不可能的实体对关系。
result: 在文档级关系抽取基准上取得更优结果，验证了提及与证据选择的收益。
conclusion: 实体类型约束可显著改进跨句实体关系的抽取和证据利用。
---

## Abstract
Document-level relation extraction (DocRE) task aims to identify relations between entities in a document. In DocRE, an entity may appear in multiple sentences of a document in the form of mentions. In addition, relation inference requires the use of evidence sentences that can provide key clues to entity pairs. These make DocRE more challenging than sentencelevel relation extraction. Existing work does not fully distinguish the contribution of different mentions to entity representation and the importance of mentions in evidence sentences. To address these issues, we observe that entity types can provide consistent semantic constraints for entities of the same type and implicitly preclude impossible relations between entities, which may help the model better understand both intra- and inter-entity mentions. Therefore, we propose a novel model ET-MIER, which for the first time leverages **E**ntity **T**ypes to guide key **M**ention **I**dentification and **E**vidence **R**etrieval. In this way, entity types not only help learn better entity representation but also enhance evidence retrieval, both of which are crucial for DocRE. We conduct experiments on widely-adopted datasets and show that our model achieves state-of-the-art performance. Our code is available at: https://github.com/NEU-IDKE/ET-MIER

---

## 论文详细总结（自动生成）

# 论文总结

## 1. 核心问题与整体含义

- **研究背景**：文档级关系抽取（DocRE）旨在识别同一文档中实体对之间的关系。与句子级关系抽取相比，DocRE 中同一实体可能以多个提及（mention）的形式分散在不同句子中，且实体间关系的推断往往需要依赖跨句的证据句子（evidence sentence），这使得任务更具挑战性。
- **核心问题**：现有 DocRE 方法在聚合提及特征构建实体表示时存在两方面不足：
  1. 未能充分区分不同提及对实体语义表示的**差异化贡献**——池化等聚合操作将同实体提及等权看待，忽略了关键提及的独特语义；
  2. 未能有效区分**证据句中提及的重要性**——已有证据检索方法通常整合实体的全部提及特征，无法集中于真正承载关键信息的提及。
- **关键观察**：实体类型（entity type）能为同类实体提供**一致的语义约束**，并可**隐式排除实体间不可能存在的关系**（如 PER 与 LOC 之间没有 “spouse” 关系）。基于此，论文提出利用实体类型同时引导关键提及识别和证据检索，以改善实体表示质量与证据句筛选精度。

## 2. 方法论

论文提出 **ET-MIER**（Entity Type-guided key Mention Identification and Evidence Retrieval）模型，整体由三部分构成：

### （1）类型特定实体表示（TSER）模块
该模块包含两个子策略：

- **实体类型优化（L_ETO）**：
  - 使用 Xavier 初始化将每个实体类型编码为原型向量 Pτ；
  - 设计对比学习损失，拉大不同类型原型向量之间的区分度，使类型语义更清晰。

- **类型引导的关键提及识别（L_KMI）**：
  - 计算每个提及向量 m_ij 与对应实体类型原型 Pτ 的语义相关性（点积+softmax），得到注意力权重 α_ij，从而识别哪些提及是“关键提及”；
  - 加权融合关键提及，生成类型特定实体嵌入 e_i^τ；
  - 结合现有池化表示（全局信息）与局部上下文嵌入，生成类型感知的上下文实体表示 z_e^τ；
  - 通过一个基于双线性分类器的实体类型识别任务（交叉熵损失）学习选择与实体真实类型最匹配的表示 z′_e。

### （2）类型引导的证据检索（Type-guided Evidence Retrieval）
- 从**全局视角**（基于池化实体注意力的句子重要性分布 q_(h,t)）与**局部视角**（基于类型特定实体表示的句子权重分布 q′）两个层面分别计算句子重要性；
- 通过平衡因子 ε 融合两种分布得到最终句子重要性分布 q̂，并以最小化与真实证据标签分布之间的 KL 散度作为训练目标（L_Evi）。

### （3）关系抽取（Relation Extraction）
- 使用类型特定实体表示 z′_eh、z′_et 作为输入，通过**分组双线性分类器**（K 组）计算每个关系的得分；
- 采用 ATLOP 提出的**自适应阈值损失**（Adaptive Thresholding Loss）进行多标签关系预测（含 NA 类）。

### 联合训练
总损失为：L_All = L_RE + λ1 L_Evi + λ2 L_ETO + λ3 L_KMI。

## 3. 实验设计

### 数据集与基准
- **DocRED**：基于 Wikipedia 与 Wikidata 的人工标注标准 DocRE 数据集，96 个预定义关系、6 类实体类型；
- **Re-DocRED**：通过重新标注修正 DocRED 漏标问题的改进数据集，提供更干净的 dev/test 集；
- 评测指标：**F1** 与 **Ign-F1**。

### 对比方法
- Transformer 基方法：ATLOP、DocuNet、KD-DocRE、EIDER、DREEAM、AA、SRF、VaeDiff-DocRE 等；
- 图基方法：GAIN、SIRE、DocGNRE 等；
- 大语言模型方法：GPT-4o + ICL、EP-RSR、AutoRE 等；
- 消融分析：分别移除 TSER、KMI、ETO、Type-guided EviR（并测试 ε=0 与 ε=1 两种极端情况）。

## 4. 资源与算力

- 论文明确说明使用的硬件为**单张 NVIDIA V100 32GB GPU**；
- 采用的预训练编码器为 BERT_base 与 RoBERTa_large；
- 主要超参数：训练 30 epochs，batch size=4，warmup ratio 为 6e-2；
- **未明确说明**的内容包括：GPU 的数量（推测为单卡，但未逐字确认）、每个实验的平均训练时长、训练总 GPU 小时数以及调参阶段的具体计算开销。

## 5. 实验数量与充分性

论文实验较为**全面充分**，大致包括以下组别：

- **主实验**：在 DocRED 与 Re-DocRED 两个数据集上、使用 BERT_base 和 RoBERTa_large 两种编码器，对比多种强基线，结果具有统计可靠性（多次运行，如 ±0.21、±0.07 等误差范围）；
- **消融实验**：在两种编码器/数据集上对核心模块逐一进行消融；
- **复杂度分析**：对比模型内存占用与可训练参数量（如内存 20.4 GiB，参数 115.4M）；
- **实体表示方法横向对比**：与 LogSumExp 池化、Relation-Specific 两种表示方式对比；
- **可迁移性/插件泛化分析**：将 TSER 作为即插即用模块分别集成到 ATLOP、AA、DREEAM 三个基线上验证提升效果；
- **弱监督跨数据集泛化实验**：用 DocRED 训练、直接迁移测试到 Re-DocRED；
- **超参数敏感性分析**（附录）：考察 ε 与 λ3 的选择对性能的影响；
- **案例研究**（附录）：结合具体实例定性分析各模块的作用。

总体而言实验数量丰富，涵盖了 benchmark 性能、模块有效性、效率、泛化性与可迁移性等关键维度；且多次运行汇报平均结果与标准差，提升了客观性。不足之处在于跨领域场景和真实噪声标注上的定量分析较少（论文仅在 Limitations 中进行了定性讨论）。

## 6. 主要结论与发现

- **性能显著领先**：ET-MIER 在 Re-DocRED 测试集上使用 RoBERTa_large 达到 Ign-F1 80.83、F1 81.41，相比 ATLOP 分别提升 3.89 和 3.68 个点，也大幅超越同期最强 LLM 方法（EP-RSR，高出约 +17 F1）；在 DocRED 上同样取得领先。
- **实体类型指导是关键要素**：消融与冻结实验表明，类型原型向量需在训练中动态更新（而非固定初始化）——冻结类型表示导致性能下降，证明学习到的类型语义对关键提及识别具有积极作用。
- **关键提及识别有效**：去除 KMI 损失后两个数据集上的指标均明显下降，证明区分提及贡献是提升实体表示质量的有效途径。
- **类型引导证据检索有效**：单纯使用池化特征（ε=0）或仅用类型特征（ε=1）的效果均不如两者融合，说明**全局语境**与**局部类型语义**具有互补性。
- **TSER 具有良好的可移植性**：将其作为插件集成到 ATLOP、AA、DREEAM 时均能带来稳定提升，验证了该模块的通用性。
- **效率与性能兼顾**：参数总量（115.4M）与 ATLOP 持平，明显低于 RSMAN/AA 等方法，在取得更高 F1 的同时保持了较低的内存开销。
- **泛化能力强**：弱监督迁移场景（DocRED 训练 → Re-DocRED 测试）下，ET-MIER 的 F1（59.94）远超 GPT-4o + ICL（27.14），表明轻量级架构在跨域场景中的鲁棒性优于大模型方法。

## 7. 优点

- **问题切入点新颖**：首次系统性地将实体类型引入 DocRE 的提及加权与证据选择过程，指出实体类型不仅能筛选关系类型，还能提升实体表示的细粒度质量，视角独到；
- **多粒度信息融合设计**：证据检索中同时引入全局（池化注意力）与局部（类型特定注意力）视角，方法设计合理、有理论依据；
- **损失函数层次清晰**：L_KMI、L_ETO、L_Evi 三个辅助信号分别引导表示学习、类型空间优化与证据选择，与主目标 L_RE 相互配合，没有引入过于复杂的外部结构；
- **实验扎实、具有说服力**：除标准 benchmark 外还包含插件泛化、跨数据集弱监督迁移、复杂度对比与案例分析，覆盖面广；
- **可复现性与开放性**：公开代码库，参数设置和超参分析较详尽；
- **公平性好**：在公开数据集上与多种基线对比，并报告多次运行均值与方差，结果的统计可信度较高。

## 8. 不足与局限

- **依赖实体类型标注质量**（论文自述）：若训练/测试数据中实体类型存在缺失、错误或不一致，噪声会经由类型引导机制传播到关系推理过程，影响最终性能；
- **跨域适应能力受限**（论文自述）：在实体类型体系差异较大的跨领域场景下，类型引导的提及选择与证据过滤策略可能难以泛化；
- **实验覆盖范围仍较窄**：仅在 DocRED/Re-DocRED 两个数据集上验证，未在 TACRED 以外的语料（如法律或生物医学领域 DocRE 数据）上测试，限制了结论的外部推广性；
- **模型在弱标注数据下需依赖类型预测**：尽管模型能在一定程度上自行预测类型，但这种预测本质上训练自人工标注，可能形成对标注规范的隐式过拟合；
- **大模型对比方式有限**：与 LLM 方法比较多直接用下游任务分数进行比对，未讨论与 RAG 类或更大上下文建模方法的系统性差异；
- **算力细节披露不够透明**：缺失训练时长和GPU总开销等信息，难以精确评估在更大数据集上的扩展成本。

（完）
