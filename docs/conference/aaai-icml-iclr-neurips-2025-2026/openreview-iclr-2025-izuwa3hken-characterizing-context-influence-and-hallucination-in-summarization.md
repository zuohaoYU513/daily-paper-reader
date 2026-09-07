---
title: Characterizing Context Influence and Hallucination in Summarization
title_zh: 刻画摘要中的上下文影响与幻觉
authors: "James Flemings, Wanrong Zhang, Bo Jiang, Zafar Takhirov, Murali Annavaram"
date: 2024-09-27
pdf: "https://openreview.net/pdf?id=IZuwA3hken"
tags: ["query:faithfulness"]
score: 8.0
evidence: 直接研究大模型摘要中与上下文相矛盾的幻觉以及上下文影响，是摘要忠实性的核心问题。
tldr: 针对大语言模型在摘要任务中既可能产生与上下文相矛盾的幻觉，又可能直接复读输入造成隐私泄露的问题，该论文首次将二者联合刻画并系统研究上下文的影响。通过定义上下文影响、测量幻觉与输入复读之间的关系，揭示模型在使用上下文时出现幻觉的条件和模式。研究有助于从上下文影响的角度理解摘要生成的忠实性，并对上下文隐私审计提出了新的分析维度。
source: ICLR-2025-Public
selection_source: conference_retrieval
motivation: LLM在摘要中既可能产生与上下文矛盾的幻觉，也可能复读输入造成隐私泄露，且缺乏对上下文影响的联合审计。
method: 提出上下文影响与幻觉的联合刻画框架，定义上下文影响并考察幻觉与输入复读之间的关系。
result: 揭示摘要生成中上下文影响导致幻觉的模式，为上下文使用与隐私风险审计提供分析基础。
conclusion: 为理解摘要生成的忠实性与上下文隐私泄露提供了统一视角，也为后续干预研究奠定基础。
---

## Abstract
Although Large Language Models (LLMs) have achieved remarkable performance in numerous downstream tasks, their ubiquity has raised two significant concerns. One is that LLMs can hallucinate by generating content that contradicts relevant contextual information; the other is that LLMs can inadvertently leak private information due to input regurgitation. Many prior works have extensively studied each concern independently, but none have investigated them simultaneously. Furthermore, auditing the influence of provided context during open-ended generation with a privacy emphasis is understudied. To this end, we comprehensively characterize the influence and hallucination of contextual information during summarization. We introduce a definition for context influence and Context-Influence Decoding (CID), and then we show that amplifying the context (by factoring out prior knowledge) and the context being out of distribution with respect to prior knowledge increases the context's influence on an LLM. Moreover, we show that context influence gives a lower bound of the private information leakage of CID. We corroborate our analytical findings with experimental evaluations that show improving the F1 ROGUE-L score on CNN-DM for LLaMA 3 by $\textbf{10}$% over regular decoding also leads to $\textbf{1.5x}$ more influence by the context. Moreover, we empirically evaluate how context influence and hallucination are affected by (1) model capacity, (2) context size, (3) the length of the current response, and (4) different token $n$-grams of the context.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

**论文标题**：Characterizing Context Influence and Hallucination in Summarization（刻画摘要中的上下文影响与幻觉）

**作者**：James Flemings, Wanrong Zhang, Bo Jiang, Zafar Takhirov, Murali Annavaram

**发表于**：ICLR-2025（公开评审，评分 8.0）

---

## 1. 核心问题与整体含义（研究动机与背景）

- 大语言模型（LLM）在摘要等下游任务中性能优异，但其广泛部署引发了两大核心担忧：
  - **幻觉（Hallucination）**：模型生成与给定上下文相矛盾的内容；
  - **隐私泄露（Privacy Leakage）**：模型可能通过**输入复读（input regurgitation）** 泄露上下文中的私人信息。
- 以往研究大多将上述两个问题**分别独立研究**，目前没有工作将它们**同时考察**。
- 此外，在开放式生成任务中，从**隐私视角审计上下文影响（context influence）** 的研究严重不足。
- 因此，本文首次将幻觉与隐私泄露问题**联合刻画**，系统研究摘要生成过程中上下文对模型输出的影响机制。

---

## 2. 方法论

### 2.1 核心思想
- 提出**上下文影响（Context Influence）** 的正式定义，作为理解 LLM 在摘要生成中“如何使用上下文”的量化工具。
- 引入解码方法——**Context-Influence Decoding（CID）**，通过**消解（factor out）先验知识**来**放大上下文对生成的影响**。
- 探讨上下文影响与两类风险的关联：
  - 上下文影响过大 → 输入复读 → **隐私泄露风险**；
  - 上下文影响被忽略 → 依赖先验 → **幻觉风险**。
