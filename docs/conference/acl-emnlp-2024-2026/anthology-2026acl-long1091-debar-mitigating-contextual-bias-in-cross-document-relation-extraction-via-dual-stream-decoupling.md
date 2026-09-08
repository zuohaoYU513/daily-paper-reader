---
title: "DEBAR: Mitigating Contextual Bias in Cross-Document Relation Extraction via Dual-Stream Decoupling"
title_zh: DEBAR：通过双流解耦缓解跨文档关系抽取中的上下文偏差
authors: "Zhixuan Yang, Fu Zhang, Huangming Xu, Jingwei Cheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1091.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 跨文档实体关系抽取，双流解耦降低单边证据偏差
tldr: 跨文档关系抽取需要综合分散在多文档中的证据，但既有方法把目标实体与桥梁实体统一融合，导致证据偏向一方而丢失完整推理链。DEBAR提出双流实体偏差消减框架，对目标实体与中间桥梁实体采用解耦的表示与推理流，以避免单边上下文偏差；同时改进二元关系是否存在判定。实验结果显示该方法在跨文档关系抽取中提升推理稳定性和关系识别效果。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1091/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1091/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 820, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1091/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1091/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1091/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 785, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1091/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 547, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1091/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 797, \"height\": 593, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 726, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 782, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 803, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 796, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 637, \"height\": 557, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1091/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 811, \"height\": 872, \"label\": \"Table\"}]"
motivation: 跨文档关系抽取中桥梁实体只对齐单侧目标实体时会产生上下文偏差和错误推理。
method: DEBAR采用双流解耦分别建模目标实体与桥梁实体证据，并改进关系存在性的判定方式。
result: 缓解了单边关系转移偏差，在跨文档关系抽取评测中取得更稳健的结果。
conclusion: 为跨文档、长文本实体关系抽取提供了降低证据偏置、增强推理链的框架。
---

## Abstract
Cross-document Relation Extraction (CodRE) requires reasoning over scattered evidence to identify relations between target entities across multiple documents. Existing methods indiscriminately fuse target entities and the intermediate bridge entities that link them into a unified representation. This leads to intermediate evidence that often aligns with only one side of the entity pair, resulting in one-sided relation transfer contextual bias and incomplete reasoning chains. Moreover, these methods typically employ a global threshold to determine relation existence for all entity pairs, limiting the model’s reasoning performance.To address these issues, we propose **DEBAR** (Dual-stream Entity Bias Reduction), a framework designed to explicitly decouple and preserve bidirectional bridge evidence, combined with a novel dynamic loss optimization objective. Specifically, DEBAR employs a **bridge-aware input construction** strategy and a **dual-stream graph reasoning network** to separately encode head and tail contexts, preventing semantic interference while capturing global dependencies through iterative message passing. Furthermore, we introduce a **curriculum-aware ranking optimization objective** that progressively tightens classification constraints to stabilize training and enforce discriminative decision boundaries. Experiments on the CodRE benchmarks show that DEBAR achieves state-of-the-art performance while effectively mitigating cross-document contextual bias. Moreover, extensive experiments on our proposed loss across backbones confirm its generalization, suggesting it as a reliable replacement for existing CodRE losses. Code is available at https://github.com/newyuyou/DEBAR.

---

## 论文详细总结（自动生成）

# 论文总结：DEBAR——基于双流解耦的跨文档关系抽取上下文偏差缓解方法

## 1. 核心问题与研究动机

- **任务背景**：跨文档关系抽取（Cross-document Relation Extraction, CodRE）要求模型在多个文档之间对分散的证据进行多跳推理，从而判定给定头实体和尾实体之间是否存在特定关系。与传统句子级或单文档级 RE 不同，CodRE 中目标实体往往出现在不相交的文档子集中，需要通过**中间桥梁实体（bridge entity）** 建立语义连接。
- **现有方法的缺陷**：
  - 已有方法（如 ECRIM、NEPD 等）将目标实体与桥梁实体**不加区分地融合进统一的表示空间**，导致中间证据往往只与实体对中的某一侧对齐。例如，桥梁实体与头实体高度语义相关、却与尾实体隔绝时，模型可能捕获了"头实体—桥梁"的关系，却无法正确传播到"桥梁—尾实体"，形成**单边关系转移上下文偏差（one-sided relation transfer contextual bias）**，造成推理链断裂。
  - 已有方法（如 ECRIM）通常对所有实体对使用**固定的全局上界与下界阈值**（上下界之间存在容差区间）来判断关系是否存在，这种区间式的分类边界无法保证正样本得分**一致高于**负样本得分，导致排序模糊与推理性能受限。
