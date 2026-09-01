---
title: "SAFE: A Sparse Autoencoder-Based Framework for Robust Query Enrichment and Hallucination Mitigation in LLMs"
title_zh: SAFE：基于稀疏自编码器的大语言模型查询扩充与幻觉缓解框架
authors: "Samir Abdaljalil, Filippo Pallucchini, Andrea Seveso, Hasan Kurban, Fabio Mercorio, Erchin Serpedin"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.496.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 利用稀疏自编码器实现LLM幻觉检测与缓解，并支持幻觉感知查询扩充
tldr: 大模型在关键应用中容易产生幻觉，现有工作未将稀疏自编码器与幻觉检测系统化结合。论文提出SAFE框架，利用稀疏自编码器检测并缓解幻觉，并实现幻觉感知的查询扩充，以提升鲁棒性。在两种模型和四个跨域数据集上的评测表明，SAFE能有效降低幻觉并改善下游表现，为幻觉治理与查询增强提供了统一方案。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp496/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp496/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1608, \"height\": 654, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp496/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1493, \"height\": 824, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp496/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 583, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp496/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 814, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp496/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1659, \"height\": 735, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp496/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 297, \"label\": \"Table\"}]"
motivation: 大模型幻觉破坏关键应用可靠性，稀疏自编码器与幻觉检测的协同尚未得到系统利用。
method: 提出SAFE框架，基于稀疏自编码器检测和缓解幻觉，并利用幻觉信息进行鲁棒查询扩充。
result: 在两种可用SAE模型和四个跨域数据集上验证了SAFE能有效检测和缓解幻觉并提升鲁棒性。
conclusion: SAE可为幻觉检测、缓解与查询增强提供统一且可迁移的框架，提升大模型部署可靠性。
---

## Abstract
Despite the state-of-the-art performance of Large Language Models (LLMs), these models often suffer from hallucinations, which can undermine their performance in critical applications. In this work, we propose SAFE, a novel framework for detecting and mitigating hallucinations by leveraging Sparse Autoencoders (SAEs). While hallucination detection techniques and SAEs have been explored independently, their synergistic application in a comprehensive system, particularly for hallucination-aware query enrichment, has not been fully investigated. To validate the effectiveness of SAFE, we evaluate it on two models with available SAEs across four diverse cross-domain datasets designed to assess hallucination problems. Empirical results demonstrate that SAFE consistently improves query generation accuracy and mitigates hallucinations across all datasets, achieving accuracy improvements of up to 29.45%.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

**研究动机与背景**

- 大语言模型（LLMs）虽然能力强大，但普遍存在**幻觉（hallucination）**问题，即在生成文本时编造与事实不符的信息。幻觉可分为两类：**事实性幻觉**（超出训练数据范围的内容）和**相关性幻觉**（内容在事实上正确但与问题上下文无关）。
- 现有缓解策略主要分为两条路径：
  - **数据驱动方法**：过滤预训练数据或利用高质量指令微调数据；
  - **输入端技术**：如检索增强生成（RAG），通过外部可验证信息扩充查询。
- 然而，这些方法普遍**忽视LLM的内部工作机制**，未触及幻觉产生的根源。一个关键原因是**多义性（polysemanticity）**——单个神经元在多个语义无关的上下文中被激活，导致模型内部决策过程不透明。多义性通常源于**叠加（superposition）**现象。
- **稀疏自编码器（SAE）** 能够将多义激活分解为大规模、可解释的单义特征字典，为深入理解模型内部表示提供了工具。
- 尽管幻觉检测技术和SAE已被分别探索，但二者的**系统化协同应用**——特别是在“幻觉感知的查询扩充”这一任务中——尚未被充分研究。本文提出的 **SAFE** 框架填补了这一空白。

**SAFE的核心洞见**

- 缓解幻觉**不需要向LLM注入新知识**，而是通过选择预训练阶段学到的最相关特征，引导模型更有效地利用已有知识，从而减少不相关激活。
- SAFE采用两阶段流程：先**检测**潜在幻觉，再通过SAE提取可解释特征来**扩充输入查询**，引导模型生成更准确、更可靠的回答。

## 2. 方法论

**整体流程（两阶段）**

