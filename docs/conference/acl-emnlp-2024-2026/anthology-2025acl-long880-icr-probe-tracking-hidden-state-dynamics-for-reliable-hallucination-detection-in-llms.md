---
title: "ICR Probe: Tracking Hidden State Dynamics for Reliable Hallucination Detection in LLMs"
title_zh: ICR探针：追踪隐藏状态动态以实现大语言模型的可靠幻觉检测
authors: "Zhenliang Zhang, Xinyu Hu, Huixuan Zhang, Junzhe Zhang, Xiaojun Wan"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.880.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 追踪各层隐藏状态更新中的信息贡献（ICR）来判别模型输出是否幻觉，是对输出正确性的隐藏状态探测。
tldr: 现有基于隐藏状态的幻觉检测大多使用静态孤立表征而忽略跨层动态。该论文关注隐藏状态的更新过程，提出ICR分数，用于量化各模块对残差流中信息更新的贡献。通过在幻觉判别任务上的实证，作者验证了ICR分数能够有效稳定地区分幻觉输出与非幻觉输出，为通过内部状态预测回答可信度提供了动态探针新思路。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1576, \"height\": 940}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 730, \"height\": 465}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 776, \"height\": 468}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 763, \"height\": 436}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1666, \"height\": 586}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 775, \"height\": 520}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 774, \"height\": 521}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 776, \"height\": 468}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long880/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 771, \"height\": 465}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1292, \"height\": 791}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 773, \"height\": 250}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 773, \"height\": 272}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 786, \"height\": 935}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 249}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 741, \"height\": 139}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1032, \"height\": 268}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1328, \"height\": 437}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1096, \"height\": 360}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long880/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1099, \"height\": 364}]"
motivation: 既有隐藏状态幻觉检测局限于静态表征，没有利用跨层演化的信息，致使其可靠性受限。
method: 提出ICR分数，刻画模块对隐藏状态或残差流更新的信息贡献，利用层间动态信息来区分幻觉。
result: 实验证明ICR分数在区分幻觉内容方面有效且可靠，优于静态表征方法。
conclusion: 将隐藏状态探测从静态表征转向动态更新过程，可为幻觉检测和可信度估计带来更稳健的信号。
---

## Abstract
Large language models (LLMs) excel at various natural language processing tasks, but their tendency to generate hallucinations undermines their reliability. Existing hallucination detection methods leveraging hidden states predominantly focus on static and isolated representations, overlooking their dynamic evolution across layers, which limits efficacy. To address this limitation, we shift the focus to the hidden state update process and introduce a novel metric, the **ICR** Score (**I**nformation **C**ontribution to **R**esidual Stream), which quantifies the contribution of modules to the hidden states’ update. We empirically validate that the ICR Score is effective and reliable in distinguishing hallucinations. Building on these insights, we propose a hallucination detection method, the ICR Probe, which captures the cross-layer evolution of hidden states. Experimental results show that the ICR Probe achieves superior performance with significantly fewer parameters. Furthermore, ablation studies and case analyses offer deeper insights into the underlying mechanism of this method, improving its interpretability.

---

## 论文详细总结（自动生成）

# 论文详细总结：ICR Probe: Tracking Hidden State Dynamics for Reliable Hallucination Detection in LLMs

## 1. 核心问题与研究动机

- 大语言模型（LLM）在各类 NLP 任务上表现优异，但生成内容中常出现幻觉，严重影响可靠性和可信度。
- 现有幻觉检测方法主要分为三类：
  - 基于输出一致性或外部参考的方法，需要多次采样或引入参考文本；
  - 基于 logit 概率的方法，对模型内在信号利用不足；
  - 基于隐藏状态的方法，虽然无需外部参考，但大多只关注**静态、孤立的表征**，忽视了隐藏状态在层与层之间的**动态演化过程**。
- 论文的核心观点是：隐藏状态的**更新过程**而非静态向量本身，可能与幻觉产生机制更密切相关。因此作者提出从“残差流更新”入手，构建新的检测信号和检测器，以突破现有方法的限制。

## 2. 方法论

### 核心思想

