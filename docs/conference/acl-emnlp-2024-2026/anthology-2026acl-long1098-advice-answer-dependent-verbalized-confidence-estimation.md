---
title: "ADVICE: Answer-Dependent Verbalized Confidence Estimation"
title_zh: ADVICE：基于答案的言语化置信度估计
authors: "KiJung Seo, Sehun Lim, Taeuk Kim"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1098.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 分析口头置信度估计并指出答案无关导致过度自信，提出基于自身答案的置信度微调显著改善校准
tldr: 针对大语言模型口头表达置信度时普遍过度自信的问题，论文发现关键原因之一是置信度估计没有基于模型自身的答案，即存在答案无关性。为此提出ADVICE，一种促使置信度锚定于自有答案的微调框架。实验表明该方法显著提升置信度校准能力，同时保持强生成性能和泛化性，为构建更可靠的模型自我评估提供了可复用的训练方案。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 817, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 202, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1654, \"height\": 669, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1643, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 788, \"height\": 596, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1656, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 799, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 802, \"height\": 195, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 564, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1314, \"height\": 560, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1315, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1263, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1160, \"height\": 887, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1098/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1161, \"height\": 892, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1633, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1648, \"height\": 769, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 636, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 809, \"height\": 588, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1637, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 814, \"height\": 668, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1366, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1381, \"height\": 1629, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1098/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1302, \"height\": 1110, \"label\": \"Table\"}]"
motivation: 大语言模型言语化置信度往往系统性过度自信，且其成因尚未被充分理解。
method: 提出ADVICE微调框架，训练置信度估计显式依赖模型自身生成的答案，使置信度与答案内容关联。
result: 大量实验表明该方法显著改善置信度校准，并保持较强的生成能力与泛化表现。
conclusion: 答案依赖的置信度估计是缓解大模型过度自信、提升可信度的有效路径。
---

## Abstract
Recent progress in large language models (LLMs) has enabled them to communicate their confidence in natural language, improving transparency and reliability.However, this expressiveness is often accompanied by systematic overconfidence, whose underlying causes remain poorly understood. In this work, we analyze the dynamics of verbalized confidence estimation and identify answer-independence-the failure to condition confidence on the model’s own answer-as a primary driver of this behavior.To address this, we introduce ADVICE (Answer-Dependent VerbalIzed Confidence Estimation), a fine-tuning framework that promotes answer-grounded confidence estimation.Extensive experiments show that ADVICE substantially improves confidence calibration, while exhibiting strong generalization to unseen settings without degrading task performance.We further demonstrate that these gains stem from enhanced answer dependence, shedding light on the origins of overconfidence and enabling trustworthy confidence verbalization.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- 近年来，大语言模型（LLM）开始能用自然语言表达自身置信度（即“言语化置信度”），目的是提升模型的透明度与可靠性。
- 然而，这类置信度表达普遍存在系统性**过度自信**（overconfidence）问题：模型往往给出较高置信度，与其回答的真实正确率不匹配。
- 已有缓解方法（提示工程、采样法、微调）大多聚焦于“如何缓解过度自信”，而对“**为什么会产生过度自信**”的深层机制探索不足。
- 本文通过分析置信度估计算法的内部过程，提出一个关键诊断：**言语化置信度几乎不依赖模型自身的答案**（答案独立性，answer-independence），即模型在回答问题时并没有将其答案内容真正纳入置信度评估的因果链条中。
- 针对该原因，作者提出 **ADVICE（Answer-Dependent VerbalIzed Confidence Estimation）**，一种基于答案的言语化置信度估计微调框架，旨在让置信度真正“锚定”在模型自己生成的答案上。

## 2. 提出的方法论

