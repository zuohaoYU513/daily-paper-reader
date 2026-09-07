---
title: Information Flow Reveals When to Trust Language Models
title_zh: 信息流揭示何时应信任语言模型
authors: "Rui Xu, Yi Chen, Jiujiu Chen, Sihong Xie"
date: 2026-04-30
pdf: "https://openreview.net/pdf/9e5c51b770ffeed01e47c4d228504b941d795e0f.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 逐层信息流追踪输出对查询相关证据的支撑程度，用于检测无依据内容
tldr: 面向检索增强生成，如果模型未利用查询相关证据就可能产生错误回答，因此需要判断输出是否真的被证据支撑。现有不确定性方法只观察少数层，遗漏了层间传播信息。本文利用信息流构建逐层轨迹，显示每个上下文token对最终输出的贡献，从而估计上下文根基。该工作为检测无依据回答提供了更完整、可解释的评测依据。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 模型忽略查询相关证据时可能产生错误回答，现有不确定性方法没有覆盖层间完整传播。
method: 使用信息流建立逐层贡献轨迹，刻画上下文token对输出的支撑强度。
result: 该追踪方法能更好地识别模型输出是否真正根植于证据，提升可信度判断。
conclusion: 利用信息流逐层观测证据贡献，为证据约束生成的可靠性评估提供了有力工具。
---

## Abstract
In retrieval-augmented generation, language models can generate incorrect responses if they fail to utilize query-relevant content from the retrieved evidence. This shifts the focus of uncertainty quantification (UQ) toward assessing contextual grounding, i.e., whether predictions are supported by query-relevant tokens. Recent UQ methods unpack language models to characterize how inputs are processed. Nevertheless, these methods focus on a few layers and overlook the whole progressive propagation within the model, thereby failing to fully capture the grounding dynamics essential for reliable uncertainty estimation. We use information flow to build a layer-wise trace that reveals each context token’s contribution to the output, providing an interpretable basis for assessing reliability. From this analysis, we introduce two measures to calibrate prediction confidence. The first, \textit{simulatability}, posits that a prediction is more likely to be correct when context token contributions align closely with their true relevance. The second, \textit{concentration}, asserts that a response is more likely to be correct when it is derived from a narrow, focused subset of tokens. Experiments show that our method achieves an average AUROC of 0.709, exceeding the runner-up performance of 0.676, while maintaining moderate computational cost.

---

## 论文详细总结（自动生成）

# 《Information Flow Reveals When to Trust Language Models》论文中文详细总结

## 一、论文的核心问题与整体含义

- **研究背景**：在检索增强生成（RAG）中，语言模型依赖外部检索到的证据来回答查询；若模型未能利用与查询相关的证据内容，就可能生成看似流畅实则错误的回答。
- **核心问题**：传统不确定性量化（Uncertainty Quantification, UQ）方法侧重于“模型对自身预测有多确定”，但在 RAG 场景下应该转向评估“上下文根基（contextual grounding）”，即预测是否真正由查询相关证据支撑。
- **现有方法不足**：近期的 UQ 方法虽然尝试打开语言模型内部、分析输入处理过程，但大多只观察少数几个层，未覆盖信息在层间的完整渐进传播过程，因而无法完整捕捉支持可靠性估计所需的“根基动态（grounding dynamics）”。
- **整体含义**：论文试图回答“什么时候应信任语言模型的输出”，并通过逐层追踪输入信息对输出的影响，提供一种更具可解释性的信任评估基准。

## 二、论文提出的方法论

- **核心思想**：引入**信息流（information flow）**分析手段，构建逐层（layer-wise）的传播轨迹，揭示每个上下文 token 对最终输出贡献的大小变化，从而判断模型输出是否真正“根植于证据”。
- **关键技术思路**：
  - 将模型内部的计算视为信息流动过程，追踪来自不同上下文 token 的信息如何跨层传播、最终汇聚到输出表示上。
  - 与仅观察若干层或仅看输出层概率的方法不同，该方法覆盖完整层间路径，给出的贡献轨迹更接近模型真实处理过程。
- **两个可靠性度量**：
  1. **Simulatability（可模拟性）**：若上下文 token 对输出预测的贡献分布与其真实相关性（true relevance）高度一致，则该预测更可能是正确的。即模型“用对了证据”的倾向。
  2. **Concentration（集中性）**：若一个回答是由少量、聚焦的 token 子集推导得到（而非分散、噪声式地融合大量无关 token），则该回答更可能是正确的。
