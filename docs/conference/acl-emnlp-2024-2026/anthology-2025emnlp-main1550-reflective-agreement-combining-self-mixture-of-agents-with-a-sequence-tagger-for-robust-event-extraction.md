---
title: "Reflective Agreement: Combining Self-Mixture of Agents with a Sequence Tagger for Robust Event Extraction"
title_zh: 反射式一致性：结合智能体自混合与序列标注的稳健事件抽取
authors: "Fatemeh Haji, Mazal Bethany, Cho-Yu Jason Chiang, Anthony Rios, Peyman Najafirad"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1550.pdf"
tags: ["query:evidence-qa"]
score: 7.0
evidence: 生成式与判别式混合的稳健事件抽取，抑制LLM幻觉
tldr: 事件抽取常面临判别式模型召回不足、生成式大模型幻觉频发的问题。ARIS提出一种自混合智能体与判别式序列标注器协同的反射式推理系统，将结构化知识约束与生成模型的语义灵活性结合，以更好识别触发词、事件类型和论元。该系统在保持高精度的同时提升对罕有事件的召回，并有效减少生成式事件抽取的不一致与幻觉输出。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1550/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1638, \"height\": 695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1550/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 1159, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1550/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 822, \"height\": 944, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main1550/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 821, \"height\": 1158, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 594, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1656, \"height\": 600, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 820, \"height\": 852, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 853, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1502, \"height\": 842, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 809, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1034, \"height\": 628, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 772, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main1550/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1667, \"height\": 827, \"label\": \"Table\"}]"
motivation: 判别式事件抽取模型精度高但召回不足，生成式大模型召回好却常产生幻觉与输出不一致。
method: 提出ARIS，结合判别式序列标注器与自混合多智能体反射机制，用结构化约束平衡生成结果的精确性。
result: 在事件抽取任务上提升了罕见事件召回，并降低生成式事件预测的不一致和幻觉。
conclusion: 混合判别与生成范式可为稳健事件抽取提供更可靠的工程路线。
---

## Abstract
Event Extraction (EE) involves automatically identifying and extracting structured information about events from unstructured text, including triggers, event types, and arguments. Traditional discriminative models demonstrate high precision but often exhibit limited recall, particularly for nuanced or infrequent events. Conversely, generative approaches leveraging Large Language Models (LLMs) provide higher semantic flexibility and recall but suffer from hallucinations and inconsistent predictions. To address these challenges, we propose Agreement-based Reflective Inference System (ARIS), a hybrid approach combining a Self Mixture of Agents with a discriminative sequence tagger. ARIS explicitly leverages structured model consensus, confidence-based filtering, and an LLM reflective inference module to reliably resolve ambiguities and enhance overall event prediction quality. We further investigate decomposed instruction fine-tuning for enhanced LLM event extraction understanding. Experiments demonstrate our approach outperforms existing state-of-the-art event extraction methods across three benchmark datasets.

---

## 论文详细总结（自动生成）

好的，我已经仔细阅读了您提供的论文内容。以下是根据您的要求生成的结构化中文总结：

---

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：事件抽取（Event Extraction, EE）旨在从非结构化文本中自动识别事件触发词、事件类型和事件论元及其角色，是信息检索、知识图谱构建等应用的基础。
- **技术矛盾**：现有方法主要分为两类：
    - **判别式方法**（如基于Transformer的序列标注器）：具有高精度和结构一致性，但在处理少见或细微事件时召回率不足。
    - **生成式方法**（基于LLM）：语义理解灵活、覆盖广、召回率高，但容易产生 **幻觉（hallucination）** 和输出不一致的问题。
    - 现有的多智能体辩论方法虽有前景，但缺乏结构化约束，可能放大幻觉，且计算开销大、推理时间不稳定。
- **研究意义**：本文旨在解决判别式和生成式方法之间的权衡问题，提出一个系统化的混合框架，以兼顾**判别式的精确性**与**生成式的语义灵活性**。

## 2. 论文提出的方法论

- **核心思想**：提出 **ARIS（Agreement-based Reflective Inference System）**，一个混合事件抽取框架，通过结构化共识检测、基于置信度的过滤和反射推理机制，系统性地整合生成式LLM与判别式序列标注器的互补优势。