- **核心思想**：让模型在给出置信度时，必须显式参考其自生成的答案信息，使置信度成为“给定问题与答案”下的条件估计，而非几乎仅由问题本身诱发。
- **训练数据构建**：
  - 从 TriviaQA 训练集随机抽取约 4000 个问题；
  - 仅保留模型在贪心解码下能答对的样本；
  - 对每个问题 q，构造“正确答案 acorrect”和“错误答案 awrong”的对；
  - awrong 由模型自随机采样得到，常包含“硬负样例”（语义合理但事实有误的答案）；
  - 使用 ScoreLetter（如 A–E）和 ScoreNumber（0–9）两种言语化格式训练，以提升格式泛化性。
- **训练目标（总损失）**：每个三元组 (q, acorrect, awrong) 定义四个损失项：
  - **L_LM**：正确答案的负对数似然，用于保持模型原有问答能力；
  - **L_JSD**：鼓励正确与错误答案下的置信度分布（Pcorrect 与 Pwrong）显著分离，通过最大化 Jensen–Shannon 散度实现：max(0, δJSD − D_JSD(Pcorrect || Pwrong))；
  - **L_Margin**：确保正确答案期望置信度 μcorrect 显著高于错误答案的 μwrong：max(0, δMargin − (μcorrect − μwrong))，防止模型学反方向；
  - **L_Sum**：约束 μcorrect + μwrong ≈ 1，以符合置信度应近似“答案正确概率”的定义：|1 − (μcorrect + μwrong)|。
  - 总损失权重 λ 均设为 1（与 ConfTuner 结合时 λ 做调整）。
- **训练方式**：使用 LoRA 低秩微调，仅训练注意力的 Q/K/V/O 投影，r=16，α=32，AdamW 优化器，学习率按模型不同设为 1e-5 或 3e-5。

## 3. 实验设计

- **模型**：三个开源 LLM：LLaMA-3.1-8B-Instruct、Mistral-7B-Instruct-V0.3、Gemma-2-9B-IT。
- **数据集与场景**：
  - 训练集：TriviaQA（open-domain QA）；
  - 评测集：TriviaQA（域内）、MMLU 与 LogiQA（域外，用于测试跨域泛化）；
  - 额外补充：SciQ（附录中进行分析，显示高准确率下校准评估的困难）。
- **置信度表达类型**：ScoreLetter、ScoreNumber、ScoreText、ScoreFloat、ScorePercent 五种；ADVICE 只用前两种做训练，后三种用于检验格式泛化。
- **对比方法**：
  - Default：直接提示；
  - Prompting：提示词要求考虑生成答案再给置信度；
  - Self-Consistency：多采样（M=5）并聚合；
  - ConfTuner：已有基于 Brier 分数微调的竞争者；
  - ADVICE 与 ConfTuner 的组合（w/ ConfTuner），用于验证正交增益。
- **评估指标**：ECE、|NCE|、Brier Score、AUROC（校准与判别能力），并报告任务准确率以确认未损害性能。

## 4. 资源与算力

- 论文只在附录 C 简要说明：所有 LoRA 训练均在 **1 块 NVIDIA H200 NVL PCIe GPU** 上完成。
- 训练轮数：GEMMA-2-9B-IT、LLaMA-3.1-8B-Instruct、Mistral-7B-Instruct-V0.3 均训练 4 epoch（ADVICE 主体）。
- 训练数据量随模型生成情况变化，约 1k–2k 条三元组样本。
- 论文未提及整体 GPU 总时数、单次训练 wall-time、推理成本对比等具体数值，也需读者自行成本评估。

## 5. 实验数量与充分性

- 实验覆盖较广，主要包括：
  1. 主实验：3 模型 × 3 数据集 × 4 指标 × 多种比对方法，结果取 3 次随机种子均值；
  2. 消融实验（Training Objectives）：评估 L_LM、L_JSD、L_Margin、L_Sum 的组合影响；
  3. 未见言语化格式泛化实验：ScoreText/ScorePercent/ScoreFloat；
  4. 答案掩蔽实验：将答案替换成填充 token，检验模型置信度是否随之变化；
  5. Attention Rollout 与 Integrated Gradients 的可解释性分析（包括训练前/后对比，中间步骤追踪）；
  6. 与 ConfTuner 正交组合实验；
  7. SciQ 高准确率场景下的补充评估。
