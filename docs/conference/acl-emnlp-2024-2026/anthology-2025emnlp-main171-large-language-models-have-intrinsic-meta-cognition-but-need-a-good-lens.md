---
title: "Large Language Models Have Intrinsic Meta-Cognition, but Need a Good Lens"
title_zh: 大语言模型具有内在元认知，但需要好的透镜
authors: "Ziyang Ma, Qingyue Yuan, Zhenglin Wang, Deyu Zhou"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.171.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 聚焦LLM内在元认知能力与步骤级自我觉察评估，提出自动化元认知评测框架，贴合自评估需求
tldr: 当前研究多关注LLM对推理链错误的检测，而较少评估其对逐步错误的内在元认知，且已有自评估指标缺少步骤级分析与适应性。该文提出自动化元认知评测框架AutoMeco，系统评估现有各类透镜下的LLM元认知表现。结果表明LLM确实具备内在元认知能力，但必须借助合适透镜才能被有效观测与利用。该工作为LLM自我评价与可靠性研究提供了新的基准和分析视角。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main171/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 755, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main171/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 540, \"height\": 1353, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main171/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main171/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1489, \"height\": 1676, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 776, \"height\": 1006, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 575, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1654, \"height\": 1330, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 717, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 470, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 800, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 811, \"height\": 540, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1364, \"height\": 822, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1351, \"height\": 826, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1489, \"height\": 1676, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1488, \"height\": 1631, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main171/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1486, \"height\": 1494, \"label\": \"Table\"}]"
motivation: 现有工作主要看推理链错误检测，缺乏对LLM步骤级自我觉察的系统评估。
method: 提出AutoMeco框架，结合多种自我评估透镜对LLM逐步正确性进行自动化元认知评测，并研究如何改进这些透镜。
result: 结果显示LLM拥有内在元认知能力，但需要合适的透镜才能可靠地反映步骤错误。
conclusion: 必须为LLM配备好的自评估透镜方能发挥其元认知潜能，为可靠性提升提供评测与改进方向。
---

## Abstract
Previous research has primarily focused on the cognitive error detection capabilities of Large Language Models (LLMs), often prompting them to analyze mistakes in reasoning chains. However, few studies have examined the meta-cognitive abilities of LLMs (e.g., their self-awareness of step errors), which are crucial for their reliability. While studies on LLM self-evaluation present some measures, such as perplexity, which can reflect the answer correctness and be viewed as the lens of meta-cognition, they lack step-level analysis and adaptation. This paper studies the evaluation of LLM meta-cognition using the current lenses and how to improve these lenses. Specifically, we propose AutoMeco, an Automated Meta-cognition Evaluation framework for benchmarking the existing lenses. Furthermore, a training-free Markovian Intrinsic Reward Adjustment strategy, MIRA, is proposed to boost current meta-cognition lenses. Experimental results on three mathematical reasoning datasets and three LLMs show the reasonableness of AutoMeco by comparing it with Best-of-N verification. Moreover, the meta-cognition ability of LLMs can be better evaluated using MIRA.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- 该论文聚焦于大型语言模型（LLM）的**元认知能力**，即模型对自身推理过程中“步骤是否正确”的内在觉察，而非传统的“认知性错误检测”（让模型检查他人生成推理链的错误）。
- 现有自评估方法（如 PPL、熵）虽然能反映最终答案的正确性，可被视为观察元认知的“透镜”，但普遍缺少**步骤级粒度**和**步骤间依赖建模**。
- 论文的核心主张是：LLM 拥有内在的元认知信号，但这些信号需要“好的透镜”才能被可靠提取和利用。为此，作者提出了：
  - **AutoMeco**：免人工标注的自动化元认知评估框架，用于评测现有透镜对步骤正确性的预测能力；
  - **MIRA**：一种无需训练的马尔可夫内在奖励调整策略，通过注入步骤间依赖来增强透镜的表现。
- 整体意义在于为 LLM 自我评价、可信度评估和自主改进提供新的评测视角与方法基础。

## 2. 方法论

### 2.1 AutoMeco：自动化元认知评测框架

