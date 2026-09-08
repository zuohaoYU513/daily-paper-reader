---
title: "Confidence v.s. Critique: A Decomposition of Self-Correction Capability for LLMs"
title_zh: 自信与批判：大语言模型自我纠错能力的分解
authors: "Zhe Yang, Yichang Zhang, Yudong Wang, Ziyao Xu, Junyang Lin, Zhifang Sui"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.203.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 通过比较自我纠错前后的答案正确性来区分自信与批判，属于对自我作答的元认知评估。
tldr: 针对大语言模型自我纠错后准确率可能下降的问题，论文将自我纠错能力分解为自信与批判两个因子：自信对应保持正确答案的能力，批判对应把错误转为正确的能力。基于纠错前后回答正确性的枚举与概率刻画，提出评估这两种能力以及整体自纠错质量的指标。该分解有助于定位自我评估与自我纠错的薄弱环节，为提升模型元认知水平提供分析工具。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1585, \"height\": 517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 343, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 185, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 587, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 179, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 737, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 782, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 817, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 795, \"height\": 1420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long203/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1581, \"height\": 467, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long203/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1620, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long203/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1605, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long203/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 744, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long203/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1642, \"height\": 1220, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long203/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 397, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long203/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1384, \"height\": 521, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long203/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1636, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long203/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1621, \"height\": 575, \"label\": \"Table\"}]"
motivation: 模型自我纠错有时导致准确率下降，需要对自我纠错能力进行细粒度分解与量化分析。
method: 枚举自我纠错前后的回答正确性，将自纠错能力分解为自信与批判两种能力并提出概率化评估指标。
result: 借助该分解与指标开展实验分析，揭示模型在自信和批判两个维度上的行为差异。
conclusion: 自我纠错应被拆解为置信度和批判能力来研究，这有助于解释为何自纠错可以提升也可能损坏回答质量。
---

## Abstract
Large Language Models (LLMs) can correct their self-generated responses, but a decline in accuracy after self-correction is also witnessed. To have a deeper understanding of self-correction, we endeavor to decompose, evaluate, and analyze the self-correction behaviors of LLMs. By enumerating and analyzing answer correctness before and after self-correction, we decompose the self-correction capability into confidence (being confident to correct answers) and critique (turning wrong answers to correct) capabilities, and propose two metrics from a probabilistic perspective to measure these 2 capabilities, along with another metric for overall self-correction capability evaluation. Based on our decomposition and evaluation metrics, we conduct extensive experiments and draw some empirical conclusions. For example, we find different models can exhibit distinct behaviors: some models are confident while others are more critical. We also find the trade-off between the two capabilities (i.e. improving one can lead to a decline in the other) when manipulating model self-correction behavior by prompts or in-context learning. Further, we find a simple yet efficient strategy to improve self-correction capability by transforming Supervision Fine-Tuning (SFT) data format, and our strategy outperforms vanilla SFT in both capabilities and achieves much higher accuracy after self-correction.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：大语言模型可以进行内在的自我纠错（intrinsic self-correction），即不借助外部反馈，自行检查并修订自己生成的答案。这种能力模仿了人类的反思过程，理论上能提升模型在数学、代码等任务上的表现。
- **核心困惑**：现有研究中存在明显争议——有些工作报告自我纠错可以提升准确率，另一些则发现模型在纠错后准确率反而下降，甚至无法判断自己答案的对错。
- **研究动机**：这种争议说明，仅仅笼统地看待“自我纠错”这一能力是不够的，需要更细粒度地剖析其内部机制。例如，判断一个答案本身是否正确、是否有信心坚持它、能否发现并修正错误，实际上是不同的认知环节。
- **目标含义**：文章提出一种系统性的方法论，将自我纠错能力分解为两个可量化的子能力——**自信能力（confidence）** 和**批判能力（critique）**，并配套提出度量指标、开展大规模实证分析，最后给出一种改进训练策略。这项研究有助于解释为何自我纠错有时有益、有时有害，也为设计更好的“自我反思／元认知”机制提供了分析工具与分析框架。

