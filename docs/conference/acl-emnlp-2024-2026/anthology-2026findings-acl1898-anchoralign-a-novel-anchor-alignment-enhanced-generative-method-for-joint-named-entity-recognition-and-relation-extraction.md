---
title: "AnchorAlign: A Novel Anchor Alignment-enhanced Generative Method for Joint Named Entity Recognition and Relation Extraction"
title_zh: AnchorAlign：通过锚点对齐增强的联合命名实体识别和关系抽取生成式方法
authors: "Xiaolong Weng, Yuanyun Zhou, Boyu Qiu, Zehua Wang, Ying Xiong, Buzhou Tang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1898.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 以锚点对齐机制改进实体与关系的联合抽取，提升跨结构一致性
tldr: 现有生成式联合NER与关系抽取常出现实体与关系错配、关系内部相互错配的问题。作者提出AnchorAlign，先通过锚点实体选择机制识别关键实体，再以锚点对齐增强生成过程，使实体与关系以及关系之间在结构上对齐。实验表明该方法能有效缓解各类对齐错误，提高联合抽取的准确率和一致性，为跨句和篇章级关系抽取中的结构化输出提供了可借鉴的生成式对齐思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1898/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1898/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 981, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1898/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1656, \"height\": 999, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1898/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 665, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1898/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 660, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1898/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 665, \"height\": 440, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1898/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1612, \"height\": 811, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1898/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1898/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1898/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 152, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1898/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1898/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1898/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 803, \"height\": 503, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1898/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1663, \"height\": 416, \"label\": \"Table\"}]"
motivation: 生成式联合抽取中实体-关系错配和关系-关系错配削弱输出一致性。
method: 提出锚点实体选择并在生成过程中增强锚点对齐，联合优化NER和关系抽取。
result: 实验结果显示AnchorAlign可有效缓解对齐错误，提升联合抽取性能。
conclusion: 锚点对齐为生成式多任务信息抽取提供了提升结构一致性的有效机制。
---

## Abstract
Named Entity Recognition (NER) and Relation Extraction (RE) are two fundamental and interdependent tasks in information extraction (IE), aiming to identify entities and relations from unstructured text. Recently, generative methods have become mainstream instead of discriminative methods for IE, especially joint multi-task IE, due to their promising performance and flexibility. For joint NER and RE, existing methods suffer from misalignment between entities and relations, as well as misalignment among relations. To address these issues, we propose AnchorAlign, a novel generative method enhanced by anchor alignment. Specifically, we first introduce an anchor entity selection mechanism to identify key entities in the text as anchor points, which serve as semantic pivots to bridge the two tasks. Then, we design a dual-level anchor alignment module: at the semantic level, we construct a cross-task semantic alignment space to align the semantic representations of anchor entities and their associated relations; at the generation level, we introduce an anchor-guided generation constraint to guide the model to generate entities and relations with strict alignment based on the anchor points. Extensive experiments on five benchmark datasets show that AnchorAlign outperforms state-of-the-art baselines, demonstrating its effectiveness. Our work provides a new perspective for optimizing the joint modeling of NER and RE, and has potential to be extended to more complex multi-task IE such as NER and Event Extraction (EE).

---

## 论文详细总结（自动生成）

## 一、论文核心问题与整体含义

**研究背景与核心问题：**
- 在信息抽取（IE）中，命名实体识别（NER）和关系抽取（RE）是两项基础且高度关联的任务。
- 近年来，生成式方法凭借其灵活性和优秀的性能，逐渐取代判别式方法，成为联合多任务 IE（尤其是 NER 与 RE）的主流技术路径。
- 现有生成式联合 NER 与 RE 方法存在两大核心问题：
    - **实体与关系间的错配（misalignment between entities and relations）**：现有对齐机制往往将一个 NER 实体仅对齐到 RE 中最近的一个实体，不管该实体在多个关系中出现，容易引入系统性偏差。
    - **关系之间的关系错配（misalignment among relations）**：缺乏对 RE 任务**内部依赖关系**（如共享同一实体的多个关系之间的结构一致性）的建模。
- 此外，现有研究虽提出多种结构化输出范式，但缺少对这些范式的系统性比较与统一。

**核心含义：**
论文主张通过在 NER 与 RE、RE 与 RE 之间建立显式的"锚点"（anchor）对齐结构，从而提升生成式联合抽取中输出结构的一致性和准确性，为联合建模提供一种新的统一视角和解决方案。

---

## 二、论文方法论

论文提出 **AnchorAlign**，一套基于锚点对齐增强的生成式联合 NER 与 RE 框架，主要包含以下核心组件：

### 1. 锚点实体选择机制（Anchor Entity Selection）
- 将 NER 与 RE 之间共享的实体定义为 **entity-relation anchor**（实体-关系锚点）；被多个关系共享的实体定义为 **relation-relation anchor**（关系-关系锚点）。
- 锚点实体充当两个任务以及多个关系之间的语义枢纽，为后续结构对齐提供基础。

