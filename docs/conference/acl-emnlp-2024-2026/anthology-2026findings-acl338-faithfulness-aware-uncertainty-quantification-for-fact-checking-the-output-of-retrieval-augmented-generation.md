---
title: Faithfulness-Aware Uncertainty Quantification for Fact-Checking the Output of Retrieval-Augmented Generation
title_zh: 面向检索增强生成输出事实核查的忠实感知不确定性量化
authors: "Ekaterina Fadeeva, Aleksandr Rubashevskii, Dzianis Piatrashyn, Roman Vashurin, Shehzaad Dhuliawala, Artem Shelmanov, Timothy Baldwin, Preslav Nakov, Mrinmaya Sachan, Maxim Panov"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.338.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 面向检索增强生成的事实性与忠实性区分不确定性量化，用于检测生成内容是否忠实于检索证据
tldr: 检索增强生成虽然能利用外部知识，但内部知识与检索证据的不一致常被混为一谈，导致把正确但不被检索支持的内容误判为幻觉。FRANQ 将事实性与忠实性分离，用忠实感知的不确定性量化来识别不被证据支撑的输出。该方法改善了 RAG 幻觉检测的精准性，为证据约束生成的事实一致性评估提供了更细粒度工具。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1648, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1626, \"height\": 675, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1629, \"height\": 596, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 755, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 755, \"height\": 595, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 755, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 759, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 762, \"height\": 627, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1618, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 805, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1311, \"height\": 644, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1315, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl338/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1327, \"height\": 597, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1570, \"height\": 696, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1620, \"height\": 823, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 760, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 737, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1648, \"height\": 731, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1647, \"height\": 732, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 794, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 787, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 786, \"height\": 748, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1642, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1644, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 821, \"height\": 567, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 757, \"height\": 149, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 792, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 796, \"height\": 520, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 796, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 796, \"height\": 521, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 793, \"height\": 634, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 796, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1647, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 671, \"height\": 987, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl338/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 773, \"height\": 1038, \"label\": \"Table\"}]"
motivation: RAG 系统仍易产生幻觉，而现有方法常混淆事实正确性与对检索证据的忠实性，误把正确但无检索支持的内容判为幻觉。
method: 提出 FRANQ，在不确定性量化中显式区分事实性与忠实性，评估生成内容是否能由提供证据可靠支持，用以检测不支持证据的输出。
result: 实验表明 FRANQ 能更准确地识别 RAG 幻觉，减少因混淆事实性与忠实性造成的误判。
conclusion: FRANQ 为 RAG 输出的事实核查提供忠实感知的量化方案，有助于证据约束生成的可信评估。
---

## Abstract
Large Language Models (LLMs) enhanced with knowledge retrieval, an approach known as Retrieval-Augmented Generation (RAG), have achieved strong performance in open-domain question answering. However, RAG remains prone to hallucinations: factually incorrect outputs may arise from inaccuracies in the model’s internal knowledge and the retrieved context. Existing approaches to mitigating hallucinations often conflate factuality with faithfulness to the retrieved evidence, incorrectly labeling factually correct statements as hallucinations if they are not explicitly supported by the retrieval. In this paper, we introduce FRANQ (Faithfulness-aware Retrieval-Augmented UNcertainty Quantification), a new method for hallucination detection in RAG outputs. FRANQ applies distinct uncertainty quantification techniques to estimate factuality, conditioning on whether a statement is faithful to the retrieved context. To evaluate FRANQ and competing uncertainty quantification methods, we construct a new long-form question answering dataset annotated for both factuality and faithfulness, combining automated labeling with manual validation of challenging cases. Extensive experiments across multiple datasets, tasks, and LLMs show that FRANQ achieves more accurate detection of factual errors in RAG-generated responses compared to existing uncertainty quantification and hallucination detection approaches.

---

## 论文详细总结（自动生成）

好的，我将按照您的要求，对论文《Faithfulness-Aware Uncertainty Quantification for Fact-Checking the Output of Retrieval-Augmented Generation》进行结构化、深入且客观的中文总结。

---

## 一、论文的核心问题与整体含义

**研究动机与背景**
- 检索增强生成（RAG）通过引入外部知识，提升了LLM在开放域问答中的表现，但**仍会产生事实性错误（幻觉）**。
- 现有RAG幻觉检测方法普遍存在一个关键缺陷：**混淆了"事实性"（Factuality）与"忠实性"（Faithfulness）**。
  - *忠实性*：生成内容是否被检索证据所蕴含（entailed）。
  - *事实性*：生成内容在客观事实上是否正确。
- 这种混淆导致一个严重误判：**模型产出了"事实正确、但不被检索证据支持"的陈述时**，会被错误地标记为幻觉。事实上，RAG的幻觉来源是多样的，既包括错误利用检索上下文（grounding错误），也包括模型内部知识本身的错误。因此，论文呼吁在RAG事实核查中，应以**检测"非事实性"内容**为首要目标，而非简单地检测"不忠实"内容。

