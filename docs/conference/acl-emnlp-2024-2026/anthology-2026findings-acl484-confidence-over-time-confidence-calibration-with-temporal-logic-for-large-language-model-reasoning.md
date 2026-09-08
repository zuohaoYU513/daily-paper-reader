---
title: "Confidence over Time: Confidence Calibration with Temporal Logic for Large Language Model Reasoning"
title_zh: 时间维度上的置信度：基于时间逻辑的大语言模型推理置信度校准
authors: "Zhenjiang Mao, Anirudhh Venkat, Artem Bisliouk, Sindhura Kumbakonam Subramanian, Akshat Kothiyal, Saithej Singhu, Ivan Ruchkin"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.484.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 用时序逻辑建模推理各步的置信度信号，以更好校准推理过程置信度
tldr: 现有置信度估计方法常将整个推理过程压成单个标量，忽略置信度在生成过程中的演变，难以区分正确推理与自信的错误。论文提出用时序逻辑（STL）刻画逐步置信度信号，通过判别式STL挖掘方法自动发现描述置信度动态的时序公式。在数学推理和科学问答等任务上，该方法提升了置信度校准质量，为多步推理场景的校准提供了时间感知的新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1584, \"height\": 305, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1420, \"height\": 696, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 928, \"height\": 310, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 602, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 810, \"height\": 384, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 748, \"height\": 936, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 544, \"height\": 605, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 799, \"height\": 706, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1653, \"height\": 933, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1515, \"height\": 2363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1146, \"height\": 2510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl484/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1552, \"height\": 1463, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1666, \"height\": 1069, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 580, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 678, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 697, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 557, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 572, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 789, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 805, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 782, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1322, \"height\": 1325, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 854, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1644, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl484/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 874, \"height\": 382, \"label\": \"Table\"}]"
motivation: 推理链条中的置信度随步骤动态变化，单标量估计丢失时间信息并被长度等表面因素干扰，需引入时序建模。
method: 用信号时序逻辑对推理过程的逐步置信度进行形式化，通过判别式STL挖掘自动提取与正确性相关的时序模式并用于校准。
result: 实验表明时间逻辑特征能够更准确地区分正确推理与自信的错误，显著提升校准性能。
conclusion: 时序逻辑为多个推理步骤的置信度演变提供了一种可解释的建模与校准工具。
---

## Abstract
Large Language Models (LLMs) increasingly rely on long-form, multi-step reasoning to solve complex tasks such as mathematical problem solving and scientific question answering. Despite strong performance, existing confidence estimation methods typically reduce an entire reasoning process to a single scalar score, ignoring how confidence evolves throughout the generation. As a result, these methods are often sensitive to superficial factors such as response length or verbosity, and struggle to distinguish correct reasoning from confidently stated errors. We propose to characterize the stepwise confidence signal using Signal Temporal Logic (STL). Using a discriminative STL mining procedure, we discover temporal formulas that distinguish confidence signals of correct and incorrect responses. Our analysis found that the STL patterns generalize across tasks, and numeric parameters exhibit sensitivity to individual questions. Based on these insights, we develop a confidence estimation approach that informs STL blocks with parameter hypernetworks. Experiments on multiple reasoning tasks show our confidence scores are more calibrated than the baselines.

---

## 论文详细总结（自动生成）

# 《Confidence over Time: Confidence Calibration with Temporal Logic for Large Language Model Reasoning》详细总结

## 1. 论文核心问题与整体含义（研究动机与背景）

- **核心问题**：现有大语言模型（LLM）置信度估计方法通常将整个长链推理过程压缩为单一标量分数（如 token 概率均值、熵、一致性等），**忽略了置信度在推理过程中随步骤动态演变的时序信息**，导致以下问题：
  - 容易受响应长度、冗长程度、填充词等表层因素干扰；
  - 难以区分“正确推理”与“表达自信但实际错误”的推理；
  - 单个步骤的置信度骤降等关键失败信号可能被平均化掩盖（论文 Fig.2 展示了典型“dip-and-recover”错误被标量法遗漏的案例）。
- **整体含义**：论文提出将逐步置信度视为**时序信号（temporal signal）**，并使用**信号时序逻辑（Signal Temporal Logic, STL）** 进行形式化建模，从而捕获置信度演变的时序模式，提升置信度校准质量，同时保留可解释性。
- **下游意义**：可靠的逐响应置信度可支持高风险场景中的弃权、Best-of-N 选择、模型路由、早期停止等决策，且 STL 结构使失败模式可审计。

## 2. 论文提出的方法论

### 2.1 核心思想
- 将每个响应 `y` 按推理步骤/语义段切分为 `n` 个片段，每个片段内 token 概率的算术平均构成逐步置信度信号 `S = [s1, ..., sn]`；
- 用 STL 公式描述置信度轨迹上的时序模式（如“始终高于阈值”“发生骤降”“末尾回落”等）；
- 通过判别式 STL 挖掘自动发现能区分**正确响应**与**错误响应**的时序公式；
- 将挖掘出的 STL 公式实例化为**可微分的 STL 块**，并通过**超网络（hypernetwork）** 按问题实例预测参数，从而实现结构固定、参数自适应的置信度估计。

