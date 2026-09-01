---
title: Active Layer-Contrastive Decoding Reduces Hallucination in Large Language Model Generation
title_zh: 主动层对比解码减少大语言模型生成中的幻觉
authors: "Hongxiang Zhang, Hao Chen, Muhao Chen, Tianyi Zhang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.150.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过主动层对比解码减少大模型生成幻觉
tldr: 大语言模型即使在长上下文中也容易产生幻觉，现有解码方法多局限于token层面的对比，难以捕捉深层事实性信号。本工作提出ActLCD，将解码建模为序列决策问题，利用奖励感知分类器指导的强化学习策略动态决定何时进行层间对比。实验表明该方法能有效降低幻觉、提升生成事实性。该工作为解码阶段幻觉缓解提供了新范式。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main150/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1562, \"height\": 975, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main150/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main150/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 625, \"height\": 1418, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 795, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1639, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 670, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 805, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 805, \"height\": 459, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 797, \"height\": 1647, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 794, \"height\": 714, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 803, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 719, \"height\": 1603, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1644, \"height\": 2042, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1643, \"height\": 1442, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main150/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1627, \"height\": 1471, \"label\": \"Table\"}]"
motivation: 现有解码方法多基于token层面对比内部表示，无法充分抑制长上下文中出现的幻觉。
method: 提出ActLCD，将解码视为序列决策问题，用强化学习策略和奖励感知分类器动态决定对比层。
result: 实验显示ActLCD在减少幻觉、提升事实性方面优于基线方法。
conclusion: ActLCD展示了解码阶段按需进行层对比的可行性，为幻觉缓解提供新思路。
---

## Abstract
Recent decoding methods improve the factuality of large language models (LLMs) by refining how the next token is selected during generation. These methods typically operate at the token level, leveraging internal representations to suppress superficial patterns. Nevertheless, LLMs remain prone to hallucinations, especially over longer contexts. In this paper, we propose Active Layer-Contrastive Decoding (ActLCD), a novel decoding strategy that actively decides when to apply contrasting layers during generation. By casting decoding as a sequential decision-making problem, ActLCD employs a reinforcement learning policy guided by a reward-aware classifier to optimize factuality beyond the token level. Our experiments demonstrate that ActLCD surpasses state-of-the-art methods across five benchmarks, showcasing its effectiveness in mitigating hallucinations in diverse generation scenarios.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 论文的核心问题与整体含义

- **研究动机**：大语言模型（LLM）在长文本生成中仍然普遍存在幻觉（Hallucination）问题，即生成看似流畅但事实错误的内容。
- **现有方法的局限**：主流的解码阶段事实性增强方法（如 DoLa、SLED）基于 token 级别的层间对比（Layer Contrasting），但它们对每一步解码独立进行静态干预，存在两个问题：
  - 对所有 token 一刀切地应用层对比，可能导致模型对简单预测“过度思考”；
  - 缺乏序列级优化，早期错误会在自回归解码中累积放大，形成“幻觉雪球效应”（Hallucination Snowballing）。
- **论文的整体含义**：提出一种新的解码策略 ActLCD，将解码视为序列决策问题，用强化学习动态决定**何时**激活层对比，从而在 token 级之上引入序列级的事实性优化。

### 2. 论文提出的方法论

**核心思想**：ActLCD（Active Layer-Contrastive Decoding）通过强化学习训练一个策略网络，在生成过程中对每个 token 决定是否应用层对比解码，既保留层对比增强事实信号的优势，又避免不必要的干预和错误累积。

**技术细节**：

- **形式化**：将解码建模为马尔可夫决策过程（MDP），状态 `st` 从中间层嵌入和 logits 中提取，动作 `at ∈ {0, 1}` 表示是否应用层对比。
- **目标函数**：结合两种解码目标：
  - `F(qN, qM)`：层间对比目标（沿用 DoLa 的对比机制）；
  - `qM`：贪心解码目标；
  - 两者通过动作 `at` 加权混合。
- **奖励设计**：基于 token 级真值标签设计序列级奖励：
  - 真阳性（正确激活）：+1.0；
  - 真阴性（正确不激活）：+2.0（鼓励稀疏、按需激活）；
  - 假阳性（多余激活）：-1.0；
  - 假阴性（漏激活）：-5.0（重点惩罚，保证事实性优先）。
- **训练流程**：采用离线强化学习框架 BCQ（Batch-Constrained Q-learning）：
  - **Stage 1（行为克隆）**：在注释数据上训练策略网络 `πφ`，学习经验中的激活模式，用于初始化并提供离线分布约束；
  - **Stage 2（Q-learning）**：训练 Q 网络，并通过概率阈值 τ 限制动作选择空间，防止离线数据外推，减小分布偏移。
- **推理**：每个时间步选择满足约束且 Q 值最大的动作，决定是否激活层对比。
- **数据注释**：用 GPT-4o（或 Llama-3-70B）标注 span 级幻觉，再通过确定性匹配算法将 span 对齐到 token，生成训练标签。

### 3. 实验设计

**数据集 / 基准**：

1. **TruthfulQA**：317 个短答案问题，评估事实性（Truth）和信息量（Info），复合指标 `T*I`；
2. **LongFact**：长文档事实性（2,280 个提示，采样 120 个用于评估），衡量 Precision、Recall@128、F1@128；
3. **StrategyQA**：多跳隐式推理基准，需生成思维链（CoT）；
4. **GSM8K**：数学应用题，需算术推理与事实理解；
5. **Package hallucination**（域特定）：评估 LLM 推荐软件包时产生的不存在/不相关包幻觉，用 pip-search/npm-search 验证真伪。

