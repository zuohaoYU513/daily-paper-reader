---
title: "UniRAG: Unified Query Understanding Method for Retrieval Augmented Generation"
title_zh: UniRAG：面向检索增强生成的统一查询理解方法
authors: "Rui Li, Liyang He, Qi Liu, Zheng Zhang, Heng Yu, Yuyang Ye, Linbo Zhu, Yu Su"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.693.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 面向RAG的统一查询理解
tldr: 针对RAG中查询增强与编码分离导致信息共享不足和累积误差的问题，提出UniRAG统一框架。该方法利用仅解码器大模型联合完成查询增强与编码，消除任务分离。实验表明UniRAG在多种查询场景下提升了RAG的性能，同时缓解了大模型幻觉与知识更新滞后问题。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long693/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long693/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1658, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long693/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1644, \"height\": 506, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long693/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 786, \"height\": 376, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long693/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1600, \"height\": 794, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long693/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long693/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long693/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 827, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long693/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 759, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long693/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 366, \"label\": \"Table\"}]"
motivation: 现有RAG查询增强任务分离且难以选择最优策略，影响性能并加剧幻觉。
method: 使用解码器大模型统一执行查询增强与编码，共享信息并避免累积误差。
result: 实验显示UniRAG在多个复杂查询场景下RAG性能显著提升。
conclusion: 为RAG查询理解提供统一高效框架，助力减少幻觉。
---

## Abstract
Retrieval-Augmented Generation (RAG) technology effectively addresses the issues of knowledge update lag and hallucinations in large language models (LLMs) by integrating internal and external knowledge. Existing query augmentation methods improve RAG’s performance in handling complex queries but face two key challenges: (1) the separation of query augmentation and encoding tasks, which hinders information sharing and introduces cumulative errors, and (2) the difficulty of selecting the optimal augmentation strategy for different scenarios. In this work, we propose UniRAG, a unified framework for query understanding in RAG. UniRAG employs a decoder-only LLM to jointly perform query augmentation and encoding, eliminating task separation. To facilitate adaptive query augmentation, we categorize existing techniques into query paraphrasing, query expansion, and query abstraction. Our model learns to select the optimal augmentation strategy based on user queries, leveraging retrieval and generation outputs as feedback. Experimental results show that UniRAG significantly outperforms traditional query augmentation methods in five knowledge-intensive benchmark tasks in both closed and open domain question answering.

---

## 论文详细总结（自动生成）

# UniRAG：面向检索增强生成的统一查询理解方法

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）在预训练中积累了海量知识，但仍面临知识更新滞后和生成幻觉（hallucination）等固有挑战。检索增强生成（RAG）通过整合参数化与非参数化知识，成为缓解上述问题的标准方法。
- **核心问题**：现有查询增强方法在提升RAG处理复杂查询能力的同时，面临两个关键挑战：
  - **任务分离问题**：查询增强与查询编码被建模为相互独立的模型或阶段，限制了信息共享，并可能引入累积误差（cumulative errors）。
  - **策略选择困难**：不同查询增强技术在不同场景下表现差异显著（如PopQA上原始查询反而最优，而TriviaQA上HyDE最优），如何为特定查询选择最优增强策略缺乏有效方案。
- **整体含义**：本文提出UniRAG，一个统一的RAG查询理解框架，通过单一解码器LLM联合完成查询增强与编码，并自适应地为每个查询选择最优增强策略，从而提升RAG系统在各类知识密集型任务上的整体性能。

## 2. 论文提出的方法论

### 2.1 核心思想

- 使用一个**仅解码器（decoder-only）LLM**统一执行两阶段任务：查询增强（query augmentation）与查询编码（query encoding），消除传统流程中的任务分离。
- 将现有查询增强技术划分为三类，并训练模型根据用户查询自适应选择最优策略：
  - **查询改写（Query Paraphrasing）**：消除歧义与模糊表达。
  - **查询扩展（Query Expansion）**：基于HyDE生成假设性文档。
  - **查询抽象（Query Abstraction）**：基于Step-Back Prompting抽象出更高层概念的问题。
  - 额外允许 **"不增强"（<Original>）** 选项。

### 2.2 两阶段训练流程

**阶段一：查询增强训练（Query Augmentation Training）**