### 2.2 关键技术细节

#### （1）逐步置信度信号构造
- 每个片段置信度为该片段内 token 概率的算术平均：
  \[
  s_j = \frac{1}{L_j}\sum_{k=0}^{L_j-1} P(y_{t_j+k} \mid y_{<t_j+k}, x)
  \]
- 分段方式可基于句子、语义步骤等；实验默认使用基于“Step N:”标记的正则级联分段。

#### （2）STL 语法与鲁棒性
- 使用谓词 `μ ≡ s_t ≥ c`，结合时序算子 `Always (□)` 和 `Eventually (◇)`；
- 量化语义（鲁棒度）通过 min/max 运算计算：
  \[
  \rho(\Box_{[a,b]}\phi, S, t) = \min_{k\in[t+a,t+b]} \rho(\phi,S,k)
  \]
  \[
  \rho(\Diamond_{[a,b]}\phi, S, t) = \max_{k\in[t+a,t+b]} \rho(\phi,S,k)
  \]
- 鲁棒度为正表示满足公式，为负表示违反，标量值可作为置信度信号。

#### （3）判别式 STL 挖掘（基于 TeLEx 思路）
- 初始化一组**基础模板**：正样例模板（WeakestLink `□_{[0,T]}(s_t≥μ)`、EndHigh、StartHigh、NeverSharpDrop 等）和负样例模板（EventuallyLow、EndLow、SharpDrop、Recovery 等）；
- 对模板参数进行优化，最大化解正确性标签的分类目标（NLL）；
- 使用**鲁棒度信号增强（signal lifting）** 构造嵌套公式；
- 通过时序嵌套与布尔组合扩充候选公式空间；
- 进行**双类判别式挖掘**：
  - `Φ_pos`：高鲁棒度对应正确响应；
  - `Φ_neg`：高鲁棒度对应错误响应（幻觉/推理失败）。

#### （4）STL 块与鲁棒度到置信度映射
- 每个 STL 块计算固定公式 φ 的聚合鲁棒度 ρ(φ, S)；
- 通过可学习 sigmoid 映射为概率：
  \[
  \hat{p} = \omega(\alpha \tilde{\rho} + \beta)
  \]
  - α 控制决策边界锐度，β 控制偏移；
  - 使用 soft-min/soft-max 保证可微性。

#### （5）超网络参数自适应（核心创新）
- **动机**：RQ2 分析显示，固定结构在不同问题上的最优参数差异大（阈值类参数尤其敏感），单一全局参数化不足；
- **做法**：固定挖掘得到的 STL 结构，用超网络 `H_ψ` 以原始提示 `x` 与置信度信号 `S` 为输入，预测每个实例的 STL 参数 θ（时间边界、谓词阈值、sigmoid 映射 α/β）；
- 超网络架构：Transformer 分支（3 层 Pre-LN，d=256）+ 统计特征分支（16 种手工统计量）→ 拼接 → MLP → 参数头；
- 训练目标：最小化正确性标签的判别损失：
  \[
  \min_\psi \frac{1}{N}\sum_{i=1}^N \mathcal{L}(c_i, \hat{P}_i)
  \]

## 3. 实验设计

### 3.1 数据集与场景
| 数据集 | 内容 | 规模 |
|---|---|---|
| GAOKAO-Math | 中国高考数学（子集） | 213 例 |
| CLadder | 因果推理 | >10,000 例 |
| SciQ | 科学多选题 | 13,679 例 |
| Big-Bench-Hard (BBH) | 23 个挑战性推理子任务 | 6511 例 |

- 所有任务为**选择题或二元决策**，保证正确性标签明确。
- 覆盖模型：**Qwen3-8B、Gemma-3-12B、Llama-3-8B** 三种主干 LLM。

### 3.2 对比方法（Baselines）
- **Logit-based**：AveLogit（平均 token 概率）
- **Internals-based**：SAR（基于注意力相关性）、InternalInspector（内部状态置信度）
- **Verbalized / Self-Eval**：自我评估置信度
- **Consistency-based**：Self-Consistency（多次采样一致性）（仅作为校准基线，非准确率基线）
- **消融变体**：
  - A1：跨任务复用正+负 STL 模式（在 BBH 上挖掘，迁移到其他任务）
  - A2：跨任务仅复用负（失败模式）STL 模式
  - A3：领域内 STL 挖掘，固定参数
  - Ours：领域内 STL + 超网络实例自适应参数
- **额外对照**：MLP、Bi-LSTM 序列分类器（有无 STL 特征），见 Appendix D.4。

### 3.3 评估指标
- **ECE**（期望校准误差）↓
- **Brier Score** ↓
- **AUROC** ↑
- 使用 5 折交叉验证，报告均值±标准差。

## 4. 资源与算力
- **论文未明确报告训练所用 GPU 型号、数量及时长**。
- 仅提供如下间接信息：
  - 超网络含约 **267 万参数**（约基础 LLM 的 0.03%）；
  - 整体推理开销约 **0.55 秒/示例**；
  - 训练在**单张 GPU** 上即可完成；
  - 对比 InternalInspector 需要 12–57M 参数、多 GPU 训练。
