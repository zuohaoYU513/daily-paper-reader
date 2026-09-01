---
title: "ReFL: Reflective Feedback Learning for Hallucination Detection of Large Language Models"
title_zh: ReFL：面向大语言模型幻觉检测的反思式反馈学习
authors: "Cunhang Fan, Jun Zhang, Xue Zhang, Shuai Zhang, Zhao Lv, Jianhua Tao, Zhengqi Wen"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.899.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 基于修正性上下文学习的幻觉检测
tldr: 针对现有幻觉检测方法依赖外部知识或内部状态、且泛化性差的问题，提出ReFL框架。该框架利用修正性上下文学习动态引导大模型识别自身预测错误并调整内部表征，且无需更新模型权重。实验表明该方法在保持实时性的同时提升了检测性能与泛化能力。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long899/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1658, \"height\": 908, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long899/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long899/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1651, \"height\": 992, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1610, \"height\": 849, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1606, \"height\": 846, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1663, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 753, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 665, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 639, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 804, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1646, \"height\": 440, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1646, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1647, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 802, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1610, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1649, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long899/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 778, \"height\": 233, \"label\": \"Table\"}]"
motivation: 现有幻觉检测要么依赖昂贵外部知识，要么使用泛化性差的内部状态。
method: 提出ReFL框架，通过修正性上下文学习引导模型识别预测错误并调整内部表示，不更新权重。
result: 实验验证ReFL能有效提升幻觉检测精度与泛化能力，并降低计算开销。
conclusion: 为无需外部知识、可实时应用的幻觉检测提供了新思路。
---

## Abstract
Large Language Models (LLMs) often generate factually incorrect content, known as “hallucinations”, which undermine the reliability and safety of their outputs. Existing hallucination detection methods either depend on external knowledge sources, incurring high computational costs and limiting real-time applicability, or extract the model’s internal states, leading to poor generalization. To address these issues, this paper proposes ReFL, a hallucination detection framework. ReFL leverages corrective in-context learning to dynamically guide LLMs to recognize their own prediction errors and adjust internal representations, critically without updating model weights. Specifically, by introducing a corrective in-context learning strategy, where triplets of input text, model prediction, and ground-truth label are embedded into the prompt to make the model explicitly aware of its own errors. The model reflects on prior outputs to adjust its internal states and generate semantically structured representations better aligned with factuality. This feedback mechanism encourages the model to shape a more coherent semantic space and enhances the LLM’s internal sensitivity to hallucinations. Experimental results on two benchmark datasets demonstrate that ReFL consistently outperforms existing methods, achieving state-of-the-art performance.

---

## 论文详细总结（自动生成）

以下是基于论文内容的详细中文总结：

## 论文总结

### 1. 论文的核心问题与整体含义

**研究动机与背景：**

- 大语言模型（LLM）在生成内容时经常产生“幻觉”（hallucination），即事实错误的内容，这严重损害了输出的可靠性和安全性，尤其是在医疗、法律、科学研究等高影响领域。
- 现有幻觉检测方法主要存在两类问题：
  - **依赖外部知识源**的方法：如查询外部知识库，计算成本高，难以满足实时应用需求；
  - **提取模型内部状态**的方法：将隐藏层激活视为静态特征，缺乏动态引导，导致跨域/跨结构泛化能力差。
- 论文受人类“从错误中反思学习”机制的启发，提出核心研究问题：**LLM 能否通过“观察自身错误”来调整内部推理模式，进而提高幻觉检测能力？**

### 2. 论文提出的方法论

**核心思想：** 通过修正性上下文学习（Corrective In-Context Learning, CICL）动态引导 LLM 识别自身预测错误并调整内部表征，整个过程无需更新模型权重。

**方法框架（ReFL）包含两个步骤：**

**步骤一：修正性上下文学习生成**

- 采用 k-shot 上下文学习策略：对测试样本 x 构造包含 k 个带标签示例的提示，计算模型对每个候选标签的归一化概率，选择概率最高的标签作为预测结果（公式省略，使用几何均值归一化消除标签长度偏差）。
- 构建**修正三元组** $t_i = (x_i, \hat{y}_i, y_i)$：
  - $x_i$ 为输入文本，$\hat{y}_i$ 为模型预测标签，$y_i$ 为真实标签；
  - 对预测错误的样本，三元组提供**负反馈信号**；对预测正确的样本，提供**正对齐信号**。
- 将修正三元组拼接到测试样本之前，构成最终输入序列：$\text{Input}_{CICL} = C_{CICL} \| (x, \hat{y}, ?)$，使模型“看到”自己过去的预测结果，从而实现内在状态的重新对齐。

**步骤二：幻觉分类器训练**

- 从 LLM 最后一层的最后一个 token 位置提取隐藏状态向量作为特征（维度为 d）；
- 训练一个三层 MLP 分类器（隐藏层维度 256→128→64，ReLU 激活，sigmoid 输出）完成二分类；
- 使用二元交叉熵（BCE）损失函数优化分类器。

### 3. 实验设计

**数据集：**

