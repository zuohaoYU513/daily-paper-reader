---
title: "Align Documents to Questions: Question-Oriented Document Rewriting for Retrieval-Augmented Generation"
title_zh: 将文档对齐到问题：面向检索增强生成的问题导向文档重写
authors: "Jiaang Li, Zhendong Mao, Quan Wang, Yuning Wan, Yongdong Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.884.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 面向问题的文档重写以提升RAG事实性
tldr: 针对RAG中模型偏好流畅但幻觉化生成内容而忽视事实证据的问题，提出QREAM文档重写框架。该方法通过风格受控改写将检索文档对齐为面向问题的风格，同时保留事实。实验表明该改写能显著提升大模型对检索证据的利用率，增强RAG输出的事实性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl884/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 785, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl884/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1664, \"height\": 1174, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl884/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1567, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl884/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 788, \"height\": 658, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1607, \"height\": 1591, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1716, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl884/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 754, \"height\": 272, \"label\": \"Table\"}]"
motivation: 检索文档的表达方式限制了RAG对事实证据的利用，导致模型偏向流畅但幻觉化的内容。
method: 提出QREAM，采用两阶段风格受控改写，将文档转换为问题导向风格并保留事实。
result: 实验证明QREAM可提升RAG在混合上下文中的事实性与证据利用率。
conclusion: 通过改写检索文档，有效缓解RAG中的幻觉与风格偏置问题。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances the factuality of Large Language Models (LLMs) by incorporating retrieved documents and/or generated context. However, LLMs often exhibit a stylistic bias when presented with mixed contexts, favoring fluent but hallucinated generated content over factually grounded yet disorganized retrieved evidence. This phenomenon reveals that the utility of retrieved information is bottlenecked by its presentation. To bridge this gap, we propose QREAM , a style-controlled rewriter that aligns retrieved documents with a question-oriented style while preserving facts, better for LLM readers to utilize. Our framework consists of two stages: (1) QREAM-ICL , which uses stylistic seeds to guide iterative rewriting exploration; and (2) QREAM-FT , a lightweight student model distilled from denoised ICL outputs. QREAM-FT employs dual-criteria rejection sampling, filtering based on answer correctness and factual consistency to ensure high-quality supervision. QREAM seamlessly integrates into existing RAG pipelines as a plug-and-play module. Experiments demonstrate that QREAM consistently enhances advanced RAG pipelines, yielding up to 8% relative improvement with negligible latency overhead, effectively balancing question relevance with factual grounding.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：Retrieval-Augmented Generation（RAG）系统在增强大语言模型（LLM）事实性方面取得了显著成效，但LLM在同时面对"检索文档"和"生成文档"两类混合上下文时存在**风格偏置（stylistic bias）**问题——模型倾向于优先采用流畅、面向问题组织但可能包含幻觉的生成内容，而非事实正确但组织零散、信息密度低的检索证据。
- **深层原因**：检索到的信息虽然具有事实可靠性，但其**呈现方式（presentation）**严重制约了LLM对其的利用效率。检索文档往往冗余、重复、结构混乱，而LLM生成的内容虽然结构清晰、与问题对齐度高，却存在幻觉风险。
- **研究含义**：作者指出，现有工作大多聚焦于改进检索器（retriever）或压缩器（compressor），却忽略了**文档表达风格**这一关键维度。因此，论文主张通过"面向问题的文档重写"来弥合检索文档与生成文档之间的表达鸿沟，使检索证据既能保持事实正确性，又能以LLM读者更易利用的问答导向风格呈现。

## 2. 论文提出的方法论

### 2.1 整体框架：QREAM

QREAM（**Q**uestion-oriented document R**E**writing for Effective **A**nswering Models）是一个即插即用（plug-and-play）的后处理模块，部署在检索与阅读之间，将原始检索文档重写为事实保留、风格对齐的"问题导向文档"。其核心思想是**将生成模型的角色从"自由生成器"转变为"风格受控、内容受约束的重写器"**。

### 2.2 Stage I：QREAM-ICL（上下文内风格探索）

- **风格种子生成（Stylistic Seeds Generation）**：从训练集中采样M个无关问题，用LLM生成"背景材料式"文档，构成示范样例。关键设计在于使用**不相关问题**作为种子，从而将风格与内容解耦——让重写器模仿结构模式而不受种子内容的干扰。
- **迭代重写（Iterative Rewriting）**：对目标问题q及检索文档R，第一轮直接让LLM在示范指导下重写；后续轮次以上一轮输出的前l个token为基础继续重写，共迭代N轮，产生候选重写集合Cq = {r̃₁, ..., r̃N}。

