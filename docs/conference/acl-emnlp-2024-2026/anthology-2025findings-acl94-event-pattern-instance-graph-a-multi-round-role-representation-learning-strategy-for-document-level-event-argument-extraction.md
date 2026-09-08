---
title: "Event Pattern-Instance Graph: A Multi-Round Role Representation Learning Strategy for Document-Level Event Argument Extraction"
title_zh: 事件模式-实例图：文档级事件论元抽取的多轮角色表示学习策略
authors: "Qizhi Wan (万齐智), Tao Liu, Changxuan Wan (万常选), Rong Hu, Keli Xiao, Yuxin Shuai"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.94.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 文档级事件论元抽取，构建事件模式-实例图建模角色与论元关系
tldr: 文档级事件论元抽取面临角色语义复杂、论元间相互影响等问题，以往跨度选择策略多依赖预训练模型而缺乏模式与实例的关联建模。作者构建事件模式-实例图，通过多轮角色表示学习同时聚合事件模式角色、实例论元及其直接和间接关系，以增强论元识别。实验验证了该方法能有效利用事件结构信息，提升文档级事件论元抽取的效果。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl94/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1406, \"height\": 663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl94/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1661, \"height\": 896, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl94/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 823, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl94/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 602, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl94/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 646, \"height\": 950, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl94/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1161, \"height\": 844, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl94/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl94/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 570, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl94/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl94/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 812, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl94/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 417, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl94/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl94/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1453, \"height\": 407, \"label\": \"Table\"}]"
motivation: 针对文档级事件论元抽取忽略论元间关联和模式-实例关联的问题，提出多轮角色表示学习。
method: 构建事件模式-实例图，对模式角色、实例论元及其直接与间接关系进行多轮表示学习。
result: 在文档级事件论元抽取任务上验证了图结构关联建模带来的有效性提升。
conclusion: 事件模式与实例的交互建模能够改善长文档事件语义理解和论元预测。
---

## Abstract
For document-level event argument extraction, existing role-based span selection strategies suffer from several limitations: (1) ignoring interrelations among arguments within an event instance; (2) relying on pre-trained language models to capture role semantics at either the event pattern or document, without leveraging pattern-instance associations. To address these limitations, this paper proposes a multi-round role representation learning strategy. First, we construct an event pattern-instance graph (EPIG) to comprehensively capture the role semantics embedded in various direct and indirect associations, including those among roles within event patterns, arguments within event instances, and the alignments between patterns and instances. Second, to enhance the learning of role node representation in the graph, we optimize the update mechanisms for both node and edge representations in the EPIG graph. By leveraging the graph attention network, we iteratively update the representations of role nodes and role edges. The role representations learned from the EPIG are then integrated into the original role representations, further enriching their semantic information. Finally, a role representation memory module and a multi-round learning strategy is proposed to retain and refine role representations learned from previously analyzed documents. This memory mechanism enhances the prediction performance in subsequent rounds of span selection. Extensive experiments on three datasets verify the effectiveness of the model.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机与背景）

文档级事件论元抽取（Document-Level Event Argument Extraction, EAE）旨在从文档中识别事件相关的论元并为其分配语义角色。论文指出现有基于角色（role）的跨度选择（span selection）策略主要存在两方面局限：

- **忽略事件实例内部论元之间的相互关系**：传统方法往往将每个角色的论元抽取视为独立任务，未显式建模同一事件中不同论元（如攻击者、目标、工具、地点）之间的结构关联。
- **未充分利用事件模式与事件实例之间的关联**：已有方法多依赖预训练语言模型（PLM）从事件模式文本或文档中捕捉角色语义，但缺少将抽象的事件模式（事件类型、角色定义）与具体的事件实例（触发词、预测论元跨度）进行对齐和联合建模的机制。

论文的目标是：通过构建"事件模式-实例图"（Event Pattern-Instance Graph, EPIG），显式建模角色间、论元间以及模式与实例间的直接与间接关联，并在此基础上设计多轮角色表示学习策略，从而丰富角色语义、提升文档级论元抽取的准确率。

---

## 2. 方法论

### 2.1 核心思想

论文提出 **EPIG-EAE** 模型，核心是将事件模式层（事件类型及其角色）和事件实例层（触发词及预测论元跨度）组织为一个双层异构的**事件模式-实例图（EPIG）**，并通过图中角色节点与角色边的多次交互式迭代更新，逐步优化角色表示，再用于下游跨度预测。

### 2.2 整体架构流程

模型主要由六个组件构成：