- **关键技术细节与流程**（大致分为五个阶段）：
    1. **分解式指令微调（Decomposed Instruction Fine-Tuning）**：
        - 提出将事件抽取任务分解为若干子任务进行微调，而不是标准的端到端微调。
        - 子任务包括：完整事件结构建模、触发词识别与分类、论元提取与角色分配以及二元正确性判别等。
        - 目标是让LLM逐步掌握事件抽取的完整推理链。
    2. **自混合多智能体（Self Mixture-of-Agents, Self-MoA）**：
        - 使用同一LLM在高温（如t=0.9）下运行 **n=10个** 独立实例（Agents），生成多样化的候选事件预测集合。
        - 结果经过规则清洗（过滤无效span、按位置排序）后得到初步集合 $E_{SMoA}(x)$。
    3. **共识检测（Consensus Detection）**：
        - 将Self-MoA的预测与判别式序列标注器（TagPrime）的预测进行交集匹配 $E_{con}(x) = E_{SMoA}(x) \cap E_{S}(x)$。
        - 当触发词或论元的文本跨度重叠超过阈值时，视为达成共识。
    4. **置信度过滤（Confidence-based Filtering）**：
        - 对于不一致的预测 $E_{dis}(x)$，分别计算其置信度。
        - 对于Self-MoA中的预测e，置信度为预测该事件的Agent比例：$C_{SMoA}(e) = \frac{|A_e|}{n}$。
        - 对于序列标注器，置信度来自softmax分数：$C_{S}(e) = \max_{t \in T_{tags}} P_S(t | span(e), x)$。
        - 高置信度的不一致预测会被保留（尤其是TagPrime的），低置信度的预测会被丢弃。
    5. **反射推理模块（Reflective Inference）**：
        - 对于置信度介于高/低阈值之间的模糊预测，将其与原文一起输入给（已微调的）LLM。
        - 设计结构化Prompt，让LLM对候选触发词或论元进行二元判定（例如，判断是否为触发词、论元是否正确），如同一个“验证器”。
        - 反射模块的最终输出用于整合产生的最终预测集：$E_{final}(x) = E_{con}(x) \cup E_{high\_conf}(x) \cup E_{reflected}(x)$。

## 3. 实验设计

- **数据集与场景（Benchmark）**：
    - 使用了三个不同领域的基准数据集，并遵循 **TextEE** 标准的 "split1" 划分：
        - **CASIE**：网络安全新闻，长段落，5种事件类型。
        - **M2E2** 仅使用文本部分：多媒体新闻，短文本（1-2句话），8种事件类型。
        - **MLEE**：生物医学领域，长段落，29种事件类型（最多样化）。
- **评价指标**：采用微型F1分数（micro F1），分别评估**触发词识别、触发词分类、论元识别、论元分类**四个子任务。
- **对比方法（Baselines）**：
    - **判别式方法**：TagPrime（基于RoBERTa的序列标注器）。
    - **生成式LLM方法**：DEBATE-EE（多智能体辩论）、MMUTF（模板填充）等。
    - **自建Baselines**：基于Llama-3.1-8B-Instruct和Phi-3-small-8k-instruct，对比了：
        - One-Shot（无微调）
        - FineTuned-EE（标准端到端微调）
        - FineTuned-DEE（本文提出的分解式微调）
        - 最后是完整的ARIS系统。

## 4. 资源与算力

- **文中明确说明（附录G）**：
    - **LLM微调**：采用LoRA进行参数高效微调，运行在单个GPU上。
        - CASIE 和 MLEE：使用 **NVIDIA H200 (140GB)**。
        - M2E2：使用 **NVIDIA A100 (80GB)**。
    - **训练时长**：
        - CASIE（8小时），MLEE（3小时），M2E2（<1小时）。
    - **序列标注器（RoBERTa）**：训练细节给出了batch size和epochs（如CASIE ED batch size 16, epochs 10；EAE batch size 4, epochs 90等），但**未明确提及使用的GPU型号和训练具体时长**。
    - **Self-MoA推理开销**：文中提到需要运行多个LLM实例，这会显著增加推理时间和计算资源，但未量化具体数值。

