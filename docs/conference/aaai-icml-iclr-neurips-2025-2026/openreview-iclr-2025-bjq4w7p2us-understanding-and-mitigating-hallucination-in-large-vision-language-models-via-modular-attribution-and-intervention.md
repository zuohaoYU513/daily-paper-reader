---
title: Understanding and Mitigating Hallucination in Large Vision-Language Models via Modular Attribution and Intervention
title_zh: 通过模块化归因与干预理解并缓解大型视觉语言模型中的幻觉
authors: "Tianyun Yang, Ziniu Li, Juan Cao, Chang Xu"
date: 2025-01-22
pdf: "https://openreview.net/pdf?id=Bjq4W7P2Us"
tags: ["query:hallu-rag"]
score: 4.0
evidence: 通过因果中介和模块级干预分析LVLM幻觉机制，对理解一般LLM幻觉有迁移价值。
tldr: 该文旨在解释大型视觉语言模型为何产生幻觉并加以缓解。通过反事实编辑进行因果中介分析，发现多头注意力模块比多层感知机对幻觉词的生成贡献更大，并定位到具体幻觉头。进一步的行为分析显示这些注意力头相对集中，可据此进行干预。该工作为理解视觉语言模型幻觉的内部机制和实现可解释缓解提供了重要线索。
source: ICLR-2025-Accepted
selection_source: conference_retrieval
motivation: 大型视觉语言模型在开放式生成中常产生幻觉，但其内部归因机制尚不清楚。
method: 进行反事实因果中介分析，定位贡献最大的多头注意力头和模块，并进行针对性干预以缓解幻觉。
result: 发现多头注意力模块比多层感知机对幻觉词生成影响更大，并识别集中出现的幻觉头。
conclusion: 提供定位幻觉内部来源和进行干预的路径，对设计可解释的幻觉缓解方法有启示。
---

## Abstract
Large Vision-Language Models (LVLMs) exhibit impressive capabilities in complex visual tasks but are prone to hallucination, especially in open-ended generation tasks. This paper explores why LVLMs tend to hallucinate and how to mitigate it. First, we conduct causal mediation analysis through counterfactual edits on specific modules in LVLMs. Our results disclose that Multi-Head Attention (MHA) modules contribute more to the probability of generating hallucination words than multi-layer perceptron modules. We then identify specific heads that are responsible for hallucination, referred to as hallucination heads. Second, we examine the behavior of hallucination heads. We find that they are concentrated in the middle and deeper layers, displaying a strong attention bias toward text tokens. Further, we show that the attention patterns of certain hallucination heads exhibit greater similarity to the base language model and change slowly during the instruction tuning process. Finally, we propose two simple yet effective methods to mitigate hallucination: one is training-free and can be applied directly during decoding, while the other involves fine-tuning. Both methods are targeted for hallucination heads to reduce their reliance on text tokens. Notably, our methods achieve up to 1.7x reduction in hallucination rate for the LLaVA-v1.5-7B model in COCO captioning task, outperforming existing baselines. Overall, our findings suggest that hallucinations in LVLMs are likely to stem from certain modules, and targeted interventions can effectively mitigate these issues.

---

## 论文详细总结（自动生成）

## ⚠️ 重要说明

当前抓取到的 OpenReview PDF 页面实际为“浏览器验证（CAPTCHA）”页，**并未包含论文正文内容**。因此，以下总结严格基于可获取的 **标题、元数据（tldr/abstract）** 编写。凡是缺失或无法从摘要中确证的内容，我会明确标注“正文不可见”。完整的公式、超参数与详细实验表，需在能够访问 PDF 原文后补充核实。

---

# 论文总结：通过模块化归因与干预理解并缓解 LVLM 幻觉

