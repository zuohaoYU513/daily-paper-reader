---
title: "RLSF-V: Mitigating Hallucinations in MLLMs via Fuzzy Semantic Self-Feedback"
title_zh: RLSF-V：基于模糊语义自我反馈缓解多模态大语言模型幻觉
authors: "Changhao He, Shuhao Yan, Shuxian Li, Xi Peng, Peng Hu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/c8eaa18a343846262c505fb3dec068c384457f32.pdf"
tags: ["query:faithfulness"]
score: 7.0
evidence: 通过模糊语义自我反馈构造偏好数据并优化偏好，缓解多模态幻觉，与偏好优化缓解事实幻觉的需求相关
tldr: 针对偏好优化缓解幻觉时依赖人工或专有模型生成策略外偏好数据的问题，提出RLSF-V框架，利用模糊语义自我反馈从模型自身输出构造偏好数据。该方案避免了对更强评估模型的依赖，缓解了生成文本与视觉证据相矛盾的内容。在多项MLLM幻觉基准上，RLSF-V在保持可扩展性的同时显著降低幻觉率，展示出自反馈偏好学习的有效性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有DPO缓解幻觉需要人工或专有模型修正，产生策略外数据并牺牲可扩展性。
method: 提出模糊语义自我反馈框架，用模型自身输出构建符合DPO假设的偏好数据，并依据模糊语义相似度指导反馈。
result: 在MLLM幻觉评测上显著降低与视觉证据矛盾的生成内容，减少对强评估模型的依赖。
conclusion: 自反馈偏好学习可成为缓解多模态幻觉的规模化训练范式。
---

## Abstract
Multimodal large language models (MLLMs) extend large language models (LLMs) with visual perception for open-world understanding, but exacerbate LLMs' hallucinations, in which generated text contradicts visual evidence or common sense. To mitigate hallucinations, a dominant strategy is Direct Preference Optimization (DPO) using hallucination-labeled responses. Existing pipelines, however, face two key limitations: they either (i) rely on human inspection or proprietary models to correct hallucinated outputs, producing off-policy preference data that violate the assumptions of DPO, or (ii) depend on stronger models to evaluate responses, leading to an unfavorable trade-off between performance and scalability. Departing from these paradigms, we propose a reference-policy \emph{self-feedback} framework that constructs preference data for hallucination mitigation without any external supervision (\textit{e.g.}, large models or humans). Specifically, we present a novel \emph{local fuzzy semantic} evaluation paradigm that derives a hallucination-sensitive confidence signal directly from the internal logits, which is then used to automatically rank diverse generated responses to build preference pairs for fine-tuning. Trained on a 10k-scale dataset, our method achieves competitive performance on both generative and discriminative benchmarks compared to existing RLHF and RLAIF baselines.

---

## 论文详细总结（自动生成）

# RLSF-V：基于模糊语义自我反馈缓解多模态大语言模型幻觉——论文总结

## 1. 核心问题与研究动机

- **背景**：多模态大语言模型（MLLMs）通过引入视觉感知能力实现了开放世界理解，但这种能力扩展同时加剧了**幻觉问题**——模型生成的文本与视觉证据或常识相矛盾。
- **现有缓解范式**：直接偏好优化（DPO）是当前主流的幻觉缓解策略，通过使用幻觉标注响应构造偏好对进行训练。
- **现有方法的两个关键缺陷**：
  1. 依赖**人工检查**或**专有模型**来修正幻觉输出，这会生成**策略外（off-policy）偏好数据**，违反 DPO 的基本假设，导致训练偏差。
  2. 依赖**更强模型**（如 GPT-4V 等）进行评估来筛选数据，导致**性能与可扩展性之间出现不利权衡**。
- **核心问题**：能否在不依赖任何外部监督（人工或更强模型）的前提下，利用模型自身的反馈构造符合 DPO 假设的偏好数据，从而实现可扩展的幻觉缓解？

## 2. 方法论：RLSF-V 框架

### 核心思想
- 提出基于**参考策略自反馈**的框架，完全**摆脱对外部监督的依赖**（无需大型模型评估，也无需人工标注），直接从模型自身输出构造偏好数据。
- 与以往方法不同，本文的反馈信号不是来自更强大的评估模型，而是源自模型内部固有的不确定性信息。

### 关键技术细节

- **局部模糊语义评估范式（Local Fuzzy Semantic Evaluation）**：
  - 传统方法通常从整体语义层面对比两个响应，但本文提出在**局部语义层面**（local fuzzy semantics）评估生成内容与视觉证据的一致性。
  - 该评估范式能从模型**内部 logits** 中提取一个对幻觉敏感的**置信度信号**（hallucination-sensitive confidence signal），将模型自身的不确定性转化为可用于偏好排序的标量评估。