- 总体充分性判断：
  - **优点**：从定量指标（ECE、Brier、AUROC等）到定性归因可视化，从域内到域外、从训练格式到未见格式，形成了较为立体的证据链；所有主要结果都报告了标准差；且使用多种开源模型增强泛化性。
  - **可能的局限**：仅使用短问答/多选题数据集，未涉及长文本、复杂推理任务；没有商业/超大规模模型；关于算力的时间和能耗报告不足；消融实验只在部分模型和数据集上展示，未全量覆盖所有模型；SciQ 上的结果显示了校准评估受准确率影响的复杂性，也间接提醒实验结论可能在极端高准确率场景下不适用。

## 6. 主要结论与发现

- **答案独立是过度自信的重要成因**：通过 JSD 分布检验、Attention Rollout（C→A 分数显著弱）和 Integrated Gradients（答案 token 归因低），说明模型在报告置信度时几乎未考虑自身答案。
- **ADVICE 显著改善校准**：相比 Default、Prompting、Self-Consistency，ADVICE 大幅降低 ECE、|NCE|、Brier，并显著提高 AUROC；在域外数据集 MMLU 和 LogiQA 上多数指标优于 ConfTuner。
- **正交效应**：ADVICE 与 ConfTuner 组合后常有额外增益，说明两种方法互补。
- **高效性**：ADVICE 相较 Self-Consistency 和 ConfTuner，生成 token 更少，校准更好，达到性能与效率的最佳平衡。
- **任务性能无损**：微调前后 QA 准确率几乎不变，说明校准提升来自真实置信度建模而非副作用。
- **因果验证**：答案掩蔽后 ADVICE 模型置信度显著下降，训练中注意力和归因分数持续向答案 token 迁移——证明改进源于增强的答案依赖。

## 7. 优点

- **诊断先行、机制清晰**：先从多角度揭示“答案独立性”这一过度自信的深层原因，再据此设计方法，具有较强的科学解释力。
- **方法简洁、可解释**：损失函数每个分量都对应一个明确目标；以对比正确/错误答案的置信分布为核心，与置信度的数学定义高度一致。
- **实验证据链闭环**：从数据统计（JSD）、内部注意力（Attention Rollout）、梯度归因（IG），到行为实验（答案掩蔽）多个层面反复验证，结论可信。
- **泛化性好**：只使用 TriviaQA 训练，却能在 MMLU、LogiQA 等域外任务和多种未见过置信格式上取得稳定改进。
- **效率优势**：单次生成即可给出校准置信度，避免采样式方法的大量 token 开销。
- **与现有方法可组合**：可与 ConfTuner 等已有方法叠加，具有实用价值。

## 8. 不足与局限

- **数据构建成本**：需要模型自生成多组答案以形成正确/错误对比对，额外增加了数据处理流程和训练复杂度。
- **任务覆盖有限**：仅验证短问答、多项选择等场景；未涉及长文本推理、对话、信息抽取或领域任务。
- **高准确率场景的校准评估挑战**：论文指出 SciQ 上模型准确率超 90% 时，校准指标与任务正确率高度耦合，甚至 Default 已很好，暗示在“强模型+简单任务”上，过度自信问题可能被过低估计或评估指标失真。
- **算力与能耗信息不足**：未披露训练时长与 GPU 总时数，复现成本难以精确判断。
- **消融范围受限**：消融研究只报出 Gemma 2-9B 与 Llama 3.1-8B，对 Mistral 的消融缺省；某些单项损失（如 L_Sum）单独使用时效果不稳定，仍需要依赖组合。
- **可扩展性未知**：在更大规模 LLM（如数百 B 参数）上的效果尚未验证，低秩微调是否适用于所有模型仍需研究。

（完）
