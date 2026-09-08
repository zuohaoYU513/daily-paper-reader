---
title: Consistent Document-level Relation Extraction via Counterfactuals
title_zh: 基于反事实实现一致性文档级关系抽取
authors: "Ali Modarressi, Abdullatif Köksal, Hinrich Schütze"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.findings-emnlp.672.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 文档级关系抽取，跨越句子边界建模实体关系并通过反事实生成提升一致性
tldr: 文档级关系抽取常用真实数据训练，模型会因实体表面形式等虚假信号产生不一致预测。作者提出CovEReD反事实生成方法，通过替换实体构造反事实文档，用于诊断并缓解偏差。实验显示模型能抽取事实数据中的三元组，但在反事实改写后无法抽取相同关系，表现出依赖特定实体与外部知识。这项工作为构建更可信的文档级关系抽取提供了反事实评测与训练手段。
source: EMNLP-2024-Findings
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-findings/anthology-2024findings-emnlp672/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 240, \"label\": \"Table\"}]"
motivation: 真实数据训练的文档级关系抽取模型偏好用实体名称等表面线索，面对反事实变化时会产生不一致的抽取结果。
method: 提出CovEReD反事实数据生成方法，利用实体替换构造反事实文档，以评测和缓解模型的事实偏差与不一致行为。
result: 实验揭示模型能从事实数据准确抽取关系三元组，但对实体替换后的反事实数据无法抽取同一关系，说明其依赖虚假信号。
conclusion: 反事实数据生成可用于诊断并缓解文档级关系抽取模型的实体依赖，为提升跨句子关系抽取的鲁棒性和一致性提供新途径。
---

## Abstract
Many datasets have been developed to train and evaluate document-level relation extraction (RE) models. Most of these are constructed using real-world data. It has been shown that RE models trained on real-world data suffer from factual biases. To evaluate and address this issue, we present CovEReD, a counterfactual data generation approach for document-level relation extraction datasets using entity replacement. We first demonstrate that models trained on factual data exhibit inconsistent behavior: while they accurately extract triples from factual data, they fail to extract the same triples after counterfactual modification. This inconsistency suggests that models trained on factual data rely on spurious signals such as specific entities and external knowledge – rather than on context – to extract triples. We show that by generating document-level counterfactual data with CovEReD and training models on them, consistency is maintained with minimal impact on RE performance. We release our CovEReD pipeline as well as Re-DocRED-CF, a dataset of counterfactual RE documents, to assist in evaluating and addressing inconsistency in document-level RE.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 一、核心问题与研究动机

- **研究对象**：文档级关系抽取（Document-level Relation Extraction, DocRE），即从多句子文档中抽取实体间的语义关系三元组。
- **核心问题**：现有 DocRE 模型在真实世界数据（如 Wikipedia）上训练时，往往依赖**实体表面形式**和**参数化记忆中的外部先验知识**等虚假信号（spurious signals），而非真正从输入上下文进行推理。
- **关键发现/动机**：
  - 模型能从**事实性数据**中准确抽取三元组；
  - 但当相同语境经过**反事实替换**（保持关系不变，仅更换实体）后，模型却无法抽取对应三元组；
  - 这种不一致性（inconsistency）揭示了模型强烈依赖实体偏差（entity bias）和事实偏差（factual bias），对文档实际语义的利用不足。
- **已有工作局限**：此类反事实研究此前主要集中在**句子级**RE（如 ENTRE 改造 TACRED）；文档级 RE 涉及跨句关系、多实体提及和实体参与多三元组等更复杂情形，此前缺乏相应的反事实评测与训练手段。
- **总体意义**：一个真正具备上下文理解能力的 DocRE 模型应当在反事实改写后依然保持一致的预测行为；若做不到，说明模型"知其然不知其所以然"。

## 二、方法论

### 2.1 核心思想

- 提出 **CovEReD**（Counterfactual data generation for document-level RE）：一种通过**实体替换**构造反事实文档的流水线，用于生成不依赖真实世界事实、但保留了原文档结构与关系语义的文档级 RE 数据。
- 核心原则：替换不是随机的，而是**选择与原实体"可类比"的新实体**——即与原文实体在类型、关系图谱、上下文语境上相似，但实际对应一个不同的事实主体。

### 2.2 技术流程（三步）

1. **实体提及清理（Entity mention cleanup）**
   - 合并完全同名的实体提及集合；
   - 去除同一句子中有重叠的较短提及（如保留 "Great Britain" 而去掉 "Britain"）。