**核心问题**
> 如何在RAG输出中，精确区分并分别评估上述两种"幻觉"来源，从而更准确地检测事实性错误？特别是，当输出语句不受检索证据支持时，如何判断它仅仅是"不忠实"还是真的"非事实"？

## 二、方法论：FRANQ

**核心思想**
FRANQ (Faithfulness-aware Retrieval-Augmented UNcertainty Quantification) 的核心思路是**先判断输出声称是否忠实于检索证据，再根据"忠实/不忠实"这一条件，采用不同的不确定性量化（UQ）方法去估计该声称的事实性**。这避免了用一套统一标准去衡量两种成因完全不同的错误。

**公式与算法流程**
FRANQ将声称c为真的概率进行了概率分解：

- **FRANQ(c) = P(忠实) × UQ_{faith}(c) + (1 − P(忠实)) × UQ_{unfaith}(c)**

该公式包含三个关键组件，分别对应图1中呈现的三步判断：

1. **忠实性评估组件 P(忠实)**：
   - 使用 **AlignScore**（基于RoBERTa的文本对齐评分模型）计算声称与检索证据之间的忠实度。
   - 论文指出AlignScore是连续且经过良好校准的（ECE仅为0.05），能避免二元分类的极端误差，适合作为概率权重。

2. **"忠实"条件下的事实性度量 UQ_{faith}**：
   - 此场景对应模型可能错误地应用了检索内容（例如，从文段中选错了实体）。
   - *长文QA设置*：使用 **Max Claim Probability**，即模型在给定原始上下文(x, r)下生成该声称token的对数概率。
   - *短文QA设置*：使用 **Semantic Entropy**（语义熵），通过采样多个输出并对其语义进行聚类以量化模型的不确定性。

3. **"不忠实"条件下的事实性度量 UQ_{unfaith}**：
   - 此场景中，声称来源于模型内部参数化知识，因此应避免检索上下文带来的分布偏移。
   - *长文QA设置*：提出 **Parametric Knowledge** 方法——将检索证据r从输入中移除，仅保留问题x，对原声称进行前向传播，计算模型仅基于内部知识生成的（对数）概率。
   - *短文QA设置*：使用 **Sum of Eigenvalues**（图拉普拉斯算子的特征值之和，一种基于样本多样性的黑盒UQ方法）。
   - *消融研究发现*：在短文QA中，这是预测不忠实声称事实性的最优选项。

4. **校准策略**：
   - 由于UQ_{faith}和UQ_{unfaith}的原始分数分布不同，直接相加会导致权重失衡。
   - 论文引入了**等渗回归（Isotonic Regression）**将原始UQ分数校准到概率空间。
   - 提出了三种校准变体：无校准、统一校准、**条件校准**（分别在忠实和不忠实的子集上单独校准两个UQ方法）。后者是论文主推的方法。

## 三、实验设计

**使用的Benchmark与数据集**
1. **新构建的长文QA数据集（主推）**：
   - **问题来源**：RAGTruth (44个最具挑战性问题) + 32个GPT-4生成的"how-to"技术问题。
   - **检索模型**：Contriever，每个问题取Top-3 Wikipedia片段。
   - **LLMs**：Llama 3B Instruct、Llama 8B Instruct、Falcon 3B Base、Gemma 4B Instruct（贪婪解码）。
   - **数据标注**：使用GPT-4o-search自动分解为原子声称，并进行事实性（True/False/Unverifiable）和忠实性（Faithful/Unfaithful）标注；对自动标注结果为"False/Unverifiable"的难例，进行**人工复核修正**。人工标注者间对事实性标签的一致性达0.87。
2. **短文QA数据集**：TriviaQA、SimpleQA、Natural Questions、PopQA。每个数据集采样200条（训练）+1000条（测试），将每个模型的输出视为一个原子声称，并与标准答案进行GPT-4o比对得到事实性标签。

**对比方法（Baselines）**
- **通用基线**：Max Sequence/Claim Prob., P(True), Perplexity, Mean/Max Token Entropy, CCP, Lexical Similarity, Degree Matrix, Sum of Eigenvalues, Semantic Entropy, SentenceSAR。
- **RAG特定基线**：AlignScore（单独使用）、Parametric Knowledge（单独使用）。
- **XGBoost方法**：使用FRANQ组件特征（AlignScore, UQ_faith, UQ_unfaith）的XGBoost；使用所有UQ特征堆叠的XGBoost。
- **FRANQ三种变体**：No calibration / Calibrated / Condition-calibrated。

**评估指标**
- **PR-AUC**（将事实性错误视为正类，侧重于检测错误）。
- **PRR**（预测拒绝比率，衡量拒绝部分输出后对正确预测的保留能力）。

## 四、资源与算力

