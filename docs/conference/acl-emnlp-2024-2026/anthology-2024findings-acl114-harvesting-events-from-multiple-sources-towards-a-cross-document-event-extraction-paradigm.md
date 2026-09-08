---
title: "Harvesting Events from Multiple Sources: Towards a Cross-Document Event Extraction Paradigm"
title_zh: 从多源信息获取事件：迈向跨文档事件抽取范式
authors: "Qiang Gao, Zixiang Meng, Bobo Li, Jun Zhou, Fei Li, Chong Teng, Donghong Ji"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.114.pdf"
tags: ["query:evidence-qa"]
score: 7.0
evidence: "提出跨文档事件抽取与CLES数据集，超过70%的指称级事件需要跨文档整合"
tldr: "针对单文档事件信息有限、论元角色易受信息源影响的问题，提出跨文档事件抽取任务并构建CLES数据集，包含20059篇文档和37688个指称级事件，超过70%需跨文档整合。方法以文档间事件信息融合为目标，为多来源与长文档场景下的完整事件抽取提供了数据和方法基础。"
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl114/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl114/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl114/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 701, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 821, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 675, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 648, \"height\": 567, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 827, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1649, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1648, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 996, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1654, \"height\": 877, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1654, \"height\": 875, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1651, \"height\": 840, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1651, \"height\": 762, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl114/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1642, \"height\": 1085, \"label\": \"Table\"}]"
motivation: 单篇文档的事件信息有限，且不同信息源会让事件论元角色产生偏差，导致事件视角不完整。
method: 提出跨文档事件抽取任务，构建CLES数据集，并设计方法将多个文档中的事件提及与论元融合成完整事件。
result: "CLES包含20059篇文档和37688个指称级事件，其中超过70%为跨文档事件，证实任务设定的必要性与挑战。"
conclusion: 为跨文档事件抽取提供数据和方法基础，可用于对多来源长文档进行结构化事件理解。
---

## Abstract
Document-level event extraction aims to extract structured event information from unstructured text. However, a single document often contains limited event information and the roles of different event arguments may be biased due to the influence of the information source.This paper addresses the limitations of traditional document-level event extraction by proposing the task of cross-document event extraction (CDEE) to integrate event information from multiple documents and provide a comprehensive perspective on events. We construct a novel cross-document event extraction dataset, namely CLES, which contains 20,059 documents and 37,688 mention-level events, where over 70% of them are cross-document. To address the task, we propose a CDEE pipeline that includes 5 steps, namely event extraction, coreference resolution, entity normalization, role normalization and entity-role resolution. Our CDEE pipeline achieves about 72% F1 in end-to-end cross-document event extraction, suggesting the challenge of this task and setting up a benchmark for future research. Our work builds a new line of information extraction research and will attract new research attention.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与研究动机

- **背景局限**：传统的文档级事件抽取（Document-level Event Extraction, DEE）仅从单篇文档中提取结构化事件信息。然而单篇文档包含的事件信息往往有限，且不同来源的文档可能对同一事件提供不同视角或侧重点，导致局部信息的碎片化与偏差。
- **核心问题**：如何整合多篇文档中分散的事件提及与论元，形成完整、统一的事件视图，以解决事件信息“完整性”问题。
- **任务提出**：作者首次提出**跨文档事件抽取（Cross-Document Event Extraction, CDEE）**任务，将事件划分为：
  - **mention-level 事件**：单个文档内定义的事件；
  - **concept-level 事件**：通过整合多个文档获得的事件完整表示。
- **核心问题来源**（TL;DR）：不同文档的事件信息互补，但传统 DEE 无法跨文档合并、去重与消解冲突，导致事件视图不完整；且跨文档信息抽取领域缺乏事件抽取相关研究。

### 2. 方法论：CDEE 流水线

论文提出五步流水线框架（对应附图 Figure 3），核心思想是“先抽取、再对齐、后整合”：

1. **文档级事件抽取（DEE）**
   - 采用基于 Doc2EDAG 风格的实体有向无环图（EDAG）方法；
   - 实体提取使用 BERT + CRF；
   - 引入**篇章结构信息（RST 树）**，结合 Transformer 编码器与 GAT（图注意力网络）进行文档级编码；
   - 支持事件类型分类与事件论元角色抽取两个子任务。

2. **事件共指消解（Coreference Resolution）**
   - 在同一文档集合内判断两个事件提及是否指向同一真实事件；
   - 基于 RST 增强的事件表示，训练多层 MLP 进行二分类，概率公式为：p = MLP(mi, mj, mi·mj)。

3. **实体归一化（Entity Normalization）**
   - 借助 HarvestText 工具进行实体链接（entity linking）到知识库；
   - 统一实体表述，如将“United States”与“USA”归为同一实体，并标准化日期、地名等属性格式。

4. **角色归一化（Role Normalization）**
   - 手工构建角色映射字典，将不同文档中表述不同但含义相同的论元角色（如“winner”与“victors”）统一为规范表示；
   - 数据集共包含 469 种唯一角色。

5. **实体-角色消解（Entity-Role Resolution）**
   - 用于跨文档信息的**去重**与**冲突消解**；
   - 冲突消解策略：
     - 时间/地点论元冲突：选取跨文档中出现频率最高的值；
     - 同一实体被赋予多个角色：基于手工构建的五级角色层次结构（Role Hierarchy），选取层级最高角色作为最终结果。

### 3. 实验设计

- **数据集**：
  - 新构建的 **CLES（CrossLinkEventScope）** 数据集（中文，源自 Wikipedia）；
  - 共 20,059 篇文档，37,688 个 mention-level 事件，4,476 个 concept-level 事件；
  - 其中跨文档事件占比超过 70%（训练 71.2% / 验证 71.7% / 测试 76.5%）；
  - 覆盖 9 种事件类型，含攻击、体育、选举、灾害、事故、奖项等，呈长尾分布；
  - 每个文档集合至多 10 篇文档。