2. **候选实体收集（Gathering entity candidates）**
   - 基于整个种子数据集中的实体池，为每个实体节点寻找合适的替代者；
   - 相似性判断依据两个信号：
     - **关系图相似性（relation map）**：实体在所有三元组中参与的关系类型及头/尾位置；
     - **上下文片段相似性（context snippets）**：每个提及前后 16 个词构成上下文文本，用 Contriever 编码为嵌入，以余弦相似度衡量；
   - 额外条件：要求候选实体**类型一致**、**不来自同一篇文档**、且实体名称嵌入的相似度落在一个区间内（既不能完全相同也不能毫无关联）。

3. **生成反事实文档（Generating counterfactual documents）**
   - 以图遍历/迭代方式，在文档中对实体节点逐一尝试替换；
   - 初始化一个字典，从原始文档出发，对每个尚未替换的实体获取候选替代并执行替换，逐步扩展生成大量反事实变体；
   - 每个实体节点**最多只替换一次**；
   - 最终输出需满足**受影响三元组比例 τr** 的阈值筛选（实验中 τr=0.7，即至少 70% 的三元组因替换而被改变）。

### 2.3 算法伪代码要点

- **Algorithm 1（生成器）**：维护 `EditTuple` 记录已替换节点；对字典中的每个文档/替换记录，遍历所有实体节点，对未替换节点调用 `GET_ALTS` 获取候选并替换；最后过滤 `AFFECT_R > τr` 的文档。
- **Algorithm 2（候选搜索）**：针对目标节点 ei，遍历候选池，按关系映射重叠度（rsim > 0）、不同文档、类型重叠三个条件初筛；在提及相似度和上下文相似度上设定双阈值 τe[MAX]=0.8、τe[MIN]=0.2、τc=0.4；排序后丢弃互为子集的候选提及集合。

## 三、实验设计

### 3.1 数据集与场景

- **种子数据**：Re-DocRED（Tan et al., 2022b）——基于 Wikipedia 的事实性文档级 RE 数据集；
- **生成数据**：Re-DocRED-CF——由 CovEReD 对 Re-DocRED 进行反事实改造得到；
  - 对 Re-DocRED train 运行 CovEReD **5 次**，得到 5 个子集作为 Re-DocRED-CF train；
  - 对 Re-DocRED test 运行 **1 次**，得到 Re-DocRED-CF test；
  - 超参数设置：τe[MAX]=0.8，τe[MIN]=0.2，τc=0.4，MN=3，τr=0.7。
- **Benchmark 数据集**：Re-DocRED 测试集（事实性数据）及其对应反事实版本 Re-DocRED-CF test（评估一致性）。

### 3.2 模型与训练设置

- **模型框架**：KD-DocRE（Tan et al., 2022a），采用轴向注意力（axial attention）+ 自适应焦点损失（adaptive focal loss）；
- 为隔离反事实数据的效应，**不使用知识蒸馏**，只做第一阶段的 human-annotated data 训练；
- 预训练模型：RoBERTa-large（Liu et al., 2019）；
- 超参数遵循原 KD-DocRE 设定；
- 所有报告数字为 **5 个随机种子实验的中位数**。

### 3.3 对比条件（三种训练数据设置）

| 训练数据 | 目的 |
|---|---|
| 仅 Re-DocRED（事实数据） | 基线，评测在事实数据上的表现与一致性 |
| 仅 Re-DocRED-CF（反事实数据） | 评测反事实训练对一致性的贡献及对事实性能的损害 |
| Re-DocRED + Re-DocRED-CF（混合训练） | 同时追求高一致性与高事实性性能（epoch 由 30 减半为 15 以保持总步数一致） |

### 3.4 评估指标

- **标准 RE 指标**：Precision / Recall / F1（在事实性 Re-DocRED test 上）；
- **一致性指标**：CONS（Pairwise consistency，引自 Paranjape et al., 2022）——模型在**事实数据上预测正确**的那些三元组，在对应反事实版本上依然预测正确的比例。

### 3.5 人工评估

- 随机选取测试集中 50 个三元组样例进行人工判断；
- 结果：45/50 被判定合理（90%），说明 CovEReD 生成的反事实案例大多为可信的、语义连贯的反事实改写。

## 四、资源与算力

- 论文**未明确报告**具体的 GPU 型号、GPU 数量、单次训练时长或总体算力开销。
- 仅可知其基于 RoBERTa-large 微调，训练了 5 个随机种子模型，每个模型训练约 30 epochs（混合训练为 15 epochs）。
- 反事实数据生成中使用 Contriever 模型获取嵌入，但未说明其推理规模与耗时。

## 五、实验数量与充分性

### 已做实验

