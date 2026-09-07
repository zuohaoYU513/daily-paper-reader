---
title: "Reasoning Models Hallucinate More: Factuality-Aware Reinforcement Learning for Large Reasoning Models"
title_zh: 推理模型更容易产生幻觉：面向大型推理模型的事实感知强化学习
authors: "Junyi Li, Hwee Tou Ng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Igq7Dyc3OL"
tags: ["query:faithfulness"]
score: 8.0
evidence: 实证显示推理RL微调显著加剧幻觉，并给出事实感知RL算法，直接回答微调训练如何影响幻觉行为。
tldr: 推理导向的强化学习微调虽显著提升推理能力，却会明显增加大模型幻觉。本文从训练动力学角度指出高方差梯度和熵引发的随机性等因素是诱因，并提出事实感知的分步策略优化算法FSPO，在每一步优化中引入显式事实校验。实验表明FSPO能够在降低幻觉的同时保持推理性能，凸显了训练目标需要显式兼顾事实性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 推理导向的强化学习微调显著提升推理能力，但本文发现它大幅增加幻觉，制约了可靠应用。
method: 提出事实感知分步策略优化FSPO，在分段RL优化中融入显式事实校验，削弱高方差梯度等致幻因素。
result: 理论分析与实验表明FSPO能降低推理模型的幻觉率，同时保持其在推理基准上的性能提升。
conclusion: RL微调应显式引入事实性约束，否则推理能力增长会伴随更严重的无依据输出风险。
---

## Abstract
Large language models (LLMs) have significantly advanced in reasoning tasks through reinforcement learning (RL) optimization, achieving impressive capabilities across various challenging benchmarks. However, our empirical analysis reveals a critical drawback: reasoning-oriented RL fine-tuning significantly increases the prevalence of hallucinations. We theoretically analyze the RL training dynamics, identifying high-variance gradient, entropy-induced randomness, and susceptibility to spurious local optima as key factors leading to hallucinations. To address this drawback, we propose Factuality-aware Step-wise Policy Optimization (FSPO), an innovative RL fine-tuning algorithm incorporating explicit factuality verification at each reasoning step. FSPO leverages automated verification against given evidence to dynamically adjust token-level advantage values, incentivizing factual correctness throughout the reasoning process. Experiments across mathematical reasoning and hallucination benchmarks using Qwen2.5 and Llama models demonstrate that FSPO effectively reduces hallucinations while enhancing reasoning accuracy, substantially improving both reliability and performance.

---

## 论文详细总结（自动生成）

由于提供的链接实际为 OpenReview 的浏览器验证页面，无法获取论文全文；以下总结严格基于所给论文元数据与摘要生成。部分细节（如具体数据集名称、公式、算力配置、完整对比方法）在元数据中未呈现，因此会明确标注为“信息缺失”。

## 1. 论文的核心问题与整体含义

- **研究背景**：大型语言模型（LLM）通过强化学习（RL）在数学推理等复杂任务上取得了显著提升，成为“大型推理模型”。
- **核心问题**：论文的经验分析揭示了推理导向 RL 微调的一个严重副作用——**它显著加剧了模型的幻觉**，即模型生成无依据或与事实不符内容的倾向。
- **整体含义**：推理能力的提升不能以牺牲事实可靠性为代价。论文强调 RL 微调目标必须显式纳入事实性约束，否则推理增强会伴随更严重的无依据输出风险，制约模型在真实场景中的可靠部署。

## 2. 提出的方法论：FSPO

- **核心思想**：提出**事实感知分步策略优化（Factuality-aware Step-wise Policy Optimization, FSPO）**，在 RL 微调过程中引入**逐步显式事实校验**，而不只是在最终答案上评估正确性。
- **技术细节**：
  - FSPO 会针对推理过程的**每一个中间步骤**，利用给定的证据进行自动化事实验证。
  - 根据验证结果，动态调整**token 级别的优势值**，从而在每一步奖励事实正确的行为、惩罚偏离证据的行为。
  - 这样可以激励模型在完整推理过程中持续保持事实一致性，而不是仅追求最终答案的格式或逻辑正确性。
- **理论分析**：论文从 RL 训练动力学的角度，指出三类导致幻觉的因素：
  - **高方差梯度**：使模型更新不稳定，可能放大随机错误；
  - **熵诱导的随机性**：鼓励探索时可能产生不可控的幻觉输出；
  - **对虚假局部最优的敏感性**：模型可能找到“能得高奖励”但与事实不符的捷径。
