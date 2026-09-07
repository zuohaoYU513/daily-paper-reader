---
title: "Retrieval is Not Enough: Enhancing RAG through Test-Time Critique and Optimization"
title_zh: 仅有检索还不够：基于测试时批判与优化的增强RAG
authors: "Jiaqi Wei, Hao Zhou, Xiang Zhang, Di Zhang, Zijie Qiu, Noah Wei, Jinzhe Li, Wanli Ouyang, Siqi Sun"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=cnUq7GkS6d"
tags: ["query:faithfulness"]
score: 9.0
evidence: AlignRAG通过测试时批判优化使模型推理与检索证据对齐，减少无依据结论
tldr: 检索增强生成虽然获得相关证据，但模型推理仍可能与证据不一致或得出无依据结论。本文将RAG理解为检索增强推理，指出核心问题是推理与证据约束的错位。作者提出AlignRAG迭代框架，通过测试时批判与优化将模型推理逐步对齐到检索证据上。实验表明该方法能显著减少事实不一致和支持度不足的输出。该工作为基于外部证据的忠实生成提供了新的推理期对齐思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 标准RAG即使检索到相关文档，模型推理仍可能与证据不一致，产生无支撑结论。
method: 提出AlignRAG，采用批判驱动对齐的迭代框架，在测试时调整推理使其符合证据约束。
result: 实验显示AlignRAG显著降低事实不一致与无依据结论，提升RAG忠实性。
conclusion: 推理期批判与优化是使RAG真正服从证据的有效路径。
---

## Abstract
Retrieval-augmented generation (RAG) has become a widely adopted paradigm for enabling knowledge-grounded large language models (LLMs). However, standard RAG pipelines often fail to ensure that model reasoning remains consistent with the evidence retrieved, leading to factual inconsistencies or unsupported conclusions. In this work, we reinterpret RAG as \textit{Retrieval-Augmented Reasoning} and identify a central but underexplored problem: \textit{Reasoning Misalignment}—the divergence between an LLM's internal reasoning trajectory and the evidential constraints provided by retrieval. To address this issue, we propose \textsc{AlignRAG}, a novel iterative framework grounded in \textit{Critique-Driven Alignment (CDA)}. We further introduce \textsc{AlignRAG-auto}, an autonomous variant that dynamically terminates refinement, removing the need to pre-specify the number of critique iterations. At the heart of \textsc{AlignRAG} lies a \textit{contrastive critique synthesis} mechanism that generates retrieval-sensitive critiques while mitigating self-bias. This mechanism trains a dedicated retrieval-augmented \textit{Critic Language Model (CLM)} using labeled critiques that distinguish between evidence-aligned and misaligned reasoning. Empirical evaluations show that our approach significantly improves reasoning fidelity. Our 8B-parameter CLM improves performance over the Self-Refine baseline by \textbf{12.1\%} on out-of-domain tasks and outperforms a standard 72B-parameter CLM by \textbf{2.2\%}. Furthermore, \textsc{AlignRAG-auto} achieves this state-of-the-art performance while dynamically determining the optimal number of refinement steps, enhancing efficiency and usability. \textsc{AlignRAG} remains compatible with existing RAG architectures as a \textit{plug-and-play} module and demonstrates strong robustness under both informative and noisy retrieval scenarios. Overall, \textsc{AlignRAG} offers a principled solution for aligning model reasoning with retrieved evidence, substantially improving the factual reliability and robustness of RAG systems. Our source code is provided at \href{https://github.com/upup-wei/RAG-ReasonAlignment}{link}.

---

## 论文详细总结（自动生成）

好的，我理解您需要的是：基于以下提炼信息完成论文总结，而非对原文逐段翻译。以下内容严格依托于提供的文本（摘要 + 元数据）进行归纳，对于文中未明确披露的细节（如具体数据集、硬件算力等）会如实指出缺失。

---

## 论文总结：《仅有检索还不够：基于测试时批判与优化的增强RAG》