**论文标题（原）**：Understanding and Mitigating Hallucination in Large Vision-Language Models via Modular Attribution and Intervention  
**论文标题（中）**：通过模块化归因与干预理解并缓解大型视觉语言模型中的幻觉  
**作者**：Tianyun Yang, Ziniu Li, Juan Cao, Chang Xu  
**来源**：ICLR-2025-Accepted / OpenReview (Bjq4W7P2Us)

## 1. 核心问题与整体含义

- 研究对象是 **大型视觉语言模型（LVLMs）**。
- 核心问题是：**LVLM 在开放式视觉生成任务中为什么会产生幻觉，以及如何缓解幻觉**。
- 背景动机是：现有方法往往只在“输出层面”检测/修正幻觉，但 **对模型内部的归因机制不够清楚**——幻觉究竟来自哪些模块、哪些注意力头，以及它为何在指令微调后仍难以被消除，都缺乏可解释的解析。
- 整体意义在于：如果能够在模型内部定位“致病”组件，就可以**从机制层面干预**，而不是仅仅做后处理式的文本修正。该文的相关思路也可能迁移到一般 LLM 幻觉研究中。

## 2. 方法论

核心思想是**因果中介分析 + 反事实编辑 + 模块级归因 + 定向干预**。

根据摘要可以重构出如下步骤：

- **反事实因果中介分析**：对 LVLM 的特定内部模块（注意力模块、MLP 模块）施加反事实编辑（counterfactual edits），观察“生成幻觉词的概率”受干扰的程度，从而衡量该模块的因果贡献。
- **模块间对比**：比较 Multi-Head Attention (MHA) 与 Multi-Layer Perceptron (MLP) 两类模块对幻觉词概率的影响大小，发现 **MHA 的贡献大于 MLP**。
- **细粒度归因：定位“幻觉头”**：进一步在多头注意力内部定位到具体哪些注意力头（heads）主要导致幻觉，提出“hallucination heads”（幻觉头）概念。
- **幻觉头行为分析**：
  - 分析其所在层分布，发现幻觉头**集中在中层和深层**；
  - 观察其注意力模式，发现它们对 **文本 token 存在明显的注意力偏置**；
  - 对比幻觉头与基础语言模型（base LM）的注意力相似性，发现在指令微调过程中，某些幻觉头的注意力模式变化**缓慢**且与基座模型更相似——说明这种偏置可能是“继承”下来的。
- **干预方法**：
  - 方法 1：training-free，在解码阶段直接干预，抑制幻觉头对文本 token 的过度依赖；
  - 方法 2：fine-tuning，对幻觉头做针对性微调，降低其文本 token 依赖。
- 公式与算法细节：由于正文不可见，**无法提供具体的因果效应公式或干预权重表达式**；但摘要明确说该方法最终作用于解码/微调过程，实现“针对性缓解”。

## 3. 实验设计

根据摘要/元数据的可见信息：

- 使用模型：**LLaVA-v1.5-7B**。
- 主要任务：**COCO captioning（图像描述生成）**。
- 幻觉评价指标：摘要中提及“hallucination rate”，但**没有明确给出基准指标名称**（如 CHAIR、POPE 等），需查正文确认。
- 对比对象：作者称“outperforming existing baselines”，但**没有列出具体基线方法名**。
- 上游分析还包括：
  - 对指令微调过程做动态观察；
  - 将模型的注意力模式与基座语言模型对比。
- 总效果：在 COCO captioning 上，**幻觉率最高降低 1.7 倍**。

## 4. 资源与算力

- 在摘要与当前可见元数据中，**没有明确说明 GPU 型号、数量、训练时长、推理代价等资源信息**。
- 由于正文不可见，无法判断是否在正文中有补充的算力描述。
- 只能推断：实验规模涉及 7B 量级模型，并需要做 fine-tuning 与解码期干预，训练成本应不低，但具体数值未知。
- 说明：这一点属于“缺失信息”，不应臆测为论文未报告。

## 5. 实验数量与充分性

从摘要可间接确认的实验环节有：