---

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 核心思想
- 通过枚举自我纠错前后答案的正确性，将结果划分为四种场景：
  1. **自信（✓ → ✓）**：初始答案正确，纠错后仍保持正确；
  2. **不自信（✓ → ✗）**：初始答案正确，但纠错后反而改错；
  3. **批判（✗ → ✓）**：初始答案错误，但经过反思改正；
  4. **固执（✗ → ✗）**：答案错误且坚持不改。
- 这四种场景进一步浓缩为两个核心能力：
  - **自信能力**：面对“正确”答案时坚持不动的能力（对应场景1 vs 场景2）；
  - **批判能力**：面对“错误”答案时纠正过来的能力（对应场景3 vs 场景4）。

### 评价指标
- 从概率视角定义了两个关键指标：
  - **Confidence Level（CL）**：给定初始答案正确时，自我纠错后仍答对的**条件概率**，即 `P(b|a)`；
  - **Critique Score（CS）**：给定初始答案错误时，自我纠错后转为正确的**条件概率**，即 `P(b|¬a)`。
- 从数学上证明了自我纠错后的准确率（Accuracy 2, `Acc2`）满足如下关键恒等式：

$$\text{Acc}_2 = \text{Acc}_1 \times CL + (1 - \text{Acc}_1) \times CS$$

其中 `Acc1` 是自我纠错前的准确率。这说明 `Acc2` 本质上是 `CL` 与 `CS` 的加权求和，从概率分解上验证了分解的合理性。
- 针对“不同模型 `Acc1` 不同、用 `Acc2` 无法公平比较自纠错能力”的问题，作者进一步提出**相对自纠错分数（Relative Self-Correction Score, RSS）**：它先推导 `Acc2` 的理论上下界，再衡量实际 `Acc2` 在上下界区间中的相对位置，从而去除初始准确率的影响。RSS 大于 0.5 表示纠错后准确率提升，小于 0.5 表示下降。

### 概率估计方法
- **生成类任务（generation tasks）**：对同一问题重复采样（通常采样次数约 3–10 次），根据初始答案和纠错后答案的正确性频率来估计 `P(ai)`、`P(bi|ai)` 和 `P(bi|¬ai)`。
- **分类任务（classification tasks）**：利用模型输出的 logits，仅保留候选标签对应的概率，经过 softmax 后直接读取候选标签的概率来进行估计；对于错误标签的情形，按全概率公式对各错误标签的修正概率加权求和。

### 改进训练方法（CCT）
- 提出 **Confidence-and-Critique Improvement Tuning（CCT）**，由两部分组成：
  - **CLT（Confidence Level Improvement Tuning）**：以“用户问题 + 一个正确初始答案”为上下文，训练模型输出正确且保持该答案；
  - **CST（Critique Score Improvement Tuning）**：以“用户问题 + 一个错误初始答案”为上下文，训练模型将其纠正为正确终答。
- CCT 的构造方式简单：直接由普通 SFT 训练数据自动转换而来，不依赖外部验证器等结构。

---

## 3. 实验设计：数据集 / 场景 / Benchmark / 对比方法

### 使用的数据集
覆盖六个数据集，对应不同的任务场景：

- **数学推理**：GSM8k；
- **代码生成**：Humaneval；
- **指令跟随**：IFEval；
- **综合知识/推理**：MMLU；
- **常识问答**：CommonsenseQA；
- **阅读理解（是非分类）**：BoolQ。

### 评测与对比方法
- **被评测模型**（均为对齐/指令微调版本）：
  - 开源模型：Llama3-8B/70B-Instruct、Qwen2.5-7B/72B-Chat、Deepseek-7B/67B-Chat、Mistral-7B-Instruct-v3、GLM4-9B-Chat；
  - 闭源模型：Qwen-Max、GPT-3.5 Turbo、GPT-4 Turbo。
