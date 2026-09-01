---
title: Mitigating Hallucinations in Large Vision-Language Models without Performance Degradation
title_zh: 在不损失性能的前提下缓解大视觉语言模型幻觉
authors: "Xingyu Zhu, Junfeng Fang, Shuo Wang, Beier Zhu, Zhicai Wang, Yonghui Yang, Xiangnan He"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.89.pdf"
tags: ["query:hallu-rag"]
score: 6.0
evidence: 多模态大模型幻觉缓解方法，可迁移至大语言模型幻觉治理
tldr: 大视觉语言模型常产生幻觉，直接基于标注数据微调成本高，现有表示级缓解方法又可能损害通用生成能力。论文提出双阶段框架MPD，通过更完整地提取幻觉成分并选择性更新参数，在缓解幻觉的同时保持生成性能。实验表明该方法能有效降低幻觉而不带来性能退化，为多模态大模型的可靠性优化提供了更优方案。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long89/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long89/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 646, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long89/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1411, \"height\": 799, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long89/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 759, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long89/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 536, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long89/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 537, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long89/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 535, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long89/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 535, \"height\": 388, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1454, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1328, \"height\": 1132, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 833, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 764, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 637, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1436, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1225, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1246, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 693, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 824, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 781, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long89/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 798, \"height\": 318, \"label\": \"Table\"}]"
motivation: 大视觉语言模型幻觉频发，现有表示级缓解方法会因幻觉成分提取不完整而损害通用能力。
method: 提出双阶段MPD框架，更完整地提取隐藏表示中的幻觉成分，并通过选择性参数更新缓解幻觉。
result: 实验显示MPD能缓解多模态模型幻觉且不造成通用生成性能下降。
conclusion: 精细化幻觉成分提取与选择性更新可兼顾多模态大模型的可靠性与通用能力。
---

## Abstract
Large Vision-Language Models (LVLMs) exhibit powerful generative capabilities but frequently produce hallucinations that compromise output reliability. Fine tuning on annotated data devoid of hallucinations offers the most direct solution, while its high computational cost motivates recent representation-based methods, which focus on mitigating hallucinatory components within hidden representations. Though efficient, we empirically observe that these methods degrade general generation capacity due to incomplete extraction of hallucination components and non-selective parameter updates. To address these limitations, we propose MPD, a dual-stage framework for mitigating hallucinations without performance degradation. Specifically, our MPD relies on two essential factors: (1) semantic-aware component disentanglement to extract pure hallucination components, and (2) interpretable parameter updates that selectively modify parameters most relevant to hallucination. Extensive experiments demonstrate that MPD achieves state-of-the-art performance, reducing hallucinations by 23.4% while maintaining 97.4% of general generative capability as evaluated on LLaVA-Bench and MME, with no additional computational cost.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

大视觉语言模型（LVLMs）在跨模态理解和生成方面能力强大，但普遍存在“幻觉”现象——生成文本描述与图像视觉内容系统性不一致，例如虚构不存在的物体、错误归因视觉属性、幻觉空间关系等。这不仅影响实际应用中的视觉-语言对齐精度，也可能导致错误信息传播和安全隐患。

现有缓解幻觉的方法主要分为两类：
- **基于微调的方法**：通过对无幻觉标注数据进行微调，效果直接但成本高昂、依赖人工标注；
- **基于表示干预的方法**：通过对比幻觉输出与忠实输出的隐藏表示，提取幻觉成分并更新模型参数来抑制幻觉。该类方法避免了大规模数据重建，但本文指出其存在两个关键缺陷：
  1. **幻觉成分提取不完整**：幻觉语义与通用语义高度耦合，现有方法容易误删通用语义成分，导致后编辑模型的隐藏表示分布偏离原始分布；
  2. **参数更新非选择性**：大量权重被全局扰动（如Nullu在LLaVA上会修改数亿参数），容易引发过拟合并破坏原有参数分布。

