---
title: "Temporal Relation Extraction in Clinical Texts: A Span-based Graph Transformer Approach"
title_zh: 临床文本中的时间关系抽取：基于跨度的图Transformer方法
authors: "Rochana Chaturvedi, Peyman Baghershahi, Sourav Medya, Barbara Di Eugenio"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1251.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 面向长临床文档的跨句事件时间关系抽取，用图传播代替局部建模
tldr: 临床文本的时间信息抽取需要识别临床事件及其时间关系，且临床记录文档长、标注稀疏。GraphTREx将基于跨度的实体-关系抽取、临床预训练语言模型与异质图Transformer结合，通过图传播建模句子间和文档级依赖，从而捕捉长距离时序关系。在I2B2 2012基准上验证了这种图结构建模对复杂临床文档时序抽取的增强效果。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1251/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1493, \"height\": 438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1251/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1490, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1251/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1618, \"height\": 727, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1251/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 227, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1251/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1397, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1251/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1633, \"height\": 983, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1251/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1655, \"height\": 958, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1559, \"height\": 572, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 734, \"height\": 384, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 825, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 828, \"height\": 489, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 724, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 823, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 701, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 816, \"height\": 747, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 826, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 838, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 827, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1157, \"height\": 514, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1251/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 814, \"height\": 553, \"label\": \"Table\"}]"
motivation: 临床文本长且语义复杂、标注稀疏，跨句时序关系抽取非常困难。
method: 融合跨度抽取、临床预训练模型与异质图Transformer，建模局部和全局时序依赖。
result: 在I2B2 2012时序关系语料上验证了其抽取临床事件和时间关系的有效性。
conclusion: 图结构信息传播能改进长临床文档的事件时间关系挖掘。
---

## Abstract
Temporal information extraction from unstructured text is essential for contextualizing events and deriving actionable insights, particularly in the medical domain. We address the task of extracting clinical events and their temporal relations using the well-studied I2B2 2012 Temporal Relations Challenge corpus. This task is inherently challenging due to complex clinical language, long documents, and sparse annotations. We introduce GraphTREx, a novel method integrating span-based entity-relation extraction, clinical large pre-trained language models (LPLMs), and Heterogeneous Graph Transformers (HGT) to capture local and global dependencies. Our HGT component facilitates information propagation across the document through innovative global landmarks that bridge distant entities and improves the state-of-the-art with 5.5% improvement in the tempeval F1 score over the previous best and up to 8.9% improvement on long-range relations, which presents a formidable challenge. We further demonstrate generalizability by establishing a strong baseline on the E3C corpus. Not only does this work advance temporal information extraction, but also lays the groundwork for improved diagnostic and prognostic models through enhanced temporal reasoning.

---

## 论文详细总结（自动生成）

# 临床文本中的时间关系抽取：基于跨度的图Transformer方法（GraphTREx）

## 1. 论文核心问题与研究动机

- **核心任务**：从电子健康记录（EHRs）中的非结构化临床文本书写中，联合抽取临床事件（如症状、药物、检验等）和时间表达式（如日期、时长、频率），并判断它们之间的时间关系（Temporal Relations / TLinks，即 Before、After、Overlap）。
- **应用价值**：
  - 准确的时间线索有助于理解疾病进展、用药时序与不良反应关系。
  - 可用于2型糖尿病（T2D）等慢性病的机会性筛查，帮助识别患者病史中的早期风险因素，减轻临床人工审查负担。
  - 支持用药模式分析、癌症治疗轨迹提取等下游临床决策任务。
- **主要挑战**：
  - 临床文本存在大量专业词汇、独特时间表达和缩写歧义，需要领域特定模型；
  - 公开可用的标注语料稀缺（标注成本高、隐私限制严格）；
  - 传统流水线式（先抽取实体、再分类关系）容易造成错误传播，且难以建模实体与关系之间的复杂交互；
  - 临床文档通常较长，而 Transformer 模型上下文长度受限，已有方法多限于“短距离”或相邻句子，忽略了长距离时间关系及其与时间表达式的交互。