- 模块级比较：MHA vs MLP 的幻觉贡献差异；
- “幻觉头”定位实验；
- 幻觉头的层分布与文本 token 注意力偏置分析；
- 与基础语言模型的对比实验；
- 指令微调过程中的动态分析；
- 两种干预实验：training-free 与 fine-tuning；
- 在 COCO captioning 上与基线对比的幻觉率实验。

需要指出的充分性问题：

- **正文中是否有跨模型、跨任务、跨数据集的实验尚不可知**；
- 摘要只提到一个主实验（LLaVA-v1.5-7B + COCO captioning），**泛化性实验**覆盖度无法判断；
- 是否存在多种随机种子、统计显著性检验、方差报告，需要看正文；
- 是否控制和“降低文本偏置”可能带来的**能力损失**，也需要看消融或质量评估实验。
- 因此：当前可见内容表明实验设计**逻辑完整、从归因到解释到缓解的链条闭环**，但“充分性”是否达到顶级水平，需在读取 PDF 全文后判断。

## 6. 主要结论与发现

1. **MHA 模块比 MLP 模块对幻觉词生成的因果贡献更大**。
2. 可以定位出“幻觉头”这一具体因果单元。
3. 幻觉头并非随机分布，而是**集中于中层和深层**。
4. 幻觉头表现出对**文本 token 的持续性注意力偏置**，这可能是视觉信息未被充分采用的表现。
5. 部分幻觉头的注意力模式与**基础语言模型更相似**，并在指令微调过程中变化缓慢——提示 LVLM 的幻觉可能部分来源于底座 LLM 的语言先验/文本偏置，而非完全由视觉指令微调造成。
6. 通过**针对幻觉头进行训练无关解码干预**或**定向微调**，能显著减少幻觉率，例如在 LLaVA-v1.5-7B 的 COCO captioning 任务上最高取得 1.7x 的幻觉率下降。

## 7. 优点

- **分析与干预的闭环**：不是做纯相关性分析或结果端修正，而是通过因果反事实找到真实“元凶”，再做定向干预，具备较强的可解释性。
- **定位粒度细**：从模块级到具体头级，从“黑盒模型”细化到“哪个头在产生幻觉”。
- **方法论简洁实用**：最后提出既有无训练解码策略又有微调策略，兼顾“快速部署”与“更强效果”。
- **发掘幻觉的纵向来源**：发现部分幻觉头与基础语言模型高度相似、指令微调变化缓慢——这为理解“为什么 LVLM 难以校准幻觉”提供了有价值的机制解释。
- 对一般 LLM/多模态模型的幻觉研究具有较好的迁移潜力和借鉴意义。

## 8. 不足与局限

- **可验证信息不足**：因为当前 OpenReview PDF 页面为验证页面，正文无法获取，包括具体方法公式、实验表格、消融细节、局限性讨论等仍未知。
- **潜在模型覆盖面问题**：可见实验只集中在 LLaVA-v1.5-7B，是否适用于 Qwen-VL、InternVL、GPT-4V 类等架构仍不明确。
- **数据集覆盖可能偏窄**：摘要中直接点名 COCO captioning；开放式幻觉是开放域问题，仅依赖一个caption任务可能不够。
- **“减少文本 token 依赖”有副作用风险**：语言先验并非一无是处，若过度抑制文本偏置，可能导致常识性表达或推理能力下降；需要验证是否对 VQA、视觉推理等任务造成性能损失。
- **因果归因的有效性高度依赖反事实编辑方式**：如果扰动方式过强/不自然，所观测到的“因果效应”可能并非真实机制，而是对非自然隐藏状态的反映；这种风险在描述中无法排除。
- **缺乏资源/算力说明**：训练、推理开销不清楚，不利于公平对比和复现。
- 部分表达存在过度归因的可能，如“1.7x reduction”虽然效果显著，但没有给出绝对数值和绝对质量指标，实际改善幅度难以直接判读。

---

（完）