因此，本文的核心目标是：**在不降低通用生成能力的前提下，高效缓解LVLMs的幻觉现象**，填补效率与效果之间的鸿沟。

## 2. 方法论：MPD框架

论文提出 **MPD（Mitigating hallucinations without Performance Degradation）**，一个双阶段框架，核心思想是：**更纯净地提取幻觉成分 + 更精准地选择性更新参数**。

### 2.1 阶段一：语义感知的幻觉成分解耦（Semantic-aware Component Disentanglement）

- 利用辅助LLM构造对比查询对：每个图像配有**忠实描述**（`x+`）和**幻觉诱导描述**（`x−`）。
- 在LLM各层提取token级隐藏表示，并对序列取平均，得到矩阵 `X+_ℓ` 和 `X−_ℓ`。
- 假设幻觉表示分解为：`X− = X_real + X_hall + ϵ−`，其中 `X_real` 是真实语义，`X_hall` 是幻觉成分，`ϵ−` 是噪声。
- 对忠实表示 `X+_ℓ` 进行SVD，取前C个奇异向量构成子空间，投影矩阵 `P = U U^T`。
- 通过正交投影提取幻觉成分：`\tilde{X}_ℓ = (I − P) X−_ℓ`，即剔除与忠实语义子空间平行的部分，仅保留正交的幻觉信号。

### 2.2 阶段二：可解释的参数选择性编辑（Interpretable Parameter Editing）

- **参数选择**：针对目标层权重矩阵 `W_ℓ`，计算每个权重向量与幻觉成分 `\tilde{X}_ℓ` 的平均余弦相似度，选出相似度最高的前K个权重向量作为编辑目标。
- **参数编辑**：构造正交补空间投影算子 `\tilde{Q} = I − \tilde{X}^T (\tilde{X} \tilde{X}^T)^{-1} \tilde{X}`，将这些被选中权重投影到幻觉子空间的正交补上，从而删除幻觉相关方向。
- 仅编辑少量关键权重（如LLaVA上约6000行权重），显著减少参数扰动（论文报道在mPLUG-Owl2上参数更新量减少42%，在MiniGPT4上减少37%）。

### 2.3 理论分析

论文在命题1中证明了：相比朴素差分估计 `X− − X+`，基于正交投影的残差 `(I−P)X−` 在估计解耦幻觉信号时具有更小的期望平方误差，因为后者避免了幻觉平行部分和噪声的干扰，能更精确地分离出真正独立的幻觉成分。

## 3. 实验设计

### 3.1 基准模型

- **MiniGPT-4 V2**
- **LLaVA-1.5-7B**
- **mPLUG-Owl2**

### 3.2 对比方法

- 解码/生成策略类：DoLa、OPERA、VCD
- 修正/解码类：LURE、HALC
- 表示干预类：Nullu（最强基线）

### 3.3 数据集与评测基准

| 类别 | 基准 | 指标 |
|---|---|---|
| 句级/实例级幻觉 | MSCOCO上的CHAIR | CHAIR_S、CHAIR_I、BLEU |
| 存在性问答 | POPE | Accuracy、Precision、Recall、F1 |
| 感知与推理 | MME | Existence、Count、Position、Color 四个子集 |
| 开放生成质量 | LLaVA-Bench | Accuracy、Detailedness（GPT-4V评分） |
| 细粒度幻觉 | HallusionBench | fACC、qACC、easyA、hardA、aACC |
| 额外验证 | OPOPE、AMBER、MMHalBench、V* Bench、MMMU、MathVision | 各基准对应指标 |

### 3.4 消融实验

- 编辑层范围的影响（16-32、18-32、...、30-32）
- 样本量变化（500到5000）
- 保留奇异值维度C（默认2500）
- 选择权重数量K（1×10^3 到 8×10^3）

## 4. 资源与算力

