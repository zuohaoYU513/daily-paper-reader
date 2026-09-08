---
title: Incorporating Temporal Coherence to Cross-Document Event Coreference Resolution
title_zh: 将时间一致性纳入跨文档事件共指消解
authors: "Xinyu Chen, Peifeng Li (李培峰), Qiaoming Zhu (朱巧明)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1345.pdf"
tags: ["query:evidence-qa"]
score: 8.0
evidence: 通过时间事件图和有序时间段显式建模事件的时间一致性，与跨句、跨文档追踪时间变化相关
tldr: 现有跨文档事件共指消解主要强化事件提及间的语义一致性，忽略时间一致性。论文提出CohTP框架，先用微调的自然语言推理模型构建时间事件图，再通过边感知图神经网络消解冲突并把事件划分为有序时间段，在时间一致片段内进行事件共指决策。实验表明显式时间约束能提升共指性能，为跨句文档中的时间关系建模与时间变化追踪提供了可迁移方法。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1345/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1345/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 839, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1345/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 1034, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1653, \"height\": 814, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 469, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1659, \"height\": 524, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 803, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 816, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 809, \"height\": 570, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 810, \"height\": 473, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 808, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 811, \"height\": 1591, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 824, \"height\": 1056, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 808, \"height\": 1056, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 818, \"height\": 1056, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 811, \"height\": 1267, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1345/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 804, \"height\": 321, \"label\": \"Table\"}]"
motivation: 既有跨文档事件共指消解忽视事件间时间一致性，影响事件对齐与演化理解。
method: 提出CohTP，用自然语言推理构建时间事件图，经边感知图神经网络消解冲突后按有序时间段执行共指解析。
result: 在跨文档事件共指数据上验证了时间一致性建模带来的性能提升。
conclusion: 显式建模时间约束能改进事件共指，为时间敏感的文档事件理解提供支持。
---

## Abstract
Previous work on cross-document event coreference resolution (CDECR) primarily focused on enhancing semantic coherence between event mentions, largely overlooking the critical aspect of temporal coherence. To address this issue, we propose CohTP, a novel Temporal Cohorence-driven event coreference framework. CohTP explicitly models and enforces temporal constraints by first constructing a temporal event graph via a fine-tuned natural language inference (NLI) model. The graph is then refined using an Edge-Aware GNN to resolve conflicts and partitioned into ordered time segments, where undirected edges group contemporaneous events. Event coreference resolution is subsequently performed within these temporally coherent segments, where event representations are further augmented with temporally consistent contexts. Experiments on the ECB+, GVC, WEC, and ECB+META datasets show that CohTP outperforms several state-of-the-art baselines.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

**核心问题**：跨文档事件共指消解（CDECR）的目标是将多个文本来源中指向同一真实世界事件的提及进行聚类。以往工作主要集中在增强事件提及间的语义连贯性，**普遍忽略了一个关键的时间约束——共指事件必须发生在重叠或相同的时间段内**。这一失误导致语义相似但时间上完全分离的事件（例如相隔数月“公司发布 A 产品”和“公司发布 B 产品”）被错误地聚在一起，产生大量假阳性共指链接。

**整体含义**：论文将“时间一致性”从辅助性软特征提升为结构化硬约束，提供了从“语义相似性判断”转向“时间约束下的语义判断”这一更高效、更准确的跨文档事件共指消解范式。作者将事件按发生时间分段，仅在时间连贯的段内进行共指消解，从根本上排除了跨时间段的错误链接，同时缩减了候选搜索空间。

## 2. 论文提出的方法论

论文提出 **CohTP（Temporal Coherence-driven Event Coreference framework）**，由三个核心环节组成：

### 2.1 时间事件图的构建与精炼（暂态关系建模）

- **时间关系初始化**：在 MAVEN-ERE 数据集上微调 BERT-NLI（将时间关系预测建模为自然语言推理问题），将时间关系二值化为 **BEFORE**（事件发生于不同时间段）与 **SAMETIME**（包含 CONTAINS/SIMULTANEOUS/OVERLAP 合并，表示同一时间区间）。对事件对双向预测并取概率分布，构建初始时间图 G。
- **Edge-Aware GNN（EA-GNN）**：为消解全局时间冲突，提出新图神经网络：
  - 节点存事件上下文表示（经 BERT-Large 编码后过 BiLSTM）；
  - 边存时间关系概率分布（BEFORE/SAMETIME）；
  - 通过消息传递机制联合更新节点与边，其中边语义参与邻居消息计算，并采用注意力聚合；
  - 迭代 K=3 层后以带层注意力权重的门控组合输出最终边概率。