- **第一阶段：可插拔的幻觉检测（Plug-and-play Hallucination Detection）**
  - SAFE可无缝集成任何输出置信度或幻觉分数的检测方法。
  - 设定阈值 φ：若检测分数超过阈值，则触发第二阶段的查询扩充。
  - 论文集成三种SOTA检测器：
    - **SINdex**：通过多个输出间的语义不一致性检测幻觉，分数越高表示幻觉风险越大。
    - **HaloCheck**：基于句子级蕴含关系计算多个响应的信息一致性分数，分数低表示存在冲突。
    - **SelfCheckGPT-NLI**：用DeBERTa-v3-large（MNLI微调）计算矛盾概率，分数越高表示幻觉可能性越大。

- **第二阶段：SAE查询扩充（Query Enrichment）**
  - **特征提取**：给定问答对 (p, r_i)，使用对应的预训练SAE提取问题特征 f_p 和响应特征 f_ri（响应提取时以问题p作为上下文输入），通过激活密度参数 δ 过滤过度通用或无信息的特征：
    - f_p = SAE(p|δ)，f_ri = SAE(r_i|δ, p)
  - **特征差分**：计算响应特有特征集 D_ri = f_ri \ f_p，即响应中不包含在问题上下文中的特征。
  - **语义相似度计算**：用Sentence-BERT模型计算每个特征与问题之间的余弦相似度：cos_dp = cos(Emb(d), Emb(p))。
  - **离群特征剔除**：对余弦相似度分布应用改进的IQR方法（使用Q1和Q2中位数代替传统的Q1和Q3），下界为 Q1 − 1.5 × IQR。低于下界的特征被视为可疑/误导特征并被丢弃，同时指示LLM在后续响应中忽略这些特征。
  - **查询扩充**：强调与问题余弦相似度较高的特征，引导模型注意力聚焦于相关语义。
  - **迭代验证**：重新计算扩充后问题的幻觉检测分数，若仍未达标则重复以上过程（最多3次迭代）。

**复杂度分析**

- 每个被标记响应的总复杂度为 O(r(n log n + nE))，其中 n 为激活特征数（通常很小）、E 为Sentence-BERT前向计算成本、r 为迭代次数（≤3）。
- 整个管线的复杂度为 O(DetectionCost) + O(r(n log n + nE))，DetectionCost 取决于所选检测器。

## 3. 实验设计

**模型**

- **Gemma-2-9b**（Google）
- **Llama-3-8b**（Meta）
- 选择标准：必须拥有可用的SAE及Neuronpedia特征级自动解释。Pythia-70M虽有全部构件但因输出质量过低未纳入。

**数据集（4个跨域基准）**

- **TruthfulQA**：评估模型面对常见误解时的真实回答能力。
- **BioASQ**：生物医学问答，含是/否问题和开放性问题。
- **WikiDoc**：基于医学专业人员平台的医学问答。
- **HaluEval**：ChatGPT用户一般查询的幻觉检测基准。
- 每个数据集随机采样 **400个问题**（沿用Farquhar et al. (2024)的设置）。

**对比方法**

- 基线模型（无任何增强）
- **Simple Enrichment**：在提示中添加通用语句“NOTE - think carefully before answering.”
- **Chain-of-Thought (CoT)** 提示（Wei et al., 2022）
- **SAFE + SINdex** / **SAFE + HaloCheck** / **SAFE + SelfCheckGPT**（三种检测器组合）

**超参数设置**

- 默认阈值：SelfCheckGPT和SINdex使用 φ=0.6，HaloCheck使用 φ=0；SAE激活密度 δ=0.05（在100个TruthfulQA样本上验证得到）。
- 使用10次生成来计算幻觉分数，最多3轮查询扩充。

## 4. 资源与算力

- 硬件：**NVIDIA A100 GPU（80GB VRAM）**。
- 文献**未明确说明**GPU数量、训练时长或总计算量。值得注意的是，SAFE是**无需训练（training-free）**的方法，不涉及模型微调或额外训练阶段，主要计算成本集中在推理期间的SAE特征提取、Sentence-BERT相似度计算和幻觉检测器的多次生成上。工具包括SAELens工具包和Neuronpedia平台。

## 5. 实验数量与充分性

**实验组数**

- **主实验**：2个模型 × 4个数据集 × 3种检测器组合（+ 2个提示基线）= 大量对比组合。
- **超参数分析**：3（φ）× 3（δ）= 9组配置，在100个TruthfulQA样本上验证。
- **消融实验（2组）**：
  - 消融A1（最不相似特征选择）：效果显著下降。
  - 消融A2（最相似特征选择）：效果下降（除BioASQ外）。
  - 消融B（跳过分数阈值对所有问题扩充）：效果显著下降。