1. **三种训练设置对比**（仅事实 / 仅反事实 / 混合），各 5 个随机种子取中位数；
2. **一致性与事实性能联合评测**（在两个版本的测试集上分别报告）；
3. **人工可读性/合理性评估**（50 个随机样本，90% 合理率）；
4. 多个反事实失败案例的可视化展示与定性分析（正文实例 + 附录 3 个补充案例）。

### 充分性评价

- **优点**：三种训练设置构成了较为完整的对照框架，有效分离了"事实数据提供性能"和"反事实数据提供一致性"的贡献；多随机种子取中位数增强了结论稳定性。
- **不足**：
  - 仅用了**一个基础 DocRE 模型**（KD-DocRE），未对比多种架构（如 ATLOP、SSAN、GRLN 等主流 DocRE 模型）；
  - 仅使用**一个种子数据集**（Re-DocRED），未验证方法对 DocRED 或跨领域、跨语言的通用性；
  - 未提供额外消融实验，无法判断 pipeline 各组件（如关系图相似性、上下文相似度、阈值设置）的**相对贡献**；
  - 人工评估样本较少（50 条），未报告人工评估者的信度（如 Cohen's kappa）；
  - 未包含对"事实+反事实"混合比例更细粒度的敏感性分析。

## 六、主要结论与发现

1. **模型存在严重不一致性**：仅在事实数据上训练的 DocRE 模型在一致性指标上仅达到 **68.6%**——超过 30% 的原本正确预测在实体替换为语义相似但非事实的实体后失败。
2. **CovEReD 生成的反事实数据质量高**：人工评估显示 90% 的反事实改写保持语义/语法合理性。
3. **反事实训练能大幅提升一致性**：
   - 仅用反事实数据训练：一致性从 68.6% 提升至 **89.5%**（+20.9pt），但 F1 下降 5.6（72.4 vs 78.0）；
   - 事实 + 反事实**混合训练**：一致性达 **88.3%**（+19.7pt），F1 仅下降 1.7（76.3 vs 78.0），效果最优。
4. **结论**：反事实数据帮助模型学会基于上下文进行推理而非依赖实体表面形式和记忆性知识；同时保留事实数据训练可保证真实应用场景下的性能不显著下降。

## 七、优点

1. **问题视角新颖**：首次将反事实生成系统性地引入**文档级**关系抽取，填补了此前仅停留在句子级（如 ENTRE、CoRE）的研究空白。
2. **方法论巧妙**：
   - 利用"关系地图 + 上下文嵌入 + 类型一致性"三重信号，保证替换实体虽非事实但与语境高度兼容；
   - 采用迭代生成框架，支持一个文档中**多个实体同时替换**且每个实体只替换一次，处理了文档级多提及、实体跨多三元组的问题；
   - 通过替换后受影响三元组比例阈值（τr）确保生成的反事实具有统计区分力。
3. **与真实应用对齐**：选择在文档级评测（而非简化后的句子级），更贴近 DocRE 的真实部署形态。
4. **资源贡献**：公开发布 CovEReD 生成 pipeline 与 Re-DocRED-CF 数据集，为后续研究提供了诊断 DocRE 偏差的标准工具。
5. **训练策略实用**："事实+反事实混合训练仅需减半 epoch 即保持性能"的结果具有很强的工程价值。
6. **案例分析丰富**：文中多张图直观展示了模型在反事实前后预测失败的模式，具有说服力。

## 八、不足与局限

1. **依赖种子 DocRE 数据集**：需要现成的关系标注文档才能生成反事实数据，对**新领域、新语言**的迁移需要额外标注或跨语料库实体对齐策略。
2. **模型覆盖窄**：只在 KD-DocRE 一种框架上验证结果；未测试其他类型模型（如基于结构建模、基于生成式大语言模型的方法），结论的普遍性有待验证。
3. **性能仍有代价**：即使是混合训练，F1 也从 78.0 降至 76.3，说明反事实训练并非完全无损，需在真实效率/性能与鲁棒性间权衡。
4. **一致性与事实性并非"以上下文为中心"的充分证据**：模型的一致性提升也可能是学到了某种新的表面启发式，而不是真正深层理解上下文。
5. **阈值设置经验性较强**：如 τr=0.7、MN=3、τe 区间等，未见对超参数敏感性的分析，在其他数据集上的适用性需要调优。
6. **人工评估规模偏小**：50 条样本不足以完整刻画全数据集的复杂错误模式；且明确排除了原本就是错误标注的反事实样本，可能存在一定的评估偏乐观。
7. **未报告算力开销**：缺少模型训练成本、实体嵌入计算与生成 pipeline 运行时间的量化信息，对可复现性和实际部署成本估算造成不便。

---

（完）