### 2. 输出范式设计（Output Paradigm）
- 初始化标签 token：通过标签文本嵌入的均值池化初始化特殊 token 向量。
- 采用两个专业解码器：
    - **NER Decoder**：线性化输出实体列表，每个实体由其 mention（+类型 token）构成。
    - **RE Decoder（前向）**：采用**以主语为中心的因子化格式**，同一主语的所有关系（object-relation 对）被归入一个块中生成。
    - **RE Decoder（反向）**：采用以宾语为中心的对偶格式。
- 该设计同时优化生成效率，并保证关系间锚点对齐（relation-relation alignment）。

### 3. 跨任务语义对齐（Cross-task Semantic Alignment）
本节包含两部分，并在概率空间而非特征空间中强制对齐：

- **正向对齐（Positive Alignment）：**
    - **NER-RE 对齐**：将 NER 解码器的输出视为高置信"教师"信号，通过 KL 散度（D_KL）约束前向和反向 RE 解码器在共享锚点实体上的预测分布与 NER 对齐。总损失取前向/反向两者的平均：
      > L_NER-RE = ½ (L_NER,fwd-RE + L_NER,rev-RE)

    - **前向-反向 RE 对齐**：将共享的三元组 τ（含主语、关系类型、宾语）作为对齐锚点，引入**对称 KL 散度**约束前向与反向 RE 解码器的预测分布一致性：
      > L_RE-Align = (1/|T|) Σ D^sym_KL(p_fwd(τ) ∥ p_rev(τ))

- **负向抑制（Negative Suppression）：**
    - 将受限词表中所有非金标 token 视为负集 N，在训练中惩罚其对负集的概率质量贡献：
      > L_suppress = -1/T Σ (1/|N|) Σ log(1 - p(v|h_t))
    - 从而锐化预测分布，防止非目标 token 的生成。

### 4. 整体训练目标
将各解码器交叉熵损失（L_Gen）与辅助对齐/抑制损失加权求和：

> L = L_Gen + α·L_NER-RE + β·L_RE-Align + γ·L_suppress

### 5. 锚点引导的生成约束（Anchor-guided Generation Constraint，推理阶段）
- 双向解码器的输出并集构成候选三元组池。
- 以 NER 输出为标准：**凡是三元组中实体 mention 未被 NER 识别的，判定为低置信并过滤舍弃**。
- 这一策略在保留召回增益的同时可有效控制误报（false positives）。

### 6. 两阶段训练框架
- **任务自适应预训练**：
  - 借助 DeepSeek-V3 进行数据增强（包含实体改写与上下文改写，并采用索引一致性约束的高质量伪标注），构建最大 10,000 条的增强语料。
  - 两段式预训练：先进行实体类型理解（mask 实体提及），再进行渐进式目标激活（先生成目标，再激活语义对齐目标）。
- **监督微调（SFT）**：
  - 基于三元组密度对训练集划分难易样本，先进行"课程热身"训练（只使用简单样本和生成目标），之后转为全量数据训练并采用渐进式目标激活协议。

---

## 三、实验设计与基准

### 数据集（五个基准数据集）
- **ACE05**：新闻语料，实体/关系抽取广泛基准。
- **Sci-ERC**：科学论文语料，含嵌套实体与重叠关系。
- **ADE**：药物不良反应医疗报告语料（采用 10 折交叉验证）。
- **NYT**：远程监督大规模新闻语料，多标签关系。
- **Text2DT**：中文医学文本决策树抽取语料。

### 评价指标
- **Relation Strict F1**：要求主语、宾语实体的 mention 与类型及关系类型全部正确。
- **Relation Boundary F1**：要求实体的 mention 与关系类型正确，不检查实体类型。

### 对比基线
- **生成式基线**：UIE、REBEL、InstructUIE、YAYI-UIE、KnowCoder。
- **判别式基线**：BiSPN、PL-Marker、USM。

---

## 四、资源与算力

论文中**未明确说明所使用 GPU 型号、数量以及训练时长**等具体算力信息。
仅在实验部分提及推理效率测试环境为单卡 GPU（batch size = 40）下的推理时间与吞吐量对比。因此无法从论文中确认完整算力投入规模。

---

## 五、实验数量与充分性分析

### 实验组数统计
论文整体实验较为丰富，涵盖以下若干维度：

1. **主实验（Main Results，Table 1）**：在 5 个数据集上对比 8+ 个基线模型，报告 Strict 与 Boundary 两类 F1。
2. **输出范式比较（Table 6）**：在 ACE05、SciERC、ADE 上比较 4 种输出范式组合。
3. **共享实体密度分析（Table 7）**：分析样本级与实体级共享密度与范式性能增益间的相关性。
4. **消融实验（Table 2）**：在 ACE05 上逐项删除训练侧组件（预训练、语义对齐、NER-RE 对齐、正反向 RE 对齐、负抑制）与推理侧策略（生成约束、解码器聚合），共 8 项消融。
5. **复杂结构分析（Table 3）**：在 SciERC 全量测试集、嵌套实体子集（17 句）、重叠关系子集（224 句）上对比基线，共 6 组数据。
6. **推理效率比较（Table 4）**：参数量、推理时延、吞吐量对比。
7. **案例研究（Figure 3）**：Text2DT 与 SciERC 两个代表案例的成功与失败模式分析。
8. **附录：语义对齐损失可视化（w/ vs w/o）**，验证对齐机制在训练/验证/测试集的泛化效果。