- **三种无监督的“时间感知一致性”loss** 约束图精炼：
  1. **传递性 loss（Ltrans）**：枚举三元事件组，强制若 e₁→e₂ 为 BEFORE 且 e₂→e₃ 为 BEFORE，则 e₁→e₃ 应倾向 BEFORE（同理 SAMETIME）；
  2. **对称性 loss（Lsym）**：最小化双向预测分布差异，纠正对称 SAMETIME 的不对称预测；
  3. **语义保持 loss（Lsem）**：用预训练在 MAVEN-ERE 上的方向/共指分类器约束精炼结果不过度偏离初始语义，防止过度修正。
  - 综合目标：L = λtransLtrans + λsymLsym + λsemLsem（λ = 1.0/0.6/0.5）。
- **规则基残余冲突修正**：针对EA-GNN输出仍可能残留的对称冲突（一方BEFORE另一方SAMETIME时取置信度更高的关系）与传递冲突（对三元组穷举有效模式，按联合概率和最高者修正），确保图逻辑一致。

### 2.2 时间划分（有序分段）

在精炼后的图上，将无向的 SAMETIME 边连接的事件归入同一段时间段 T_m；BEFORE 有向边定义段间顺序，从而形成有序的时间分段 T = {T₁, T₂, …, T_M}，供后续共指解析只在同一段内进行。

### 2.3 时间感知的共指消解

- **跨时间共指恢复**：对相邻时间段间的 BEFORE 预测，用“性能监测”策略识别导致 MAVEN-ERE 时间测试集性能（模型置信度）下滑的低质量样本（约占全部 BEFORE 预测 32%），交由 GPT-4 多轮重新判断。约 65% 被修正为 SAMETIME，挽回因时间误判而散落到不同分段的真共指事件对。
- **时间上下文增强**：对同一时间段 Tε 内的候选共指对 (ei, ej)，利用 Coh(·) 模块在前段 Tε−1 与后段 Tε+1 中各挑选语义最连贯的事件提及 eprev/enext，构建扩展序列 S = [ctx(eprev); ctx(e); ctx(enext)]。
- **共指打分**：以 Longformer 编码扩展序列，MLP 输出 Sigmoid 共指分数，用二元交叉熵训练；推理时采用 best-first 聚类生成最终共指链。

## 3. 实验设计

### 数据集与 Benchmark
- **五个评测集**：ECB+、GVC、WEC、ECB+META1 与 ECB+METAm（覆盖英语新闻与维基等多种语料，META 为隐喻改写生成的加强版挑战集）。
- 数据切分与 Bugert et al. (2021)、Ahmed et al. (2024b) 保持一致；主实验使用 gold mention，并另设 predicted mentions 对比。
- 评价指标：Pairwise F1 与 CoNLL-F1（MUC/B³/CEAF_e 的以整体分数），附录提供完整三项分解。

### 对比方法
- **主流基线**：CD-DCE、MP、KD、LLM-Min、DSSI、CD-DRS、HT（HeidelTime 规则时间基线）等近期最优系统。
- **消融与分析方法**：
  - 时间消融（w/o Temporal；w/o Temporal&Coh）；
  - 图精炼消融（w/o Trans；w/o Sym；w/o Sem）；
  - LLM 干预策略（全样本干预、无干预、CohTP 选择性干预）；
  - LLM 可替代性（LLaMa-Only、LLaMa+Temp）；
  - 恢复窗口大小（δ=0/1/2/3/4）；
  - 不同骨干模型组合（BERT-Large/DeBERTa-v3/ModernBERT × Longformer/DeBERTa/ModernBERT 等）；
  - 超参数敏感性（隐藏维度 128/256/512、层数 K=2/3/4）、概率和与概率积两种冲突解法等。

### 评估充分性判断
消融覆盖范围全面，兼顾了时间建模（分割、恢复、上下文增强）、图精炼的三种约束、LLM 干预策略的精度/召回影响、不同骨干泛化性与关键超参数敏感性；附录还补充了提取提及下的表现、与其他 LLM（GPT-3.5/LLaMa/Flan-T5）的替换实验、跨段场景分析、完整指标。实验设计较为充分，客观性与公平性较好。

## 4. 资源与算力

