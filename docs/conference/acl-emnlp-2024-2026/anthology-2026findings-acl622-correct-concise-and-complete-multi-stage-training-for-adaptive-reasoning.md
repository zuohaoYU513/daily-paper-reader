---
title: "Correct, Concise and Complete: Multi-stage Training For Adaptive Reasoning"
title_zh: 正确、简洁且完整：面向自适应推理的多阶段训练
authors: "Nathanaël Carraz Rakotonirina, Ren Pang, Neha Anna John, Michael Bohlke-Schneider, Momchil Hardalov"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.622.pdf"
tags: ["query:metacognitio"]
score: 4.0
evidence: 训练模型在首个答案后自我校验以决定是否继续推理；涉及自我判断但核心是推理效率
tldr: 大语言模型的思维链推理常生成过多中间token，增加计算成本却不提高甚至降低准确率，即过度思考现象。论文提出多阶段高效推理训练方法，融合拒绝采样或推理迹重整的监督微调和带自适应长度惩罚的强化学习，使用轻量奖励函数惩罚首个正确答案之后的冗余tokens，引导模型仅在必要时进行自我校验。实验显示该方法能在保持正确率的同时显著减少推理长度，缓解过度思考问题。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl622/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl622/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl622/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1636, \"height\": 811, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl622/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1645, \"height\": 631, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl622/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1662, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl622/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1571, \"height\": 1159, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl622/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1658, \"height\": 611, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl622/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 812, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl622/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 815, \"height\": 759, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl622/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1652, \"height\": 520, \"label\": \"Table\"}]"
motivation: 思维链推理经常过度冗长，增加成本甚至损害准确率，需要对推理长度进行自适应控制以兼顾效率与正确性。
method: 提出多阶段训练框架，先用拒绝采样或格式重整进行监督微调，再用自适应长度惩罚的强化学习训练模型，奖励首个正确答案之后的简洁性并保留所需自校验。
result: 实验显示多阶段训练能引导模型在首个正确答案后停止思考，减少不必要token的同时保持或提升准确率，缓解过度思考。
conclusion: 自适应长度惩罚是一种有效的训练信号，可使推理模型更简洁且不损失正确性，为低延迟推理提供了一条可行路径。
---

## Abstract
The reasoning capabilities of large language models (LLMs) have improved substantially through increased test-time computation, typically in the form of intermediate tokens known as chain-of-thought (CoT). However, CoT often becomes unnecessarily long, increasing computation costs without improving accuracy and sometimes even degrading performance, a phenomenon known as “ overthinking ”. We propose a multi-stage efficient reasoning method that combines supervised fine-tuning—via rejection sampling or reasoning trace reformatting—with reinforcement learning using an adaptive length penalty. We introduce a lightweight reward function that penalizes tokens generated after the first correct answer, encouraging the model to perform self-verification only when beneficial. We conduct a holistic evaluation across seven diverse reasoning tasks, analyzing the accuracy–response length trade-off. Our approach reduces response length by an average of 28% for 8B models and 40% for 32B models, while incurring only minor performance drops of 1.6 and 2.5 points, respectively. Despite its conceptual simplicity, it achieves a better trade-off than more complex state-of-the-art efficient reasoning methods, scoring 76.6 on the area under the Overthinking-Adjusted Accuracy curve ( AUC OAA )—5 points above the base model and 2.5 points above the second-best approach.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究对象**：大语言模型（LLMs）的思维链（Chain-of-Thought, CoT）推理中的"过度思考"（overthinking）现象。
- **问题定义**：LLM 在推理密集型任务（数学、代码等）上通过生成更长的中间推理 token 来提高准确率，但这导致大量冗余、重复的推理内容，不仅增加了计算成本和推理延迟，有时还会反过来**损害准确率**。
- **现有方法的不足**：已有高效推理方法往往依靠**预定义的推理预算**（如硬截断或固定阈值），无法针对不同问题自适应地调整推理长度——有的问题不需要长推理却被迫走完整个预算，有的问题需要更多校验却被过早截断。
- **核心目标**：在不损失（或仅轻微损失）准确率的前提下，**自适应地缩短推理长度**，让模型学会在"何时该停止思考、何时该继续校验"之间做出合理判断。

## 2. 方法论：核心思想、技术细节与公式

论文提出一个**"SFT → RL"的多阶段训练框架**，具体的两条技术路线如下：

