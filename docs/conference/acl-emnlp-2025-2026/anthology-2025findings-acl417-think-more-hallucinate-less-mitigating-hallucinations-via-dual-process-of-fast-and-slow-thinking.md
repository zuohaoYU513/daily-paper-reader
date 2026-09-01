---
title: "Think More, Hallucinate Less: Mitigating Hallucinations via Dual Process of Fast and Slow Thinking"
title_zh: 多思考少幻觉：通过快慢思维双过程缓解幻觉
authors: "Xiaoxue Cheng, Junyi Li, Wayne Xin Zhao, Ji-Rong Wen"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.417.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 提出基于树搜索的HaluSearch框架，在推理阶段缓解LLM幻觉
tldr: 针对自回归生成缺乏审慎推理导致幻觉的问题，提出结合树搜索的显式慢思考框架HaluSearch。它将文本生成视为逐步推理过程，用自评估奖励模型为每一步打分并引导搜索走向最可靠路径。在平衡效率的同时显著降低幻觉，提升生成内容的可信度和事实准确性。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl417/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 678, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl417/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 840, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl417/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1660, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl417/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 323, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl417/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1650, \"height\": 844, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl417/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 425, \"label\": \"Table\"}]"
motivation: 典型自回归生成缺乏审慎推理，易产生不可信和事实错误的内容。
method: HaluSearch将生成框架转为逐步推理，结合MCTS树搜索和自评估奖励模型选择可靠路径。
result: 实验显示HaluSearch在多个任务上显著减少幻觉，并兼顾效率。
conclusion: 显式慢思考推理可有效抑制LLM幻觉，提升生成可靠性。
---

## Abstract
Large language models (LLMs) demonstrate exceptional capabilities, yet still face the hallucination issue. Typical text generation approaches adopt an auto-regressive generation without deliberate reasoning, often leading to untrustworthy and factually inaccurate responses. In this paper, we propose HaluSearch, a novel framework that incorporates tree search-based algorithms (e.g., MCTS) to enable an explicit slow thinking generation process for mitigating hallucinations during inference. Specifically, HaluSearch frames text generation as a step-by-step reasoning process, using a self-evaluation reward model to score each generation step and guide the tree search towards the most reliable generation pathway. To balance efficiency and quality, we introduce a hierarchical system switch mechanism, which dynamically switches between fast and slow thinking modes at both instance and step levels. We conduct extensive experiments on both English and Chinese datasets, and the results show that our approach significantly outperforms baseline approaches.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 大型语言模型（LLM）在生成文本时存在严重的**幻觉问题**，即产生不可信、与事实不符的内容。
- 典型的自回归生成方式缺乏**审慎推理**，是导致幻觉的重要原因之一。
- 现有推理阶段的缓解方法（如RAG、CoT、自一致性等）多停留在**响应级**或仍受自回归范式约束，中间错误容易累积，无法充分挖掘模型内部知识。
- 论文借鉴认知科学中的**双过程理论**（System 1 快思考 / System 2 慢思考），提出在推理阶段引入显式的、逐步的“慢思考”过程，以缓解幻觉。
- 整体含义：将文本生成从“快速直觉式”转变为“可规划的审慎推理”，从而提升LLM输出的可靠性与事实准确性。

## 2. 论文提出的方法论

### 核心思想
- 提出 **HaluSearch** 框架，使用**蒙特卡洛树搜索（MCTS）**将文本生成转化为**逐步推理过程**。
- 将每个“句子”视为一个推理步骤，通过树搜索探索多条生成路径，并用**自评估奖励模型**对每一步打分，引导搜索走向最可靠的路径。
- 同时引入**动态系统切换机制**，在实例级和步骤级自适应地在快思考（System 1）和慢思考（System 2）之间切换，平衡效率与质量。

### 关键技术细节
- **问题建模**：将回答 `y = ⟨y1, ..., yT⟩` 视为逐步生成，每个句子 `yt` 对应树中一个节点，节点包含生成句子、访问次数 `N(st)` 和值 `V(st)`。
- **MCTS 四阶段**：
  1. **选择（Selection）**：从根节点开始，按 UCT 分数选择最有探索潜力的叶节点。  
     UCT 公式：`UCT(st) = V(st) + w·√(ln N(p) / N(st))`，其中 `w` 控制探索与利用的平衡。
  2. **扩展（Expansion）**：用策略模型生成 `K` 个候选下一句作为子节点。
  3. **评估（Evaluation）**：对每个子节点做 `m` 次 rollout，用奖励模型评分，取平均值作为该节点初始值。
  4. **反向传播（Backpropagation）**：沿路径更新祖先节点的访问次数和值。
- **终止条件**：达到最大迭代次数 `M`，或遇到低于奖励阈值（低幻觉风险）的终节点。
- **最终选择**：采用贪心策略沿最高值路径拼接句子作为最终回答。

### 奖励模型（自评估）
- 用 GPT-4 对 rollout 生成响应按 1–5 分打分（分数越高幻觉风险越高），并包含真实答案作为参考。
- 训练两种奖励模型：
  - **生成式奖励建模（Generative RM）**：直接预测分数。
  - **基于批评的奖励建模（Generative RM + Critic）**：先生成批评分析，再预测分数。
- 训练损失采用交叉熵，在策略模型同源基础模型上 SFT 微调。

### 动态系统切换（MCTSwitch）
- **实例级切换**：判断当前问题是否需要慢思考（简单问题直接用 System 1）。
- **步骤级切换**：在 MCTS 扩展时，根据当前节点值是否超过阈值 `γ` 决定该步骤用快或慢思考生成子节点。
- **切换模型训练**：从搜索树中根据节点值标注标签（值>γ 为需要慢思考，否则为快思考）；实例级则根据直接生成的正确性标注。混合训练获得切换模型。