**模型**：

- 通用 LLM（5 个）：LLaMA-3.1-8B、GLM-4-9B-Chat、Gemma-2-9B-it、Mistral-7B-Instruct-v0.3、DeepSeek-V2-Lite-Chat；
- 代码 LLM（4 个，用于包幻觉基准）：CodeGemma-7B-it、DeepSeek-Coder-V2-Lite-Instruct、Qwen2.5-Coder-7B-Instruct、Codestral-22B-v0.1。

**对比方法**：Greedy、DoLa（层间对比解码）、SLED（自 logits 演化解码）。

**评估方式**：TruthfulQA 用 GPT-4o-mini 评估 Truth/Info；LongFact 用 GPT-4o-mini 提取原子事实并验证；CoT 任务按标准准确率度量；包幻觉基准按幻觉率度量。

### 4. 资源与算力

- 论文**未明确说明**使用了多少 GPU 型号、数量或训练时长。
- 从方法实现上看，ActLCD 在推理时为每步引入一个轻量策略网络，作者报告的解码延迟相比 DoLa 仅增加约 3%–5%，开销很小。
- 训练阶段使用离线数据集（由 GPT-4o 或 Llama-3-70B 注释），所需训练资源应远小于模型微调，但论文未提供具体算力数字。

### 5. 实验数量与充分性

- **覆盖面较广**：
  - 5 个通用 LLM + 4 个代码 LLM，共 9 个模型；
  - 5 个基准（短问答、长文档、CoT 推理 x2、领域包幻觉），涵盖短句到文档级生成。
- **消融与分析**：
  - 对比了阈值式激活（Confidence Threshold）替代方案，验证 RL 策略的必要性；
  - 比较 BC-only 与 BC+RL 结果，证明 Q-learning 阶段的有效性；
  - 测试了不同注释源（GPT-4o vs Llama-3-70B）的鲁棒性；
  - 分析了浅层 bucket 选择的敏感性，ActLCD 总体比 DoLa 更稳定；
  - 报告了延迟开销，并在 GSM8K 和 StrategyQA 上各给出一个案例研究。
- **公平性**：对 SLED 进行了超参数搜索（evolution_rate/evolution_scale），尽力复现其最优配置；DoLa 用 Hugging Face 现成实现，整体对比较为规范。
- **局限**：每个 LongFact 只采样 120 条（全文提到 2,280 个提示但只评估 120 个，是为控制成本），可能对长文档场景的统计效力有限；包幻觉基准上，部分 DoLa 结果大幅劣化（如 CodeGemma 的 JS 从 12.94% 恶化到 22.43%），原因未展开分析。

### 6. 论文的主要结论与发现

- **主要结果**：ActLCD 在 TruthfulQA、LongFact、StrategyQA、GSM8K 和包幻觉基准上全面超越 DoLa 和 SLED，最大增幅分别为 +19.81%（Mistral3，T*I）、+3.30%（LLaMA3.1，F1@128）、+7.51%（LLaMA3.1，StrQA）、+7.21%（LLaMA3.1，GSM8K）以及 +6.5%（Python）/ +5.6%（JS）包幻觉率下降。
- **序列级优化是关键**：与在每一步独立做 token 级对比的方法不同，ActLCD 能识别哪些情境需要激活层对比，避免早期错误级联，显著缓解幻觉雪球。
- **鲁棒性验证**：在不同模型架构、不同任务类型和不同注释源下均获得一致提升，不同于 DoLa/SLED 在某些模型上出现性能退化。
- **效率可控**：推理时引入的策略网络开销很小，适合实际部署。

### 7. 优点

- **方法层面**：
  - 将解码从静态 token 级对比提升到序列级决策，理论上更能应对多步推理中的误差累积；
  - 不依赖外部检索或多轮采样，只需模型内部信息，单次前向即可完成推理；
  - 奖励函数经仔细设计（强惩罚漏激活），兼顾事实性与信息量。
- **实验层面**：
  - 覆盖面广：短问答、长文档、CoT、数学推理、领域特定包幻觉均有评测；
  - 多种补充分析（阈值变体、BC-only、注释源、浅层选择、延迟）验证了设计选择的合理性；
  - 对 SLED 的超参数进行调优，尽力保证基线公平。
- **实际价值**：训练好的策略网络可以即插即用地用于不同基础模型，对生产环境的计算开销影响很小。

### 8. 不足与局限

- **训练依赖注释**：需要先对生成序列做 token 级幻觉标注，注释质量会影响最终策略；虽然验证了 Llama-3-70B 注释的可行性，但整体流程仍比纯无监督解码方法更复杂（需要为每个目标模型或任务重新收集数据）。
- **论文未明确提供训练算力细节**，包括 GPU 型号、卡数、训练时长，外部复现时的资源估算较困难。
- **并非所有场景都稳定提升**：在 LongFact 上对 GLM-4 的 F1@128 和 R@128 出现下降（-5.76 和 -1.45），说明长文档场景下仍可能牺牲信息量；包幻觉上未解释为何 DoLa/Codestral 等基线会发生显著退化。
- **评估依赖 LLM 裁判**：TruthfulQA 和 LongFact 的事实性判断均使用 GPT-4o-mini，可能引入裁判模型的偏差或噪声。
- **局限性（原文自述）**：当基础模型本身缺乏足够领域知识时，任何解码策略都无法完全消除幻觉。
- **扩展性**：当前只考虑“激活/不激活”的二元决策，未来可以探索更细粒度的干预方式（如层选择、对比强度的软调节等），进一步提升事实性上限。

（完）