## 2. 提出方法：GraphTREx

- **总体思想**：采用“文本编码 → 初始关系预测 → 文档级异质图构建 → 图传播精化 → 最终关系解码”的端到端框架，同时建模局部上下文与全局文档依赖。
- **第一阶段：SpanTREx（基于跨度的联合抽取）**
  - 枚举文本中长度不超过 7 个 token 的所有连续跨度作为候选实体；
  - 使用临床预训练模型 BioMedBERT 获得每个 span 的表示：拼接该 span 起始 token、结束 token 的嵌入及 span 宽度嵌入；
  - 通过 FFN + softmax 对每个 span 进行实体类型分类（含 NOT-ENTITY）；
  - 对非空实体两两配对，构造关系分类表示：拼接两个 span 的嵌入、元素积、预测的实体类型嵌入，以及两个 span 之间的最大池化上下文表示；
  - 使用另一个分类器对关系类型（Before/After/Overlap/NO-RELATION）打分；
  - 训练采用联合损失 L = Ln + Lr（实体交叉熵损失 + 关系交叉熵损失）。
- **长文档处理——滑动窗口**：
  - 以固定窗口大小（与 BioMedBERT 限制一致，512 token）和一定步长滑动读取长文档，保证每个 token 能从唯一窗口中得到最终上下文增强表示，缓解模型长度限制。
- **第二阶段：构建文档级异质图（Heterogeneous Graph）**
  - 实体节点：SpanTREx 预测的非 NOT-ENTITY 跨度成为实体节点，节点类型等于预测实体类型；
  - 高置信度关系边：仅保留关系预测概率高于阈值 τ 的 TLink 作为初始边，避免噪声传播；
  - 上下文节点：对一定 token 距离内的跨度对，插入表示区间信息的 context 节点，节点特征为两实体间词向量的最大池化；该设计用于建模局部依赖；
  - 窗口节点（全局地标）：每个滑窗对应一个 WINDOW 节点，用该窗的 [CLS] 嵌入初始化；实体与其所在窗口按实体类型通过特定边相连，窗口节点按文本顺序相连。这些节点用于汇聚远距离信息并帮助推断传递性关系。
- **第三阶段：HGT 图传播与最终预测**
  - 利用异质图 Transformer（HGT）在实体节点、上下文节点、窗口节点之间进行相互注意力、消息传递和聚合，获得结构增强的节点表示；
  - 将图精化后的实体表示与原始 span 嵌入做加权残差连接，再送入关系解码器进行最终的时间关系判定；
  - 整个模型端到端训练，可以挖掘出一些 SpanTREx 无法发现的长期隐含关系。

## 3. 实验设计

- **主要数据集（Benchmark）**：
  - **I2B2 2012 Temporal Relations Challenge corpus**：310 份出院小结，官方划分为 190 训练 / 120 测试；本文另从训练集抽 9 份作为开发集。实体包括临床事件、时间表达式、SECTIME；关系含 Before/After/Overlap，可在事件-事件、事件-时间、时间-时间之间。
  - **E3C corpus（English subset）**：欧洲临床病例语料，规模较小；本文保留大多数 EVENT-EVENT TLink（训练/开发/测试划分见附录），用于检验跨数据集泛化能力。
- **评估指标**：
  - I2B2 2012 主指标为基于时间闭包的 tempeval F1（考虑传递性和可逆性），辅助给出实体识别（EI）和实体类型（EC）指标；
  - E3C 使用 micro-F1 评估实体和关系。