- 在 transformer 每一层中，隐藏状态的更新来自两个模块的贡献：
  - MHSA（多头自注意力）负责从上下文重分配已有信息，可视为“上下文路由器”；
  - FFN（前馈网络）从参数中检索事实知识，可视为“键值记忆库”。
- 不同层中两个模块的主导程度不同，因此残差流更新会呈现层间动态变化。作者将这种动态变化量化为 **ICR Score（Information Contribution to Residual Stream）**，并在此基础上训练轻量检测器 **ICR Probe**。

### ICR Score 的计算步骤

1. **提取注意力分数**
   - 计算每个 token 对所有上下文中 token 的注意力分数，再对所有注意力头取平均，得到向量 Attn。
2. **识别隐藏状态更新方向**
   - 定义第 `ℓ` 层 token `i` 的隐藏状态更新：`Δx = a + m`，其中 `a` 是 MHSA 贡献，`m` 是 FFN 贡献；
   - 将 `Δx` 投影到各 token 的隐藏状态 `x_j` 上，计算投影长度 `p = (Δx^T x_j) / ||x_j||`；
   - 对所有 token 的投影长度做 softmax，得到投影分布 Proj。
3. **计算一致性**
   - 取注意力分数最高的 top-k 个 token，计算 Proj 与 Attn 的 **Jensen-Shannon Divergence（JSD）**，即得到该 token 在该层的 ICR Score。
- **ICR Score 的解释**：
  - 分数偏小：隐藏状态更新方向与注意力分布高度一致，说明 MHSA 主导更新，FFN 更多是加强已有信息；
  - 分数偏大：表示更新偏离注意力分布，FFN 在注入新的参数化知识方面更为主导。

### ICR 特征的经验验证

- ICR Score 在各数据集上呈现稳定的逐层变化模式：早期层分数低（MHSA 主导），中间层分数高（FFN 主导、知识注入），深层分数回落（MHSA 再次主导），且标准差窄，说明特征具有跨数据集稳定性。
- 在 HaluEval 上，直接用 ICR Score 做检测，多个层的 AUROC 超过 0.7，层 11 峰值达到 0.7690，且概率密度分布显示幻觉与非幻觉样本可分。

### ICR Probe

- 将原始 `N×L` 的 ICR 矩阵按 token 求平均，得到 `1×L` 向量，作为分类器输入。
- 分类器为极轻量 MLP，结构为 `L→128→64→32→1`，使用 Leaky ReLU、批归一化、Dropout，输出经 sigmoid 得到非幻觉概率。
- 参数总量约 16K，远小于 SAPLMA 的 110K；训练一次即可用于实时、单次生成的幻觉检测。

## 3. 实验设计

### 模型与数据集

- **模型**：三个主流开源指令模型：Gemma-2-9B-it、Qwen2.5-7B-Instruct、Llama-3-8B-Instruct；附录补充 Qwen2.5-3B 和 Qwen2.5-14B，用于验证模型规模泛化性。
- **数据集**：每个模型使用四个任务：
  - HaluEval（幻觉检测基准）；
  - SQuAD（阅读理解）；
  - TriviaQA（常识问答）；
  - HotpotQA（多跳问答）。
  - 每个数据集随机采样 10,000 条，按 80/20 划分训练与测试。

### 对比方法

- **无训练方法**：PPL、LN-Entropy、LLM-check；
- **基于训练的方法**：SAPLMA（隐藏状态探针）、SEP（语义熵探针）；
- 附录还补充了 Semantic Entropy（Kuhn et al., 2023）作为额外基线。
- 所有基线均采用与 ICR Probe 相同的数据划分和实验设置。

### 评估指标

- 幻觉检测被建模为二分类任务，使用 **AUROC**（阈值无关指标）。

## 4. 资源与算力

- 论文的实验说明中明确写到了计算基础设施：
  - 10 张 NVIDIA GeForce RTX 3090 GPU（单卡 24 GB）；
  - CUDA 12.0、Ubuntu 20.04.5 LTS；
  - 多轮实验总计约 **600–800 GPU 小时**。
- 除此之外，论文没有提供每个单独实验更细化的训练时长或内存消耗。

## 5. 实验数量与充分性