- **数据合成**：从多个知识密集型QA和检索数据集（Natural Questions、MS MARCO、BoolQ、NarrativeQA、Dolly15k、SQuAD）构建种子数据集，使用GPT-4o-mini应用三种增强策略生成增强查询。
- **反馈信号收集**：
  - **检索器反馈**：基于倒数排名（reciprocal rank）计算检索反馈分数 s_ret(x) = 1/rank_x。
  - **生成器反馈**：将查询与检索文档拼接后送入生成器，计算生成答案的对数概率 s_gen(x) = log p_G(r|C(x))。
- **数据过滤**：丢弃增强查询反馈分数低于原始查询的样本；若原始查询本身最优，则保留"不增强"样本。最终获得263K条指令微调数据（含105K有效反馈信号）。
- **联合训练目标**（L_enh = L_sel + L_gen）：
  - **策略选择损失 L_sel**：将检索器和生成器反馈分数映射到动作词表分布，通过KL散度对齐模型预测的增强策略选择概率。
  - **增强查询生成损失 L_gen**：基于选定的策略，以标准下一词预测损失监督增强查询的生成。

**阶段二：查询编码训练（Query Encoding Training）**

- 将原始查询、增强策略及增强查询组合成指令格式，并添加`<EOS>`标记提取嵌入。
- 使用**InfoNCE对比学习损失** L_ret 优化查询与文档的匹配，使正样本对的相似度高于负样本对。
- 数据集中加入挖掘的难负样本（hard negatives）以提升检索性能。

### 2.3 推理解码策略

- **默认解码（Default）**：通过约束解码生成动作token，选择概率最高的增强策略并贪心生成增强查询。
- **阈值解码（Threshold-based）**：根据`<Original>`概率与最大增强策略概率的比值与阈值γ比较，动态决定是否执行增强，平衡精度与计算成本。
- **树状解码（Tree-based）**：生成所有概率不低于`<Original>`的增强动作，通过beam search探索多条增强路径，最终使用**倒数排名融合（RRF）**合并多条查询的检索结果，进一步提升召回率。

## 3. 实验设计

### 3.1 数据集与Benchmark

覆盖**封闭域**和**开放域**共5个知识密集型基准数据集：

| 数据集 | 类型 | 规模 | 任务描述 |
|--------|------|------|----------|
| PopQA | 开放域 | 1,399 | 长尾实体的事实性问答 |
| TriviaQA-unfiltered | 开放域 | 11,313 | 常识问答（验证集+测试集） |
| PubHealth | 封闭域 | 3,610 | 公共健康事实核查 |
| ARC-Challenge | 封闭域 | 948 | 科学考试多项选择推理 |
| TimeQA | 开放域 | 5,226（测试） | 时间敏感型复杂问答 |

### 3.2 对比方法（Baselines）

- **无检索基线**：Zero-shot Prompting。
- **标准检索基线**：使用原始查询直接检索（Original Query）。
- **三种单策略增强方法**：
  - Query Paraphrase（基于Ma et al., 2023）
  - HyDE（Gao et al., 2023a）
  - Step-back Prompting（Zheng et al., 2023）
- **生成器**：统一使用Llama-3-8B-Instruct、Llama-3-70B-Instruct和GPT-4o-mini三种LLM作为生成器，验证模型无关性。
- **检索器**：使用Contriever-MS MARCO作为固定检索器。

### 3.3 评估方式

- 使用准确率（accuracy）作为评估指标。
- 不强依赖严格文本匹配，而是判断模型生成结果是否包含标准答案。

## 4. 资源与算力

- **硬件**：4张NVIDIA A100 GPU，每张80GB显存。
- **训练配置**：
  - 查询增强指令微调阶段：3个epoch，batch size 256，峰值学习率2e-5，线性衰减+3% warmup，最大token长度512。
  - 查询编码对比学习阶段：1个epoch，最大token长度256，温度参数τ=0.01。
  - 采用LoRA（rank=16）、DeepSpeed ZeRO-3、BFloat16精度和FlashAttention2加速。
- **推理加速**：使用vLLM。
- **未明确说明的部分**：论文**未明确报告**两个训练阶段的具体训练时长（wall-clock time），也未说明合成数据生成（GPT-4o-mini API调用）的总成本。

## 5. 实验数量与充分性

### 实验组数统计

- **主实验（表1）**：5个数据集 × 3种生成器模型 × 6种方法（含UniRAG），共90组实验对比。
- **消融实验（表2）**：共6组消融变体，涵盖两个阶段：
  - 查询增强阶段：仅检索器反馈、仅生成器反馈、拒绝采样（rejection sampling）策略。
  - 查询编码阶段：使用Contriever检索、跳过增强训练（w/o Lenh）、不加入增强查询数据（w/o Extra Data）。