- **规模对比实验**：与Gemma2-27b和Llama3-70b大模型进行对比。
- **案例研究**：TruthfulQA、BioASQ、WikiDoc三个数据集的具体样例分析。

**充分性评估**

- **优点**：跨4个领域数据集验证了泛化性；3种检测器验证了模块可插拔性；消融实验验证了各组件（特征选择策略、分数阈值）不可替代性；与更大模型的对比具有较强的实际参考价值。整体实验设计**较为系统和客观**。
- **潜在不足**：主实验每个数据集仅400个样本；超参数验证仅在单个数据集（TruthfulQA）上完成，其他数据集的适用性有待验证；仅评估了两种模型（均为8-9B规模）；未与RAG等外部知识增强方法对比（作者明确排除了此类方法）。

## 6. 主要结论与发现

1. **SAFE普遍有效**：在全部4个数据集上，SAFE相较基线一致地提升了准确率，最高提升达 **29.45%**（Llama3-8b + SINdex on TruthfulQA）。
2. **模型间差异显著**：
   - Gemma2-9b 改进较为温和（0.81%~3.04%）；
   - Llama3-8b 改进幅度更大（3.65%~29.45%），说明SAFE对基线较弱模型的增益更明显。
3. **检测器选择影响效果**：SINdex整体表现最佳，但SelfCheckGPT在HaluEval上对Llama3-8b取得了最高增益（5.67%），体现了SAFE的模块灵活性。
4. **Prompt增强基线效果有限或有害**：Simple Enrichment和CoT在某些数据集上反而降低了准确率（如HaluEval上Simple下降8.2%），SAFE的定向特征引导更具优势。
5. **SAFE可缩小模型规模差距**：Gemma2-9b + SAFE在TruthfulQA、BioASQ、WikiDoc上均**超越**Gemma2-27b；Llama3-8b + SAFE接近Llama3-70b（在TruthfulQA仅差0.7%），但在BioASQ和HaluEval上差距较大。
6. **消融验证关键组件**：A1、A2和B消融均导致性能显著下降，证明：
   - 正确识别并剔除误导特征对性能至关重要；
   - 仅关注最相似特征会过度收窄模型注意力；
   - 基于分数的选择性扩充比无差别扩充更有效。

## 7. 优点

- **无需训练（training-free）**：可直接嵌入现有LLM管线，无需额外微调，部署成本低。
- **模块化架构**：检测器可无缝替换，具有高度的灵活性和可扩展性。
- **创新性**：首次将SAE可解释特征系统性地用于幻觉感知的查询扩充，为幻觉治理提供了新视角。
- **可解释性**：利用SAE提取单义特征，并通过Neuronpedia获得人类可理解的语义解释，增强了方法的透明度和可审计性。
- **跨域验证充分**：覆盖通用问答、生物医学、医学、一般查询等多个领域，展示了方法的泛化能力。
- **代码开源**：已公开代码（GitHub），促进可复现性和后续研究。

## 8. 不足与局限

- **模型依赖性强**：方法要求目标LLM必须提供SAE和可解释特征（如Neuronpedia自动解释），这严重限制了适用模型的范围。目前仅少数开源模型（Llama 3、Gemma 2系列）具备这些条件。
- **语言覆盖有限**：仅支持英文输入，多语言和多模态场景尚未探索。
- **超参数迁移性存疑**：φ和δ在TruthfulQA上确定后直接用于所有数据集，其他数据集的语义分布差异可能影响最优阈值选择。
- **上下文窗口约束**：查询扩充增加输入长度，可能受到上下文窗口限制。
- **输入质量影响**：方法效果受限于输入查询质量，低质量查询仍可能导致次优性能（作者对此有明确声明）。
- **计算开销未完全透明**：虽然复杂度分析表明单轮扩充开销不大，但多次迭代结合检测器的多次生成（10次）带来的总延迟和算力成本未在实验中进行量化。
- **测试规模有限**：每个数据集仅400个样本，且模型规模集中在8-9B，缺少对更大规模模型的验证（尽管有与大模型的对比，但未在更大模型上运行SAFE）。

（完）
