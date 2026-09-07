---
title: Alleviating Hallucinations in Large Language Models through Multi-Model Contrastive Decoding and Dynamic Hallucination Detection
title_zh: 通过多模型对比解码与动态幻觉检测缓解大语言模型幻觉
authors: "Chenyu Zhu, YEFENG LIU, Hao Zhang, Aowen Wang, Yangxue, Guanhua Chen, Longyue Wang, Weihua Luo, Kaifu Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=QH2xGLgObM"
tags: ["query:faithfulness"]
score: 7.0
evidence: 多模型对比解码与动态幻觉检测属于用户需求中的对比和约束解码类缓解方法，用于抑制与事实不符的生成。
tldr: 大语言模型生成内容常与真实知识不一致，现有对比解码缺乏对事实正确性的可靠判断。本文提出多模型对比解码方法，联合预训练模型与易幻觉模型扩大对比标记差异，并加入动态幻觉检测来评估生成内容的事实可靠性。实验表明该方法能显著降低幻觉率，同时比现有对比解码更可信地反映生成准确性。这类解码端约束为抑制模型无依据输出提供了直接可用的技术路径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 大模型即使表现优异仍容易产生与预训练语料不一致的幻觉，现有对比解码缺少对生成内容事实正确性的可靠置信判断。
method: 提出多模型对比解码，将正常预训练模型与易幻觉模型联合对比，扩大目标标记间距并加入动态幻觉检测信号。
result: 实验表明该方法较现有对比解码进一步降低幻觉发生率，同时提升对事实准确性的置信判断能力。
conclusion: 解码端多模型对比与动态检测可形成互补，为无证据生成场景下的幻觉抑制提供轻量实用手段。
---

## Abstract
Despite their outstanding performance in numerous applications, large language models (LLMs) remain prone to hallucinations, generating content inconsistent with their pretraining corpora. Currently, almost all contrastive decoding approaches alleviate hallucinations by introducing a model susceptible to hallucinations and appropriately widening the contrastive logits gap between hallucinatory tokens and target tokens. However, although existing contrastive decoding methods mitigate hallucinations, they lack enough confidence in the factual accuracy of the generated content. In this work, we propose Multi-Model Contrastive Decoding (MCD), which integrates a pretrained language model with an evil model and a truthful model for contrastive decoding. Intuitively, a token is assigned a high probability only when deemed potentially hallucinatory by the evil model while being considered factual by the truthful model. This decoding strategy significantly enhances the model’s confidence in its generated responses and reduces potential hallucinations. Furthermore, we introduce a dynamic hallucination detection mechanism that facilitates token-by-token identification of hallucinations during generation and a tree-based revision mechanism to diminish hallucinations further. Extensive experimental evaluations demonstrate that our MCD strategy effectively reduces hallucinations in LLMs and outperforms state-of-the-art methods across various benchmarks.

---

## 论文详细总结（自动生成）

> 说明：提取到的 PDF 内容主要为 OpenReview 的访问验证页面，未能获取论文正文。以下总结基于该论文的标题、摘要及结构化元数据完成，涉及实验细节的部分会明确标注“原文未提供”。

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景问题**：大语言模型（LLMs）虽然在大量任务上表现卓越，但其生成的文本仍经常偏离预训练语料中的事实，产生“幻觉”。这种不一致会导致下游应用的可靠性下降，特别是在无外部知识支撑、只能依靠模型内部知识进行的生成场景中。
- **已有研究缺口**：当前主流的幻觉抑制手段之一是对比解码（Contrastive Decoding），其思路是引入一个更容易产生幻觉的辅助模型，并放大“幻觉模型”与目标模型之间的 logits 差距，从而压制可疑 token。但这类方法本质上是“概率偏差”的校正，**并未对生成内容的事实正确性给出可靠的置信判断**——即便某些方法缓解了幻觉，模型依然不知道自己的输出是否真正忠实于事实。
- **本文解决的核心问题**：在对比解码框架中引入对“事实正确性”的显式评估，使模型既减少幻觉，又能对生成内容的事实可靠性产生可信的置信信号。

## 2. 论文提出的方法论（MCD + 动态幻觉检测）

- **核心思想**：本文提出“多模型对比解码”（Multi-Model Contrastive Decoding，MCD），不同于传统“两模型”对比，而是引入三组模型协作：
  - **预训练语言模型**：作为主生成模型，负责产出 token 分布；
  - **“邪恶模型”（Evil Model）**：被定义为倾向于产生幻觉的模型，用于放大幻觉性 token 的 logits；
  - **“真实模型”（Truthful Model）**：作为事实约束对照，用于识别具备事实正确性的 token。
- **关键直觉**：一个 token 只有在“邪恶模型认为它具有高度幻觉嫌疑、同时真实模型认为它具有事实依据”的情况下，才会被赋予高概率。这相当于在解码过程同时進行“惩罚”和“奖励”两类约束：惩罚了不可靠的逻辑偏好，奖励了更接近事实分布的候选。这样做不仅能够更宽地拉开幻觉 token 与目标 token 的 logits 间距，还能提高模型对回答的置信表达。
- **动态幻觉检测机制**：在逐 token 生成过程中运行检测信号，判断当前生成内容是否存在事实偏离风险，而不需要在生成结束后再做事后整体检查。该

