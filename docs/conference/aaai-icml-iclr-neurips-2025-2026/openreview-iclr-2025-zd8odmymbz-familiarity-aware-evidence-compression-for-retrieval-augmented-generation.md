---
title: Familiarity-Aware Evidence Compression for Retrieval-Augmented Generation
title_zh: 面向检索增强生成的熟悉度感知证据压缩
authors: "Dongwon Jung, Qin Liu, Tenghao Huang, Ben Zhou, Muhao Chen"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=Zd8ODMYMBZ"
tags: ["query:hallu-rag"]
score: 7.0
evidence: 面向RAG的证据压缩方法，使检索证据对下游模型更熟悉，减少基于证据生成中的干扰。
tldr: 针对RAG中证据不一致或无关信息干扰模型，且压缩后证据对下游模型不够熟悉的问题，提出无需训练的熟悉度感知证据压缩方法FaviComp。它使压缩后的证据与目标模型更契合，提升模型利用证据的效率并降低生成不可靠风险。实验表明FaviComp能帮助模型更好地使用多证据信息，为改进基于证据的生成提供了一种轻量且通用的手段。
source: ICLR-2025-Public
selection_source: conference_retrieval
motivation: 检索增强生成易受无关或不一致证据干扰，现有压缩得到的证据对下游目标模型不够熟悉，影响利用效果。
method: 提出无需训练的FaviComp技术，通过熟悉度感知的方式压缩检索证据，使其与目标模型的熟悉度匹配以利于后续生成。
result: 在需要多证据的检索增强生成场景中，FaviComp可提升压缩证据的可利用性，降低不一致证据引起的性能下降。
conclusion: 为证据约束的检索增强生成提供了一种轻量、免训练的证据压缩新方案，可提升基于证据生成的可靠性。
---

## Abstract
Retrieval-augmented generation (RAG) improves large language models (LMs) by incorporating non-parametric knowledge through evidence retrieved from external sources. However, it often struggles to cope with inconsistent and irrelevant information that can distract the LM from its tasks, especially when multiple evidence pieces are required. While compressing the retrieved evidence with a compression model aims to address this issue, the compressed evidence may still be unfamiliar to the target model used for downstream tasks, potentially failing to utilize the evidence effectively. We propose FaviComp (Familiarity-aware Evidence Compression), a novel training-free evidence compression technique that makes retrieved evidence more familiar to the target model, while seamlessly integrating parametric knowledge from the model. Specifically, FaviComp proactively composes the compressed evidence in a way to lower the perplexity of the target model by combining decoding probabilities from both the compression model and the target model to generate context that is more familiar to the target model. This approach balances the integration of parametric and non-parametric knowledge, which is especially helpful in complex tasks where the retrieved evidence set may not contain all the necessary information. Experimental results show that FaviComp consistently outperforms most recent evidence compression baselines across multiple open-domain QA datasets, improving accuracy by up to 23.91% while achieving high compression rates. Additionally, we demonstrate the effective integration of both parametric and non-parametric knowledge during evidence compression.

---

## 论文详细总结（自动生成）

## 论文总结：Familiarity-Aware Evidence Compression for Retrieval-Augmented Generation

### 1. 核心问题与整体含义

- **研究背景**：检索增强生成（RAG）通过引入外部非参数知识来增强大语言模型，但当检索到的证据包含不一致、无关或冗余信息时，模型容易被干扰，尤其在需要同时利用多条证据的复杂任务中表现不佳。
- **已有方法及其不足**：现有工作尝试使用“证据压缩模型”对检索结果进行压缩，以过滤噪声。然而，经过压缩后的证据往往在语言风格、分布特征上与用于下游任务的目标模型“不够熟悉”，导致目标模型难以充分理解或利用这些证据，压缩反而可能造成知识利用效率下降。
- **核心问题**：如何让压缩后的证据不仅去除噪声，还能与下游目标模型的内部语言建模特性相匹配，从而提升证据的可利用性和生成结果的可靠性。
- **总体含义**：论文提出了一个轻量、免训练的“熟悉度感知”压缩方案，尝试在压缩过程中主动照顾目标模型的先验知识，使压缩证据既能保留检索知识，又能与模型的参数化知识顺畅融合。

### 2. 方法论：核心思想、关键技术细节

- **方法名称**：FaviComp（Familiarity-aware Evidence Compression）。
- **核心思想**：利用两种模型——压缩模型（用于提炼证据）和目标模型（用于执行下游任务）——的**解码概率**共同指导压缩证据的生成，使得最终输出的压缩文本对目标模型而言具有更低的困惑度（perplexity），即“更熟悉”。
- **关键技术流程**：
  1. 输入原始检索证据与任务提示；
  2. 在生成压缩证据的每一步，同时计算压缩模型与目标模型对候选词的输出概率；
  3. 通过融合两者的解码概率（例如线性插值或某种加权组合），在每一步选择使目标模型困惑度最小化的词元；
  4. 逐步生成一段“兼顾信息保留”且“目标模型熟悉”的压缩文本，同时隐式地将目标模型的参数化知识融入压缩过程中。