| 数据集 | 内容与用途 |
|--------|-----------|
| **True-False 数据集** | 短事实陈述，涵盖六个语义主题（动物、城市、公司、化学元素、科学事实、发明），用于跨域幻觉检测评估 |
| **LogicStruct 数据集** | 包含四种句法结构（肯定、否定、合取、析取），用于评估跨句法结构的泛化能力 |
| **TruthfulQA 数据集**（附加实验） | 真实世界问答场景，用 BLEURT 分数阈值（0.25 / 0.5）标注幻觉 |

**评估设置：**

- True-False：留一主题交叉评估（训练其他主题，测试当前主题）；
- LogicStruct：用肯定句训练，在否定、合取、析取结构上测试；
- TruthfulQA：前 20% 数据训练，后 80% 评估。

**对比基线：**

- LN-PP（长度归一化预测概率）、SAPLMA（隐藏层激活探测器）、MIND（无监督内部状态方法）、MM（事实性方向投射）、PRISM（提示引导内部状态方法，含 PRISM-MM 和 PRISM-SAPLMA 两种变体）、SelfCheckGPT、Semantic Entropy。

**评估模型：** LLaMA2-7B、LLaMA2-13B、LLaMA3-8B、OPT-6.7B、Qwen2.5-3B/7B/14B（含 instruct 版本）。

**评估指标：** 准确率（ACC）和 ROC 曲线下面积（AUC）。

### 4. 资源与算力

- 论文明确提及使用 **NVIDIA H100 GPU** 进行效率分析实验，使用 **NVIDIA A800 GPU** 实施主要实验。
- 效率分析表明 ReFL 的总运行时间最短（128.91 秒），其中特征提取时间仅 68.43 秒。
- 论文**未明确说明**具体 GPU 数量、训练时长等更细粒度的算力配置信息，也未提供预训练 LLM 权重微调等计算资源信息（LLM 本身保持冻结）。

### 5. 实验数量与充分性

**实验总量较为丰富：**

- **主实验**：在 True-False 和 LogicStruct 两个基准上，对多个 LLM（≥6种）与 6+ 种基线方法对比 ACC 和 AUC；
- **效率分析**：对比各方法的特征提取和训练时间；
- **消融实验（4组）**：
  - 修正三元组 vs. 静态探测 vs. 标准 ICL；
  - 内部状态探测 vs. LLM-as-judge；
  - 修正比例（0% 到 100%）的影响；
  - TruthfulQA 真实问答场景验证；
- **附录补充实验**：额外模型（LLaMA2-13B、Qwen2.5-7B/14B）、示例数量影响、层选择影响、特征提取策略比较、内部表征统计与可视化分析（方差比、t-SNE）。

**充分性评估：**
- 实验覆盖面较广，包含跨模型、跨主题、跨句法结构、跨特征提取策略等多维度评估，比较充分；
- 消融实验设计合理，能有效验证各设计选择（修正三元组、内部状态探测、50% 修正比例、最后一层最后 token 特征）的必要性；
- 所有基线结果均自行复现以保证公平性；每个实验重复 3 次取平均；
- 但在基线覆盖上缺少对更近期（2025 年后）方法的对比，且在 LLM 架构多样性上（缺少如 Mistral、Gemma 等）仍有扩展空间。

### 6. 论文的主要结论与发现

- ReFL 在 True-False 和 LogicStruct 数据集上**一致地超越所有基线**，达到 SOTA 性能（如 LLaMA3-8B 上 ACC 88.1%，AUC 95.6%；LogicStruct 平均 ACC 81.1%）；
- 修正三元组反馈机制能够有效**重构 LLM 的内部表示空间**，使事实性相关信号更加突出（方差比平均提升超过 121%）；
- 该方法擅长**跨句法结构泛化**（否定句上准确率可达 90% 以上），弥补了现有内部状态方法的不足；
- 内部状态探测比直接生成式判断更可靠（85% vs. 61%），表明事实性信息在隐藏状态中更完整地保留；
- ReFL 只需**单次前向传播**，天然支持批量推断，计算效率更优。

### 7. 优点

- **无需权重更新**：通过提示级动态引导实现内部状态调整，参数高效且保持模型原有能力；
- **不依赖外部知识库**：避免了推理阶段的高额查询成本，适合实时应用；
- **跨域、跨结构泛化能力强**：修正三元组让模型关注“正确性结构”而非特定主题/语法关联，有效缓解过拟合；
- **方法设计有认知科学依据**：借鉴人类“从错误中学习”的反思机制，思想新颖、可解释；
- **补充实验充分**：包含内部表征的定性和定量分析（方差比、t-SNE 可视化），实证支撑有力。

### 8. 不足与局限

- **适用范围受限**：主要针对**语句级**事实性判断，扩展到段落级、长文级幻觉检测尚需探索；
- **不适合闭源商业模型**：核心依赖 LLM 内部状态提取，对不暴露内部状态的闭源模型（GPT-4o、Gemini）难以直接应用；
- **依赖部分标注信息**：训练分类器需要监督数据（标签），在完全无监督场景下表现未验证；
- 修正三元组需要提前知道模型预测，增加了一次预推理前向计算，在 Pipeline 设计中属于前置开销；
- 实验中的 LLM 均为开源模型，未覆盖更广泛的模型族系；也未充分讨论不同提示模板、示例选择策略的影响；
- 从元数据看，该论文时间标注为 2026 年，但读者可注意到其方法未与 2025 年后新出现的强基线进行比较，时效性对比存在提升空间。

（完）