- **本文目标**：通过显式解耦并保存双向桥梁证据，提出新的动态优化目标，同时缓解上述两类问题。

## 2. 方法论：DEBAR 框架

DEBAR（Dual-stream Entity Bias Reduction）包含三个核心模块：

### 2.1 桥梁感知的输入构建模块（Bridge-Aware Input Construction, BIC）

- **动机**：有效桥梁实体应同时与头实体和尾实体都表现出连接强度，而非仅与单侧高度共现。
- **单侧连接分**：对桥梁实体 $e_b$ 与目标实体 $e_k$（$k\in\{h,t\}$）定义三层加权的共现得分：
$$S_k(e_b) = \alpha\cdot\phi_s(e_b,e_k) + \beta\cdot\phi_p(e_b,e_k) + \gamma\cdot\phi_d(e_b,e_k)$$
其中 $\phi_s,\phi_p,\phi_d$ 分别表示在句子、段落、文档级别上的互斥共现计数。
- **双向平衡得分**：采用几何平均惩罚单侧偏差：
$$S_{bri}(e_b)=\sqrt{S_h(e_b)\cdot S_t(e_b)}$$
该式保证只有当桥梁实体与头、尾两侧都保持连通时得分才非零，从而过滤虚假单侧链接。
- **句子级扩展**：将桥梁实体的得分传播到包含它的句子上；若句子同时包含两个目标实体则赋予无穷大权重（最高优先级）。随后对所有句子按得分排序，截取前 $K$ 句供应编码器使用。
- **输出**：为头实体和尾实体分别构建两条独立的输入流。

### 2.2 双流图推理网络（Dual-Stream Graph Reasoning Network, DSGN）

- **双流编码**：对头侧输入流 $X_h$ 和尾侧输入流 $X_t$ 分别用同一个 PLM 独立编码：$H_h=\mathrm{PLM}(X_h)$，$H_t=\mathrm{PLM}(X_t)$，避免早期交互带来的语义干扰。
- **实体表示抽取**：通过 max-pooling 分别提取头、尾实体表示；对出现在两侧输入中的每个桥接实体，则各自提取一个上下文相关表示。
- **全局实体图构建与 GRN 推理**：
  - 以实体为节点构建全局图 $G$，边表示语义共现；
  - 初始节点状态为双流编码得到的实体表示；
  - 用带**门控聚合**的 GRN 进行 $L$ 轮（文中 $L=2$）迭代消息传递：
$$h_v^{(l)}=\mathrm{GRU_{node}}\left(m_v^{(l)}\oplus g^{(l-1)},\;h_v^{(l-1)}\right)$$
$$g^{(l)}=\mathrm{GRU_{global}}\left(\mathrm{Pool}(\{h_v^{(l)}\}),\;g^{(l-1)}\right)$$
其中 $m_v^{(l)}$ 是对邻居表示的加权和，$g$ 为全局状态向量，从而同时捕捉局部与全局依赖。

### 2.3 预测与课程式排序优化（Curriculum-aware Ranking Optimization, CAO）