### 充分性评估
- **优点**：主实验覆盖 5 个数据集、多个难易不同的领域；消融实验区分训练侧与推理侧，归属明确；复杂结构专项分析增强了论证深度；共享实体密度分析为范式设计合理性提供了归因证据，具有较强的说服力。
- **不足**：
    - NYT 与 Text2DT 仅报告 Boundary F1，缺乏 Strict F1 的全维度比较。
    - ADE 使用 10 折交叉验证，与其它数据集使用固定划分的评估口径不同，严格可比性稍有欠缺。
    - 消融实验仅基于 ACE05 单一数据集完成，缺少在 SciERC（含重叠关系与嵌套实体）等多结构数据集上的消融验证。

---

## 六、主要结论与发现

1. **性能提升显著**：AnchorAlign 在 SciERC 和 ADE 的 Relation Strict F1 上取得新 SOTA（分别提升 +0.61% 和 +0.14%），在 Relation Boundary F1 上于 ACE05、SciERC、ADE、Text2DT 四个数据集上取得新 SOTA（分别 +0.72%、+1.00%、+0.88%、+0.12%）。
2. **语义对齐是关键**：完整去除语义对齐导致最大性能跌幅（−2.00%）；其中 NER-RE 对齐贡献最大（−1.48%），证实了跨任务对齐的核心地位。
3. **聚合与过滤相互补充**：前向/反向 RE 解码器的聚合（召回增益，−1.66%）与锚点引导的生成约束（精度滤噪，−1.72%）从不同方向改进性能，两策略叠加带来最大增益（去除后 −2.72%）。
4. **复杂结构显著受益**：在 SciERC 重叠关系子集中，AnchorAlign 较基线提升 +2.64% RE Strict F1，验证了锚点对齐对关系内部结构冲突的缓解作用。
5. **预训练贡献明确**：去除任务自适应预训练造成 −1.17% 下降，说明预训练有效注入结构化输出先验。
6. **局限**：结构对齐并不能完全弥补模型内在领域知识的不足——在 Text2DT 案例中仍出现关系方向反转、实体封装等推理缺陷。

---

## 七、方法论的优点与亮点

- **统一视角创新**：用"锚点实体"统一了以往分散的输出范式，并推导出两种新范式（实体分组式关系输出），填补了范式统一比较的空白。
- **兼顾任务间与任务内对齐**：同时建模 NER-RE（跨任务）与 RE-RE（任务内）依赖，突破了现有方法只关注任务间对齐的局限。
- **概率空间对齐思路新颖**：相较常见特征空间的对齐方法，在输出概率空间约束决策级一致性，实现简单且能弥合不同解码器的表征差异。
- **对称双向 RE 解码设计**：用前向与反向两个解码器互为校正，再通过锚点约束合并，有效缓解了生成顺序带来的偏差。
- **正负双向约束**：不仅通过正对齐拉近目标分布，还引入负抑制锐化预测分布，显著提升区分度。
- **推理期无额外成本的约束过滤**：仅利用 NER 预测对 RE 候选做集校验，以极小代价获得大幅精度提升。
- **两阶段训练与课程学习**：预训练增强泛化、SFT 分难易样本推进，训练策略细化且与目标一致。

---

## 八、不足与局限

### 方法层面的局限
- **无法修复实体语义正确性问题**：语义对齐可有效锐化实体边界、促使关系论元正确分配，但无法纠正被错误识别的实体本身的语义属性，改善了一致性未能覆盖"实体封装错误"等歧义。
- **无法弥补领域知识不足**：如 Text2DT 案例所示，实体边界即使被正确识别，关系类型判断与方向性仍可能出现偏差（如头尾倒置），结构约束不能替代复杂推理所需的领域知识。
- **多任务多样化不足**：论文实验聚焦 NER 与 RE，对事件抽取等更复杂任务的适用性仅为展望性提及，并未实证。

### 实验与评估层面的局限
- **算力信息缺失**：未报告 GPU 型号、训练时长、显存占用等资源信息，可复现成本不够透明。
- **推理效率天然劣势**：基础模型使用 BART-Large（914M 参数），推理吞吐量远低于判别式基线（9.51 vs 21.92/41.21 samples/s），在工业实时场景中可能受限。
- **消融实验范围有限**：仅 ACE05 一个数据集上做消融验证，数据集间的结论一致性未知。
- **单一语种主导**：五个数据集多为英文（Text2DT 为中文），跨语言适用性未考虑。

---

（完）
