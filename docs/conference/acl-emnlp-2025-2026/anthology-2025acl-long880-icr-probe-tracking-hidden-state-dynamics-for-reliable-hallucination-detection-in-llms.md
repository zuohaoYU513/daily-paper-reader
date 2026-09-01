---
title: "ICR Probe: Tracking Hidden State Dynamics for Reliable Hallucination Detection in LLMs"
title_zh: ICR探针：跟踪隐藏状态动态以实现可靠的大模型幻觉检测
authors: "Zhenliang Zhang, Xinyu Hu, Huixuan Zhang, Junzhe Zhang, Xiaojun Wan"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.880.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: ICR探针跟踪跨层隐藏状态动态以检测幻觉
tldr: 基于隐藏状态的幻觉检测通常使用静态孤立表示，忽略了跨层动态变化。该工作提出信息贡献残差流分数(ICR Score)，量化各模块对隐藏状态更新的贡献，并构建ICR Probe进行检测。实验证明ICR Score能有效可靠地区分幻觉，相比静态表示方法显著提升检测性能，为幻觉检测提供新工具。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1576, \"height\": 940, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 730, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 776, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 763, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1666, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 775, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 774, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 776, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 771, \"height\": 465, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1292, \"height\": 791, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 773, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 773, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 786, \"height\": 935, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 741, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1032, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1328, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1096, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1099, \"height\": 364, \"label\": \"Table\"}]"
motivation: 现有隐藏状态幻觉检测多关注静态表示，忽略了跨层演化信息。
method: 提出ICR Score度量模块对残差流更新的贡献，并构建ICR探针检测幻觉。
result: 实验显示ICR Score有效区分幻觉，检测可靠性提升。
conclusion: 跟踪隐藏状态动态是增强幻觉检测可靠性的关键。
---

## Abstract
Large language models (LLMs) excel at various natural language processing tasks, but their tendency to generate hallucinations undermines their reliability. Existing hallucination detection methods leveraging hidden states predominantly focus on static and isolated representations, overlooking their dynamic evolution across layers, which limits efficacy. To address this limitation, we shift the focus to the hidden state update process and introduce a novel metric, the **ICR** Score (**I**nformation **C**ontribution to **R**esidual Stream), which quantifies the contribution of modules to the hidden states’ update. We empirically validate that the ICR Score is effective and reliable in distinguishing hallucinations. Building on these insights, we propose a hallucination detection method, the ICR Probe, which captures the cross-layer evolution of hidden states. Experimental results show that the ICR Probe achieves superior performance with significantly fewer parameters. Furthermore, ablation studies and case analyses offer deeper insights into the underlying mechanism of this method, improving its interpretability.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、核心问题与研究动机

论文针对大语言模型（LLM）中的**幻觉（Hallucination）问题**展开研究。LLM 虽然在各类 NLP 任务上表现优异，但生成不合事实或无意义内容的倾向严重削弱了其可靠性，因此幻觉的可靠检测成为关键需求。

现有基于隐藏状态（hidden states）的幻觉检测方法存在明显局限：

- **主流方法聚焦于静态、孤立的表示**（如某一层或某几个层的嵌入向量），忽略了隐藏状态随层数增加的动态演化过程；
- 隐藏状态维度高（约 4000 维），直接作为特征会限制信息提取能力；
- 难以捕捉残差流（residual stream）跨层的更新与演化，从而制约了检测性能。

论文的核心主张是：**将关注点从隐藏状态本身转向其逐层更新过程**，通过量化各模块对隐藏状态更新的贡献来实现更可靠的幻觉检测。

## 二、方法论

### 2.1 核心思想

受既有机制可解释性研究启发（FFN 和 MHSA 在不同层发挥不同作用），论文提出 **ICR Score（Information Contribution to Residual Stream，信息贡献残差流分数）**，用于量化每个层中多头自注意力（MHSA）和前馈网络（FFN）对隐藏状态更新的相对贡献，并基于此构建 **ICR Probe** 分类器进行幻觉检测。