- 但未说明具体硬件型号和能耗。

## 5. 实验数量与充分性

### 5.1 实验数量
- **主实验**：Table 1 中在 4 个数据集 × 3 种主干模型 × 7 种对比方法（含消融）下全面报告 ECE/Brier；
- **AUROC 补充实验**：Table 11 报告各方法 AUROC；
- **RQ1 跨任务结构分析**：Fig. 4、Fig. 8/9、Table 8（Jaccard 相似度，含 BBH 子任务级验证）；
- **RQ2 参数敏感性分析**：Fig. 5、图 10/11、Table 12（跨折参数 MAE）；
- **消融实验**：
  - STL 模板数量（Table 7）；
  - 分段策略（Table 5）；
  - STL 特征必要性（Table 6）；
  - 跨任务复用正/负模式（A1/A2）；
  - 实例级自适应 vs 固定参数（A3 vs Ours）；
- **鲁棒性分析**：问题相似性 vs 参数变异性（Table 13）。
- 整体实验量大，覆盖多样化场景与模型。

### 5.2 充分性与公平性
- **优点**：包含多种基线类型、多种模型、多种数据集，并进行交叉验证，统计严谨；
- **客观性**：所有方法在同一数据划分与推理设置下比较，Self-Consistency 纯为校准基线，声明正交性；
- **潜在不足**：主实验集中在结构化推理与明确答案任务，未涉及开放生成场景；跨任务迁移分析中 A1/A2 缺少 BBH 自身结果（因与 A3 相同），对完整对比略有影响。

## 6. 主要结论与发现

- **标量置信度存在盲区**：平均式标量法会掩盖单步骤降等失败信号，STL 可捕获“dip-and-recover”等时序失败模式。
- **时序结构不对称泛化（RQ1）**：错误推理（负模式）STL 结构跨任务高度相似（Jaccard ~0.74–0.81），正确推理模式跨任务相似度低（~0.47–0.55）——失败模式的时序签名具有可移植性。
- **参数对问题敏感（RQ2）**：固定 STL 结构下，谓词阈值和差分相关参数随问题变化大，时间参数较稳定；且不单纯由问题表面/语义相似性解释。
- **领域内挖掘优于跨任务复用**：A2（仅负模式迁移）优于 A1，但两者都不如领域内挖掘（A3/Ours）。
- **超网络自适应进一步改善校准**：Ours 在多数数据集上取得最低 ECE/Brier，尤其 CLadder（Qwen3: ECE 0.035 vs A3 0.057）和 BBH。
- **效率与性能可兼得**：Ours 推理耗时 0.55s/例，平均 ECE 0.051，比 AveLogit 降低 83%，远优于 Self-Consistency、SAR 等慢方法；InternalInspector 虽快但显著恶化校准。
- **STL 表征带来增益**：单纯 Bi-LSTM 在原始信号上并不优于 AveLogit；加入 STL 特征后即使 MLP 也能达到接近完整方法的校准水平——增益来自 STL 表示。

## 7. 优点

- **问题视角新颖**：将自信估计从静态标量提升为时序逻辑表征，针对“自信的错误”这一痛点。
- **方法论完整闭环**：发现现象（RQ1/RQ2）→ 提出机制（超网络自适应）→ 验证效果，逻辑链条紧密。
- **兼顾校准与可解释性**：STL 公式结构固定，失败模式可审计（如 SharpDrop、Recovery），而不像端到端黑箱。
- **轻量高效**：超网络仅 2.67M 参数，单 GPU 可训，推理开销约 0.55s，显著优于多采样方法的安全性经济性。
- **实验覆盖广**：3 种 LLM、4 个基准、6 类以上基线、多条消融路径，统计报告完善。
- **实证深入**：不仅报告指标，还揭示了跨任务不对称泛化与参数敏感性的规律，具有启发性。

## 8. 不足与局限

- **依赖分段质量**：默认“Step N:”标记分段，非结构化输出不适用；尽管分段策略消融显示框架仍具鲁棒性，但无显式步骤标记时校准性能下降。
- **任务范围有限**：仅覆盖结构化推理（数学、科学、因果/逻辑推理）及选择题/二元判定，对**开放生成、长文摘要、对话**等场景未验证。
- **领域内挖掘依赖标签数据**：最佳配置（Ours）需要领域内带正确性标签的训练数据；纯跨任务迁移（A1）校准效果明显下降。
- **超网络参数变异性缺乏语言学解释**：论文仅证明问题相似性不能解释参数变异性，但**未揭示参数变化的语义/逻辑驱动因素**。
- **论文未报告训练算力细节**：如 GPU 型号、批量大小、训练轮数等，复现成本不透明。
- **基线设置**：Self-Consistency 作为校准基线仅使用一致性率，未结合语义熵等先进一致性变体；内部状态基线数量较少。
- **评估指标侧重 ECE/Brier**：对高置信区间或高错误率子组的条件风险分析不足。

（完）