- **对比方法**：
  - 早期规则+机器学习系统：Xu et al. (2013)、Tang et al. (2013)；
  - 生成式框架：REBEL+BART；
  - 多头注意力方法（Miller et al., 2023，此前 THYME 上 SOTA）；
  - 联合抽取 baseline：SPERT；
  - 本文自身消融：SpanTREx（无 HGT 部分）；
  - 附录中还报告了基于 BioMedBERT-UMLS 实体抽取 + Zhong & Chen 关系分类的流水线对比，以及不同编码器的对照。
- **主结果**：
  - 在 I2B2 2012 上，GraphTREx 取得 tempeval F1 = 68.81%，比此前最好水平（Xu et al., 2013：63.36%）提高约 5.45 个百分点；
  - GraphTREx 相比无图模块的 SpanTREx（F1 = 66.63%）也高出约 2.2%，且文档级 F1 差异统计显著（p = 4.26×10⁻⁶；原文写 p-value = 4.26 × 10^−9？应为 10^-9？文本中有“p-value = 4 .26 × 10 −9”注意原文是 10^−9 吗？可能因为 text 中“4 .26 × 10 −9”其实是 10^-9；需要确认。我按原文：paired t-test p-value = 4.26 × 10^−9）。
  - E3C 上 GraphTREx 的 TLink F1 = 23.48%，显著高于 SPERT（13.63%）和多头注意力（3.97%），说明方法具有一定泛化性。

## 4. 资源与算力

- 论文在附录中说明：**所有实验均基于单张 NVIDIA-A100 GPU**，没有提多卡数量。
- 训练耗时：GraphTREx 约 10.8 小时（正文正文也说大约 11 小时）；SpanTREx 约 7.3 小时。
- 推理耗时：GraphTREx 平均每篇文档约 14 秒，120 篇完整 I2B2 测试集约需 30 分钟。
- 额外计算/参数信息见附录表 S5，但该表排版较混乱，读者可参考原文，这里不转述未确认的数字。
- 需要指出：论文并未详细报告预训练模型的能耗或完整参数量，只给了有限的训练/推理时间指标。

## 5. 实验数量与充分性

- **实验数量较多、覆盖角度较全面**：
  - 在 I2B2 2012 上的端到端抽取主实验（表 1）；
  - E3C 泛化实验（表 2）；
  - 长距离关系性能分析（按实体间隔距离分层：d=0、d>0、d>1，表 3）；
  - SpanTRex 的配对嵌入组成部分消融（上下文、预测实体类型、翻转关系增强，图 4）；
  - 图节点类型消融（实体/上下文/窗口节点，表 4）；
  - 不同基础编码器（BERT、RoBERTa、Clinical-Longformer）对比（表 5）；
  - 不同关系类别（Before/After/Overlap）上的性能拆解（表 6）；
  - 附录中还提供：不同临床预训练编码器对比、UMLS 知识融合的 BioMedBERT-UMLS、流水线 baseline、E3C 上的图节点消融、定性案例图、距离与可扩展性分析等。
- **结论评估**：
  - 整体实验设计较为系统和客观：主对比、消融、距离长尾、跨数据集验证和定性分析均有体现；
  - 但并未在所有公开临床时间关系语料上验证（如 THYME 因许可限制未使用）；
  - E3C 语料规模小、标注稀疏，因此只能作为初步泛化验证；
  - 消融实验中选择性只报告局部 F1 或特定子场景，仍可以看出图模块在长距离关系上的显著增益支持了核心假设。

## 6. 主要结论与发现

- GraphTREx 在 I2B2 2012 端到端时间关系抽取上取得新的 SOTA，tempeval F1 为 68.81%，比此前最好方法显著提升；
- 长距离（跨窗口、跨句子）关系抽取受益最大：在 d>1 的远距离实体对上，GraphTREx 相比 SpanTREx 提升约 8.9%，说明全局图传播有助于推断隐含传递性关系；
- 异质图节点对局部与全局信息均有贡献：上下文节点提升局部关系，窗口节点（全局地标）帮助长距离关系，二者结合效果最好；
- 基于滑动窗口 + span 表示 + 额外的上下文提示显著优于传统流水线或仅局部建模的方法；
- 在 E3C 语料上也优于多个强 baseline，展示出跨数据集的一定泛化能力；
- 定性分析发现，图结构可以修正金标中的传递性矛盾，并且在金标遗漏实体时仍能识别有意义的指称事件。