### 2.2 ICR Score 的计算流程

在 transformer 解码器的第 ℓ 层，隐藏状态按如下方式更新：

```
xℓi = xℓ−1i + aℓi + mℓi
```

其中 `aℓi` 为 MHSA 的贡献，`mℓi` 为 FFN 的贡献，总更新量 `∆xℓi = aℓi + mℓi`。

ICR Score 的计算分为三步：

1. **提取注意力分数**（Extracting Attention Scores）：计算第 i 个 token 在所有注意力头上对各上下文 token 的平均注意力分布 `Attnℓi`；
2. **识别隐藏状态更新方向**（Identifying the Update Direction）：计算更新向量 `∆xℓi` 在输入上下文各 token 隐藏状态方向上的投影长度，经 softmax 归一化后得到投影分布 `Projℓi`；
3. **计算一致性**（Computing Consistency）：使用 **Jensen-Shannon Divergence (JSD)** 度量投影分布与注意力分布之间的差异：

```
ICRℓi = JSD(Projℓi, Attnℓi)
```

（实际计算时选取注意力分数最高的 top-k = 20 个 token，以减少噪声干扰。）

**ICR Score 的解释：**

- **较小的 ICR 分数**：隐藏状态更新与注意力分布高度一致，说明 MHSA 主导更新，FFN 主要起强化作用；
- **较大的 ICR 分数**：更新方向与注意力分布显著偏离，说明 FFN 主导更新，注入更多参数化知识。

### 2.3 ICR Probe 的构建

- 将原始 `N × L` 的 ICR 矩阵在 token 维度上做平均池化，得到 `1 × L` 的向量；
- 输入一个轻量级 MLP 分类器（结构为 `L → 128 → 64 → 32 → 1`，含 BatchNorm、Dropout 和 Leaky ReLU 激活）；
- 输出为 0-1 之间的标量，表示生成内容为非幻觉的概率；
- **参数量仅约 16K**，显著低于 SAPLMA 的 110K。

## 三、实验设计

### 3.1 评估模型与数据集

- **模型**：Llama-3-8B-Instruct、Qwen2.5-7B-Instruct、Gemma-2-9B-it（另有 Qwen2.5-3B/14B 补充实验）；
- **数据集**：HaluEval（幻觉检测基准）、SQuAD（阅读理解）、TriviaQA（常识问答）、HotpotQA（多跳问答）；
- **评估指标**：AUROC（阈值无关的二元分类指标）；
- 每个数据集随机采样 10,000 条，按 80%/20% 划分训练/测试集，结果按各数据集分别报告。

### 3.2 对比基线

- **无训练方法**：PPL（困惑度）、LN-Entropy（长度归一化熵）、LLM-check（注意力核相似性分析）；
- **基于训练的方法**：SAPLMA（单一层隐藏状态探针）、SEP（语义熵探针）。

### 3.3 额外实验设计

- 跨数据集泛化实验（训练于一个数据集、测试于另一个数据集的热力图分析）；
- 组件消融（仅投影、投影+注意力）；
- 层级消融（移除早/中/深层组）；
- top-k 取值消融（k = 5/20/30/ALL）；
- 探针结构消融（隐藏层数 1-5）；
- token 级检测案例分析；
- 不同模型规模（3B/7B/14B）的对比验证。

## 四、资源与算力

论文在实验设置中有明确说明：

- **硬件**：10 块 NVIDIA GeForce RTX 3090 GPU（各 24GB 显存）；
- **软件环境**：CUDA 12.0、Ubuntu 20.04.5 LTS；
- **总计算预算**：跨多轮实验合计约 **600-800 GPU 小时**。

此外，论文未报告单一实验的具体训练时长或单次推理的耗时细节。

## 五、实验数量与充分性

### 5.1 实验数量

论文实验覆盖面较广，主要包括：