- 工作流程分为四个阶段：
  1. **结构化响应生成**：让 LLM 按“Step n:”格式输出分步推理，并用边界检测切出 N 个步骤。
  2. **步骤级状态聚合**：提取每个步骤中每个 token 的隐藏状态、logits 与概率向量。
  3. **内在奖励计算**：使用某个自评估函数（透镜）\( F \) 为每个步骤计算置信分数：
     \[
     s_i^{\mathrm{pred}} = F(H_i, Z_i, P_i)
     \]
  4. **步骤正确性自动标注与指标计算**：用过程奖励模型（PRM）对每个步骤打分：
     \[
     \{s_i^{\mathrm{true}}\} = \mathrm{PRM}(Q, R_{1:N})
     \]
     再按阈值 \(\theta\) 转为二值标签，并计算 AUROC、AUPR、FPR95。

- 框架设计为**完全不依赖人工步骤标注**，从而支持自动 benchmark。

### 2.2 MIRA：马尔可夫内在奖励调整

- 将推理过程建模为确定性马尔可夫决策过程（MDP）：
  - 第 i 个状态 \(S_i\) 为问题 Q 与前 i-1 个步骤的拼接；
  - 动作 \(R_i\) 为第 i 个推理步骤；
  - 状态转移：\(S_{i+1} = \mathrm{concat}(S_i, R_i)\)。
- 通过 Q 值反向传播调整原始置信分数：
  - 从终态 \(V(S_{N+1})=0\) 开始；
  - 反向计算 \(Q(S_i,R_i) = s_i^{\mathrm{pred}} + \gamma \cdot V(S_{i+1})\)；
  - 价值函数取 \(V(S_i)=\max_{R_i} Q(S_i,R_i)\)；
  - 最后用 softmax 归一化得到调整后分数。
- 核心思想是：一个步骤的元认知置信度不仅取决于当前内在状态，还应该受到后续步骤“未来回报”的影响，从而弥补原透镜忽略步骤间依赖的缺陷。

## 3. 实验设计

- **数据集**：三个数学推理数据集，难度递增：
  - GSM8K（取前 250 题，小学水平）；
  - MATH500（竞赛题子集）；
  - MinervaMATH（大学/奥赛级题）。
- **被测 LLM**：Qwen2.5-7B、Llama-3-8B-Instruct、Mistral-7B-Instruct。
- **标注用 PRM**：Qwen2.5-Math-PRM-7B；在 PRM 一致性分析中使用 Skywork-o1-Open-PRM-Qwen-2.5-7B 作为第二个 annotator。
- **对比的元认知透镜**：CoE-C、CoE-R、ΔEntropy、Maxprob、PPL、Entropy。
- **评测方式**：
  - AutoMeco 框架下的步骤正确性二分类指标；
  - Best-of-N（BoN）验证，用平均步骤奖励选择 N=6 个样本中的最佳响应；
  - 比较 MIRA 前后效果；
  - Majority voting 与 PRM-voting 作为 BoN 精度基线。
- **辅助分析**：
  - 内在分数与 PRM 分数的 Spearman/Kendall 相关分析；
  - 正确/错误步骤隐藏特征的 KDE 可视化；
  - 两个 PRM 之间的步骤/实例级一致性分析；
  - AutoMeco 与 BoN 排名一致性（Top-K match、Last-K match、一致性率 CR）；
  - 延迟测量与典型案例研究。

## 4. 资源与算力

- 论文中明确提到：“All the experiments are conducted on four 24G 3090 GPUs or one A100 80G GPU.”
- 未给出总训练/推理时长、具体批次大小、GPU 使用天数等细节。
- 由于主要方法（透镜 + MIRA）均不需要训练，只涉及推理阶段采集状态和数值计算，因此算力需求相对较低。
- 延迟测试显示 MIRA 带来的每实例额外耗时“不超过 0.03 毫秒”（考虑到吞吐量，实际上应理解为在统计中很小），说明其额外计算开销可忽略。

## 5. 实验数量与充分性

- **实验总量较充分**：
  - 主表覆盖 3 个模型 × 3 个数据集 × 6 个透镜，每个配置报告 4 个指标（BoN Acc、AUROC、FPR95、AUPR），共 54 个配置；
  - MIRA 有效性统计：在 61.1% 的 BoN 配置和 68.5% 的 AUROC 配置中取得提升；
  - 另外还有相关性表、PRM 一致性表、AutoMeco-BoN 一致性表、延迟表、案例可视化等；
  - 附录补充了 Llama 和 Mistral 上的统计可行性、推理步骤分布统计等，实验类型较丰富。
