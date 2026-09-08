---
title: "Truth as a Trajectory: What Internal Representations Reveal About Large Language Model Reasoning"
title_zh: 真实即轨迹：内部表示揭示大语言模型推理
authors: "Hamed Damirchi, Imezadelajara, Ehsan Abbasnejad, Afshar Shamsi, Zhen Zhang, Javen Qinfeng Shi"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2073.pdf"
tags: ["query:metacognitio"]
score: 8.0
evidence: 基于轨迹的隐层分析揭示正确与错误推理结构，可用于预测输出正确性
tldr: 针对现有可解释性方法把隐状态当作静态点、线性探针只能学到表层词汇模式的问题，该文提出Truth as a Trajectory（TaT）：将Transformer推理展开为逐层迭代精化的轨迹，通过分析表示在层间的几何位移捕捉推理的结构模式。实验表明正确与错误推理在轨迹空间中的可分性强于单层静态探针。该方法为利用内部状态判断LLM生成正确性提供了更有效的几何表征工具。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2073/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 716, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2073/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 811, \"height\": 558, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2073/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 816, \"height\": 553, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 719, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 161, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 780, \"height\": 887, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 778, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 777, \"height\": 520, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1339, \"height\": 482, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 808, \"height\": 161, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1657, \"height\": 557, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1650, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1660, \"height\": 944, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1659, \"height\": 1153, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1660, \"height\": 939, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1658, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2073/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1661, \"height\": 881, \"label\": \"Table\"}]"
motivation: 单层静态隐状态分析难以分离正确与错误推理结构，线性探针容易依赖表层词汇。
method: 将Transformer推理视作层间迭代精化轨迹，用表示位移捕捉正确与错误推理的结构性差异。
result: TaT在推理任务上比静态线性探针更准确地区分正确与错误推理轨迹。
conclusion: 基于层间几何位移的轨迹分析能揭示LLM推理正确性信号，可用于事实正确性预测。
---

## Abstract
Existing explainability methods for Large Language Models (LLMs) typically treat hidden states as static points in activation space, assuming that correct and incorrect inferences can be separated using representations from an individual layer. However, these activations are saturated with polysemantic features, leading to linear probes learning surface-level lexical patterns rather than underlying reasoning structures. We introduce Truth as a Trajectory (TaT), which models the transformer inference as an unfolded trajectory of iterative refinements, shifting analysis from static activations to layer-wise geometric displacement. By analyzing displacement of representations across layers, TaT captures structural patterns in the evolution of inference that distinguish valid reasoning from spurious behavior. We evaluate TaT across dense and Mixture-of-Experts (MoE) architectures on benchmarks spanning commonsense reasoning, question answering, and toxicity detection. Without access to the activations themselves and using only changes in activations across layers, we show that TaT effectively mitigates reliance on static lexical confounds, outperforming conventional probing, and establishes trajectory analysis as a complementary perspective on LLM explainability.

---

## 论文详细总结（自动生成）

## 论文中文详细总结

### 一、论文核心问题与研究背景

- **核心问题**：现有 LLM 可解释性方法大多将隐状态视为激活空间中的**静态点**，假设在某一单层即可用线性方式区分正确与错误的推理。然而，Transformer 激活充满**多义性（polysemantic）特征**，导致线性探针学到的是**表层词汇模式**而非底层推理结构。
- **背景痛点**：
  - 线性表示假说（LRH）与基于静态激活的探针/激活操控方法，受限于对比样本和特定数据集，难以跨任务泛化。
  - 已有研究发现"真实性的几何结构（geometries of truth）"在不同任务间是正交的、任务特定的（Azizian et al., 2025）。
  - 探针的**层选择缺乏原则性**：有效的层通常只是模型中部一个狭窄区间，跨数据集表现不稳定。
  - 近期的动力学研究（如推理速度场、曲率推理）虽然指出了轨迹/运动学信号的存在，但仅在理想化、受控的逻辑结构中验证，未在真实基准上检验。
- **核心论点**：推理有效性是**动态属性**，应通过激活在层间计算轨迹上的几何位移来刻画，而非在单个静态层寻找可分方向。正确推理的轨迹编码了**跨任务不变的结构特征**，可作为任务无关的有效性检测信号。

---

### 二、方法论：Truth as a Trajectory (TaT)

#### 1. 核心思想
- 将 Transformer 推理过程**跨所有层和 token 展开为一条连续轨迹**，放弃"单层快照"视角。
- 分析对象从**原始激活本身**转为**逐层位移（layer-wise displacement）**，以消除静态词元身份、词法内容等高幅度持久成分的干扰，聚焦于残差流"正在被写入什么"（过程/机制）而非"存有什么"（记忆状态）。

#### 2. 关键公式与技术细节
- **残差更新**：$h_{\ell+1} = h_\ell + f_\ell(h_\ell)$（等价于求解 ODE 的 Euler 步）。
- **位移向量**：$d_{t,\ell} = h_{t,\ell+1} - h_{t,\ell}$
  - 动机：基于"特权基假设"（Privileged Basis Hypothesis），层间差分可衰减静态高频/持久成分，突出活性残差更新 $f_\theta(h_{t,\ell})$，降低多义性与叠加干扰。