- **主实验**：3 个模型 × 4 个数据集 = 12 组完整对比实验；
- **泛化实验**：每模型 4×4 交叉数据集热力图评估；
- **模型规模实验**：额外覆盖 3B、14B 两个规模；
- **消融实验**：至少 4 组（组件消融、层级消融、k 值消融、结构消融）；
- **案例分析**：token 级别的幻觉检测实例。

### 5.2 充分性评价

- **客观性较好**：与基线方法采用完全一致的实验设置和数据划分，对比公平；
- **消融设计合理**：逐步验证了 ICR Score 各组成部分的必要性和不同层组的贡献；
- **泛化验证充分**：多种跨数据集组合以及与不同规模模型的结合，增强了结论的可信度；
- **小幅不足**：未报告多次运行的标准差/置信区间（仅提及多次运行取平均），且基准数据集均为问答类任务，缺少开放式生成或对话任务的评估。

## 六、主要结论与发现

1. **ICR Score 是稳定可靠的检测信号**：跨数据集呈现出高度一致的逐层演化模式（早期 MHSA 主导 → 中期 FFN 主导 → 后期回归 MHSA），窄标准差带证实了其稳定性；
2. **ICR Score 具有区分能力**：单层 ICR Score 直接用于分类即可达到较高 AUROC（如 HaluEval 上最佳层达 0.7690），概率密度分布显示幻觉与非幻觉样本明显可分；
3. **ICR Probe 全面优于基线**：在 12 组主实验中全部优于所有基线方法，平均提升显著；
4. **跨数据集泛化能力强**：与 SAPLMA 和 SEP 相比，域迁移平均 AUROC 下降最小（仅 8.61%）；
5. **参数效率极高**：仅 16K 参数即可超越 110K 参数的 SAPLMA；
6. **中层对检测最关键**：移除中间层（15-28）导致性能下降最大，验证了该层段信息贡献的重要性；
7. **token 级检测具有选择性**：对答案关键 token 敏感（能识别核心信息的幻觉），但对高频无信息 token 容易误判。

## 七、优点

- **新颖的检测视角**：从静态表示转向动态演化过程，填补了现有方法忽略跨层更新模式的空白；
- **理论支撑扎实**：基于残差流更新机制和 FFN/MHSA 功能分化的可解释性研究，方法有据可依；
- **参考无关（reference-free）**：无需外部知识库或多轮采样，单次前向传播即可检测；
- **参数高效且扩展性好**：16K 参数、全自动池化，无需人工选择特定层或 token；
- **无需多次生成**：与依赖多代采样的语义熵方法相比，计算开销大幅降低；
- **可解释性强**：层间模式分析、消融实验和案例研究共同揭示了方法的内部机理；
- **跨模型规模鲁棒**：在 3B、7B、14B 模型上均稳定优于基线。

## 八、不足与局限

- **仅适用于开源模型**：方法需要访问模型内部隐藏状态和注意力权重，无法直接应用于 API 形式的闭源商用模型；
- **仅检测、不缓解**：论文只解决幻觉的识别问题，不涉及幻觉的抑制或修正，实际应用价值有限；作者也承认期待未来工作基于 ICR Score 做残差流干预；
- **数据集覆盖有限**：实验集中于 QA 类任务，缺少开放性生成、多轮对话、RAG 场景等更复杂任务的验证（泛化实验中也看到 Llama-3 在 TriviaQA 上跨域性能明显下降至 0.5658-0.5933，说明存在一定的域敏感性）；
- **token 级检测偏置**：对高频无信息词（如冠词、标点）的误判率较高，token 级应用受限；
- **k 值需人工设定**：虽然 k=20 在实验中表现稳定，但最佳 k 值可能随模型或任务变化，引入了一定的超参数依赖；
- **未报告统计显著性检验**：论文未说明多次运行结果的方差或置信区间，难以判断性能差异的统计显著性。

---

（完）