### 2.3 Stage II：基于双向去噪的蒸馏（Bidirectional Denoising Distillation）

通过**双标准拒绝采样（Dual-Criteria Rejection Sampling）**对ICL候选输出进行筛选，构建高质量训练集训练轻量学生模型QREAM-FT：

- **下游效用检查（Downstream Utility Check）**：将候选重写输入固定QA阅读器，要求预测答案包含真实答案字符串（硬过滤），并以token-level F1作为性能评分Sperf。
- **上游保真检查（Upstream Fidelity Check）**：利用分解式验证方法（类似FactScore），从重写中抽取原子事实，逐条判断其是否被原始检索文档蕴含，计算一致性分数Sfact。
- **总质量分数**：Stotal = ½(Sperf + Sfact)，选择得分最高的候选作为"黄金重写"（golden rewrite）。
- **学生训练**：使用标准化指令模板对Llama-3.2-1B-Instruct进行监督微调，最大化黄金重写的似然。

### 2.4 公式要点

- 风格种子：gi = MGen(TGen(q̂i))
- 迭代重写：r̃n = MRew(TRew(E, r̃n−1[:l], q))
- 一致性分数：Sfact(r̃, rraw) = (1/|F|) Σ I(rraw ⊨ f)
- 总分数：Stotal(r̃) = ½(Sperf(r̃) + Sfact(r̃, rraw))
- 黄金选择：r̃* = argmax Stotal(r̃)，并满足I(a* ∈ â) = 1
- 训练目标：L = −Σ log Pθ(r̃* | TFT(q, rraw))

## 3. 实验设计

### 3.1 数据集与Benchmark

- 四个广泛认可的开放域问答（ODQA）基准，覆盖单跳与多跳推理：
  - **NQ**（Natural Questions，单跳）
  - **TQA**（TriviaQA，单跳）
  - **HotpotQA**（多跳）
  - **2WikiMultiHopQA**（多跳）
- 使用官方划分，采用**Accuracy（Acc）**和**token-level F1**作为评估指标。

### 3.2 对比方法

- **标准RAG管道基线**：仅检索文档、仅生成文档、检索+生成拼接。
- **检索后处理方法**：LongLLMLingua（提示压缩）、CompAct（主动压缩）、RECOMP（抽象压缩）、FaviComp（熟悉度感知融合）。
- **先进RAG框架**：将QREAM集成到Self-RAG和HippoRAG中验证即插即用能力。
- **读者模型**：Llama-3-8B-Instruct和Mistral-7B-Instruct-v0.3作为QA读者；附录中另外用GPT-5 mini进行扩展评估。

### 3.3 实现配置

- 检索器：Contriever-MSMARCO，取top-5段落。
- QREAM-ICL：M=4个风格种子，N=3轮迭代，截断长度l=100。
- QREAM-FT：每个数据集采样1,000个训练样本（共4,000），用Llama-3.2-1B-Instruct微调。

## 4. 资源与算力

- **论文未明确披露GPU型号、数量及训练时长等硬件信息**。
- 从可推断的信息来看：学生模型为Llama-3.2-1B-Instruct（轻量级），训练语料规模为4000条样本（4数据集×1000条），推理阶段单次前向传播的延迟仅0.18s（与标准RAG的0.16s相当），说明其训练与推理成本均控制在较低水平。
- 由于论文未给出具体算力细节，无法精确量化训练所需资源。

## 5. 实验数量与充分性

论文实验设置较为丰富，整体充分性较高：

- **主实验**：在4个数据集×2种读者模型×10+种方法下进行系统性对比（表1），覆盖标准管道与先进框架两种集成场景。
- **消融实验**：验证了双标准过滤策略（无过滤/仅效用/仅保真/双标准）的贡献（表4）；验证了风格种子的必要性、来源设计（无关问题 vs. 自生成）及数量影响（图3）。
- **风格偏置验证**：在Context-Conflicting对抗设置下，验证QREAM能有效缓解LLM读者对生成内容的偏见（表5）。
- **文档质量分析**：提出新颖的sorient风格对齐指标和rinc幻觉率指标，量化对比不同文档类型（表3）。
- **效率分析**：对比ICL与FT的推理延迟（表2）。
- **定性分析**：展示典型案例说明QREAM的优势（表6）。
- **附录补充**：迭代轮数分析、提示词鲁棒性测试（5种变体）、GPT-5 mini扩展实验。

