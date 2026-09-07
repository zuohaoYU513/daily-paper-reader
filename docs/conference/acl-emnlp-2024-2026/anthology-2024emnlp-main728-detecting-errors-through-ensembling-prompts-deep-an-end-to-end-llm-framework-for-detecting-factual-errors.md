---
title: "Detecting Errors through Ensembling Prompts (DEEP): An End-to-End LLM Framework for Detecting Factual Errors"
title_zh: 通过提示集成检测错误（DEEP）：检测事实错误的端到端LLM框架
authors: "Alex Chandler, Devesh Surve, Hui Su"
date: 2024-11-01
pdf: "https://aclanthology.org/2024.emnlp-main.728.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 集成多样化提示检测摘要事实错误并输出校准概率
tldr: 该文针对摘要事实错误检测的可靠性问题，提出端到端框架DEEP。它使用多组提示让LLM识别事实不一致点，将输出作为二值特征交给集成模型，并经校准得到摘要是否忠实的准确概率。实验证明DEEP能有效检测摘要中的事实错误，并提供可信的概率判断，可用于自动评测与人工审查辅助。
source: EMNLP-2024-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main728/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 752, \"height\": 654, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main728/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 744, \"height\": 914, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main728/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1599, \"height\": 640, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2024-main/anthology-2024emnlp-main728/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1494, \"height\": 924, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main728/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 438, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main728/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 833, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main728/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 602, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main728/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1648, \"height\": 903, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main728/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1651, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2024-main/anthology-2024emnlp-main728/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1647, \"height\": 266, \"label\": \"Table\"}]"
motivation: 大模型摘要事实错误代价高，但人工审查整篇文档成本过大，需可靠的自动检测方法。
method: 设计不同LLM提示产生事实不一致判定，作为特征输入集成模型并做概率校准。
result: DEEP在事实错误检测任务上性能优于基线，产出校准良好的一致性概率。
conclusion: 为摘要事实一致性自动化检测提供了鲁棒、内蕴概率的LLM框架。
---

## Abstract
Accurate text summarization is one of the most common and important tasks performed by Large Language Models, where the costs of human review for an entire document may be high, but the costs of errors in summarization may be even greater. We propose Detecting Errors through Ensembling Prompts (DEEP) - an end-to-end large language model framework for detecting factual errors in text summarization. Our framework uses a diverse set of LLM prompts to identify factual inconsistencies, treating their outputs as binary features, which are then fed into ensembling models. We then calibrate the ensembled models to produce empirically accurate probabilities that a text is factually consistent or free of hallucination. We demonstrate that prior models for detecting factual errors in summaries perform significantly worse without optimizing the thresholds on subsets of the evaluated dataset. Our framework achieves state-of-the-art (SOTA) balanced accuracy on the AggreFact-XSUM FTSOTA, TofuEval Summary-Level, and HaluEval Summarization benchmarks in detecting factual errors within transformer-generated text summaries. It does so without any fine-tuning of the language model or reliance on thresholding techniques not available in practical settings.

---

## 论文详细总结（自动生成）

好的，我将遵循您的要求，对这篇论文进行详细的中文分析和总结。

### 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：大型语言模型（LLM）生成的文本虽然语言流畅，但经常包含看似合理实则错误的“幻觉”内容（事实不一致）。文本摘要是LLM最常用且重要的任务之一，其错误可能带来高昂代价，而人工审查完整文档的成本同样巨大，因此亟需可靠的自动事实一致性检测方法。
- **现存问题与核心动机**：
    1.  **传统评估指标失效**：基于n-gram重叠的传统指标（如ROUGE、BLEU）无法捕捉存在词汇差异时的语义等价性，与人类判断相关性差。
    2.  **现有专用模型性能受限**：以往基于编码器（如RoBERTa）的微调模型在处理新一代LLM生成的摘要时效果不佳。
    3.  **阈值依赖严重**：这是论文的核心关注点。现有（编码器）模型输出连续分数，需要通过阈值映射为二分类标签。论文指出，此前研究普遍存在在“测试集”上优化阈值的“不切实际”做法。作者实验证明，当阈值在不同数据集间迁移或设为默认中间值时，这些模型性能显著下降。这意味着，在无标注数据的真实场景下，这些模型缺乏实用价值。
    4.  **LLM自身过拟合与过度自信**：直接让LLM判断摘要一致性，其回答往往过于自信，导致高假阳性率（错误地将不实摘要判为正确）。