- **自动偏好对构建**：
  - 基于上述置信度信号，对模型生成的多个多样化响应进行**自动排序**；
  - 排序后形成**偏好对**，用于后续的偏好优化微调。由于数据来自参考策略自身的解码过程，属于**在策略（on-policy）数据**，从根本上克服了 DPO 面临的 off-policy 问题。
- **整体流程**：模型自生成候选响应 → 提取 logits 流计算局部模糊语义置信度 → 自动排序构建偏好对 → DPO 式偏好优化微调 → 得到幻觉率更低的 MLLM。

## 3. 实验设计

- **训练数据规模**：基于 **10k 量级（万级）** 的数据集进行训练。
- **评测基准**：涵盖**生成式（generative）** 与**判别式（discriminative）** 两类主流 MLLM 幻觉评估基准。
- **对比方法**：
  - **RLHF（人类反馈强化学习）** 系列基线；
  - **RLAIF（AI 反馈强化学习）** 系列基线。
- 结果显示：在与现有 RLHF / RLAIF 基线相当的条件下，本文方法取得了**有竞争力的性能**。

> 注：原文提供的文本中未给出具体的基准名称（如 POPE、CHAIR、MME 等）及各方法的具体数值对比表，这些细节只能以论文全文为准。

## 4. 资源与算力

- 原文摘要与元数据中**均未明确报告 GPU 型号、数量、训练时长、模型参数量级**等信息。
- 只能确认训练数据集规模约为 **10k 条**，相对轻量。
- 如需完整的算力统计（如 GPU 卡时、显存占用），需要查阅论文原文实验段落。

## 5. 实验数量与充分性

- **实验数量**：文本可确认的实验分组相对有限，明确提及的维度包括：
  - 两类评测范式（生成式 + 判别式）；
  - 两类基线框架（RLHF + RLAIF）；
  - 一个 10k 规模训练数据集。
- **充分性评估**：
  - 摘要中未明确报告**消融实验**（如去掉模糊语义模块后的效果）、**不同偏好数据规模的影响分析**，或**性能-可扩展性权衡的量化曲线**；
  - 评测基准覆盖面是否足够广（当前主要验证幻觉指标，泛化与通用能力是否退化未知）；
  - 因此，从已有文本看实验**设计方向合理且验证了核心主张**，但**报告内容尚不足够全面**，有待论文全文中更多消融与扩展实验佐证。

## 6. 主要结论与发现

- 模型自身内部信息（logits 层面的局部模糊语义置信度）可以被有效利用，用于构造高质量偏好数据，缓解多模态幻觉。
- 自反馈构造的偏好对天然符合 DPO 的 **on-policy 假设**，相较人工修正或强模型评估更加**无偏与可扩展**。
- RLSF-V 在 10k 量级数据上即可达到与 RLHF / RLAIF 基线有竞争力的表现，说明**自反馈偏好学习是一种可规模化（scalable）的幻觉缓解训练范式**。

## 7. 方法优点

- **完全摆脱外部监督**：无需人工标注、无需调用专有/更强模型，自包含训练闭环。
- **方法论创新性强**：将 logits 内部信号与模糊语义结合来定位“幻觉敏感信号”，在偏好数据构建机制上与传统 RLAIF 有本质区别。
- **数据质量高**：由于使用参考策略自生成偏好，避免了 off-policy 数据的分布偏移问题，理论上更契合 DPO 优化目标。
- **成本优势**：10k 级数据 + 无需额外推理大模型评估，训练成本与门槛显著降低，具备良好的**可扩展性**。

## 8. 不足与局限性

- **细节缺失**：从给定文本无法判断具体的正则化设计、模糊语义相似度阈值设定、logits 信号的提取位置（中间层 vs. 最终层）等实现细节。
- **实验报告不完整**：未提供完整 baseline 性能表格、消融分析、误差分析、幻觉类型细分（对象幻觉/属性幻觉/关系幻觉），全面性受限。
- **应用范围有限**：目前聚焦幻觉缓解，缺乏对模型通用能力（常识推理、指令跟随、多轮对话等）是否会因偏好优化而受损的验证。
- **潜在偏差风险**：模型自我评估可能存在**“盲区”**——当模型以高置信度输出错误内容时，置信度信号可能不会将其识别为幻觉，需要进一步探讨自反馈信号的失效边界。
- **数据集规模较小**：仅 10k 训练数据，对于多模态任务多样性支撑有限，大规模场景中的表现尚待验证。

（完）