论文实验数量较为丰富，包含多个维度的验证：

- 主实验：3 个模型 ×4 个数据集，共 12 组结果；
- 跨数据集泛化实验：在 Gemma-2 上做了完整的训练集↔测试集组合热图；附录补充了 Qwen2.5 和 Llama-3 的跨数据集矩阵；
- 跨模型规模实验：Qwen2.5-3B 和 Qwen2.5-14B；
- ICR Score 组件消融：仅投影、投影+注意力、无信号；
- 层分组消融：去掉早期层、中间层、深层，观察性能变化；
- 超参数 k 消融：k=5, 20, 30, ALL；
- 探针网络结构消融：隐藏层数 1–5；
- Token 级别案例研究，展示关键 token 的检测概率。

从整体看，实验设计比较充分，既覆盖了不同模型、不同数据集，也包含泛化性和消融分析；对基线的实验设置也与本文保持一致，通常可以说比较公平。不过需要注意：核心消融（表 2、表 3、k 选择等）多以 Gemma-2 为主，虽然主实验覆盖三个模型，但跨层的系统消融并未所有模型上完整重复，这在一定程度上限制了泛化结论的全面性。

## 6. 主要结论与发现

- ICR Score 能够稳定、一致地刻画模型残差流的层间更新模式，并具有区分幻觉输出的能力；
- ICR Probe 在大部分数据集和模型设置上显著优于 PPL、LN-Entropy、LLM-check、SAPLMA、SEP 等基线；
- 跨数据集的平均性能下降：ICR Probe 为 8.61%，显著小于 SAPLMA（10.18%）和 SEP（11.67%），表明其更依赖模型内在机制而非数据集表层特征；
- 层消融实验显示：中间层的信息贡献对幻觉检测最为重要，去掉中间层会导致性能大幅下降；
- 组件消融显示：仅使用投影方向的熵已能获得较好检测效果；融合注意力信号后性能进一步提升，说明两者互补；
- Token 级案例表明，ICR Probe 对关键内容词（如数字、实体）的幻觉检测有效，但对低频、无信息量的虚词仍存在误判，可作为后续改进方向。

## 7. 优点

- **新颖视角**：将幻觉检测的关注点从静态隐藏状态转向隐藏状态在残差流中的更新过程，具有较好的原创性和可解释性；
- **构建逻辑清晰**：参考已有机制分析（MHSA 与 FFN 分工、不同层主导性差异），将更新方向与注意力分布之间的 JS 散度定义为检测信号，直觉合理；
- **指标稳定**：ICR Score 在多个数据集上表现出窄标准差，说明其反映的是模型内在规律而非数据集噪声；
- **检测器轻量**：ICR Probe 只有约 16K 参数，远小于 SAPLMA 等基线，且支持单次前向过程的实时检测，无需多次采样或外部参考；
- **泛化性验证充分**：跨数据集、跨模型规模实验表明该方法具有较强的可迁移性；
- **可解释性较好**：通过逐层特征分析、层消融和 token 案例，论文揭示了“FFN/MHSA 主导性差异”与幻觉之间的关联，使检测过程更具可理解性。

## 8. 不足与局限

- **依赖开源模型内部状态**：需要读取 hidden states 和注意力分数，无法直接用于 API 式闭源模型；
- **只做检测，不做缓解**：论文未提出基于该信号减少幻觉的具体干预方法；
- **实验任务类型有限**：虽使用了四个数据集，但整体仍以问答型、抽取型任务为主，对开放式长文本生成等更复杂场景的覆盖不足；
- **消融集中在单个模型**：部分关键超参和层消融主要在 Gemma-2 上完成，跨所有模型完整重复会更有说服力；
- **Token 级检测不稳定**：对高频虚词存在高概率误判，可能影响对回答局部内容的细致判断；
- **注意力分数与投影的近似度量仍存在简化**：例如 FFN 计算本身基于 MHSA 输出，ICR Score 只能从相关性和一致性角度间接推断模块贡献，无法彻底分离两类模块信息；
- 论文还提到，方法对需要细粒度归因或复杂推理链的任务可能还有待进一步验证。

（完）