### 1. 论文的核心问题与整体含义

- **研究背景与动机**：检索增强生成（RAG）已成为增强大语言模型（LLM）知识能力的主流范式。然而，标准 RAG 流水线无法保证模型在获得相关证据后，其内部推理过程与检索到的证据保持一致，常出现**事实不一致**或**无依据结论**的情况。
- **核心问题**：论文将 RAG 重新阐释为 **Retrieval-Augmented Reasoning（RAG = 检索增强推理）**，指出一个关键且此前未被充分探索的问题——**推理错位**（Reasoning Misalignment），即 LLM 的内部推理轨迹与检索证据提供的**证据约束**之间存在偏差。
- **整体含义**：论文立意是**将“检索”与“推理”视为一个整体系统**，而非把证据简单拼接到 prompt 中。其核心立场是：仅仅“检索到”正确文档是不够的，必须在**推理阶段**让模型的推理过程真正服从证据。

### 2. 论文提出的方法论

- **核心思想**：提出 **AlignRAG**，这是一个基于 **Critique-Driven Alignment（CDA，批判驱动对齐）** 的迭代测试时框架。它在推理阶段通过“生成-批判-再推理”的循环，逐步约束模型推理向检索证据对齐。
- **主要模块**：
  - 训练一个专用的小规模 **检索增强的批判语言模型**（Critic Language Model, CLM），用于生成针对当前答案/推理链的批评意见。
  - 机制核心为 **对比批判合成**（Contrastive Critique Synthesis）：使用“证据对齐”和“证据错位”两类对比数据来训练 CLM。区别于一般自我反思（Self-Refine）模型，该机制能在生成批评时**缓解模型的自偏差（self-bias）**。
- **关键算法流程（文字阐述）** ：
  1. 初始生成 → 利用外部检索证据 + 当前模型的推理答案生成批判性反馈。
  2. 若批判指出推理与证据不符（如缺乏支撑、推理链跳跃），则依据该批判对原有推理进行**迭代修改与再生成**。
  3. 对齐后的回答输出。
- **扩展变体 AlignRAG-auto**：无需预先设定批判迭代轮次，引入**自动终止机制**，根据模型是否已与证据充分对齐来动态决定结束迭代，兼具效率与自动化。
- **通用性**：AlignRAG 被设计为一种与现有RAG架构兼容的 **即插即用** 模块（即不修改检索或生成模块的参数）。

### 3. 实验设计

论文摘要提供的信息有限，可分为明确提及与推测两方面：

- **核心对比任务**：以 RAG 场景下的**事实一致性/忠实度**评估为主，核心指标是减少**事实错误**与**无支撑结论**。
- **对比方法**：
  - 基线：标准 RAG 管线与 **Self-Refine** 基线（作为对比批判模型的主要参照）。
  - 不同规模的批判模型对比（8B 参数 vs 72B 参数）。
- **场景与基准设置**：
  - 包含 **跨领域（Out-of-Domain, OOD）任务**测试（用于验证泛化性）。
  - 设置了**信息丰富**（informative）与**噪音检索**（noisy retrieval）两种强烈对比的检索场景。
  - 额外构建了基于**检索证据对齐 vs 错位**的对比批判数据做训练和评测（即 Critique 自身质量的评估）。
- 关于具体数据集名称（如是否使用 Natural Questions、Biography、内部QA等）与核心 benchmark 来源，**在提供的文本中未被明确介绍**，属于披露缺口。

### 4. 资源与算力

- 在提供的论文摘要文本（与论文元数据）中，作者**并未说明任何具体算力消耗信息**，例如：
  - 训练 AlignRAG 的 CLM（8B）所用的 GPU 型号、卡数与训练时长。
  - 对抗性对比批判数据构建所需的推理开销。
  - 72B批判模型的参数量与部署资源。
- 若需要了解算力及部署条件，需暂缺。

### 5. 实验数量与充分性