- **阶段一：监督微调（SFT）作为 RL 前的预热**，目的是让模型初步偏向简洁推理。有两种数据构造方式：
  1. **拒绝采样（Rejection Sampling）**：对每题生成多个续写结果，挑选其中**最短的正确回答**作为训练数据（称为 *Adaptive-Answer*）。
  2. **轨迹格式重整（Trace Reformatting）**：去除模型推理轨迹末尾的**总结性摘要**，仅保留最终答案，让模型直接给出答案而不做冗余复述（称为 *Format-Adaptive-Answer*）。

- **阶段二：带自适应长度惩罚的强化学习（RL）**
  - 使用 **GRPO**（Group Relative Policy Optimization）进行训练。
  - 奖励函数由两部分构成：正确性奖励 \( R_C(y) \) 与自适应长度惩罚 \( R_L(y) \)：
    \[
    R(y) = R_C(y) - \lambda \cdot R_L(y)
    \]
  - 长度惩罚的核心思想是**只惩罚"首个正确答案之后"生成的 token**：
    \[
    R_L(y) =
    \begin{cases}
    \frac{L(y) - L(y_{\text{first}})}{L(y)}, & \text{若答案正确} \\
    0, & \text{否则}
    \end{cases}
    \]
    其中 \( y_{\text{first}} \) 为第一个正确答案出现前的 token 前缀，\( L(\cdot) \) 为 token 数量。
  - **关键优势**：
    - 如果模型开头回答错误、后期自我纠正，则**不施加任何惩罚**，保留了纠错能力；
    - 如果模型已写出正确答案但还在重复验证、反复自我确认，则**惩罚冗余 token**。
  - 这一设计鼓励模型只在**收益大于成本**时才执行自我验证（self-verification），实现**input-dependent（输入自适应）的推理预算**。
- 相比已有的截断或逐句剪枝方法（TokenSkip、Stepwise Perplexity 等），本方法**不打断推理流程**，通过奖励信号让模型自己学会何时停止，兼顾**正确（correct）、简洁（concise）、完整（complete）**三个要求。

## 3. 实验设计：数据集、基准与对比方法

- **训练数据**：DeepScaleR（13K 数学题，来源覆盖 AIME 1983–2023、AMC、Omni-Math、STILL）。**仅使用数学训练，但跨域评估泛化性**。
- **评估基准（7 个数据集，覆盖多领域）**：
  | 类型 | 数据集 |
  |---|---|
  | 数学 | MATH-500、AIME 24、AIME 25 |
  | 科学问答 | GPQA Diamond |
  | 常识问答 | CommonsenseQA |
  | 代码生成 | LiveCodeBench v6 |
  | 长上下文推理 | LongBenchv2 |
- **评估模型**：
  - 主模型：Qwen3-8B
  - 泛化验证：Qwen3-1.7B、Qwen3-32B、DeepSeek-R1-Qwen-7B-distilled
- **对比基线方法（较全面）**：
  - No Thinking（关闭思考模式）
  - First-Answer Truncation（需访问真实答案的强基线）
  - 纯 SFT（最短正确样本微调）
  - RL + Hard Length Penalty（16k、8k、8k→4k curriculum 三档）
  - RL + Soft Length Penalty（DAPO 式软惩罚）
  - RL + Normalized Length Penalty（Kimi k1.5 式组内归一化）
  - RL + TWYN（Think When You Need 成对比较式奖励）
- **评估指标**：
  - 准确率（Accuracy）
  - 响应长度（生成 token 数）
  - **AUC-OAA**（Area under Overthinking-Adjusted Accuracy curve）——以统一度量平衡准确率与长度，避免单一指标比较不全面。

## 4. 资源与算力

- 论文**未明确报告**具体的 GPU 型号、GPU 数量、训练时长或总计算量（FLOPs）。
- 仅报告了训练超参数信息：
  - SFT：2 epochs、batch size 256、学习率 1e-5；
  - RL：GRPO 组大小 8、global batch size 256、50 轮迭代、学习率 1e-6、KL 正则 β=0.001。
- 评估时采样次数为 AIME 24/25 各 64 次、其余数据集 10 次，说明推理开销不小，但训练的总算力消耗未能从文中准确评估。

## 5. 实验数量与充分性