- **行为操控实验**（不微调）：
  - 使用三类提示词：`Reask`（基线）、`Confidence Prompt`（强调信心）、`Critique Prompt`（强调置疑和复查）；
  - 使用不同的上下文学习示例（ICL，4-shot），调整“自信示例”与“批判示例”比例。
- **改进实验**（微调）：
  - 以 Llama2-7B-Base 为基础模型，对比了 SFT、CLT、CST、CCT、SFT+CCT；
  - 进一步探讨了 CLT 与 CST 训练数据不同混合比例（从 0% 到 100%）对 CL、CS、Acc1、Acc2 的影响。

---

## 4. 资源与算力（基建信息）

- 论文在正文中并未给出完整的训练算力账单（如总 GPU 小时数、训练时长等）。
- 在附录中可以找到的部分信息：
  - 面试实验使用 NVIDIA A100 80G GPU：小模型（<10B）用 1 张；70B 级大模型用 4 张 A100 80G，并使用 vLLM 加速推理；
  - 闭源模型通过 API 调用获取结果；
  - 微调实验使用 LoRA（rank=64, alpha=16, dropout=0.1），学习率 5e-5，混合精度 bf16；BoolQ 和 GSM8k 训练 2 epochs，MMLU 训练 1 epoch；
  - 未提供端到端训练时间、总 GPU 消耗量或碳排放等量的信息。

---

## 5. 实验数量与充分性

### 实验数量
- 论文的实证覆盖面较广：
  - 在 6 个不同类型的数据集上、对 11 种不同规模与系列的模型进行自我纠错能力评估；
  - 报告了 `Acc1`、`Acc2`、`CL`、`CS` 四个指标，并给出了 RSS 结果的表格；
  - 做了一组行为操控实验：不同类型的 prompt（2 个变体 vs 基线）、ICL 示例比例调节（0–4 个自信示例）；
  - 在 3 个数据集上进行了训练方法对比（SFT/CLT/CST/CCT/SFT+CCT）；
  - 在 BoolQ 上进行了数据混合比例的消融实验（每个比例测试 3 次并取平均）。

### 充分性 / 客观性评估
- **优点**：实验囊括了数学、代码、常识、知识、指令、是非题等多种任务维度，既包含开源也包含闭源模型，既有零样本也有 ICL 与微调场景，证据链条较完整；RSS 的提出也能较好地消除初始能力差异。
- **不足**：
  1. 对闭源模型由于无法获取 logits，只能增加采样次数来估计概率，估计精度不同；
  2. 作者的“分解”依赖于对初始答案正误的二值化判断，仅将错误来源归结为“固执”或“批判失败”，无法区分“模型明明不会却固执”与“问题超纲”等不同原因；
  3. 行为操控实验只选取了 Llama3-8B-Instruct 一个模型，推广性有限；
  4. ICL 实验只对 4-shot 场景进行了分析；
  5. 微调实验仅在 7B 规模模型（Llama2-7B-Base）上进行，未验证更大规模或更强基座模型上的效果。

---

## 6. 论文的主要结论与发现

1. **自我纠错不必然带来准确率提升**：如 GSM8k 上 GPT-3.5 Turbo 的 RSS 显著高于 GPT-4 Turbo，后者虽然 Acc1、Acc2 绝对值更高，但其纠错实质上是“拖后腿”的。
2. **总体而言，模型的自信能力高于批判能力**：多数模型的 CL 相对较高（90% 上下），而 CS 常较低（部分模型只有 1%–20%），说明“改错”能力普遍是自我纠错中的短板。
3. **不同模型存在明显的行为性格差异**：
   - “保守型”模型（如 Deepseek-7B-Chat、Mistral-7B-Instruct）具有高 CL、低 CS；
   - “激进/反叛型”模型（如 Llama3-8B-Instruct、GLM4-9B-Chat）呈现低 CL、高 CS。