- **整体含义与研究目标**：为克服上述挑战，论文提出一种名为DEEP（Detecting Errors through Ensembling Prompts）的端到端框架，旨在以无需微调LLM、不依赖“测试集特定阈值”的方式，实现对LLM生成摘要的事实性错误进行高精度且具备良好概率校准的检测。

### 2. 方法论（核心思想与关键技术细节）

DEEP框架的核心思想是“集思广益”：通过设计多样化的提示（Prompts）调用LLM，使其从不同角度审视摘要的一致性，再将该多位“弱评论者”的意见（二值输出）交由一个集成的“仲裁者”模型进行汇总，最终输出一个经过校准的、具有实际概率意义的一致性分数。

**核心流程分三步**：

1.  **多提示生成（Prompt Ensembling）**：
    - **提示设计**：作者设计了大量（超过9个）不同的提示模板。这些提示在生成时使用了不同的策略（如不同的Chain of Thought步骤、显式的错误类型清单、对比分析要求）或不同的评估角度（如逐句分析、针对数字/实体等特定信息的核查）。每个提示要求LLM对摘要与源文档的一致性做出二值判断（0表示不一致，1表示一致）。
    - **作用**：每个提示相当于一个“弱分类器”，不同的提示能从不同维度捕捉不一致信息，其输出的二值结果构成一个特征向量。

2.  **集成建模（Ensembling）**：
    - **核心思想**：将第一步生成的所有二值特征（由不同LLM提示的输出组成）拼接成一个特征向量，训练一个集成模型来学习如何最优化地组合这些提示的判断。
    - **技术细节**：实验对比了16种不同的集成学习算法，包括逻辑回归、决策树/随机森林、梯度提升树（如XGB、LGBM）、支持向量机，以及专门用于弱监督学习的标签模型（如Snorkel中的LabelModel和Dawid-Skene）。其中，**LabelModel** 由于专门设计用于融合多个可能存在噪声的弱分类器，表现尤为突出。
    - **训练方式**：与测试集严格分离，所有集成模型均在待评估数据集的“其他三个数据集”上进行训练（如在AggreFact-XSUM上测试时，模型只在HaluEval和TofuEval的两个子集上训练）。这确保了评估的公平性和现实性。

3.  **概率校准（Calibration）**：
    - **核心思想**：LLM及神经网络普遍存在“过度自信”问题，输出的概率与真实准确率往往有偏差。为使最终输出具有可靠的概率意义（如80%的概率表示真正的80%准确率），需要对集成模型的输出进行校准。
    - **技术细节**：对比了多种校准方法，包括参数化的Platt Scaling和Temperature Scaling，以及非参数化的Histogram Binning、Isotonic Regression和BBQ（贝叶斯分箱）。其中，**Platt Scaling** 性能最佳。

**最终输出**：对于给定的“摘要-文档”对，DEEP输出一个介于0和1之间的校准概率，代表摘要事实一致（或不存在幻觉）的可能性。

### 3. 实验设计（数据集、基准与对比方法）

- **数据与基准（Benchmark）**：实验聚焦于由**近期Transformer模型**生成摘要的数据集，以贴合真实应用场景。共使用四个测试子集：
    1.  **AggreFact-XSUM FTSOTA**：基于XSUM数据，包含由多种最新微调Transformer模型生成的摘要。
    2.  **TofuEval MediaSum Summary-Level**：基于MediaSum的对话摘要，由LLM生成。
    3.  **TofuEval MeetingBank Summary-Level**：基于MeetingBank的会议摘要，由LLM生成。
    4.  **HaluEval Summarization**：一个大型基准，包含由ChatGPT生成的、带有人工标注幻觉的摘要。因其无官方划分，论文从10,000条中随机抽取3,000条平衡样本作为测试集。

- **对比方法**：
    1.  **编码器模型（Encoder Models）**：包括AlignScore, QuestEval, SummaC-ZS, SummaC-Conv, QAFactEval等五种流行的、基于NLI或QA的专用事实一致性检测模型。
    2.  **LLM解决方案（LLM Solutions）**：指通过提示工程直接让LLM进行判断的方法，如ChatGPT-ZS/CoT（由Luo等人提出）、ChatGPT-DA/Star（由Wang等人提出）、Tang2024等，采用GPT-3.5和GPT-4。
    3.  **自有方法（LLM Ensembles）**：DEEP框架，具体包括集成不同数量提示的变体：Ensemble-Top-3, Ensembled-Top-5, 和Ensemble-Top-9。

### 4. 资源与算力