- **关系预测**：在 GRN 精化后的实体表示基础上，参考 ECRIM 的做法，按路径构造关系表示，用跨路径自注意力融合，通过 MLP 得到路径级概率，再经 max-pooling 得到包级（bag-level）得分。
- **动态阈值损失 $L_{CL}$**（课程式边界移动）：用动态标量边界 $m_n^{(t)}$与 $m_p^{(t)}$取代固定阈值区间，训练过程中边界从宽松逐渐收紧（正类下界从 8 线性上升至 10，负类上界从 10 线性下降至 8）。
$$L_{CL}=\log\left(e^{m_n^{(t)}}+\sum_{r\in\Omega_{neg}}e^{\hat{y}(r)}\right)+\log\left(e^{-m_p^{(t)}}+\sum_{r\in\Omega_{pos}}e^{-\hat{y}(r)}\right)$$
- **排序惩罚项 $L_{rank}$**：对每个正负样本对加权惩罚，要求正样本得分必须高于负样本得分超过一个边界 $\delta$：
$$\ell(r_p,r_n)=\sigma(\hat{y}(r_n)-\hat{y}(r_p))\cdot\max\left(0,\;\delta+\hat{y}(r_n)-\hat{y}(r_p)\right)$$
- **最终目标**：$L_{CAO}=L_{CL}+\lambda L_{rank}$，其中 $\lambda=0.1$、$\delta=0.3$。

## 3. 实验设计

### 3.1 数据集与评测场景

- **数据集**：CodRED（Yao et al., 2021），从 Wikipedia/Wikidata 构建的大规模跨文档关系抽取数据集，含 276 种关系类型、3 个子集（Train/Dev/Test），文档平均约 4,939 个 token，需要跨分散文本进行多跳推理。
- **主要评测场景**：
  1. **Closed setting**：直接给定有效文本路径（text paths），模型只需要做关系分类；
  2. **Open setting**：不给定路径，需要先从语料库中检索路径再分类；
  3. **额外设置**：移除 CodRED 中单文档子集后仅用纯跨文档实例训练/测试；
  4. **与 LLM 对比**（遵循 NEPD 的协议，用 Micro-F1 在 dev 集上比较）。
- **评测指标**：AUC、F1、P@500、P@1000，以及 NEPD 协议下的 Micro-F1。

### 3.2 对比方法

- 预训练语言模型骨干：**BERT-base** 和 **RoBERTa-large**。
- 基线模型：Pipeline、End-to-end（原始 CodRED 方法）、**ECRIM**（实体中心）、**MR.COD**（多跳检索）、**LGCR**（局部到全局因果推理）、**NEPD**（非桥梁实体增强与预测去偏）、KD-CodRED（增补外部知识，在相关工作提及）。
- 大语言模型方法（LLM）：GPT-3.5-turbo、InstructUIE、InstructUIE-FT。

## 4. 资源与算力

- 论文正文中**没有明确说明 GPU 的型号与数量**。
- 在效率分析（Cost Analysis）部分给出了每个 epoch 的训练耗时：
  - End-to-end：6.5 小时/epoch；
  - ECRIM：9.7 小时/epoch；
  - DEBAR：10.2 小时/epoch。
- 文中指出：与 ECRIM 相比，DEBAR 的训练时间仅增加约 5.2%，但 F1 从 60.85 提升至 64.58。由于缺失 GPU 型号和批大小等信息，尚无法精确评估总预算，模型共训练 10 个 epoch。

## 5. 实验数量与充分性分析

DEBAR 共开展了 8 类主要实验：

1. **主实验**：BERT-base 下闭式与开式设置的 Dev/Test 对比（Table 2）；
2. **骨干泛化实验**：RoBERTa-large 下的闭式设置对比（Table 3）；
3. **严格跨文档实验**：去除单文档子集后的纯跨文档训练与测试（Table 4）；
4. **消融实验**：包括去掉 BIC、去掉双流编码器、去掉 GRN、同时去掉双流与 GRN、去掉 CAO 共 5 个变体（Table 5）；
5. **效率对比实验**（Table 6）；
6. **桥接实体数量敏感性实验**（Figure 3a/3b）；
7. **CAO 损失泛化实验**：将 CAO 移植到 End-to-end 与 ECRIM 上验证通用性（Table 7），并结合正负样本得分分布可视化（Figure 4）证明其决策边界的有效性；
8. **与 LLM 对比实验**（Table 8），以及案例分析（Table 9）和附录中的超参数敏感性分析（$\alpha,\beta,\gamma$、$\lambda$、$\delta$）。