- **实验组数非常多、覆盖面广**：
  1. **主实验**：Qwen3-8B 上 11 种方法 × 7 个数据集（含准确率、长度、AUC-OAA 三维度比较——一组 77+ 的量化结果）；
  2. **组件消融实验**：Base / SFT(RS) / SFT(Format) / RL(no SFT) / Adaptive-Answer / Format-Adaptive-Answer 的逐步对比；
  3. **规模泛化实验**：4 种模型 × 2 种方法（表 3）；
  4. **分布分析**：正确/错误答案的响应长度分布对比（图 3）；
  5. **行为分析**：中间正确答案数量分布（图 4）；
  6. **难度分析**：MATH-500 按 1–5 难度层级查看准确率、响应长度和中间答案数（图 5）；
  7. **定性分析**：实际推理轨迹对比案例（图 6）。
- **公平性与客观性**：
  - 使用 AUC-OAA 作为统一排序指标，避免只比准确率或只比长度的片面判断；
  - 基线的响应长度截断上限均设为相同的 16,384 tokens，解码参数统一采用 Qwen3 推荐设置，控制变量较严格；
  - 在首个正确答案截断基线（First Answer Truncation）这类需要访问真实标签的"作弊"基线上，本方法依然胜出，说明增益并非简单来自"删除冗余内容"。
- **结论：实验数量充足、设计相对客观公平，可信度较高。**

## 6. 主要结论与发现

- **核心量化结果**：
  - Qwen3-8B：响应长度平均缩短 **28%**，准确率仅降 **1.6** 点；
  - Qwen3-32B：响应长度缩短 **40%**，准确率降 **2.5** 点；
  - Format-Adaptive-Answer 在 Qwen3-8B 上实现平均 **33%** 长度缩减且准确率仅降 1.2 点；
  - 相较基线的 AUC-OAA 分数提升 5 点（71.6 → 76.6），比第二名方法高 **2.5 点**。
- **模型规模趋势**：缩减比例随模型规模增加而增加（1.7B: 22% → 8B: 28% → 32B: 40%），说明**越大越强的模型从高效推理训练中获益越多**。
- **奖励机制的有效性**：训练后的模型即使在正确答案出现后，也会**主动减少重复自我校验和换法重算（sanity check）**等冗余行为；
- **领域无关性**：尽管只在数学上训练，推理效率的提升可以迁移到科学、代码、长上下文等非数学任务上（缩减幅度略小但仍有效）。
- **SFT 的必要性**：不带 SFT 的纯 RL 在准确率上有明显劣势，SFT 与 RL 组合才能同时兼顾精度和效率。

## 7. 优点（方法或实验设计上的亮点）

- **奖励函数设计简洁而轻量**：只惩罚"首个正确答案之后"的冗余 token，既有明确的可验证性、又保留了模型自我纠错空间，相比复杂的基于组内归一化或硬截断的方法效果好且实现简单；
- **无需为每个输入预先设定推理预算**：模型通过训练自我学会"何时该继续推理、何时该停止"，具备真正的**自适应能力**；
- **对"过度思考"给出了精细的行为解读**：图 6 明确展示模型从 7 次自我校验降至 2 次乃至 0 次的过程，并结合 quantitative analysis 区分了"同法重复校验"vs"异法 sanity check"两种自我验证的形式，分析深入；
- **使用了 AUC-OAA 统一度量**，解决了"准确率-长度"不可直接比较的问题，使跨方法比较更公平；
- **在 DeepSeek 模型上的结果也保持稳定**，表明方法对模型族有一定通用性；
- **验证了数学任务中习得的推理风格具有迁移性**。

## 8. 不足与局限

- **训练域限制**：只在数学数据集中训练，对代码、科学、长上下文领域的效果（尤其是 LiveCodeBench 和 LongBenchv2 上的表现）弱于数学任务，跨域泛化仍有提升空间；
- **依赖可验证答案**：奖励函数要求存在确定性的"正确/错误"判断标准，无法直接推广到开放式生成、创意写作或主观问答等**弱可验证任务**；
- **方法属于事后干预（post hoc）**：未探索将自适应长度惩罚直接加入模型初始 RL 训练阶段的方案，对从零训练推理模型的借鉴意义有待验证；
- **模型范围有限**：仅覆盖 Qwen3 系列稠密模型及一个 DeepSeek 蒸馏模型，未覆盖 MoE 架构或其他主流模型族；
- **评估范围聚焦于推理任务**：未衡量训练后模型在通用能力（如指令跟随、事实问答、安全性等）上的潜在变化或灾难性遗忘风险；
- **一个小代价**：Format-Adaptive-Answer 去除了推理末尾的总结摘要，可能降低推理过程的可读性，对需要用户核验推理过程的场景不够友好；
- **计算资源报告不透明**：未报告 GPU 类型/数量/训练时长，难以评估方法复现的实际算力成本。

（完）