- **轨迹序列构建**：将某个候选续写 $c_i$ 的所有 token $t$ 与所有层 $\ell$ 的位移向量按展开顺序拼接：
  $$S_i = [d_{1,0}, \dots, d_{1,L-1},\ d_{2,0}, \dots, d_{N_i,L-1}] \in \mathbb{R}^{M_i \times d},\quad M_i = N_i \times L$$
- **动力学建模**：采用轻量级 **LSTM** 对序列 $S_i$ 逐步建模（选择 LSTM 而非 Transformer 探针的原因：显式建模时序依赖 + 计算开销小）。最后隐状态 $z_{M_i}$ 经线性分类头输出有效性概率：
  $$\hat{y}_i = \sigma(W^T z_{M_i} + b)$$

#### 3. 前期探索：运动学描述符（Kinematic Descriptors）
作者先检验了简单直观的标量运动学量：速度 $v_\ell=\|\Delta h_\ell\|_2$、加速度、加加速度（jerk）、方向曲率、动力学曲率 $\kappa^{kin}_\ell = \|a_\ell\|_2 / \|v_\ell\|_2^2$、弧长 $S=\sum_{\ell=0}^{L-1}\|h_{\ell+1}-h_\ell\|_2$。
- **结论**：速度（velocity）携带一定预测信号，但没有任何单一标量描述符能在多个数据集上一致超过基础模型本身 → 必须使用**可学习模型**捕获高维轨迹中的非线性结构不变量。

---

### 三、实验设计

#### 1. 数据集与场景
- **推理/问答基准（8 个）**：ARC-Easy、ARC-Challenge、BoolQ、Hellaswag、OpenBookQA、StoryCloze、CommonsenseQA、CosmosQA、SocialIQA（含跨数据集 OOD 迁移评估）。
- **毒性检测**：
  - In-Distribution：RealToxicityPrompts
  - OOD（隐式/对抗性有害语言）：ToxiGen（设计上规避关键词依赖）。
- **任务格式**：给定 prompt + 候选续写，判定哪个候选正确/有毒，为受约束的选择任务以保证监督信号无歧义。

#### 2. 模型架构
- 稠密模型：Llama-3.1-8B、Qwen2.5-14B、Qwen3-32B
- MoE 模型：Qwen3-30B MoE

#### 3. 对比方法
- **基础模型本身**：zero-shot、few-shot（ICL）准确率。
- **线性探针（Linear Probe）**：中间层最后一 token 激活上训练（另报告 mid-to-late 层扫掠以及"事后最优层"oracle 探针）。
- **TaT (Raw)**：同一 LSTM 但输入为原始激活轨迹（位移消融对照）。
- **TaT (Disp.)**：本文方法（位移轨迹）。
- **LoRA（rank=16）**：参数高效微调基线，用于检验"是否只是学到更好的任务特定模型"。
- **Set MLP**：无序集合基线（验证时序性的必要）。
- **运动学描述符**：如速度、曲率等单独作为分类器。

#### 4. 主要实验组
1. 运动学描述符在 4 个基准上的判别力（Llama-3.1-8B + Qwen2.5-14B）。
2. 8 个推理数据集间的交叉迁移（Table 1 / Appendix Table 6，跨两种模型）。
3. 与 LoRA 的泛化对比（Table 2）。
4. 毒性检测（4 个模型 × 3 方法，Table 3）。
5. 位移 vs 原始轨迹消融（Table 4 + Appendix F）。
6. 轨迹网格消融：仅中层-全 token vs 最后 token-全层 vs 全网格（Table 5 + Appendix G）。
7. Set MLP 无序基线（Appendix H）。
8. 探针层敏感性 + Oracle 探针对比（Appendix I）。

---

### 四、资源与算力说明

- **论文正文未报告所使用 GPU 型号、数量与训练时长**，也未给出各实验的具体 wall-clock 时间。
- 附录 E 给出了**相对开销**的量化：在 Llama-3.1-8B（fp16）上，所增加的 LSTM 分类器参数量约 4.76M（占基础模型 0.06%），模型显存开销 18.1 MB（占 0.12%），朴素实现下推理时间约 10.5 ms（相对前向传播约 16%）；作者指出实际部署中可随层内联将其降至可忽略水平。
- 训练数据规模很小（如 ARC-C 约 2,000 样本即可完成训练），训练仅需一次，之后新任务只需推理。

---

### 五、实验数量与充分性评估

#### 实验数量
- 覆盖 **8 个推理基准 + 2 个毒性数据集**、**4 种模型架构**（2 稠密 + 1 大稠密 + 1 MoE），跨模型验证（Llama-3.1-8B 与 Qwen2.5-14B）。
- 消融非常全面：位移 vs 原始激活、全轨迹 vs 行/列子轨迹、LSTM vs 无序 Set MLP、线性探针层敏感性、oracle 最优层、运动学描述符等，每组还报告了 ID 与 OOD 指标。
- 在 Llama-3.1-8B 上每个训练集都给出完整 8 数据集评估矩阵（Table 10–12），而非仅有汇总平均。