- **充分性评价**：
  - 覆盖面广：闭式和开放式设置、两种骨干、纯跨文档设置、LLM 对比、消融及可迁移性验证均被覆盖，实验总体充分。
  - 公平性较好：与基线结果对齐引用原论文数据，消融实验在 dev 集上完成；各模块独立拆解清晰，案例分析直观展示了偏差缓解的机制。
  - 不足：CAO 的跨模型验证只测试了 2 个骨干模型（且都较旧，均为浅层结构），未在 MR.COD、LGCR、NEPD 等更新的基线上验证；实验未报告多次重复运行的标准差，统计显著性检验缺失。

## 6. 主要结论与发现

- DEBAR 在 CodRED 的闭式/开式设置、BERT-base/RoBERTa-large 骨干下均取得了 SOTA 或显著优于基线的最佳结果。例如 BERT-base 闭式下 F1 领先最优基线 0.95 个点，开式下 F1 领先 0.24；RoBERTa-large 下 dev 集 F1 领先 LGCR 2.06，test 集 F1 领先 3.73。
- 在只保留纯跨文档实例的设置上，DEBAR（F1 39.32）仍然领先 NEPD（F1 38.22）与 ECRIM（F1 36.41），说明其在缺少单文档捷径时也能有效抽取高质量证据。
- 每个组件都有贡献：去掉 BIC 使 F1 下降 5.74 个点（最大降幅）；去掉双流编码器 F1 下降 2.16；去掉 GRN 下降 0.73；去掉 CAO 下降 0.44。这说明桥梁感知输入构建和双流结构是缓解单边偏差的关键。
- 保持其他模块不变、仅替换为 CAO 损失后，End-to-end（51.26→52.37）和 ECRIM（60.85→61.73）的性能均稳定提升，说明 CAO 是一种可泛化、可替代现有 CodRE 损失函数的优化策略。

## 7. 主要优点

- **问题定位准确**：论文明确指出现有统一融合表示导致的单边证据偏差问题，以及固定全局阈值导致的排序不严格问题，并以图例和实例阐明其危害。
- **方法设计针对性强且结构优雅**：
  - 用**几何平均**筛选双向相连的桥梁实体，简单有效，从源头抑制单边证据；
  - 采用**双流编码 + 全局 GRN 推理**实现了"局部解耦、全局整合"，兼顾特征独立性和全局依赖；
  - 动态边界加排序约束的**课程式优化目标**在思路新颖性和可迁移性上都优于简单阈值损失。
- **实验设计与分析完整**：不仅提供主结果，还有消融、效率分析、桥接实体数量影响、Loss 可视化、泛化验证和案例分析，并公开了超参数敏感性分析。
- **工程成本控制较好**：效率分析表明相对 ECRIM 仅增加约 5.2% 训练时间即可获得显著收益；代码开源，也增强了可复现性。

## 8. 不足与局限性

- **方法层面的局限**（论文作者自述）：
  1. 双流结构对头尾上下文独立编码，引入了约 5.2% 的训练延迟；
  2. 方法依赖显式桥梁实体来构建证据路径，当中间连接稀疏或缺失时适应能力有限；作者提出后续可通过隐式推理机制和非桥梁实体的辅助语境来补充证据链。
- **实验方面的局限**：
  1. 大部分实验在 dev 集上报告消融结果，缺少在 test 集上的完整消融对比（Table 5 未报告对应 test 结果）；
  2. 缺少多次重复运行的标准差和统计显著性检验，收益的稳定性缺乏数字支撑；
  3. 超参数分析只在固定配置上进行逐项扫描，未说明各超参数之间的交互影响；
  4. 未报告在不同随机种子、不同初始化条件下的方差，结果的可靠性评估仍有提高空间；
  5. 与 LLM 的对比实验在更全面的 Open setting 下没有给出实际值，而只在 dev 集闭式设置（Micro-F1）上对比。
- **效率分析的局限**：只对比了每 epoch 时间，未报告总数据集规模下的整体显存占用、GPU 型号和推理速度；实际算力开销的完整评估仍不充分。

（完）