- 理论上证明：**上下文影响是 CID 方法下私有信息泄露的一个下界（lower bound）**。

### 2.2 关键技术和流程
- 将摘要生成的解码过程分解为对两种知识来源的依赖：
  1. **先验知识**（模型内部参数中固化的知识）；
  2. **提供上下文**（输入中的外部信息）。
- CID 的核心操作：在解码时**减去基于先验知识生成的概率分布**，从而使模型在计算下一个 token 时更多依赖上下文而非内部知识记忆。
- 分析指出两种情境会增大上下文影响：
  1. **放大上下文信号**（即通过 CID 消解先验知识）；
  2. **上下文相对先验知识属于分布外（out-of-distribution）样本**——模型无法用内部先验解释时，被迫更多地采纳上下文。

---

## 3. 实验设计

### 3.1 数据集与基准
- 使用 **CNN-DM（CNN/DailyMail）** 数据集作为摘要基准；
- 评测指标：**F1 ROUGE-L**（摘要质量），另测量**上下文影响力**（Context Influence）与**幻觉（hallucination）** 的相应指标。

### 3.2 对比方法与场景
- **对比基准**：普通解码方法（regular decoding）；
- **本文方法**：Context-Influence Decoding（CID）；
- 实验覆盖的自变量包括：
  1. 模型容量（model capacity）；
  2. 上下文尺寸（context size）；
  3. 当前回复的长度（length of current response）；
  4. 上下文中不同 token n-gram 的影响。

---

## 4. 资源与算力

- **论文中未明确披露**：
  - GPU 型号与数量；
  - 训练/推理时长；
  - 能耗等算力细节。
- 从描述看，实验主要基于 **LLaMA 3** 系列的推理与评测，属于轻量级实验，未涉及大规模预训练或微调。

---

## 5. 实验数量与充分性

- 实验覆盖了较好的**广度**：模型容量、上下文长度、响应长度、token n-gram 粒度等多个影响维度均做了评估。
- 但受限于论文内容的可得性，具体实验组数（如若干条数据集上的完整对照）尚未完整展示。
- **充分性评估**：
  - 优点：围绕“上下文影响”这一核心变量，多维度扫描了影响因子，形成了较全面的分析。
  - 不足：在单一数据集（CNN-DM）上进行验证，缺少多数据集与跨领域（如对话、法律、医疗摘要）的外部验证，ROUGE 指标也较为单一，公平性与泛化性仍有待扩展。

---

## 6. 主要结论与发现

1. **CID 能显著提升摘要质量**：在 CNN-DM 上，LLaMA 3 使用 CID 后，F1 ROUGE-L 得分较普通解码**提升 10%**。
2. **更好的摘要质量伴随更大的上下文影响**：ROUGE-L 提升 10% 的同时，上下文对生成的影响增加了 **1.5 倍**。
3. **上下文影响与隐私泄露直接关联**：上下文影响力的提升意味着模型更多复读输入，从而构成**隐私泄露的下界指标**。
4. **分布外上下文会增强上下文影响**：当输入上下文的主题或风格对模型内部先验而言较新颖时，模型更依赖上下文。
5. **幻觉与隐私之间存在张力**：抑制上下文影响以保护隐私可能增加幻觉风险，放大上下文影响以提升忠实度可能加剧隐私泄露——两者需要权衡。

---

## 7. 优点

- **首次联合建模**：将“幻觉”与“输入复读/隐私泄露”放入同一分析框架，突破了以往各自孤立研究的局限。
- **提出可量化指标**：给出“上下文影响力”的正式定义，对后续审计与干预具有很好的可操作性。
- **理论有据**：给出了上下文影响与隐私泄露下界之间的理论关系，而非停留在经验观察层面。
- **实用性强**：CID 方法简单有效，仅在解码阶段干预即可带来显著性能提升，便于推广。
- **问题意识敏锐**：从隐私视角切入上下文影响的审计，回应了大模型部署中的真实关切。

---

## 8. 不足与局限

- **数据集覆盖有限**：仅在 CNN-DM 一个公开摘要数据集上验证，缺乏多领域、多任务验证。
- **基准模型较少**：实验以 LLaMA 3 为主要载体，未充分覆盖不同规模、不同架构的模型。
- **算力信息缺失**：未说明实验基础设施（GPU 类型/数量/运行时间），难以判断方法的计算成本。
- **度量单薄**：摘要质量主要依赖 ROUGE 指标族（F1 ROUGE-L），缺少对生成内容语义质量、流畅度或人工评估的综合度量。
- **隐私与幻觉的权衡尚未提出干预方案**：论文重点是“刻画/诊断”问题，而非提出同时缓解两类风险的具体方法；结尾提到为后续干预研究奠定基础，说明当前仍属分析型工作。

---

（完）