- **亮点**：
  - **无需训练**：FaviComp 不需要额外的训练或微调，直接利用已有模型的推理概率进行解码。
  - **参数化与非参数化知识平衡**：通过将目标模型的概率纳入压缩解码，可在检索证据信息不足时，依靠模型内部知识进行补充或纠偏，从而减少生成失真。
  - **通用性强**：该策略可以适配任意压缩模型与任意目标模型的组合，作为即插即用模块。

### 3. 实验设计

- **任务与数据集**：论文聚焦于**开放域问答（open-domain QA）**，并且特别关注需要**多条证据**的场景——即一个问题的回答需要联合多个证据片段。
- **Benchmark 数据集**：摘要中未完全列出数据集名称，仅笼统提到“multiple open-domain QA datasets”。结合 RAG 证据压缩的常见基准，推测可能包括 Natural Questions、TriviaQA、HotpotQA 等多跳问答数据集，但原摘要并未给出具体名单。
- **对比方法**：与最新的多种“证据压缩基线方法（evidence compression baselines）”进行比较。具体基线名称在摘要中未列出，但通常对照项可能包括抽取式压缩、生成式压缩（如 Compressor、Recomp 等），以及不压缩直接拼接的原始 RAG 方法。
- **评估指标**：主要报告**准确率（accuracy）**，同时报告**压缩率（compression rates）**，以验证方法在保持信息量的同时能有效缩短上下文。

### 4. 资源与算力

- 论文的可用文本（摘要与元数据）中**没有明确说明**使用的 GPU 型号、数量、训练时长或推理资源开销。
- 由于方法声称“无需训练”，可以合理推断其主要开销来自推理阶段同时运行压缩模型和目标模型的解码计算，但具体硬件配置和耗时数据在当前材料中缺失。

### 5. 实验数量与充分性

- **已知实验数量**：从摘要中可以确认的实验包括：
  - 在多个开放域问答数据集上与多种证据压缩基线的对比；
  - 对“知识融合”效果的分析性实验，即验证参数化知识和非参数化知识在压缩过程中是否被有效结合；
  - 报告了压缩率与准确率之间的权衡。
- **充分性评估**：
  - **积极方面**：覆盖了多数据集、多基线的比较，且额外进行了关于“熟悉度”与“知识融合”的机制验证，这在方法类论文中是合理的。
  - **客观性/公平性风险**：由于无法查看论文正文，无法判断对比方法的超参数是否公平调优、使用的目标模型是否完全一致、是否进行了多次随机种子重复实验、是否报告了方差与显著性检验。
  - **总体判断**：摘要所展示的实验广度基本符合该研究问题的主流验证需求，但在我们可获得的信息范围内，无法确认实验的完整性和统计严谨性。

### 6. 主要结论与发现

- **性能提升**：在多个开放域 QA 数据集上，FaviComp 相比最新证据压缩基线，准确率最高提升 **23.91%**，同时保持较高压缩率。
- **证据可用性改善**：FaviComp 压缩出的证据对下游目标模型更“熟悉”，能帮助模型更有效地利用多条证据，降低不一致信息引发的干扰。
- **知识融合有效**：实验证据显示，FaviComp 在压缩过程中能够有效融合参数化知识与非参数化知识，当检索证据不完整时，可利用模型内部知识弥补信息缺口，从而进一步提升鲁棒性。
- **轻量通用**：无需额外训练，即可作为一个通用后处理模块应用于不同的压缩模型和目标模型组合。

### 7. 优点

- **问题切入点新颖**：将“证据压缩”与“目标模型熟悉度（perplexity）”联系起来，发现了现有压缩方法忽略的适配性问题。
- **技术简单高效**：免训练、即插即用，降低了应用成本，符合当前大模型时代对轻量可迁移模块的需求。
- **知识融合视角清晰**：把检索知识与模型参数知识放在统一的概率框架下权衡，理论上可在信息不充分时抑制幻觉。
- **效果显著**：最高接近 24% 的准确率提升，说明即使只改变解码阶段，也能带来强烈增益。
- **评价维度合理**：既关注答案质量（准确率），又报告压缩率，兼顾实际部署时的上下文窗口限制。

### 8. 不足与局限

- **信息不完整**：我们仅获取到标题、元数据与摘要，无法评估模型设计细节、公式定义、算法伪代码以及更多实验细节；若依据现有文本推断，上述分析存在一定不确定性。
- **实验覆盖范围有限**：摘要仅明确了开放域问答应用，尚未涉及对话、摘要、事实验证等其他 RAG 场景；也未明确是否测试不同规模的目标模型（如 7B、70B）或不同架构。
- **对比方法不透明**：没有列出具体基线名称、数据集名称和模型版本，难以判断实验的对比范围是否全面、是否包含最先进的压缩方法。
- **算力与分析缺失**：未说明运行方法所需的额外推理开销或延迟成本；免训练也可能带来更大的计算消耗（同时运行两个模型），但论文摘要未讨论该代价。
- **潜在偏差风险**：选择“熟悉”的证据可能使模型过于依赖参数化记忆，若目标模型本身存在知识偏差或事实错误，这种压缩方式可能会放大原有偏见；此外，概率融合中的权重设置可能对特定模型过度拟合，泛化性需进一步验证。
- **实际文本质量有限**：当前提供的可用内容仅为摘要，无法对方法内部机制进行更深入批判。

---

（完）