- 论文中**未明确提及**训练或推理所使用的具体GPU型号、数量、总耗时等硬件资源信息。
- 文中仅在局限性部分提到，此LLM方法**需要更多的计算资源**，其参数量可能比微调的编码器模型高出数个数量级。具体的端到端推理成本和训练能耗并未提供。

### 5. 实验数量与充分性

- **实验数量**：
    1.  **提示性能评估**：展示了前5个最优提示在多个LLM（GPT-3.5和GPT-4）上于所有4个数据集的结果。
    2.  **集成方法比较**：比较了16种集成方法在4个数据集和3种提示池规模（3、5、9个提示）下的表现。这是一个非常大规模的矩阵式实验。
    3.  **与现有方法对比**：在核心结果表（Table 3）中，将DEEP与多种编码器模型和LLM方案进行了对比。
    4.  **校准分析**：评估了4种不同校准方法在所有数据集上对14种集成模型的影响，并比较了校准前后的ECE。

- **充分性与客观性**：
    - 论文的**对比实验设计非常公平且严格**。关键在于，所有编码器模型的阈值都不是在测试集上优化的（这是以往工作的通病），而是在“其他”数据集上训练的，这模拟了真实世界，客观反映了这些模型的泛化能力局限。
    - 集成了多种学习和非学习的集成方法，进行了寻找最优化特征的实验分析。
    - 校准实验部分科学地拆解了框架各组件对整体性能的增益。
    - **实验相当充分**。涵盖了不同数据域（新闻、对话、会议）、不同生成模型（微调与指令微调LLM）、多种对比基线和严格的评测设置，并为主要结论做了统计分析。

### 6. 主要结论与发现

- 传统的编码器型事实一致性检测模型对数据集特异性的阈值极度敏感，在不能于测试集上调阈值时性能会退化明显，不适用于真实世界场景。
- DEEP框架通过在多个LLM基准（AggreFact-XSUM FTSOTA、TofuEval Summary-Level、HaluEval Summarization）上达到新的最先进的平衡准确率（SOTA），明显优于被观测的现有最佳方法，而无需微调LLM或依赖测试集阈值技巧。
- 通过将多个提示的二元判断进行集成，性能可以稳定地超过任何一个最高性能的“单一”提示。在多数情况下，加入更多提示（9个）并不总是优于精选5个提示。
- 应用Platt Scaling对集成模型输出进行校准，能够显著降低期望校准误差（ECE），使预测概率更接近实测的真实可能性。

### 7. 优点

- **问题定位精准**：有力地揭露和证明了“在测试集上优化阈值”这一普遍做法的不现实性和性能欺骗性，给本领域其他研究者敲响了警钟。
- **方法论新颖且可行**：提出“提示集成”的想法，有效结合了不同提示的优势，利用弱监督集成学习化解了单一提示的偏见与不稳定性。
- **端到端与无监督适配**：提供了一种在无需访问目标数据标注的条件下即可工作的全流程方法，具有很高的实用性。
- **校准作为核心环节**：将概率校准作为框架的重要一步，追求高准确率的同时更专注于增强预估置信度的可靠性，为高风险的部署场景提供了实用可行模式。
- **实验设计严谨**：对比试验具有实验公平性，避免了常见的方法陷阱。

### 8. 不足与局限

- **算力与效率**：LLM的使用使推理成本远高于基于编码器的方法，这可能限制其在超大规模或实时性要求高场景下的应用（论文在Limitations中已承认）。
- **统计显著性受限**：作者承认在AggreFact-XSUM FTSOTA和TofuEval数据集上的表现虽优于次优方法，但在小样本量下没有拒绝零假设；显著的增益仅在较庞大的HaluEval数据集中得到统计确认。
- **外部泛化范围不清晰**：所有实验均基于英文数据；对跨语言摘要的检测表现仍没有可靠支持。其性能在新类型生成模型、其他语言和领域上是否依然稳健仍是开放问题。
- **标签噪声**：作者指出，除TofuEval采用多人注释外，其他基准测试中的注释噪声程度未知，可能影响实验的最终公正性。
- **提示模型的依赖**：集成方法的表现可能与基础LLM（GPT-4）的版本和“创意”紧密耦合，对模型迭代升级和开放源代码LLM的性能迁移尚待后续验证。
- **机制可解释性较低**：尽管端到端给出了准确率，但是否能清晰定位摘要中的哪一部分句子为何属于不实仍有进一步提升的余地（但论文表明中间提示已有一定可分析性，而这一点并非文章主要聚焦）。

（完）