- 论文明确报告了实验硬件为 **NVIDIA RTX 4090 GPU**，但**未说明具体 GPU 数量**。
- 给出了若干相对耗时数据：CDECR 中平均每对事件提及耗时约 1.1 s（对比 CD-DCE 的 2.1 s）；对低置信度候选样本的性能诊断在 6 路并发下约需 **2 小时**完成；CohTP 全流程在约含 400 对的句组上总耗时 441.6 s，约为 CD-DCE（826.5 s）的一半。
- 未提供各阶段训练所需的精确 GPU 时长总量。

## 5. 实验数量与充分性

- **数据集覆盖广**：5 个常用标准评测集，并给出完整 MUC、B³、CEAF_e 与 CoNLL 各项指标。
- **对比实验多**：与 7 类以上近期系统比较，含 2 类提取提及对比；
- **消融丰富**：上述 20 余组不同维度的对照实验系统解释了时间信息、图精炼各一致性模式、LLM 干预策略和骨干编码器的作用；
- **误差分析扎实**：量化了时间预测误差导致的召回损失、图精炼修正的成功与失败比例、LLM 干预的正面/负面效应；
- **恢复窗口实验**给出了 δ 扩展的代价/收益边界；案例研究直观展示了模型行为。

**总体评价**：实验充分性较高，多数据集 + 多基线 + 多维消融 + 误差统计方式使结论较为可信。

## 6. 主要结论与发现

1. **时间一致性是 CDECR 中被低估但必要的约束**：加入时间分段把共指候选限制在同一时间段内，显著降低假阳性并减少候选空间，CohTP 在 ECB+、GVC、WEC、ECB+META1、ECB+METAm 上普遍超越已有 SOTA（ECB+ CoNLL-F1 88.9，GVC 87.7 等）。
2. **效率与性能兼得**：相比基于复杂话语结构建模的 CD-DCE，CohTP 以更轻量结构达到相近甚至更优的性能，且速度接近两倍。
3. **EA-GNN 的全局精炼有效**：传递性约束损失贡献最明显，移除后 EC+ 下降 1.5、GVC 下降 2.2；图精炼将时间冲突率降低约 58.8%–66.9%。
4. **选择性 LLM 干预优于全量或零干预**：针对性纠正 32% 低置信度 BEFORE 预测中约 65% 的错误，实现精度与召回更好平衡，过度盲目干预反而引入噪声。
5. **时间+话语连贯是互补增强**：去掉时间仅留连贯（ECB+ -2.3/ GVC -1.9），再去掉连贯损失更大（ECB+ -5.0/GVC -7.3），两者结合取得最佳。
6. 真实错误以“语义相似但时间不同被误分别/误聚”为主，显式时间提示（如 today、Wednesday、Sunday）可有效区分场景中事件。

## 7. 优点

- **范式创新**：将时间从软特征升级为“结构化的硬约束”，具有清晰且可泛化到其他时间敏感 NLP 任务的研究思路；
- **方法体系完整**：从 NLI 时间预测、图精炼、残差修正、有序分段到上下文增强，模块流程自洽且互为支撑；
- **解决实际瓶颈**：在减少误报的同时兼顾恢复被误分段的真实共指对，显著压缩搜索空间，效率提升明显；
- **实验全面且严谨**：统一 Pairwise/CoNLL 指标、多数据集 + 丰富的消融 + 多层次误差分析；
- **误差分析解释力强**：用量化比例说明时间预测错误来源、图精炼有效/失效机制、LLM 干预成败原因，信息密度高；
- 提供多种 LLM 对比、骨干替换、恢复窗口分析和完整指标，考察了方法的可迁移性、稳定性和边际收益。

## 8. 不足与局限

- **上游依赖限制**：仅在 gold mention 上做共指解析，未联合提及检测；在 predicted mentions 设置下 CoNLL-F1 从 88.9 跌至 62.8，性能受错误传播制约。
- **对初始时间预测高度敏感**：约 27.8% 的真实共指对被误判为 BEFORE，导致错分段并被排除出候选集，构成主要召回损失来源，说明时间关系分类器仍是整体性能的“瓶颈”。
- **句段粒度调节困难**：过细分段会分离真共指事件，过粗分段又可能混入时间不相容事件，如何自动选择合适分段粒度尚未解决。
- **跨较多段恢复收益有限**：恢复窗口 δ≥2 时精度下降明显且仅带来很小的召回增益（只有 3.5% 的真实共指对间隔≥2 段），需要更复杂的多跳/图传播式恢复机制才能进一步提升。
- **对 LLM 的潜在依赖**：跨时间共指恢复