- **分析实验**：
  - 解码策略性能与延迟对比（阈值解码 vs 树状解码，图3a）。
  - 合成数据规模影响（5K/10K/20K/50K/100K vs 263K全量，图3b）。
  - 策略选择准确率验证（2.1K验证集上的win/tie/lose对比，图4）。

### 充分性与公平性评估

- **充分性**：实验覆盖两个域（开放域+封闭域）、三种不同规模的生成器模型，验证了方法的普适性；消融实验系统性地验证了各模块的贡献。
- **公平性**：与基线方法统一使用相同生成器和检索器，提示模板保持一致（来自各基线官方实现），设置合理。
- **可改进空间**：论文未报告多次运行的方差/显著性检验；未与更多近期RAG增强方法（如Self-RAG、RRR等）进行端到端对比；消融实验中训练数据规模的影响测试仅覆盖两个数据集。

## 6. 论文的主要结论与发现

- **UniRAG持续优于所有单策略基线**：在5个基准数据集和3种生成器设置下，UniRAG均取得最优性能，例如PopQA上较最优基线提升约5个百分点，ARC-Challenge上提升约3-4个百分点。
- **统一框架优势明显**：将查询增强与编码集成于同一模型，通过信息共享减少累积误差，优于独立的"增强+编码"两阶段方法。
- **自适应策略选择有效**：不同数据集受益于不同增强策略（PopQA原始查询最优、TriviaQA和PubHealth适用HyDE），UniRAG能动态选择最合适策略，并在超过90%的情况下提升检索性能。
- **检索器与生成器反馈互补**：消融实验表明生成器反馈比检索器反馈对策略选择更重要，融合两者效果最佳；设计精细的KL散度损失优于简单的拒绝采样。
- **解码策略灵活适配**：树状解码性能最优但延迟最高；阈值解码可通过调整γ权衡性能与效率，适应不同应用需求。
- **数据规模效应明显**：训练数据从5K增至263K时，模型性能持续提升，提示进一步扩大合成数据规模可能带来更多增益。

## 7. 优点

- **统一建模视角新颖**：首次将查询增强与查询编码整合到单一decoder-only LLM中，突破了传统两阶段流水线的局限，减少了信息碎片化。
- **自适应增强策略**：不同于静态选择单一增强方法，UniRAG基于检索器和生成器的反馈信号，为每个查询动态决策最优策略（包括"不增强"），设计合理且实用。
- **即插即用兼容性**：可灵活集成不同LLM，支持自定义解码算法（阈值/树状），能根据下游应用需求调整增强频率。
- **数据质量把控严谨**：包含反馈信号收集、数据过滤（仅保留有正向增益的增强样本）、难负样本挖掘等环节，确保训练数据质量。
- **实验验证全面**：在5个知识密集型数据集、3种生成器（含更强的70B模型和GPT-4o-mini）上验证了方法的鲁棒性与模型无关性；消融实验设计系统，分析实验（解码策略、数据规模、策略准确性）覆盖多个角度。

## 8. 不足与局限

- **依赖预定义增强策略**：论文仅涵盖三种增强策略（改写、扩展、抽象），对更广泛或更细粒度的增强方法（如多轮重写、结构化查询等）缺乏扩展性验证，可能无法泛化到所有领域或用户意图。
- **未报告训练时长与计算成本**：论文未说明两阶段训练的具体耗时和GPT-4o-mini数据合成的API成本，限制了读者对部署可行性的全面评估。
- **对检索质量的依赖**：UniRAG虽提升了查询理解，但整体性能仍受检索文档质量制约；在低资源或高度专业化领域，检索噪声可能削弱最终生成效果。
- **反馈信号偏差风险**：检索器反馈和生成器反馈均由固定模型（Contriever、Llama-3-8B-Instruct）提供，可能引入模型偏差；合成数据由GPT-4o-mini生成，同样可能继承其内在偏见。
- **数据集域外泛化待验证**：实验集中于问答和事实核查类任务，对对话检索、代码检索、多模态检索等其他RAG应用场景缺乏验证。
- **统计学检验不足**：未报告多次运行的标准差或显著性检验结果，对方法稳定性的论证略显不足。

（完）