**公平性考量**：论文在多个维度上进行了同读者模型、同检索器的公平对比，且附录中的提示词鲁棒性测试排除了"特定提示工程带来的偶然提升"这一混淆因素。整体实验设计较为客观，但以下方面存在提升空间：训练集来源于各数据集自身的训练部分（存在潜在的数据泄漏风险）、未在更多样的RAG场景（如多文档问答、对话式RAG）下验证。

## 6. 论文的主要结论与发现

- **风格偏置是可缓解的**：通过改变文档呈现方式（而非训练或修改读者模型），能有效改变LLM读者对证据的偏好。在Context-Conflicting设置下，QREAM将Llama-3在NQ-CC上的准确率从19.4%大幅提升至77.4%。
- **QREAM显著提升RAG性能**：QREAM-FT在标准RAG管道上平均准确率达到45.6%（Llama-3读者），较原始检索提升5个百分点；在多跳数据集（HotpotQA、2WikiMQA）上获得约8%的相对提升；与FaviComp等压缩方法相比，风格导向重写能更好保留多跳推理所需的逻辑链条。
- **轻量学生模型可超越教师**：1B参数的QREAM-FT匹配甚至超越了8B教师模型（QREAM-ICL）的性能，归功于双标准拒绝采样的去噪效果——学生学到的是分布更干净的改写模式。
- **即插即用能力得到验证**：集成到Self-RAG和HippoRAG中均获得一致性增益，在GPT-5 mini上也带来持续提升。
- **风格与事实可兼得**：QREAM-FT的风格得分（−1.45）接近生成文档（−1.35），同时幻觉率（9.2%）远低于生成文档（33.7%）甚至低于教师ICL（13.8%）。

## 7. 优点

- **问题定位精准且独到**：从"文档呈现方式"这一被忽视的角度切入RAG改进，识别出LLM读者的"风格偏置"现象，具有较强的洞见性。
- **双向去噪蒸馏机制设计精巧**：下游效用检查保证"答得对"，上游保真检查保证"有依据"，从两方面共同确保训练数据质量，逻辑清晰且有效。
- **风格种子解耦设计新颖**：使用不相关问题作为示范，有效实现风格与内容的解耦，避免种子内容污染重写过程（对比实验证明"自生成种子"反而有害）。
- **效率与效果兼顾**：通过蒸馏将重写延迟从2.41s降至0.18s（约13倍加速），与标准RAG管道几乎无差异，满足实际部署需求。
- **评估体系全面**：除标准Acc/F1外，提出sorient风格对齐指标、rinc幻觉率指标，并在对抗性CC场景下验证风格偏置缓解效果，多维度支撑核心论断。
- **良好的通用性**：在两种开源读者、一种专有读者、两个SOTA RAG框架上均获得一致性增益，证明方法具有跨模型、跨框架的稳健性。

## 8. 不足与局限

- **依赖初始检索质量**：论文自身在Limitations中承认，QREAM假设检索已完成，若检索缺失关键信息或返回大量不相关内容，重写的增益将受到限制。未探索检索与重写的联合优化。
- **数据泄漏风险**：风格种子（QREAM-ICL）和训练数据（QREAM-FT）均来自各数据集自身的训练划分，尽管用于不同目的（种子用于ICL示范、数据用于蒸馏），这种同源采样仍存在评估偏见风险，跨领域泛化性未得到验证。
- **内容信息损失风险**：重写过程本质上是一种有损压缩，对于需要精确数字、时间线或细微语义区别的问题，结构化重写可能导致信息丢失。
- **实验场景覆盖有限**：仅在ODQA任务上进行验证，未涉及多文档摘要、代码检索、事实验证等RAG的其他典型应用场景；风格种子数量、迭代轮数等超参数在更大规模上的敏感性未被充分探索。
- **算力信息不透明**：未报告具体的GPU型号、训练时长、能耗等资源信息，降低了可复现性评估的完整性。
- **对LLM-as-judge的依赖**：事实一致性验证依赖LLM进行原子事实抽取和文本蕴含判断，其本身存在错误传播风险，且未讨论这一验证环节的成本与替代方案。

（完）