- **算法流程（文字说明）**：按推理步骤分段优化，在每一步引入“生成 → 证据对比 → 事实判定 → 校正优势值 → 策略更新”的循环，最终兼顾推理准确性与事实性。

## 3. 实验设计

- **任务场景**：数学推理 + 幻觉检测/抑制基准。
- **评估模型**：Qwen2.5 系列和 Llama 系列模型。
- **对比方法**：摘要中未具体列出比较对象，推测至少与常规推理 RL 微调方法（如无事实约束的策略优化）进行对比，但具体基线名称在元数据中缺失。
- **评价指标**：推理准确率和幻觉率（或事实一致性指标）。
- **结果概述**：FSPO 在降低幻觉的同时，能保持甚至提升推理性能，证明了方法的有效性。

## 4. 资源与算力

- 论文元数据与摘要中**没有提及**使用的 GPU 型号、数量、训练时长、显存或能源消耗等具体算力信息。
- 若要评估训练成本，需补充阅读全文实验部分，但当前信息无法给出任何量化说明。

## 5. 实验数量与充分性

- 根据现有信息，实验覆盖了：
  - 两个模型家族（Qwen2.5、Llama）；
  - 两种任务（数学推理与幻觉基准）；
  - 一个核心方法（FSPO）及其在提升事实性、维持推理性能方面的效果。
- **充分性判断**：
  - 优点：方法在两类任务、两类模型上均验证，且被 NeurIPS 接收，说明实验设计在当时评审中具有说服力。
  - 不足：由于摘要中未给出消融实验、多个 baselines、误差范围、统计显著性检验等细节，无法从现有材料判断实验的全面性与严格性。例如，是否单独验证每一步校验的贡献、不同校验器的影响、超参数敏感性等均未知。

## 6. 主要结论与发现

- **现象结论**：推理导向的 RL 微调虽然大幅提升推理能力，却会显著增加幻觉。
- **机制结论**：高方差梯度、熵导致的随机性、对伪局部最优的敏感性是幻觉增殖的关键训练动力学因素。
- **方法结论**：FSPO 通过显式分步事实校验，能够有效抑制幻觉，同时增强推理准确性，实现可靠性与性能的双重提升。
- **实践启示**：RL 微调目标必须显式融入事实性约束，否则模型“越来越聪明”的同时会“越来越频繁地胡编乱造”。

## 7. 优点

- **问题发现重要**：研究直接指出推理 RL 训练伴随的幻觉代价，对当前 LLM 后训练范式的安全性提出了关键警示。
- **方法与问题对齐**：不像传统 RL 只奖励最终答案，FSPO 在**推理过程中的每一步**都进行事实校验，切中幻觉形成的微观环节。
- **理论引导设计**：将梯度方差、熵、局部最优等训练动力学分析与算法设计相关联，为理解 RL 幻觉机制提供了理论视角。
- **动态 token 优势调整**：将事实校验结果细粒度地映射到 token 的重要性权重，能够更精准地控制策略更新方向。
- **实证覆盖合理**：在两类主流开源模型（Qwen2.5、Llama）上同时评测推理和幻觉，增强了结论的普适性。

## 8. 不足与局限

- **全文不可获取**：本分析所依据的元数据中缺少具体公式、算法伪代码、完整实验细节，无法全面评估技术贡献的实现细节。
- **基准信息不全**：具体数学推理基准（如 GSM8K/MATH 等）和幻觉基准的名称未列出，无法判断难度与覆盖范围。
- **对比矩阵未知**：未给出与哪些既有 RL 算法（如 GRPO、PPO、DPO 等）比较，消融实验也没有展示，对 FSPO 各组件有效性的证据不足。
- **算力/复现信息缺失**：没有模型规模、训练超参数、计算资源等，外部研究者难以估算复现成本。
- **事实校验依赖证据**：FSPO 要求“给定证据”并在每一步自动验证，但许多推理任务没有显式外部证据，或证据本身可能不完整、带噪声；这种假设在开放域问题中的可扩展性尚待检验。
- **泛化性局限**：论文验证集中在数学与事实性基准，对开放式问答、长文本生成、多步工具调用等更贴近真实场景的任务，效果未知。
- **潜在偏差风险**：若自动事实校验器本身有误差，可能会将模型推向符合“校验器偏好”而非客观真相，形成新的 reward hacking 路径。

（完）