论文在实现细节中说明：所有实验在**单张A40 GPU（40G显存）**上完成，未提及多卡或训练时长。对比方法如OPERA、HALC的延迟较高，而MPD的推理延迟为3.7秒（接近Greedy的3.1秒），峰值GPU内存约15019MB，远低于OPERA（23742MB）和HALC（22135MB）。论文未报告参数编辑阶段的具体耗时，但强调**推理阶段无额外计算成本**。

## 5. 实验数量与充分性

论文实验较为丰富：

- **主实验**：在3个LVLM × 2个主基准（CHAIR、POPE）上进行了系统对比；
- **补充评测**：增加了OPOPE、AMBER、MMHalBench、HallusionBench、V* Bench、MMMU、MathVision，覆盖对象级幻觉、属性/空间幻觉、多模态推理等；
- **消融研究**：涉及编辑层范围、样本量、SVD保留维度、权重选择数量K；
- **效率对比**：报告了延迟、GPU内存、CHAIR_S；
- **案例分析**：展示了LLaVA-1.5在LLaVA-Bench上的定性对比。

整体实验设计较为充分，对比方法全面，指标多样。但存在一定不足：
- 所有实验仅在**7B规模及更小的模型**上验证，未涉及更大规模LVLM（如13B/34B）；
- POPE实验中仅报告了与“Original”和“Nullu”的对比，缺少与其他方法的POPE结果；
- 没有报告多次运行或显著性检验的详细信息（除了部分均值和标准差）。

## 6. 主要结论与发现

- MPD在CHAIR上显著降低幻觉：相比Nullu，在LLaVA-1.5-7B上CHAIR_S从15.20降至12.80，CHAIR_I从5.30降至4.20；在mPLUG-Owl2上同样取得最优。
- POPE上MPD在所有采样策略（random/popular/adversarial）下均取得最高F1分数，说明对复杂对抗场景有鲁棒性。
- 在LLaVA-Bench上，MPD同时提升Accuracy和Detailedness，表明不仅没有损伤生成质量，反而有所改善。
- MME上MPD在Existence和Count上取得最优，Position和Color保持竞争力。
- 隐藏表示分布分析显示，MPD编辑后的表示比Nullu更贴近原始分布，避免过度偏移。
- 总体概括：幻觉降低23.4%，通用生成能力保留97.4%，无额外推理成本。

## 7. 优点

- **兼顾效果与效率**：不同于微调方法，无需大规模标注数据；不同于解码类方法，无额外推理延迟。
- **方法论创新**：首次将“语义感知正交解耦”与“选择性参数编辑”结合，从理论上证明投影残差比朴素差分更准确。
- **参数更新量小**：仅编辑少量关键权重，大幅减少对原始模型的扰动，从而保持生成能力。
- **可解释性**：参数选择基于余弦相似度，直观且可操作。
- **实验充分且覆盖面广**：从对象级幻觉到属性/空间幻觉，再到数学推理基准，验证了方法的通用性。
- **效率对比清晰**：报告了延迟与GPU显存，说明实用性。

## 8. 不足与局限

- **计算资源信息不完整**：只说了用单张A40，没有提及编辑时间、总GPU小时数或对比方法的训练/编辑成本，难以完全评估实际开销。
- **模型规模有限**：仅实验了7B及以下模型，未验证在更大模型（如13B/34B）上的扩展性。
- **POPE实验对比不完整**：主文中POPE只对比了Original和Nullu，缺少与更多基线的横向对比，可能弱化说服力。
- **依赖辅助LLM生成对比数据**：需要额外使用GPT-3.5/GPT-5.1等模型构建对比对，尽管是一次性离线成本，但涉及外部API依赖和潜在偏差。
- **自动化基准的局限性**：论文自己也承认，CHAIR、POPE等基准可能无法完全反映长文连贯性、风格多样性以及模糊视觉输入下的表现。
- **编辑层、K、C等超参数需手动调节**：不同模型可能需要重新调参，实际使用中需要额外的验证成本。
- **理论假设较强**：命题1假设忠实表示能良好刻画grounded语义子空间，且噪声为高斯，在复杂真实分布中可能不完美。

（完）