1. **嵌入层（Embedding Layers）**：使用 BART 编码文档得到文档表示，将角色提示模板（prompt）与文档编码一并送入 BART 解码器，得到各角色的初始表示。
2. **初步跨度选择（Preliminary Span Selection）**：基于角色当前表示，预测其在文档中的开始/结束位置概率分布，得到初步论元跨度。
3. **事件模式-实例图构建（EPIG Construction）**：将预测跨度填入图中的跨度节点，构建以下三类结构性边（均为无向边）：
   - 事件实例层：触发词节点 ↔ 跨度节点，边类型为对应角色名称；
   - 事件模式层：事件类型节点 ↔ 角色节点，边类型为"属性"；
   - 跨层匹配关联：事件类型节点 ↔ 触发词节点，角色节点 ↔ 对应跨度节点。
4. **节点-边交互式多轮学习网络（Node-Edge Interactive Multi-round Learning Network）**：在图中通过优化的图注意力网络（GAT）交替更新节点与边表示——更新节点时将边表示作为虚拟节点参与注意力计算；更新角色边时融合角色节点、触发词节点、跨度节点及旧边表示的语义。
5. **历史角色记忆模块（Historical Role Memory）**：为每个角色维护记忆单元，融合历史角色知识、图谱学习到的角色表示与原始提示角色表示，提升对新实例的泛化能力。
6. **论元抽取（Argument Extraction）**：使用最终轮次的角色表示进行跨度起止位置预测，采用二分图匹配损失进行训练。

### 2.3 关键公式与机制（文字说明）

- **跨度选择**：角色表示分别与可学习的起始/结束参数相乘，经 softmax 后在文档全上下文上得到起止概率分布。
- **跨度节点初始表示**：取预测跨度内各 token 表示的平均值。
- **节点更新**：在 GAT 中将角色边表示与邻居节点表示拼接，计算注意力系数，多头聚合后更新当前节点；丢弃机制（dropout）被引入以避免过拟合。
- **边更新**：将边自身的旧表示与相关角色节点、触发词节点、跨度节点表示求平均后经权重矩阵变换得到新的边表示。
- **最终角色表示**：将最后更新轮次得到的角色节点表示与角色边表示取平均。
- **角色融合**：历史记忆表示、图谱更新后的角色表示与原始提示角色表示三者融合，得到用于下一轮/最终预测的角色表示。

---

## 3. 实验设计

### 3.1 数据集

论文在三个数据集上评估模型：

| 数据集 | 语言 | 事件类型数 | 角色数 | 文档规模（事件数） |
|---|---|---|---|---|
| RAMS | 英语 | 139 | 65 | 9,124 个事件 |
| WikiEvents | 英语 | 50 | 59/69 | 3,951 个事件（部分文档多事件） |
| OEE-CFC | 中文（金融评论） | 1 | 21 | 17,469 个事件 |

其中 RAMS 每篇文档只有一个事件，WikiEvents 涉及多事件抽取场景，OEE-CFC 为单事件类型、多角色的中文开放事件抽取场景。

### 3.2 评估指标

- **Arg-I（论元识别 F1）**：预测跨度边界与任一黄金论元跨度匹配即视为正确；
- **Arg-C（论元分类 F1）**：预测跨度边界与黄金跨度匹配且角色类型一致才视为正确。

### 3.3 对比基线

论文与多类近期方法进行对比，包括：

- **TSAR**（基于 AMR 增强）、**PAIE**（基于提示的角色跨度选择）、**TabEAE**（多事件并行抽取）、**SCPRG**（上下文线索+角色相关性）、**SPEAE**（软提示建模文档语义）、**EACE**（角色依赖树）、**DEEIA**（上下文注意力加权角色表示）、**HMPEAE**（超球多原型匹配）等。

### 3.4 实验规模

实验涵盖：总表性能对比（RAMS、WikiEvents、OEE-CFC）× 多种预训练模型规模（base/large）、图结构的边消融与变体实验、节点/边不同更新机制消融、角色融合策略消融、图更新迭代次数实验、多轮角色学习机制实验。

---

## 4. 资源与算力

论文正文及附录中**未明确说明**所使用的 GPU 型号、数量、训练时长等硬件与算力资源信息，也未报告训练成本（如参数量、显存占用、单轮训练耗时）。因此该部分信息暂缺。

---

## 5. 实验数量与充分性

### 5.1 实验数量

论文的实验设计比较全面，主要实验包括：

1. **总表对比**：RAMS 和 WikiEvents 上使用 BART-base / BART-large（部分基线用 RoBERTa），另在 OEE-CFC（BART-base）上测试；
2. **EPIG 边消融（4 组）**：逐一移除触发词-跨度边、类型-角色边、类型-触发词边、跨度-角色边；
3. **其他图结构变体（4 组）**：增加跨度-跨度边、角色-角色边、两者同时增加，以及删除同角色共享连接；
4. **更新机制消融（3 组）**：边更新时去掉角色节点、节点更新时去掉角色边、完全不更新边；
5. **角色融合策略消融（4 组）**：去掉历史角色记忆、去掉角色边融合、去掉角色节点融合、同时去掉角色节点与角色边融合；
6. **图更新迭代次数实验**：1/2/3/4/5/10 次；
7. **多轮角色学习轮数实验**：两种策略（重构 EPIG vs. 原图迭代更新）× 5 轮。