## 7. 优点

- **端到端联合建模**：将实体与关系抽取放入同一框架，利用 span-based 方法减少传统 token 序列标注的级联错误；
- **针对长文档设计**：滑动窗口保留局部上下文，HGT + 窗口节点进行全局信息传播，有效弥补 Transformer 上下文长度限制；
- **

针对长文档设计**：滑动窗口保留局部上下文，HGT + 窗口节点进行全局信息传播，有效弥补 Transformer 上下文长度限制，且实验证明对跨句、跨窗口的远距离关系增益显著；
- **结构信息与文本信息互补**：实体节点、上下文节点和窗口节点的异质图设计，使模型能够既显式建模“两实体间局部文本”，又隐式聚合“文档级全局证据”，比纯序列模型更利于推断传递性时间关系；
- **实验验证扎实**：覆盖主实验、跨语料泛化、长距离分层分析、多组消融和不同编码器对比，且统计检验支撑了核心结论；
- **附带实用的工程细节**：报告了训练/推理时间、单卡实验环境等，便于他人复现与估计资源消耗。

## 8. 缺点与局限性

- **计算开销较大**：约 10.8 小时训练 + 每篇文档 14 秒推理，在单卡 A100 上尚可接受，但多窗口候选跨度枚举与图传播使其扩展性存疑，距真实大规模临床语料部署仍有差距；
- **对比 baseline 略显陈旧**：I2B2 2012 上的主要对比对象是 2013 年左右的方法，对近年基于 Transformer 的联合抽取模型仅在 E3C 上做了少量对比，缺少更多同类端到端系统的并列评测；
- **绝对性能仍有提升空间**：68.81% 的 tempeval F1 虽为 SOTA，但离高准确率的临床应用仍有明显距离；E3C 上 TLink F1 = 23.48% 也表明跨语料/跨机构的泛化能力相当有限；
- **图构建依赖候选质量与阈值**：图中只保留置信度高于阈值 τ 的初始边，τ 的设定对最终结果及消融表现影响较大，但论文未深入讨论其敏感性；
- **实体 span 长度上限较硬**：候选跨度限制在 7 个 token 内，较长的时间表达式或复合临床事件指称可能被系统性遗漏；
- **对标注噪声的处理不足**：论文利用图传播“修正”了少量金标矛盾，但也揭示出训练数据本身噪声较高；模型对这些噪声缺乏显式建模，性能上限可能受限于标注不一致；
- **未涉及 THYME 等更广泛语料**：受许可限制未使用 THYME，使得与某些既有 SOTA 的直接比较缺乏说服力；
- **部分分析与结论依赖特定实现细节**：例如滑动窗口的步长、窗口节点连接方式、加权残差系数等，论文没有给出系统的超参数敏感性实验，复制到新语料时可能需要进行较多调参。

## 9. 综合评价

GraphTREx 是一篇思路清晰、实现完整的工作：它准确把握了临床时间关系抽取中“局部信息容易获取、全局关系难以建模”的痛点，提出 span-level 联合抽取 + 文档级异质图传播的两阶段方案，并在 I2B2 2012 这一标准语料上取得了可验证的提升。尤其值得肯定的是，作者通过距离分层实验，证明图模块确实有效解决了长距离关系推断问题，而非仅仅依靠更强的编码器带来整体提升。少量明显的不足在于计算代价偏高、与最新端到端方法的对标尚不够充分、以及跨语料泛化能力距离实际应用仍远。总体而言，该论文研究设计规范、实验证据较充分，结论稳健，对 NLP 与临床信息学交叉领域有一定参考价值。

（完）