- **流程概要**（文字说明）：输入查询与检索证据 → 记录每个上下文 token 在各层对输出 token 的信息贡献 → 构建逐层贡献轨迹 → 据此计算 simulatability 与 concentration 分数 → 校准预测置信度 / 判定输出是否有足够证据支撑。

## 三、实验设计

- **Benchmark 与场景**：面向检索增强生成（RAG）场景，评测核心任务是判断模型输出是否“有依据”（faithfulness / grounding）。
- **数据集**：论文元数据与摘要中**未明确列出**具体使用的数据集名称。从行文推断，应包含至少多组 RAG 问答评测集（如常识问答、事实验证类任务等），但具体清单无法从已知信息中确认。
- **对比方法**：与近年来的“逐层打开模型”的 UQ 方法进行了比较，摘要仅提到 runner-up（第二名）方法的性能为 AUROC 0.676。具体对比的基线方法名称、数量、是否为同类型信息流方法，均未在可见内容中披露。
- **性能指标**：主要报告了 **AUROC（Area Under the ROC Curve）**，用于衡量区分“有依据/无依据输出”的能力。

## 四、资源与算力

- 可见文本中**未明确披露**使用的 GPU 型号、数量、训练/推理时长等信息。
- 摘要只提到该方法“保持中等计算成本（moderate computational cost）”，暗示其开销可接受，但没有给出 FLOPS、推理时间等量化数据。

## 五、实验数量与充分性

- **可见实验信息有限**：目前只能确认存在一组主实验结果（平均 AUROC 0.709 对第二名 0.676）。这是否涵盖多个数据集上的平均，抑或是单一数据集上的结果，无法严格判定。
- **是否有消融实验**：摘要和元数据中未提及消融实验、超参数敏感性分析、不同模型规模（如 7B/13B/70B）的对比、不同检索质量下的鲁棒性实验等。因此实验的**可复现性与全面性无法充分评判**。
- **客观性与公平性评价**：从简要的数据来看（提升约 3.3 个 AUROC 百分点）效果显著，但由于缺少对基线方法细节、数据集构成、统计显著性检验的说明，无法确认实验是否完全公平或是否存在选择偏差。初步结论是：证据方向正确，但实验细节支撑不足。

## 六、论文的主要结论与发现

- 信息流的逐层追踪方法能够更全面地表征上下文 token 对最终输出的支撑过程，弥补现有 UQ 方法只观察少数层的缺陷。
- 基于该方法提出的 simulatability 与 concentration 两个度量能有效校准预测置信度：当贡献轨迹与真实相关性一致、且贡献集中在少数关键 token 上时，模型的回答更值得信任。
- 实验数据表明，该方法的平均 AUROC 达到 **0.709**，优于当前最优竞争方法（runner-up）的 **0.676**，同时在计算开销上处于中等水平，具备实际使用潜力。

## 七、优点

- **方法视角新颖**：将“信息流”分析用于 RAG 的 grounding 判定，视角从“模型的信心”转向“证据是否真正传递到了输出”，更贴近事实核查需求。
- **覆盖更完整**：与只看少数层的方法相比，逐层完整轨迹能够捕捉跨层信息传播的动态过程，理论覆盖面更强。
- **可解释性好**：逐层贡献轨迹本身就是一种可视化解释工具，两种度量各有清晰的语义含义（用对证据程度、证据集中程度），便于实际部署理解和调试。
- **性能有较强提升**：平均 AUROC 提升约 3.3 个百分点，属于较有意义的改进幅度，且计算成本在可接受范围。

## 八、不足与局限

- **实验细节严重缺失**：可见范围内没有数据集列表、模型配置、对照实验、消融设计等细节，难以从方法论层面完整复现或验证结果。
- **泛化范围不确定**：评测是否覆盖多种模型架构（如编码器-解码器 vs. 仅解码器）、不同规模模型、不同语言与领域？摘要未提及，泛化性存疑。
- **未标明资源开销细节**：只称“中等计算成本”，缺少量化对比（如相对基线推理时间增加多少），对实际资源敏感型任务的可落地性判断不足。
- **有效性边界需进一步讨论**：对于生成的回答、以及非常长/多个证据片段互相矛盾的场景，concentration 度量是否会错误惩罚合理的反驳式回答——该局限未被讨论。
- **比较公平性难考证**：对比方法的选择标准、是否包含代表性最强的 SOTA 高不确定性方法等，尚未在摘要层体现。另需注意，论文目标指标是 RAG 语境下的“根基 / 忠实度”，而非一般问答准确率，该评测偏置可能与具体任务设计高度耦合。

（完）