### 5.2 充分性与公平性评价

- **充分性较好**：在三个不同语言、不同标注规模、不同事件结构（单事件、多事件、单类型多角色）的数据集上验证，且同时提供了多种消融性分析（边结构、图结构、更新机制、融合策略、迭代次数），能从多个角度论证设计组件的有效性。
- **公平性方面需注意**：并非所有基线的预训练语言模型完全一致（如有些用 RoBERTa-large、有些用 BART），不同结果可能部分来源于主干模型差异而非方法本身；但从各基线论文引用各自报告的结果来看，总体上符合该方向的实验惯例。OEE-CFC 上仅与 PAIE 做了对比，缺少更多基线参考，是该文实验对比相对薄弱的一环。

---

## 6. 主要结论

1. **EPIG 结构有效**：在三个数据集上均取得有竞争力的结果。在 RAMS（BART-base）上达到 Arg-C 52.10%，与 SOTA 基线持平或更优；OEE-CFC 上全面优于 PAIE。
2. **各类边均有贡献**：触发词-跨度边对性能影响最大（移除后 Arg-C 下降最多），其余边也均有助于丰富角色语义，移除任意一边均带来不同程度的性能下降。
3. **边添加需谨慎**：在图中额外增加跨度-跨度边、角色-角色边等会引入噪音，反而不利于建模，说明 EPIG 的稀疏化结构更稳健。
4. **节点-边交互更新是有效机制**：边更新中角色节点信息不可替代；角色边参与节点更新能带来显著提升。
5. **多轮迭代需适度**：图的节点/边更新以 2 次迭代为最优，迭代过多导致过平滑；多轮角色学习中第 1~2 轮效果最佳，轮数过多会导致误差累积和过拟合。

---

## 7. 优点

1. **创新性的双层图结构建模**：将事件模式（事件类型→角色）与事件实例（触发词→论元）通过跨层映射边结合，弥补了既有研究中对模式层与实例层关联建模的不足。EPIG 同时编码了三种层面的语义关联：模式层角色关系、实例层论元关系、跨层模式-实例对齐关系，设计较为完整。
2. **节点-边联合迭代更新机制设计较新颖**：在 GAT 基础上将边表示作为虚拟节点参与注意力计算，并在边更新中聚合节点和边自身的信息，能够实现节点与边表示的双向语义融合，比以往仅更新节点或仅用固定矩阵更新边的方法更具表达力。
3. **结构化设计规避噪音**：构建图时避免直接把不同论元（跨度）直接相连，而是通过触发词节点传递间接关联，降低错误传播风险，在工程上具备合理性。
4. **历史记忆机制与多轮学习相结合**：通过跨文档记忆角色表示、并采用多轮"预测→构图→更新表示→再预测"的迭代策略，与人类认知中不断修正思路的过程一脉相承。
5. **实验分析深入**：不仅提供总表结果，还针对边结构、图结构变体、更新机制、融合策略分别进行了多组消融与分析，讨论相对充分。

---

## 8. 不足与局限

1. **资源与算力信息缺失**：论文未报告 GPU 类型、数量、训练时间、模型参数规模等关键训练成本信息，可复现性和工程参考价值受限。
2. **对单类型、多角色数据的适配性存在局限性**：论文自己在 Limitations 中承认，在一些数据集上，如 OEE-CFC 只有 1 个事件类型时，事件类型节点失去了模式层区分能力，所有角色挂在该事件类型下会产生结构性冗余，可能在图中传播噪声。
3. **超参数敏感性较高**：论文指出图更新迭代次数、多轮学习轮数在不同数据集上表现差异明显且难以一概而论，简单场景下迭代过多导致过平滑。这种不稳定性造成模型实用时需要为每个数据集单独调整超参数，泛化门槛较高。
4. **基线对比范围不完全一致**：不同基线的预训练模型（BART、RoBERTa）不完全统一，英文数据上部分结果来自原论文报告值，若各基线系统实现细节不统一会引入一定不公平比较风险。OEE-CFC 数据集只与 PAIE 作了对比，基线数量不足。
5. **错误累积风险**：多轮学习依赖前一轮预测跨度来构图，若首轮预测误差较大，后续轮次误差会被逐步放大，论文实验中随着轮数增加的性能下降也印证这一风险。
6. **应用场景受限**：EPIG 的构图方式依赖事件类型、角色提示和触发词，因此仍主要适用于有相对固定事件模板（事件本体）的场景，对完全开放式的、无预定义事件类别与角色的抽取场景支持有限。
7. **复杂图结构可解释性有限**：通过图注意力与交互更新后获得了更丰富的表示，但边和节点高维迭代更新过程的语义解释性没有展开讨论，难以清晰说明几何上学习的多重语义融合。

---

（完）