论文在附录E中明确记录了算力消耗：
- **长文QA实验**：完整的生成与UQ基线评估约需 **8天** 的NVIDIA **V100 32GB GPU** 时间。
- **短文QA实验**：耗时不到 **1天**。
- **API成本**：使用OpenAI API（GPT-4o）进行声称分解、匹配和标注，每运行一个模型（如Llama 3B Instruct）成本约为 **100美元**。
- **人工标注**：6名学生标注员，每人约**3小时**的人工复核工作量。
- **额外计算成本**：FRANQ方法的额外推理开销很小，条件校准的等渗回归拟合仅需**不到1秒**，训练体积仅几KB。

## 五、实验数量与充分性

**实验数量**
- 实验规模十分丰富。涵盖**4个长文QA模型**与**4个短文QA数据集 × 4个模型**的矩阵测试，并在12张详细表格中给出了完整结果。
- **2个主要benchmark**（长文与短文）。
- **大量消融实验**：
  - 不同UQ_{faith}与UQ_{unfaith}组合分析（图2）。
  - 对AlignScore进行二值化阈值转换的效果对比。
  - 对AlignScore额外进行校准的影响。
  - **鲁棒性测试**：在检索数据被随机打乱或包含事实性错误（corrupted）情况下的表现比较。
  - **监督规模影响**：通过改变校准训练数据的规模，展示带校准FRANQ的稳定性。
  - **XGBoost决策树结构分析**（验证其分裂逻辑和FRANQ相似）。
  - **模型校准性能（ECE）的对比**。

**实验是否充分、客观、公平**：
- **充分**：实验设计维度丰富，覆盖不同任务、模型大小和数据类型，且总计算量不小，足以支持主要结论。
- **客观**：使用了混合（自动+人工）标注，并在文中讨论了标注质量。通过PR-AUC和PRR等客观指标进行评估，避免了单一指标可能带来的偏差。
- **公平**：对比了广泛的基线，包括信息型、采样型样本多样性、RAG特定型和监督型方法。重要的是，FRANQ在长文和短文QA中选用的组件（如UQ_faith等）均基于公开库实现，且实验设置（如模型输入）保持固定，控制变量，具有较好的公平性。

## 六、主要结论与发现

1. **FRANQ有效提升检测精度**：在长文QA中，FRANQ（条件校准变体）在大多数模型上取得了最优的PR-AUC和PRR。在短文QA的所有模型中，条件校准版FRANQ几乎均取得最优的平均性能。
2. **区分事实性/忠实性是关键**：对于"正确但不受支持"的声称，FRANQ能给出相对较高的事实性分数，从而避免将事实正确的输出误判为幻觉。
3. **忠实性条件对UQ方法选择至关重要**：消融分析显示，不忠实分支的方法选择对结果影响巨大（Parametric Knowledge在长文QA中表现突出）；而忠实分支的方法选择则相对鲁棒（语义熵在短文QA中表现最佳）。
4. **泛化与鲁棒姓**：在检索被降级（shuffled）或误导（corrupted）时，FRANQ（条件校准版）均优于所有基线，表现出很强的鲁棒性。
5. **可解释性与资源效率**：通过简单的等渗回归校准，就能在极低的算力开销下（训练时长<1秒）获得显著增益，同时保留了概率解释性。

## 七、优点

- **概念创新性强**：将**忠实性**从**事实性**中剥离出来，提出了新的错误分解逻辑，为RAG幻觉检测提供了更精确的理论框架，克服了传统方法对"正确但不受支持"数据的误判。
- **方法设计巧妙**：将概率公式与任务特性（长文/短文QA中的模型不确定性本质差异）紧密结合，针对不同误差来源选择了不同的UQ策略，而无需重新训练模型。
- **新数据集的贡献**：发布了同时标注了事实性与忠实性的细粒度长文QA数据集，并采用了"自动化+人工复核"的高效标注策略，为后续研究提供了宝贵资源。
- **实验全面且严谨**：涵盖多模型、多任务、多数据集的密集测试，尤其是针对检索噪声的鲁棒性实验非常出色，能够反映方法在真实场景下的表现。

## 八、不足与局限

- **对基础信号的依赖**：FRANQ的有效性依赖于AlignScore等底层组件的可靠性。在遇到极其复杂或隐含的推理、或严重检索偏离时，其表现依然会受底层组件准确度的限制。
- **监督信号的使用**：虽所需数据量极小，但FRANQ的变体仍需要少量带标签数据进行校准，限制了在零标签场景下的即插即用。
- **任务与数据覆盖面**：实验集中在QA任务，未涉及到开放式对话或摘要生成等领域，是否可泛化至广泛的知识生成任务仍需验证。
- **LLM标注偏差风险**：长文数据集的自动标注（含GPT-4o-search与GPT-4o）仍可能引入模型本身的偏好或固有偏见。尽管对难例进行了人工复核，但整体标注流程仍有内在的系统性偏差风险。
- **对检索器的依赖**：实验固定使用Contriever，未尝试不同检索器组合（如BM25、密集检索混合）下FRANQ的表现，其泛化性对不同检索架构的适应性未知。

**（完）**