## 3. 实验设计

### 数据集与场景
- **英文**：HaluEval-QA、TruthfulQA、SimpleQA
- **中文**：HalluQA、ChineseSimpleQA、ChineseFactEval
- 评估指标：**准确性（Accuracy）**，使用 GPT-4 对比模型输出与标准答案进行判定。

### 策略模型
- Llama3.1-8B-Instruct
- Qwen2-7B-Instruct

### 对比基线
- **Direct Generation**（直接生成，作为下限参考）
- **Chain-of-Thought (CoT)**：零样本 CoT 提示
- **Self-Consistency (SC)**：多响应采样选取一致性最高者
- **Best-of-N (BoN)**：通过奖励模型从 N 个响应中选最优
- **Self-Refine**：自我反馈迭代改进
- **ITI (Inference-Time Intervention)**：推理时激活干预（仅在英文数据集上报告，因其在 TruthfulQA 上调优）

### 实现细节（部分）
- MCTS：每步扩展 10 个节点，每个节点 5 次 rollout，最大模拟 20 次，UCT 权重 `w=0.4`。
- SC 和 BoN 采样 20 条响应。
- 解码温度 0.9，零样本设置。

## 4. 资源与算力

- 论文**未明确说明**使用的 GPU 型号、数量、训练时长等具体算力资源。
- 仅提及训练奖励模型数据规模：过滤后获得 **52K 条奖励数据**和 **38K 条批评数据**。
- 从方法本身推断，MCTS 推理计算成本较高（如慢思考模式下每问题平均推理时间可达 53.3 秒），但论文未提供硬件配置细节。

## 5. 实验数量与充分性

### 实验组数量
- **主实验**：在 6 个数据集（英/中）× 2 个策略模型，与 6 类方法对比，共 12 组核心结果（表1）。
- **奖励模型分析**：对比 GPT-4 RM、Generative RM、Generative RM + Critic 三种奖励模型（表2）。
- **系统切换分析**：不同阈值 `γ` 对准确率和推理时间的影响（图2）。
- **超参数分析**：扩展节点数 {10,20,50} 和模拟次数 {10,20,30} 的影响（图4）。
- **案例研究**：展示了一个 TruthfulQA 上的推理过程示例。

### 充分性与客观性
- 实验覆盖面较广：涵盖中英文、多种问答难度、多种基线类型（提示、采样、干预、自我精炼）。
- 奖励模型和切换模型的训练均使用合成数据，在一定程度上存在**数据偏差风险**（依赖 GPT-4 打分和正确标签）。
- ITI 仅报告英文结果，比较时未在中文上公平对齐，但作者已说明原因。
- 总体而言，实验设计较充分，结果可信；但缺少对更大参数量模型（如 70B）或更强模型（如 GPT-4 作为策略模型）的验证。

## 6. 论文的主要结论与发现

- **HaluSearch 在所有六个数据集上均取得最佳结果**，显著优于所有基线（如 Llama3.1 在 HaluEval-QA 上达到 45.40%，而 Direct Generation 仅 35.60%；Qwen2 在 ChineseFactEval 上达 70.40%，优于基线最大值 64.00%）。
- 逐步细粒度的奖励信号能**有效减少错误累积**，比响应级方法更有效地缓解幻觉。
- **基于批评的奖励模型**优于纯生成式奖励模型，甚至在部分数据集上超过 GPT-4 仅打分的效果（如 TruthfulQA 上 Llama3.1 达到 50.00% vs GPT-4 RM 47.50%）。
- **动态系统切换机制**能在准确率和推理成本之间取得良好折中，阈值越高，慢思考比例越低，推理时间大幅下降而准确率仅略有降低。
- 增加 MCTS 扩展节点数和模拟次数可以提升性能，但收益递减，受限于模型内部知识和奖励模型精度。

## 7. 优点

- **方法创新性强**：将认知科学的双过程理论引入 LLM 幻觉缓解，提出“快慢思维动态切换”的新范式。
- **细粒度推理**：基于句子的逐步奖励，比响应级方法更精细，能定位和避免局部错误。
- **自评估奖励模型**：可训练、不依赖闭源大模型，且引入“批评”步骤提升评分准确性。
- **效率与质量平衡**：通过实例/步骤双重切换，避免所有输入都进行昂贵的慢思考，实用性强。
- **实验规模较扎实**：中英文双覆盖、多数据集、多基线，验证了方法的通用性和鲁棒性。

## 8. 不足与局限

- **计算成本高**：即使有系统切换，慢思考模式的 MCTS 仍非常耗时（每次问答平均数十秒），不适用于实时场景。
- **算力资源未披露**：未说明 GPU 型号、数量、训练时长，影响可复现性和成本评估。
- **实验规模有限**：仅使用 8B 量级策略模型，未覆盖更大或更强模型；未在更多领域（如对话、长文本生成）验证。
- **数据偏差风险**：奖励模型和切换模型的训练数据均由 GPT-4 生成和标注，可能引入 GPT-4 自身的偏见；数据平衡只靠 TF-IDF 去重和分布调整，可能仍不充分。
- **切换模型性能依赖**：系统切换的准确性受限于切换模型自身能力，若判断失误会导致质量或效率损失。
- **方法应用限制**：主要针对单轮问答，对多轮或开放式生成任务可能不适用；奖励函数的设计也依赖人工设定标准。

（完）