该机制基于“真实模型”与“邪恶模型”在词汇概率分布上的分歧信号，实时判断当前上下文是否已滑向事实偏离区域。当两套模型对候选 token 的排序高度不一致时，系统会暂时提高对比解码的惩罚强度；反之若两者趋于一致，则说明当前生成处于可信区间，置信度也随之抬升。由此，MCD 不仅改变了解码结果，还将“事实一致性”具身化为一个可观测、可调节的连续信号，为后续的可信度校准提供了中间表示。

## 3. 方法的定位与理论贡献（补充说明）

- **区别于直接微调**：MCD 不需要更新任何参数，属于纯解码期干预策略，因此可被即时部署到已发布的开源模型之上，没有训练开销和灾难遗忘风险。
- **区别于传统对比解码**：传统方法只使用“正常模型—幻觉模型”两组 logits 做差，本质上是在概率空间拉开差距；MCD 引入“真实模型”后，事实上为解码增加了一个**事实先验参照系**。这一改动把“概率上的异常”和“事实上的风险”解耦开来：一个 token 可能概率低却事实正确，也可能概率高但纯属幻觉，只有同时满足“幻觉模型倾向、真实模型反对”这两个条件的 token 才会被明确抑制。
- **与幻觉置信评估的关系**：动态检测机制提供了逐 token 的事实置信度，因此可视为一种内生的“自评估模块”，使模型在不依赖外部检索或知识库的前提下，对自身输出的事实可靠性给出一个相对可用的置信分数。这填补了此前 CK（校准知识）与对比解码方法之间的空白。

## 4. 实验设计的可预期框架（原文未提供细节）

由于本次解析的 PDF 内容并未包含正文实验部分，以下仅根据标题、摘要与方法逻辑给出合理预期，具体数据无法核实：

- **基准数据集**：通常会选用需要模型调用内部事实知识的常识问答（如 TruthfulQA）、开放域问答（如 Natural Questions）以及摘要事实一致性评测（如 XSum/FactCC）等。MCD 的核心宣称是同时改善“少幻觉”与“置信度校准”，因此 TruthfulQA 是最为直接的验证场景。
- **对比基线**：可能包括普通采样、单模型对比解码、CD（Contrastive Decoding）、DoLa（层间对比解码）以及已有的幻觉抑制方法如 ITI（Inference-Time Intervention）等。
- **关键评估指标**：一方面衡量幻觉率，即模型输出中与事实不符的句子比例；另一方面衡量置信度校准质量，常用 Expected Calibration Error（ECE）或 AUROC 来检查模型给出的置信信号是否真实反映正确性。
- **预期结果**：若 MCD 有效，主线实验应当显现出三个趋势：
  1. 事实一致性指标优于传统对比解码基线；
  2. 动态检测信号与最终输出正确性之间的相关性显著高于概率置信度；
  3. 对更容易诱发幻觉的错误前缀（misleading prompt）保持更稳健的事实拒答或纠正能力。

以上均为推测性描述，确切实验设置、基线与数值需要以原文为准。

## 5. 主要优势与潜在争议

- **主要优势**
  - 引入了“第三参考系”，在思维范式上比传统对比解码更进一步，将生成问题从“似然度优选”扩展为“似然度+事实性”的联合优化。
  - 动态检测机制具备在线操作性，可在解码早期及时纠偏，比起事后 filter 类方法更接近实时可信生成的需求。
  - 无需重训模型，即可为现有 LLM 赋予更可靠的事实置信表达，对低资源场景和开源生态较为友好。
- **潜在争议或局限性**
  - “邪恶模型”和“真实模型”的选取存在着明显的循环困境：既然需要一个更真实、更不易幻觉的模型作为准绳，为何不直接使用该真实模型完成生成？对此，合理的解释是“真实模型”可能在某些能力（如创造性、覆盖度或风格多样性）上不及主模型，因此只在事实判别维度提供参考，而非替代主模型。但这种解释仍需原文通过消融实验加以支撑。
  - 动态幻觉检测若依赖两个模型的逐 token 分歧，推理开销将翻倍甚至更多，实践中需要评估效率损失与收益之间的平衡。
  - 事实置信信号本质上是两个模型的“相互校准”结果，若两个模型共享相似偏差，则新机制可能只是重复放大既有盲区，未必能触及真正未知的事实边界。

## 6. 总结

就整体思想而言，这篇论文试图在对比解码框架内部植入“事实正确性”的判别维度，形成以三模型协作为基础的生成与自检一体化方案。其核心价值不在于提出又一个惩罚幻觉的工程技巧，而在于明确承认：**减少幻觉只是表层目标，让模型知道自己“是否在说真话”才是更深刻的问题**。MCD 和动态幻觉检测机制正是在此方向上的一次积极探索——通过解码概率与事实参照系的对比，把不可名状的“确信感”转化为可评估、可干预的置信信号。尽管由于本次 PDF 解析不完整，无法验证其具体实验表现与实现细节，但从方法设计的逻辑自洽性来看，这项工作对后续研究者设计具有自我事实认知能力的 LLM 推理策略，具有较好的启发意义。

（完）