- **三组主要实验**（对应流水线的三个核心模块）：
  1. **文档级事件抽取实验**（验证引入 RST 的效果）
     - 对比方法：Doc2EDAG（Zheng et al., 2019）、RAAT（Liang et al., 2022）；
     - 指标：R、P、F1；
     - 结果：事件角色提取 F1 分别领先 Doc2EDAG 4.6 个点、与 RAAT 接近。
  2. **事件共指消解实验**
     - 对比方法：Yu et al. (2022)；
     - 指标：MUC、B³、CEAF、CoNLL；
     - 结果：在所有指标上均优于基线，CoNLL F1 达 82.1。
  3. **端到端跨文档事件抽取实验**
     - 对比方法：
       1. 规则基线（基于字典匹配与最大频次原则）；
       2. 本文流水线框架；
       3. **Llama2-Chinese-7b-Chat**（LoRA/全参数微调，4×A100-80G）。
     - 指标：R、P、F1；
     - 结果：流水线 F1 72.6%（优于规则基线的 69.7%）；LLM 达到 79.1%。
- **评测说明**：LLM 实验的评测口径较宽松（预测结果只要包含于 gold 标注即判定正确），与流水线模型的严格匹配不完全可比。

### 4. 资源与算力

- 论文**仅**在 5.4 节清晰说明 LLM 微调实验使用 **4 张 A100-80G GPU**，学习率设为 2e-6，batch size 设为 8；
- **未明确说明**：其他非 LLM 模块（如文档级事件抽取、共指模型）使用的 GPU 型号/数量、总训练时长、参数量与计算量等细节，论文中并未披露。

### 5. 实验数量与充分性评估

- **实验组数**：3 组模块化主实验 + 1 组 LLM 补充实验。
- **充分性评价**：
  - **优点**：实验与流水线结构一一对应，能够独立验证每一模块的效果，且端到端实验能反映整体性能，思路清晰；
  - **不足**：
    - **缺少系统性消融实验**：未逐一剔除/替换各模块以量化每个归一化或消解步骤的边际贡献；
    - **对比基线较少**：跨文档事件抽取尚无前人工作，规则基线较简单，流水线方法的优势说服力有限；LLM 实验仅用单一模型、单一 prompt 与较宽松的评测口径，对比不够全面；
    - **评测口径不一**：LLM 采用“包含即正确”的宽松匹配，与基于精确/部分匹配的流水线评估并不完全公平，结论的客观性受限；
    - 缺少跨语言/跨领域泛化评估（仅在中文 Wikipedia 一个场景上测试）。

### 6. 主要结论与发现

- 单文档视角不足以覆盖事件全貌，需要跨文档事件抽取来完成事件信息的聚合。
- CLES 数据集中超过 70% 的事件都涉及跨文档整合，说明该任务的必要性和挑战性。
- 提出的 CDEE 流水线（RST 增强文档建模 + 显式共指消解 + 实体/角色归一化 + 冲突消解）端到端取得约 72% F1，远未饱和。
- 引入篇章结构（RST）与实体关系的模型均能有效提升文档级事件抽取表现。
- 通用大语言模型（Llama2-Chinese-7b）经微调后在此任务上表现较强（约 79% F1），但存在过拟合、输出格式不稳定及 prompt 敏感等问题。

### 7. 优点

- **任务新颖性高**：首次系统性地定义并形式化“跨文档事件抽取”任务，填补了事件抽取研究的一个空白。
- **数据集规模大且真实**：CLES 基于 Wikipedia 超链接网络聚合文档，包含大量真实、多来源的跨文档事件，为后续研究提供了良好底座；数据统计全面（触发词、角色分布、文档集合规模等均有分析），并报告了标注一致性（Kappa ≈ 0.72）。
- **方法结构化、可解释性强**：五步流水线的模块划分清晰，每一步针对明确问题（抽取、聚合、归一化、去重、冲突消解），便于逐步分析和后续改进；在该任务尚无现成方法的背景下率先提供了一个可复用的基准。
- **构造了角色层次体系**：用五级角色优先级解决不同文档对同一实体指派不同角色时的冲突问题，具有较强的语义合理性。
- **初步探索了 LLM 在该任务上的能力**，为后续研究提供参考。

### 8. 不足与局限

- **框架模块尚不成熟**（作者自述为“first attempt”，各模块实现远非最优，存在错误传播的累积风险）。
- **数据集层面**：
  - 仅覆盖 9 个粗粒度事件类型且类型分布严重不均衡（攻击类事件占绝对多数）；
  - 仅基于中文 Wikipedia 一个来源，领域与时段的覆盖具有内在偏差；
  - 文档集合构建依赖超链接网络质量，可能引入系统性噪声；
  - 高比例的跨文档事件与长尾角色分布也给后续模型泛化带来挑战。
- **实验层面**：
  - 缺少详细的消融实验，难以具体衡量每个模块的真正贡献；
  - 与 LLM 对比存在评估口径不一致的问题（LLM 采用宽松匹配，流水线采用严格/候选匹配），公平性受限；
  - 未开展跨数据集/跨语言的一般化验证。
- **计算资源披露不充分**：只报告了 LLM 微调所用 GPU 型号和数量，未说明其他模型的资源开销、训练时长与总代价。
- **应用限制**：中文 Wikipedia 社区的事件覆盖偏向攻击、体育、选举等特定类型，将该数据集和方法迁移到新闻、社交媒体、金融等实时多源场景时，需要谨慎考虑事件类型分布、语言适用性以及噪声信息源的差异。

（完）