4. **同系列模型行为趋于一致**（Llama3 系列偏“批判”、Qwen 系列偏“自信”），说明自纠错行为特征可能与预训练语料和训练策略相关，而非完全随机。
5. **在不微调的情况下，自信能力和批判能力之间呈“跷跷板”关系**：
   - 使用“自信提示词”会提升 CL 但压低 CS；
   - 使用“批判提示词”会提高 CS 但显著降低 CL；
   - ICL 中自信示例越多则 CL 越高、CS 越低，反之亦然。
6. **普通 SFT 效果有限**：SFT 得到最高的初始 Acc1，却无法有效教会模型自我纠错，自纠错后准确率提升极小。
7. **CCT 能同时提升 CL 与 CS**：与普通 SFT 相比，CCT 打破了上述“跷跷板”，在三个任务上的 Acc2 都显著高于其他微调方案；最佳 CLT 数据比例约 40%。
8. **SFT+CCT 可兼得基础能力与纠错能力**：将 CCT 数据加入 SFT 可视为一种数据增强策略，能在保持较高 Acc1 的同时获得较高 Acc2。

---

## 7. 优点：方法或实验设计的亮点

- **概念分解清晰、可操作**：将抽象的“自我纠错能力”拆解为“对正确答案的自信”和“对错误答案的批判”，对应关系直观，且有清晰的形式化定义。
- **概率化指标数学推导严谨**：
  - 给出 CL、CS 的概率定义与推导过程；
  - 推导出 `Acc2 = Acc1·CL + (1-Acc1)·CS` 这一简洁恒等式，揭示了它们之间的线性关系；
  - RSS 的设计有上界下界作为锚点，使不同初始能力模型之间的自纠错效果可以公平比较。
- **实验覆盖广**：任务类型多样（数学、代码、指令、常识、知识、是非题），模型跨度从 7B 到闭源超大模型，结论具有一定的普遍性。
- **对以往争议提供了解释框架**：指出不同论文中“自我纠错有用/无用”的争论可能源于提示词不同或模型特性不同，核心差异可以在 CL 与 CS 的坐标系内进行解释。
- **改进方案简单有效、易于落地**：CCT 不需要复杂的外部验证器、多轮强化学习等复杂结构，仅通过将现有 SFT 数据做格式转换（把初始答案作为上下文）即可实现，具备较强的实用价值。

---

## 8. 不足与局限

- **计算代价较高**：需要针对同一问题多次重复采样（或获取多次 logits）来估计概率，成本显著高于一次性的准确率评测，不适合大规模快速评测场景。
- **分析粒度较粗**：
  - 将“错误”一律归为 `¬a`，无法区分“模型因能力不足而答错”与“模型知道答案但输出失误”等不同错误子类型；
  - 只能评估数据集总体层面的 CL/CS，不能指出具体哪类问题更容易触发自信或批判行为。
- **指标边界条件依赖假设**：RSS 推导依赖 `CS ≤ Acc1 ≤ CL` 的经验不等式，论文虽给出实验证据说明通常成立，但在理论上并非对所有模型都严格保证。
- **反事实与实际推理过程并不完全一致**：概率指标假设纠错前后是条件独立/一次采样关系，而真实模型在纠错时可能受多种随机因素影响，马尔可夫式简化可能不足以描述多轮自我反思。
- **行为操控实验规模有限**：prompt 和 ICL 操控只在 Llama3-8B 上验证；不同模型对 prompt 的敏感性差异可能极大，结论外推需谨慎。
- **训练实验的规模与基座局限**：只使用 7B 规模的 base 模型做 LoRA 微调，未能展示 CCT 在更大模型或 Chat 模型上的增益效果。
- **混合策略仍较静态**：只探索了固定比例的 CCT 数据混合，没有尝试训练中动态调节 CLT/CST 比例的更优策略。
- **机理层面的解释有限**：作者观察到同系列模型行为相似，但未能从预训练数据或对齐策略层面揭示更深层原因。

---

（完）