## 5. 实验数量与充分性

- **实验数量**：
    - 主实验（表1）：在3个数据集上，使用了2种基础模型（Llama, Phi-3），并与多种主流基线（TagPrime, DEBATE-EE, MMUTF, One-Shot等）进行对比。
    - 消融实验（表2）：在 *3个数据集上取平均*，对比了完整ARIS与“ARIS w/o TagPrime”，以及与单独Self-MoA、单独的TagPrime的差异。
    - 超参数敏感性实验（表3）：考察了不同温度（0.1, 0.6, 0.9）对系统性能的影响。
    - 此外还有关于分解式微调增量的分析（附录F.3）以及具体的Pipeline案例（附录H）。
- **充分性评估与客观性**：
    - **优点**：覆盖了多个差异显著的领域（网络安全、新闻、生物医学），且对比了多种不同的SOTA架构和策略，跨模型的评估也增强了泛化性。
    - **不足**：**消融实验不够彻底**。虽然明确了TagPrime的贡献，但没有独立验证共识检测、置信度过滤和反射模块各自的贡献值，或是在没有TagPrime情况下（但保留反射）的影响。
    - **风险**：置信度阈值是数据集特定的，需要在验证集上搜索，可能存在过拟合验证集的风险，跨领域的零样本泛化能力未知。
    - **偏差**：M2E2是多模态数据集，论文声明只用了文本，这可能导致与此前报道的SOTA结果（如MMUTF）不完全可比。

## 6. 论文的主要结论与发现

- ARIS在三个基准数据集的所有指标上**始终优于**现有最佳方法。
- 在论元提取任务上的改进尤为显著，例如在MLEE数据集上，Phi-3版本的ARIS在论元分类F1上比TagPrime高出超过10个百分点。
- **分解式微调**显著优于标准端到端微调，证明了其教授LLM复杂结构推理的有效性。
- **温度鲁棒性**：尽管温度对单独的Self-MoA性能影响巨大，但完整的ARIS系统在不同温度下表现稳定，证明共识机制、置信度过滤和反射模块能有效消除采样随机性带来的影响。
- 通过结合生成式的灵活性和判别式的精度，ARIS能够在不牺牲高精度的情况下提升召回，并抑制幻觉。

## 7. 优点（亮点）

- **新颖的混合思路**：ARIS逻辑清晰，将“生成”与“判别”的结合形式化，构建了一套完整的从共识到过滤再到反思的闭环，降低了幻觉风险。
- **放弃复杂辩论，改用共识与反思**：相比多智能体辩论（Debate），ARIS通过投票和单步验证（Reflection）解决了分歧，机制更简单，推理路径更可控。
- **分解式教学**：在微调阶段引入细粒度的任务分解是一个亮点，让LLM对事件抽取的链条有更深刻的理解。
- **温度稳定性**：对温度不敏感是一个工程上的重要优势，降低了在实际部署中调参的不确定性。

## 8. 不足与局限

- **计算开销大**：需要运行多个LLM Agent实例，且需要训练判别式模型和LLM（即使使用LoRA），相比传统判别式方法训练和推理成本很高。
- **反射机制的极限**：反射模块对模糊案例的解决能力存在天花板，对于最难识别的样本可能依然无法纠正（论文在Limitations中也提到了这一点）。
- **消融不充分**：未能分解性的展示共识检测、置信度过滤、反射推理各环节的独立贡献。
- **实验覆盖有限**：仅评估了三个特定领域的英文数据集（且M2E2未使用视觉信息），缺乏对跨领域泛化的验证，文中也提及未来可研究联合训练。
- **阈值敏感性**：针对不同数据集和温度设定了特定的阈值（主要是从验证集上选取），最优阈值的选取规则未详细扩展，存在对验证集过拟合的风险。
- **基线的局限性**：对比的最强判别式模型为RoBERTa-based TagPrime，未与其他更新的开源判别模型（如基于大模型的少样本微调）进行对比。

（完）