- **公平性与客观性**：采用三个模型、三个难度不同的数据集，比较方法均基于公开开源实现，MIRA 与基线使用相同内部状态，并统计了 p 值，整体上较公平。
- **仍有局限**：数据集全部来自数学推理，领域较窄；主实验只选用三个 7B/8B 开源模型，未包含更大参数模型或 o1/R1 等大型推理模型；BoN 与 AutoMeco 的一致性并不高（平均 CR 48.15%），说明 AutoMeco 不能完全替代真实推理结果验证。

## 6. 主要结论与发现

- **LLM 确实具备内在元认知信号**：自评估内在分数与 PRM 步骤奖励在简单任务上显著正相关，说明可以通过自身内部状态观察到部分步骤级正确性。
- **任务难度影响可观察性**：当题难度上升时，相关性下降，说明元认知观测的前提是模型对任务有一定掌握程度。
- **现有透镜需要改进**：多数透镜对步骤粒度预测能力不足，忽略了步骤间的顺序依赖；
- **MIRA 有效**：在多数实验配置中，MIRA 能提升透镜的步骤判别能力（AUROC 等）和 BoN 选答准确率；
- **在困难任务上，经过校准的自评估可以超过 Majority voting**，例如 Qwen2.5-7B + CoE-R + MIRA 在 MinervaMATH 上达到 12.13% vs Majority 10.66%，说明自诊断信号可用于高质量推理路径的选择；
- **PRM-as-a-Judge 基本可靠**：两个不同 PRM 在实例级判断上有较强一致性（最高 Cohen's Kappa 0.7334），但步骤级一致性较低，表明自动标注仍可能引入噪声。

## 7. 优点

- **切入角度新颖**：将认知科学中的“元认知/错误感（Feeling of Error）”引入 LLM 评估，关注步骤级自我觉察，而不是传统的事后错误检测。
- **框架免人工标注**：AutoMeco 借助 PRM 自动标注步骤正确性，可规模化复用于多种模型与数据集。
- **MIRA 设计轻量且具理论支撑**：无需训练、无需外部奖励模型，仅基于 MDP/Q-value 建模步骤间依赖，就能提升多个透镜；
- **实验规范**：同时使用相关系数、分类指标、BoN 精度、消融分析、内部特征可视化、人工可读案例，多角度验证结论。
- **具有实践意义**：验证了“通过内部自评估信号改进推理选择”的可行路径，为 LLM 自主纠错和自我改进提供了一种低成本信号来源。

## 8. 不足与局限

- **依赖白盒内部状态**：最精细的透镜（如 CoE 依赖隐藏状态）不适用于 GPT-4 等闭源模型，限制了方法的应用范围；只有概率类指标可迁移到黑盒场景。
- **存储与计算开销**：需要记录所有 token 的隐藏状态，带来额外显存占用；在长序列上代价可能进一步放大。
- **难以泛化到大型推理模型（LRM）**：o1/R1 类模型的推理过程更长、更动态，需要更自适应的步骤边界和状态建模，论文未做验证。
- **评测标签依赖 PRM**：PRM 非完美 judge，且步骤级 PRM 间一致性低于实例级，因此 AutoMeco 的“真实标签”本身存在噪声风险；
- **实验覆盖有限**：仅数学推理、仅英文指令模型，未涉及代码/逻辑/常识等领域，也未覆盖更大的模型尺寸；
- **BoN 验证中报告数字偏低**：如在 GSM8K 上多数透镜的 BoN 精度仅为 50%–70%，但 Majority/PRM 达到 86.8%/75.2%，说明这些自评估指标在相对简单的任务中并不能完全替代多数投票，优势主要体现在困难任务上；
- **未与采样一致性类方法（如 SelfCheckGPT）对比**：对单样本内部状态方法的研究选择性较强，可能弱化与其他不确定性估计方法的比较。
- **作者在 Limitations 中坦诚**，当前研究主要面向开源模型，MIRA 的额外计算代价尚可接受，但大规模实际部署仍需进一步优化。

（完）