#### 充分性与公平性
- **公平性考量较好**：TaT 始终以 zero-shot 方式（prompt 中无示例）评估，而 baseline 模型允许 few-shot（如 ARC-C 25-shot、Hellaswag 10-shot）；与 oracle 探针（事后选最优层）比较时 TaT 仍在 8 个数据集中 7 个胜出。
- **潜在不足**：
  - 主要评估集中于受约束的候选选择任务，对自由生成/多步推理链的检测仅留作未来工作。
  - 训练集与评估集的候选构造方式、标签格式差异（如 BoolQ 的 Yes/No vs 多项选择）可能影响迁移结论，作者对此只做了部分讨论。
  - 实验以英文数据集为主；未报告多次种子的方差/置信区间（仅提到 3 seeds 取平均选最优 session），统计显著性检验缺失。

---

### 六、主要结论与发现

1. **轨迹可泛化**：TaT 在单数据集上训练后即可跨任务迁移，OOD 平均准确率显著优于线性探针，整体平均也优于基础模型自身的 zero-shot/few-shot 性能（尽管无任何输入示例）。
2. **位移变换是关键**：在毒性检测中，位移轨迹（TaT Disp.）在 OOD 的 ToxiGen 上优于原始激活轨迹和线性探针（例如 Llama-3.1-8B：84.23% vs 81.99% vs 79.62%），说明位移有效滤除词元级/词法混淆。
3. **完整网格优于任何子轨迹**：同时建模"层深度 × token"展开的全网格稳定最佳；仅中层或仅最后 token 的表现弱得多（例如 OpenQA 训练时 OOD 平均从 76.83% 降至 63.25%/69.57%）。
4. **顺序性重要**：无序 Set MLP 在最强源任务（ARC-C、ARC-E、OpenQA）上不如 TaT，说明判别信号存在于位移的顺序组合中。
5. **复杂源任务迁移性更好**：ARC-Challenge、ARC-Easy、OpenBookQA 这类需要丰富推理结构的源任务训练出的分类器泛化最广；简单任务（如 SocialIQA）迁移效果较差。
6. **简单运动学规则不通用**：速度等标量描述符虽优于随机，但与数据集的"最优规则"不一致，无法替代学习方法。
7. **LoRA 不是等价替代**：LoRA 微调过拟合源任务语义分布，跨任务迁移不稳定；TaT 在冻结模型上学习检测机制，对分布漂移更鲁棒。

---

### 七、方法/实验亮点

1. **视角创新**：将可解释性从"静态快照"转向"动态轨迹几何"，呼应 Transformer 作为离散动力系统的理论视角，且首次在真实基准上验证了这一视角的有效性。
2. **位移而非原始激活**：理论动机清晰（特权基、残差对齐），实验上证明能有效降低词汇/上下文静态特征的干扰，对提示格式变化更鲁棒。
3. **极低额外开销**：LSTM 分类器参数量仅为基座模型的 0.06%，接近免费的可解释性附加模块。
4. **对比设置慷慨而严格**：基础模型获得 few-shot 示例、线性探针获得 oracle 层选择，TaT 仍能胜出，增强了结论说服力。
5. **消融体系完整**：行/列网格消融、有无顺序消融、原始 vs 位移消融互相支撑，能精确定位性能来源是"全轨迹 + 位移 + 顺序建模"三者共同作用。
6. **跨架构验证**：在稠密和 MoE 上均验证，说明结论并非某一模型特有。

---

### 八、不足与局限

1. **计算成本高于线性探针**：需要提取并处理所有层、所有 token 的激活轨迹，比单层静态探针昂贵（虽然 LSTM 本身开销小，但激活采集成本仍在）。
2. **可解释性有限**：LSTM 虽然能判断轨迹"是否有效"，但学到的几何特征仍然隐含，无法像注意力头/回路那样给出直接可读的机制解释——从"检测有效性"到"解释为何有效"之间仍有鸿沟。
3. **依赖训练数据**：方法需要标注好的有效/无效配对数据来训练分类器；作者指出若运动学描述符足够成功可免去训练需求，但实验表明简单描述符不可靠。
4. **任务范围受限**：实验均为受约束的选择型任务（确保监督无歧义），对模型自生成的多步推理链中的错误/幻觉检测尚未验证。
5. **对源任务/数据集特性敏感**：部分源任务（如 BoolQ、SocialIQA、ComQA）作为训练源时 TaT 增益不明显甚至弱于 Set MLP 或 oracle 探针，提示方法的迁移优势对源任务自身的推理丰富度有依赖。
6. **缺少统计显著性与方差报告**：正文未报告多次运行的置信区间或显著性检验，难以判断某些较小差距（如 ARC-E 上 73.81% vs 75.55%）是否可靠。
7. **未报告主要算力投入细节**：无 GPU 型号、数量、训练时长，复现成本难以预估。
8. **理论分析与实证的衔接仍较松**：文中提出的"残留对齐/位移激活特定特征"假设属于解释性动机，缺乏直接的机制验证（如通过因果干预证实位移确实对应具体特征写入）。

---

（完）