- 从文本呈现的实验数据来看，主要列举了三大实验类别：
  1. **OOD 泛化能力对比验证**（AlignRAG vs Self-Refine，+12.1%）。
  2. **跨规模对比验证**（8B自研CLM vs 72B CLM，+2.2%）。
  3. **自适应消融验证**（Auto变体 vs 静态迭代轮次，展示自动终止机制SOTA）。
- 同时实验覆盖了 **信息丰富/噪音检索** 的环境（鲁棒性验证）。
- **对充分性的判断**：
  - **优势**：突出展示了检索质量对对齐的影响，并针对模型规模做了对照（较有说服力）。
  - **不足**：由于这里只提供了提炼后的“摘要级”数据，关于**消融实验的细致程度**、**是否在不同检索器/生成器下做交叉验证**、**是否包含人类评测**等细节完全无法判断。特别地，需关注仅凭单项评测集得出的指标是否具有统计置信度。

### 6. 论文的主要结论与发现

- 提出了将 RAG 的核心问题重构为**“推理与证据的空隙”**，即从检索系统问题转向推理与证据约束的一致性对齐问题。
- 验证了通过测试时批判与对比合成的批判模型进行**外部约束**，能有效引导 LLM 遵守证据事实。
- 量化结论：
  1. **自研 8B CLM** 在 OOD 场景比 Self-Refine 基线提升了 **12.1%**。
  2. **8B CLM** 的性能表现能够超越 72B 规模的通用/标准CLM基线（提升 **2.2%**），以轻量模型实现较强忠实性控制。
  3. **AlignRAG-auto** 能动态决定迭代次数，在不损失效果的前提下提高了 RAG 推理效率。
  4. 机制在**证据噪声较高**时仍具鲁棒性，保留了跨架构的即插即用友好性。

### 7. 优点

- **视角新颖且切中痛点**：将 RAG 问题从“检索有效性”扩展至“推理—证据对齐”，抓住 RAG 瓶颈的关键（找到了不完整证据与无依据推理之间存在的不匹配）。
- **方法论有效性**：对比批判合成（Contrastive Critique Synthesis）设计巧妙，通过区分“对齐”与“错位”的样例训练，从根源上规避了仅靠 LLM“自我反思”产生自偏差的风险。
- **高效与普适性**：同时做到了小型8B批判模型超越大模型72B的效果，且模块设计极具工程友好性（即插即用），无需修改 RAG 系统与推理模型权重，便于直接部署在现有系统上。
- **自适应条件终止**：引入 Auto 动态停止机制，将“迭代次数”从超参变为自适应判断，兼顾了性能与计算开销。

### 8. 不足与局限

- **实验覆盖的信息披露有限**：论文摘录中没有明确给出所涉及的具体**基准数据集名称与评测协议**（如LFQA、StrategyQA等）、**训练数据规模**及**具体案例定性分析**，这些作为评估忠实性RAG效果的重要维度未被展示。
- **搜索策略的耦合风险**：实验在“具备信息”和“带噪”环境下都做了测试，但并未展示对**检索器本身失败（证据完全缺失）**时的应对——无法验证当上下文里根本没有答案时，该批判机制是否会造成误导性强逼推理。
- **未报告计算复杂度衡量**：虽然 Auto 变体意在解决效率，但关于 8B批判模型的详细训练耗时、几次迭代的平均Round数未在摘要中呈现。在真实任务中，若需要多次循环（CLM生成多次），可能引入高昂推断开销，文中未进行深度延迟与成本权衡分析。
- **对齐范围局限性**：机制约束的更多是“证据-推理”匹配，而**面向事实的选择性偏好（selection-bias）**或逻辑多样性等未考虑。仅用对比批判数据训练，可能在一定边界条件（如长上下文推理）会失效。
- **相关数据缺口**：资源限制下，全文更多展示的是在泛化任务（OOD）上的显著优势，而如果未来需要复现，批判数据的构造要求较高，可及性与数据构建难度将构成一定的落地门槛。

（完）
